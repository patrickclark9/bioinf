# QSAR

## Introduzione

La **QSAR** (Quantitative Structure-Activity Relationship) è un approccio che tenta di formulare la relazione tra una struttura molecolare e la sua attività biologica, sotto forma di un modello matematico.

La **QSPR** (Quantitative Structure-Property Relationship) è un'estensione della QSAR che correla la struttura molecolare con qualsiasi altra proprietà molecolare, come solubilità, stabilità metabolica, ecc.

> Per la costruzione di un modello è impossibile connettere tutte le proprietà alla struttura simultaneamente: ogni singola proprietà va considerata una per volta.

La QSAR tenta di stabilire una relazione matematica tra una struttura molecolare e una proprietà chimica/biologica. Dati _k_ composti, i **descrittori** descrivono la struttura chimica, mentre l'**attività** è la quantità da valutare/predire.

Ponendo la risposta biologica sperimentale come attività:

$$\text{Activity} = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \beta_3 X_3$$

dove:

- $X_1, X_2, X_3, ...$ → descrittori molecolari
- $\beta_1, \beta_2, \beta_3$ → coefficienti stimati da dati sperimentali
- $\beta_0$ → intercetta

Questo è un esempio di modello QSAR semplice.

### A cosa serve la QSAR

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

### Da SAR qualitativa a QSAR quantitativa

La QSAR diventa _quantitativa_ perché tenta di trasformare una semplice SAR (Structure-Activity Relationship qualitativa):

> "Aggiunta di un gruppo idrofobico aumenta l'attività"

in una relazione quantitativa:

> $\text{Activity} = 2.3 + 1.4(\text{lipofilicità}) - 0.8(\text{parametro sterico})$

I coefficienti forniscono direzione e contributo approssimativo di ciascun descrittore. Ad esempio:

$$\text{Activity} = 2 + 1.5\log P$$

Significa che, all'interno di questa serie chimica e dominio, incrementare logP è associato a un incremento nell'attività predetta — **non** che l'incremento di logP _causi_ automaticamente l'incremento di attività.

La QSAR moderna si basa su tre contributi principali: **Equazione di Hammett**, **Contributo di Hansch**, **Analisi di Free-Wilson**.

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

**Nomenclatura orto/meta/para**: in chimica organica indicano le posizioni relative di due sostituenti su un anello benzenico:

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

Venne poi introdotto un **termine parabolico** per il logP, per tenere conto delle molecole che rimangono intrappolate nella membrana e non possono raggiungere il sito d'azione. L'equazione QSAR fu quindi ampliata con nuovi descrittori:

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

Si utilizza poi la **regressione multipla lineare** per derivare l'equazione QSAR dalla matrice strutturale:

$$\text{Activity} = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \beta_3 X_3 ...$$

---

## Riepilogo: i tre contributi principali

| Contributo      | Idea chiave                                                                          | Descrittori                  |
| --------------- | ------------------------------------------------------------------------------------ | ---------------------------- |
| **Hammett**     | Relazione lineare dell'energia libera tra sostituenti ed equilibrio di dissociazione | ρ, σ                         |
| **Hansch**      | Lipofilicità come driver del passaggio di membrana, con termine parabolico           | logP, σ, Es, π, MR           |
| **Free-Wilson** | Attività come somma di contributi additivi dei sostituenti                           | Variabili indicatore ($x_i$) |

#  Descrittori Molecolari
I descrittori molecolari sono numeri che catturno la struttura e le proprietà fisico-chimiche della molecola. Per essere utili, i descrittori devono essere biologicamente rilevanti, cioè devono essere in grado di differenziare le molecole attive da quelle inattive.
