
# PCA
La PCA è una tecnica di analisi multivariata -> Si costruiscono le componenti principali, ovvero combinazioni lineari delle variabili iniziali estratte secondo il principio della massima varianza e della ortogonalità.
Le componenti sono tra loro ortogonali (indipendenti).
Ortogonalità -> Perpendicolarità (formano un angolo di 90 gradi). Geometricamente implica che formando un angolo retto tra assi, muoversi su uno degli assi non altera la posizione del punto sugli altri assi (muoversi su asse X non altera la posizione sull'asse Y, i due assi sono indipedenti). Statisticamente, la covarianza tra le due è esattamente 0. In PCA, PC1 cattura la massima possibile varianza nel dataset, PC2 è ortogonale a PC1, di conseguenza cattura nuova varianza senza informazione duplicata già catturata da PC1. Al crescere del numero di componenti, ogni componente è ortogonale alle altre (PC3 è ortogonale a PC1 e PC2). Graficamente, X = PC2 - Y= PC1, entrambe sono forzatamente ortogonali.

Si parte dalla matrice $X$ dei dati, di dimensione $n\times p$, con $n = \text{molecole}$ e $p = \text{descrittori}$.
Le relazioni tra i descrittori vengono quantificate calcolando la matrice di covarianza $S$ e la matrice di correlazione $C$.

## Varianza 
Misura la distribuzione dei valori rispetto alla media

$$\sigma^2 = \sum_{i=1} ^n (x_{ij$$