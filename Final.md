---
id: Final
aliases: []
tags: []
---

# Applicazioni di NGS

| DNA                                                       | RNA                                                            |
| --------------------------------------------------------- | -------------------------------------------------------------- |
| Risequenziamento genomico (SNP, GWAS)                     | Analisi qualitativa e quantitativa del trascrittoma            |
| De-novo sequencing                                        | Identificazione e caratterizzazione di miRNA e altri ncRNA     |
| Identificazione di varianti strutturali                   | RNA Editing                                                    |
| Interazioni della cromatina 3D                            | Metatrascrittomica (analisi funzionale di campioni ambientali) |
| Epigenomica (stato cromatinico e metilazione)             |                                                                |
| Metagenomica (analisi tassonomica di campioni ambientali) |                                                                |

---

## Genome Resequencing

Consiste nel sequenziare nuovamente l'intero genoma di una specie di cui si ha un genoma di riferimento, permettendo l'identificazione di varianti come SNP, indel e varianti strutturali.

---

## Whole Genome Sequencing (WGS)

Processo in cui si va a determinare l'intera sequenza del DNA di un organismo, incluso il DNA cromosomale e mitocondriale.

---

## Target Enrichment

L'arricchimento consiste nel catturare, o arricchire, specifiche regioni di interesse (esoni, ncRNA, geni specifici) prima del sequenziamento. Le tecniche descritte qui si riferiscono all'arricchimento di **DNA genomico**; per gli ncRNA si utilizzano tecniche differenti data la loro struttura complessa e diversificata.

### Array Hybridization

Si utilizzano probe (piccoli oligonucleotidi sintetici) su un vetrino (array). Il DNA genomico viene introdotto sull'array, dove il DNA target si lega ai probe complementari; il DNA non-target viene rimosso. Il DNA catturato viene poi sequenziato.

### In Solution Hybridization

Il metodo più comune oggi. I probe vengono **biotinilati** e inseriti insieme al DNA genomico in soluzione. Dopo l'ibridizzazione, bead con **streptavidina** legano la biotina, recuperando i probe e il DNA di interesse e permettendo di rimuovere il resto del materiale genomico.

### Molecular Inversion Probe (MIP)

Un oligonucleotide a singolo filamento con le terminazioni complementari al DNA target. Quando si lega al target, si **inverte** formando un cerchio attorno ad esso. Una reazione di gap-filling e ligazione chiude il cerchio. Solo i probe circolarizzati vengono sottoposti a PCR.

---
## Exome Sequencing
![[Pasted image 20260423183843.png]]

---

## Varianti Strutturali

Varianti strutturali identificabili con sequenziamento di seconda generazione:

- Mutazioni puntiformi
- Indel
- Delezioni omozigoti → Copy Number Variation (CNV)
- Delezioni emizigoti → Copy Number Variation (CNV)
- Gain → Copy Number Variation (CNV)
- Punti di breakpoint di traslocazioni
- Patogeni

### Workflow di Variant Calling

I dati vengono sequenziati e allineati contro un genoma di riferimento per creare un file **BAM**.

#### Varianti Ereditarie

Si utilizzano 3 BAM: **proband**, **madre** e **padre**. Si effettua un **joint variant calling** (SNV/Indel/SV/CNV), seguito da filtro per rimozione di artefatti e conferma con review manuale. Per le alterazioni **de novo** è necessaria anche la rimozione dei falsi positivi.

#### Varianti Somatiche

Si utilizzano 2 BAM: **tumore** e **controllo (normale)**. Si cercano SNV/Indel/SV/CNA somatiche, si rimuovono gli artefatti e si conferma manualmente.

### Annotazione delle Varianti

WES e WGS producono dati su numerose varianti genetiche, la maggior parte delle quali non è rilevante nel contesto di uno studio su una particolare malattia — non avendo effetto funzionale sulle proteine o a livello sistemico. Tutti gli individui presentano un gran numero di varianti ereditarie e mutazioni de novo, ma solo una piccola frazione impatta effettivamente la funzione proteica o sistemica (es. mutazioni non senso).

L'annotazione di varianti ha come obiettivo produrre **metadati ausiliari** per le variant call grezze filtrate per qualità, al fine di approfondire le varianti che probabilmente hanno un impatto funzionale o sistemico.

> Le linee guida e gli standard per l'identificazione di varianti genetiche sono ancora in sviluppo.

---

## ChIP-Seq

### Protocollo

1. **Cross-linking** con formaldeide — crea legami covalenti tra proteine e DNA (ma anche tra RNA e altre proteine)
2. **Frammentazione della cromatina** — si rompe la cromatina in frammenti di alta qualità, anche al di sotto di **500 bp**, per massimizzare il risultato del genome mapping
3. **Immunoprecipitazione** — si utilizza un anticorpo contro la proteina di interesse, seguito da incubazione e centrifugazione. Questo step permette anche la rimozione di siti di binding non specifici
4. **Recupero e purificazione del DNA** — si effettua l'inversione del cross-link DNA-proteina per separarle, e si estrae e purifica il DNA
5. **Analisi** — si ligano adattatori oligonucleotidici ai frammenti di DNA per prepararlo al sequenziamento massivo

L'ultimo step dipende dalla strategia di sequenziamento:

- **Seconda generazione** — end-repair, ligazione, PCR (cluster o emPCR)
- **Helicos** — aggiunta di coda di poli(A)

### Analisi Bioinformatica

Le short read generate dai frammenti immunoprecipitati (dette **tag**) vengono allineate al genoma. Si studia poi la loro distribuzione:

1. Ogni posizione mappata viene estesa con un frammento di dimensione stimata per generare un **profilo**
2. Il profilo combinato viene analizzato tramite algoritmi di **peak-calling** (es. MACS) per distinguere segnali di binding dal rumore di fondo
3. L'identificazione dei picchi può essere effettuata su qualsiasi profilo generato

## Metagenomica

La metagenomica è lo studio della struttura e della funzione di intere sequenze nucleotidiche isolate e analizzate da tutti gli organismi in un campione "bulk", tipicamente ambientale (es. feci → microbiota). È spesso utilizzata per studiare uno specifico gruppo di microorganismi, come quelli che si trovano sulla pelle umana, nel suolo o nell'acqua.

Tradizionalmente studiati basandosi su colonie clonali coltivate, i recenti studi utilizzano metodologie shotgun per raccogliere campioni di tutti i geni di tutti i membri della colonia di interesse.

---

### Amplicon Metagenomics

Si estrae il **16S rRNA** da molteplici specie. Il sequenziamento di ampliconi è diventato uno strumento potente per studiare la **diversità delle colonie**, effettuando il sequenziamento di parti del:

- **16S rDNA** → per i procarioti
- **ITS** (Internal Transcribed Spacer) → per i funghi

Questo permette la rapida e profonda analisi delle comunità microbiche da campioni ambientali.

#### Workflow

1. Estrazione del DNA dal campione
2. Amplificazione del gene rRNA tramite **PCR**
3. Sequenziamento dei geni rRNA amplificati
4. Clusterizzazione delle sequenze per identità (es. 99%) in unità chiamate **OTU** (Operational Taxonomic Units)
5. Ricerca delle sequenze rRNA tramite **BLAST** contro un database con milioni di sequenze tassonomicamente classificate

---

### Shotgun Metagenomics

Si estraggono short read da **tutte le specie** presenti nel campione, senza targeting specifico di un marcatore.

#### Workflow

1. Raccolta e frammentazione del DNA
2. Sequenziamento del DNA amplificato
3. **Assembly** del genoma tramite metodi di assemblaggio
4. **Gene finding** e annotazione per organizzare le sequenze
5. **Phylogenetic binning** per raggruppare i genomi per specie
6. **Ricostruzione metabolica**

---

### Confronto
|                                | Amplicon                        | Shotgun                          |
| ------------------------------ | ------------------------------- | -------------------------------- |
| **Target**                     | Marcatore specifico (16S, ITS)  | Tutto il DNA del campione        |
| **Informazione**               | Diversità tassonomica           | Tassonomia + funzione metabolica |
| **Costo**                      | Più basso                       | Più alto                         |
| **Complessità bioinformatica** | Minore                          | Maggiore                         |
| **Organismi**                  | Procarioti (16S) / Funghi (ITS) | Tutti gli organismi              |

---

# RNA-seq

RNA-seq è una procedura sperimentale per generare read di sequenza derivate dall'intera molecola di RNA. Può essere usata per costruire una mappa completa del trascrittoma tra tutti i tipi cellulari, perturbazioni e stati. Facilita la scoperta di nuovi trascritti, l'identificazione di geni soggetti a splicing alternativo e la scoperta di espressione allele-specifica.

---

## Preparazione della Libreria

1. Estrazione dell'RNA totale dal materiale scelto (cellula o tessuto)
2. **Arricchimento** tramite:
    - **Poli(A) selection** → arricchisce trascritti con coda poli(A)
    - **Ribodepletion** → rimozione dell'RNA ribosomale
3. Conversione dell'RNA in **cDNA** tramite trascrittasi inversa
4. Ligazione degli adattatori di sequenza alle terminazioni dei frammenti di cDNA
5. Amplificazione tramite **PCR** → libreria pronta per il sequenziamento

---

## Tipi di Trascrittomica

|Tipo|Descrizione|
|---|---|
|**Bulk**|Tutto l'RNA proveniente da tutte le cellule|
|**Single Cell**|RNA isolato per ogni singola cellula|
|**Spaziale**|Include informazioni sulla posizione spaziale 3D del trascritto|

---

## Bulk RNA-seq

### Workflow

1. Allineamento delle read
2. Quantificazione

### Analisi possibili

- Espressione differenziale
- Analisi di ncRNA
- Analisi di isoforme di splicing
- Analisi di eventi di RNA editing
- Eventi di poliadenilazione alternativa

---

### Tipi di Read

|Tipo|Descrizione|
|---|---|
|**Paired-end**|Coppie di read: una forward e una reverse dello stesso trascritto, con un dato numero di nucleotidi in overlap|
|**Single-end**|Read individuali senza una controparte reverse della stessa regione|

---

### Tipi di Librerie

Le librerie di mRNA possono essere **stranded** o **unstranded**.

I protocolli stranded preservano l'informazione riguardante lo strand da cui l'mRNA si è originato — informazione che viene persa nel protocollo unstranded.

|Tipo|Comportamento delle read|
|---|---|
|**Stranded forward**|Le read mappano principalmente sullo stesso strand del gene|
|**Stranded reverse**|Le read mappano principalmente sul filamento opposto|
|**Unstranded**|Le read mappano indipendentemente dall'orientamento → ~50% forward, ~50% reverse|

**Come si ottengono le librerie stranded:**

- **First strand library** → si sintetizza il secondo strand utilizzando **dUTP**, che viene poi rimosso per digestione con **uracil-DNA-glicosilasi**
- **Second strand library** → si rimuove l'RNA dopo la sintesi del filamento template, prima della PCR e del sequenziamento

---

## Read Mapping

Per allineare le sequenze contro il genoma di interesse è necessario un **allineatore spliced-aware** (es. STAR, TopHat2, SOAPSplice, Bowtie).

Esistono due approcci generali:

### Exon-First Approach

1. Si mappano le read continuativamente al genoma con un allineatore unspliced
2. Le read non mappate vengono divise in segmenti più corti e allineate indipendentemente

**Vantaggio**: molto efficiente quando solo una piccola porzione di read richiede il secondo step (computazionalmente dispendioso).

**Svantaggio**: le read esoniche possono mappare sia su un gene sia su uno pseudogene, preferendo il gene per la mancanza di mutazioni; una read spliced potrebbe però comunque essere assegnata allo pseudogene (apparendo come esonica), impedendo l'esplorazione di un allineamento spliced ad alto score.

---

### Seed-Extend Approach

Approccio stile BLAST:

1. Le read vengono divise in **k-mer** (seed)
2. Si usa un **FM-index** per trovare ogni possibile locazione dove un seed combacia al reference
3. Le regioni candidate vengono esplorate con metodi ad alta sensibilità: **Smith-Waterman** o estensione iterativa con merging dei seed iniziali, per determinare l'esatto allineamento spliced

**Svantaggio**: in media impiega **8 volte più tempo** dell'exon-first, risultando solo in 1.5 spliced read aggiuntive.

---

## STAR (Spliced Transcripts Alignment to a Reference)

STAR utilizza un approccio basato sui **MMP** (Maximal Mappable Prefixes): per ogni read, cerca la sequenza più lunga che corrisponde esattamente in una o più locazioni sul genoma di riferimento.

### Algoritmo

1. Si trova il primo MMP della read
2. Si ripete la ricerca solo sulla **porzione non mappata** per trovare il successivo MMP
3. Se non viene trovato un match esatto per mismatch o indel, l'MMP precedente viene **esteso**
4. Se l'estensione non produce un buon allineamento, la porzione a bassa qualità o l'adattatore viene **soft-clipped**
5. I seed separati vengono **riuniti** per ricostruire la read completa:
    - Prima si clusterizzano i seed in base alla prossimità con un insieme di seed detti **anchor** (seed non in condizioni di multi-mapping)
    - Poi si riuniscono in base all'allineamento migliore per la read (score dipende da mismatch, indel, gap e tutto ciò che impatta l'allineamento)

> STAR utilizza un **uncompressed Suffix Array** per ricercare velocemente gli MMP contro i genomi di riferimento più grandi. La ricerca sequenziale delle sole porzioni non mappate garantisce l'efficienza dell'algoritmo.

---

## Ricostruzione del Trascrittoma

Esistono due strategie principali:

### Genome-Guided Approach

1. Si allineano le read contro il genoma di riferimento
2. I frammenti allineati vengono assemblati a formare un **grafo dei trascritti**
3. Il grafo viene parsato in trascritti
4. Si ottengono i **loci genomici** assemblati dall'RNA frammentato

Software: **Cufflinks**, **Scripture**

### Genome-Independent Approach

1. Le read vengono rotte in **k-mer**
2. Si assemblano le read usando la strategia dei **grafi di De Bruijn**
3. Il grafo risultante viene parsato in sequenze
4. Le sequenze vengono allineate contro il genoma → si ottengono i **loci genomici** assemblati dall'RNA frammentato

Software: **ABySS**, **Trinity**

---

## Espressione Genica — Normalizzazione

Le conte di RNA-seq necessitano di normalizzazione prima di poter essere utilizzate. I principali fattori da tenere in considerazione sono:

|Fattore|Problema|
|---|---|
|**Sequencing Depth / Library Size**|Variabilità nel numero di read prodotte per run → fluttuazioni nel numero di frammenti mappati tra campioni|
|**Gene Length**|La frammentazione dell'RNA porta i geni lunghi a generare più read rispetto ai trascritti corti, a parità di abbondanza|
|**RNA Composition**|Pochi geni altamente differenzialmente espressi, differenze nel numero di geni tra campioni, o contaminazione possono introdurre asimmetria|

---

### RPM / CPM (Reads/Counts Per Million)

Normalizza solo per la **profondità di sequenziamento**.

$$\text{RPM/CPM} = \frac{\text{Nr. reads mappate al gene} \cdot 10^6}{\text{Nr. totale reads mappate}}$$

**Vantaggi**
 - Comparazione tra conte per uno stesso gene tra repliche dello stesso gruppo
**Svanataggi**
- NON per comparazione tra geni nello stesso campione
- NON per DE analysis
- Fortemente biased in RNA-seq dove la lunghezza del gene influenza l'espressione

---

### RPKM / FPKM (Reads/Fragments Per Kilobase Million)

Normalizza per **lunghezza del gene** e **profondità di sequenziamento**.

$$\text{RPKM} = \frac{\text{Nr. reads mappate al gene} \cdot 10^3 \cdot 10^6}{\text{Nr. totale reads mappate} \cdot \text{lunghezza gene (bp)}}$$

Dove $10^3$ normalizza per la lunghezza del gene e $10^6$ per la profondità/library size.

| Metrica  | Applicazione                                                                                                                |
| -------- | --------------------------------------------------------------------------------------------------------------------------- |
| **RPKM** | Read single-end                                                                                                             |
| **FPKM** | Read paired-end (due read = un singolo frammento; se una read della coppia non ha mappato, una read = un singolo frammento) |

**Vantaggi**
-  Comparazione tra conte di geni diversi nello stesso campione
**Svantaggi**
-  NON per comparazione tra campioni
-  NON per DE analysis

---

### TPM (Transcripts Per Million)

Alternativa a RPKM/FPKM. La media è costante ed è proporzionale alla **concentrazione molare relativa** di RNA.

$$A = \frac{\text{Nr. reads mappate al gene} \cdot 10^3}{\text{lunghezza gene (bp)}}$$

$$\text{TPM} = A \cdot \frac{1}{\sum A} \cdot 10^6$$

**Vantaggi**
-  Comparazione tra geni nello stesso campione
-  Comparazione tra campioni
**Svantaggi**
-  NON per DE analysis

---

## DE Analysis (Analisi dell'Espressione Differenziale)

La DE analysis compara le conte di uno stesso gene tra campioni diversi. La **lunghezza del gene non serve** come fattore di normalizzazione (anzi, potrebbe essere detrimentale). Si usano normalizzazioni che tengono conto solo di:

- **Library Size** — numero di frammenti/read che mappano su un campione. Le differenze potrebbero non avere nulla a che fare con il fenomeno biologico. La lunghezza del gene non è considerata poiché si confronta lo stesso gene tra campioni, non geni diversi tra loro.
- **Library Composition** — alcuni geni potrebbero essere specifici di un campione ma non di un altro. Questo **non è** espressione differenziale. La normalizzazione delle conte aiuta a rimuovere questo tipo di falsi positivi.

**DESeq2** utilizza una normalizzazione chiamata **Median of Ratios**.

### Median of Ratios (DESeq2)

1. **Media geometrica** per ogni gene tra i campioni — più robusta agli outlier rispetto alla media aritmetica: $$\text{GeomMean} = \sqrt{\text{geneCount}_A \cdot \text{geneCount}_B}$$
    
2. **Divisione delle conte per la media geometrica**:
    
    - Untreated: $\frac{\text{Count}_\text{untreated}}{\text{GeomMean}}$
    - Treated: $\frac{\text{Count}_\text{treated}}{\text{GeomMean}}$
3. **Mediana dei rapporti** — si prende la mediana dei rapporti calcolati al passo 2 per ogni condizione (una mediana per untreated, una per treated) → questo è il **size factor**
    
4. **Divisione delle conte grezze per il size factor**:
    
    - Untreated diviso per la mediana dei rapporti di untreated
    - Treated diviso per la mediana dei rapporti di treated


## Gene Fusions

Dall'RNA-seq è possibile identificare **fusioni geniche**, come la **BCR:ABL** derivata da una traslocazione reciproca tra chr9 e chr22.

Mentre indel e mutazioni puntiformi possono essere catturate con il Whole Exome Sequencing, i riarrangiamenti genomici richiedono tipicamente WGS. L'RNA-seq fornisce l'**esoma espresso**, catturando solo le regioni genomicamente trascrizionalmente attive, permettendo di identificare riarrangiamenti strutturali senza dover ricostruire l'intero genoma.

### Strategie di Rilevamento

| Approccio | Descrizione |
|---|---|
| **Mapping-first** | Si allineano le read al genoma per identificare read mappate discordanti, che suggeriscono riarrangiamenti |
| **Assembly-first** | Si assemblano direttamente le read in trascritti più lunghi, seguita dall'identificazione di trascritti chimerici consistenti con riarrangiamenti cromosomici |

### Tipi di Read per la Rilevazione

Un riarrangiamento viene misurato da due tipi di evidenza:

- **Read chimeriche** (split o junction read) — hanno un overlap diretto con la junction chimerica del trascritto di fusione
- **Read discordanti** (bridging read pair / fusion-spanning read pair) — ogni read mappa su lati opposti della junction chimerica, senza overlap diretto della junction
### Software

- **STAR-fusion** — utilizza gli allineamenti identificati da STAR come chimerici e discordanti per la predizione delle fusioni
- **TrinityFusion** — utilizza read chimeriche e assembly del trascrittoma per ricostruire i trascritti di fusione e identificare candidati
### Note

> La fusion detection è fortemente influenzata dai **livelli di espressione**: livelli troppo bassi (ma anche semplicemente non elevati) riducono la capacità di identificare trascritti di fusione.

Il **sequenziamento long-read** aumenta significativamente la capacità di rilevamento, specialmente per i metodi basati sull'assembly.

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
