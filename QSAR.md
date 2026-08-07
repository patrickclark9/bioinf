# QSAR

La QSAR è un approccio che tenta di formulare la relazione tra una struttura molecolare e la sua attività biologica, sotto forma di un modello matematico.
La QSPR invece è una estensione della QSAR che correla la struttura molecolare con ogni altra proprietà molecolare, come solubilità, stabilità metabolica etc...

Per la costruzione di un modello, è impossibile connettere tutte le proprietà alla struttura simultaneamente, motivo per cui ogni singola proprietà va considerata una per volta.

La QSAR ci permette di:
- Rivelare informazioni riguardo il sito di legame di un recettore.
- Il modello può essere utilizzato per predire l'attività biologica di analoghi che non sono stati sintetizzati.
- In chimica combinatoriale, la QSAR riduce grosse librerie virtuali in dimensioni pratiche per sintesi e screening

La QSAR moderna si basa su 3 contributi:
## Equazione di Hammet

L'equazione di hammet correlate le proprietà elettriche degli acidi e basi organiche con le costanti di equilibrio.
Le costanti di dissociazione degli acidi aromatici sono influenzate dalle proprietà elettroniche dei sostituenti sull'anello fenile.
Poichè le costandi di dissociazione sono associate con l'energia libera, questa è anche nota come **relazione lineare dell'energia libera**
$$\log\frac{K}{K_0} = \rho\sigma$$
dove
- $\rho$ -> Mette in relazione uno scaffold/equilibrio con un acido benzoico di riferimento
- $\sigma$ -> Un descrittore di un sostituenti che descrive la sua influenza sulla dissociazione. È positivo per gruppi accettori di elettroni e negativo per gruppi donatori di elettroni

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