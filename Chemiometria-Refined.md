# Chemiometria

La **chemiometria** è una branca della chimica che si occupa di relazionare le misure effettuate su un sistema o su un processo chimico allo stato del sistema, attraverso metodi matematici o statistici.

## QSAR come applicazione della chemiometria

La QSAR è un'applicazione della chemiometria.

![[Pasted image 20260808092802.png]]

Centrale alla QSAR non è solo il fitting del modello: è fondamentale **validare matematicamente** il modello (test-set, cross-validation, Y-scrambling) per valutarne le effettive prestazioni.

---

# Data Curation per QSAR

Essenziale prima di effettuare qualsiasi analisi QSAR è la **curatela del dataset** con cui verranno effettuate le analisi.

> Curare il dataset di partenza è fondamentale: un insieme iniziale di dati di bassa qualità produrrà, come risultato, un modello di bassa qualità.

## Cosa deve essere scelto

**Qualitativamente:**

- **Dati appropriati** — le misurazioni devono corrispondere alla domanda biologica/chimica da affrontare.
- **Riduzione della variabilità sperimentale**.
- **Copertura del dominio chimico** da parte dei dati sperimentali.

**Quantitativamente:**

- Numero di molecole il più alto possibile, particolarmente per casi complessi.
- Senza che queste molecole aggiungano complessità non necessaria al modello.

---

## Criteri Base per la Data Curation

### 1. Esperimenti in condizioni simili

Valori di attività fortemente differenti per uno stesso composto possono essere interpretati come rumore, o — peggio — il modello può individuare una relazione scorretta dovuta alla variabilità sperimentale.

### 2. Gestione dei duplicati e degli errori

È vitale identificare se la stessa molecola è presente più volte nel dataset, specialmente se etichettata con valori di attività differenti (es. una marcata come attiva, l'altra come inattiva). Questo rappresenta un problema, soprattutto in presenza di informazione contraddittoria.

### 3. Standardizzazione strutturale

- La rappresentazione strutturale deve essere **consistente**.
- Definire l'aromaticità, ad esempio, è una delle sfide principali, dato che esistono più possibilità di rappresentazione; la maggior parte dei software riconosce solo lo stile di rappresentazione "basic".
- È importante sceglierne una in modo coerente, perché il calcolo del descrittore **dipende dalla rappresentazione**.
- Lo stesso composto chimico può presentare rappresentazioni diverse: protonazione, aromaticità, tautomeri, stereochimica, sali, acidi carbossilici, gruppi nitro.
- Alcune proprietà non sono invarianti (es. lo stato di ionizzazione in funzione del pH).
- Due rappresentazioni molecolari diverse possono produrre valori differenti per lo stesso descrittore molecolare, specialmente per approcci basati su fingerprint o su frammenti.
- **Standardizzare prima del calcolo dei descrittori molecolari è essenziale.**![[Pasted image 20260808100537.png | 350]]![[Pasted image 20260808100526.png|350]]
### 4. Rimozione di miscele e composti inorganici

- I composti inorganici vengono spesso rimossi dal dataset.
- Per le miscele, la pratica standard è mantenere solo il frammento o la molecola con il **peso molecolare maggiore**.
- La QSAR richiede un'entità chimica ben definita, associata a una misurazione: la rimozione delle miscele è quindi fondamentale, perché il descrittore deve essere calcolato per una sola specie chimica — una miscela ne contiene più di una.

![[Pasted image 20260808095357.png]]