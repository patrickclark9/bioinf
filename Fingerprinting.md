# Proteomica: Strategie di Analisi

---

## 1. Due Approcci Principali

| | **Top-Down** | **Bottom-Up** |
|---|---|---|
| **Oggetto di misura** | Proteine intere e loro frammenti | Peptidi derivati da digestione |
| **Applicazioni** | Struttura terziaria e quaternaria | Identificazione, quantificazione, PTM |
| **Limitazione chiave** | Le proteine grandi non eluiscono dalla colonna cromatografica | Si perde il contesto della proteina intera |
| **Diffusione** | Poco diffuso | Approccio dominante |

---

## 2. Due Scuole di Pensiero (Bottom-Up)

### 2.1 Approccio Elettroforetico (classico)
- Separazione mediante **PAGE** (mono- o bi-dimensionale)
- Processo **manuale**: l'operatore taglia ogni spot dal gel, lo lavora individualmente, poi lo analizza per MS/MS
- Laborioso e poco scalabile

### 2.2 Approccio Cromatografico (moderno)
- Separazione mediante **LC in fase liquida + ESI**
- Processo **automatizzato**: estratto proteico → digestione → HPLC → MS/MS
- Permette throughput molto superiore e analisi di miscele complesse

---

## 3. Workflow Bottom-Up

```
Campione proteico
      ↓
1. Separazione / Frazionamento proteico
      ↓
2. Proteolisi (es. tripsina → taglia dopo Lys/Arg)
      ↓
3. Separazione peptidica
      ↓
4. Ionizzazione  (MALDI · ESI · FAB · EI · CI)
      ↓
5. Analisi MS / MS/MS  (Ion trap · TOF · ...)
      ↓
6. Detezione  (MCP · Dynode-EM)
      ↓
7. Elaborazione dati
```

---

## 4. Il Problema del Frazionamento

### 4.1 Perché è Necessario

Due ragioni fondamentali:

1. **Range dinamico di espressione**: la proteina più abbondante può essere $10^{11}$ volte più abbondante della meno abbondante — strumentalmente impossibile da coprire in un'unica analisi.
2. **Velocità di acquisizione**: la raccolta degli spettri MS/MS non è abbastanza rapida da coprire tutti i peptidi in un campione complesso senza perdita.
3. **Similarità chimica**: i peptidi hanno proprietà fisico-chimiche simili, rendendo difficile la separazione cromatografica di miscele troppo complesse.

### 4.2 Esempio Quantitativo

Dato un campione relativamente semplice:

| Parametro | Valore |
|---|---|
| Numero di proteine | 5.000 |
| Frammenti peptidici attesi | ~40.000 |
| Peso molecolare medio | 30 kDa |
| Quantità minima per sequenziamento | 15 fmol / proteina |

**Caso ideale** (abbondanza uniforme):

$$15 \text{ fmol} \times 30 \text{ kDa} = 450 \text{ pg/proteina} \times 5000 = \mathbf{2.25\ \mu g\ \text{totali}}$$

**Caso reale** (range di abbondanza $10^6$):

Per ottenere 15 fmol della proteina *meno abbondante*, serve $10^5 \times$ più campione:

$$2.25\ \mu g \times 10^5 = \mathbf{225\ mg\ \text{di proteina totale}}$$

→ **Quando il campione è limitante, il frazionamento non è opzionale — è necessario per ridurre la complessità prima dell'analisi**.

---

## 5. Strategie di Frazionamento

### 5.1 Pre-digestione (Separazione della Proteina)

Si riduce la complessità a livello proteico, prima di digerire.
Separazione della proteina intatta mediante elettroforesi

| Metodo                       | Esempi                                     |
| ---------------------------- | ------------------------------------------ |
| Isolamento di organelli      | Mitocondri, nucleo, membrana plasmatica    |
| Frazionamento per solubilità | Frazione di membrana vs. frazione solubile |
| Separazione cromatografica   | Scambio cationico / anionico               |
| Separazione elettroforetica  | 1D-SDS-PAGE · 2D-PAGE (pI + MW)            |
| Affinity Chromatography      |                                            |
![[Pasted image 20260616201219.png]]
### 5.2 Post-digestione (Separazione del Peptide)

Si riduce la complessità a livello peptidico, dopo la digestione.

| Metodo | Note |
|---|---|
| **Cromatografia a fase inversa** (RP-HPLC) | Step finale prima dell'ingresso nello spettrometro |
| **Cromatografia multidimensionale** (MudPIT) | Es. SCX → RP; aumenta drasticamente la copertura del proteoma |
![[Pasted image 20260616201207.png]]


---

## 6. Quadro Riassuntivo

```
                     CAMPIONE PROTEOMICO
                           │
           ┌───────────────┴───────────────┐
     Pre-digestione                  Post-digestione
   (separa proteine)               (separa peptidi)
           │                               │
    organelli / gel             RP-HPLC / SCX-RP
           │                               │
           └───────────────┬───────────────┘
                     Proteolisi
                  (tripsina → peptidi)
                           │
                     Ionizzazione
                   (MALDI o ESI-LC)
                           │
                   MS / MS/MS
                           │
                   Identificazione
```



# Proteomica: Esperimenti e Tecniche di Separazione

---

## 1. Classi di Esperimenti di Proteomica

|Tipo|Complessità campione|Proteine analizzate|Dettaglio analitico|
|---|---|---|---|
|**Expression Analysis (PEA)**|Elevata|Quante più possibile|Basso — solo espressione|
|**Analisi di gruppi specifici**|Media|20–200 proteine preselezionate (stessa famiglia, stesso organello)|Intermedio|
|**Studio PTM**|Bassa|Poche proteine|Alto — composizione AA per ricercare modificazioni|

---

## 2. Tecniche di Separazione Proteica

### 2.1 SDS-PAGE

L'**SDS** (dodecil solfato di sodio) è un detergente fortemente ionico che:

- Denatura le proteine
- Conferisce una **carica elettrica negativa** mediamente ogni **2 residui amminoacidici**
- Rende la carica totale proporzionale al peso molecolare

|Peso molecolare|Cariche negative approssimative|
|---|---|
|40 kDa|~180|
|80 kDa|~360|

In campo elettrico di corrente continua le proteine (tutte negative) migrano verso il **catodo**, con velocità **inversamente proporzionale al peso molecolare**.

**Applicazioni principali:**

- Valutare la purezza di una proteina purificata
- Determinare il peso molecolare

---

### 2.2 Elettroforesi Bidimensionale (2D-PAGE)

Separa miscele proteiche complesse lungo **due dimensioni ortogonali**, sfruttando principi fisici indipendenti:

#### Prima dimensione — Isoelettrofocalizzazione (IEF)

- Gel di poliacrilammide con **gradiente di pH** generato da molecole anfotere
- Le proteine cariche migrano fino a raggiungere il proprio **punto isoelettrico (pI)** → si fermano (carica netta = 0)

#### Seconda dimensione — SDS-PAGE

- Il campione uscito dall'IEF viene trattato con **SDS**
- Separazione per **peso molecolare** (vedi §2.1)

#### PTM e pattern caratteristici

Le modificazioni post-traduzionali (PTM) possono alterare:

- Il **pI** → spostamento orizzontale dello spot
- Il **peso molecolare** → spostamento verticale dello spot

> **"Train" di spot**: quando una proteina è estensivamente modificata compaiono più spot alla stessa altezza (uguale massa) ma pI diverso — coesistenza di specie con diversi livelli di modificazione.

---

## 3. Gel-Based Proteomics

### 3.1 Applicazioni

|Categoria|Esempi|
|---|---|
|**Mappe di riferimento**|Frazioni organellari, frazione solubile|
|**Differenze qualitative**|Comparazione genotipica, comparazione di organelli diversi|
|**Differenze quantitative**|Risposta a farmaci, progressione di malattia, risposta a stimoli|

---

### 3.2 Workflow (campione singolo)

```
Tessuti
  └─► Elettroforesi 2D
        └─► Staining del gel
              └─► Image analysis & matching dei gel
                    └─► Comparazione degli spot
```

---

### 3.3 Quantificazione degli Spot

Il volume di uno spot si ricava dalla somma dei pixel interni ai suoi confini (image analysis).

**Normalizzazione:**

$$\text{Spot normalizzato} = \frac{\text{Volume spot}}{\text{Volume totale di tutti gli spot sul gel}}$$

Con **repliche biologiche** (controllo/trattato) si ottiene significatività statistica, e si procede con analisi statistica. L'elettroforesi è poco riproducibile però
![[Screenshot from 2026-06-17 08-55-16.png]]

---

### 3.4 Problemi: Variazioni Gel-to-Gel

Le variazioni tra gel compromettono la riproducibilità e l'accuratezza della quantificazione.

#### Prima dimensione (IEF)

|Fonte di variazione|
|---|
|Reidratazione non uniforme degli strip IEF|
|Perdita di proteina durante il trasferimento dal gel IEF|
|Quantità di campione recuperata dall'IEF diversa tra campioni|
|Streaking orizzontale di alcuni spot|

#### Seconda dimensione (SDS-PAGE)

|Fonte di variazione|
|---|
|Differenze/difetti nel settaggio del gel|
|Streaking verticale|

**Effetti:**

- Matching gel-to-gel problematico
- Inaccuratezza nella quantificazione

---

### 3.5 Strategie per Limitare le Variazioni

| Strategia           | Implicazione                                                    |
| ------------------- | --------------------------------------------------------------- |
| Repliche biologiche | ≥3 campioni biologici indipendenti                              |
| Repliche tecniche   | ≥3 gel per ciascun campione biologico                           |
| **Totale tipico**   | **3 biologiche × 3 tecniche × 2 (treated/untreated)  = 18 gel** |

> **Limite:** aumentare il numero di repliche incrementa costi in reagenti e tempo in modo significativo.


### 3.6 Strategia DiGE

La strategia DiGE consiste in un miglioramento della 2D-Electrophoresis, nella quale le proteine vengono marcate prima di essere analizzate. Con la tecniche DiGE è possibile caricare inoltre più di un campione alla volta, in quanto ad ogni campione viene legata una molecola che produce una fluorescenza differente (Multiplexing). Le proteine vengono marcate con molecole chiamate **Cianine** (Cya), che fungono da coloranti legando il gruppo amminico libero dei residui Lys -> L'ultimo gruppo, il primo (carbonio alpha) è impegnato in un legame peptidico.
Il multiplexing riduce il numero di gel da produrre. L'utilizzo di tinte fluorescenti incrementa la sensitività e ha un range dinamico grande (1-100.00).
Ci permette inoltre di creare uno standard interno rimuovendo la necessita per repliche tecniche, migliorando il gel-matching
![[Pasted image 20260617091745.png]]
![[Pasted image 20260617091835.png]]