# Strategie di Sequenziamento Genomico

---

## Marker e Mappe

Un **marker** è un sito unico nel genoma, tipicamente una sequenza. I marker sono utilizzati nella costruzione delle mappe, che forniscono una guida per esperimenti di sequenziamento mostrando le posizioni dei marker genomici (geni e altro).

Per convenzione i metodi di mapping si dividono in due categorie:

|Tipo|Base|Tecniche|
|---|---|---|
|**Genetic Mapping**|Tecniche genetiche|Cross-breeding, analisi di pedigree|
|**Physical Mapping**|Biologia molecolare|Esame diretto delle molecole di DNA|

---

## Genetic Mapping

Una **mappa genetica** (linkage map) mostra la locazione relativa dei marker genetici su un cromosoma. Si basa sul **linkage genetico**: più vicini due marker sono su un cromosoma, più tenderanno a segregare insieme.

I geni sono marker genetici, ma non sono ideali per il mapping nei genomi grandi: sono spesso estremamente sparsi, con enormi gap tra loro, e solo una frazione esiste in forma allelica distinguibile.

Feature mappate che non sono geni si chiamano **DNA Marker**. Come i geni, i DNA marker devono possedere almeno due alleli per essere utili.

### Tipi di DNA Marker

|Marker|Descrizione|
|---|---|
|**RFLP** (Restriction Fragment Length Polymorphism)|Presenza/assenza di siti di restrizione tra individui. Rilevato con enzimi di restrizione: la molecola con il sito aggiuntivo viene tagliata in un pezzo in più|
|**SSLP** (Simple Sequence Length Polymorphism)|Array di sequenze ripetute con lunghezza variabile; alleli diversi contengono numero diverso di unità ripetute|
|**SNP** (Single Nucleotide Polymorphism)|Posizioni in cui singoli individui differiscono per un singolo nucleotide. Almeno 1,5 milioni di SNP nel genoma umano. Raramente danno vita a RFLP|

La costruzione della mappa si basa sull'**analisi linkage**; l'affidabilità di un marker è data dal **PIC index**.

---

## Physical Mapping

Una mappa genetica è raramente sufficiente per il sequenziamento diretto, per due motivi:

- **Risoluzione limitata dal numero di Crossing-Over** — nei grandi eucarioti è possibile studiare poche meiosi; geni distanti decine di migliaia di kb possono apparire nella stessa posizione nella mappa genetica
- **Accuratezza limitata** — i crossover avvengono più frequentemente in determinate zone

Una **mappa fisica** è una rappresentazione grafica delle locazioni fisiche di marker e landmark all'interno di un cromosoma o genoma. Una sequenza completa di un genoma è la forma più dettagliata di mappa fisica.

### Tecniche principali

- **Restriction mapping** — localizza le posizioni relative di siti di riconoscimento per endonucleasi di restrizione su una molecola di DNA
- **FISH** (Fluorescent In Situ Hybridization) — le locazioni dei marker vengono mappate per ibridizzazione di un probe con il cromosoma intatto
- **STS mapping** (Sequence Tagged Site) — le posizioni di corte sequenze sono mappate da PCR e/o analisi di ibridizzazione

#### STS (Sequence Tagged Site)

Una STS è una corta sequenza di **100–500 bp**, facilmente riconoscibile e presente **una sola volta** nel cromosoma o nel genoma studiato. La PCR si usa per determinare quale frammento contiene ciascuna STS.

Le STS si ottengono principalmente da:

- **EST** (Expressed Sequence Tags) — corte sequenze ottenute da analisi di cloni cDNA
- **SSLP** — già mappati da linkage analisi, particolarmente utili perché forniscono una **connessione diretta tra mappa genetica e mappa fisica**
- **Random genomic sequences** — ottenute sequenziando pezzi di DNA genomico clonato o da database

---

## Clone-by-Clone (Hierarchical Shotgun)

La strategia Clone-by-Clone è una strategia di physical mapping in cui vengono prodotte serie di cloni in overlap (**contig**), ognuno dei quali copre una lunga regione contigua del genoma.

### Vettori di Clonaggio

|Vettore|Base|Dimensione inserzione|
|---|---|---|
|**BAC** (Bacterial Artificial Chromosome)|Plasmide mini-F di E. coli (fattore F circolare)|>300 kb|
|**PAC** (P1-derived Artificial Chromosome)|Batteriofago P1, introduzione per elettroporazione|130–150 kb|

Il vettore BAC mantiene il clone in singola copia o copy number molto basso per cellula, riducendo eventi di ricombinazione e incrementando la stabilità del DNA clonato.

### Minimal Tiling Path (MTP)

Il **Minimal Tiling Path** è il più piccolo numero di cloni che copre l'intera regione di interesse/cromosoma nella mappa fisica.

Nel protocollo Clone-by-Clone:

1. Si costruisce prima la mappa fisica
2. I cloni nel MTP vengono sequenziati uno a uno

Questa strategia è stata usata per sequenziare i genomi di _A. thaliana_, _H. sapiens_ e altri. Nel Whole-Genome Shotgun il MTP viene usato per **validare e migliorare la qualità dell'assemblaggio**.

### Protocollo

1. I cloni nel MTP (es. BAC) vengono selezionati e il DNA viene purificato in grande quantità
2. Il DNA purificato viene frammentato per **shearing fisico** in frammenti random di 2–5 kb
3. I frammenti vengono subclonati
4. Vengono generate read da una o entrambe le estremità dei subcloni selezionati casualmente (migliaia di read per ogni BAC da 100–150 kb)
5. Le read casuali vengono assemblate sulla base di overlap → **prefinished sequence**
6. La sequenza preliminare contiene gap e zone di bassa qualità, con ordine e orientamento dei contig spesso ignoti
7. Si applica il **sequence finishing**: generazione di dati aggiuntivi per chiudere i gap e migliorare la qualità
8. Si ottiene la sequenza finita e accurata dell'intero clone

---

## Whole Genome Shotgun (WGS)

Nel WGS l'intero genoma viene frammentato e sequenziato senza costruire prima una mappa fisica. L'assemblaggio avviene per:

1. **Contig** — assemblaggio iniziale delle read individuali in base agli overlap
2. **Scaffold** — i gruppi di contig vengono organizzati sulla base delle informazioni di linking fornite dalle **coppie di read** (paired-end: una read si assembla in un contig, l'altra in un altro contig a distanza nota)
3. **Ancoraggio** — gli scaffold vengono allineati al genoma di riferimento identificando marker sequence-based già mappati, associandoli con una locazione nota nel genoma

### Hybrid Shotgun

In approcci ibridi si uniscono elementi del Clone-by-Clone e del WGS:

1. Si prepara una libreria di subcloni dall'intero genoma e si generano numerose read genome-wide
2. Contemporaneamente, BAC individuali vengono sottoposte a shotgun sequencing
3. Le read derivanti dai BAC identificano sequenze in overlap nella grande collezione WGS, **riducendo la complessità del dataset** in una serie di bin di dimensioni di un BAC
4. L'insieme combinato di read per ogni BAC viene assemblato individualmente e sottoposto a sequence finishing

---

## Ridondanza e Coverage

La **ridondanza** indica quante volte una base è stata coperta. Trovare nuove sequenze è un evento raro che segue una **distribuzione di Poisson**:

$$P_0 = e^{-R}$$

Dove $P_0$ è la probabilità di non coprire una base dato il livello medio di ridondanza $R$.

Il **coverage** del genoma si calcola come:

$$C = \frac{L \cdot N}{G}$$

|Parametro|Significato|
|---|---|
|$C$|Coverage|
|$L$|Lunghezza delle read|
|$N$|Numero di read|
|$G$|Lunghezza del genoma (aploide)|

---

## Ripetizioni nell'Assemblaggio

Le ripetizioni nei genomi eucariotici rappresentano un grande ostacolo. Quando un genoma contenente DNA ripetitivo viene frammentato, alcuni pezzi conterranno gli stessi motivi di sequenza. Questo può portare a:

- Trascurare il DNA tra coppie di ripetizioni durante il riassemblaggio
- Connettere erroneamente pezzi separati sullo stesso o su cromosomi diversi

Una **mappa genomica** permette di evitare questi errori.

---

## Overlap Layout Consensus (OLC)

L'algoritmo OLC è il metodo classico di assemblaggio. Si articola in tre fasi:

### 1. Overlap

Si cercano read in overlap. Le read vengono considerate come **nodi** in un grafo; gli **archi** rappresentano allineamenti tra read.

L'assembler individua i merge in base a:

- Lunghezza dell'overlap
- % di identità nella regione di overlap
- Dimensione dell'overhang

### 2. Layout

Si mergiano le read in contig e supercontig. L'obiettivo è trovare la **Shortest Common Superstring**.

Si percorre un **cammino Hamiltoniano** nel grafo: ogni nodo (read) viene attraversato una sola volta → ogni read viene inclusa una volta nell'assemblaggio.

> ⚠️ Il problema del cammino Hamiltoniano è **NP-Hard**: la costruzione del grafo di overlap su dataset con miliardi di read è computazionalmente proibitiva.

Per semplificare il grafo si rimuovono gli **archi transitivamente inferibili** (archi che "saltano" uno o due nodi). I contig ottenuti corrispondono a stretch non ramificanti. Bisogna anche tenere conto di sottografi spuri causati da errori di sequenziamento.

### 3. Consensus

Le read che costituiscono un contig vengono allineate e si prende il **voto consensus** per ogni posizione.

### Svantaggi di OLC

La costruzione del grafo di overlap è lenta. I dataset di sequenziamento moderni contengono fino a miliardi di read e centinaia di miliardi di nucleotidi totali, rendendo OLC impraticabile su larga scala senza ottimizzazioni significative.


---

## DeBrujin Graph

Un'alternativa all'OLC sono i grafi di DeBrujin (DBG).
Si inizia con una collezione di read, sottostringhe del genoma di riferimento

ogni K-mer viene diviso in left-mer ed un right-mer di dimensioni k-1.
3-mer -> AAC -> L-2-mer -> AA  
3-mer -> AAC -> R-2-mer -> AC 

Un suffisso sono tutti i nucleotidi eccetto il primo. Prefisso tutti i nucleotidi eccetto l'ultimo.

Ogni kmer in input viene diviso in due sottostringhe di overlap, L-k-1-mer e R-k-1-mer.
Ponendo i 2-mer come nodi in un nuovo grafo, si immette un arco da ogni k-1-mer sinistro al corrispondente k-1-mer destro.

Nei grafi di De Brujin, le stringhe devono essere di lunghezza uguale, cosi che quando usate nell'assemblaggio  lo step iniziale è quello di rompere le read in segmenti o k-mer di 20-30 nt. k-mer duplicati vengono scartati, così questo step riduce le dimensioni del dataset. Ogni k-mer è poi convertito in una sequenza preffiso e suffisso.

Gli overlap tra k-mer vengono poi identificati e i k-mer vengono collegati tra loro come un grafo di de-brujin. Ogni k-mer viene identificatgo da un nodo, con archi che connettono i k-mer che hanno suffissi e prefissi in overlap.
La master sequenze può essere letta dal grafo

Se la sequenza contiene DNA ripetitivo, allora il grafo di de brujin si ramificherà al posto di linearizzarsi. In questo caso, allora si tenta di identificare un cammino euleriano attraverso il grafo, cammino dove ogni nodo viene osservato una sola volta.
Se viene identificato un cammino euleriano, allora l'assemblaggio di sequenza corretto verrà trovato, anche in presenza di sequenze ripetute


## Scaffolds
Un assembler DeBrujin o OLC risulterà sempre in un insieme di contig. 
Il prossimo step è identificare contig adiacenti uno all'altro nel genome e stabilire una serie di scaffold, dove ogni scaffold compone un insieme di sequenze contig separate da gap, non coperte dal dataset.

3 strategie per la costruzione degli scaffold. I contig adiacenti uno all'altro possono essere identificati da read in pair-end, per referenza ad una mappa genetica, e da sequenze long-read.

- Pair-end possono essere utili. Se due membri di una coppia di read cadono in contig differenti, allora chiaramente questi contig devono essere adiacenti uno all'altro nella sequenza del gneoma, e il gap tra loro potrebbe essere riempito da ulteriore sequenziamento del frammento da cui le read in pair end sono state ottenute
- Se è disponibile una mappa genetica o fisica, allora questa può essere usata per ancorare i contig sulla sequenza del genoma e per identificare i contig adiacenti. Mappe ottiche sono ora frequentemente utilizzate per questo motivo, e percheè sono relativamente facili da generare ed hanno un elevata densità di marker
- Se i contig sono stati assemblati da short read, allora SMRT o Nanopore sequencing possono essere utilizzati per generare long-read che mostreranno quali contig short read sono adiacenti


## Mapping Ottico -> Bionano

Si parte con DNA labelling
1. HMW DNA viene nickato con una endonucleasi scelta che introduce single strand nick nel genoma
2. Taq polimerasi riconosce questi siti e rimpiazza diversi nucleotidi con nucleotidi marcati a fluorescenza, aggiunti alla soluzione
3. Le due estremità del DNA sono ligate utilizzando la ligasi
4. Il backbone del DNA viene marcato con una tinta per DNA
Il dsDNA etichettato viene carico su un chip di flowcells. Viene applicato un voltaggio che concentra il DNA coiled sulla lip. Il DNA viene poi spinto verso i pillars al centro per perdere la struttura/raddrizzarsi. Il DNA viene poi fermato e rilevato nei nanocanali. 
Blu -> DNA Backbone staining, Verde -> Siti nickati etichettati a fluorescenza

Visualizzazione del DNA
Una volta ottenuta una immagine grezaz delle lunghe molecole di  DNA etichettato, viene converitto in rappresentazione digitale dei pattern label motif-specific.
Un software assembla i dati de novo per ricreare una whole genome map assembly
### qualità
Due parametri devono essere considerati per misurare la qualità del genoma
1. Completezza -> Frazione di eucromatina sequenziata
2. Accuratezza -> % errori
Sono state create misurazioni statistiche per ottener una più accurata indicazione dellaqualità del gnoma sequenziato. 
N50 size -> applicvabile a contig o scaffold