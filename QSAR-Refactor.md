# [[QSAR]]

## Introduzione

La **[[QSAR]]** (Quantitative Structure-Activity Relationship) è un approccio che tenta di formulare la relazione tra una struttura molecolare e la sua attività biologica, sotto forma di un modello matematico.

La **QSPR** (Quantitative Structure-Property Relationship) è un'estensione della [[QSAR]] che correla la struttura molecolare con qualsiasi altra proprietà molecolare, come solubilità, stabilità metabolica, ecc.

> Per la costruzione di un modello è impossibile connettere tutte le proprietà alla struttura simultaneamente: ogni singola proprietà va considerata una per volta.

La [[QSAR]] tenta di stabilire una relazione matematica tra una struttura molecolare e una proprietà chimica/biologica. Dati _k_ composti, i **descrittori** descrivono la struttura chimica, mentre l'**attività** è la quantità da valutare/predire.

Ponendo la risposta biologica sperimentale come attività:

$$\text{Activity} = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \beta_3 X_3$$

dove:

- $X_1, X_2, X_3, ...$ → descrittori molecolari
- $\beta_1, \beta_2, \beta_3$ → coefficienti stimati da dati sperimentali
- $\beta_0$ → intercetta

Questo è un esempio di modello [[QSAR]] semplice.

### A cosa serve la [[QSAR]]

- Rivelare informazioni riguardo il sito di legame di un recettore.
- Predire l'attività biologica di analoghi non ancora sintetizzati: una volta definito un modello che riproduce correttamente i dati noti, può essere usato per predire l'attività di nuovi analoghi.
- In chimica combinatoriale, ridurre grosse librerie virtuali a dimensioni pratiche per sintesi e screening.

---

## Struttura vs Descrittore vs Attività

È importante distinguere tra:

**Struttura molecolare** — l'effettiva struttura rappresentata in 2D (es. SMILES, grafo molecolare).

> Esempio: benzene → benzene sostituito → fenolo sostituito

**Descrittore molecolare** — rappresentazione numerica di una proprietà della struttura:

- Peso molecolare
- logP
- Superficie polare (polar surface area)
- Numero di donatori/accettori di legame idrogeno
- Volume molecolare
- Polarizzabilità
- Indici topologici
- Parametri elettronici

$$\text{Struttura} \rightarrow \text{Descrittore}$$

**Attività** — quantità sperimentale da predire/spiegare:

- IC50
- EC50
- Affinità di binding
- Percentuale di inibizione
- Tossicità
- Attività enzimatica
- Rate di reazione

> Spesso l'attività viene trasformata in scala logaritmica per ottenere una scala meglio rappresentabile.

### Da SAR qualitativa a [[QSAR]] quantitativa

La [[QSAR]] diventa _quantitativa_ perché tenta di trasformare una semplice SAR (Structure-Activity Relationship qualitativa):

> "Aggiunta di un gruppo idrofobico aumenta l'attività"

in una relazione quantitativa:

> $\text{Activity} = 2.3 + 1.4(\text{lipofilicità}) - 0.8(\text{parametro sterico})$

I coefficienti forniscono direzione e contributo approssimativo di ciascun descrittore. Ad esempio:

$$\text{Activity} = 2 + 1.5\log P$$

Significa che, all'interno di questa serie chimica e dominio, incrementare logP è associato a un incremento nell'attività predetta — **non** che l'incremento di logP _causi_ automaticamente l'incremento di attività.

La [[QSAR]] moderna si basa su tre contributi principali: **Equazione di Hammett**, **Contributo di Hansch**, **Analisi di Free-Wilson**.

---

## Equazione di Hammett

Correla le proprietà elettroniche degli acidi e basi organiche con le costanti di equilibrio.

- La dissociazione consiste nella rimozione di un protone dal composto neutro, lasciando un anione. La reazione è misurata dalla **costante di dissociazione K**.
- Le costanti di dissociazione degli acidi aromatici sono influenzate dalle proprietà elettroniche dei sostituenti sull'**anello fenile**.
- Le costanti di dissociazione di acidi benzoici e fenilacetici sostituiti indicano che i gruppi _electron-withdrawing_ incrementano la dissociazione, mentre i gruppi _electron-donating_ la diminuiscono.

![[Pasted image 20260807095916.png]]

Poiché le costanti di dissociazione sono associate all'energia libera ($\Delta G = -RT\log K$), questa relazione è nota anche come **relazione lineare dell'energia libera**:

$$\log\frac{K}{K_0} = \rho\sigma$$

dove:

- $K$ → costante di reazione per il composto sostituito
- $K_0$ → costante di reazione per il composto di riferimento
- $\rho$ → mette in relazione uno scaffold/equilibrio con un acido benzoico di riferimento; descrive quanto forte è la risposta di una particolare reazione all'effetto di un sostituente elettronico
- $\sigma$ → descrittore che quantifica l'effetto di un sostituente sulla dissociazione: positivo per gruppi accettori di elettroni, negativo per gruppi donatori. Descrive come un sostituente cambia il carattere elettronico di una molecola rispetto all'idrogeno.
    - _Effetto mesomerico_ → risonanza (overlap) dell'orbitale p, relazionata alla topologia della molecola e all'elettronegatività

![[Pasted image 20260807105613.png]]

L'equazione di Hammett è un esempio di **QSPR**: compara una proprietà molecolare (la costante di dissociazione) con un insieme di descrittori molecolari, ρ e σ.

> Il valore di σ differisce a seconda che il sostituente sia in posizione **meta** o **para**.

**[[Nomenclatura]] orto/meta/para**: in chimica organica indicano le posizioni relative di due sostituenti su un anello benzenico:

- **Orto** (1,2) → posizioni adiacenti
- **Meta** (1,3) → separate da un carbonio
- **Para** (1,4) → posizioni opposte

---

## Contributo di Hansch

Hansch riconobbe l'importanza della **lipofilicità** per l'attività biologica, poiché i farmaci devono attraversare il bilayer di membrana per raggiungere i target. La lipofilicità è correlata alla presenza di gruppi idrofobici e all'assenza di gruppi polari/ionizzabili.

### logP

Hansch introdusse il **logP** (coefficiente di partizione tra fase lipidica, 1-octanolo, e fase acquosa) come misura della lipofilicità:

$$P = \frac{[\text{farmaco}]_{organico}}{[\text{farmaco}]_{acquoso}}$$

- P > 1 (logP > 0) → molecola lipofilica
- P < 1 (logP < 0) → molecola idrofilica

**Prima formulazione** (un solo descrittore): $$\text{Activity} = f(\log P)$$

Venne poi introdotto un **termine parabolico** per il logP, per tenere conto delle molecole che rimangono intrappolate nella membrana e non possono raggiungere il sito d'azione. L'equazione [[QSAR]] fu quindi ampliata con nuovi descrittori:

$$\log \frac{1}{C} = a(\log P)^2 + b \log P + c\sigma + dE_s + e$$

### Descrittori del modello di Hansch

**σ — Descrittore elettronico** (vedi equazione di Hammett sopra).

**Es — Descrittore di Taft** (costante sterica): valore sperimentale basato su costanti del rate di un dato modello di reazione. Misura l'effetto sterico esercitato da un sostituente sull'equilibrio — più grande il sostituente, più negativo sarà Es.

$$Es = \log K_x - \log K_H$$

![[Pasted image 20260807105255.png]]

**π — Lipofilicità del sostituente**: caratterizza la lipofilicità di un sostituente specifico. Definito come la differenza tra il logP del composto sostituito e quello non sostituito. Sostituenti più idrofobici dell'H hanno π positivo; sostituenti meno idrofobici dell'H hanno π negativo.

$$\pi = \log P - \log P_H$$

![[Pasted image 20260807104810.png]]

**MR — Rifrazione molare**: descrittore che contiene informazioni sul volume di un composto, corretto per l'indice di rifrazione (rapporto tra velocità della luce nel vuoto e velocità della luce nella sostanza di interesse):

$$MR = \frac{(n^2-1)MW}{(n^2+1)d}$$

![[Pasted image 20260807105055.png]]

con:

- $d$ → densità
- $n$ → indice di rifrazione
- $MW$ → peso molecolare

### Il termine parabolico (logP)²

Il termine quadratico $(\log P)^2$ è particolarmente interessante perché l'attività biologica **non** incrementa indefinitamente con la lipofilicità — esistono punti di massimo globale/locale:

$$\text{Activity} = a\log P - b(\log P)^2$$

Questa equazione produce una relazione a **U rovesciata**: un composto troppo idrofilico non attraversa la membrana, ma un composto troppo idrofobico presenta problemi di solubilità, binding non specifico, o rimane intrappolato nelle membrane idrofobiche.

![[Pasted image 20260807110201.png]]

---

## Analisi di Free-Wilson

Modello matematico basato sull'ipotesi che l'attività biologica sia la somma di tutti i contributi elementari dei sostituenti.

- Invece di descrivere i sostituenti tramite proprietà fisico-chimiche, rappresenta le modifiche strutturali con **variabili indicatore**.
- Utilizza variabili indicatore ($x_i$, con valori 1 o 0) per descrivere la presenza o assenza di un sostituente in una specifica posizione dello scaffold.

$$\log \frac{1}{C} = \sum a_i x_i + \mu$$

dove:

- $a_i$ → peso del sostituente
- $\mu$ → attività media

Funziona particolarmente bene quando si studia una **serie congenerica**, dove i composti differiscono per sostituzioni sistematiche. Il modello è però vincolato alle particolari modifiche strutturali presenti nel dataset.

Il modello si costruisce a partire da una **matrice strutturale** composta da variabili indicatore:

![[Pasted image 20260807111056.png]]

Si utilizza poi la **regressione multipla lineare** per derivare l'equazione [[QSAR]] dalla matrice strutturale:

$$\text{Activity} = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \beta_3 X_3 ...$$

---

## Riepilogo: i tre contributi principali

| Contributo      | Idea chiave                                                                          | Descrittori                  |
| --------------- | ------------------------------------------------------------------------------------ | ---------------------------- |
| **Hammett**     | Relazione lineare dell'energia libera tra sostituenti ed equilibrio di dissociazione | ρ, σ                         |
| **Hansch**      | Lipofilicità come driver del passaggio di membrana, con termine parabolico           | logP, σ, Es, π, MR           |
| **Free-Wilson** | Attività come somma di contributi additivi dei sostituenti                           | Variabili indicatore ($x_i$) |

#  Descrittori Molecolari


Tutte le equazioni [[QSAR]] hanno proprietà molecolari espresse come una funzione di specifici descrittori. Differiscono nelle proprietà che correlano, nei descrittori utilizzati e nell'espressione matematica del modello
![[Pasted image 20260807115016.png]]
I descrittori molecolari sono numeri che catturno la struttura e le proprietà fisico-chimiche della molecola. Per essere utili, i descrittori devono essere biologicamente rilevanti, cioè devono essere in grado di differenziare le molecole attive da quelle inattive.

Si converte la molecola in una serie di descrittori $X_1, X_2, ...,X_k$.


## Classi di Descrittori
### Costituzionali
- Descrivono la composizione molecolare semplice
	- Peso molecolare
	- Numero di Atomi
	- Numero di Atomi di Carbonio
	- Numero di Eteroatomi
	- Numero di Anelli
### Topologici
- Descrivono come gli atomi sono connessi
	- Indice di Wiener
	- Indici di connettività
	- Indici basati su grafi
- Non richiedono struttura 3D. È il motivo per cui questa è chiamata 2D [[QSAR]]

### Fisico-Chimici
- Sono i descrittori come:
	- $\log P$
	- $MW$
	- Donatori di legami idrogeno
	- Accettori di legami idrogeno
- Influenzano
	- Permeabilità di membrana
	- SolubilitàQ
	- Partizionamento
	- Legame a [[proteine]]
### Elettronici
- Descrivono le caratteristiche elettroniche
	- Carica
	- Densità elettronica
	- Sostituenti con effetti eletronici
	- Polarizzabilità
- Diventano importanti se l'attività dipende da una specifica interazione con un target

### Sterici
- Descrivono la dimensione e forma della molecola o gli effetti sterici, due sostituenti possono avere simili caratteristiche chimiche ma differenti effetti sterici

## Selezione dei Descrittori
I descrittori possono essere quindi tantissimi. L'utilizzo di un gran numero di descrittori non è necessariamente un fattore positivo, in quanto spesso molti possono essere:
- Ridodanti
- Correlati tra loro
- Irrilevanti
- Rumorosi
Inoltre utilizzare troppi descrittori può facilmente rendere il modello peggiore a causa dell'overfitting.
Diventa quindi fondamentale e cruciale identificare descrittori che sono rilevanti per un dato problema, quindi identificare i descrittori **rilevanti** e quelli **irrilevanti**, ovvero che ci permettono di differenziare molecole che possiedono una determinata proprietà e quelli che non la possiedono.
I descrittori possono essere estratti sperimentalmente, oppure calcolati. Quelli sperimentali sono spesso complessi da ottenere.


# Modellazione
La costruzione di un modello QSAR è un processo iterativo:
1. Selezione dei composti
2. Selezione dei descrittori
3. Si deriva l'equazione da un insieme iniziale di descrittori
4. Validazione
5. Si migliora il modello aggiungendo/rimuovendo descrittori
6. Si rifinisce l'equazione


## Selezione di Composti

Si inizia costruendo e assemblando un insieme di composti con attività biologica nota. Vanno scelte molecole che definiscono un insieme omogeneo e che meglio rappresentano un determinato sistema.
I composti selezionati per una QSAR dovrebbero coprire un grosso range di valori per i descrittori rilevanti per l'attività biologica.
Ciò incrementa la probabilità che futuri composti avranno descrittori nel range definito e permette di ottenere predizioni interpolative al posto di estrapolative.

**In generale**, predizioni interpolative sono più accurate di quelle estrapolative.
- **Interpolation**: Estimates a value _inside_ the range of known data points. It fills in missing intermediate values or gaps.

- **Extrapolation**: Estimates a value _outside_ the range of known data points. It projects trends into the unknown future or past
### Attività biologica in termini di 1/C

Per riflettere la variazione di energia libera che avviene in un'azione biologica, queste vengono rappresentate come logaritmo della concentrazione del composto ($\log \frac{1}{C}$), dove $C$ è la concentrazione di composto richiesta per produrre una data risposta standard. Attività biologiche devono essere accurate e devono avere span di 2-3 ordini di grandezza
$$E+S \rightarrow ES$$
$$K = \frac{[ES]}{[E][S]}$$
$$\Delta G  = -RT\log K \approx \log \frac{1}{[S]}$$
$$\Delta G \approx \log \frac{1}{[C]}$$

### Outlier
Il modellamento QSAR si basa sull'assunzione di omogeneità e sull'assenza di outlier all'interno del training set.
Un outlier può essere una molecola che si comporta differentemente, un valore incorretto o con attività biologica differente.
Un numero elevato di molecole e ripetute misurazioni aiutano a ridurre le distorsioni imposte dall'outlier.

## Selezione dei Descrittori
Un buon modello QSAR è caratterizzato da un piccolo numero di descrittori scelti accuratamente. Quando troppi descrittori vengono analizzati, incrementa la probabilità che una correlazione casuale possa avenire
### Manuale
Si basa sulla conoscenza del SAR, si scelgono manualmente i descrittori per l'analisi. Ad esempio se analisi preliminari mostrano che sostituenti idrofobici o sterici incrementano l'attività, allora descrittori come $MR$ e $\pi$ saranno sicuramente rilevanti.

### Automatica
Si utilizza un metodo di scoring e ranking automatizzato per andare a selezionare automaticamente i descrittori più rilevanti e selezionari quelli più semplici da interpretare.
Metodi moderni utilizzano algoritmi genetici per effettuare queste predizioni.

L'identificazione sistematica del sottoinsieme migliore di descrittori è ovviamente infattibile, considerando che ogni descrittore può essere inserito oppure no, si hanno $2^{k}$ con $k = descrittori$ possibili sottoinsiemi da esplorare, motivo per cui si usano metodi differenti per la selezione del sottoinsieme migliore di descrittori
#### Forward Selection
Si inizia da un singolo descrittore che meglio si correla con la variabile dipendente. Da qui, ad ogni step iterativo, il modello aggiunge il prossimo descrittore che contribuisce maggiormente al modello. Il processo iterativo termina quando l'aggiunta di un descrittore non migliora le prestazioni del modello, valutate appropriamente con metodologie statistiche rilevanti
#### Backwards Elimination
È l'esatto opposto della forward selection, si utilizzano tutti i descrittori, ad ogni step si rimuove quello che non degrada le prestazioni del modello. Il processo termina quando le prestazioni del modello calano significativamente

#### Stepwise Regression
È un misto dei due precedenti. Si inizia con un singolo descrittore, ma ad ogni step si può aggiungere il prossimo descrittore che migliora le prestazioni del modello e/o si possono togliere descrittori che non influiscono sulle prestazioni del modello. Si termina quando aggiungere o rimuovere descrittori peggiora le prestazioni del modello


#### Descrittori Correlati
L'utilizzo di descrittori correlati, ovvero descrittori che comunicano la stessa informazione su una serie di molecole, va evitato. 
La costruzione di matrici di correlazione aiuta a identificare e rimuovere descrittori fortemente correlati tra loro. Tra tutti quelli correlati si va a selezionare uno solo, gli altri rimossi. Tipicamente si mantiene quello che possiede informazione strutturale più forte, mentre si rimuove quello meno intuitivo, oppure si rimuove quello con la più alta correlazione con altri descrittori.
Ad esempio, un descrittore per il numero di atomi di carbonio ed un descrittore per il peso molecolare per gli alcani saranno ovviamente fortemente correlati tra loro (CnH2n+2)

#### Regola centrale della QSAR
In un buon modello QSAR, il numero di molecole nel training set **eccede** il numero di descrittori di 3-5 volte. 


## Costruzione del modello QSAR

1. Data Matrix -> Matrice Composti e attività + descrittori ![[Pasted image 20260807161631.png]]
2. Analisi grafica dei dati per una preliminare interpretazione dei dati: Aiuta a comprendere se i dati sono ordinati, se sono visibili pattern noti, se questi pattern sono traducibili in espressioni chimico-fisiche![[Pasted image 20260807161745.png]]
3. Scelta dell'equazione: L'analisi preliminare dovrebbe aiutare nella scelta della corretta equazione, che contenga informazioni che riflettono il comportamento e permettono una interpretazione strutturale del sistema. La scelta dell'equazione dipende dalla forma dell'equazione matematica e dal numero di descrittori presi in considerazione. L'analisi può essere una regressione lineare, un modello parabolico, una regressione multipla, o altro.![[Pasted image 20260807162215.png]]
4. Il modello QSAR può essere skewed non intenzionalmente dalla scelta di un modello matematico troppo potente. Un'equazione che modella i dati di un training set può produrre un'equazione che è perfetta per i dati di addestramento ma inutile per dati non noti. Questo fenomeno è noto come overfitting. L'overfitting si verifica quando le prestazioni ottenute in addestramento non si riflettono su dati non visti. Nell'esempio in basso, il modello più complesso si adatta benissimo nei dati di addestramento, ma in presenza di dati nuovi, fallisce nella corretta classificazione della molecola rispetto al modello più semplice, in quanto si è addattato troppo bene ai dati di addestramento, e la curva prodotta non è rappresentativa per dati nuovi![[Pasted image 20260807162727.png]]![[Pasted image 20260807162747.png]]![[Pasted image 20260807162757.png]]![[Pasted image 20260807163053.png]]
	- in un approccio QSAR, non è troppo problematico che l'equazione si adatti alle peculiarità dell'insieme di addestramento. È comunque importante non fittare troppo i dati, in quanto può produrre modelli inutili dal punto di vista della predicibilità

#### Modelli Lineari
##### Regressione Lineare Semplice
Nella forma più semplice di un modello QSAR si ha un modello lineare a singolo descrittore, ed è un modello di regressione lineare semplice
$$y = \beta_o + \beta_1X$$
Con $\beta_0$ intercetta sull'asse delle ordinate e $\beta_1$ la pendenza della retta.
![[Pasted image 20260807163818.png]]

##### Regressione Multipla:
Non è sempre possibile correlare attività biologica con un singolo descrittore, motivo per cui si può estendere il modello QSAR ad utilizzare più descrittori.
In questo caso si fa utilizzo del metodo di regressione multipla MLR.
In questo modello, la linearità viene mantenuta per ognuno dei descrittori individualmente
$$\text{activity} = \beta_0 + \beta_1x_1 + \beta_2x_2 + \beta_3x_3 + ... + \beta_nx_n$$
con $\beta_k$ coefficienti e $x_k$ descrittori.

In questo esempio si vede che la regressione singola per ogni singolo descrittore non produceva una buona correlazione (r =<0.40). L'utilizzo di più descrittori insieme mediante regressione multipla invece produce modelli più accurati (r > 0.8)
![[Pasted image 20260807164129.png]]

##### Analisi dell'equazione MLR
Uno dei motivi per cui si utilizza la QSAR è anche quello di comprendere quali forze governano l'attività di una particolare classe di composti, ed aiutare nel design di farmaci.
Le analisi QSAR aiutano a comprendere la relativa importanza dei descrittori utilizzati, andando a valutare il contributo dei singoli descrittori utilizzati nel modello.
![[Pasted image 20260807164607.png]]
#### Modelli Non Lineari

Una equazione non lineare invece è una estensione del modello di regressione multipla. In alcuni sistemi la linearità potrebbe non essere sufficiente per raggiungere una buona correlazione.
Il termine parabolico introdotto da Hansch fu il primo termine non lineare introdotto.
Ad esempio, l'attività di anticonvulsionanti in un insieme di molecole venne inizialmente trovata come linearmente correlata alla $\log P$ (idrofobicità). Erà però implauisibile assumere che l'attività biologica potesse aumentare indefinitivamente con la lipofilicità delle molecole. È noto che composti troppo lipofilici non possono raggiungere il sito di interesse perchè rimangono incastrati nella membrana, o sono poco solubili.
L'utilizzo di una equazione non lineare ha permesso di dimostrare che esiste un punto di massimo, in cui l'attività raggiungeva il massimo possibile, prima di incominciare a decresce all'aumentare della idrofobicità

![[Pasted image 20260807165100.png]]

##### Modelli Non lineari utilizzati
I modelli non lineari vengono utilizzati per la cinetica del trasporto di molecole, l'equilibrio della sua distribuzione, effetti allosterici, farmacocinetica, metabolismo, solubilità ecc... .
Alcuni dei modelli utilizzati sono:
- Modello Parabolico (Hansch) -> $\log \frac{1}{C} =  a(\log P)^2 +b\log P + c$
- Modello Probabilistico (McFarland) -> $\log \frac{1}{C} =  a(\log P) -2a\log (P+1) + c$
- Modello di Equilibrio (Hyde) -> $\log \frac{1}{C} =  a(\log P)-\log (aP+1) + c$
- Modello Bilineare (Kubinyi) -> $\log \frac{1}{C} =  a(\log P) -b\log (\beta P+1) + c$

## Validazione dei modelli

I modelli vengono validati:
- In fase di addestramento, si valuta quando bene l'equazione QSAR riproduce i dati sperimentali
- In fase di predizione, come il modello si comporta in predizione con nuovi composti

### Deviazione standard
Misura più semplice. Si va a validare il modello computando l'errore standard o deviazione standard $\sigma$. Calcolata come la media del quadrato della deviazione di ogni residuo dalla media. Questo indice riflette la deviazione tra dati e modello. Tanto più stretta, tanto più il modello performa bene
$$\sigma = \sqrt{\frac{\sum {y_{obs} - y_}}{}}$$ 