
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