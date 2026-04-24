
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

