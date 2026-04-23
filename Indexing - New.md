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

|Componente|Funzione|
|---|---|
|**Tally**|Conta le occorrenze cumulative di ogni carattere dall'inizio della colonna L|
|**Checkpoints**|Sottoinsieme del Tally salvato a intervalli regolari per risparmiare spazio|
|**Suffix Array**|Una volta trovata la sottostringa, la sua posizione nel genoma si trova al corrispondente indice nel Suffix Array|

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


## Formato SAM/BAM

Il formato SAM sta per sequence alignment/map format. È un formato tab-delimited che consiste in una sezione header, opzionale, una sezione allineamento.
Ogni allineamento ha 11 campi mandatori per informazioni di allineamento essenziali, come mappaggio delle posizioni, e diversi campi opzionali per informazioni allineamento-specifiche o generali.

- QNAME -> readID
- FLAG -> Informazioni sull'allineamento della read: paired aligned: Il flagscore è un decimale usato per rappresentare un binario specifico. Il flag sono 12bit, in cui ogni bit rappresenta un attributo diverso, con 0 = false e 1 = true. Un valore decimale di 3 corrisponde a 000000000011, quindi flippati solo i bit corrispondenti a pair-end read e allineate appropriatamente, dove appropriatamente significa che entrambe le read in una coppia sono orientate una verso l'altra (fwd, rvrs), sullo stesso contig e sono a distanza attesa l'una dall'altra. Altra nota è il flag all'ottavo bit che significa che la read è un allineamento secondario. In questo caso secondario fa riferimento al fatto che ha molteplici potenziali allineamenti e che questo non è la prima scelta tra tutti quelli disponibili. Valori decimali corrispondono ad un preciso bit flipping, e quindi ad una serie precisa di flag
- RNAME -> Reference sequence name
- POS -> 1-based position
- MAPQ -> Mapping quality
- CIGAR -> Riassunto dell'allineamento: inserzioni, delezioni
- RNEXT -> reference sequence name dell'allineamento primario della NEXT read. per pair-end sequencing, NEXT read è la read paired, corrispondente alla colonna RNAME
- PNEXT -> Posizione dell'allineamento primario della NEXT read nel template. 0 quando non disponibile. Corrisponde alla colonna POS
- TLEN -> Numero di basi coperte da read dello stesso frammento. +/- significa che la read attuale è la più a sinistra/destra. E.g. comparazione tra prima e ultima riga.
- SEQ -> la sequenza della read
- QUAL -> La qualità della read. * significa che non è disponibile
- Optional Fields TAG\:TYPE\:VALUE