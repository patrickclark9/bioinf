# Validazione della QSAR

## Test Set

- Partizionamento del dato in **training set** e **test set**.
- I composti devono presentare una rappresentatività uniforme.
- Il test set non deve essere né troppo simile al training set (rischio di sovrastima delle prestazioni), né troppo dissimile (predizione troppo difficile).
- Aiuta a identificare l'**overfitting**: se i miglioramenti nel training set non si traducono in una migliore predizione, il modello si è adattato troppo bene ai dati di addestramento, ma non generalizza in fase predittiva.

> L'overfitting diventa problematico spesso quando il modello è troppo complesso. In alcuni casi, tuttavia, la presenza di termini di interazione è necessaria per descrivere un fenomeno complesso — come nell'equazione generale di solvatazione di Abraham, il cui termine $$\sum \alpha_2^H \cdot \sum \beta_2^H$$ rappresenta il prodotto tra l'acidità e la basicità di legame idrogeno dei soluti in soluzione.

### Criteri per un buon test set

- I metodi sperimentali per la determinazione della risposta in training e test devono essere simili.
- I valori delle risposte devono estendersi su ordini di grandezza comparabili, senza eccedere troppo quelli del training set.
- Il rapporto tra molecole attive/inattive tra training e test deve essere simile.

---

## Cross-Validazione

La cross-validazione è un metodo di validazione **interno**, effettuato esclusivamente sul training set. Misura la stabilità e la robustezza del modello matematico — resta comunque necessario un test set indipendente per la validazione esterna.

> Ogni modello deve essere validato con dati nuovi e indipendenti, per evitare il problema della correlazione fortuita.

### Leave-One-Out (LOO)

- Si partiziona il dataset in $k$ partizioni, dove $k = N$ (il numero di campioni).
- Si massimizza il training set: il modello viene addestrato su $N-1$ campioni.
- Si lascia un campione per la validazione.
- A rotazione, ogni data-point viene usato per la validazione.

**Vantaggi:**

- Basso bias — l'utilizzo di quasi tutto il dataset per il training previene l'underfitting.
- Deterministico — gli split sono fissati a priori.

**Svantaggi:**

- Costo computazionale altissimo — dipende da $N$; per $N \gg 500$ significa addestrare un numero enorme di modelli.
- Alta varianza — la predizione può fluttuare in funzione del rumore del singolo campione lasciato fuori.

### K-Fold

- Identico al Leave-One-Out, ma invece di partizionare il dataset con $k=N$, si definisce un valore di $k$ a priori, tipicamente non molto grande (es. $k=5$, $k=10$), a seconda delle dimensioni del campione.
- Il dataset viene partizionato in $k$ parti uguali: $k-1$ fold vengono utilizzati per l'addestramento, 1 fold per la validazione.
- L'addestramento-validazione avviene $k$ volte, così ogni partizione viene usata una volta per la validazione.
- Il risultato medio dei $k$ modelli creati costituisce la metrica delle prestazioni complessive.

**Varianti:**

- **K-Fold stratificato** — ogni partizione contiene più o meno lo stesso rapporto di classi (in regressione: lo stesso valore di risposta medio tra tutte le partizioni).
- **Repeated cross-validation** — il partizionamento viene ripetuto più volte, catturando le prestazioni del modello su più run.

> Il Leave-One-Out è un caso particolare di K-Fold, dove $k = N$.

---

## Q²

Il **Q²** è una metrica statistica utilizzata per valutare il potere predittivo e la generalizzabilità di un modello.

### PRESS

La **PRESS** (Predictive Error Sum of Squares):

$$\text{PRESS} = \sum_{i=1}^{N} (y_i - \hat{y}_{i/i})^2$$

È analoga alla RSS, ma calcolata sul valore predetto $\hat{y}_{i/i}$ per l'i-esimo campione, ottenuto da un modello in cui quel campione **non** è stato utilizzato in training. Viene calcolata tramite Leave-One-Out.

### Formula del Q²

Utilizzando la PRESS al posto della RSS, si ottiene la percentuale di varianza spiegata dal modello **in predizione**:

$$Q^2 = R^2_{CV} = 1 - \frac{\text{PRESS}}{\text{TSS}}$$

- A differenza dell'R² (ma similmente all'R² aggiustato), il Q² presenta un massimo in corrispondenza della complessità ottimale del modello, e ridiscende quando si aggiungono variabili non predittive.
- Il Q² viene esplicitamente calcolato per esprimere una misura **predittiva**, non descrittiva (di fitting), del modello.

![[Pasted image 20260809170446.png]]

> Non esiste correlazione garantita tra Q² e la predizione sul test set ($R^2_{pred}$): non vi è necessariamente relazione tra predizione interna ed esterna. Spesso, ad una maggiore predizione interna corrisponde una predizione esterna più bassa.

---

## Y-Scrambling

Procedura:

1. Si valutano le prestazioni predittive del modello permutando (shuffle) la variabile target $Y$, lasciando immutate le $X$.
2. Le etichette/valori di $Y$ vengono riorganizzati casualmente.
3. Il modello viene riaddestrato sui dati "scrambled", utilizzando le stesse feature di input.
4. Vengono raccolte le metriche di prestazione.
5. Si ripetono scrambling e addestramento molte volte, costruendo una distribuzione di score casuali.
6. Il modello originale viene confrontato contro questa distribuzione: se lo score originale è significativamente più alto, il modello possiede un potere predittivo effettivo.

**Utilità:**

- Aiuta a visualizzare eventuale overfitting.
- Espone correlazioni dovute al caso.
- Ampiamente utilizzato nei modelli QSAR per validare modelli relazionali struttura-attività.

---

## Classificazione

- Le prestazioni sono tipicamente valutate mediante **matrici di confusione**.
- Metriche principali: **Accuratezza**, **Precisione** e **Richiamo (Recall)**.

![[Pasted image 20260809174014.png]]

---

## Modelli di Classificazione per QSAR

Quando l'obiettivo non è predire un valore continuo (es. IC50) ma assegnare i composti a una categoria (es. attivo/inattivo, tossico/non tossico), si utilizzano modelli di **classificazione** anziché di regressione.

### Alberi Decisionali (Decision Trees)

- Suddividono ripetutamente lo spazio dei descrittori in base a soglie su singole variabili, costruendo una struttura ad albero di regole if/then.
- Ogni nodo interno rappresenta un test su un descrittore (es. "logP > 3?"), ogni foglia rappresenta una classe finale (attivo/inattivo).
- **Vantaggi**: facilmente interpretabili, permettono di identificare visivamente quali descrittori guidano la classificazione.
- **Svantaggi**: tendenza all'overfitting se l'albero cresce troppo in profondità; instabili a piccole variazioni nel dataset.
- Estensioni come **Random Forest** combinano molti alberi per ridurre la varianza e migliorare la generalizzazione.

### SVM (Support Vector Machine)

- Cerca l'iperpiano che meglio separa le classi nello spazio dei descrittori, massimizzando il margine tra le classi (i punti più vicini all'iperpiano, i "support vector").
- Per dati non linearmente separabili, utilizza il **kernel trick** (es. kernel RBF) per proiettare i dati in uno spazio a dimensionalità superiore, dove diventano separabili.
- **Vantaggi**: efficace anche con un numero elevato di descrittori rispetto al numero di composti; robusto all'overfitting grazie alla massimizzazione del margine.
- **Svantaggi**: meno interpretabile rispetto agli alberi; la scelta del kernel e dei suoi iperparametri richiede tuning accurato.

### KNN (K-Nearest Neighbors)

- Classifica un nuovo composto sulla base della classe maggioritaria tra i suoi **K vicini più prossimi** nello spazio dei descrittori, secondo una data misura di distanza (es. Euclidea, Tanimoto per fingerprint).
- Non richiede una fase di addestramento esplicita (metodo "lazy"): la predizione avviene calcolando le distanze al momento della classificazione.
- **Vantaggi**: semplice, intuitivo, si adatta naturalmente a confini di decisione complessi e non lineari.
- **Svantaggi**: computazionalmente costoso su grandi dataset (deve calcolare la distanza da tutti i punti); sensibile alla scelta di K e alla scala dei descrittori (richiede normalizzazione).

> La scelta del modello dipende dal compromesso tra **interpretabilità** (favorita da alberi decisionali) e **capacità predittiva su relazioni complesse e non lineari** (favorita da SVM e KNN) — un compromesso analogo a quello già visto tra modelli QSAR lineari e non lineari.