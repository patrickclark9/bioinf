# Chemiometria
La chemiometria è una branca della chimica che si occupa di relazionare le misure effettuate su un sistema o su un processo chimico allo stato del sistema attraverso metodi matematici o statistici.

## QSAR
La QSAR è una applicazione della chemiometria:
![[Pasted image 20260808092802.png]]

Centrale alla QSAR non è solo fittare il modello, è importante validare matematicamente (test-set, CrossValidation, Y-scrambling) per valutare l'effettive prestazioni del modello.
## Data Curation for QSAR

Essenziale prima di effettuare una qualsiasi analisi QSAR è quella di curare il dataset con cui verranno effettuate le analisi.
In principio, curare il dataset di partenza è fondamentale perchè un set iniziale di dati di bassa qualità avrà come risultato un modello di bassa qualità.
È importante che vengano scelti:
- Dati appropriati -> Le misurazioni devono corrispondere alla domanda biologica/chimica da effettuare
- Ridurre la variabilità sperimentale
- Dominio chimico deve essere coperto dai dati sperimentali
E quantitativamente:
- Numero di molecole più alto possibile, particolarmente per casi complessi
- Senza che queste molecole aggiungano complessità non necessaria al modello

I criteri basi per la data curation sono:
- Effettuare esperimenti in condizioni simili -> Valori di attività fortemente differenti per uno stesso composto possono essere interpretati come rumore, o peggio il modello può trovare una relazione incorretta dovuta alla variabilità sperimentale
- Gestione dei duplicati e degli errori -> È vitale identificare se la stessa molecola è presente più volte, specialmente se etichettata con valori di attività differenti (e.g. una marcata attiva, l'altra disattiva). Questo rappresenta un problema, soprattutto se presente informazione contraddittoria.
- Standardizzazione strutturale -> La rappresentazione strutturale deve essere consistente. Definire l'aromatizzazione ad esempio è una delle sfide principali, dato che esistono più possibilità di rappresentazione. La maggior parte dei software riconosce solo il basic style di appresentazione. È importante sceglierne uno perchè il calcolo del descrittore dipende dalla rappresentazione. La rappresentazione deve essere standardizzata. Lo stesso composto chimico può presentare differenti rappresentazioni (protonazione, aromaticità, tautomeri, stereochimica, sali, acidi carbossilici, gruppi nitro). Alcune proprietà non sono invarianti (stato di ionizzazione in funzione del pH). Due rappresentazioni molecolari possono produrre differenti valori per un descrittore molecolare, specialmente per approcci basati su fingerprint o su frammenti. Standardizzare prima del calcolo dei descrittori molecolari è essenziale
- Rimozione delle miscele e composti inorganici -> I composti inorganici vengono rimossi spesso. Per miscele, la pratica standard è mantenere solo il frammento o la molecola con il peso molecolare maggiore. La QSAR richiede un'entità chimica ben definita, associata con una misurazione. La rimozione delle miscele è quindi fondamentale, perchè il descrittore deve essere calcolato per una sola specie chimica, una miscela ne contiene più di una

![[Pasted image 20260808095357.png]]