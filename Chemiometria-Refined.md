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
- **Standardizzare prima del calcolo dei descrittori molecolari è essenziale.**![[Pasted image 20260808100537.png|250]]![[Pasted image 20260808100526.png|350]]
### 4. Rimozione di miscele e composti inorganici

- I composti inorganici vengono spesso rimossi dal dataset.
- Per le miscele, la pratica standard è mantenere solo il frammento o la molecola con il **peso molecolare maggiore o il numero maggiore di atomi**.
- La QSAR richiede un'entità chimica ben definita, associata a una misurazione: la rimozione delle miscele è quindi fondamentale, perché il descrittore deve essere calcolato per una sola specie chimica — una miscela ne contiene più di una.

![[Pasted image 20260808095357.png|350]]

## Descrizione molecolare
- Formula bruta -> Informazione composizionale, peso molecolare
- Struttura 2D -> Connessione tra atomi, tipi di legame, configurazione Z/E
- Struttura 3D -> Include coordinate spaziale $<x_i, y_i, z_i>$, descrive volume molecolare, superficie molecolare, momento dipolare, superficie polare
- Struttura 4D -> Informazione conformazionale, Distribuzione elettronica
- Ulteriori livelli in 4 dimensioni -> Proprietà di dinamica molecola in un sistema spazio-tempo, proprietà biologiche se valutate le interazioni con l'ambiente
Le dimensioni rappresentano non solo 4 coordinate, ma diversi livelli di informazione sul livello molecolare
![[Pasted image 20260808101345.png]]

## Fingerprint Molecolare
Le fingerprint molecolari sono sistemi sviluppati per la codifica e rappresentazione vettoriale delle feature molecolari.
Un esempio di fingerprint molecolari sono le fingerprint strutturali, in cui si va a rappresentare la presenza o assenza di una determinata feature strutturale (anello aromatico, gruppo ossidrilico, ammina, ammide ecc...) attraverso un vettore binario, in cui ogni posizione rappresenta la presenza/assenza di una data feature strutturale: $$<1,0,1,1,0,0>$$
Di fingerprint ne esistono molte tipologie differenti con significati diversi in grado di codificare differenti feature della molecola, a partire dalle substrutture fino a codificare la struttura tridimensionale molecolare.

Le fingerprint sono particolarmente utili per operazioni di:
- Clustering
- Similarity Searching
- Virtual Screening
- Machine Learning

Le fingerprint sono uno dei motivi per cui la standardizzazione è importante: Differenti rappresentazioni avranno diverse fingerprint.

## Descrittori 3D
I Descrittori tridimensionali dipendono dalle coordinate $<x,y,z>$ , di conseguenza se una molecola può assumere differenti conformazioni $C_1, C_2, C_3$, allora il descrittore calcolato sulle conformazioni sarà differente $D(C_1) \ne D(C_2)$ potenzilamente.
Il valore di un descrittore 3D cambia in funzione delle coordinate atomiche delle differenti conformazioni, introducendo un problema -> quale conformazione scegliere.
Questo problema diventa esponenzialmente più complesso per le proteine:
### Paradosso di Levinthal
Data una proteina di 100 amminoacidi, se ogni amminoacidi possiede anche solo 3 possibili conformazioni, allora il numero di possibili conformazioni totali sarebbe $$3^{100} \approx 10^{48}$$
Impossibile raggiungere la struttura nativa, richiederebbe troppo tempo anche esplorando miliardi di conformazioni al secondo.

I descrittori 3D quindi introducono un livello non banale di complessità conformazionale


## Descrittori Chirali
La stereochimica è un altro problema importante, dato che diversi enantiomeri, pur avendo stessa:
- Formula chimica
- Connettività
- Peso Molecolare
Presentano struttura 3-D differente, e quindi anche differente attività biologica, dato che il target è anch'esso tridimensionale e spesso chirale.

Nella sintesi molecolare, ogni centro chirale introduce una complessità importante:

$$2^{\text{centri chirali}}$$
È il numero di enantiomeri prodotti durante la sintesi. Con 4 centri chirali:
$$2^4 = 16 \space \text{enantiomeri diversi}$$
### Easson-Stedman
Il modello Easson-Stedman introduce il modello a 3 punti di interazioni:
- Il ligando chirale può interagire con il recettore chirale attraverso più punti di interazione $$A \rightleftarrows A'$$ $$B \rightleftarrows B'$$ $$C \rightleftarrows C'$$
- Di conseguenza solo uno stereoisomero può ottenere il corretto arrangiamento spaziale, mentre gli altri non possono simultaneamente soddisfare le stesse interazioni ![[Pasted image 20260808103826.png]]![[Pasted image 20260808103848.png]]For geometric isomerism:

/and\

are used.

For example:

Br/C=C/Br

and

Br/C=C\backslashBr

represent different geometric arrangements.

For tetrahedral stereochemistry, SMILES uses:

@

and: @@

## Feature Selection
Dato che il numero di descrittori utilizabili sono tantissimi, bisogna accuratamente selezionare e scegliere quali sono particolarmente importanti per il dato caso di studio
### Caso: Lipinski Rule of Five
The four criteria shown are:

MW>500 logP>5 HBD>5 HBA>10

These are commonly expressed as the Rule of Five because compounds violating more of these criteria tend to have poorer oral drug-like properties.

The important connection to QSAR is that:

simple molecular descriptors can provide useful biological/ADME information​

For example:

#### High MW

Can make diffusion more difficult.

#### High logP

Means high lipophilicity.

#### Many H-bond donors/acceptors

Means a molecule has many polar interaction sites.

Together these descriptors provide a rough indication of whether a molecule has favourable properties for oral absorption.

## Spazio Chimico 

![[Pasted image 20260808104158.png]]
Ogni molecola è un punto sul gigantesco spazio multidimensionale, dove ogni asse è una proprietà molecolare. Ogni composto è quindi un punto nello spazio chimico.

# Modellazione del dato
- Preprocessing
- Variable selection
- Model derivation
## Data pre-processing - Normalizzazione
- Autoscaling delle ascisse
- Trasformazione logaritimica delle Y

La normalizzazione è necessaria per evitare problemi di scala differente di valori per i singoli descrittori molecolari, ed evitare che determinate feature vengano interpretate come più importanti a livello biologico solo in funzione del numero più grande in termini assoluti.

### Autoscaling
Prima fase è la centratura:
Per un descrittore X: $$x'_i = x_i - \overline{x}$$con $$\overline x = \frac{1}{n}\sum_i x_i$$
Quindi dopo la centratura $$\text{mean} = 0$$
L'autoscaling introduce anche un secondo step dopo la centratura:
$$x_i - \overline{x}$$
l'autoscaling divide per la deviazione standard:
$$x'_i = \frac{x_i - \overline{x}}{\sigma_x}$$

E si ottiene $$\text{mean} = 0$$ e approssimativamente $$\sigma^2 = 1$$
Ovvero la dimensione normalizzata, rendendo i descrittori più comparabili numericamente.
La centratura pone solo media = 0. L'autoscaling pone media = 0 e varianza = 1.

### Log-Transform

L'asse delle Y viene log-trasformato spesso, quindi invece di modellare direttamente l'attività (es. IC50) si usa la log-trasformazione
$$pIC_{50} = -\log_{10}(IC_{50})$$

## Variable Selection - Pruning
Andiamo a rimuovere:
- Variabili costanti -> $\text{Varianza} = 0$, ovvero quelle variabili in cui non c'è informazione, non oscillano, e non son