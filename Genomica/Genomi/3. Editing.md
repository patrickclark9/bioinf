---
publish: true
---
# Modificazioni dell'RNA

L'RNA può subire più di **170 modificazioni** caratterizzate fino ad oggi. Sono presenti abbondantemente negli ncRNA (rRNA, tRNA, snRNA), dove sono importanti per mantenere la funzione durante traduzione e splicing.

Nell'mRNA eucariotico le principali modificazioni sono:

| Modificazione          | Sigla |
| ---------------------- | ----- |
| N6-metiladenosina      | m⁶A   |
| 5-metilcitidina        | m⁵C   |
| Inosina                | A->I  |
| Pseudouridina          | Ψ     |
| N1-metiladenosina      | m¹A   |
| 5-idrossimetilcitidina | hm⁵C  |

La moltitudine di modificazioni ha portato alla creazione del termine **RNA Epigenetics** e, per analogia alla regolazione epigenetica mediata da DNA e istoni, del concetto di **epitrascrittoma**.

---

## RNA Editing

L'RNA editing è una modifica post-trascrizionale che genera molecole di RNA che differiscono dal rispettivo stampo DNA in una o più posizioni, **modificando l'informazione genetica contenuta nel gene**.

### Meccanismi

|Meccanismo|Descrizione|
|---|---|
|**Conversione di base**|Una base viene chimicamente modificata in un'altra|
|**Editing inserzionale**|Inserzione o delezione di nucleotidi|

### Effetti possibili

- Sostituzione di un aminoacido → alterazione delle proprietà strutturali e funzionali della proteina
- Creazione o eliminazione di codoni di inizio/terminazione
- Creazione di intere ORF (nel caso dell'editing inserzionale)

---

## Editing per Conversione

Il processo riguarda solo **siti specifici**, riconosciuti dall'azione enzimatica di fattori proteici o di RNP che riconoscono motivi di sequenza e/o strutturali in prossimità dei siti bersaglio. È regolato in funzione dello:

- Stadio di sviluppo
- Tessuto
- Condizione fisiologica

È un processo diffuso in tutti gli organismi eucarioti, sia per trascritti nucleari sia organellari.

---

### Editing negli Organelli delle Piante

> Nei mitocondri delle piante, specifiche citosine sono deamminate in uracile ad opera di enzimi della famiglia **PPR**. Nei cloroplasti e mitocondri di piante inferiori è stato osservato anche il **reverse editing** (U → C) mediante amminazione. I fattori molecolari coinvolti non sono ancora noti.

L'editing è fortemente **gene- e organismo-dipendente**: uno stesso gene può essere modificato in più o meno posizioni a seconda dell'organismo.

---

### Editing negli Animali

Negli animali, e soprattutto nei mammiferi, l'editing avviene quasi esclusivamente per conversione di basi e **non interessa il mitocondrio**. Nelle cellule umane si osservano due tipi di conversione:

|Conversione|Enzima|Frequenza|
|---|---|---|
|**C → U**|Citidina deamminasi / Transaminasi (reazione inversa)|Rara|
|**A → I**|ADAR (Adenosine Deaminase Acting on RNA)|Molto diffusa|

---

#### Editing C → U

**Esempio principale**: gene dell'**apolipoproteina B** nei vertebrati.

- La conversione C → U in posizione **6666** dell'mRNA avviene **solo nell'intestino**
- Trasforma il codone `CAA` (glutammina) in `UAA` (stop prematuro)
- Risultato: due proteine distinte — **ApoB-100** (fegato, no editing) e **ApoB-48** (intestino, con editing)

---

#### Editing A → I

La deamminazione A → I è diffusa nei pre-mRNA dei mammiferi. Le macchine molecolari (traduzione, spliceosoma) **interpretano l'inosina come guanosina**, quindi il sequenziamento di un RNA editato rivela sostituzioni **A → G**.

**Substrato**: RNA a doppio filamento, formato da:

- Appaiamento esone–introne a valle
- Regioni ripetute in orientamento opposto (es. due elementi Alu)
- RNA a singolo filamento (in alcuni casi)

**dsRNA** -> Endogenous retroviruses, natural sense-antisense transcript pairs, mitochondrial transcripts, and repetitive nuclear sequences, including short and long interspersed elements (SINE and LINEs), are some of the primary sources of endogenous dsRNA

**Enzimi ADAR** -> Adenine deaminase acting on RNA -> Responsabili dell'editing A->I:

| Enzima | Espressione                       | Note                     |
| ------ | --------------------------------- | ------------------------ |
| ADAR1  | Ubiquitaria (nucleo e citoplasma) | Può editare RNA endogeno |
| ADAR2  | Ubiquitaria                       |                          |
| ADAR3  | Solo cervello                     |                          |

**Esempio**: evento su codone `CAG` → `CIG` comporta sostituzione di **glutammina** (CAG) in **arginina** (CIG = CGG). Questa modifica altera la permeabilità al calcio del canale **AMPA**, con potenziali conseguenze a livello del cervello e del sistema ematopoietico.

![[Pasted image 20260419094852.png]]

---

#### Effetti dell'editing A → I

|Regione del trascritto|Effetto|
|---|---|
|**Regione coding**|Sostituzione di AA → formazione di nuove isoforme proteiche|
|**Siti di splicing**|Interferenza con segnali esistenti o creazione di nuovi siti|
|**3'UTR (non-coding)**|Creazione/distruzione di siti di riconoscimento per miRNA|
|**miRNA**|Riprogrammazione del target del miRNA|
|**Sequenza parentale di circRNA**|Interferenza con il processamento del circRNA|
|**Risposta immunitaria**|Prevenzione del misriconoscimento da parte di MDA5 (vedi sotto)|

---

#### Ruolo di ADAR1 nella risposta immunitaria innata

Il ruolo principale dell'editing ADAR1 dsRNA-specifico è **prevenire l'attivazione erronea della risposta immunitaria innata**. In assenza di editing:

1. Il dsRNA endogeno strutturato non viene "mascherato"
2. **MDA5** (pattern recognition receptor citoplasmatico) lo riconosce erroneamente come dsRNA non-self
3. Viene attivato l'**asse MDA5-MAVS** → induzione di risposta infiammatoria/interferonica inappropriata (l'RNA è endogeno)

L'editing da parte di ADAR1 disavvolge la struttura secondaria del dsRNA, **prevenendo il misriconoscimento**. ADAR1 può anche editare il dsRNA virale e partecipare attivamente alla risposta immunitaria.

---

#### Editing in Elementi Ripetuti

L'accoppiamento di ripetizioni invertite è una sorgente primaria di dsRNA endogeno. La variabilità nel numero di queste strutture e l'estensione dell'editing dipende molto probabilmente dal **tipo di elementi ripetuti** presenti nel genoma, data l'elevata variabilità in eventi di editing tra animali diversi. 

| Organismo | Ripetizioni                            | Caratteristiche                                                                             | Editing       |
| --------- | -------------------------------------- | ------------------------------------------------------------------------------------------- | ------------- |
| **Topi**  | Molte famiglie SINE (~100 bp)          | Alta diversità tra famiglie → accoppiamento inverso meno probabile → strutture meno stabili | Minore        |
| **Umani** | Solo famiglia **Alu SINE** (~300 bp)   | Bassa divergenza → target abbondanti e stabili                                              | Elevato       |
| **Rane**  | **Harbinger** (struttura palindromica) | Si ripiega in dsRNA autonomamente, senza necessità di ripetizione fiancheggiante            | Molto elevato |

---
### RNA Editing e Splicing

Lo splicing controlla eventi di editing A→I tessuto-specifici per siti introne-dipendenti. La struttura dsRNA necessaria per l'azione di ADAR si forma attraverso l'appaiamento tra il **sito di editing** e una sequenza complementare chiamata **ECS** (Editing Complementary Site), la cui localizzazione — intronica o esonica — determina il rapporto di dipendenza tra editing e splicing.

![[Pasted image 20260419104050.png]]

---

## Tipi di ECS e la loro relazione con lo Splicing

### ECS Intronica

![[1776588085123_image.png]] _(Licht et al. 2019 Gen. Res. — Pannelli A, C, E)_

Quando l'ECS si trova in un **introne** (pannello A), la struttura dsRNA si forma tra l'esone contenente il sito di editing e la sequenza complementare intronica. L'editing deve quindi avvenire **prima che lo splicing rimuova l'introne**, poiché una volta che l'introne viene escisso l'ECS scompare e la struttura dsRNA non può più formarsi.

**Conseguenza**: esiste una **correlazione negativa** tra il rapporto esone/introne e il livello di editing.

> Più alto è il rapporto esone/introne (cioè più splicing è avvenuto), minore è l'editing osservato — l'introne con l'ECS è già stato rimosso prima che ADAR potesse agire.

**Evidenza sperimentale (pannelli C e E)**: i grafici mostrano correlazioni negative forti per geni con ECS intronica:

- _FLNB_ (intronic): r = −0.75
- _GRIK2_ (intronic): r = −0.70
- _GRIA3_: r = −0.78 **
- _GRIK1_: r = −0.76 **
- _TMEM63B_: r = −0.81 **

La tabella del pannello E riporta tutti i siti di editing con ECS intronica: la maggioranza mostra valori r negativi, molti statisticamente significativi (**), confermando la competizione tra splicing ed editing.
\*\* -> pvalue < 0.01

---

### ECS Esonica

Quando l'ECS si trova in un **esone** (pannello B), la struttura dsRNA si forma tra due regioni esoniche. In questo caso lo splicing **non rimuove l'ECS**, e il legame tra livello di editing e splicing è debole o assente.

**Conseguenza**: la correlazione tra rapporto esone/introne ed editing è vicina a zero o lievemente positiva.

**Evidenza sperimentale (pannello D)**:

- _GABRA3_ (exonic ECS): r = +0.20 → correlazione debole e positiva, coerente con l'indipendenza dall'escissione intronica

---

## Schema Riassuntivo: Competizione Editing–Splicing

```
ECS INTRONICA
─────────────────────────────────────────────────────
Pre-mRNA:   [Esone A]──────[Introne (ECS)]──────[Esone B]
			               ↑ editing dsRNA si forma qui
                  
Se ADAR agisce PRIMA dello splicing → editing avviene ✅
Se splicing avviene PRIMA → introne rimosso, ECS scompare → no editing ❌

Risultato: rapporto esone/introne ↑  →  editing ↓  (r negativo)

ECS ESONICA
─────────────────────────────────────────────────────
Pre-mRNA:   [Esone A (sito)]──[Introne]──[Esone B (ECS)]

Lo splicing non rimuove l'ECS → il dsRNA può formarsi indipendentemente

Risultato: rapporto esone/introne non correla con l'editing  (r ≈ 0)
```

---

## Implicazioni Biologiche

La dipendenza tra editing e splicing introduce un livello aggiuntivo di regolazione post-trascrizionale **tessuto-specifica**:

- Tessuti con **splicing più rapido** o efficiente tenderanno ad avere **meno editing** per i siti con ECS intronica
- Tessuti con **splicing più lento** (o con intron retention) avranno più finestra temporale disponibile per ADAR → **più editing**
- Questo permette la generazione di **diversità proteica tessuto-specifica** partendo dallo stesso gene, attraverso la combinazione di isoformi di splicing e varianti di editing

> Il cervello, dove sia ADAR1 che ADAR2 sono altamente espressi e dove il livello di editing è complessivamente più alto che in altri tessuti, è l'esempio principale di questo tipo di regolazione. Geni come _GRIA2_, _GRIK1_, _GRIK2_ (recettori del glutammato) mostrano editing esteso e tessuto-specifico con ECS introniche.

---
### Applicazioni dell'Editing
**TRIBE** -> Target of RNA-Binding proteins Identified By Editing è un metodo che permette l'identificazione di target  di una RBP di interesse
- Si va a fondere una RBP di scelta con il dominio deaminasico di una ADAR dsRNA specifica. La proteina di fusione lascia una traccia di inosina sull'RNA target della RBP, che può essere trovata attraverso il sequenziamento dell'RNA cercando mismatch A->G

Le ADAR possono essere direzionate verso specifici nucleotidi all'interno del trascrittoma per manipolare le sequenze di RNA senza alcun effetto sul genoma. Tre approcci possibili illustrati

![[Pasted image 20260419121649.png]]![[Pasted image 20260419121731.png]]

--- 
### Editing Detection
Possiamo rilevare l'editing andando a confrontare il locus genomico con il corrispondente cDNA sequenziato con metodologia Sanger.
La maggior parte degli eventi canditati sono stati identificati attraverso analisi computazionali poichè la rilevazioni di eventi di editing non è possibile per esperimenti su larga scala. Allineare mRNA/EST contro il genoma originale per verificare la presenza di eventi A->G è una delle possibilità.