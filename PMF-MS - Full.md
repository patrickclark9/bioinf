# Spettrometria di Massa

Tutti gli spettrometri di massa misurano le molecole in stati ionizzati. Tutti i valori determinati da MS sono relativi al rapporto m/z:

$$m/z = (m_i + (m_A \cdot z)) / z$$

---

## MALDI/TOF

Ottimo per il **PMF (Peptide Mass Fingerprinting)**.

**Vantaggi**

- Veloce e facile da misurare
- Tollerante ai sali (più rispetto agli altri metodi → Crosta bianca)
- Funziona relativamente bene anche con molecole ad alto peso molecolare
- Nessun limite temporale → campione su supporto stabile
- Genera principalmente ioni +1, rari ioni multicarica

**Svantaggi**

- Elevata accuratezza richiede calibrazione
- MS/MS è complessa da effettuare con MALDI
- Il segnale può essere soppresso in miscele complesse
- Le condizioni di cristallizzazione influenzano i risultati

![[Pasted image 20260618083515.png| MALDI Tryptic Digest]]

---

## Elettrospray (ESI)

Perfetta per **MS/MS**, può essere accoppiata direttamente a HPLC (in fase inversa) e genera ioni 2+/3+.

**Vantaggi**

- Accoppiamento diretto con HPLC
- Genera ioni 2+/3+, molto utili per peptidi triptici

**Svantaggi**

- L'introduzione di campioni è più complessa
- L'analisi è più complessa data la presenza di ioni 2+ e 3+
- One-shot analysis → limiti di tempo, il picco sparisce
- Bassa tolleranza agli agenti contaminanti

### Perché 2+/3+ è utile per peptidi triptici

La tripsina taglia il C-terminale vicino a Lys e Arg → ogni peptide ha un residuo basico al C-terminale (Lys K o Arg R), oltre a un N-terminale libero → **almeno due siti di protonazione**.

### Charge state e spaziatura isotopica

|Charge state (z)|Spacing tra picchi isotopici|
|---|---|
|1+|Δm = 1.0 Da|
|2+|Δm = 0.5 Da|
|3+|Δm = 0.33 Da|

Regola generale: $z = 1 / \Delta m_{\text{isotope}}$

---

## MS vs MS/MS

### MS (singolo stadio)

1. Produzione di ioni
2. Separazione di ioni
3. Detection

### MS/MS (tandem)

1. Produzione di ioni
2. Separazione di ioni (selezione del parent)
3. Frammentazione CID → generazione daughter
4. Separazione degli ioni daughter
5. Detection

### Schema fisico del tandem MS

```
MS1 → Collision Cell → MS2
```

- **MS1** → seleziona ioni a un particolare m/z (è sostanzialmente una sorgente ionica per MS2)
- **Collision cell** → gas neutrale ad alta pressione (He, Ar, N₂); l'energia cinetica viene convertita in energia interna → rottura di legami
- **MS2** → analizza gli ioni daughter

In MS1 si ionizza il campione, poi un singolo ione è selezionato (quadrupolo, settore magnetico, ion cyclotron resonance). Solo un tipo di ione passa nella camera di collisione. In MS2, gli ioni daughter vengono rilevati e lo spettro finale è composto dai picchi dello ione selezionato e di tutti i suoi daughter.

![[Pasted image 20260618090804.png]]

### Principio delle reazioni filiate

Lo spettro di un composto complesso è difficilmente interpretabile: si osservano molti picchi e i più intensi corrispondono al costituente maggiore, rendendo complessa l'identificazione di un singolo composto. Selezionando un singolo precursore e frammentandolo si ottiene uno **spettro diagnostico** per la struttura della molecola.

### Output di MS/MS

- **MS1** → masse dei peptidi intatti
- **MS/MS** → ioni di frammento → informazione di sequenza (pseudo-sequenza)
- Eseguito per **molti peptidi** in un campione → ~**uno spettro MS/MS per peptide precursore selezionato**
- Acquisizione di file ortogonali multipli (1 spettro per peptide)

> "Intatto" è relativo a MS/MS: il peptide non è ancora stato rotto nella Collision Chamber.

### Serie ioniche (CID)

CID rompe legami peptidici lungo il backbone, risultando in frammenti classificati in base al terminale ritenuto e al legame rotto:

|Ion series|Terminale ritenuto|Legame rotto|Note|
|---|---|---|---|
|**a**|N-terminale|Cα–CO|= b − 28 Da (perdita di CO)|
|**b**|N-terminale|CO–N|Serie N-terminale più comune|
|**c**|N-terminale|N–Cα|Meno comune|
|**x**|C-terminale|CO–N|Raro|
|**y**|C-terminale|N–Cα|Serie C-terminale più comune|
|**z**|C-terminale|Cα–CO|Meno comune|

Negli spettri di frammentazione di peptidi triptici si osservano spesso **serie y e b**. Lo ione y₁ a 147 Da (Lys) o 175 Da (Arg) è caratteristico del residuo basico terminale lasciato dalla tripsina.

![[Pasted image 20260618093635.png]] ![[Pasted image 20260618093642.png]]

---

## Identificazione di Proteine per Spettrometria di Massa

La tripsina digerisce una proteina in un insieme di peptidi con massa prevedibile. Il pattern specifico di masse dei peptidi è una **fingerprint unica** (o quasi unica) per una proteina.

![[Pasted image 20260618094554.png]]

### Workflow PMF (MALDI-TOF)

```
Banda proteica (SDS-PAGE)
    ↓  digestione in-gel con tripsina
Miscela di peptidi
    ↓  MALDI-TOF MS
Lista di picchi (valori m/z degli ioni peptidici)
    ↓  ricerca in database (digestione in silico di tutte le proteine)
Identificazione della proteina
```

Data una lista di picchi, si confronta contro liste di masse ioniche di peptidi generate da un database di sequenze proteiche.

### Effetto dell'accuratezza di massa (specificità della ricerca)

|Accuratezza|Tolleranza (Da)|Hits (esempio)|
|---|---|---|
|Bassa|1.0|478|
|Media|0.1|164|
|Alta|0.01|25|
|Molto alta|0.001|4|
|Ultrahigh|0.0001|2|

> **L'accuratezza di massa è il singolo fattore più determinante per la specificità della ricerca in PMF.**

### Effetto del numero di peptidi interrogati (tolleranza fissa 0.1 Da)

|Peptidi interrogati|Hits|
|---|---|
|1 peptide|204|
|2 peptidi|7|
|3 peptidi|1|

> **Più peptidi = identificazione esponenzialmente più specifica.**

### Parametri di ricerca (Mascot / ProFound)

|Parametro|Valore tipico / Note|
|---|---|
|**Database**|UniProtKB/SwissProt, NCBInr, ecc.|
|**Tassonomia**|Restringere all'organismo quando possibile (riduce lo spazio di ricerca)|
|**Enzima**|Tripsina (taglia C-terminale a Lys/Arg, non prima di Pro)|
|**Missed cleavages**|1–2 (digestione incompleta)|
|**Modificazioni fisse**|Carbamidometil (C) — da alchilazione con iodoacetamide durante la prep del gel. Dipende dalla tecnica; possono non esserci modificazioni fisse.|
|**Modificazioni variabili**|Ossidazione (M) — ossidazione della catena laterale di Met è un artefatto comune|
|**Valori di massa**|MH⁺ (monoisotopico preferito per strumenti ad alta risoluzione)|
|**Tolleranza**|in Da o ppm|

I dati possono essere importati da file oppure inseriti manualmente come lista di picchi m/z. ProFound è molto simile a Mascot; le modificazioni parziali tipiche includono l'ossidazione della metionina, ma se ne possono aggiungere altre in entrambi gli strumenti.

### Mascot Score

$$\text{Score} = -10 \times \log(P)$$

dove P = probabilità che il match sia casuale. Score > 50–63 sono tipicamente significativi (p < 0.05) — la soglia dipende dalla dimensione del database.

### Output: Sequence Coverage Map

I peptidi matched vengono evidenziati nella sequenza proteica. La **sequence coverage (%)** rappresenta la frazione della proteina coperta dai peptidi identificati.

---

## Identificazione di Proteine per MS/MS

### Limiti del PMF

- Richiede proteine relativamente pure
- Non riesce a gestire miscele complesse
- Non fornisce informazioni di sequenza del peptide

MS/MS invece fornisce informazioni di **pseudo-sequenza per peptide** ed è compatibile con l'analisi di miscele complesse → **Shotgun Proteomics**

---

### Automated LC-ESI-MS/MS (Shotgun Proteomics)

#### Setup LC (nanoLC)

- Colonna a fase inversa C₁₈: lunghezza 15–25 cm, diametro interno 75 μm
- Flow rate: 200–300 nL/min (T-splitter da pompa HPLC standard)
- Gradiente di solvente organico (tipicamente MeCN/H₂O + 0.1% acido formico) → eluisce i peptidi per idrofobicità

#### Data-Dependent Acquisition (DDA)

Lo spettrometro di massa automaticamente:

1. Acquisisce uno scan MS1 completo (TIC/survey scan)
2. Seleziona i top-N precursori più intensi
3. Isola ciascuno in sequenza e frammenta per CID
4. Acquisisce lo spettro MS/MS per ciascuno

→ Una singola corsa LC genera centinaia/migliaia di spettri MS/MS, ciascuno (idealmente) da un peptide distinto.

#### Data-Independent Acquisition (DIA)

La logica di selezione in MS1 cambia:

- MS1 può ancora acquisire scan completi, ma lo strumento frammenta **tutti** gli ioni all'interno di finestre m/z ampie (es. chunk da 25 Da)
- Nessuna selezione del picco più intenso — tutto viene frammentato in modo sistematico

---

### Database Search (MS/MS)

Ogni spettro MS/MS viene ricercato contro un database: per ogni proteina candidata si computa il numero teorico di ioni b/y, e si cercano match con gli ioni osservati. Mascot riporta:

- **Score peptidico individuale** per ogni spettro
- **Overall protein score** → somma degli score peptidici significativi

---

### Ortogonalità

Ogni spettro di frammentazione è un dataset indipendente (ortogonale) legato a una specifica sequenza. Data la probabilità $P_i$ che un match sia dovuto al caso per lo spettro $i$:

$$P(\text{due match casuali alla stessa proteina}) = P_1^2$$

Esempio: $P_1 = 5 \times 10^{-3}$ → $P_2 = 2.5 \times 10^{-5}$ — due ordini di grandezza più stringente.

La probabilità che due spettri distinti matchino la stessa sequenza per caso è due ordini di grandezza inferiore rispetto a un singolo spettro. In generale, **si necessitano almeno 2 peptidi per proteina** per ottenere confidenza sufficiente. Ogni peptide è assegnato univocamente alla sua sequenza parent → molte proteine identificabili per run.

---

### Distinzione Critica

> **Identificazione proteica ≠ Caratterizzazione proteica**

- Due peptidi sono **sufficienti per identificare** una proteina
- Ma si stanno caratterizzando **solo quei due peptidi**
- Sequenze molto simili (isoforme, paraloghi) possono non essere distinguibili
- Per rilevare PTM è essenziale una **coverage di sequenza estesa**

---

## Proteomica Quantitativa (Shotgun) — Isotope Labelling

La MS non è inerentemente quantitativa: i segnali ionici dipendono dall'efficienza di ionizzazione, che varia per peptide e per run. Per comparare l'abbondanza tra campione A e campione B si sfrutta il **labelling isotropico**:

1. Si etichetta ogni campione con reagenti chimicamente identici ma con isotopi diversi
2. Si mescolano i campioni → co-analisi → le coppie isotopo leggero/pesante coeluiscono in LC e vengono distinte per massa
3. La massa degli ioni frammento identifica la sequenza peptidica
4. Si quantifica analizzando l'area del picco

> Mescolare prima rimuove variabilità analitica downstream.

**Tipi di labelling**

- **Post-sintesi proteica**: modificazioni specifiche sulla catena amminoacidica. Applicabile a qualsiasi campione, ma possono avvenire reazioni indesiderate.
- **Metabolico**: incorporazione di amminoacidi etichettati durante la sintesi proteica. Usa proteine native (no modifiche alle catene laterali), ma richiede un organismo coltivabile.

---

### ICAT — Isotopically Coded Affinity Tagging

Sfrutta marcatura H/D (8 Da di separazione) o ¹²C/¹³C (9 Da). Il deuterio interagisce con la fase stazionaria della colonna → si è passati al carbonio.

**Struttura del reagente**

- **Biotin tag** → isolazione per affinità dei peptidi etichettati (streptavidina)
- **Linker chain** (H o D, 8 Da di differenza)
- **Reactive group** → tipicamente iodoacetamide → lega residui Cys (tio-alchilazione)

![[Pasted image 20260618155459.png]]

**Workflow**: un campione è etichettato con la sonda leggera (d0), l'altro con quella pesante (d8). I campioni vengono combinati, digeriti con tripsina e soggetti a cromatografia di affinità con avidina per isolare i peptidi etichettati. L'analisi LC-MS permette di quantificare i rapporti di intensità delle coppie di peptidi.

|---|---|
| **Pro** | Applicabile a qualsiasi campione; bassa complessità (solo peptidi con Cys); variabilità ridotta mescolando all'inizio |
| **Contro** | Copre solo 50–70% delle proteine (quelle con ≥1 Cys); possibili reazioni con altri residui; perdita durante purificazione con streptavidina |
|---|---|

---

### iTRAQ — Isobaric Tags for Relative and Absolute Quantitation

Permette di etichettare e comparare fino a **4 campioni** (o 8 con versioni estese) in una singola analisi.

**Principio**

- **Reactive group**: NHS ester → reagisce con N-terminale e Lys ε-ammina
- Le proteine vengono digerite prima dell'etichettatura
- Nessuna riduzione dovuta alla composizione amminoacidica → si analizzano tutti i peptidi

**Innovazione chiave**: 4 reagenti con **massa totale identica (145 Da)** ma distribuzione interna diversa — il gruppo reporter porta la differenza di massa (114, 115, 116, 117 Da).

Poiché la massa totale del tag è 145 Da per tutti i reagenti, lo stesso peptide dai 4 campioni ha lo **stesso precursore m/z in MS1** → tutti e 4 vengono co-isolati per frammentazione in un singolo evento MS/MS.

**MS/MS fornisce due tipi di informazione simultaneamente**

- **Reporter ions** (regione 114–117 Da): abbondanza relativa del peptide nei 4 campioni → **quantificazione**
- **Ioni b/y**: sequenza peptidica → **identificazione**

**Workflow**

```
Campione 1 → digest → [114-tag] ──┐
Campione 2 → digest → [115-tag] ──┤
Campione 3 → digest → [116-tag] ──┤ → Mix → frazionamento SCX → nanoLC-MS/MS
Campione 4 → digest → [117-tag] ──┘
```

|||
|---|---|
|**Pro**|4 (o 8) campioni per run; qualsiasi proteina (non limitato a Cys); un singolo evento MS/MS fornisce sia ID sia quantificazione|
|**Contro**|Richiede MS/MS per quantificare (non quantificabile da MS1); co-isolazione isobarica può causare ratio compression; analisi dati più complessa|

---

### SILAC — Stable Isotope Labelling by Amino Acids in Cell Culture

Labelling metabolico: le cellule vengono cresciute in terreno dove un amminoacido specifico è sostituito dalla versione con isotopo pesante.

**Label comuni**

- ¹³C₃-Leucina ("Leu D3") vs. leucina normale → 3 Da per residuo Leu
- ¹³C₆-Arg / ¹³C₆-Lys ("heavy SILAC") → attualmente più comune

Dopo ~5 divisioni cellulari, essenzialmente tutte le proteine sono completamente etichettate.

**Workflow**

```
Cellule light (controllo)              Cellule heavy (stimolate)
        ↓                                       ↓
  Crescita in terreno normale          Crescita in terreno ¹³C/¹⁵N-AA
        └────────── Mix subito dopo lisi ───────────┘
                           ↓
         (Opzionale: immunoprecipitazione / frazionamento)
                           ↓
                      LC-MS/MS
                    ↓           ↓
          Identificazione    Quantificazione
           (MS/MS)        (rapporto area picchi MS1 heavy/light)
```

Il mass shift è variabile (dipende dal numero di residui etichettati per peptide) — ben gestito da software come MaxQuant.

|---|---|
|**Pro**|Nessuna modificazione chimica; peptidi nativi; variabilità minima (mescolati prima di qualsiasi manipolazione); quantificazione a livello MS1 (no ratio compression da co-isolazione)|
|**Contro**|Applicabile solo a organismi coltivabili; tipicamente limitato a 2–3 condizioni (light/medium/heavy); non applicabile direttamente a tessuti o campioni clinici|
|---|---|


---

## Applicazioni

### 2D-PAGE + MALDI-TOF PMF

Le proteine vengono separate per pI (isoelettrofocalizzazione, 1ª dimensione) e PM (SDS-PAGE, 2ª dimensione). Gli spot vengono escissi → digestione in-gel con tripsina → MALDI-TOF PMF.

**Perché SDS-PAGE è un buon metodo di preparazione**

- Robusto, ampiamente disponibile, low-tech
- Rimuove molti contaminanti durante i passaggi di fissazione/colorazione
- Analitico e micropreparativo

**Limitazioni**

- La digestione in-gel non è quantitativa
- Il recupero di peptidi dal gel è incompleto
- Scarso recupero di proteine molto idrofobiche o di grandi dimensioni

**Esempio — adattamento di _E. coli_ a basso glucosio (Wick et al., _Environ Microbiol_ 2001)**: 2D-PAGE di _E. coli_ cresciuta in glucosio normale vs. molto basso → 15 spot proteici differenzialmente regolati identificati per PMF. Categorie funzionali: enzimi metabolici + proteine di trasporto → shift verso fonti energetiche alternative.

![[Pasted image 20260618153646.png]] ![[Pasted image 20260618153655.png]] ![[Pasted image 20260618153705.png]]

---

### Gel-Free Shotgun Proteomics

Sostituisce la separazione su gel con digestione in soluzione + frazionamento LC + MS/MS. Permette:

- Analisi di proteomi complessi (migliaia di proteine per esperimento)
- Quantificazione tramite SILAC, iTRAQ o metodi label-free
- Rilevazione di proteine a bassa abbondanza

---

### Altri Campi

- **Fosfoproteomics**: arricchimento di fosfopeptidi (TiO₂, IMAC) seguito da LC-MS/MS; localizzazione del sito di fosforilazione da MS/MS
- **Ubiquitinomics**: arricchimento di proteine/peptidi ubiquitinati
- **Proteomica clinica / Biomarker discovery**: proteomica di siero/plasma; comparazione pazienti vs. controlli sani
- **Proteome imaging**: MALDI su sezioni di tessuto → mappe spaziali di distribuzione di proteine/peptidi senza estrazione