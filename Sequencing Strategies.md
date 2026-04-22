

# Strategies
## Clone-by-Clone Vector

La strategia Clone-by-Clone Vector è una strategia di physical mapping, dove vengono prodotti serie di cloni (contig) in overlap, ognuno dei quali controlla una lunga, contigua regione del genoma di partenza.
Per la strategia shotgun, ogni clone mappato è subclonato in librerie più piccole, dalle quali si ottengono casualmente read delle sequenze.
Nel caso di BAC, tipicamente richiede la generazione di diverse migliaia di read per clone.
Il dataset risultante di sequenze viene poi utilizzato per assemblare la completa sequenza del clone.

Il sistema BAC utilizza il fattore di fertilità circolare F di E.coli che può stabilmente trasportare frammenti di DNA di dimensioni elevate >300Kb.
Il vettore BAC si basa su un plasmide mini-F, che mantiene il clone BAC in singola copia o con copy number molto basso per cellula batterica, riducendo il numero di eventi di ricombinazione in elementi genomici virali e incrementando la stabilità del genoma clonato.

Il vettore P1 per l'introduzione di DNA ricombinante in E.coli tramite tecniche di elettroporazione deriva dal batteriofago P1.
P1-derived Chromosomes (PAC) possono trasportare pezzi di DNA con una dimensione di inserzione di 130-150Kb.

### Minimal Tiling Path
Il più piccolo numero di cloni che coprono l'intera regione d'interesse/cromosoma rappresentata dalla mappa fisica è chiama Minimum Tiling Path.
La determinazione del più piccolo set di cloni che copre una intera regione è cruciale nel Clone-by-Clone (hierarchical). 
In questo protocollo, prima si costruisce la mappa fisica, poi i cloni nel MTP vengono sequenziati uno a uno.
Questa strategia è stata usata per sequenziare il genoma di A.thaliana, H.sapiens e altri.
Ultimamente in Whole-Genome Shotgun si utilizza un MTP derivato da una mappa fisica per validare e migliorare la qualità dall'assemblaggio.

#### Marker e Mappe
Un marker è un sito unico nel genoma, tipicamente una sequenza. I marker sono utilizzati nella costruzione delle mappe.
Una mappa fornisce una guida per esperimenti di sequenziamento mostrando le posizioni dei marker genomici (geni e altro).

Per convenzione si dividono i metodi di mapping del genoma in 2 categorie:
- Genetic Mapping -> Si basa sull'utilizzo di tecniche genetiche per costruire mappe che mostrano la posizione dei geni ed altre sequenze sul genoma. Le tecniche genetiche includono cross-breeding, o l'esaminazione delle genealogie (pedigree) per gli umani.
- Physical Mapping -> Tecniche di biologia molecolare per esaminare le molecole di DNA direttamente per costruire mappe mostrando le posizioni di sequenze, inclusi geni
###  Genetic mapping
Una mappa genetica (linkage map) mostra la locazione relativa dei marker genetici (riflettendo siti di varianti genomiche) su un cromosoma.
Si basa sul linkage genetico -> Più vicini due marker sono su un cromosoma, più tenderanno a segregare insieme.
Studiando i pattern di ereditarietà possono essere stabiliti l'ordine relativo e la locazione dei marker genetici lungo un cromosoma.
I geni sono marker genetici, ma non sono ideali per il mapping. In genomi grandi, una mappa basata solo sui geni non sarà molto dettagliata. Inoltre nei genomi eucariotici i geni sono spesso estremamente sparsi nel genoma, con enormi gap tra loro.
Solo una frazione dei geni esiste in forma allelica, e può essere distinta convenientemente.
Feature mappate che non sono geni prendono il noem di DNA Marker. Come i geni, i DNA marker devono possedere almeno due alleli per essere utili.
Tre feature di sequenze DNA soddisfano questi requisiti:
- RFLP restriction fragment length polymorphism -> Alcune molecole presentano siti di restrizioni assenti in altre molecole. Un RFLP viene scoperto con il trattamento da enzimi di restrizione, dove una molecola con il sito in più verrà tagliata in un pezzo aggiuntivo rispetto l'altra
- SSLP simple sequence length polymorphism -> Sono Array di sequenze ripetute con differente lunghezza, i differenti alleli contengono differente numero di unità ripetute
- SNP single nucleotide polymorphism -> Posizioni nel genoma dove singoli individui presentano un Nucleotide mentre altri individui presentano altri nucleotidi. Ci sono almeno 1.5 milioni di SNP nel genoma umano, ed alcuni possono dare vita a RFLP, ma è raro perche la sequenza in cui si trovano spesso non è riconosciuta da enzimi di restrizione
La costruzione della mappa si basa sull'analisi linkage, motivo per cui i DNA marker devono essere eterozigoti. L'affidabilità di un marker è data dal PIC index


### Mappe fisiche
Una mappa genetica è raramente sufficiente per il sequenziamento diretto:
- La risoluzione dipende dal numero di Crossing-Over -> non è un problema per microorganismi, lo è per eucarioti in cui la riproduzione è lenta e non è possibile ottenere un gran numero di progenie, quindi possono essere studiate poche meiosi, e il potere della linkage analisi è abbastanza ristretto. Geni che si trovano a distanza elevata (decine di migliaiai di kb) possono apparire nella stessa posizione nella mappa genetica 
- Le mappe genetiche hanno accuratezza limitata -> I crossover avvengono più frequentemente in determinate zone invece di altre
Tecniche di mapping fisiche sono quindi necessarie. Una mappa fisica è una rappresentazione grafica dellle locazioni fisiche di marker e landmark (geni, DNA marker, varianti ecc...) all'iterno di un cromosoma o genoma
Una sequnza completa di un genoma è una tipologia di mappa fisica. Le mappe fisiche sono utilizzate per generare complete sequenze di un genoma

Tra le molte tecniche, le più importanti sono:
- Restriction mapping -> localizza posizioni relative su una molecola di DNA di sequenze di riconoscimento per endonucleasi di restrizione
- Fluorescent in situ hybridization -> locazione dei marker sono mappate per ibridizzazione di un probe contenente il marker con il cromosoma intatto
- Sequence tagged site STS mapping -> In cui le posizioni di corte sequenze sono mappate da PCR e/o analisi di ibridizzazione di frammenti del genoma

#### STS
È una delle più potenti tecniche di mapping fisico, e quella responsabile per la generazione delle mappe dettagliate di genomi grandi.
Una sequence tagged site o STS è una corta sequenza, tra 100 e 500 bp, facilmente riconoscibile e che appare una sola volta nel cromosoma o nel genoma studiato.
La PCR si usa per determinare quale framment contiene STSs.
Le STS si possono ottenere in diversi modi, i più comuni sono EST SSLP e random genomic sequences.
- EST Expressed sequence Tags -> corte sequenze ottenuta da analisi di cloni cDNA
- SSLP possono essere usati come STS in mapping fisico. SSLP polimorfici sono già stati mappati dalla linkage analisi e sono particolarme utili poichè danno una connessione diretta tra mappa genetica e mappa fisica
- Random genomic sequences -> Ottenuta sequenziando pezzi di DNA genoma clonato o scaricando sequenze depositate sui database


### Clone by Clone
Una volta definito il MTP, i cloni individuali come il BACK vengono selezionati, e un grande quantitativo di DNA BAC viene purificato. Il DNA purificato viene frammetanto da metodi di shearing fisico. I frammenti random di 2kb-5kb sono subclonati.
Le read poi vengono generate da una estremità o entrambe le estemità di subcloni selezionati a caso (migliaia di read per ogni BAC di 100-150kb).
Le read casuali poi vengono assemblate sulla base di overlap, portando ad un assmeblaggio preliminare (prefinished sequence).
Questa sequenza è imperfetta, viene associata sia a gap e sia a zone di qualità molto bassa. Ordine ed orientamento dei contig spesso non è noto.
Seguono metodi di sequence finishing, che coinvolgono la generazione di dati addizionali di sequenze per chiudere gap e migliorare la qualità di alcune zone.
Dopo questo step si ottiene la seuqnza finita e accurata di tutto il clone intero.


## Whole Genome Shotgun

Sequenze individuali generate da un Whole Genome Shotgun vengono inizialmente assemblate in contig.
I gruppi di contig vengono organizzati in scaffold sulla base di informazioni di linking date dalle coppie di read (per ogni caso, una read da una coppia si assembla in un conting e l'altra read in un altro contig).
Gli scaffold vengono allineati a turno relativamente al genoma di partenza per identificazione di marker sequence-based già mappati nel contig, associandoli con una locazione nota nel genoma
### Hybrid Shotgun
In approcci ibridi, si uniscono elementi del Clone-by-Clone e del Whole Genome Shotgun.
Una libreria di subcloni dal whole genome viene preparata, e numerose read vengono generate genome-wide.
Contemporaneamente, BAC individuali vengono sottoposte a shotgun sequencing.
Le read derivanti dal BAC possono esere usate per identificare sequenze in overlap nella grande collezione di whole-genome-derived reads, riducendo la complessità del dataset whole-genome shotgun in una serie di bin di dimensioni di un BAC.
L'insieme combinato di read per ogni bAC può poi essere assemblato individualmente ed è soggetto a sequence finishing.


## Ripetizioni
Le ripetizioni contenute nei genomi eucariotici rappresentano un grande ostacolo che complica l'assemblaggio. Queste sequenze arrivano a lunghezze in Kb, ripetute in almeno 2 posizioni nel genoma.
Quando un genoma contenente DNA ripetitivo viene rotto in frammenti, alcuni dei pezzi risultanti conterranno gli stessi motivi di sequenza.
Sarebbe semplice riassmblare queste sequenze cosi che il DNA tra coppie di ripetizioni venga trascurato, o anche connettere due pezzi separati su stesso o differente cromosoma. Una mappa genomica permette di evitare questo tipo di errori

## Ridodanza e Coverage
La Ridodanza indica quante volta una base è stata coperta.
Trovare nuove sequenze è un evento raro che segue Poisson. $P_0 = e^{-R}$  ovvero la probabilità di trovare una nuova base sequenziata dipende dalla ridodanza media.
L'equazione usta per calcolare il coverage del genoma è $$C = \frac{LN}{G}$$
C -> Coverage
L -> Read Length
G -> Lunghezza genoma (Aploide)
N -> Nr di Read

## Overlap
Le read in overalp vengono estese per ricostruire la regione genomica originale.
1. Si cerca overlap tra le sequenze primarie
2. Si assembllano in contig per ottenere corte sequenze consensus
3. L'assemblaggio di supercontig utilizzando le informazioni nelle coppie di sequenze (terminazioni + distanza)
4. Completamento della consensus

La regione sovrapposta è l'overlap. Regioni non allineati sono overhang.
L'assembler individua i merge in base a:
- Lunghezza overlap
- % identità nella regione di overlap
- dimensione dell'overhang

## Overlap Layout Consensus
1. Overlap -> Si cercano read in Overlap
2. Layout -> Si mergiano le read in contig e supercontig
3. Consensus -> Si costruisce la sequenza consensus e si correggono errori nelle read

Una strategia consiste nel considerare le read come nodi in un grafo, con gli archi che rappresentano allineamenti tra le read. Si percorre un cammino hamiltoniano seguendo gli archi in ordine numerico ricostruendo il genoma combinando gli allineamenti tra read successive.
Hamiltoniano -> Ogni nodo è attraversato 1 sola volta e termina al nodo di partenza. Ogni read verrà quindi inclusa una volta nell'assemblaggio -> NP-HARD

I vertici sono read o kmer, gli edge sono allineamenti pairwise.

Durante la fase layout cerchiamo di identificare la Shortest common superstring. Non è semplice dato che il grafo di overlap è grande.
Si inizia rimuovendo archi transivitevely inferred, parendo da archi che saltano uno o due nodi.

I contig ottenuto corrispondono a stretch non ramificanti.
In fase di layout bisogno anche tenere conto di sottografi spuri a causa di erori di sequenziamento.

Consensus
Si prendono le read che costituiscono un contig e si allineano. SI prende poi il voto consensus.

Svantaggi OLC
La costruzione del grafo di overlap è lenta. Dataset di sequenziamento contengono fino a miliardi di read, centinaia di miliardi di nucleotidi in totale.


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
- N50 size -> applicvabile a contig o scaffold
	- Dato un set di contig, N50 è definito come la lunghezza della sequenza del contig più corto al 50% della lunghezza totale del genoma
	- Uno svantaggio di N50 è che non tiene in considearzione la dimensione del genoma, quindi 2 assembly possono avere identiche N50 dimensioni ma rappresentare differenti gradi di completezza del genoma
- NG50 aggira il problema permettendo comparazione diretta tra assembly genomiche di differente specie

### Genoma T2T
Il genoma reference umano copre solo le regioni eucromatiche del genome, lasciando importanti regioni eterocromatiche non finite. La rimanente parte 8% del genoma è stata completata dal consorzio T2T. 3.055 miliardi di base pair sequence che include assembly gapless per ogni cromosoma eccetto l'Y, correggendo errori in referenze precedenti, e introducendo quasi 200 milioni di bp di sequenza contenente 1956 predizioni di gene, 99 dei quali sembrano essere protein-coding.
Le regioni completate includono tutti gli array satellite centromerici, duplicazioni segmentali ed il braccio corto di tutti e 5 i cromosomi acrocentrici.
Per terminare le ultimi regioni del genoma, aspetti complementari di sequenziamento PacBio (20kbp) e ONT ultralong read (>100kbp) sono state prese in considerazione per assemblare l'uniformemente omozigote CHM13hTERT cell line (46,XX).
