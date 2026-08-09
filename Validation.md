
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