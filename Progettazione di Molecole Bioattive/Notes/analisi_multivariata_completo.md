# Analisi Multivariata: PCA, Similarità Molecolare, Clustering, Algoritmi Genetici

## Tecniche di Selezione delle Variabili
- PCA
- Clustering
- Strategie Forward-selection / Backward-selection
- Algoritmi Genetici

---

# PCA (Principal Component Analysis)

## Introduzione

La **PCA** è una tecnica di analisi multivariata: si costruiscono le **componenti principali**, ovvero combinazioni lineari delle variabili iniziali, estratte secondo il principio della massima varianza e dell'ortogonalità.

Formalmente, la PCA è definita come una trasformazione ortogonale su uno spazio prodotto interno reale, che trasforma i dati in un nuovo sistema di coordinate tale per cui la massima varianza (misurata tramite proiezione scalare dei dati) si trova sulla prima coordinata (la **prima componente principale**), la seconda massima varianza sulla seconda coordinata, e così via.

### Ortogonalità
- Le componenti sono tra loro **ortogonali** (indipendenti) — perpendicolari, formano un angolo di 90°.
- Geometricamente: muoversi lungo un asse non altera la posizione del punto sugli altri assi.
- Statisticamente: la covarianza tra due componenti è esattamente 0.
- **PC1** cattura la massima varianza possibile nel dataset; **PC2** è ortogonale a PC1, quindi cattura nuova varianza senza duplicare l'informazione già catturata da PC1. Ogni componente successiva è ortogonale a tutte le precedenti.

## Matrice dei Dati

Si parte dalla matrice $X$ dei dati, di dimensione $n \times p$, con $n$ = numero di molecole e $p$ = numero di descrittori.

Le relazioni tra i descrittori vengono quantificate calcolando la **matrice di covarianza S** e la **matrice di correlazione C**, prima ancora di estrarre le componenti principali.

### Varianza
$$\sigma^2_{jj} = \frac{\sum_{i=1}^n (x_{ij} - \overline{x}_j)^2}{n-1} \qquad 0 \le \sigma^2 < +\infty$$

### Covarianza
$$\sigma_{jk} = \frac{\sum_{i=1}^n (x_{ij} - \overline{x}_j)(x_{ik} - \overline{x}_k)}{n-1} \qquad -\infty < \sigma_{jk} < +\infty$$

### Correlazione di Pearson
$$-1 \le \rho \le 1 \qquad \rho_{XY} = \frac{\sigma_{XY}}{\sigma_X \sigma_Y}$$

- $\rho = +1$ → correlazione lineare positiva perfetta
- $\rho = 0$ → assenza di correlazione lineare
- $\rho = -1$ → correlazione lineare negativa perfetta

## Costruzione delle Componenti Principali

Si calcolano $S$ e $C$.

![[Pasted image 20260808165025.png | 300]]![[Pasted image 20260808165037.png | 300]]

La trasformazione è definita da un insieme di dimensione $l$, dove $l < p$, allo scopo di ridurre la dimensionalità.

### Diagonalizzazione della matrice di correlazione

La PCA diagonalizza la matrice di correlazione $C$, la cui diagonalizzazione produce:
- $\Lambda$ → matrice degli **autovalori**
- $L$ → matrice dei **loadings** (autovettori)

![[Pasted image 20260808165543.png]]

#### Matrice Λ (autovalori)
- Ogni autovalore rappresenta l'esatta frazione di varianza catturata dalla corrispondente componente principale.
- Ordinati diagonalmente per varianza spiegata: $\lambda_1 \ge \lambda_2 \ge ... \ge \lambda_k \ge 0$.
- $\sum_i \lambda_i = trace(C)$

**Criteri per scegliere il numero di componenti:**
- **Scree-Plot** o **criterio di Kaiser-Guttman**: si mantengono solo le componenti con $\lambda > 1$.

  ![[Pasted image 20260808180950.png]]

- **Varianza cumulata**: si scelgono tante componenti quante bastano a raggiungere una soglia (es. 90% di varianza cumulata).

#### Matrice L (loadings / autovettori)
- Ogni riga rappresenta un descrittore originale; ogni colonna una nuova componente principale.
- $l_{j,m}$ indica il peso della variabile $j$ nella componente $m$.
- $-1 \le l_{j,m} \le 1$, con $\sum_j l^2_{j,m} = 1$.

### Matrice degli Score

$$T = XL$$

- La matrice dei loading agisce come matrice di rotazione, proiettando i dati originali in un nuovo spazio ortogonale.
- Gli score ($t_{i,m}$) sono le nuove coordinate cartesiane delle molecole nello spazio delle componenti principali.

---

# Similarità Molecolare

- Le molecole vengono rappresentate in notazione lineare compatta, come la notazione **SMILES**, che rappresenta le molecole in funzione dei modelli di valenza.

![[Pasted image 20260808174532.png]]

## Spazio Chimico

![[Pasted image 20260808104158.png]]

Ogni molecola è un punto in un gigantesco spazio multidimensionale, dove ogni asse rappresenta una proprietà molecolare. Ogni composto è quindi un **punto nello spazio chimico**.

- Lo spazio chimico è uno spazio astratto multidimensionale in cui i composti sono rappresentati come punti.
- I descrittori molecolari definiscono la posizione dei composti nello spazio.
- La similarità/dissimilarità quantifica le distanze tra i composti nello spazio chimico.

## Dissimilarità / Similarità

Si quantifica il grado di similarità tra coppie di molecole attraverso opportuni coefficienti di similarità, calcolati su:

- **Proprietà chimico-fisiche e indici topologici** (MW, lipofilia, ecc.) — riducibili mediante PCA:
  - I descrittori 1D sono spesso fortemente correlati tra loro, e fornire al modello tutti questi descrittori ridondanti può causare problemi (overfitting).
  - La PCA aiuta a risolvere questo problema comprimendo la descrizione dei dati ed eliminando il rumore di fondo.
  - Le componenti principali sono inoltre ortogonali, quindi l'informazione contenuta in ciascuna componente è unica.
  - Raggruppare le variabili insieme permette di individuare le proprietà che hanno effettivamente un impatto sull'attività biologica.
- **Fingerprint 2D** per chiavi strutturali.
- **Punti di farmacoforo**.

> La **diversità molecolare** esprime una misura numerica di distanza tra due oggetti caratterizzati da un set di attributi comuni.

I descrittori utilizzati per la similarità devono essere:
- Facili da calcolare su grossi database molecolari
- Rilevanti in termini di endpoint biologici
- Facili da interpretare

## Relazione tra Similarità e Distanza

$$s_{A,B} = \frac{1}{1+d_{A,B}} \qquad d_{A,B} = \frac{1-s_{A,B}}{s_{A,B}}$$

![[Pasted image 20260808173806.png]]

### Indici di Misurazione

| Indice | Formula (distanza, salvo indicazione) |
|---|---|
| **Hamming** | $d_{A,B} = \sum_{i=1}^{p} \lvert x_{Ai} - x_{Bi} \rvert$ — conta il numero di posizioni in cui i valori dei due vettori differiscono |
| **Euclidea** | $d_{A,B} = \sqrt{\sum_{i=1}^{p} (x_{Ai} - x_{Bi})^2}$ — distanza geometrica diretta nello spazio multidimensionale |
| **Soergel** | $d_{A,B} = \dfrac{\sum_i \lvert x_{Ai} - x_{Bi} \rvert}{\sum_i \max(x_{Ai}, x_{Bi})}$ — spesso usata come complemento della similarità di Tanimoto per dati continui |
| **Tanimoto** (similarità) | $s_{A,B} = \dfrac{c}{a+b-c}$ — il coefficiente più usato per fingerprint binarie |
| **Dice** (similarità) | $s_{A,B} = \dfrac{2c}{a+b}$ — simile a Tanimoto, ma pesa maggiormente le feature condivise |
| **Cosine** (similarità) | $s_{A,B} = \dfrac{\sum_i x_{Ai}\,x_{Bi}}{\sqrt{\sum_i x_{Ai}^2}\sqrt{\sum_i x_{Bi}^2}} = \dfrac{c}{\sqrt{ab}}$ — misura l'angolo tra i due vettori, indipendente dalla loro magnitudine |

> Per fingerprint binarie, $a$ e $b$ sono il numero di bit "attivi" (1) rispettivamente in A e in B, mentre $c$ è il numero di bit attivi in comune (intersezione).

---

# Clustering

## Introduzione

Il **clustering** è un'operazione di raggruppamento di un insieme di oggetti in cluster, tale che gli oggetti in uno stesso cluster siano più simili tra loro rispetto agli oggetti in cluster differenti.

- Algoritmi **non supervisionati**: determinano i gruppi di similarità in un dataset di oggetti non etichettati, senza addestramento su output noti a priori.
- Il risultato dipende da come viene calcolata la similarità: algoritmi differenti possono produrre output differenti, senza un motivo a priori per preferirne uno.

### Tipologie di algoritmi
- **Parametrici** — sfruttano conoscenza a priori per fissare il numero di classi; diventa un problema di ottimizzazione con funzione obiettivo da minimizzare.
- **Non parametrici** — in assenza di conoscenza a priori, determinano una gerarchia di classi in funzione di una scala di osservazione, producendo **dendrogrammi**.

## K-Means

1. Si sceglie **K**, il numero di cluster.
2. Si computano K centroidi iniziali, posizionati casualmente.
3. Ogni punto viene assegnato al centroide più vicino.
4. Si ricalcola la posizione dei centroidi.
5. Si itera finché non viene minimizzata la **distorsione**:

$$D = \sum_{i=1}^{N} \lVert x_i - c(x_i) \rVert^2$$

dove $c(x_i)$ è il centroide associato al punto $x_i$.

### Scelta di K
Si plottano i valori di K contro il **TSS** (total sum of within-cluster square distances), individuando il "gomito" della curva (*elbow method*).

![[Pasted image 20260808181955.png]]

## Algoritmi Gerarchici (Linkage)

1. Ogni oggetto è inizialmente un cluster a sé stante; si calcola la matrice delle distanze.
2. I due oggetti più vicini vengono raggruppati e considerati un unico oggetto.
3. Si ricalcolano le distanze e si uniscono gli oggetti più vicini, iterando fino a un unico cluster finale, ottenendo il **dendrogramma**.

### Misure di distanza tra cluster

| Tipo di linkage | Definizione |
|---|---|
| **Single Linkage** | $d(A,B) = \min\, d(a,b)$ |
| **Complete Linkage** | $d(A,B) = \max\, d(a,b)$ |
| **Average Linkage** | Media delle distanze tra tutti i punti dei due cluster |
| **Centroid Linkage** | Distanza tra i centroidi dei due cluster |

![[Pasted image 20260808182511.png]]

![[Pasted image 20260808182638.png|400]]![[Pasted image 20260808182651.png]]

### Agglomerativi vs Divisivi

Il clustering gerarchico produce una gerarchia di cluster, senza partizioni fisse — a differenza di K-means, che forza i dati in un numero prefissato di gruppi.

**Agglomerativo (bottom-up)** — il più comune:
- Ogni punto parte come cluster isolato.
- Si uniscono i due punti più simili in un nuovo cluster.
- Si prosegue salendo lungo l'asse y, finché tutto converge in un unico cluster finale.

**Divisivo (top-down)**:
- Si parte da un unico cluster contenente tutti i punti.
- Si suddivide progressivamente, scendendo lungo l'albero, fino a isolare ogni punto.

### Criterio di similarità
Basato su **distanza spaziale** (es. Euclidea, Manhattan) o **correlazione statistica** (es. Pearson).

### Taglio del dendrogramma
Il dendrogramma viene tagliato dove è maggiore il **lifetime** del cluster: la lunghezza verticale dei rami. Un ramo verticale lungo indica che il cluster resta stabile su un ampio intervallo di distanza/similarità prima di unirsi ad un altro gruppo — tagliare in corrispondenza di questi rami isola cluster distinti e stabili.

---

# Algoritmi Genetici

Gli algoritmi genetici sono algoritmi evoluzionistici che emulano i processi biologici di ricombinazione genetica, mutazione e selezione per generare possibili soluzioni.
Sono metodi di ottimizzazione stocastica, caratterizzati dalla capacità di esplorare diverse regioni dello spazio parametrico.

## Analogia Biologica

| Biologia | Equivalente GA |
|---|---|
| Individuo | Soluzione candidata |
| Gene | Variabile (descrittore) |
| Cromosoma | Sottoinsieme di descrittori |
| Popolazione | Insieme di modelli |
| Fitness | Qualità del modello |
| Selezione | Mantenimento dei modelli migliori |
| Mutazione | Cambiamento casuale |
| Crossover | Combinazione di modelli |

## Procedura

1. Una popolazione iniziale di N cromosomi viene generata casualmente. Ogni cromosoma è costruito attraverso una combinazione casuale dei geni.
2. Ogni cromosoma viene valutato in relazione alla risposta prodotta.
3. L'algoritmo prosegue finché:
   - Non viene trovata una soluzione accettabile
   - Non viene raggiunto un criterio di convergenza
   - Non vengono conclusi tutti i cicli di iterazione

   ![[Pasted image 20260809090601.png]]

4. **Crossing-over** — coppie di cromosomi vengono ricombinate per formare nuovi individui.
5. **Mutazione** — il contenuto genico del cromosoma viene alterato in maniera casuale.

I valori che ogni variabile può assumere vengono codificati attraverso un codice binario. La concatenazione di gruppi di bit costituisce un individuo. Ogni cromosoma è valutato sulla base della sua risposta rispetto a una funzione obiettivo da minimizzare.

### Applicazione alla QSAR

Nel caso della QSAR, un cromosoma può essere una stringa binaria che definisce una particolare combinazione di descrittori.

![[Pasted image 20260809085954.png]]

Per ciascun cromosoma generato viene determinata la risposta, ovvero il valore della funzione obiettivo. Una funzione tipica è $q^2$, ovvero la varianza spiegata dal modello in predizione rispetto a un dato endpoint.

### Evoluzione della popolazione

Durante la fase evolutiva, ciascun cromosoma della popolazione può casualmente subire una mutazione, oppure possono essere accoppiati cromosomi genitori presenti nella popolazione tramite lo scambio dell'informazione contenuta nei rispettivi geni. In ogni caso, viene calcolata la nuova risposta corrispondente.

- Se la risposta calcolata è migliore di quella corrispondente al cromosoma peggiore della popolazione esistente, il nuovo cromosoma entra a far parte della popolazione, nella posizione corretta in base alla qualità. Altrimenti viene scartato.
- La **probabilità di mutazione** deve essere piccola: evita di generare cromosomi troppo diversi casualmente da quelli che costituiscono la popolazione ottimale, il che allontanerebbe la ricerca dalla probabile regione ottima.
- La **probabilità di crossing-over** deve invece essere sufficientemente elevata da permettere alcune delle possibili ricombinazioni, mantenendo comunque porzioni consistenti del patrimonio genetico parentale.

### Selezione dei Cromosomi Parentali

La selezione dei cromosomi genitori per generare nuovi individui tramite crossing-over si ottiene con metodi stocastici:

- **Roulette-wheel** — la selezione dei cromosomi genitori avviene con una probabilità direttamente proporzionale alla qualità della risposta associata a un cromosoma.

  ![[Pasted image 20260809090417.png]]

## Genetic Programming

Il cromosoma è un **albero** di forma e lunghezza variabili, dove i nodi sono funzioni e le foglie sono variabili.

![[Pasted image 20260809090744.png]]

### Meccanismo

- Il **GP** (Genetic Programming) ricerca lo spazio delle **equazioni**, non solo delle variabili, sfruttando le rappresentazioni ad albero.
- Gli step sono simili a quelli degli algoritmi genetici classici, ma al posto di generare cromosomi sotto forma di stringa binaria di inclusione/esclusione, vengono generate **equazioni casuali**, e ad ogni step si memorizzano le equazioni con le prestazioni migliori.
- Le **mutazioni** avvengono rimpiazzando parte dell'albero con nuove equazioni, oppure aggiungendo o rimuovendo nodi.

### Vantaggi

- È in grado di modellare relazioni **non lineari**.
- Non è necessario predefinire la struttura dell'equazione.
- Risulta più **flessibile** rispetto ai modelli di regressione tradizionali.
