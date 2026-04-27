# Algoritmi di Allineamento — Approfondimento

---

## Needleman-Wunsch (Allineamento Globale)

### Idea di fondo

Needleman-Wunsch (1970) è un algoritmo di **programmazione dinamica** che garantisce di trovare l'allineamento globale **ottimale** tra due sequenze. "Globale" significa che l'allineamento si estende per l'intera lunghezza di entrambe le sequenze — ogni residuo deve essere allineato con qualcosa (un altro residuo oppure un gap).

Il principio chiave della programmazione dinamica applicata qui è la **sottostruttura ottimale**: l'allineamento ottimale fino alla posizione $(i, j)$ può essere calcolato in modo efficiente se si conoscono già le soluzioni ottimali per le posizioni precedenti. Questo evita la ricerca esaustiva di tutti i possibili allineamenti, che cresce esponenzialmente.

---

### Setup della matrice

Date due sequenze:
- **Sequenza A** di lunghezza $m$: $a_1, a_2, \ldots, a_m$ (sulle colonne)
- **Sequenza B** di lunghezza $n$: $b_1, b_2, \ldots, b_n$ (sulle righe)

Si costruisce una matrice $F$ di dimensioni $(n+1) \times (m+1)$. La prima riga e la prima colonna vengono inizializzate con multipli della penalità di gap:

$$F(i, 0) = i \cdot d \quad \text{e} \quad F(0, j) = j \cdot d$$

dove $d$ è la penalità per l'apertura/estensione di un gap (valore negativo). Questo riflette il costo di allineare $i$ residui di B con dei gap, o $j$ residui di A con dei gap.

---

### Funzione di ricorrenza

Per ogni cella $(i, j)$ con $i \ge 1$ e $j \ge 1$, lo score viene calcolato come:

$$F(i,j) = \max \begin{cases} F(i-1,\, j-1) + s(a_j,\, b_i) & \text{(match/mismatch: diagonale)} \\ F(i-1,\, j) + d & \text{(gap in A: su)} \\ F(i,\, j-1) + d & \text{(gap in B: sinistra)} \end{cases}$$

Dove $s(a_j, b_i)$ è lo score di sostituzione per la coppia di residui, ricavato dalla matrice di scoring (es. BLOSUM62). Ogni cella tiene traccia anche da quale delle tre direzioni proviene lo score massimo — questo viene salvato nella **traceback matrix**.

---

### Gap Penalty: lineare vs affine

La penalità di gap più semplice è **lineare**: un gap di lunghezza $k$ costa $k \cdot d$.

Tuttavia biologicamente non è realistico: aprire un nuovo gap è molto più raro evolutivamente che estenderne uno già aperto. Per questo si usa spesso la **penalità affine**:

$$\text{Gap cost} = d + (k-1) \cdot e$$

dove:
- $d$ = penalità di apertura del gap (gap open, es. −11)
- $e$ = penalità di estensione del gap (gap extend, es. −1)
- $k$ = lunghezza del gap

Con la penalità affine la funzione di ricorrenza si complica: si devono mantenere tre matrici separate ($M$, $I_x$, $I_y$) che tengono traccia rispettivamente dello stato di match/mismatch, di un gap aperto in A, e di un gap aperto in B.

---

### Traceback

Una volta riempita tutta la matrice, lo **score ottimale dell'allineamento globale** si trova nella cella $F(n, m)$ (in basso a destra).

Si ricostruisce l'allineamento seguendo a ritroso i puntatori salvati durante il riempimento:
- **Diagonale** → match o mismatch (si aggiunge $a_j$ allineato a $b_i$)
- **Su** → gap in A (si aggiunge $-$ in A, $b_i$ in B)
- **Sinistra** → gap in B (si aggiunge $a_j$ in A, $-$ in B)

Il traceback parte da $F(n,m)$ e termina in $F(0,0)$.

> ⚠️ Possono esistere **più allineamenti ottimali** con lo stesso score massimo, se in alcune celle ci sono pareggi tra le tre direzioni.

---

### Complessità

| | Complessità |
|---|---|
| Tempo | $O(mn)$ |
| Spazio | $O(mn)$ per la matrice completa; $O(\min(m,n))$ con l'algoritmo di Hirschberg |

---

### Quando usarlo

Needleman-Wunsch è ideale quando:
- Le due sequenze hanno lunghezza simile
- Si assume che siano omologhe lungo tutta la loro estensione
- Si confrontano sequenze della stessa famiglia proteica o ortologhi

Non è adatto quando una sequenza è molto più corta dell'altra, o quando si cerca un dominio/motivo conservato all'interno di una sequenza più lunga.

---

## Smith-Waterman (Allineamento Locale)

### Idea di fondo

Smith-Waterman (1981) è la versione **locale** di Needleman-Wunsch. Invece di allineare le sequenze per tutta la loro lunghezza, trova la **sottosequenza comune di score massimo** — ovvero la regione di maggiore similarità tra le due sequenze, ignorando il resto.

Questo è fondamentale quando, ad esempio, si confrontano due proteine che condividono solo un dominio funzionale conservato, ma divergono nel resto della struttura.

---

### Modifiche rispetto a Needleman-Wunsch

La funzione di ricorrenza diventa:

$$H(i,j) = \max \begin{cases} 0 & \text{(reset: nessun allineamento negativo)} \\ H(i-1,\, j-1) + s(a_j,\, b_i) & \text{(match/mismatch)} \\ H(i-1,\, j) + d & \text{(gap in A)} \\ H(i,\, j-1) + d & \text{(gap in B)} \end{cases}$$

L'unica differenza chiave rispetto a Needleman-Wunsch è l'introduzione dello **0** come opzione. Questo ha due effetti fondamentali:

1. **Nessuno score può diventare negativo** — se continuare un allineamento peggiora lo score, si preferisce ricominciare da capo.
2. **L'allineamento "dimentica" le regioni poco simili** — ogni cella rappresenta il miglior allineamento locale che *termina* in quella posizione.

Anche l'**inizializzazione** cambia: la prima riga e la prima colonna sono tutte inizializzate a 0 (non a multipli di $d$), perché l'allineamento locale può iniziare ovunque.

---

### Traceback

Lo score ottimale si trova nel **valore massimo nell'intera matrice** $H$ (non necessariamente nell'angolo in basso a destra). Il traceback parte da questa cella massima e procede a ritroso seguendo i puntatori fino a raggiungere una cella con valore **0** — qui termina l'allineamento locale ottimale.

Questo permette di identificare la regione di massima similarità indipendentemente dalla sua posizione nelle due sequenze.

---

### Confronto diretto NW vs SW

| Caratteristica | Needleman-Wunsch | Smith-Waterman |
|---|---|---|
| Tipo | Globale | Locale |
| Inizializzazione | $F(i,0) = i \cdot d$ | $H(i,0) = 0$ |
| Ricorrenza | Max di 3 valori | Max di 4 valori (include 0) |
| Score ottimale | Cella $(n,m)$ | Cella con valore massimo in $H$ |
| Inizio traceback | $(n,m)$ | Cella con score massimo |
| Fine traceback | $(0,0)$ | Prima cella con valore 0 |
| Score negativi | Possibili | Mai (azzerati) |
| Uso tipico | Sequenze omologhe globalmente | Ricerca di domini/motivi |

---

### Limitazione pratica

Entrambi gli algoritmi hanno complessità $O(mn)$ in tempo e spazio. Per database di milioni di sequenze, questo è **proibitivamente lento**. Smith-Waterman su un intero database come UniProt richiederebbe settimane su un singolo core. Per questo motivo sono stati sviluppati algoritmi euristici come FASTA e BLAST, che approssimano l'allineamento locale in tempi molto più brevi, sacrificando la garanzia di ottimalità.

> **Nota**: Implementazioni accelerate di Smith-Waterman su GPU (es. SWIPE, CUDASW++) riescono a raggiungere velocità competitive con BLAST mantenendo l'ottimalità, ma rimangono impraticabili per ricerche quotidiane su database di grandi dimensioni.

---

## FASTA

### Contesto storico

FASTA (Pearson & Lipman, 1988) è stato il primo algoritmo pratico per la ricerca rapida di similarità su database di sequenze biologiche. Precede BLAST ed è costruito sull'osservazione che sequenze simili condividono **parole esatte** (k-tuple) in posizioni vicine. Invece di calcolare l'allineamento ottimale per ogni coppia query-database, FASTA usa queste parole come "segnali rapidi" per identificare candidati promettenti prima di fare un allineamento rigoroso.

---

### Passo 1 — Costruzione dell'indice (k-tuple lookup)

Si sceglie una lunghezza di word $k$:
- $k = 2$ per sequenze proteiche
- $k = 6$ per sequenze nucleotidiche

Si estraggono tutte le k-tuple dalla sequenza di query con una **finestra scorrevole con overlap** di 1 posizione. Per una query di lunghezza $L$, si ottengono $L - k + 1$ parole.

Per ogni k-tuple, si registra la sua **posizione** nella query. Si costruisce quindi un dizionario:

$$\text{word} \to [\text{posizione}_1, \text{posizione}_2, \ldots]$$

Questo indice viene poi usato per cercare match identici nel database.

> **Esempio** (k=2, proteica): la query `ACDEF` genera le k-tuple `AC`, `CD`, `DE`, `EF`. Se nel database compare `AC` alla posizione 37, si registra un hit query[0] ↔ db[37].

---

### Passo 2 — Identificazione degli hot-spot (diagonali)

Per ogni k-tuple trovata identicamente nella query e in una sequenza del database, si calcola la **diagonale** su cui cade il match nella matrice di allineamento:

$$\text{diagonale} = \text{pos\_query} - \text{pos\_database}$$

Match sulla stessa diagonale indicano un possibile allineamento senza gap. FASTA accumula hit sulle diagonali e identifica quelle con il **maggior numero di match** (o lo score più alto se si usano matrici di sostituzione per pesare i match).

Le diagonali con molti hit vengono chiamate **hot-spot** o **initial regions (init1)**.

---

### Passo 3 — Estensione e unione dei frammenti (initn)

I frammenti contigui sulla stessa diagonale vengono estesi. Poi si tenta di **unire frammenti vicini** su diagonali adiacenti, introducendo una piccola penalità per i gap necessari a passare da una diagonale all'altra.

Il risultato è uno score **initn** — lo score del miglior insieme di frammenti concatenati per quella sequenza del database. Questo serve come filtro rapido: solo le sequenze con initn sopra una certa soglia vengono passate al passo successivo.

---

### Passo 4 — Allineamento locale ottimale (opt)

Per le sequenze candidate sopra la soglia di initn, FASTA applica **Smith-Waterman** ma solo su una **banda ristretta attorno alla migliore diagonale**, non sull'intera matrice. Questo riduce drasticamente il tempo di calcolo pur mantenendo un allineamento di alta qualità.

Lo score finale di questo allineamento locale è chiamato **opt score**.

---

### Passo 5 — Valutazione statistica

Come in BLAST, FASTA calcola la significatività degli score tramite la distribuzione **extreme-value (Gumbel)**. Gli score vengono normalizzati tenendo conto della lunghezza delle sequenze e della composizione aminoacidica, producendo un **E-value** confrontabile tra ricerche diverse.

---

### Schema riassuntivo del flusso FASTA

```
Query
  │
  ▼
[1] Indicizzazione k-tuple della query
  │
  ▼
[2] Ricerca k-tuple identiche nel DB → hit su diagonali
  │
  ▼
[3] Accumulo hit per diagonale → hot-spot (init1)
  │
  ▼
[4] Unione frammenti adiacenti → initn (filtro soglia)
  │
  ├─── sotto soglia → scartato
  │
  ▼
[5] Smith-Waterman su banda ristretta → opt score
  │
  ▼
[6] Calcolo E-value (distribuzione extreme-value)
  │
  ▼
Output: allineamenti ordinati per E-value
```

---

### FASTA vs BLAST — differenze chiave

| Aspetto | FASTA | BLAST |
|---|---|---|
| Indicizzazione | Query (con overlap) | Query (con overlap) + neighbourhood |
| Tipo di word | Identità esatta | Identità + sostituti sopra soglia T |
| Estensione | Unione di diagonali → SW su banda | Estensione bidirezionale con dropoff |
| Allineamento finale | SW su banda ristretta (opt) | HSP con gapped extension |
| Sensitività | Leggermente superiore per sequenze distanti | Leggermente inferiore, ma più veloce |
| Velocità | Più lento di BLAST | Più veloce in pratica |
| Statistica | Extreme-value (Gumbel) | Altschul statistics (stessa base) |

> **FASTA è generalmente considerato più sensibile di BLAST per sequenze molto divergenti**, perché considera le diagonali globalmente prima di estendere, mentre BLAST parte da singoli seed. Tuttavia BLAST è più rapido grazie al neighbourhood delle word e al Two-Hit Method, ed è diventato lo standard de facto.

---

## Note sull'ottimalità e le euristiche

È importante ricordare la gerarchia di garanzie:

| Algoritmo | Garantisce l'ottimo? |
|---|---|
| Needleman-Wunsch | ✅ Sì (globale) |
| Smith-Waterman | ✅ Sì (locale) |
| FASTA | ❌ No (euristico) |
| BLAST | ❌ No (euristico) |

FASTA e BLAST possono **non trovare** l'allineamento ottimale, specialmente per sequenze molto divergenti o con molti gap. Il guadagno in velocità (ordini di grandezza) rende però questo compromesso accettabile per la ricerca su database. Quando la certezza dell'ottimo è indispensabile (es. confronto tra due singole sequenze di interesse), si preferisce sempre Smith-Waterman o Needleman-Wunsch.
