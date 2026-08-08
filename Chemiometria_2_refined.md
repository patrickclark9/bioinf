# Analisi Multivariata: PCA

## Introduzione

La **PCA** (Principal Component Analysis) è una tecnica di analisi multivariata: si costruiscono le **componenti principali**, ovvero combinazioni lineari delle variabili iniziali, estratte secondo il principio della massima varianza e dell'ortogonalità.

Formalmente, la PCA è definita come una trasformazione ortogonale su uno spazio prodotto interno reale, che trasforma i dati in un nuovo sistema di coordinate tale per cui la massima varianza (misurata tramite proiezione scalare dei dati) si trova sulla prima coordinata (la **prima componente principale**), la seconda massima varianza sulla seconda coordinata, e così via.

### Ortogonalità

- Le componenti sono tra loro **ortogonali** (indipendenti) — perpendicolari, formano un angolo di 90°.
- Geometricamente: muoversi lungo un asse non altera la posizione del punto sugli altri assi (es. muoversi sull'asse X non altera la posizione sull'asse Y — i due assi sono indipendenti).
- Statisticamente: la covarianza tra due componenti è esattamente 0.
- In PCA: **PC1** cattura la massima varianza possibile nel dataset; **PC2** è ortogonale a PC1, quindi cattura nuova varianza senza duplicare l'informazione già catturata da PC1. Al crescere del numero di componenti, ciascuna è ortogonale a tutte le precedenti (es. PC3 è ortogonale sia a PC1 sia a PC2).
- Graficamente, con X = PC2 e Y = PC1, i due assi sono forzatamente ortogonali.

---

## Matrice dei Dati

Si parte dalla matrice $X$ dei dati, di dimensione $n \times p$, con $n$ = numero di molecole e $p$ = numero di descrittori.

Le relazioni tra i descrittori vengono quantificate calcolando la **matrice di covarianza S** e la **matrice di correlazione C**, prima ancora di estrarre le componenti principali.

- Le componenti principali sono nuove variabili, costituite da combinazioni lineari di quelle originali (i descrittori molecolari).
- Intercettano la direzione di massima varianza in uno spazio multivariato.
- Ogni combinazione lineare spiega parte della varianza totale.
- Sono ortogonali: l'informazione contenuta in ciascuna componente è unica.

### Varianza

Misura la dispersione di una singola variabile rispetto alla propria media — misura della variabilità dei valori assunti dalla variabile stessa.

$$\sigma^2_{jj} = \frac{\sum_{i=1}^n (x_{ij} - \overline{x}_j)^2}{n-1} \qquad 0 \le \sigma^2 < +\infty$$


### Covarianza

Misura la dispersione congiunta di due variabili rispetto alle rispettive medie. Indica se i valori variano nella stessa direzione (positivo) o in direzioni opposte (negativo).

$$\sigma_{jk} = \frac{\sum_{i=1}^n (x_{ij} - \overline{x}_j)(x_{ik} - \overline{x}_k)}{n-1} \qquad -\infty < \sigma_{jk} < +\infty$$

> _Nota: la covarianza si indica con $\sigma_{jk}$ (non $\sigma^2_{jk}$) — non è una varianza al quadrato, ma una misura di co-dispersione tra due variabili distinte; il quadrato è proprio solo del caso j = k (cioè la varianza)._

### Correlazione di Pearson

Indice che esprime un'eventuale relazione lineare tra due variabili.

$$-1 \le \rho \le 1$$

- $\rho = +1$ → correlazione lineare positiva perfetta
- $\rho = 0$ → assenza di correlazione lineare
- $\rho = -1$ → correlazione lineare negativa perfetta

$$\rho_{XY} = \frac{\sigma_{XY}}{\sigma_X \sigma_Y}$$

dove $\sigma_{XY}$ è la covarianza tra le variabili X e Y, mentre $\sigma_X$ e $\sigma_Y$ sono le rispettive deviazioni standard.

> _Nota: anche qui il numeratore è la covarianza $\sigma_{XY}$, non $\sigma^2_{XY}$._

---

## Costruzione delle Componenti Principali

Si calcolano $S$ (matrice di covarianza) e $C$ (matrice di correlazione).

![[Pasted image 20260808165025.png | 300]]![[Pasted image 20260808165037.png | 300]]

La trasformazione è definita da un insieme di dimensione $l$, dove $l < p$ (numero di descrittori), allo scopo di ridurre la dimensionalità.

### Diagonalizzazione della matrice di correlazione

La PCA diagonalizza la matrice di correlazione $C$. Dalla matrice iniziale $X$ si calcola $C$, la cui diagonalizzazione produce due matrici:

- $\Lambda$ — matrice degli **autovalori**
- $L$ — matrice dei **loadings** (autovettori)

![[Pasted image 20260808165543.png]]

#### Matrice Λ (autovalori)

- Ogni autovalore rappresenta l'esatta frazione di varianza catturata dalla corrispondente componente principale.
- Sono ordinati diagonalmente per frazione di varianza spiegata: $\lambda_1 \ge \lambda_2 \ge \lambda_3 \ge ... \ge \lambda_k \ge 0$.
- La somma degli autovalori è pari alla traccia della matrice $C$:

$$\sum_i \lambda_i = trace(C)$$

- Per decidere il numero di componenti principali da mantenere, si utilizzano lo **Scree-Plot** o il **criterio di Kaiser-Guttman**, che suggerisce di mantenere solo le componenti con $\lambda > 1$.

#### Matrice L (loadings / autovettori)

- Ogni riga rappresenta un descrittore originale; ogni colonna rappresenta una nuova componente principale.
- Ogni valore $l_{j,m}$ indica il peso (l'importanza) della variabile originale $j$ nella nuova componente principale $m$.
- I valori sono standardizzati, con $-1 \le l_{j,m} \le 1$, e la loro somma quadratica per ciascuna componente è pari a 1:

$$\sum_j l^2_{j,m} = 1$$

### Matrice degli Score

Lo step finale è il calcolo della **matrice degli score T**, ottenuta moltiplicando la matrice dei dati originali autoscalati $X$ per la matrice dei loading $L$:

$$T = XL$$

- La matrice dei loading agisce come matrice di rotazione, proiettando i dati originali in un nuovo spazio ortogonale.
- Gli score ($t_{i,m}$) sono le nuove coordinate cartesiane delle molecole all'interno dello spazio delle componenti principali.