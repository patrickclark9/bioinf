![[Pasted image 20250816172107.png]]

La cinetica fenomenologica studia l'evoluzione temporale dei sistemi chimici reagenti al fine di determinare il meccanismo di reazione ed i valori delle costanti cinetica.

Differisce dalla **Dinamica chimica** che invece si occupa del cacolo delle costanti cinetiche per le reazioni elementari a partire da principi primi.
__________

**Sistema chimico reagente**: Regione dello spazio in cui hanno luogo le reazioni chimiche

***Classificazioni***:
- Scambi Energetici:
	- Aperto
	- Chiuso
	- Isolato
- Cambiamenti di Fase
	- Monofasico -> Una fase
	- Eterogeneo -> Più fasi

**Reazioni**:
- Principio di Conservazione della Massa: Massa dei reagenti = Massa dei prodotti $$\sum^{Prodotti}_i n_{P_i} \cdot PM_{P_i} - \sum^{Reagenti}_j n_{R_j} \cdot PM_{R_j} = 0$$

---

**Osservabili**: Le osservabili fenomelogiche sono grandezze fisiche misurabili legate alle quantità delle specie chimiche che prendono parte al processo.
Le osservabili sono fondamentali per lo studio *temporale* di un sistema chimico reagente.
Nei casi più semplici sono proporzionali alle quantità delle specie reagenti presenti nel sistema
Nei casi più complessi sono legate alle specie in maniera non lineare o a più specie contemporaneamente.
Solitamente si scelgono proprietà intensive del sistema come osservabili.

----

**Analisi cinetica fenomenologica**: Trovare un meccanismo di reazione compatibile con tutti i dati sperimentali raccolti.
Permette di scoprire gli stadi lenti di un processo ed eventuali intermedi di reazione. Permette di definire le migliori condizioni sperimentali affinchè un processo avvenga nella direzione desiderata.

-----
**Meccanismo di Reazione**: Lista di reazioni elementari che sommate portano all'equazione chimica del processo
**Reazione elementare**: Reazione senza intermedi di reazione del tipo $A\rightarrow B$

**Simboli**
- $A = B$ -> Reazione bilanciata
- $A \Rightarrow B$ -> Processo avviene da sinistra verso destra
- $A \rightarrow B$ -> Processo elementare da sinistra verso destra
- $A \leftrightarrows B$ -> Processo elementare e reversibile
- $A \leftrightharpoons B$ -> Processo all'equilibrio

---
**Intermedio di reazione**: Specie instabile che scompare in tempi lunghi, non è presente tra i prodotti se non in tracce. I suoi tempi di vita sono abbastanza lunghi da essere rilevati.
![[Screenshot 2025-08-16 at 17.46.21.png | 550]]

----

**Non è possibile dimostrare la fondatezza di un meccanismo cinetico, solo la sua falsità**.
Se viene dimostrato come falso, un meccanismo cinetico viene rifiutato. È valido solo se non viene dimostrata la sua inadeguatezza.

---
## Approcci di Analisi: Formale
![[Screenshot 2025-08-16 at 17.53.39.png]]
## Approcci di Analisi: Empirica

Si analizzano le osservabili sperimentali dipendenti dal tempo, e si ricavano:
- Equazione Cinetica
- I valori delle costanti cinetiche fenomenologiche

A partire da questi due valori ricavati si determina un meccanismo di reazione compatibile con l'equazione cinetica e l'equazione chimica.


---

## Velocità di Reazione

La velocità di reazione può essere formulata in due maniere: Estensivamente ed Intensivamente

**Formulazione Estensiva**: Numero di eventi reattivi per unità di tempo
**Formulazione Intensiva**: Numero di eventi reattivi per unità di tempo e unità di volume

Queste definizioni però sono poco pratiche,non permettono la semplice determinazione della velocità. 
La velocità di reazione deve essere legata alla velocità di variazione delle osservabili in gioco, ma indipendente dal loro andamento: crescita per i prodotti, diminuzione per i reagenti

**Definizioni alternative**:
- Variazione di concetrazioni: Espressa come variazione di concentrazioni, la velocità di reazione diventa una grandezza intensiva $r = -\frac{1}{a} \frac{d[A]}{dt} = -\frac{1}{b} \frac{d[B]}{dt} = +\frac{1}{b} \frac{d[B]}{dt} = ... = +\frac{1}{p} \frac{d[P]}{dt} = + \frac{1}{q} \frac{d[Q]}{dt}$
- Variazione del numero di moli: v può essere definita come la derivata rispetto al tempo del numero di moli di una data specie chimica diviso il rispettivo coefficiente stechiometrico, positivo (prodotti) o negativo (reagenti)  $v = \frac{d\xi}{dt} = -\frac{1}{a}\frac{dn_A}{dt} = -\frac{1}{b}\frac{dn_B}{dt} = ... = +\frac{1}{p}\frac{dn_P}{dt} = +\frac{1}{q}\frac{dn_Q}{dt}$

**Relazione fra v ed r**
$r = - \frac{1}{a}\frac{d[A]}{dt} = -\frac{1}{aV}\frac{dn_A}{dt} = \frac{v}{V}$
$r = \frac{v}{V}+\frac{[A]}{aV}\frac{dV}{dt}$
![[Screenshot 2025-08-16 at 18.35.26.png]]
**La catena di uguaglianze può non essere sempre verificata, va confermata sperimentalmente per stabilire se l'equazione è valide oppure no ed in quali intervalli di tempo**.

### Equazione di Arrhenius
$ln(K) = ln(A) - \frac{E_a}{RT}$
è la riformulazione dell'equazione di Arrhenius in forma logaritmica, con cui è possibile determinare il fattore pre-esponenziale A e l'energia di attivazione Ea, effettuando misure di k a valori diversi di temperatura e riportando in grafico contro l'inversa di T.
![[Screenshot 2025-08-16 at 18.46.13.png]]