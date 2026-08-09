
# Validation of QSAR


## Test set

- Partizionamento del dato in test-training
- I composti devono presentare una rappresentatività uniforme
- Il test set non deve essere nè troppo simile (superstima) al training set nè troppo dissimile (predizione dfficile)
- Aiuta a identificare overfitting -> Miglioramenti nel training set non si traducono in una migliore predizione -> Si è adattato troppo bene ai dati di training, ma in predizione il modello non presenta buoni risultati
L'overfitting diventa problematico spesso anche quando il modello è troppo complesso.
In alcuni casi però la presenza di termini di interazioni è necessario per descrivere un fenome complesso, come nella equazione generale della solvatazione di Abraham, il cui termine $$\sum \substack{\alpha2H} \sum\substack{\beta2H}$$
rappresenta il prodotto della hydrogen bond acidity and basicity di soluti in soluzione

Nel test set:
- I metodi sperimentali per la determinazione della risposta in training e test devono essere simili
- I valori delle risposti devono estendersi in ordini di grandezza, ma non eccedere troppo quelli del training set
- Il rapporto tra molecole attive/inattive tra trainin e test deve essere simile

## Cross Validazione
La cross Validazione è un metodo di validazione INTERNO, effettuato esclusivamente sul training set.  Misura la stabilità e la robustezza del modello matematico. Serve un Test set per validare il resto.
Ogni modello deve essere validato con dati nuovi e indipendenti per evitare il problema della correlazione fortuita.
### Leave One Out
- Si partiziona il dataset in $k$ partizioni dove $k=N$ il numero di campioni
- Si massimizza il training set, in quanto il modello viene addestrano su $N-1$ campioni
- Si lascia un campione per la validazione
- A rotazione, ogni data-point verrà usato per la validazione

Vantaggi:
- Basso bias -> L'utilizzo di tutto il dataset per il training previene underfitting
- Deterministico -> Gli split sono fissati a priori
Svantaggi
- Altissimo costo computazionale -> dipende da $N$. Per $N >> 500$ significa addestrare un numero enorme di modelli
- Alta varianza -> La predizione può fluttuare dipendentemente dal rumore del campione

### K-Fold
- Identico alla Leave-One-Out, ma invece di partizionare il dataset $k=N$, si definisce un valore per $k$ a priori, tipicamente non molto grande, ma dipende dalle dimensioni del campione (e.g. $k=5, k=10$)
- Il dataset viene partizionato in $k$ parti uguali, dove $k-1$ fold vengono utilizzati per l'addestramento, ed 1 fold viene utilizzato per la validazione
- L'addestramento-validazione avviene $k$ volte, quindi ogni partizione verrà usata per la validazione
- Il risultato medio dei $k$ modelli creati è una metrica delle prestazioni del modello
- Di strategie di K-Fold ne esistono tante, tra cui la stratificata, dove ogni partizione contiene più o meno lo stesso rapporto di classi. In regressione significa che il valore di risposta medio è più o meno lo stesso tra tutte le partizioni
- Nella repeated cross-validation, il partizionamento avviene più volte, e le prestazioni del modello possono essere catturate da più run
La Leave-One-Out è un caso particolare di K-Fold, dove $k = N$.

## $Q^2$
Il $Q^2$ è una metrica statistica utilizzata per valutare il potere predittivo e la generalizzabilità di un modello.
La $\text{PRESS}$ o Predictive Error Sum of Squares $$\text{PRESS} = \sum_{i=1} ^N(y_i - \hat y_{i/i})^2$$
È uguale alla RSS, ma calcolato sul valore di $y$ predetto definito come $\hat y$ per l'i-esimo campione da un modello in cui il campione non è stato utilizzato in training. Viene calcolato ovviamente mediante LeaveOneOut.

Utilizzando la PRESS al posto di RSS possiamo ottenere la percentuale di varianza spiegata dal modello in predizione: 
$$Q^2 = R^2_{CV}=1- \frac{\text{PRESS}}{\text{TSS}}$$
Diversamente da $R^2$ ma similmente allo stesso aggiustato, $Q^2$ presenta un massimo per la complessità ottimale del modello, e ridiscende ogni volta che aggiungiamo al modello variabili non predittive.
$Q^2$ viene esplicitamente valutato per esprimere una misura predittiva e non descrittiva (fitting) del modello
![[Pasted image 20260809170446.png]]
Non esiste correlazione tra $Q^2$ e la predizione del test set $R^2_{pred}$, ovvero non vie è relazione tra predizione interna ed esterna.
Spesso ad una maggiore predizione interna corrisponde una più bassa predizione esterna.


## Y-Scrambling

- Consiste nell'andare a valudare le prestazioni preditivve del modello andando a shufflare la variabile target $Y$ e lasciando immutate le $X$.
- Le etichette-valori di $Y$ vengono riorganizzate o permutate
- Il modello viene riaddestrato sui dati "scrambled" utilizzando le stesse feature di input
- Vengono raccolte metriche di prestazioni
- Si ripete lo scrambling e l'addestramento molte volte per costruire una distribuzione di score casuali
- Il modello originale viene comparato contro la distribuzione di score casuali.
	- Se lo score originale è più alto il modello ha potere predittivo effettivo

Aiuta nel visualizzare eventuale overfitting
Espone correlazioni dovute al caso
Vastamente utilizzato in modelli QSAR per validare modelli relazionali struttura-attività

## Classificazione

- Prestazioni tipicamente valutati mediante matrici di confusione
- Accuratezza, Precisione e Richiamo
![[Pasted image 20260809174014.png]]

## Modelli di Classficazione
- Alberi
- SVM
- KNN