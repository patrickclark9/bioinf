# Indicizzazione (Indexing)

L'indicizzazione rappresenta una delle sfide più grandi per effettuare ricerca e trovare la regione mappata con elevata accuratezza.

Gli indici possono essere:

- **Invertiti** (word → locazione)
- **Forward** (locazione → word)

Algoritmi efficienti di indicizzazione sono essenziali per organizzare le sequenze del genoma di riferimento e le short read in memoria, e per consentire ricerche rapide di pattern.

### Principio generale

Dato un indice $T$ e una query $Q$:

1. Si spezza la query in sottostringhe definite
2. Si esplora l'indice $T$ per verificare se le sottostringhe sono presenti
3. Se presenti, si estende per verificare se l'intera sequenza ha un match

> Un indice per il solo cromosoma 1 umano può occupare fino a **12 GB**. Una soluzione pratica per ridurre lo spazio è saltare alcune sottostringhe durante la creazione dell'indice (es. includere ogni 4a sottostringa può ridurre 12 GB a 8 GB).

### Strutture dati principali

|Struttura|Spazio (genoma umano)|Note|
|---|---|---|
|Hash Table|Variabile|Accesso O(1) per chiave esatta|
|Suffix Tree|~47 GB|Potente ma molto pesante|
|Suffix Array|~12 GB|Più compatto del suffix tree|
|BWT + FM-index|Molto compatto|Comprimibile, reversibile, ricercabile|

---

## Hash Table

Si costruisce una struttura stile dizionario in cui ogni sottostringa è una **chiave** a cui corrispondono i **valori delle posizioni** in cui quella chiave appare nel testo.

---

## Trees e Tries

### Trie a lunghezza fissa

Si costruisce un indice usando sottostringhe di lunghezza fissa (es. lunghezza 2, saltando ogni altra sottostringa). La lista ordinata viene convertita in una **trie**, che mappa ogni sottostringa alla sua posizione (offset).

Proprietà di ogni trie:

- Ogni **arco** è etichettato con un carattere dell'alfabeto
- Ogni **nodo** ha un singolo arco uscente per ogni carattere dell'alfabeto
- Ogni **chiave** (sottostringa) si estende lungo un percorso dalla radice

### Suffix Trie

Un'estensione più potente: invece di sottostringhe a lunghezza fissa, si usano tutti i **suffissi** della stringa.

Prendendo $T = \text{abaaba\$}$, dove `$` marca la terminazione:

- Ogni suffisso è rappresentato da un percorso dalla radice a una foglia
- Il carattere `$` garantisce che ogni suffisso abbia un percorso unico (senza il `$`, alcuni suffissi non avrebbero percorsi distinti)
- Ogni nodo è etichettato con la stringa formata da tutti i caratteri lungo il cammino dalla radice al nodo

La suffix trie permette di:

- Verificare rapidamente se un pattern è presente nel testo
- Verificare se una stringa è suffisso del testo
- Contare quante volte una sottostringa appare nel testo

### Suffix Tree

Collassando tutti i **percorsi non ramificanti** nella suffix trie e concatenando le etichette, si ottiene il **suffix tree**: ogni foglia è etichettata con l'offset del corrispondente suffisso.

La logica è uguale alla suffix trie, con la differenza che lungo alcuni archi solo una **porzione** dei caratteri dell'etichetta combacerà durante la ricerca.

> **Applicazione comune**: trovare la più lunga sottosequenza comune tra due sequenze genomiche.

**Svantaggio**: occupa ~**47 GB** per il genoma umano intero.

---

## Suffix Array

Il suffix array offre una soluzione più **compatta** rispetto al suffix tree. Specifica un **ordine lessicografico** ordinando tutti i suffissi derivati dal testo $T$.

Non richiede una struttura ad albero per la rappresentazione → utilizza vastamente meno memoria:

| Struttura    | Spazio |
| ------------ | ------ |
| Suffix Tree  | ~47 GB |
| Suffix Array | ~12 GB |

---

## Burrows-Wheeler Transform (BWT)

La BWT è una **permutazione reversibile** di una stringa con tre caratteristiche fondamentali che la rendono ideale per rappresentazioni compatte di dati genomici:

1. **Comprimibile** — la stringa trasformata è facilmente comprimibile
2. **Invertibile** — può essere invertita per ricostruire la stringa originale
3. **Ricercabile** — può essere usata direttamente come indice

### Costruzione della BWT

1. Si aggiunge `$` alla fine della stringa
2. Si generano tutte le rotazioni della stringa
3. Si ordinano le rotazioni lessicograficamente (**T-Ranking**)
4. La BWT è l'**ultima colonna** (L) della matrice ordinata; la **prima colonna** (F) contiene i caratteri in ordine lessicografico

> L'ordine del ranking viene mantenuto coerentemente tra la prima colonna (F) e l'ultima colonna (L).

### LF Mapping (ricostruzione)

Il **mapping LF** permette di ricostruire il testo originale dalla BWT. Si legge da destra verso sinistra:

1. Si inizia dalla prima riga → F contiene `$`, L contiene il carattere immediatamente prima di `$` (es. `a₀`)
2. LF indica a quale riga in F corrisponde quella occorrenza in L
3. Si salta alla riga corrispondente in F e si legge il nuovo carattere in L
4. Si ripete fino a raggiungere `$`

Il mapping LF può essere usato anche per **ricercare una sottostringa** nella BWT: si verifica se il range di righe che iniziano con il pattern si restringe ad un insieme non vuoto.

> **Esempio**: cercare `aba` nella BWT restringerà progressivamente il range. Cercare `bba` non produrrà alcun match se la stringa non è presente.

### Svantaggi della BWT

- Difficoltà nel determinare **dove** si trovano i match nel genoma (la BWT da sola non fornisce le posizioni)
- Alcune limitazioni di prestazioni su certi pattern

---

## FM-Index (Full-text index in Minute space)

Combinare la BWT con strutture dati ausiliarie produce l'**FM-index**, che risolve il problema della localizzazione dei match.

Le componenti dell'FM-index utilizzate per allineare read al genoma sono:

| Componente       | Funzione                                                                                                          |
| ---------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Tally**        | Conta le occorrenze cumulative di ogni carattere dall'inizio della colonna L                                      |
| **Checkpoints**  | Sottoinsieme del Tally salvato a intervalli regolari per risparmiare spazio                                       |
| **Suffix Array** | Una volta trovata la sottostringa, la sua posizione nel genoma si trova al corrispondente indice nel Suffix Array |

---
## Graph FM Index
Il genome di riferimento hg38 non include varianti genomiche della popolazione umana.
Protocolli di allineamento del sequenziamento basati su questo singolo genoma di reference sono a volte non in grado di allineare le read correttaemnte, specialmente quando il genoma di partenza è distante dalla reference.
Di base la reference potrebbe anche non contenere le varianti più comuni per locus
L'algoritmo HISAT2 implementa una struttura dati a grafo chiamata GraphFM index.

Assumendo una sequenza di 6 bp, contenente SNP e indel.
Creiamo la rappresentazione grafica della sequenza + varianti.
Segue uno step di prefix doubling e pruning delle ramificazioni.
Questa è una tecnica di compressione in cui prima si individuano tutti path di lunghezza 1.
Dopo i path di lunghezza 1 si identificano tutti i path di lunghezza 2, 4,8  cosi via.
Conoscendo il cammino ordinato di lunghezza k, possiamo identificare i cammini di lunghezza 2k concatenandoli e ordinando i risultati.
Il processo continua ifnchè la lunghezza del cammino è >= alla lunghezza della read da mappare.
Il prefix doubling consiste del creare altri prefissi per i diversi percorsi, ottenendo un indice compresso di tutti i possibili cammini attraverso il grafo fino ad una specifica lunghezza.
Infine si crea una rappresentazione tabulare dei grafi ordinati per prefisso.
La ricerca inizia leggendo la read, una volta raggiunto un nodo del grafo con molteplici nodi entranti o uscenti, vengono attraversati tutti i percorsi contemporaneamente. Viene mantenuto un insieme di nodi attivi, ovvero nodi che matchano la read, e si esplorano tutti. 


# Formato SAM/BAM

Il formato **SAM** (Sequence Alignment/Map) è un formato tab-delimited composto da:

- Una sezione **header** (opzionale)
- Una sezione **allineamento**

Ogni allineamento ha **11 campi mandatori** per le informazioni essenziali (posizioni di mappaggio, ecc.) e diversi **campi opzionali** per informazioni specifiche.

---

## Campi Mandatori

|Campo|Descrizione|
|---|---|
|**QNAME**|Read ID|
|**FLAG**|Informazioni sull'allineamento (vedi sotto)|
|**RNAME**|Reference sequence name|
|**POS**|Posizione 1-based nel reference|
|**MAPQ**|Mapping quality|
|**CIGAR**|Riassunto dell'allineamento: inserzioni, delezioni, ecc. (vedi sotto)|
|**RNEXT**|Reference sequence name dell'allineamento primario della read accoppiata. Corrisponde a RNAME per il paired-end|
|**PNEXT**|Posizione dell'allineamento primario della read accoppiata. `0` quando non disponibile. Corrisponde a POS|
|**TLEN**|Numero di basi coperte dalle read dello stesso frammento. `+/-` indica se la read attuale è la più a sinistra/destra|
|**SEQ**|Sequenza della read|
|**QUAL**|Qualità della read. `*` indica non disponibile|

---

## FLAG

Il FLAG è un valore decimale che rappresenta un **numero binario a 12 bit**, dove ogni bit rappresenta un attributo diverso (`0` = false, `1` = true).

> **Esempio**: valore decimale `3` → `000000000011` → solo i primi due bit sono attivi → la read è paired-end ed è allineata appropriatamente (entrambe le read della coppia sono orientate una verso l'altra, sullo stesso contig e a distanza attesa).

Nota importante: il bit alla posizione 8 indica che la read è un **allineamento secondario** — ovvero ha molteplici potenziali allineamenti e quello corrente non è la prima scelta tra quelli disponibili.

---

## CIGAR

Il campo CIGAR riassume l'allineamento con una stringa di operatori, ognuno preceduto dal numero di nucleotidi a cui si applica.

> **Esempio**: `2S5M` → i primi 2 nt sono soft-clippati, i successivi 5 nt sono match.

|Operatore|Significato|
|---|---|
|`M`|Alignment match|
|`I`|Insertion rispetto al reference|
|`D`|Deletion rispetto al reference|
|`N`|Skipped region dal reference|
|`S`|Soft clipping (sequenza clippata **presente** in SEQ)|
|`H`|Hard clipping (sequenza clippata **non presente** in SEQ)|
|`P`|Padding (silent deletion da reference paddato)|
|`=`|Sequence match|
|`X`|Sequence mismatch|

---

## Campi Opzionali

Formato: `TAG:TYPE:VALUE`

- Ogni tag può apparire **una sola volta** ed è una stringa di **2 caratteri**
- L'ordine dei campi opzionali non è importante

|TYPE|Tipo di dato|
|---|---|
|`A`|Carattere|
|`C`|Intero 8-bit|
|`f`|Numero reale|
|`H`|Array esadecimale|
|`i`|Intero 32-bit|
|`Z`|Stringa|
