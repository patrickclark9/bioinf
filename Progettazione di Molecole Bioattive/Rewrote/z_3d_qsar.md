# 3D-QSAR

## Introduzione

La 3D-QSAR, a differenza dell'analoga 2D-QSAR, studia e analizza le forze molecolari in tre dimensioni ("i campi") prodotti dalla vicinanza di composti diversi, per trovare correlazioni tra attività biologica e campi.

- Si sfrutta particolarmente quando la struttura del target (es. un recettore) non è del tutto nota.
- La 3D-QSAR si basa sul mappare e confrontare **campi sterici ed elettrostatici** attorno a un insieme di ligandi, per stabilire una QSAR in tre dimensioni.
- Si basa su descrittori tridimensionali, calcolati in diverse posizioni nello spazio attorno alle molecole, risultando in un numero di descrittori enormemente maggiore rispetto alla 2D-QSAR classica.

---

## Interazioni Elettrostatiche

Le interazioni elettrostatiche avvengono tra gruppi polari o carichi. Possono essere attrattive o repulsive:

$$E_{es} = \frac{q_a \, q_b}{r_{ab}}$$

> *Nota: la formula originale riportava $q_a/q_b$ (rapporto) invece di $q_a \cdot q_b$ (prodotto) — corretto qui, poiché l'energia elettrostatica secondo la legge di Coulomb è proporzionale al **prodotto** delle due cariche, non al loro rapporto.*

- Sono calcolate come somma delle interazioni tra cariche puntuali, utilizzando la legge di Coulomb.
- Se $E_{es} > 0$ la forza è repulsiva; se $E_{es} < 0$ è attrattiva.
- L'energia elettrostatica è esprimibile come l'inverso della distanza tra gli atomi che interagiscono: $\dfrac{1}{r}$.

> Poiché dipendono dall'inverso della distanza (e non da una potenza superiore), le interazioni elettrostatiche non sono trascurabili anche quando le molecole sono relativamente distanti tra loro.

---

## Interazioni Steriche

Le interazioni steriche descrivono le interazioni tra atomi non legati, di natura non elettrostatica. Le forze associate, dette di **Van der Waals**, possono essere repulsive o attrattive a seconda della distanza tra gli atomi coinvolti.

$$E_s = \frac{A}{r^{12}} - \frac{B}{r^6}$$

- A corta distanza sono **repulsive**, a causa dell'interpenetrazione delle nuvole elettroniche.
- A distanze maggiori si osserva una leggera forza **attrattiva**.
- Il termine repulsivo dipende dall'inverso della dodicesima potenza della distanza: $\dfrac{1}{r^{12}}$ — motivo per cui la repulsione sterica decade molto rapidamente e diventa trascurabile a distanze anche modeste.

---

## Campi di Interazione

Un campo di interazione può essere misurato solo se qualcosa è in grado di interagirci: a questo scopo si utilizzano sonde, dette **"probe"**.

- Si testa la presenza di un campo posizionando queste sonde in punti selezionati dello spazio, per quantificare il valore del campo della molecola in quel punto.
- La sonda deve essere dello stesso tipo del campo misurato: sonde di Van der Waals per le interazioni steriche, sonde cariche per le interazioni elettrostatiche.

### Grid Tridimensionale

Per semplificare i calcoli, si utilizza una **griglia (grid) tridimensionale** con punti regolarmente distribuiti nello spazio, calcolando le energie di interazione tra molecola e sonda a ogni punto, tramite una funzione dell'energia potenziale. La grid permette di campionare lo spazio con un numero finito di punti, rendendo il calcolo computazionalmente fattibile.

**Campi elettrostatici** — calcolati secondo la legge di Coulomb a ogni punto della grid:

$$E_{es} = \frac{1}{4\pi\epsilon_0} \sum_{i=1}^N \frac{q_i q_p}{r_i}$$

**Campi sterici** — ottenuti calcolando l'energia di interazione di Van der Waals tra molecola e sonda a ogni punto della grid:

$$E_s = \sum_{i=1}^N \left( \frac{A}{r^{12}} - \frac{B}{r^6} \right)$$

### Altri MIF (Molecular Interaction Fields)

Oltre a sterico ed elettrostatico, altri campi di interazione molecolare comunemente utilizzati sono:
- Lipofilicità molecolare
- Campo idrofobico
- Campo donatore di legame idrogeno (H-bond donor)
- Campo accettore di legame idrogeno (H-bond acceptor)

---

## Tecnica GRID

La tecnica GRID viene utilizzata per esplorare, ad esempio, il sito attivo di una proteina. Consiste nel calcolare sistematicamente le energie di interazione tra proteina e sonda, a ogni punto della grid definita.

$$E = \sum E_{ij} + \sum E_{es} + \sum E_{hb} + S$$

dove:
- $E_{ij}$ — termine di Lennard-Jones (interazioni steriche)
- $E_{es}$ — termine elettrostatico
- $E_{hb}$ — potenziale per i legami idrogeno
- $S$ — termine entropico

GRID predice le posizioni con interazioni favorevoli per la sonda, dette **hot spot**. Se vengono utilizzati frammenti come sonde, predice le regioni dove un frammento potrebbe potenzialmente legarsi — informazione utile per il **design de novo** di nuove molecole.

### Requisiti
- Coordinate 3D del target
- Identificazione del sito target
- Un insieme di probe o frammenti

### Considerazioni pratiche
- Se il sito di legame è noto, la grid può essere centrata unicamente sul sito attivo.
- Se non è noto, si può posizionare la grid sull'intera proteina, ma il numero di calcoli cresce rapidamente fino a diventare enorme.
- La scelta dei probe (aromatici, idrofobici, polari, legami salini) dipende dalla natura dei gruppi presenti nel sito attivo.

Il numero totale di calcoli è generalmente pari a:

$$N_{calc} = N_{compounds} \times N_{\text{grid points}} \times N_{probes} \; (\times N_{rotations})$$

---

## Tecnica CoMFA

La **CoMFA** (Comparative Molecular Field Analysis) è un metodo basato sull'assunzione che la distribuzione dei campi di interazione di un composto contenga informazioni rilevanti per comprenderne l'attività biologica.

La CoMFA cerca di correlare l'attività biologica con i valori dei campi in ciascun punto della grid: ogni valore, calcolato per un dato campo in un dato punto (x,y,z), costituisce un descrittore.

### Fasi della CoMFA
1. Un insieme di analoghi (dataset di composti).
2. Una regola di superimposizione (allineamento strutturale).
3. Un reticolo 3D (3D-lattice) di grid point, con il calcolo per ogni molecola delle interazioni con una sonda in ogni punto.
4. Una funzione di correlazione.
5. La validazione della capacità predittiva del modello.

### Assunzioni della CoMFA
- Le molecole condividono lo stesso meccanismo d'azione.
- Sono attive per la stessa ragione.
- Si legano al target nella stessa maniera.
- Il processo di binding è guidato entalpicamente.
- Il termine entropico è simile per tutti i composti.
- Le energie di desolvatazione sono simili per tutti i composti.

### Superimposizione delle Strutture

Tutte le molecole del dataset devono essere allineate tra loro prima del calcolo. Il metodo di allineamento si basa spesso su uno scaffold comune o su punti farmacoforici comuni.

> I modelli CoMFA sono estremamente dipendenti dall'allineamento e dal modo in cui le molecole vengono sovrapposte. È inoltre fondamentale che l'allineamento produca, per tutte le molecole, una conformazione **biologicamente attiva**.

### Calcolo del Modello

Tipicamente la regressione viene effettuata mediante **PLS** (Partial Least Squares), un metodo in grado di:
- Analizzare dati ad elevata dimensionalità rispetto a un numero contenuto di composti.
- Gestire un'elevata collinearità tra i descrittori.

Il modello va validato, come di consueto, con le metriche standard: cross-validazione, test set esterno, Q², ecc.

### Mappe dei Contorni

Riproiettando l'equazione PLS nello spazio dei dati originali, si può utilizzare questa equazione per generare le **mappe dei contorni** (contour maps).

- Una mappa di contorni si crea connettendo i punti della grid con un simile coefficiente favorevole/sfavorevole per un dato campo, moltiplicato per la deviazione standard.
- Le mappe di contorno indicano le regioni dello spazio dove le interazioni sono critiche per l'attività biologica.
- Vengono costruite una per campo, fornendo un'indicazione di quali regioni — per gruppi specifici del campo considerato (elettrostatico, sterico, ecc.) — aumentano o diminuiscono l'attività.
