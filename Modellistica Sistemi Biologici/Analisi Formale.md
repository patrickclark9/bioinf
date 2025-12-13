**Analisi Formale**:
1. Viene assunto un meccanismo compatibile con l'equazione stechiometrica e dei valori iniziali delle costanti cinetiche
2. Vengono calcolate le osservabili e confrontate con i dati sperimentali
3. Vengono minimizzati gli scostamenti fra andamenti calcolati e sperimentali variando le costanti cinetiche (Passo di ottimizzazione)
4. Se le curve teoriche ben riproducono gli andamenti delle osservabili allora il meccanismo resta convalidato insieme ai valori delle costanti cinetiche

Una volta descritto un meccanismo compatibile cinetico con l'equazione stechiometrica, il secondo passo dell'analisi formale consiste nel tradurlo in un insieme di equazioni differenziali (ODE) da risolvere per ottenere l'andamento temporale delle concentrazioni in funzione del tempo.

Il sistema da risolvere avrà tante equazioni quante sono le specie chimiche coinvolte nel processo come descritto dal meccanismo proposto.
Per ogni specie chimica la derivata della concentrazione rispetto al tempo verrà eguagliata alla somma delle velocità di reazione degli stadi a cui tale specie prende parte, moltiplicati per il coefficiente stechiometrico con il segno appropriato (- reagente, + prodotto).

Se il sistema non è aperto, è possibile scrivere una o più equazioni di conservazione della massa. Il numero totale di equazioni di conservazione che possono essere scritto è uguale al numero di specie **atomiche** che compaiono nell'equazione.

Le equazioni di conservazione non sono altro che la forma macroscopica del principio di conservazione della massa per la reazione chimica stessa, quindi il numero di atomi che prende parte ad una reazione chimica deve restare costante prima e dopo la reazione, espresso in unità di volume del sistema chimico reagente.
$$2[I_2]_0 + [HI]_0 = 2[I_2] + [I] + [HI]$$
Da questa equazione di esempio si evince che il valore delle concentrazioni degli atomi di Iodio al tempo t=0 deve mantenersi costante durante tutto il processo. Infatti solo le grandezze sulla destra dipendono dal tempo.

Queste equazioni possono essere estratte dal sistema ODE. Derivando rispetto al tempo le equazioni di conservazione della massa si ottengono relazioni fra le derivate delle concentrazioni che devono essere soddisfatte dalle equazioni differenziali.
![[Screenshot 2025-08-17 at 16.41.57.png]]
(Derivata di una costante = 0, il resto è la derivata rispetto a t)

Le equazioni di conservazione possono anche essere usate per verificare l'esattezza del sistema ODE.

Per risolvere un sistema è possibile scegliere fra equazioni differenziali e di conservazione. Solitamente quelle di conservazione vengono usate per rimuovere variabile e ridurre il numero di equazioni del sistema ODE.

## Equazioni differenziali
Equazione che mette in relazione una funzione con le sue derivate.
- Ordinarie -> Derivate rispetto ad una variabile
	- Ordinaria di ordine N -> N è il massimo ordine della derivata 
- Derivate parziali -> Equazione in cui sono presenti derivate parziali

## Sistemi di Equazioni Differenziali
- Sistemi Ordinari ODE -> Formato solo da equazioni differenziali ordinari 
	- Se di ordine superiore al primo può sempre essere ricondotto ad un sistema del primo ordine
- Sistemi Parziali PDE -> Formato da equazioni differenziali parziali
### Sistemi Espliciti
![[Screenshot 2025-08-17 at 10.42.09.png]]
### Sistemi Autonomi
Viene detto **Autonomo*** se la variabile indipendente (t) non compare mai esplicitamente nelle equazioni $$\frac{dy}{dt} = y' = f(y)$$
Nei sistemi autonomi, la variabile indipendente è sempre eliminabile:
$$\begin{cases}
	\frac{dy_1}{t} = f_1(y_1,y_2)\\
	\frac{dy_2}{t} = f_2(y_1,y_2)
\end{cases} \rightarrow \frac{dy_1}{dy_2} = \frac{f_1(y_1)}{f_2(y_2)}$$
#### Spazio delle Fasi
Diagramma in cui su ogni asse viene riportata la concentrazione di una specie reagente. Un punto rappresenta uno stato del sistema.

## Soluzioni per un sistema ODE
Per risolvere analiticamente un sistema ODE, bisogna trovare n funzioni le cui derivate prime $y_i(t) (i = 1,2,3,...,n)$ calcolate rispetto a t soddisfino le equazioni del sistema.
Affinché le soluzioni $y_i(t)$ siano determinate univocamente sono necessarie ulteriori equazioni.
**Problema dei valori iniziali**: Le soluzioni assumono particolari valori al tempo t=0
**Problema dei valori di contorno**: Le soluzioni assumono particolari valori agli estremi dell'intervallo di definizione di t.