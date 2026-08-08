# Analisi

## PCA
La PCA è una tecnica di analisi multivariata -> Si costruiscono le componenti principali, ovvero combinazioni lineari delle variabili iniziali estratte secondo il principio della massima varianza e della ortogonalità.
Le componenti sono tra loro ortogonali (indipendenti).
Ortogonalità -> Perpendicolarità (formano un angolo di 90 gradi). Geometricamente implica che formando un angolo retto tra assi, muoversi su uno degli assi non altera la posizione del punto sugli altri assi (muoversi su asse X non altera la posizione sull'asse Y, i due assi sono indipedenti). Statisticamente, la covarianza tra le due è esattamente 0. In PCA, PC1 cattura la massima possibile varianza nel dataset, PC2 è ortogonale a PC1, di conseguenza cattura nuova varianza senza informazione duplicata già catturata da PC1. Al crescere del numero di componenti, ogni componente è ortogonale alle altre (PC3 è ortogonale a PC1 e PC2). Graficamente, X = PC2 - Y= PC1, entrambe sono forzatamente ortogonali.

Si parte dalla matrice $X$ dei dati, di dimensione $n\times p$, con $n = \text{molecole}$ e $p = \text{descrittori}$.
Le relazioni tra i descrittori vengono quantificate calcolando la matrice di covarianza $S$ e la matrice di correlazione $C$.

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

Dalla matrice X iniziale ci si calcola $C$ la matrice di correlazione, la cui diagonalizzazione produce due matrici: $\Lambda$ la matrice degli autovalori, $L$ la matrice dei loadings.
![[Pasted image 20260808165543.png]]