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