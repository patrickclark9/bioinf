# Proteomica: Strategie di Analisi

---

## 1. Due Approcci Principali

| | **Top-Down** | **Bottom-Up** |
|---|---|---|
| **Oggetto di misura** | Proteine intere e loro frammenti | Peptidi derivati da digestione |
| **Applicazioni** | Struttura terziaria e quaternaria | Identificazione, quantificazione, PTM |
| **Limitazione chiave** | Proteine grandi non eluiscono dalla colonna | Si perde il contesto della proteina intera |
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

## 3. Workflow Bottom-Up - MS

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

1. **Range dinamico di espressione**: la proteina più abbondante può essere $10^{11}$ volte più abbondante della meno abbondante — strumentalmente impossibile da coprire in un'unica analisi.
2. **Velocità di acquisizione**: la raccolta degli spettri MS/MS non è abbastanza rapida da coprire tutti i peptidi di un campione complesso senza perdita.
3. **Similarità chimica**: i peptidi hanno proprietà fisico-chimiche simili, rendendo difficile la separazione cromatografica di miscele troppo complesse.

### 4.2 Esempio Quantitativo

| Parametro | Valore |
|---|---|
| Numero di proteine | 5.000 |
| Frammenti peptidici attesi | ~40.000 |
| Peso molecolare medio | 30 kDa |
| Quantità minima per sequenziamento | 15 fmol / proteina |

**Caso ideale** (abbondanza uniforme):

$$15\ \text{fmol} \times 30\ \text{kDa} = 450\ \text{pg/proteina} \times 5000 = \mathbf{2.25\ \mu g\ \text{totali}}$$

**Caso reale** (range di abbondanza $10^6$):

Per ottenere 15 fmol della proteina meno abbondante, serve $10^5\times$ più campione:

$$2.25\ \mu g \times 10^5 = \mathbf{225\ mg\ \text{di proteina totale}}$$

> Quando il campione è limitante, il frazionamento non è opzionale — è indispensabile per ridurre la complessità prima dell'analisi.

---

## 5. Strategie di Frazionamento

### 5.1 Pre-digestione (a livello di proteina)

Si riduce la complessità prima della digestione, lavorando sulla proteina intatta.

| Metodo | Note |
|---|---|
| **Isolamento di organelli** | Mitocondri, nucleo, membrana plasmatica |
| **Frazionamento per solubilità** | Frazione di membrana vs. frazione solubile |
| **Separazione cromatografica** | Scambio cationico / anionico |
| **Separazione elettroforetica** | 1D-SDS-PAGE · 2D-PAGE (pI + MW) |
| **Affinity chromatography** | Arricchimento per tag, leganti specifici o PTM |

![[Pasted image 20260616201219.png]]
### 5.2 Post-digestione (a livello di peptide)

Si riduce la complessità dopo la digestione triptica.

| Metodo | Note |
|---|---|
| **RP-HPLC** | Step finale prima dell'ingresso nello spettrometro |
| **MudPIT** (SCX → RP) | Due colonne ortogonali in serie; aumenta drasticamente la copertura del proteoma |
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

---

# Proteomica: Esperimenti e Tecniche di Separazione

---

## 1. Classi di Esperimenti di Proteomica

| Tipo | Complessità campione | Proteine analizzate | Dettaglio analitico |
|---|---|---|---|
| **Expression Analysis (PEA)** | Elevata | Quante più possibile | Basso — solo espressione |
| **Analisi di gruppi specifici** | Media | 20–200 proteine preselezionate (stessa famiglia, stesso organello) | Intermedio |
| **Studio PTM** | Bassa | Poche proteine | Alto — composizione AA per ricercare modificazioni |

---

## 2. Tecniche di Separazione Proteica

### 2.1 SDS-PAGE

L'**SDS** (dodecil solfato di sodio) è un detergente fortemente ionico che:
- Denatura le proteine
- Conferisce una **carica elettrica negativa** mediamente ogni **2 residui amminoacidici**
- Rende la carica totale proporzionale al peso molecolare

| Peso molecolare | Cariche negative approssimative |
|---|---|
| 40 kDa | ~180 |
| 80 kDa | ~360 |

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

![[Screenshot from 2026-06-17 08-55-16.png]]


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

![[Pasted image 20260617091745.png]]
![[Pasted image 20260617091835.png]]

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

![[Pasted image 20260617093909.png]]

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

| | Cromatografia tradizionale | Fase inversa (RP) |
|---|---|---|
| Fase stazionaria | Polare | **Idrofobica** |
| Fase mobile | Apolare | **Idrofilica → Idrofobica** (gradiente) |

I peptidi idrofobici si legano alla colonna; vengono eluiti scalando gradualmente la fase mobile verso composizioni più idrofobiche.

#### Gradiente di Eluizione

| Fase | Solvente dominante | Peptidi eluiti |
|---|---|---|
| Inizio | Alto % solvente A (acquoso) | Idrofilici (bassa affinità per la colonna) |
| Progressione | Aumento % solvente B (organico) | Idrofobici in ordine crescente |
| Fine | Alto % solvente B | Fortemente idrofobici |

> Quando l'idrofobicità della fase mobile eguaglia o supera la forza del legame peptide–colonna, il peptide si ripartisce nella fase mobile e viene eluito.

#### Qualità del Picco Cromatografico

| Tipo di picco | Causa | Conseguenza |
|---|---|---|
| **Picco ottimale** (stretto, simmetrico) | Tutte le molecole si staccano contemporaneamente | Segnale netto → area quantificabile |
| **Picco slargato** (con spalla) | Distacco lento o interazione anomala | Segnale non torna a zero → quantificazione impossibile |

---

### 4.4 Sistema a Due Colonne (MudPIT)

Un proteoma intero genera milioni di peptidi: troppi per una singola colonna (sovrapposizione dei picchi). Si usano **due colonne in serie con criteri ortogonali**:

```
Peptidi
  └─► Colonna 1: Scambio ionico
      (separazione per carica)
        └─► Colonna 2: RP-HPLC
            (separazione per idrofobicità)
              └─► Eluizione scaglionata nel tempo → spettrometro di massa
```

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

---

## 5. Analizzatore di Massa: TOF (Time-of-Flight)

### 5.1 Principio Generale

|Aspetto|Altri analizzatori|TOF|
|---|---|---|
|Tipo di separazione|Nel **tempo**|Nello **spazio** (distanza fissa)|
|Forza applicata durante il drift|Sì|No — gli ioni sono in deriva libera|
|Modalità di acquisizione|Scansione|Tutto simultaneamente (snapshot)|

Il TOF misura il **tempo impiegato da uno ione per percorrere una distanza fissa** (drift region). Ioni con massa diversa acquistano velocità diverse e arrivano al rivelatore in tempi diversi → separazione per m/z.

> **Accoppiamento naturale:** MALDI/TOF è stato a lungo lo standard della proteomica. MALDI ionizza anche macromolecole intatte, e TOF ha un range di massa teoricamente illimitato.

---

### 5.2 Fisica del TOF

#### Conservazione dell'energia

Nella zona sorgente tutti gli ioni vengono accelerati dallo **stesso potenziale U** (costante). L'energia potenziale acquisita si converte interamente in energia cinetica:

$$E_P = qU \qquad E_K = \frac{1}{2}mv^2$$

$$E_P = E_K \Longrightarrow qU = \frac{1}{2}mv^2$$

dove $q = ze$ , $U$ = voltaggio di accelerazione, $m$ = massa, $v$ = velocità nella drift region.
$q$ è la carica elettrica totale dello ione -> +1, +2, +3 ecc...
$e$ è la carica elementare (la carica di un singolo protone o elettrone, $1.602\times 10^{-19}Coulomb$)

La formula $E_P​=qU$ descrive l'**energia potenziale elettrica** che lo strumento fornisce allo ione.


> Poiché U è uguale per tutti, a parità di carica uno ione con massa minore raggiunge velocità maggiore → arriva prima al rivelatore.

#### Tempo di volo

Da $v = d/t$ e dall'equazione sopra si ricava:

$$\boxed{t = \frac{d}{\sqrt{2U}}\sqrt{\frac{m}{q}}}$$

Invertendo per ottenere la massa:

$$m = \frac{2qU}{d^2},t^2$$

Il tempo di volo è dunque una misura diretta di $\sqrt{m/q}$ — da $t$ misurato si risale a $m/z$.

---

### 5.3 Resolving Power

Differenziando $m = \frac{2qU}{d^2}t^2$:

$$dm = \frac{2qU}{d^2}\cdot 2tdt$$

Dividendo membro a membro:

$$\frac{m}{dm} = \frac{t}{2dt} ;\Longrightarrow; \boxed{R = \frac{m}{\Delta m} = \frac{t}{2\Delta t}}$$

**Interpretazione:** la risoluzione di massa dipende direttamente dalla precisione temporale $\Delta t$. Per separare due masse simili occorre che il fascio ionico di ciascuna massa arrivi al rivelatore entro un intervallo di tempo $\Delta t$ il più stretto possibile → **focalizzazione del fascio ionico**.
![[Pasted image 20260617151250.png]]

---

### 5.4 Problemi: De-focalizzazione del Fascio Ionico

In pratica, ioni con la **stessa** m/z non arrivano tutti nello stesso istante, causando allargamento della banda ionica e perdita di risoluzione. Le cause sono tre:

| Effetto                    | Causa                                                                                                                                           | Conseguenza                                       |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| **Position spread**        | Ioni formati in posizioni diverse nella sorgente → diversa distanza percorsa nella zona di accelerazione                                        | Diversa energia cinetica acquisita                |
| **Direction spread**       | Ioni emessi con direzioni diverse → componente assiale della velocità variabile. Raggiungono l'uscita ma impiegano più tempo (turn-around time) | Tempi di transito diversi anche a parità di massa |
| **Energy/Velocity spread** | Energia cinetica iniziale (pre-accelerazione) variabile                                                                                         | Velocità di partenza non uniformi                 |

Tutti e tre i fenomeni **ampliano la distribuzione temporale** degli ioni a massa uguale → $\Delta t$ aumenta → $R$ diminuisce.
$\Delta t$ è dato quindi dalla somma del tempo trascorso nella regione **source** (formazione dello ione, position spread, velocity spread, direction spread) e il tempo trascorso nel **drifting tube** (position spread, velocity spread), oltre al response time del detector (dovrebbe essere circa costante).

---

### 5.5 Soluzioni Tecniche per la Focalizzazione

#### 1. Dual Stage Extraction - Position Spread

Anche detta focalizzazione spaziale di Wiley-McLaren. Si applica l'accelerazione in **due stadi** invece di uno:

- **Stadio 1:** campo più debole vicino alla sorgente → corregge le differenze di posizione e di energia cinetica iniziale
- **Stadio 2:** campo più intenso → accelerazione finale uniforme

La correzione del primo stadio è dipendente dalla massa, compensando esattamente il position spread per ciascuna specie.
Avendo due stadi di accelerazione indipendenti, è possibile "modulare" le tensioni in modo che gli ioni partiti da posizioni leggermente diverse (e che quindi subiscono potenziale diverso) convergano temporalmente _esattamente_ nel punto in cui si trova il rivelatore.

#### 2. Time-Delayed Extraction (DE) - Velocity Spread

Si introduce un **ritardo** ($\sim$ nanosecondi (MALDI)–microsecondi (ESI)) tra l'ionizzazione e l'applicazione del campo di accelerazione:

- Durante il ritardo, gli ioni con velocità iniziale maggiore si allontanano di più dalla sorgente -> parziale diffusione di energia cinetica
- Quando il campo viene applicato, gli ioni più veloci (più lontani) si trovano in una regione a potenziale inferiore → ricevono meno energia → arrivano al rivelatore insieme agli ioni più lenti
- Risultato: **compressione temporale** della distribuzione → riduzione del position e del velocity spread tra ioni con lo stesso m/z che lasciando la sorgente

#### 3. Reflectron - Compensazione ulteriore per velocity spread

Specchio elettrostatico posto in fondo alla drift region, formato da **elettrodi a potenziale crescente** con segno opposto al campo di accelerazione.

```
Sorgente ──────────────► Reflectron ──────────────► Rivelatore
         drift region 1              drift region 2
```

Il voltaggio viene impostato a 1.05-1.1 moltiplicato per il voltaggio di accelerazione. Gli ioni entrano nel reflectron, penetrano fino al raggiungimento di 0 energia cinetica, e poi vengono accelerati nella direzione del detector

**Meccanismo di correzione:**

| Ione                        | Velocità | Penetrazione nel reflectron | Percorso extra | Effetto                       |
| --------------------------- | -------- | --------------------------- | -------------- | ----------------------------- |
| Più veloce (più energetico) | Alta     | Maggiore                    | Più lungo      | Rallentamento più aggressivo  |
| Più lento (meno energetico) | Bassa    | Minore                      | Più corto      | Rallentamento meno aggressivo |

I due ioni, pur entrando in tempi diversi, escono dal reflectron e arrivano al rivelatore **contemporaneamente** → focalizzazione indipendente dalla posizione di partenza.

> Il voltaggio del reflectron è **superiore** al potenziale di accelerazione iniziale e di **segno opposto**: tutti gli ioni vengono decelerati, invertiti ed espulsi, ma con percorsi diversi in funzione della loro energia.

Il campo ritardante/riflettente permette una compensazione **Indipendente dalla massa** per la velocity spread.

**Tanto più corto il path dello ione, tanto più accurata deve essere la misurazione del time of flight**.

#### Configurazione Ottimale: Dual Stage Reflectron

La combinazione di **dual stage extraction + time-delayed extraction + reflectron** massimizza la focalizzazione del fascio ionico su tutte e tre le cause di spreading, consentendo la massima risoluzione raggiungibile in un TOF.
È lo standard per ottenere massima risoluzione e accuratezza per un analizzatore TOF.

---

### 5.6 Riepilogo: Problema → Causa → Soluzione

| Problema                                  | Causa fisica                                 | Soluzione                             |
| ----------------------------------------- | -------------------------------------------- | ------------------------------------- |
| Position spread                           | Ioni formati in punti diversi della sorgente | Dual stage extraction + TDE           |
| Direction spread                          | Emissione in direzioni diverse               | TDE (compressione temporale parziale) |
| Energy spread                             | Diversa $E_K$ iniziale                       | TDE + Reflectron                      |
| Spreading residuo (indipendente da massa) | Imperfezioni del campo                       | Reflectron                            |
