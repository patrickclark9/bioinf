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
$$\sigma = \sqrt{\frac{\sum {(y_{obs} - y_{calc})^2}}{n-m-1}}$$ con $n$ dimensione del campione, $m$ numero di descrittori, $y_{obs}$ attività osservata, $y_{calc}$ attività calcolata

### Indice di correlazione
L'indice di correlazione $r^2$, che è il quadrato del coefficiente di correlazione. $r^2$ misura il grado di correlazione tra i valori di attività calcolati dal modello e quelli misurati sperimentalmente.
$r^2 \in [0,1]$
![[Pasted image 20260807172125.png]]

### T-test
Il test di Student utilizza la distribuzione t per testare se il coefficiente di correlazione ottenuto dalla QSAR è significativamente diverso da 0.
Tanto più grande $t$, tanto più grande la probabilità che $r^2$ differisca da 0, ovvero è più probabile che il descrittore utilizzato per l'analisi sia rilevante per l'attività.
- **One-Sample t-Test**: Compares the mean of a single group against a known or target value. 

- **Independent Two-Sample t-Test**: Compares the means of two completely separate and unrelated groups (such as a control group vs. a treatment group).

- **Paired Samples t-Test**: Compares the means from the same group at two different times, such as a "before and after" intervention measurement.
1. Si calcola $t$ come $t = r\sqrt{\frac{N-2}{1-r^2}}$
2. Si seleziona un grado di significatività (e.g. 0.05)
3. Si cerca il valore di $t$ all'interno della distribuzione T derivato per il corretto numero di campioni N al livello di significatività posto
4. Se il valore di $t$ calcolato è più grande del valore di $t$ tabulato, allora l'equazione di regressione è significativa a quel dato grado di significatività


#### Assunzioni
- I campioni seguono distribuzione circa Normale
- I campioni sono indipendenti tra loro e selezionati casualmente
- Nella variante indipendente, i due gruppi di campioni devono avere varianza simile
### F-test
Simile al T-test come svolgimento ma utilizza la distribuzione F di Fisher.  Valuta se un insieme di variabili indipendenti collettivamente spiegano un quantitativo significativo di varianza della variabile dipendente rispetto ad un modello basilare. Utilizzato anche per comparare la varianza tra due popolazioni
- **Comparing Two Variances:** Tests whether two population variances are equal by dividing the larger sample variance by the smaller one. 

- **Analysis of Variance (ANOVA):** Tests if the means of three or more groups are significantly different by comparing between-group variance to within-group variance. 

- **Regression Analysis:** Evaluates whether a set of independent variables collectively explains a significant amount of variance in the dependent variable compared to a baseline model

1. Si calcola $F$ come $F = \frac{r^2(N-k-1)}{k(1-r^2)}$
2. Si seleziona un grado di significatività (e.g. 0.05)
3. Si cerca il valore di $F$ all'interno della distribuzione F derivato per il corretto numero di campioni N al livello di significatività posto
4. Se il valore di $F$ calcolato è più grande del valore di $F$ tabulato, allora l'equazione di regressione è significativa a quel dato grado di significatività
#### Assunzioni
- I campioni seguono distribuzione circa Normale
- I campioni devono essere indipendenti e selezionati casualmente


### Valutare il Potere Predittivo del modello
I test precedenti possono essere utilizzati per valutare i risultati di una QSAR. Questi parametri però sono utili solo per valutare l'abilità del modello QSAR nel riprodurre i dati di addestramento, non servono per valutare la qualità della predizione nell'attività per composti mai osservati.

Per valutare il potere predittivo del modello si utilizza il metodo del "Test-set", ovvero partizionare i dati di partenza in due insiemi separati, uno di addestramento ed uno di validazione, ed è la strategia preferita quando il numero di composti iniziale è molto grande.
L'insieme di partenza viene diviso in due parti in maniera del tutto casuale, la prima viene utilizzata per costruire e addestrare il modello QSAR, il secondo viene utilizzato per validare il modello QSAR.

## Finale
- **Diversity**
- **Relevance**
- **Reliability**
- **Prediction**

These can be understood as follows.

### Diversity

Does the dataset cover sufficiently diverse chemical structures?

If all molecules are almost identical, the model may have limited scope.

### Relevance

Are the chosen descriptors actually related to the biological phenomenon?

### Reliability

Is the model statistically robust and properly validated?

### Prediction

Can it successfully predict new compounds?

A model should ideally satisfy **all four**, rather than merely having a high R2.
# Why R2 alone is insufficient

Suppose:

R2=0.98

It is tempting to conclude:

> Excellent QSAR model.

But that can be misleading.

A sufficiently complex model can achieve a very high R2 simply because it has enough parameters to fit the training data.

Therefore, you need to consider things such as:

- training performance
- test-set performance
- cross-validation
- number of descriptors
- dataset size
- outliers
- applicability domain
- chemical diversity

This is essentially the reason separates **modelling** from **model quality**.