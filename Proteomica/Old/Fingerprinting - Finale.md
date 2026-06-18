# Proteomica: Esperimenti e Tecniche di Separazione






## 0. Due Approcci Principali

|                        | **Top-Down**                                                  | **Bottom-Up**                              |
| ---------------------- | ------------------------------------------------------------- | ------------------------------------------ |
| **Oggetto di misura**  | Proteine intere e loro frammenti                              | Peptidi derivati da digestione             |
| **Applicazioni**       | Struttura terziaria e quaternaria                             | Identificazione, quantificazione, PTM      |
| **Limitazione chiave** | Le proteine grandi non eluiscono dalla colonna cromatografica | Si perde il contesto della proteina intera |
| **Diffusione**         | Poco diffuso                                                  | Approccio dominante                        |

---

## 1. Due Scuole di Pensiero (Bottom-Up)

### 1.1 Approccio Elettroforetico (classico)
- Separazione mediante **PAGE** (mono- o bi-dimensionale)
- Processo **manuale**: l'operatore taglia ogni spot dal gel, lo lavora individualmente, poi lo analizza per MS/MS
- Laborioso e poco scalabile

### 1.2 Approccio Cromatografico (moderno)
- Separazione mediante **LC in fase liquida + ESI**
- Processo **automatizzato**: estratto proteico → digestione → HPLC → MS/MS
- Permette throughput molto superiore e analisi di miscele complesse
---

## 2. Classi di Esperimenti di Proteomica

| Tipo                            | Complessità campione | Proteine analizzate                                                | Dettaglio analitico                                |
| ------------------------------- | -------------------- | ------------------------------------------------------------------ | -------------------------------------------------- |
| **Expression Analysis (PEA)**   | Elevata              | Quante più possibile                                               | Basso — solo espressione                           |
| **Analisi di gruppi specifici** | Media                | 20–200 proteine preselezionate (stessa famiglia, stesso organello) | Intermedio                                         |
| **Studio PTM**                  | Bassa                | Poche proteine                                                     | Alto — composizione AA per ricercare modificazioni |

---

## 3. Tecniche di Separazione Proteica

### 2.1 SDS-PAGE

L'**SDS** (dodecil solfato di sodio) è un detergente fortemente ionico che:
- Denatura le proteine
- Conferisce una **carica elettrica negativa** mediamente ogni **2 residui amminoacidici**
- Rende la carica totale proporzionale al peso molecolare

| Peso molecolare | Cariche negative approssimative |
| --------------- | ------------------------------- |
| 40 kDa          | ~180                            |
| 80 kDa          | ~360                            |

In campo elettrico di corrente continua le proteine (tutte negative) migrano verso il **catodo**, con velocità **inversamente proporzionale al peso molecolare**.

**Applicazioni principali:**
- Valutare la purezza di una proteina purificata
- Determinare il peso molecolare

---

### 2.2 Elettroforesi Bidimensionale (2D-PAGE)

Separa miscele proteiche complesse lungo **due dimensioni ortogonali**, sfruttando principi fisici indipendenti:

#### Prima dimensione — Isoelettrofocalizzazione (IEF)

- Gel di poliacrilammide con **gradiente di pH** generato da molecole anfotere
- Le proteine cariche migrano fino a raggiungere il proprio **punto isoelettrico (pI)** → si fermano (carica netta = 0) -> Separazione per punto isolettrico

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

| Categoria | Esempi |
|---|---|
| **Mappe di riferimento** | Frazioni organellari, frazione solubile |
| **Differenze qualitative** | Comparazione genotipica, comparazione di organelli diversi |
| **Differenze quantitative** | Risposta a farmaci, progressione di malattia, risposta a stimoli |

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

Con **repliche biologiche** (controllo/trattato) si procede con analisi statistica.

---

### 3.4 Problemi: Variazioni Gel-to-Gel

Le variazioni tra gel compromettono la riproducibilità e l'accuratezza della quantificazione.

#### Prima dimensione (IEF)

| Fonte di variazione |
|---|
| Reidratazione non uniforme degli strip IEF |
| Perdita di proteina durante il trasferimento dal gel IEF |
| Quantità di campione recuperata dall'IEF diversa tra campioni |
| Streaking orizzontale di alcuni spot |

#### Seconda dimensione (SDS-PAGE)

| Fonte di variazione |
|---|
| Differenze/difetti nel settaggio del gel |
| Streaking verticale |

**Effetti:**
- Matching gel-to-gel problematico
- Inaccuratezza nella quantificazione

---

### 3.5 Strategie per Limitare le Variazioni

| Strategia | Implicazione |
|---|---|
| Repliche biologiche | ≥3 campioni biologici indipendenti |
| Repliche tecniche | ≥3 gel per ciascun campione biologico |
| **Totale tipico** | **3 biologiche × 3 tecniche = 18 gel** |

> **Limite:** aumentare il numero di repliche incrementa costi in reagenti e tempo in modo significativo.

---

### 3.6 Strategia DiGE (Difference Gel Electrophoresis)

La DiGE è un'evoluzione della 2D-PAGE che risolve il problema della variabilità gel-to-gel tramite **marcatura fluorescente pre-elettroforetica** e **multiplexing** (più campioni sullo stesso gel).

#### Principio del labelling

Le proteine vengono marcate con **cianine (Cy)**, coloranti fluorescenti che si legano al **gruppo amminico libero dei residui Lys** (il gruppo α-amminico è impegnato nel legame peptidico). Ogni campione riceve un colorante con frequenza di eccitazione distinta:

| Colorante | Uso tipico |
|---|---|
| **Cy3** | Campione Controllo |
| **Cy5** | Campione Trattato |
| **Cy2** | Standard interno (mix dei due) |

I campioni marcati vengono **miscelati e caricati sullo stesso gel**: correndo insieme, gli spot non subiscono distorsioni relative — il confronto avviene tra immagini dello stesso gel, non tra gel diversi.

#### Standard interno e quantificazione

Lo standard interno (Cy2) è un pool equimolare di tutti i campioni dell'esperimento. L'abbondanza di ogni spot è espressa come rapporto rispetto allo standard:

$$\text{Abbondanza relativa} = \frac{\text{Spot}_{\text{Controllo o Trattato}}}{\text{Spot}_{\text{Standard (Cy2)}}}$$

Fissando l'abbondanza dello standard a 1, le espressioni nelle singole condizioni sono direttamente comparabili tra gel diversi.

#### Vantaggi rispetto alla 2D-PAGE classica

| Aspetto | 2D-PAGE classica | DiGE |
|---|---|---|
| Campioni per gel | 1 | 2–3 (multiplexing) |
| Confronto tra campioni | Gel-to-gel | Intra-gel |
| Variabilità tecnica | Alta | Minimizzata |
| Standard interno | ✗ | ✓ (Cy2) |
| Repliche tecniche necessarie | Sì (≥3) | Non necessarie |
| Sensibilità / range dinamico | Limitata | 1:100.000 |

> La DiGE riduce il numero totale di gel da produrre e rimuove la necessità di repliche tecniche, migliorando sia il gel-matching sia l'accuratezza della quantificazione.

---

### 3.7 Image Analysis in DiGE

Il workflow di analisi dell'immagine in DiGE si svolge in quattro fasi sequenziali:

```
1. Gel Imaging
   └─► 1 gel → 3 immagini separate (Cy2 / Cy3 / Cy5)

2. Spot Detection
   └─► Co-detection degli spot nelle 3 immagini
       Gli algoritmi sfruttano i pixel di tutte e 3 le immagini in parallelo

3. Gel Matching
   └─► Allineamento basato sullo standard interno (Cy2)
       → Nessun confronto gel-to-gel necessario

4. Spot Quantification
   └─► Ogni spot quantificato in rapporto allo standard interno
       → Valori comparabili tra gel diversi
```

---

## 4. Gel-Free Proteomics

### 4.1 Motivazione: Limiti dell'Approccio Gel-Based

| Limite | Dettaglio |
|---|---|
| Variabilità biologica | Dipende dalla natura del campione |
| Variabilità tecnica | Legata all'esecuzione della 2D-PAGE |
| Scala | Difficile gestire proteomi di grande complessità |
| Macromolecole | La cromatografia moderna fatica con proteine intatte |

Gli approcci **Gel-Free** combinano labelling isotopico, tecniche cromatografiche e spettrometria di massa per l'identificazione e quantificazione su larga scala.

---

### 4.2 Approccio Bottom-Up: Digestione Triptica

La 2D-PAGE analizza **proteine intatte**. Nell'approccio Bottom-Up, invece, le proteine vengono **digerite enzimaticamente** prima della separazione.

```
Proteoma complesso
  └─► Digestione con Tripsina
        └─► Miscela di peptidi
              (PM ridotto, polarità variabile → separabili cromatograficamente)
```

La **tripsina** taglia specificamente dopo i residui **Lys** e **Arg**, producendo peptidi di lunghezza prevedibile — fondamentale per la successiva identificazione in spettrometria di massa.

---

### 4.3 Separazione Cromatografica — RP-HPLC

#### Principio della Fase Inversa

La cromatografia a **fase inversa (RP)** inverte la logica tradizionale:

|                  | Cromatografia tradizionale | Fase inversa (RP)                       |
| ---------------- | -------------------------- | --------------------------------------- |
| Fase stazionaria | Polare (Idrofilica)        | **Idrofobica**                          |
| Fase mobile      | Apolare (idrofobica)       | **Idrofilica → Idrofobica** (gradiente) |

I peptidi idrofobici si legano alla colonna; vengono eluiti (fatti uscire) scalando gradualmente la fase mobile verso composizioni più idrofobiche.

#### Gradiente di Eluizione

| Fase         | Solvente dominante              | Peptidi eluiti                             |
| ------------ | ------------------------------- | ------------------------------------------ |
| Inizio       | Alto % solvente A (acquoso)     | Idrofilici (bassa affinità per la colonna) |
| Progressione | Aumento % solvente B (organico) | Idrofobici in ordine crescente             |
| Fine         | Alto % solvente B               | Fortemente idrofobici                      |

> Quando l'idrofobicità della fase mobile eguaglia o supera la forza del legame peptide–colonna, il peptide si ripartisce nella fase mobile e viene eluito.

#### Qualità del Picco Cromatografico

| Tipo di picco | Causa | Conseguenza |
|---|---|---|
| **Picco ottimale** (stretto, simmetrico) | Tutte le molecole si staccano contemporaneamente | Segnale netto → area quantificabile |
| **Picco slargato** (con spalla) | Distacco lento o interazione anomala | Segnale non torna a zero → quantificazione impossibile |

---

### 4.4 Sistema a Due Colonne (MudPIT)

Un proteoma intero genera milioni di peptidi: troppi per una singola colonna (sovrapposizione dei picchi). Si usano **due colonne in serie con criteri ortogonali**:
- La prima separa i peptidi per scambio ionico -> In base alla loro carica
- I peptidi in uscita dalla prima colonna passano in una seconda, che li separa in base alla idrofobicità

Questo distribuisce i peptidi su un arco temporale più lungo, evitando il sovraffollamento del sistema.


---

### 4.5 Ionizzazione ESI e Accoppiamento con HPLC

L'**ESI (Electrospray Ionization)** vaporizza e ionizza un flusso di liquido in tempo reale → accoppiamento naturale con HPLC a flusso continuo.

L'ESI richiede un **donatore di protoni** per caricare i peptidi (es. acido formico), ma impone vincoli severi sui solventi e sui sali utilizzabili.

#### Incompatibilità con Sali Non Volatili

| Reagente | Problema in ESI |
|---|---|
| Fosfati (comuni in HPLC tradizionale) | Non evaporano → precipitano come crosta sulla sorgente |
| Acidi/basi forti | Non volatili → contaminano e danneggiano lo strumento |
| Concentrazioni elevate di ioni forti | **Effetto matrice**: i sali competono con i peptidi per la carica → soppressione della ionizzazione → segnale assente |

> In ESI si usano **esclusivamente acidi/sali volatili e deboli** (es. acido formico, acetato d'ammonio a bassa concentrazione).

#### Desalting

Prima di iniettare campioni complessi, è indispensabile un passaggio di **desalting** (rimozione dei sali):

- Tecnica tipica: resine **C18 miniaturizzate** in puntali da pipetta (es. **ZipTip**)
- Particolarmente critico per l'ESI, più intollerante ai sali rispetto al MALDI

---

### 4.6 Riepilogo: Gel-Based vs Gel-Free

| Caratteristica | Gel-Based (2D-PAGE / DiGE) | Gel-Free (Bottom-Up LC-MS) |
|---|---|---|
| Forma analizzata | Proteina intera | Peptidi (dopo digestione triptica) |
| Separazione | IEF + SDS-PAGE | RP-HPLC (± scambio ionico) |
| Rilevazione | Densitometria / fluorimetria | Spettrometria di massa |
| Scala | Centinaia di proteine | Migliaia di proteine |
| PTM | Visibili come shift di spot | Identificabili dal frammento peptidico |
| Variabilità tecnica | Alta (gel-to-gel) | Ridotta |
| Informazione quantitativa | Diretta (volume spot) | Richiede labelling o label-free |
