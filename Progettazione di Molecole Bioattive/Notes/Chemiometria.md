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
- Variabili costanti -> $\text{Varianza} = 0$, ovvero quelle variabili in cui non c'è informazione, non oscillano, e non sono utili alla distinzione dei composti
- Variabili quasi costanti -> $\text{Varianza} \approx 0$, come sopra, ma c'è un minimo di variazione, non molto informativa
- Variabili correlate -> Possono essere raggruppate in gruppi di correlazione, e poi scegliere quelle maggiormente correlate alla risposta/attività, rimuovendo le altre. 
- Variabili correlate TRA loro -> Rimuovere l'informazione ridodante, dovuta a correlazione TRA descrtittori
- Gestione dei valori mancanti -> Dipendente dal modello, bisogna gestire eventualmente i dati mancanti. Le opzioni sono
	- Rimozione dei composti problematici per cui mancano dati
	- Imputazione dei valori
	- Ricalcolo dei descrittori
	- Utilizzo di algoritmi che possono gestire dati mancanti per alcune feature
	- L'approccio corretto dipende dalla ragione per cui manca il dato

## Correlazione
Suppose:

r=0.95

You might think:

> Excellent descriptor!

But you still have to ask:

- Is the relationship causal?
- Is it just correlation?
- Is the descriptor redundant with another descriptor?
- Does it work on new compounds?
- Is the relationship linear?
- Is there an outlier driving the correlation?
- Is the compound inside the applicability domain?

Therefore:

high correlation=validated QSAR model

Conceptually:

r=σX​σY​cov(X,Y)​
with:

−1≤r≤1

### r=1

Perfect positive linear relationship.

### r=0

No linear relationship.

### r=−1

Perfect negative linear relationship.

For example:

X↑⇒Y↑

gives positive correlation.



