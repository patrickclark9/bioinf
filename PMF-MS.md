
# Spettrometria di Massa

Tutti gli spettrometri di massa misurano le molecole in stati ionizzati. Tutti i valori determinati da MS sono relativi al rapporto m/z:


$$\frac{M}{Z} = \frac{M_r + (M_a \times Z)}{Z}$$

- $M_r$ = true molecular mass
- $M_a$ = mass of the ionizing adduct (typically H⁺ in positive mode; $M_a = 1.0072$ u)
- $Z$ = charge state

**Single vs. multiple charge states** can be observed, depending on compound, ionization mode, and instrument. Work is almost always done in **positive (+) ion mode** — peptides are protonated (MH⁺) under acidic conditions.


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

| Analyzer              | Resolution    | Key Feature                                               |
| --------------------- | ------------- | --------------------------------------------------------- |
| Quadrupole (Q)        | Low           | Transmit, scan, or select by m/z                          |
| 3D Ion Trap (IT)      | Low           | Trap → select → fragment → scan                           |
| Linear Ion Trap (LIT) | Low           | Higher capacity than 3D-IT                                |
| TOF (Time-of-Flight)  | Moderate–High | Separation by flight time; reflectron improves resolution |
| FT-ICR                | Very High     | Ion cyclotron resonance, Fourier transform detection      |
| Orbitrap (OT)         | Very High     | Orbital trapping; standard high-res platform              |
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

## Identificazione di Proteine per Fingeprinting Molecolare

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

Ogni spettro di frammentazione è un dataset indipendente (ortogonale) legato a una specifica sequenza. Data la probabilità $P_i$ che un match sia dovuto al caso per lo spettro $i$:`

$$P(\text{due match casuali alla stessa proteina}) = P_1^2$$

Esempio: $P_1 = 5 \times 10^{-3}$ → $P_2 = 2.5 \times 10^{-5}$ — due ordini di grandezza più stringente.

La probabilità che due spettri distinti matchino la stessa sequenza per caso è due ordini di grandezza inferiore rispetto a un singolo spettro. 
In generale, **si necessitano almeno 2 peptidi per proteina** per ottenere confidenza sufficiente. Ogni peptide è assegnato univocamente alla sua sequenza parent → molte proteine identificabili per run.

---

### Distinzione Critica

> **Identificazione proteica ≠ Caratterizzazione proteica**

- Due peptidi sono **sufficienti per identificare** una proteina
- Ma si stanno caratterizzando **solo quei due peptidi**
- Sequenze molto simili (isoforme, paraloghi) possono non essere distinguibili
- Per rilevare PTM è essenziale una **coverage di sequenza estesa**

## Gel Based Proteomics Workflow Base
2D Electrophoresis -> MALDI-TOF:
Separazione elettroforetica (non cromatografica) + MALDI/TOF -> Workflow tipico perchè MALDI non può essere accoppiato ad un HPLC come ESI.

![[Pasted image 20260618153646.png]]
![[Pasted image 20260618153655.png]]![[Pasted image 20260618153705.png]]
## Quantitative Proteomics (Shotgun approaches) - Isotope Labelling

Ovviamente vogliamo quantificare -> Espressione differenziale -> Chi cambia e quanto cambia

Perchè il labelling -> La spettrometria di massa non è inerentemente quantitativa -> segnali ionici dipendono dall'efficienza di ionizzazione, che varia per peptide e per run. Per comparare l'abbondanza tra cambione A e campione B:
1. Si va a etichettare ogni campione con reagenti identici chimicamente, ma sfruttando isotopi diversi
2. Si mescolano i campioni -> Si co-analizzano -> Le coppie isotopo leggero-pesante coeluiscono in LC e vengono distinte per massa
3. Le masse dei frammenti ionici ci permettono di identificare la sequenza peptidica -> protein identification
4. Si quantifica analizzando l'area del picco
Mescolare prima rimuove variabilità analitica downstream.

L'etichettatura può essere fatta post-sintesi proteica -> Specifiche modificazioni nella catena Amminoacidica. Applicabile ad ogni sample, ma possono avvenire reazioni
Metabolicamente -> durante la sintesi proteica, incorporazione di uno o più amminoacidi etichettati. Si utilizzano proteine native (no modifiche alle catene laterali), ma necessitano di un organismo di coltivazione

## ICAT - Isotopically Coded Affinity Tagging

Sfrutta marcatura Idrogeno-Deuterio (8 Da di separazione) o Carbonio-13 vs -12 (9 Da separazione) -> Deuterio interagisce con la fase stazionaria della colonna, motivo per cui si è passato al carbonio.

I reagenti sono:
- Biotin Tag -> Utilizzato per l'isolazione per affinità dei peptidi etichettati (mediante streptavidina)
- Linker chain (H o D, 8 Da di differenza)
- Reactive group -> Tipicamente Iodoacetamide.Lega residui Cys (tio-alchilazione)
![[Pasted image 20260618155459.png]]

Pro: Utilizzabile su qualsiasi tipo di campione, bassa complessità (solo i peptidi contenenti residui Cys sono analizzati), elmina variabilità analitica mescolando all'inizio

Con: Copre solo il 50-70% delle proteine (quelle con più di 1 Cys); possibili reazioni con altri residui, perdita durante purificazione con streptavidina

For the quantitative comparison of two proteomes, one sample is labeled with the isotopically light (d0) probe and the other with the isotopically heavy (d8) version. To minimize error, both samples are then combined, digested with a protease (i.e., trypsin, and subjected to avidin affinity chromatography to isolate peptides labeled with isotope-coded tagging reagents. These peptides are then analyzed by LC-MS. The ratios of signal intensities of differentially mass-tagged peptide pairs are quantified to determine the relative levels of proteins in the two samples.