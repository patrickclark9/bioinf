
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
- Si massimizza il training se