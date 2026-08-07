# [[QSAR]]

La [[QSAR]] è un approccio che tenta di formulare la relazione tra una struttura molecolare e la sua attività biologica, sotto forma di un modello matematico.
La QSPR invece è una estensione della [[QSAR]] che correla la struttura molecolare con ogni altra proprietà molecolare, come solubilità, stabilità metabolica etc...

Per la costruzione di un modello, è impossibile connettere tutte le proprietà alla struttura simultaneamente, motivo per cui ogni singola proprietà va considerata una per volta.

La [[QSAR]] tenta di stabilire una relazione matematica tra una struttura molecolare e proprietà chimica/biologica.
Dati k composti, i descrittori descrivono la struttura chimica, mentre l'attività è la quantità che bisogna valutare/predire.

Ponendo la risposta biologica sperimentale come l'attività
$$Activity = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \beta_3X_3$$
con 
- $X_1, X_2, X_3,...$ descrittori molecolari
- $\beta_1,\beta_2. \beta_3$ coefficienti stimati da dati sperimentali
- $\beta_0$ intercetta
È un esempio di modello [[QSAR]] semplice.


La [[QSAR]] ci permette di:
- Rivelare informazioni riguardo il sito di legame di un recettore.
- Il modello può essere utilizzato per predire l'attività biologica di analoghi che non sono stati sintetizzati. Una volta definito il modello, che riproduce correttamente dati noti,  questo può essere usato per predire l'attività biologica di analoghi non ancora sintetizzati
- In chimica combinatoriale, la [[QSAR]] riduce grosse librerie virtuali in dimensioni pratiche per sintesi e screening

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
La [[QSAR]] è diventa quantitativa perchè si tenta di trasformare la semplice SAR:
> Aggiunta di un gruppo idrofobico aumenta l'attività

In una relazione quantitativa:

> $\text{Activity} = 2.3+1.4(\text{lipofilicità}) -0.8(\text{parametro sterico})$

I coefficienti ci danno direzione e contributo approssimativo del descrittore

Ad esempio $$\text{Activity} = 2 +1.5\log P$$
Significa che all'interno di questa serie chimica e dominio, incrementare logP è associato con incremento nell'attività predetta.

Questo non significa automaticamente che incrementare logP causa l'incremento di attività

La [[QSAR]] moderna si basa su 3 contributi: Equazione di Hammet, contributo di Hansch e Analisi di Free-Wilson.
## Equazione di Hammet

L'equazione di Hammet correlate le proprietà elettriche degli acidi e basi organiche con le costanti di equilibrio.
La dissociazione consiste nella rimozione di un protone dal composto neutrale, lasciando un anione. La reazione viene misurata dalla costante di dissociazione $K$.
Le costanti di dissociazione degli acidi aromatici sono influenzate dalle proprietà elettroniche dei sostituenti sull'**anello fenile**.
Le costanti di dissociazione di acidi benzoici e fenilacetici sostiuiti indicano che gruppi electron-withdrawing incrementano la dissociazione, mentre gruppi electron-donating diminuiscono la dissociazione.
![[Pasted image 20260807095916.png]]
Poichè le costanti di dissociazione sono associate con l'energia libera $\Delta G = -RT\log K$, questa è anche nota come **relazione lineare dell'energia libera**
$$\log\frac{K}{K_0} = \rho\sigma$$
dove
- $K$ -> Costante di reazione per il composto sostituito
- $K_0$ -> Costante di reazione per il composto di riferimento
- $\rho$ -> Mette in relazione uno scaffold/equilibrio con un acido benzoico di riferimento. Descrive quanto forte è la risposta di una particolare reazione all'effetto di un sostituente elettronico
- $\sigma$ -> Un descrittore che quantifica l'effetto di un sostituente, descrivendo la sua influenza sulla dissociazione. È positivo per gruppi accettori di elettroni e negativo per gruppi donatori di elettroni. Descrive come un sostituente cambia il carattere eletronico di una molecola relativo all'idrogeno.
	- Effetto mesomerico -> Risonanza (overlap) dell'orbitale p, relazionata alla topologia della molecola e all'elettronegatività
![[Pasted image 20260807105613.png]]
L'equazione di Hammet è un esempio di QSPR.
Compara una proprietà molecolare, la costante di dissociazione, con un insieme di descrittori molecolari, $\rho$ e $\sigma$.
Il valore di $\sigma$ differisce se il sostituente è meta o para.
In chimica organica, ==**orto, meta e para** indicano le posizioni relative di due sostituenti su un anello benzenico==. La posizione **orto** (1,2) è vicina, **meta** (1,3) è separata da un carbonio e **para** (1,4) è opposta
## Contributo di Hansch
Hansch riconobbe l'importanza dello lipofilicità per l'attività biologica, in quanto i farmaci devono essere in grado di attraversare il bilayer di membrana per raggiungere i target. La lipofilicità è correlata alla presenza di gruppi idrofobici e all'assenza di gruppi polari e ionizzabili.
Introduce il $\log P$ (coefficiente di partizione tra fase lipidica (1-octanolo) e fase acquosa) come misura della lipofilicità.
Venne introdotto poi un termine parabolico per il $\log P$ per tenere conto di molecole che rimangono intrappolate nella membrana e che non possono raggiungere il sito di azione.
$$P = \frac{[farmaco]_{organico}}{[farmaco]_{acquoso}}$$
Dove per P>1 (logP>0) la molecola è lipofilica, P < 1 (logP<0) è idrofobica. 
$$\log \frac{1}{C} = a(\log P)^2 + b \log P + c\sigma + dE_s + e$$
Eventualmente l'equazione QSAR venne ampliata introducendo nuovi descrittori:
$\sigma$ -> Descrittore Elettronico
$Es$ -> Descrittore di Taft -> È la costante sterica, un valore sperimentale basato su costanti del rate di un dato modello di reazione. Misura l'effetto sterico esercitato da un sostituente sull'equilibrio. Più grosso il sostituente, più negativo sarà $Es$.
$$Es = \log K_x - \log K_H$$
![[Pasted image 20260807105255.png]]

$\pi$ -> Lipofilicità - > Il descrittore $\pi$ caratterizza la lipofilicità di un sostituente. Definito come la differenza tra logP del sostituito e del non sostituito. Sostituenti più idrofobici di H avranno $\pi$ positivo, mentre sarà negativo per sostituenti con $\pi$ meno idrofobici di H.
$$\pi = \log P - \log P_H$$
![[Pasted image 20260807104810.png]]
$MR$ -> Rifrazione molare -> La rifrazione molare è un descrittore che contiene informazioni sul volume di un composto corretto per l'indice di rifrazione (rapporto velocità della luce nel vuoto contro la velocità della luce in una sostanza di interesse) $$MR = \frac{(n^2-1)MW}{(n^2+1)d}$$
![[Pasted image 20260807105055.png]]
Con:
- $d$ -> densità
- n -> indice di rifrazione
- MW -> Peso molecolare

Il termine quadratico $(\log P)^2$ è particolarmente interessante perchè l'attività biologica non incrementa indefinitivamente con la lipofilicità, esistono punti di massimo globale/locale.
$$\text{Activity} = a\log P - b(\log P)^2$$
## Analisi di Free-Wilson
Questo modello matematico  invece si basa sull'ipotesi che l'attività biologica è la somma di tutti i contributi elementari dei sostituenti.
Utilizza variabili indicatore ($x_i$ con valori di 1 o 0) per descrivere la presenza o l'assenza di un sostituente in  una specifica posizione di scaffold.

$$\log \frac{1}{C} = \sum{a_ix_i+\mu}$$
Dove $a_i$ è il peso del sostituente e $\mu$ e l'attività media.

## Descrittori Molecolari
I descrittori molecolari sono numeri che catturno la struttura e le proprietà fisico-chimiche della molecola. Per essere utili, i descrittori devono essere biologicamente rilevanti, cioè devono essere in grado di differenziare le molecole attive da quelle inattive.