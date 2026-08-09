
# Validation of QSAR


## Test set

- Partizionamento del dato in test-training
- I composti devono presentare una rappresentatività uniforme
- Il test set non deve essere nè troppo simile (superstima) al training set nè troppo dissimile (predizione dfficile)
- Aiuta a identificare overfitting -> Miglioramenti nel training set non si traducono in una migliore predizione -> Si è adattato troppo bene ai dati di training, ma in predizione il modello non presenta buoni risultati

Nel test set:
- I metodi sperimentali per la determinazione della risposta in training e test devono essere simili
- I valori delle risposti devono estendersi in ordini di grandezza, ma non eccedere troppo quelli del training set
- Il rapporto tra molecole attive/inatt