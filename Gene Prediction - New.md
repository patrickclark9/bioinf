# Gene Prediction

I metodi di gene prediction vengono utilizzati per annotare lunghe sequenze contigue generate dal Whole Genome Sequencing. La maggior parte dei programmi ha come obiettivo il predire l'intera **struttura esone-introne** dei trascritti protein-coding. I risultati sono distribuiti attraverso i **genome browser**.

Procarioti ed eucarioti presentano strutture geniche differenti, quindi sono necessarie strategie diverse.

---

## Strategie

### Estrinseca (Similarity-Based)

Utilizza la similarità con annotazioni già note (proteine, cDNA, EST) tramite **BLAST**. Non identifica geni nuovi: funziona solo per geni già presenti nel database.

**Limiti:**

- Non identifica geni nuovi
- Errori nel database si propagano nell'annotazione
- I confini della similarità non sono ben definiti

**Vantaggio**: produce evidenza di geni biologicamente rilevanti, poichè ci si basa su dati biologici pre-esistenti

---

### Comparativa

Utilizza la similarità tra genomi attraverso comparazione diretta, individuando geni **evolutivamente conservati**. `tblastx` e `blastn` sono comunemente usati per identificare esoni candidati negli umani usando il genoma del topo.

**Limiti:**

- I confini esatti della similarità non sono ben definiti
- Soffre degli stessi problemi di errori nelle annotazioni nel genoma di riferimento
- Difficoltà nel trovare la **distanza evolutiva ottimale** dal genoma di riferimento (i pattern di conservazione differiscono tra i diversi loci)

**Vantaggio**: produce evidenza di geni biologicamente rilevanti.

---

### Intrinseca (Ab initio)

Non usa similarità né comparazioni genomiche. Identifica geni nella sequenza primaria utilizzando due tipi di sensori:

#### Content Sensor

Cercano di classificare una regione di DNA come **coding vs non-coding**, discriminando le due tipologie in base a differenze statistiche nella composizione della sequenza.

Misurazioni comunemente usate (combinazioni sono particolarmente efficaci):

|Misurazione|Descrizione|
|---|---|
|Composizione nucleotidica|GC-rich vs AT-rich|
|Codon composition|Frequenza di utilizzo dei codoni|
|Hexamer frequency|Frequenza di esanucleotidi specifici|

I content sensor si distinguono ulteriormente in:

- **Estrinseci** — trovati tramite ricerche basate sulla similarità
- **Intrinseci** — rilevati da metodi predittivi

#### Signal Sensor

Cercano di rilevare la presenza di **siti funzionali specifici** all'interno o ai confini di regioni genomiche, coinvolti nell'espressione di geni protein-coding.

Esempi di segnali rilevati:

- Transcription factor binding sites
- TATA box
- Siti donatori e accettori di splicing
- Branch point
- Sito di poli(A)
- Initiation site
- Codoni di stop

Metodi computazionali utilizzati per la ricerca di signal sensor:

- Consensus-sequence con allineamento multiplo
- **PWM** (Positional Weight Matrices)
- Modelli di Markov probabilistici

#### Signal Sensors - Introns

![[Pasted image 20260422172809.png]]
#### Intron Phase

![[Pasted image 20260422161723.png]]

---

### Integrata

Combina elementi delle strategie estrinseca, comparativa e ab initio per migliorare la predizione complessiva.

---

## Struttura del Gene Umano

![[Pasted image 20260422161856.png]]

---

## Assessment della Gene Prediction

| Metrica                     | Formula              | Significato                            |
| --------------------------- | -------------------- | -------------------------------------- |
| **Sensitività**             | $\frac{tp}{tp + fn}$ | Nr esoni corretti / Nr esoni reali     |
| **Specificità**             | $\frac{tp}{tp + fp}$ | Nr esoni corretti / Nr esoni predetti  |
| **Missing Sensitivity**     | $\frac{fn}{tp + fn}$ | Nr esoni mancanti / Nr esoni reali     |
| **Missing Specificity**     | $\frac{fp}{tp + fp}$ | Nr esoni sbagliati / Nr esoni predetti |
| **Correlation Coefficient** |                      |                                        |
| **Approximate Correlation** |                      |                                        |

---

## Formati di File Genomici

### GFF (General Feature Format)

Comunemente utilizzato per mapping, annotazione e genomica comparativa. Fornisce una visione comprensiva delle feature genomiche tra DNA, RNA e proteine.

|Campo|Descrizione|
|---|---|
|**seqID**|Nome della sequenza|
|**Source**|Algoritmo o procedura utilizzata per generare la feature (software o database)|
|**Type**|Tipo di feature: `gene`, `exon`, `CDS`, `5'UTR`, `3'UTR`. In un GFF ben strutturato tutte le feature figlie seguono il parente in un singolo blocco|
|**Start**|Coordinata genomica di inizio della feature — **1-based** (offset di 1 base)|
|**End**|Coordinata genomica di fine della feature — **1-based**|
|**Score**|Confidenza nella feature annotata. `.` indica valore nullo|
|**Strand**|`+` (5'→3'), `-` (3'→5'), `.` (nullo), `?` (rilevante ma sconosciuto)|
|**Phase**|Fase di una CDS: `0`, `1`, `2`. `.` per tutto il resto|
|**Attributes**|Lista di coppie tag-valore separate da `;` con informazioni aggiuntive|

> Le feature e le relazioni devono essere compatibili con gli standard del **Sequence Ontology Project**.

---

### GTF (Gene Transfer Format)

Struttura simile al GFF, particolarmente utile per studi di espressione genica come **RNA-seq** e analisi del trascrittoma.

Formato: `<seqname> <source> <feature> <start> <end> <score> <strand> <frame> <attributes>`

Ogni attributo deve avere la forma: `nome_attributo "valore_attributo";`

Attributi principali:

|Attributo|Descrizione|
|---|---|
|**gene_id**|Identificatore unico per la sorgente genomica del trascritto. Usato per raggruppare trascritti in geni|
|**transcript_id**|Identificatore unico per il trascritto predetto. Usato per raggruppare feature per trascritto|

---

### BED (Browser Extensible Data)

Formato semplice e computazionalmente efficiente. Ogni riga è un record completo, con **minimo 3 colonne** e fino a 9 colonne opzionali.

> Il sistema di coordinate BED è **0-based per chromStart** e **1-based per chromEnd**. Un nucleotide in posizione 1 nel genoma avrà `start = 0` e `end = 1` — a differenza di GFF/GTF che usano coordinate 1-based.

| #   | Campo           | Descrizione                                                                                  |
| --- | --------------- | -------------------------------------------------------------------------------------------- |
| 1   | **chrom**       | Cromosoma o scaffold                                                                         |
| 2   | **chromStart**  | Coordinata di inizio (0-based, inclusiva)                                                    |
| 3   | **chromEnd**    | Coordinata di fine (1-based, **non inclusiva**)                                              |
| 4   | **name**        | Nome della riga                                                                              |
| 5   | **score**       | Score tra 0 e 1000                                                                           |
| 6   | **strand**      | `+`, `-` o `.`                                                                               |
| 7   | **thickStart**  | Coordinata da cui l'annotazione viene visualizzata in grassetto (es. codone di start)        |
| 8   | **thickEnd**    | Coordinata da cui l'annotazione non viene più visualizzata in grassetto (es. codone di stop) |
| 9   | **itemRGB**     | Valore RGB per il colore di visualizzazione dell'annotazione                                 |
| 10  | **blockCount**  | Numero di blocchi nella riga (es. numero di esoni)                                           |
| 11  | **blockSizes**  | Lista CSV delle dimensioni dei blocchi (deve corrispondere a blockCount)                     |
| 12  | **blockStarts** | Lista CSV degli inizi dei blocchi, relativi a chromStart (deve corrispondere a blockCount)   |