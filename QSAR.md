# QSAR

La QSAR è un approccio che tenta di formulare la relazione tra una struttura molecolare e la sua attività biologica, sotto forma di un modello matematico.
La QSPR invece è una estensione della QSAR che correla la struttura molecolare con ogni altra proprietà molecolare, come solubilità, stabilità metabolica etc...

Per la costruzione di un modello, è impossibile connettere tutte le proprietà alla struttura simultaneamente, motivo per cui ogni singola proprietà va considerata una per volta.

La QSAR tenta di stabilire una relazione matematica tra una struttura molecolare e proprietà chimica/biologica.
Dati k composti, i descrittori descrivono la struttura chimica, mentre l'attività è la quantità che bisogna valutare/predire.

Ponendo la risposta biologica sperimentale come l'attività
$$Activity = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \beta_3X_3$$
con 
- $X_1, X_2, X_3,...$ descrittori molecolari
- $\beta_1,\beta_2. \beta_3$ coefficienti stimati da dati sperimentali
- $\beta_0$ intercetta
È un esempio di modello QSAR semplice.


La QSAR ci permette di:
- Rivelare informazioni riguardo il sito di legame di un recettore.
- Il modello può essere utilizzato per predire l'attività biologica di analoghi che non sono stati sintetizzati. Una volta definito il modello, che riproduce correttamente dati noti,  questo può essere usato per predire l'attività biologica di analoghi non ancora sintetizzati
- In chimica combinatoriale, la QSAR riduce grosse librerie virtuali in dimensioni pratiche per sintesi e screening

È importante distinguere la struttura molecolare dai descrittori:
- La struttura molecolare è l'effettiva struttura rappresentata in 2D, come SMILES, o grafico molecolare
	- Benzene -> benzene sostituito -> fenolo sostituito
- Un descrittore molecolare è una rappresentazione numerica di una proprietà della struttura
	- molecular weight
	- logP
	- polar surface area
	- number of H-bond donors
	- number of H-bond acceptors
	- molecular volume
	- polarizability
	- topological indices
	- electronic parameters
Quindi **Struttura -> Descrittore**
L'attività invece è una quantità sperimentale da predire/spiegare:
- IC50
- EC50
- Affinità di binding
- Percentuale di inibizione
- Tossicità
- Attività enzimatica
- Rate di reazione

Spesso trasformiamo l'attività in scala logaritmica per produrre una scala meglio rappresentabile.
La QSAR è diventa quantitativa perchè si tenta di trasformare la semplice SAR:
> Aggiunta di un gruppo idrofobico aumenta l'attività

In una relazione quantitativa:

> $\text{Activity} = 2.3+1.4(\text{lipofilicità}) -0.8(\text{parametro sterico})$

I coefficienti ci danno direzione e contributo approssimativo del descrittore

Ad esempio $$\text{Activity} = 2 +1.5\log P$$
Significa che all'interno di questa serie chimica e dominio, incrementare logP è associato con incremento nell'attività predetta.

Questo non significa automaticamente che incrementare logP causa l'incremento di attività

La QSAR moderna si basa su 3 contributi: Equazione di Hammet, contributo di Hansch e Analisi di Free-Wilson.
## Equazione di Hammet

L'equazione di hammet correlate le proprietà elettriche degli acidi e basi organiche con le costanti di equilibrio.
Le costanti di dissociazione degli acidi aromatici sono influenzate dalle proprietà elettroniche dei sostituenti sull'anello fenile.
Poichè le costandi di dissociazione sono associate con l'energia libera, questa è anche nota come **relazione lineare dell'energia libera**
$$\log\frac{K}{K_0} = \rho\sigma$$
dove
- $k$ -> Costante di reazione per il composto sostituito
- $k_0$ -> Costante di reazione per il composto di riferimento
- $\rho$ -> Mette in relazione uno scaffold/equilibrio con un acido benzoico di riferimento
- $\sigma$ -> Un descrittore di un sostituente che descrive la sua influenza sulla dissociazione. È positivo per gruppi accettori di elettroni e negativo per gruppi donatori di elettroni

## Contributo di Hansch
Hansch riconobbe l'importanza dello lipofilicità per l'attività biologica, in quanto i farmaci devono essere in grado di attraversare il bilayer di membrana per raggiungere i target.
Introduce il $\log P$ (coefficiente di partizione tra 1-octanolo e fase acquosa) come misura della lipofilicità.
Venne introdotto poi un termine parabolico per il $\log P$ per tenere conto di molecole che rimangono intrappolate nella membrana e che non possono raggiungere il sito di azione.
$$\log \frac{1}{C} = a(\log P)^2 + b \log P + c\sigma + dE_s + e$$

## Analisi di Free-Wilson
Questo modello matematico  invece si basa sull'ipotesi che l'attività biologica è la somma di tutti i contributi elementari dei sostituenti.
Utilizza variabili indicatore ($x_i$ con valori di 1 o 0) per descrivere la presenza o l'assenza di un sostituente in  una specifica posizione di scaffold.

$$\log \frac{1}{C} = \sum{a_ix_i+\mu}$$
Dove $a_i$ è il peso del sostituente e $\mu$ e l'attività media.

## Descrittori Molecolari
I descrittori molecolari sono numeri che catturno la struttura e le proprietà fisico-chimiche della molecola. Per essere utili, i descrittori devono essere biologicamente rilevanti, cioè devono essere in grado di differenziare le molecole attive da quelle inattive.