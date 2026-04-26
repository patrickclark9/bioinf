---
id: old 2
aliases: []
tags: []
---

# Applicazioni di NGS

Alcune applicazioni delle piattaforme NGS sono:
## Sequenziamento DNA
- Risequenziamento Genomico (SNP, GWAS)
- De-novo sequencing
- Identificazioni di varianti strutturali del genoma
- Interazioni della cromatina 3D
- Epigenomica (stato cromatinico e metilazione)
- Metagenomica (analisi tassonomica di campioni ambientali)
## Sequenziamento RNA
- Analisi qualitativa e quantitativa del trascrittoma
- Identificazione e caratterizzazione di miRNA e altri ncRNA
- RNA Editing
- Metatrascrittomica (analisi funzionale di campioni ambientali)

## Genome Resequencing

Consiste nel sequenziare nuovamente l'intero genoma di una specie di cui si ha un genoma di reference, permettendo l'indetificazione di varianti come SNP, indel, e varianti strutturali

## Whole Genome Sequencing
Processo in cui si va a determinare l'intera sequenza del DNA di un genoma di un organismo , incluso cromosomale e mitocondriale.


## Target Enrinchment

L'arricchimento consiste nel catturare, o arricchire, specifiche regioni di interesse, che possono essere esoni, ncRNA, o specifici geni, prima del sequenziamento.
Le tecniche presentate sono utilizzate per l'arricchimento di DNA genomico, quindi non utilizzate per l'arricchimento di ncRNA. 
Per ncRNA si utilizzano tecniche differenti data la loro complessa e diversificata struttura.

### Array Hybridization
Approccio che consiste nell'utilizzare probe, piccoli olignonucleoitidi sintetici,  su un vetrino (array). DNA genomico viene introdotto sull'array, dove DNA target legherà i probe complementari sull'array, mentre il DNA non target viene rimosso. Il DNA catturato viene poi sequenziato
### In Solution Hybridization
Il metodo più comune utilizzato oggi. I probe vengono biotinilati (taggati), ed inseriti insieme al DNA genomico in soluzione. Dopo ibridizzazione, vengono utilizzati bead con streptavidina che lega la biotina, tirandosi i probe target in complesso con DNA di interesse, permettendo di rimuovere il resto del materiale genomico. 

### Molecular inversion probe
Oligonucleotide a singolo filamento prodotto cosi che le terminazioni siano complementari al DNA target. Quando si lega il probe, si inverte e forma un cerchio attorno al target. Una reazione di gap-filling e ligazione chiudono il cerchio. Solo i probe circolarizzati vengono sottoposti a PCR.
![[Pasted image 20260423183843.png]]

## Varianti strutturali
Varianti strutturali identificabili da seconda generazione:
- Mutazioni puntiformi
- Indel
- Delezioni omozigoti -> Copy Number variation
- Delezioni emizigoti -> Copy Number Variation
- Gain ->  Copy number Variation
- Punto di breakpoint di Traslocazioni
- Patogeni

Si sequuenziando e allineando i dati contro un genoma di riferimento al fine di creare un file BAM pronto per essere utilizzato. Nel variant calling di Varianti ereditarie, si fa utilizzo di 3 BAM, proband BAM, Madre BAM e Padre BAM. Si fa un joint-variant calling, in cui vengono analizzate SNV/Indel/SV/CNV. Segue un filtro di rimozione di artefatti, e conferma con una review manuale.
Per de Novo alterazioni bisogna rimuovere anche i falsi positivi.
Variant calling si può fare anche per varianti somatiche, utilizzando un BAM per Tumore ed un altro per controllo (normale).
Si cercano SNV/Indel/SV/CNA somatiche, si rimuovono gli artefatti, e si conferma manualmente che sia una variante.
Linee guida e standard per l'identificazione di varianti genetiche sono ancora in sviluppo. WES e WGS producono molti dati su numerose varianti genetiche, la maggior parte delle quali, nel contesto di uno studio su una particolare malattia, non sono rilevanti, dato che non hanno effetto funzionale sulle proteine o a livello sistemico. Da notare è che tutti presnetiamo un gran numero di varianti genetiche ereditarie e de novo mutazioni, ma una piccola frazione di queste effettivamente impatta la funzione proteica o sistemica (ad esempio mutazioni non senso).
L'annotazione di varianti ha come obiettivo produrre metadati ausiliari per variant call putative grezze filtrate per qualità, al fine di approfondire le varianti che probabilmente hanno un impatto funzionale o sistemico.


## ChIPSeq
1. Cross-linking con formaldeide e grandi quantità di DNA
	1. I crosslink sono effettuati tra la proteina ed il DNA, ma anche tra RNA e altre proteine
2. Si frammenta la cromatina, rompendola e così ottenendo pezzi ad alta qualità di DNA per l'analisi ChIP. Questi frammenti possono essere tagliati anche al di sotto di 500bp, per massimizzare il risultato del genome mapping
3. Il terzo step è chiamato Immunprecipitazione, dove si utilizza un anticorpo contro la proteina di interesse, a cui segue un processo di incubazione e centrifiguzaione in modo da ottenere l'immunoprecipitazione. Questo step permette anche la rimozione di siti di binding non specifici
4. Si recupera il DNA e lo si purifica. Per effetto inverso sul cross-link DNA-proteina per separarle e per estrarre e purificare il DNA
5. Lo step finale consiste nell'analisi, utilizzando qPCR, ChIP-on-chip o ChIP sequencing. Vengono poi ligati adattatori oligonucleotidici ai piccoli frammenti di DNA legati alla proteina di interesse per prepararlo a sequenziamento massivo. 
L'ultimo step dipende dalla strategia di sequenziamento. Si effettua la classica end-repair e ligazione seguita da PCR (cluster o emPCR) per sequenziamenti di seconda generazione.
Si attacca una coda di poli(A) per Helicos o altro in base al sequenziatore.
Dopodichè allineamo le short read.
I tag sono le short read generate dai frammenti di DNA immunoprecipitato.
Se ne studia quindi la distribuzione, andando a ricercare i picchi tramite algoritmi di peak-calling (MACS) al fine di distinguere segnali di binding da rumore di fondo.
Il profilo viene generato da tag combinati, quindi per esempio ogni locazione mappata viene estesa con un frammento di dimensione stimata.
L'identificazione dei picchi può essere fatta su qualsiasi profilo


## RNA-seq
RNA-seq è una procedura sperimentale per generare read di sequenza derivate dall'intera molecola di RNA.
Può essere usata per costruire una mappa completa del trascrittoma tra tutti i tipi cellulari, perturbaazioni e stati.
L'RNAseq facilita la scoperta di nuovi trascritti, identificando geni oggetto di splicing alternativo e la scoperta di espressione allele-specifica.

Per RNA-seq, l'RNA totale viene estratto dal materiale scelto (cellula o tessuto). Sottoinsieme di molecole di RNA vengono ottenutte tramite procedure di arricchimento, quali poli(A) selection per arricchire trascritti con poli(A), o ribodepletion, quindi la rimozione dell'RNA ribosomale. L'RNA viene poi convertito in cDNA da una trascrittasi inversa e adattatori di sequenza vengono ligati alle terminazioni dei frammenti di cDNA. Dopo amplificazione con PCR, la libreria di RNA-seq è pronta per essere sequenziata

Dividiamo la trascrittomica in:
- Bulk -> Tutto l'RNA proveniente da tutte le cellule
- Single Cell -> Isolare l'RNA proveniente per ogni singola cellula
- Spaziale -> Informazioni aggiuntive sulla posiziona spaziale 3D del trascritto
- e altre man mano che vengono sviluppate

### Bulk
Dalla bulk:
1. Allineamo le read
2. Quantifichiamo
Possiamo effettuare:
- Espressione differenziale
- Analisi ncRNA
- Analisi di isoforme di splicing
- Analisi di eventi di RNA editing
- Eventi di poliadenilazione alternativa
#### Tipi di Read
Le read possono essere single o pair-end, dove le pair end sono coppie di read in cui una forward ed una in reverse dello stesso trascritto, con un dato numero di nucleotidi in overlap.
Le read in single-end sono read individuali senza una controparte in reverse della stessa regione.

#### Tipi di librerie
Le librerie di mRNA possono essere:
- Stranded
- Unstranded
I protocolli stranded + e stranded - preservano l'informazione riguardante lo strand da cui l'mRNA si è originato, informazione che viene persa nel protocollo unstranded.
In una libreria stranded forward, le read mapperanno principalmente sullo stesso strand del gene. In reverse, mapperanno principalmente sul filamento opposto.
Una libreria unstranded invece presenterà read che mapperanno indipendentemente dall'orientamento del gene, quindi si otterrà una distribuzione di circa 50% forward e 50% reverse.
Librerie stranded si ottengono degradando il secondo strand oppure rimuovendo l'RNA, prima di PCR e sequenziamento.
Per una first strand library si sintetizza il secondo strand utilizzato dUTP. Il dUTP viene rimosso per digestione con uracil-DNA-glicosilasi.
Una second strand library si ottiene rimuovendo l'RNA dopo la sintesi del filamento template.

### Read Mapping
Per allineare le sequenze contro il genoma di interesse, bisogna utilizzare un allineatore spliced-aware, quali STAR, TopHat2, SOAPSplice, BowTie ecc....
Questi usano due approcci generali:
- Exon First Approach: Si mappano read continuativamente al genome utilizzando aligner unspliced. Poi le read non mappate vengono divise in segmeni più corti ed allineate indipendentemente. Sono molto efficienti quando solo una piccola porzione di read richiedono il secondo step, che è computazionalmente dispendioso
- Seed Extend Approach: Si utilizza un approccia stile BLAST, in cui si divide in kmer le read sequenziate, chiamati seed. Si utilizza un FM-index per trovare ogni possibile locazione dove un seed combacia al reference. Una volta trovato il seed, le regioni candidate vengono esplorate con metodi a sensibilità più elevata, quali Smith-Waterman o l'estensione iterativa con merging dei seed iniziali per determinare l'esatto allineamento spliced per la read

In media un seed-extend ci mette 8 volte più tempo di un exon-first, che produce 1.5 spliced read aggiuntive. Un potenziale svataggio dell'exon first è ad esempio che read esoniche mapperanno sia su un gene sia su un pseudogene, preferendo il gene per la mancanza di mutazioni, ma una read spliced potrebbe comunque essere assegnata al pseudogene poichè può apparire come esonica, impedendo l'esplorazione di un allineamento splice ad alto score

## STAR

Per ogni read che STAR allinea, cerca la più lunga sequenza che corrisponde esattamente in una o più locazioni sul genoma di riferimento. Queste sequenze corrispondenti sono chiamate Maximal Mappable Prefixes (MMPs).
STAR ripete la ricerca solo per la porzione della read non mappata per trovare la prossima più lunga sequenza che ha corrispondenza nel genoma di riferimento, o il prossimo MMP.
La ricerca sequenziale di solo le porzioni non mappate raccoglie l'efficienza dell'algoritmo STAR. STAR uitlizza un uncompressed Suffix Array per ricercare velocemente MMP contro i genomi di riferimento più grandi.
Se non viene trovato un match esatto per ogni parte della read per mismatch o indel, allora l'MMP precedente  viene esteso.
Se l'estensione non ha un buon allineamento, allora la porzione a bassa qualità o l'adattatore viene soft-clipped.
I seed separati vengono riuniti per creare una read completaprima clusterizzando i seed in base alla prossimità con un insieme di seed detti "anchor", che sono seed che non si trovano in condizioni di multi-mapping, poi riuniti in base all'allineamento migliore per la read (score dipende da mismatch, indel, gap e tutto ciò che impatta l'allineamento).

## Ricostruzione del trascrittoma
Sono due strategie principali
- Genome Guided Approach:
	- Si parte allineando le read contro il genoma
	- I frammenti allineati contro il genoma di riferimento vengono assemblati a formare un grafo dei trascritti
	- Il grafo dei trascritti viene parsato in trascritti
	- Si ottengono i loci genomici assemblati dall'RNA frammentato
	- Cufflink, Scripture utilizzano questo approccio
- Genome Independent Approach:
	- Si rompono le read in k-mer
	- Si assemblano le read
	- Si utilizza la strategia dei grafi di de Brujin per costruire l'assemblaggio
	- Il grafo risultante viene parsato in sequenze
	- Le quali vengono allineate contro il genoma, ottenendo i genomic loci assemblati dall'RNA frammentato
	- Abyss, Trinity sono software che utilizzano questo approccio

## Espressione Genica
Le conte di RNA-seq necessitano di apposita normalizzazione prima di poter essere utilizzate. I principali fattori sono:
- Sequencing Depth/Library Size -> Variabilità nel numero di read prodotta da ogni run. Questa variabilità può causare fluttuazioni nel numero di frammenti mappati tra i campioni
- Gene Length -> La frammentazione dell'RNA durante la costruzione delle libreria porta i geni lunghi a creare più read in confronto ai trascritti corti, data medesima abbondanza nel campione
- RNA-Composition -> Pochi geni altamente differenzialmente espressi, differenze nel numero di geni tra campione, o presenza di contaminazione può portare asimmetria in alcuni tipi di normalizzazione

### Normalizzazioni

#### RPM o CPM
Count per million/ Read per million -> Basica, normalizza solo per la profondità di sequenziamento. CPM è fortemente biased in applicazioni dove la lunghezza del gene influenza la sua espressione, quindi RNA-seq
$$\text{RPM or CPM} = \frac{\text{Nr of reads mapped to gene} \cdot 10^6}{\text{Total nr of mapped reads}}  $$
Utile per comparazione tra conte per un gene tra repliche di un stesso gruppo di campioni. NON per comparazione nel campione o per DE analysis
#### RPKM e FPKM
Reads per kilobase million/ Fragments per kilobase million -> normalizza per lunghezza del gene e profondità del sequenziamento.
$$RPKM = \frac{\text{Nr of reads mapped to gene} \cdot 10^3 \cdot 10^6}{\text{Total number of mapped reads} \cdot \text{gene length in bp}} $$
$10^3$ normalizza per lunghezza del gene e $10^6$ normalizza per la profondità/library size
Utile per comparazione tra conte di geni differenti in un campione. NON per comparazione tra campioni o per DE analysis.
FPKM è uguale ma RPKM venne sviluppata per read single-end.
FPKM invece tiene conto del fatto che due read corrispondono ad un singolo frammento, o se una read nella coppia non ha mappato, una read corrisponde al singolo frammento.
RPKM -> Single end
FPKM -> PairEnd
#### TPM
Transcript per million -> Alternativa alle F/RPKM. La media è costante ed è proporzionale alla concentrazione molare relativa di RNA.
$$TPM = A \cdot \frac{1}{\sum{A}}\cdot 10^6$$
$$A = \frac{\text{total read mapped to gene} \cdot 10^3}{\text{gene length in bp}}$$
Utile per comparazione tra geni all'interno di un campione o tra campione. NON per DE analysis

### DE Analysis
L'analisi dei differenzialmente espressi comparano le conte di geni tra campioni per uno stesso gene, la lunghezza del gene quindi non serve come fattore di normalizzazione, anzi potrebbe risultare anche detrimentale. Si utilizzano quindi tipi di normalizzazione diverse, che tengono in considerazione solo Sequencing Depth e RNA composition.
Deseq2 utilizza una sua normalizzazione chiamata median of ratios.

Technical Variation to account for:
- Library Size -> Number of fragments/reads that map on sample. This could be due to differences in the sequences and have nothing to do with the biological phenomenon. Sequencing depth might be the reason of differences. Gene length is not considered because the comparison is same gene between samples and not comparing between genes. Using these counts to compare gene expression level is wrong, they are not normalised for gene length like TPM.
- Library Composition -> Find actually differently expressed genes and filter out as many false positive as possible. E.G. -> Certain genes might be specific to one sample but not another one. This is NOT differential expression. Normalising counts leads to results here.
Method of estimation of size factor -> Median of ratios.
Median of ratios:
1. Geometric mean -> Robustness to outliers compared to mean -> sqrt(geneCounts Sample A \cdot geneCount Sample B) 
2. Divide Counts by geometric mean -> Counts/GeometricMean: Count for untreated / GeomMean; Counts for Treated / GeomMean
3. Median of Ratios -> Grab the median of the ratios calculated in step 2. One median of untreated, one median for treated.
4. Divide the raw counts by the size factor. Size factor is  the Median of Ratios. So untreated will be divided by Median of Ratio of Untreated, while treated will be divided by Median of Ratio of Treated.


## Gene Fusions
Dall'RNA-seq possiamo anche identificare fusioni geniche, come la BCR:ABL derivata da una traslocazione reciproca tra chr9 e chr22.
Rilevazione di indel e mutazioni puntiformi possono essere catturate con un semplice Whole Exome Sequencing, tipicamente riarrangiamenti genomici richiede WGS.
L'RNA seq ci fornisce l'esoma espresso, catturando solo le regioni genomiche trascrizionalmente attive, dandoci la possibilità di identificare di trovare e identificare riarrangiamenti strutturali senza dover ricostruire l'intero genoma.
Tipicamente l'RNA-seq based fusion detection viene effettuata secondo due strategie:
1. Mapping first approach -> Si allineano le read dell'RNA-seq a geni e genomi per identificare read mappate discordanti, che possono suggerire riarrangiamenti
2. Assembly first approach -> Si assemblano direttamente le read in trascritti più lunghi seguita dall'identificazione di trascritti chimerici consistenti con riarrangiamenti cromosomici.

Tipicamente un riarrangiamento viene misurato dal numero di frammenti trovati che sono read chimeriche (split o junction) che hanno un overlap diretto con la junction chimerica del trascritto di fusione, oppure coppie di read discordanti (bridging read pair o fusion-spanning read), dove ogni read mappa su lati opposti della junction chimerica senza un diretto overlap della junction chimerica stessa.

L'algoritmo STAR-fusion utilizza allineamenti identificati dall'allineatore STAR come chimerici e discordanti per la predizione delle fusioni. TrinityFusion ad esempio invece utilizza read chimeriche e assembly del trascrittoma per ricostruire i trascritti di fusione e identificare candidati per fusione.

In generale la fusion detection è fortemente influenzata dai livelli di espressione, dove livelli di espressione troppo bassi, ma anche non eccessivamente, risultano in una ridotta capacità di identificare trascritti di fusione.

Sequenziamento Long-read aumenta significativamente la capacità di rilevamento di fusione, specialmente per i metodi basati sull'assembly.




## SmallRNA detection

L'RNA-seq viene utilizzato anche per la rilevazione di piccoli RNA come i miRNA.
Si inizia con un processo di arricchimento detto size-selection. La tecnica di laboratorio utilizzata si chiama PAGE (Polyacrylamide Gel Electrophoresis), che separa e purifica small RNA di dimensioni inferiori a 35bp.
Dopo questa fase di size selection segue la ligazione degli adattori e la trascrizione inversa.
Segue un secondo processo di size selection dove vengono rimossi ulteriori RNA. Si procede al sequenziamento.

Per miRNA:
- Post-PAGE potrebbe essere utile fitlrare le read che si allineano contro database di soli tRNA, snRNA e snoRNA per verificare che le read prodotte non siano appartenenti ad un'altra categoria di RNA
- Le read sequenziate vengono filtrate per presenza della sequenza 3'-Linker.
- Le read con 3'-linker vengono prima di tutto confrontate contro un database di noti miRNA
- Le read che non hanno nessun match contro il database vengono invece analizzate con software quali mirDeep per verificare l'identificazione di nuovi miRNA. Questo software adopera strategia come l'Hairpin test, ovvero va a mappare le read che non hanno matchato contro il database di miRNA e le mappa contro l'intero genoma di riferimento. Il test hairpin lo effettua quando identifica un cluster di read mappate ad una specifica regione genomica. Avvia un RNA-folding algorithm (ViennaRNA) e controlla se questa sequenza si folda naturalmente in una stem-loop. Se forma un hairpin e la read mappa perfettamente al braccio dell'hairpin, allora viene flaggato come potenziale miRNA con un score.
- Da notare l'esistenza di isomiRNA che sono miRNA 1 base più lunghi o più corti del reference, dato da errori nel Dicer
- Si validano questi nuovi miRNA identificati ad esempio con un Northern Blot

### circRNA Detection
La rilevazione dei circRNA è più complessa, poichè la forma circolarizzata del circRNA non è osservabile semplicemente da dati di sequenziamento.
I circRNA variano sia per genesi sia per dimensione rispetto agli RNA lineari, quindi non possono essere purificati semplicemente filtrando gli RNA per dimensione o per sequenza.
Si utilizzano invece trattamenti applicabili in ordini differenti:
- rRNA depletion -> Rimozione dell'rRNA che compone l'80-90% della popolazione totale di RNA. Fondamentale poichè i circRNA compongono solo lo 0.1% dell'RNA totale. Principalmente la si effettua per subtractive hybdrization (ibridizzazione di probe di ssDNA biotinilato al rRNA, con la susseguente applicazione di bead composti da streptavidina in grado di separare gli rRNA marcati da biotina dal resto degli RNA) e da RNase H degradation, dove sempre probe di ssDNA si ibridizzano specificatamente a rRNA, ed in seguito questi duplex vengono degradati dalla RNase H aggiunta in soluzione. La sola rRNA depletion è altamente inefficace poichè rimuove solo rRNA e non tutto il resto dell'RNA lineare.
- RNase R treatment e/o polyadenilation treatment -> Diversi studi hanno dimostrato che gli RNA lineari sono resistenti alla trattamento con RNasi R poichè presentano determinate strutture al 3', limitazione che viene superata tramite l'aggiunta di una coda di poli(A) al 3' di tutte le specie lineari. Questa lunga terminazione non strutturata è un punto di binding adeguato per l'RNasi R, che effettua attività esonucleasica 3'->5'. Rimuove un gran numero di RNA lineare.
Si possono combinare le tecniche anche:
- rRNA- + Poli(A) + RNase R
- Poli(A) + RNase R + rRNA-
È stato dimostrato che la qualità dell'analisi downstream dei circRNA è estremamente variabile in base ai metodi di arricchimento utilizzati ed in quale ordine. Cambiano il numero di circRNA purificati, la precisione e la sensitività.
Queste variazioni sono dovute alla complessità dei metodi, e quanto essi riescono a purificare circRNA ed eliminare RNA lineari, che interferiscono con l'analisi downstream.

La rilevazione può essere fatta o tramite RT-PCR utilizzando primer divergenti, primer appositi con direzionalità opposta che coprono la BackSplice Junction dei circRNA. Questi primer amplificano circRNA ma non le controparti lineari, dato che primer divergenti diventano convergenti solo se l'RNA è circolare
In alternativa, post arricchimento il campione può essere sequenziato e si possono applicare tecniche di RNA-seq per la loro identificazione.
- Tool per l'identificazione della Back Splice Junction, che è una firma molecolare importante. Molti tool si basano sullo splittare le read o basati su pre-definite BSJ e sequenze fiancheggianti
- Integrated -> Ensemble di tool in grado di integrare e unire i risultati di molteplici tool

## RNA Editing
Il sequenziamento massimo di RNA facilita lo studio dell'intero trascrittoma, quindi anche di eventi post-trascrizionali come l'editing e lo splicing.
Le NGS forniscono un gran numero di sequenze per una data posizione genomica, facilitando la rilevazione di sostituzioni dovute a RNA editing.
Possiamo utilizare dati di NGS (RNA-seq, genome resequencing, exome sequencing) per studiare l'RNA editing a diversi livelli:
- Identificazione di nuovi eventi di editing
- Esplorazione della presenza di conosciuti eventi di A->I

L'identificazione di nuovi eventi può essere effettuata tramite strategie come:
- Genome/Exome vs RNA-seq per l'identificazione
- RNA-seq per l'identificazione di de novo candidati ad Editing

La vera problematica dell'editing de novo è distinguere SNP o eventi simili da eventi di Editing.
L'inosina viene identificata come G da polimerasi et al. Una sostituzione A->G nell'RNA quindi può essere sia un evento di editing, sia una mutazione puntiforme.
Una delle strategie è il confronto RNA-seq contro DNA-seq. Ovviamente se la posizione nel DNA-seq risulta essere una A, mentre i trascritti sono predominantemente G, allora possiamo identificare con una certa confidenza un evento di Editing.
Un'altra possibilità dato che il DNA-seq è abbastanza dispendioso è utilizzare un database di SNP conosciuti per verificare che non sia uno SNP ma un effettivo evento di Editing.
In assenza di entrambe, si utilizzano filtri per minimizzare la quantità di falsi positivi. Protocolli strand-specifici sono preferiti perchè facilitano l'identifiazione in regioni con transcritti in overlap generati da strand opposti.


## Il Trascrittoma
L'espressione è altamente tessuto specifica.
La distanza tra i vari cluster dimostrano come tessuti simili mostrano livelli di espressione simili. All'aumentare della distanza, il profilo di espressione cambia significativamente
![[Pasted image 20260425180742.png]]

## Single Cell
La deconvoluzione di dati di RNA seq consiste in metodi computazionali utilizzati per stimare le relative porzioni di differenti tipi cellulari o subpopolazioni all'interno di un campione eterogeneo basandosi sui profili di espressione genica.
È molto utile per trovare e identificare profili di espressione genica specifici ad un particolare tipo cellulare/subpopolazione.
Presenta alcuni limiti:
- Non ci sono marker affidabili cellula-specifici
- L'eterogeneità all'interno dei tipi cellulari
- Fattori tecnici come batch-effect e profondità di sequenziamento
- L'assunzione di independeza dell'espressione genica tra differenti tipi cellulari

Nuove tecnologie oggi permettono l'anilisi dell'RNA a livello delle singole cellule, chiamato scRNA-seq ovvero single cell RNA seq.
Gli step sono molto simili a quelli già visti:
- Si dissociano le cellule prelevate dal tesuto, creando isolazione per la singola cellula
- Si estrae l'RNA e si preparano le librerie dai diversi tipi cellulari
- Si effettua un pooling dell'RNA e lo si sequenzia
- Le read prodotte vengono allineate al genoma di riferimento
- Si ricostruire il profilo di espressione per cellula, riportando i livelli di espressione per il gene k per la cellula j
- Si effettua una operazione di clustering sui profili di espressione in modo da identificare i tipi cellulari

Lo step di dissociazione avviene per disaggregazione meccanica e dissociazione enzimatica con collagenasi e DNasi. Il prodotto dell'utilizzo di queste tecniche dipende strettamente dal tessuto ed è opportuno determinarlo empiricamente.

La strategia utilizzata per la cattura delle cellule invece determina il throughput (quante cellula da isolare), la qualità e la riproducibilità dell'esperimento. Le 3 opzioni più utilizzate sono:
1. Microtitre plate -> Isolazione delle cellule in pozzetti di un vetrino, utilizzando ad esempio microdissezione o FACS (fluorescent activated cell sorting). Può identificare e scartare cellule danneggiate o trovare pozzetti contenenti doublets (2 o più cellule in un pozzetto). Basso throughput ed è molto dispendioso in termini di tempo di lavoro per cellula
2. Microfluidic-array-based -> Permette un sistema integrato di cattura delle cellule oltre ad effettuare le reazioni chimiche necessarie per la preparazione delle librerie. Ha un throughput più elevato rispetto a microtitre-plate. Tipicamente solo il 10% delle cellule vengono cattuare in una piattaforma microfluidica. I nanopozzetti sono specifici per una particolare dimensione, ha quindi un effetto sul campionamento unbiased delle cellule in tessuti complessi 
3. Microfluidic-droplet-based -> Offre il throughput più elevato e sono i metodi più popolari. Incapsulano cellule individuali all'interno di una gocciolina di dimensione di un nanolitro di olio, insieme ad un bead. Il bead è caricato con enzimi e altre componenti richieste per costruire la libreria. Le piattaforme droplet hanno costi bassi in termini di library preparation (0.05 USD/cell)

Il fluidigm C1 integrate fluidic circuit system è il più comune dispositivo utilizzato per la preparazione di campioni single-cell. Il sistema automatizzato può processare fino a 800 cellule individuali in parallelo. Microvalvole facilitano la cattura delle singole cellule seguite dalla spinta di cellula in camere downstream per la lisi, Trascrittasi inversa, amplificazione e altri trattamenti, dipendentenmente dal target dell'analisi (DNA, mRNA, esomi)

Le droplet microfluidiche stanno emergendo come tecnologia di scelta facilmente implementabili, ad alto throughput e relativamente a basso costo, per un largo range di analisi single cell.
Le goccioline possono essere aricate con singole cellule utilizzando una sospensione cellulare diluita come fase acquosa. La distribuzione delle cellule in goccioline segue distribuzione di poisson, minimizzando il rischio di incapsulazione di molte cellule in una gocciolina.
Una volta formata, le goccioline con cellule incapsulate possono essere manipolate in diverse maniere.

### Library Preparation (Droplet)
Esistono diverse strategie per le droplet microfluidiche
- inDrop -> Indexing droplets. Si utilizzano le droplet microfluidiche per incapsulare una soluzione altamente diluita di cellula con bead barcoding fatti di idrogel
- dropSeq -> Simile a inDrop ma le cellule sono incapsulate in droplet con bead barcoding fatti di resina dura
- 10x -> È una combinazione di inDrop + dropSeq

### Library sequencing
Ogni libreria contiene un barcode che identifica una cellula ed un UMI che identifica il gene, maniera tale che identificare tipi cellulare e geni sia semplice.
Si raggruppano le cellule per barcode, e si contano gli UMI unici per ogni gene in ogni cellula


### Applicazioni
- Profilazione single-cell
- espressione differenziale
- fattori di trascrizione
- Cell-cell interaction
- Disease specific population
- Lineage Trajectory reconstitution
- Cellule staminali cancerogeni
