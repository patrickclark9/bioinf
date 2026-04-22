# Gene Prediction

I metodi di Gene prediction sono utilizzato per annotare lunghe sequenze contigue generate da Whole Genome Sequencing.
La maggior parte dei programmi usati per questo scopo hanno come obiettivo il predire l'intera struttura esone-introne dei trascritti protein-coding.
I risultati sono distribuiti attraverso i genome browser.
Porcarioti ed eucarioti presentano strutture geniche differenti, quidni sono necessarie diverse strategie


## Strategie 
- Estrinseca similarity based -> I metodi similarity base utilizzano similarità di annotazioni come proteine, cDNA ETS, utilizzando BLAST. Questi metodi non identificano geni nuovi, ma funzionano solo per geni presenti già nel database. Fondamentalmente si va a blastare la sequenza in ricerca di annotazioni conosciute con sequenze simili alla query. Errori nel database sono un grosso problema, oltre al fatto che i confini della similarità non sono esattamente ben definit
- Comparativa -> I metodi comparativi utilizzano la similarità tra genoma attraverso una comparazione diretta. Vanno ad individuare geni evolutivamente conservati. Anche qui i confini esatti della similarità non sono ben definiti. Soffrono anche questi di problemi in erorri nelle annotazione del genoma reference. In teoria però dovrebbero produrre evidenza di geni biologicamente rilevanti. tblastx e blastn sono comunemente utilizzato per identificare esoni candidati negli umani utilizzando il genoma del topo. È complicato trovare la distanza evolutiva ottimale dal genoma di riferimento, ovvero pattern di conservazione differiscono tra i diversi loci
- Intrinseca ab initio -> Non usano similarità o comparazioni su genoma. Identificano geni nella sequenza del genoma primario utilizzando Content Sensor e Signal Sensors intrinseci.
	- Content sensor: Misure che cercano di classificare una data regione di DNA in tipi, coding vs non coding. Si cerca di discrimanre regioni coding da non coding in eucarioti in base a differenze statistiche tra la composizione della sequenza di queste due regioni. Molte misure per discrimanre segmenti coding (coding potential) sono state investigate. Alcune misurazioni sono ampiamente utilizzate e sono empiricamente efficaci (nt composition -> G/C rich o A/T rich, codon composition, hexamer frequency). Combinazioni di diverse misurazioni possono risultare molto efficaci
		- Estrinseco: Sensori trovati per ricerche basate sulla similarità
		- Intrinseco: Rilevati da metodi predittivi 
	- Signal Sensor: Misure che cercano di rilevale la presenza di siti funzionali specifici per un gene. Sono specifici siti funzionali all'interno o nei confini di varie regioni genomiche e sono coinvolti in diversi livelli di espressione di geni protein-coding. Per esempio, i transcription factor binding site, TATA box, siti donatori e accettori, branch point, poli(A) site, initiation site, codoni di stop. Questi segnali possono esssere trovati utilizzati tramite una varietà di metodi computazionali come la consensus-sequence allineamento multiplo-based, PWM (positional weight matrices) o Modelli di Markov probabilistici altamente complessi
	- Intron Phase -> ![[Pasted image 20260422161723.png]]
- Integrata

Human Gene structure -> ![[Pasted image 20260422161856.png]]

### Assessment

Sensitività = tp/tp+fn -> nr esoni corretti / nr esoni reali
Specificità = tp/tp+fp -> nr esoni corretti/ nr esoni predetti
MissingSensitività = tp/tp+fn -> nr esoni mancanti / nr esoni reali
MissingSpecificità = tp/tp+fp -> nr esoni Sbagliati/ nr esoni predetti

Coefficienti di coorelazione
Correlazione approssimata

### Formati GFF e GTF

Il gene transfer format e il general feature format sono due comuni formati di file utilizzati per la rappresentazione di dati genomici, utilizzati ampiamente in diversi aspetti della ricerca per la loro abilità nel rappresentare dati genomici complessi in un formato standardizzato.
I file GFF sono comunemente utilizati nel mapping, nell'annotazione e nella genomica comparativa. Ci danno una visione comprensiva delle feature genomiche tra DNA RNA e proteine.
I file GTF sono particolarmente utili nello studio dell'espressione genica come RNA-seq e analisi del trascrittoma.
GFF:
1. seqID -> nome sequenza
2. Source -> algoritmo o procedura utilizzata per generare la sequenza. tipicamente software o database
3. Type -> feature type, "gene" " exon" "CDS" "5'UTR", "3' UTR". In un GFF ben strutturato tutte le feature figlie seguono ii parenti in un singolo blocco (tutti gli esoni di un trascritto seguono immediatamente il parente "transcritp" , prima di ogni altro "transcript" parente. Tutte le feature e le relazioni dovrebbero essere compatibile con sstandard del Sequence Ontology Project)
4. Start -> Genomic start della feature, con offset di 1 base, in contrasto ad altri formati come il BED che hanno offset 0
5. End -> Genomic end della feature con 1 base di ofset
6. Score -> Valore numerico che indica la confidenza della sorgente nella feature annotata. Il punto "." indica un valore nullo
7. Strand -> singolo carattere. Può essere + (5'->3'), - (3'->5'), "." indica valore nullo, ? per feature in cui la strand è rilevante ma sconosciuta
8. Phase -> Fase di una CDS, 0,1,2 per una CDS, "." per tutto il resto.
9. Attributes -> Lista di tag-valore coppie separate da un ";" puntoe virgola con informazioni aggiuntiva

Il GTF ha strutura simile al GFF: <seqname><source><feature><start><end><score><strand><frame><attributes>
Ogni attributo di attribute deve avere forma: nome_atributo "valore attributo";.
gene_id -> identificatore unico per la sorgente genomica del trasccritto. Usato per raggruppare i trascritti in geni.
transcript_id -> identificatore unico per il trascritto predetto. Utilizzato per raggruppare feature per trascritto



### Bed
I file bed contengono un singolo record per linea e sono facilmente parsabili, computazionalmente semplici da parsare.
Ogni riga è un record completo.
Minimo 3 colonne per riga, con 9 aggiuntive colonne opzionali.
Invece del sistema a coordinate utilizato da GFF e GTF, il sistema bed è zero based per coordinate start e 1-based per coordinate end. Quindi un nucleotide con coordinata 1 un nel gnoma avrà start = 0 ed end = 1.
1. Chrom -> cromosoma o scaffold
2. chromStart -> coordinata di inizio sul cromosoma o sullo scaffold per la sequenza considerata
3. chromEnd -> coordinata di terminazione sul cromosoma o scaffold. La posizione è non inclusiva, a differenza di chromStart.
4. name -> nome della riga del bed
5. score -> score tra 0 e 1000
6. strand -> +,