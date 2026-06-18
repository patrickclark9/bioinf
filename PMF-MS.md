
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