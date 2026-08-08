# Analisi

## PCA
La PCA è una tecnica di analisi multivariata -> Si costruiscono le componenti principali, ovvero combinazioni lineari delle variabili iniziali estratte secondo il principio della massima varianza e della ortogonalità.
Le componenti sono tra loro ortogonali (indipendenti).
Ortogonalità -> Perpendicolarità (formano un angolo di 90 gradi). Geometricamente implica che formando un angolo retto tra assi, muoversi su uno degli assi non altera la posizione del punto sugli altri assi (muoversi su asse X non altera la posizione sull'asse Y, i due assi sono indipedenti). Statisticamente, la covarianza tra le due è esattamente 0. In PCA, PC1 cattura la massima possibile varianza nel dataset, PC2 è ortogonale a PC1, di conseguenza cattura nuova varianza senza informazione duplicata già catturata da PC1. Al crescere del numero di componenti, ogni componente è ortogonale alle altre (PC3 è ortogonale a PC1 e PC2). Graficamente, X = PC2 - Y= PC1, entrambe sono forzatamente ortogonali.

Si parte dalla matrice $X$ dei dati, di dimensione $n\times p$, con $n = \text{molecole}$ e $p = \text{descrittori}$.
Le relazioni tra i descrittori vengono quantificate calcolando la matrice di covarianza $S$ e la matrice di correlazione $C$.

Prima di estrarre le componenti, le relazioni tra le variabili iniziali vanno quantificate con queste due matrici

Le componenti principali sono nuove variabili costituite dalla combinazione lineare di quelle originali (i descrittori molecolari)
Le componenti principali sono nuove variabili che intercettano la direzione di massima varianza in uno spazio multivariato
Ogni combinazione lineare spiega parte della varianza totale
Sono ortogonali, ovvero l'informazione contenuta in ognuna di esse è unica
### Varianza 
Misura la dispersione di una singola variabile rispetto alla sua media. Misura della variabilità dei valori assunti dalla variabile stessa

$$\sigma^2_{jj} = \frac{\sum_{i=1} ^n (x_{ij} - \overline x_j)}{n-1} $$
$$ 0 <\sigma^2 < +\infty$$
### Covarianza
Misura la dispersione di una singola variabile rispetto alla sua media e rispetto ai valori di un'altra variabile. Indica se i valori variano nella stessa direzione (positivo) o in direzioni opposte (negativo)

$$\sigma^2_{jk} = \frac{\sum_{i=1} ^n (x_{ij} - \overline x_j) (x_{ik} - \overline x_k)}{n-1} $$
$$ -\infty <\sigma^2 < +\infty$$

### Correlazione di Pearson
Indice che esprime una eventuale relazione lineare tra loro.
Ha valori $$-1 \le \rho \le 1$$
Dove +1 rappresenta ad una perfetta correlazione lineare positiva, 0 ad una assenza di correlazione, -1 ad una correlazione lineare negativa. Espressa come
$$\rho_{XY} = \frac{\sigma^2_{XY}}{\sigma_X \sigma_Y}$$
dove $\sigma^2 _{XY}$ è la covarianza tra le due variabili X e Y, mentre $\sigma_X$ e $\sigma_Y$ sono le deviazioni standard.


## Costruzione delle componenti principali
PCA is defined as an orthogonal  on a real inner product space that transforms the data to a new coordinate system such that the greatest variance by some scalar projection of the data comes to lie on the first coordinate (called the first principal component), the second greatest variance on the second coordinate, and so on.
Ci si calcola $S$ e $C$.
![[Pasted image 20260808165025.png | 300]]![[Pasted image 20260808165037.png | 300]]

La trasformazione è definita da un insieme di dimensione $l$, dove $l < \text{features}$ per ridurre la dimensionalità.
La PCA diagonalizza la matrice di correlazione $C$:
Dalla matrice X iniziale ci si calcola $C$ la matrice di correlazione, la cui diagonalizzazione produce due matrici: $\Lambda$ la matrice degli autovalori, $L$ la matrice dei loadings (autovettori).
![[Pasted image 20260808165543.png]]

- $\Lambda$ -> Ogni autovalore rappresenta l'esatta frazione di varianza catturata dalla corrispondente componente principale
	- Sono ordinati diagonalmente per frazione di varianza spiegata: $\lambda_1 \ge \lambda_2 \ge \lambda_3 \ge ... \ge \lambda_k \ge 0$
	- La somma degli autovalori è pari alla traccia della matrice $C$ -> $$\sum_{i} \lambda_i = trace(C)$$
	- Per decidere il numero di componenti principali da calcolare, si utilizzano gli Scree-Plot o il criterio Kaiser-Guttman, che suggerisce di mantenere solo le componenti con $\lambda > 1$
- $L$ -> La matrice degli autovettori o loading
	- Ogni riga rappresenta il descrittore originale, mentre la colonna rappresenta la nuova componente principale
	- Ogni valore $l_{j,m}$ mostra il peso o l'importanza della variabile $j$ originale nella nuiova componente principale $m$
	- I valori sono standardizzati cosicchè $-1 \le l_{j,m} \le 1$, e la loro somma quadratica è pari a 1 $$\sum_j l^2_{j,m} = 1$$

Lo step finale è calcolare la matrice degli Score $T$, fatto moltiplicando il valore originale della matrice dei dati autoscalati per la matrice dei loading $L$ $$T = XL$$
- La matrice dei loading agisce come matrice di rotazione, proiettando i dati originali in un nuovo spazio ortogonale
- Gli score ($t_{i,m}$) sono nuove coordinate cartesiane di molecole all'interno dello spazio delle componenti principali


# Similarità Molecolare
- Le molecole sono rappresentate in notazione lineare compatta, come la notazione SMILES, che rappresenta le molecole in funzione dei modelli di valenza


---

## Spazio Chimico

![[Pasted image 20260808104158.png]]

Ogni molecola è un punto in un gigantesco spazio multidimensionale, dove ogni asse rappresenta una proprietà molecolare. Ogni composto è quindi un **punto nello spazio chimico**.

- Lo spazio chimico è uno spazio astratto multidimensionale in cui i composti sono rappresentati come punti
- I descrittoi molecolari definiscono la posizione dei composti nello spazio
- La similarità/dissimilarità quantifica le distanze tra i composti nello spazio chimico

## Dissimilarità\Similarità

- Si va a quantificare il grado di similarità tra coppie di molecole attraverso opportuni coefficienti di similarità
	- Proprietà chimico-fisiche e indici topologici (MW, lipofilia, ecc) -> riducibili mediante PCA
	- Fingerprint 2D per chiavi strutturali
	- Punti di farmacoforo
- La diversità molecolare esprime una misura numerica di distanza molecolare tra due oggetti caratterizzzati da un set di attributi comuni

Alcuni indici di misurazione sono:
- Hamming
- Euclidea
- Soergel
- Tanimoto
- Dice 
- Cosine

Questi sono principalmente indici che valutano la distanza, trasformabili in indici di similarità poichè basta invertire il coefficiente -> la similarità è data dalla distanza tra due oggetti. La distanza è data dalla similarità di due oggetti
$$s_{A,B} = \frac{1}{1+d_{A,B}}$$
$$d_{A,B} = \frac{1-s_{A,B}}{s_{A,B}}$$
![[Pasted image 20260808173806.png]]

# Clustering
Il clustering è una operazione di raggruppamento di un insieme di oggetti in cluster, tale che gli oggetti in un cluster sono per una qualche ragione più simili tra loro rispetto agli oggetti in cluster differenti

- Gli algoritmi di clustering sono algoritmi non supervisionati in quanto determinano i gruppi di similarità all'interno di un dataset di oggetti non etichettati -> Non c'è "addestramento" del modello con dati pre-etichettati e guidati con l'output corretto
- Il risultato dipende da come viene calcolata la similarità -> algoritmi differenti possono avere output differenti e non ci sono a priori motivi per preferire uno rispetto all'altro

Gli algoritmi possono essere:
- Parametrici -> Sfruttano conoscenza a priori sul dataset per fissare il numero di classi -> diventa un problema di ottimizzazione con una funzione obiettivo da minimizzare
- Non Parametrici -> In assenza di conoscenza a priori, l'algoritmo determina una gerarchia di classi in funzione di una scala di osservazione, producendo dendogrammi

## K-Means
- Si sceglie K il numero di cluster
- Si computano i K centroidi iniziali casualmente all'interno dello spazio
- Ogni punto (dato) viene assegnato al centroide più vicino sulla base di una data misura della distanza
- Si ricalcola la posizione dei centroidi sulla base dei cluster generati
- Si itera finchè non viene minimizzata una funzione obiettivo, spesso la distorsione $$D = \sum^N_{i=1} ||x_i - c(x_i)||^2$$
	- Dove $c(x_i)$ è il centroide associato al punto $x_i$ 
- Il numero di cluster vieno fissato arbitrariamente, spesso plottando valori di K contro il TSS (total sum of within cluster square distances)  e prendendo il "gomito" della curva![[Pasted image 20260808181955.png]]

## Algoritmi Gerarchici di Linkage
- Si inizia considerando ogni oggetto come un cluster e si calcola la matrice delle distanze
- I due oggetti più vicini vengono raggruppati in un cluster e considerati come un unico oggetto
- Si ricalcolano le distanze e si uniscono gli oggetti più vicini
	- La distanza tra cluster può essere considerata come
		- Single Linkage $d(A,B) =  \min{d(a,b)}$
		- Complete Linkage $d(A,B) = \max{d(a,b)}$![[Pasted image 20260808182511.png]]
		- Average Linkage -> Distanza tra cluster è la media delle distanze tra tutti i punti dei due cluster
		- Centroid Linkage -> La distanza fra cluster è la distanza fra i centroidi dei cluster
	- Si prosegue finchè tutti gli oggetti non vengono raggruppati in un unico cluster e si ottiene il dendogramma![[Pasted image 20260808182638.png|400]]![[Pasted image 20260808182651.png]]
 Questo produce una gerarchia di cluster, senza partizioni fisse,(Unlike algorithms such as K-means that force data into a strict, pre-defined number of boxes (fixed partitions), hierarchical clustering builds a continuous tree-like structure known as a **dendrogram** (shown on the right side of the slide). This diagram maps out the relationships and distances between all data points (labeled 1 through 5) at various levels of similarity.) agglomerativi o divisivi (- **Agglomerative (Bottom-Up / _agglomerativi_):** Indicated by the upward-pointing arrow. This is the most common approach. It starts by treating every single data point (1, 3, 2, 4, 5) as its own isolated cluster. It then finds the two most similar points (e.g., 1 and 3) and merges them into a new cluster. It repeats this process, joining clusters together step-by-step as you move up the y-axis, until everything is merged into one massive, all-encompassing cluster at the top.
**Divisive (Top-Down / _divisivi_):** Indicated by the downward-pointing arrow. This approach does the exact opposite. It starts with all data points lumped into one giant cluster at the top. It then progressively splits the cluster into smaller, increasingly distinct subsets as you move down, until every point stands alone.).To decide which points to merge (agglomerative) or split (divisive), the algorithm requires a mathematical rule to define how "alike" two objects are. This similarity index can be based on spatial **distance** (like Euclidean or Manhattan distance) or statistical **correlation** (like the Pearson coefficient). Il dendogramma viene tagliato dove è maggiore il lifetime del cluster Because the algorithm generates a continuous tree rather than a final set of groups, the researcher must decide how many clusters to ultimately use. This is done by drawing a horizontal "cut" across the dendrogram. The slide specifies that this cut should be made where the **lifetime** of the clusters is greatest. "Lifetime" refers to the vertical length of the branches (the vertical lines in the graph). A long vertical branch means that the cluster remains stable over a large range of distance/similarity before it is forced to merge with another group. Cutting through these long vertical lines ensures you are isolating highly distinct, stable clusters.