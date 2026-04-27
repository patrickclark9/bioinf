# Alignment

Allineare le sequenze è importante per ottenere una comparazione diretta, oltre ad essere prerequisito per analisi più complesse contro database, per la costruzione di alberi filogenetici o identificazione di motivi funzionali.

**Omologia** → Due entità condividono la stessa origine filogenetica, da cui si sono evolute differenziandosi dalle altre → _Qualitativa_

**Similarità** → Il termine similarità ha un significato generale, utilizzato a prescindere dalla motivazione. La similarità biologica può essere dovuta ad omologia ma anche dovuta al caso, o da fenomeni di convergenza adattiva → _Quantitativa_

- **Ortologhi** → Speciazione
- **Parologhi** → Duplicazione
- **Xenologhi** → Trasferimento orizzontale

> **BioMart** → Raccoglimento di ortologhi e parologhi di un gene

**Gap Opening** → Si apre un gap assegnando uno score negativo, la cui estensione comporta ulteriore penalità.

![[Screenshot from 2026-04-14 17-11-14.png]]

---

## Matrici

1. Identità
2. Genetic-Code
3. Matrice delle proprietà chimiche
4. Matrici Empiriche
    - PAM
    - BLOSUM
    - Gonnet

PAM e BLOSUM si basano sulle frequenze osservate di specifiche sostituzioni amminoacidiche. La similarità tra due amminoacidi è proporzionale alla loro frequenza di sostituzione osservata.

Queste matrici si basano su evidenze biologiche: le differenze osservate tra sequenze omologhe negli allineamenti sono dovute solo a eventi di mutazione. Alcune di queste mutazioni hanno effetti minimi o assenti nella struttura/funzione delle proteine.

La scelta di una delle matrici è cruciale per ottenere buoni risultati:

|Divergenza|Matrici consigliate|
|---|---|
|Sequenze poco divergenti|BLOSUM80 e PAM1|
|Mediamente divergenti|BLOSUM62 e PAM120|
|Molto divergenti|BLOSUM45 e PAM250|

---

### PAM

L'idea base delle matrici PAM nasce da studi di filogenetica molecolare su 71 famiglie di proteine con un minimo di 85% di similarità. L'assunzione di partenza è che analizzando sequenze filogeneticamente associate è possibile calcolare la percentuale di mutazioni accettate.

> **1 unità PAM** = 1% di cambiamento di posizione di un aminoacido = una sostituzione ogni 100 aminoacidi.

Si è partiti ricostruendo la sequenza ancestrale partendo da allineamento multiplo tra proteine con similarità elevata >85%.

Le sostituzioni "accettate" sono riportate su una matrice da cui è possibile ottenere la **mutabilità relativa** ($m_i$) del residuo $i$. Una volta definita la mutabilità, la domanda da porsi è qual è la probabilità che sia cambiato in $j$.

$$M_{ij} = m_i \cdot \frac{f_{ij}}{f_i} = \frac{f_{ij}}{f_i} \cdot \frac{f_i}{100 \cdot fp_i} = \frac{f_{ij}}{100 \cdot fp_i}$$

La probabilità che il residuo $i$ non cambi è $1 - M_{ij}$.

La probabilità di una mutazione dipende dal tempo trascorso dalla divergenza delle sequenze. I valori sono normalizzati per il tempo necessario ad introdurre 1 mutazione ogni 100 residui (distanza = 1 PAM).

Matrici PAM con indice maggiore di 1 si ottengono moltiplicando la matrice PAM per se stessa $k$ volte: $\text{PAM2} = \text{PAM1} \times \text{PAM1}$.

Le Matrici PAM si dividono in:

- **Scoring**
- **Substitution**

Le matrici di scoring utilizzate dai programmi di allineamento sono calcolate dalle matrici di sostituzione come:

$$s(a,b) = \text{int}\left(10 \cdot \log\frac{M(a,b)}{C(a,b)}\right)$$

Dove:

- $s(a,b)$ → score per una coppia di aminoacidi
- $M(a,b)$ → probabilità di sostituzione di un aminoacido
- $C(a,b)$ → probabilità di una sostituzione casuale di un aminoacido

Il rapporto $\frac{M(a,b)}{C(a,b)}$ indica quante volte la probabilità di omologia è maggiore della probabilità casuale.

---

### BLOSUM

Le matrici BLOSUM si basano sul **BLOCKS database**, il quale mantiene blocchi di sequenze relazionate tra loro con un definito valore di identità aminoacidica, generalmente tra il 30% ed il 95%. A partire da ogni blocco è possibile calcolare la frequenza di sostituzione osservata e la probabilità di accoppiamento casuale.

$$s(a,b) = \text{int}\left(10 \cdot \log\frac{M(a,b)}{C(a,b)}\right)$$

In questo caso $M(a,b)$ si riferisce alla probabilità di sostituzione osservata per ogni blocco.

- Per ogni allineamento nel database BLOCKS le sequenze sono raggruppate in cluster con almeno il 50% (per BLOSUM50, oppure 80% per BLOSUM80, ecc.) di residui identici.
- Tutte le coppie di sequenze sono comparate, e la frequenza delle coppie osservata viene annotata.
- La frequenza attesa delle singole coppie viene computata dalle singole frequenze aminoacidiche: $f_{A,C} = f_A \cdot f_C$
- Per ogni coppia di aminoacidi lo score di sostituzione viene computato con $s(a,b)$.

---

## DotPlot

Il dotplot aiuta a ispezionare la relazione tra due sequenze e ad identificare potenzialmente regioni conservate. Si interpreta come segue:

- **Diagonalmente attraverso i dot** → Match
- **Diagonalmente attraverso celle vuote** → Mismatch
- **Orizzontalmente** → Gap
- **Verticalmente** → Gap

L'allineamento viene effettuato muovendosi lungo la matrice in maniera tale da utilizzare le diagonali con i punti più grandi, massimizzando il numero di match.

Il metodo DotPlot si utilizza sia su sequenze nucleotidiche sia su sequenze proteiche. Poiché all'aumentare della lunghezza della sequenza aumentano anche i match spuri e quindi il rumore di fondo, i parametri di **window size** e **stringency** aiutano a visualizzare meglio.

![[Screenshot from 2026-04-15 16-21-31.png]]

---

## Tipologie di Allineamento

- **Globale** → Tiene conto della similarità tra sequenze per l'intera lunghezza (Query Coverage 100% sempre)
- **Locale** → Tiene conto della similarità tra sequenze soltanto per specifiche regioni simili tra parti della sequenza in analisi (cambia il Query Coverage)

> Lo score di allineamento più elevato non significa necessariamente che sia biologicamente significativo rispetto ad un altro allineamento con score inferiore.

Il tipo di allineamento (globale o locale) dipende strettamente dal caso in studio. Considerando che il numero di allineamenti cresce al crescere della lunghezza delle sequenze, tecniche come il **dynamic programming** vengono utilizzate per esplorare le possibili soluzioni in un tempo ragionevole.

L'algoritmo globale **Needleman-Wunsch** e quello locale **Smith-Waterman** utilizzano questa tecnica.

---

### Needleman-Wunsch

L'algoritmo di Needleman-Wunsch può essere riassunto in 3 step principali:

1. Riempimento della matrice
2. Calcolo dello score
3. Allineamento

Le sequenze compongono la matrice principale e le regole di composizione sono uguali a quelle del DotPlot. Ogni punto della matrice può essere raggiunto da 3 possibili posizioni; si sceglie quello con lo score più elevato tra le 3 possibilità per ottenere il best alignment score per uno specifico punto.

---

### Smith-Waterman

La Smith-Waterman si ottiene modificando la formula introducendo lo 0, così da non avere score negativi. L'allineamento si ricostruisce dal valore più elevato e termina allo 0.

Lo score è pari al massimo tra:

- $\text{score}(x, y-1) - \text{gap\_penalty}$
- $\text{score}(x-1, y-1) + \text{substitution\_score}(x,y)$
- $\text{score}(x-1, y) - \text{gap\_penalty}$

In principio l'allineamento locale è utile per cercare similarità in un database. Smith-Waterman è però troppo lento per identificare regioni simili ad una query in database molto grandi. Genera allineamenti ottimali ed esaustivi unicamente.

Per la ricerca su database si utilizzano algoritmi più complessi quali **FASTA** e **BLAST**.

![[Screenshot from 2026-04-15 17-10-18.png]]

---

## FASTA

L'algoritmo FASTA viene sviluppato nel 1985 basandosi sull'**indicizzazione delle parole** di una data lunghezza (**k-tuple**) (2 per a.a. e 6 per acidi nucleici). L'indicizzazione consiste nel creare una lista di tutte le posizioni in cui ogni possibile word $w$ appare all'interno della sequenza. Nel caso delle proteine, per $k=2$ avremo $20 \cdot N$ parole diverse (dove $N$ è la lunghezza delle k-tuple).

Il primo step è creare un indice di word della sequenza di query. Ogni parola verrà poi utilizzata per la ricerca all'interno del database. Nello specifico:

1. Si trovano parole contigue sulla stessa diagonale
2. Si calcolano gli score con le matrici di sostituzione
3. Si uniscono i frammenti che possono essere uniti con una threshold $T$ di accettabilità
4. Si applica Smith-Waterman su una porzione solamente (i frammenti riuniti) per ottenere l'allineamento migliore

---

## BLAST

**BLAST** (Basic Local Alignment Search Tool) — Parametri principali: W, T, S, X.

|Parametro|Descrizione|
|---|---|
|**W** (Wordsize)|↑ W → meno word generate → algoritmo più rapido, ma sensitività ↓|
|**T** (Threshold)|↓ T → più W-mers inclusi → tempo ↑, sensitività ↑|
|**S** (Score)|↓ S → HSP più lunghi|
|**X** (Dropoff)|↑ X → più regioni attorno agli HSP esplorate → tempo ↑. Controlla quanto lo score può scendere prima di arrestare l'allineamento|

Funzionamento basilare del BLAST:

1. Si crea un indice di tutte le $w$ della sequenza di query (con overlap)
    - Si ottengono tutte le $w$ dalla sequenza di query
    - Si crea una lista di tutte le word con match al di sopra della threshold $T$ (es. se la $w$ è GSW → GTW, GNW, GAW, ATW, GTF sono alcune delle possibili word; in base alla sostituzione si calcola lo score e se siamo sopra $T$, la word viene aggiunta alla lista)
2. Ogni parola della lista viene ricercata all'interno del database per trovare i match
3. Si estende la sequenza in entrambe le direzioni
4. Ci si ferma quando lo score diminuisce, o la sequenza termina (full-match)

Una delle estensioni recenti è il **Two-Hit Method**: l'estensione di un HSP viene attivata solo se due hit indipendenti si allineano per un certo numero di residui $A$ senza alcun gap tra loro.

### Altschul Statistics

Per verificare che un allineamento sia statisticamente significativo (e non dovuto al caso), sono state sviluppate le **Altschul statistics**.

Per due sequenze $m$ ed $n$, la funzione cumulativa di distribuzione degli score $S$ è:

$$P(S < x) = \exp\left(-e^{-\lambda(x-u)}\right)$$

Per allineamenti senza gap, il parametro $u$ dipende dalla lunghezza delle sequenze comparate:

$$u = \frac{\ln Kmn}{\lambda}$$

dove $m$ ed $n$ sono le lunghezze delle sequenze e $K$ è una costante.

La probabilità di osservare uno score uguale o superiore a $x$ per caso è:

$$P(S \ge x) = 1 - \exp\left(-Kmn \cdot e^{-\lambda x}\right)$$

Il parametro $Kmn \cdot e^{-\lambda x}$ è il numero di allineamenti senza gap con uno score di almeno $x$. Il prodotto $m \cdot n$ rappresenta sostanzialmente lo spazio di ricerca.

L'**E-value** (numero atteso di HSP con score $\ge S$ per caso) è:

$$E = Kmn \cdot e^{-\lambda x}$$

Per $E \to 0$, la probabilità che un allineamento sia avvenuto per caso tende a 0. Un alto score corrisponde ad un **E-value basso**.

$$P = 1 - e^{-E}$$

P-value ed E-value sono modi differenti di rappresentare la significatività di un allineamento.

### Bit-Score

Il **bit-score** $S'$ è uno score normalizzato con le variabili statistiche che definiscono un dato sistema di scoring. Permette di comparare allineamenti differenti, anche se utilizzano matrici di scoring differenti in ricerche diverse tramite BLAST.

$$S' = \frac{\lambda S - \ln K}{\ln 2}$$

L'E-value corrispondente sarà:

$$E = mn \cdot 2^{-S'}$$

---

## BLAT

Il **BLAST Like Alignment Tool (BLAT)** eredita le caratteristiche del BLAST, ma al posto di indicizzare la query, **indicizza il database** in k-mer senza overlap, contro cui viene linearmente comparata la sequenza di query.

- Si formano k-mer senza overlap nelle sequenze del database → si forma l'indice. Il processo è molto memory-hungry, ma riduce notevolmente il tempo di esecuzione.
- Il database è tipicamente molto grande, quindi salvare tutti i k-mer in un indice senza overlap diventa dispendioso.
- La query viene indicizzata in k-mer **con overlap**. Ogni k-mer della query viene comparato con il database.

---

## CLUSTALW

È un algoritmo di **allineamento multiplo**. Date 4 sequenze, si allineano S1 con S2 e S3 con S4. Dopodiché, i risultati degli allineamenti (S1, S2) ed (S3, S4) vengono a loro volta allineati, al fine di creare tutti i pairwise alignments. L'allineamento dei risultati di allineamento delle coppie aiuta a ridurre il numero di allineamenti da effettuare.