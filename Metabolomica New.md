# Metabolomica

> Il metaboloma è l'indicatore ultimo dello stato funzionale di un sistema biologico.

---

## Definizione e Rilevanza

La **metabolomica** studia e analizza l'insieme di tutti i metaboliti presenti in un sistema biologico in un dato momento.

### Perché il Metaboloma?

Il metaboloma colma il divario tra **genotipo e fenotipo**:

- Non esiste una relazione lineare tra mRNA e proteina
- Una proteina può essere presente ma inattivata da modificazioni post-traduzionali (PTM)
- La quantificazione dei metaboliti fornisce il **readout funzionale diretto** del sistema: ci dice cosa sta succedendo a livello fisiologico

I metaboliti sono quindi indicatori dello stato cellulare: le loro disregolazioni si manifestano **più rapidamente** rispetto a variazioni a livello proteico o genico. Questo li rende candidati promettenti come **biomarcatori precoci** di stati patologici.

### Metabolismo ed Epigenetica

Il metabolismo è centrale nella **regolazione epigenetica**: il fenotipo è fortemente influenzato dall'ambiente esterno, e il metabolismo è il meccanismo con cui il sistema risponde ai segnali ambientali.

> **Esempio:** La _S-adenosilmetionina_ (SAM) è uno dei principali donatori di metile per la metilazione del DNA.

---

## Il Problema: Scala ed Eterogeneità

Il numero di metaboliti in un organismo **eccede di gran lunga** quello delle proteine e dei geni:

|Proprietà|Valore|
|---|---|
|Metaboliti totali stimati|>200.000|
|Classi chimiche distinte|~3.000|

I metaboliti si distinguono per origine:

- **Endogeni** → prodotti ciclicamente da anabolismo e catabolismo
- **Esogeni** → derivanti da dieta, farmaci o ambiente

**Conseguenze pratiche:**

- Non esiste un'unica tecnica in grado di coprire l'intero metaboloma in un solo esperimento
- La concentrazione **non è correlata** all'importanza funzionale: metaboliti poco abbondanti possono avere ruoli chiave
- Sono necessari sistemi ad **alta risoluzione**, **alto range dinamico** e **alto throughput**

### Separazione in Comparti

Dato che un singolo sistema cromatografico non è sufficiente, il metaboloma viene analizzato separatamente:

- **Metaboloma idrofilico** → estratto e analizzato con metodi per molecole polari
- **Lipidomica** → comparto lipidico analizzato separatamente (→ vedi sezione [[#Lipidomica]])

---

## Requisiti Strumentali

La MS in metabolomica deve soddisfare requisiti spesso contrastanti:

|Requisito|Motivazione|
|---|---|
|**Alta risoluzione**|Molecole diverse possono avere valori di m/z identici o molto simili|
|**Alta accuratezza di massa**|Necessaria per distinguere isobare|
|**Ampio range dinamico**|Le concentrazioni dei metaboliti variano di ordini di grandezza|
|**Alta sensibilità**|Rilevare anche i metaboliti meno abbondanti|
|**Alto throughput**|Analisi di grandi coorti di campioni (N elevato), con automazione e velocità|

> Alta risoluzione e alta sensibilità contemporaneamente non sono semplici da ottenere nello stesso sistema.

### Ionizzazione

In metabolomica si applicano classicamente **sorgenti di ionizzazione hard**: la frammentazione indotta è specifica e riproducibile, cruciale per l'identificazione di piccoli metaboliti.

---

## Approcci Sperimentali

### Per Scala Spaziale

|Approccio|Descrizione|
|---|---|
|**Bulk**|Tradizionale; analizza il metaboloma aggregato dell'intero campione|
|**Spaziale / Single-cell**|Innovativi; permettono di analizzare il metaboloma con risoluzione spaziale o a livello della singola cellula|

### Per Dimensione Temporale

|Approccio|Descrizione|
|---|---|
|**Statico**|Analisi di uno stato metabolico preciso (snapshot)|
|**Dinamico (Flussonomica)**|Utilizza precursori marcati con **isotopi stabili** per tracciare percorso e velocità del flusso attraverso le vie metaboliche|

---

## Tecnologie

### NMR

Prevalente in passato. Principale limitazione: **bassa sensibilità**, che richiedeva grandi quantità di campione.

### Spettrometria di Massa (MS)

Ha soppiantato l'NMR come tecnica dominante. I progressi in:

- **velocità di scansione**
- **risoluzione di massa**

hanno permesso l'identificazione di metaboliti a concentrazioni molto più basse, spingendo lo sviluppo dell'intera disciplina.

---

## Lipidomica

La lipidomica è una disciplina a sé stante all'interno della metabolomica. Le caratteristiche chimiche dei lipidi (principalmente l'**apolarità**) richiedono:

- Sistemi HPLC dedicati (fasi inverse, colonne C18/C8)
- Metodi di estrazione specifici
Tipicamente LC ottimizzati sono i più utilizzati.
I lipidi hanno range di massa enorme (150Da-1500Da) e strutture molto variabili (lunghezza delle catene, insaturazioni, teste polari).
Isomeri posizionali (es. posizione del doppio legame) vengono risolti mediante tecniche di frammentazione MS/MS specifiche (MRM, Neutral Loss Scan) per la lipidomica.
Le librerie standard specifiche per i lipidi sono molte estese, aiutano nell'identificazione significativamente.
Per sua natura la lipidomica è una delle aree più complesse della metabolomica.

La metabolomica "generale" ha beneficiato maggiormente dalle tecniche MS applicate a molecole più **polari e reattive**, mentre i lipidi sono analizzati in pipeline separate.


# Bulk Metabolomics

Analisi dell'intero tessuto o campione biologico. Non risolve eterogeneità spaziale o cellulare, ma permette una visione aggregata del metaboloma.

---

## Tipologie di Analisi

### Untargeted (Screening)

Analisi non selettiva: l'analizzatore (tipicamente MS) scansiona un intero range di m/z d'interesse senza preselezionare alcun valore.

- Produce un **profilo metabolico globale**
- Prevalentemente **qualitativa o semi-quantitativa**
- L'identificazione dei metaboliti avviene **a posteriori** (es. via MS/MS), per confronto con standard noti o librerie spettrali

### Targeted

Analisi selettiva: quantifica un insieme **specifico e conosciuto** di metaboliti, spesso coinvolti in un pathway d'interesse.

Richiede per ogni metabolita target:

|Elemento|Scopo|
|---|---|
|**Standard puro**|Caratterizzazione spettrale (TR, m/z parent e daughter)|
|**Curva di calibrazione**|Diluizioni seriali dello standard; relazione lineare tra concentrazione e area del picco|

Si lavora in **selettività**: vengono acquisiti solo gli m/z noti dallo standard. L'area del picco nel campione, interpolata sulla curva, fornisce la concentrazione assoluta del metabolita.

---

## Variabilità

In metabolomica occorre distinguere due fonti di variabilità:

|Tipo|Origine|
|---|---|
|**Analitica**|Errore strumentale o di protocollo|
|**Biologica**|Differenze naturali tra campioni; più accentuata che in proteomica, perché i metaboliti sono a valle del flusso informazionale e mostrano maggiore dispersione nelle concentrazioni|

> È indispensabile un **N statisticamente adeguato** per garantire la potenza statistica dell'analisi.

---

## Workflow

```
Campione biologico
       │
       ▼
   Quenching  ──────────────────────────────────────────────────────┐
  (blocco attività enzimatica)                                       │
       │                                                             │
       ▼                                                             │
Rimozione proteine                                        Metodi di quenching:
  (centrifugazione)                                        - Congelamento ultrarapido (N₂ liquido)
       │                                                     → polverizzazione meccanica
       ▼                                                   - Solventi organici freddi (es. MeOH)
Estrazione selettiva                                         → denaturazione proteica + lisi
  (frazionamento per polarità)                             - Acidi / buffer specifici
       │                                                     (es. acido perclorico)
       ▼
Separazione cromatografica (LC o GC)
       │
       ▼
Analisi MS
       │
       ▼
Analisi dei dati
```

### Estrazione

L'estrazione è **selettiva per polarità**: molecole idrofiliche e lipofiliche vengono estratte separatamente.

- **Estrazione sequenziale**: prima i metaboliti polari, poi quelli apolari (es. cloroformio per il comparto lipofilico)
- Esistono metodi onnicomprensivi, ma tendono a favorire le molecole polari

### Campioni: Intracellulare vs Extracellulare

|Origine|Procedura|
|---|---|
|**Intracellulare**|Separare biomassa dal sovranatante per centrifugazione → MeOH/H₂O freddi per estrarre metaboliti e indurre quenching → centrifugazione per rimozione proteine|
|**Extracellulare** (sovranatante)|Separare le cellule per centrifugazione → aggiungere MeOH freddo per precipitare le proteine → centrifugazione per rimozione|
|**Campioni solidi / ambientali**|Disomogeneizzazione (N₂ liquido + meccanica) in presenza di solventi freddi → raccolta del lisato post-centrifugazione|

---

## Separazione Cromatografica

Passaggio **obbligatorio** nel workflow metabolomico. Ha due funzioni principali:

1. **Risoluzione** → separa metaboliti con lo stesso PM (isobari) grazie al diverso tempo di ritenzione in colonna
2. **Diluizione temporale** → distribuisce nel tempo l'ingresso dei metaboliti nella sorgente di ionizzazione MS; un flusso simultaneo dell'intero metaboloma renderebbe impossibile l'acquisizione MS/MS

> Per la **quantificazione assoluta** è indispensabile una curva di calibrazione per ciascun metabolita: concentrazione nota dello standard vs. area del picco cromatografico, da cui si interpolano i dati campione.

---

## GC-MS

### Principio

La GC separa composti **volatili**: il campione liquido viene iniettato a temperature elevate e volatilizzato immediatamente. La separazione è modulata da un **gradiente di temperatura** (non dalla composizione della fase mobile, come in LC): all'aumentare della temperatura, i composti eluiscono progressivamente.

Sorgente di ionizzazione standard: **impatto elettronico (EI)**.

### Derivatizzazione

La maggior parte dei metaboliti biologici **non è volatile** ed è **termolabile**. Si ricorre alla **derivatizzazione**:

1. **Essiccazione** del campione (rimozione dell'acqua)
2. **Aggiunta di silani** → gruppi **TMS** (trimetilsilil) reagiscono con gruppi nucleofili (ammine, ossidrili, carbossilici), aumentando volatilità e stabilità termica
3. Per **gruppi carbonilici** (C=O, non nucleofili): uso di **metossiamina** per stabilizzarli prima della sililazione

**Conseguenze e soluzione:**

|Effetto|Dettaglio|
|---|---|
|Modifica del PM|Ogni gruppo TMS aggiunto incrementa l'm/z|
|Pattern di frammentazione alterato|L'EI produce ioni frammento già nella sorgente, con pattern dipendenti dalla derivatizzazione|
|**Soluzione: librerie dedicate**|Le librerie GC-MS contengono spettri di metaboliti **già derivatizzati** → identificazione affidabile anche **senza standard in loco**, con m/z attesi (ione molecolare + frammenti) già noti|

---

## LC-MS

Standard: **ESI-LC-MS**. Il grande sviluppo della LC in metabolomica è stato guidato dall'innovazione nei materiali delle colonne (particelle sub-2 µm in UPLC/UHPLC), che hanno migliorato efficienza di separazione e risoluzione analitica.

### Reversed-Phase (RP-LC)

- **Fase stazionaria**: apolare/idrofobica (catene C-18 o C-8)
- **Fase mobile**: inizia acquosa/polare → progredisce verso organica/apolare (es. acetonitrile + 0,1% acido formico)
- I composti **meno polari** eluiscono **dopo** (interagiscono più fortemente con la fase stazionaria apolare)

**Limite**: i metaboliti molto polari vengono scarsamente trattenuti e co-eluiscono, con perdita di risoluzione → si ricorre a HILIC.

### HILIC (Hydrophilic Interaction Chromatography)

- **Fase stazionaria**: polare
- **Fase mobile**: inizia apolare → progredisce verso più acquosa (aumento progressivo della componente acquosa)
- I composti **più polari** vengono trattenuti più a lungo → maggiore risoluzione e separazione temporale dei metaboliti polari

HILIC è complementare alla RP: insieme coprono un range di polarità molto più ampio.

---

## MS vs NMR: Confronto

La risonanza magnetica atomica valuta un assorbimento di energia da parte dei nuclei atomici, che viene rilasciata.

|Proprietà|MS|NMR|
|---|---|---|
|**Sensibilità**|Alta|Bassa (richiede campioni abbondanti)|
|**Preparazione campione**|Complessa (estrazione, separazione)|Semplice (solo solubilizzazione)|
|**Distruttività**|Sì|No|
|**Riproducibilità**|Buona|Molto alta|
|**Distinzione isomeri**|Difficile senza cromatografia|Buona|
|**Tracing isotopico**|Possibile|Eccellente (molto sensibile agli isotopi pesanti)|
|**Campo magnetico richiesto**|No|Sì (intenso)|

> La bassa sensibilità NMR deriva dalla piccola separazione energetica tra i livelli di spin nucleare, che aumenta solo con l'intensità del campo magnetico applicato.

In genere si **combinano più tecniche** per ottenere alta sensibilità, identificazione e dati strutturali completi.

**Analizzatori MS comuni in metabolomica:**

|Tipo|Caratteristiche|
|---|---|
|Ion-Trap, Q, QqQ, Q-TOF|Bassa/media risoluzione; comuni per quantificazione|
|Orbitrap, FT-ICR-MS|Altissima risoluzione e accuratezza di massa; permettono di distinguere molecole con masse molto vicine|

Spesso GC-MS e LC-MS vengono usati in combinazione, in funzione della classe di metabolita.

---

## Analisi: Dal Cromatogramma all'Identificazione

L'output iniziale è il **cromatogramma**: visualizza i picchi dei metaboliti nel tempo (separazione cromatografica).

### MS singolo → Dati 2D

Per ogni picco cromatografico:

- **Tempo di ritenzione (tR)** → istante di eluizione del metabolita
- **m/z** → aprendo lo spettro di massa a quel tR
- **Intensità del picco** → proporzionale alla quantità di metabolita

### MS/MS → Impronta Molecolare

Un ulteriore livello analitico aggiunge:

- **m/z dei frammenti daughter** → lo spettro di frammentazione è unico per ogni molecola

La combinazione **(tR, m/z precursore, m/z frammenti)** costituisce un'impronta molecolare specifica.

L'obiettivo finale è una **tabella** che riporti per ciascun campione tutti questi parametri + l'area sottesa al picco (quantificazione).

---

## Qualità del Picco

Il **picco ideale** è:

- Stretto e simmetrico (alta risoluzione)
- Con baseline stabile (ritorna al valore di fondo)
- Senza indentazioni

**Problemi comuni e soluzioni:**

|Problema|Causa/Soluzione|
|---|---|
|Code asimmetriche|Interazioni non ideali con la fase stazionaria|
|Baseline mobile|Variazione del segnale di fondo durante la corsa|
|Picco troncato (flat-top)|Saturazione del rivelatore → diluire il campione e rianalizzare|
|Picchi sovrapposti|Risoluzione insufficiente → **deconvoluzione**: sfrutta assunzioni sulla forma ideale del picco (simmetria) per separare i contributi; le assunzioni sono puramente analitiche|

---

## Identificazione

### Strategie

**1. Standard-based**

|Tipo|Descrizione|Affidabilità|
|---|---|---|
|**In-house**|Confronto con standard di metaboliti precedentemente analizzati in laboratorio|Massima|
|**Esterno (librerie pubbliche)**|Confronto con database pubblici; più comune per GC-MS, dove gli spettri EI sono altamente riproducibili|Alta (GC-MS), minore per LC-MS|
Il match viene confermato dal confronto simulataneo di tR, m/z del precursore ed m/z dei frammenti. Cruciale è che la metodologia cromatografico sia la più simile possibile tra analisi del campione e generazione della libreria, per riproducibilità.

**2. Standard-free / putative identification** (per metaboliti non noti)

Se non otteniamo un match (metabolita sconosciuto o non esiste uno standard commerciale), la **massa esatta** e il **pattern di frammentazione** rimangono gli strumenti principali per l'identificazione, anche quando si cambiano metodi cromatografici o di frammentazione, calcolando i valori di m/z attesi.

- **MS1 → formula molecolare (candidati), non struttura**
- **MS2 → pattern di frammentazione**  
    → ricostruiamo la struttura analizzando:
    - frammenti (picchi)
    - gap (perdite neutre: H₂O, CO₂, ecc.)
- **Similarity searching**  
    → cerchiamo pattern di frammentazione simili  
    → indica **stesso scaffold chimico con modificazioni** (es. glicosilazione)
- **In silico fragmentation prediction**  
    → confronto con spettri teorici generati computazionalmente
- **De novo elucidation**  
    → integrazione con tecniche come **NMR**

Nello standard-free spesso si sfruttano algoritmi di machine learning e banche dati esterne per definire la struttura molecolare del metabolita incognito a partire dai soli dati strumentali.


### Considerazioni per il Confronto

Per il confronto tra spettri è essenziale che la frammentazione sia riproducibile, quindi deve essere identico l'esperimento di frammentazione.

**Variazioni in frammentazione MS/MS**

- Energia di collisione e modalità di frammentazione possono variare tra strumenti → producono pattern di frammenti diversi
- Il confronto richiede **stessa energia di frammentazione**, stessa metodica e durata simili

**Addotti**

- I metaboliti possono formare addotti (es. sodiazione \[M+Na]⁺) che alterano il m/z rispetto alla massa nativa
- Occorre identificare correttamente la tipologia di ione prima di assegnare la massa molecolare

**Drift del tempo di ritenzione**

- Colonne o strumenti diversi, o usura della colonna, causano variazioni di tR → rende difficile il confronto diretto con librerie esterne


### Deconvoluzione degli Addotti

La sorgente MS può produrre vari addotti a partire dalla stessa molecola. La deconvoluzione mira a identificare queste forme derivanti da un unico analita per evitare di contarle come metaboliti distinti.
Ad ogni tempo di ritenzione, si ricercano feature separate da differenze di massa dati dalle diverse forme adduttive.

### Isotopologhi
Gli isotopologhi sono problematici -> Sono molecole di struttura identica ma con distribuzione isotopica differente.
La de-isotopizzazione è il processo di ricerca dei picchi corrispondenti a isotopologhi della stessa molecola.
All'interno di ogni spettro, si ricercano masse separate da sostituzioni isotopiche conosciute
La capacità di distinguere isotopologhi è fondamentale e viene sfruttata quando il sistema viene arricchito artificialmente con isotopi più pesanti (flussomica).

### Allineamento
L'allineamento è necessario quando si confrontano più campioni. Anche tentando di mantenere costanti le condizioni cromatografiche, piccoli shift nei tempi di ritenzione si verificano inevitabilmente tra le iniezioni.
L'allineamento corregge questi scostamenti, sincronizzando i picchi attraverso tutti i campioni in modo che la matrice di dati sia corretto.

### QA/QC

Per garantire riproducibilità e accuratezza, è essenziale implementare diversi fattori di controllo:
- Replicati -> Replicati tecnici dello stesso campione per valutare la variabilità strumentale e analitica
- Randomizzare l'ordine dei campioni di analisi per evitare bias sistematici (Deriva strumentale, effetto carry-over) influenzino i risultati
- QC -> Blanks -> fondamentali per valutare e sottrarre il background strumentale ed eventuale contaminazione
	- Standard -> Iniezione periodica di standard a concentrazione nota per monitorare le prestazioni dello strumento
- QA -> Ispezione manuale della qualità dei dati generati dal software, verificando forma dei picchi, stabilità della baseline e coerenza degli spettri di massa
### Normalizzazione
Mira a ridurre variabilità biologica e analitica. Dipende da molti fattori -> metodologia comune di normalizzazione in campioni cellulari è la normalizzazione rispetto al contenuto proteico. Si quantifica il pellet proteico e la quantità di metaboliti ritrovata viene normalizzata rispetto alla quantità di proteina iniziale, fungendo da misura del volume cellulare o della biomassa 
L'output finale è una tabella completa che riporta i parametri identificativi (Nome, tR, m/z
Parent/Daughter) e le aree dei picchi normalizzate per tutti i campioni, pronta per l'analisi statistica.

---

## Quantificazione

| Tipo         | Metodo                                                        | Output                                  |
| ------------ | ------------------------------------------------------------- | --------------------------------------- |
| **Relativa** | Solo area del picco, normalizzata per variabilità di carico   | Confronto dei livelli tra campioni      |
| **Assoluta** | Curva di calibrazione con diluizioni seriali di standard puri | Concentrazione assoluta (molare, ng/mL) |

---

## Isomeri e Isobari

|Caso|Problema|Soluzione|
|---|---|---|
|**Isomeri**|Stesso m/z → indistinguibili per MS|Separazione cromatografica efficiente: spesso il tR differisce|
|**Isobari**|Sostanze non correlate con m/z quasi identico → in MS/MS la frammentazione coinvolgerebbe entrambe simultaneamente|Separazione cromatografica: molecole diverse hanno quasi certamente tR diversi|

---

## Formati File

I file raw degli strumenti sono spesso in formato **proprietario**. **ProteoWizard** (msConvert) converte tra formati proprietari e formati aperti (es. mzML, mzXML).


# Fluxonomica

Un approccio della metabolomica Targeted è la flussonomica, assistita da isotopi stabili.
L'obiettivo principale della flussonomica non è misurare le quantità assolute ma misurare le velocità (i flussi) con cui i metaboliti si formano e si interconvertono
- Monitoraggio -> Si monitora l'incorporazione di marcatori isotopici lungo un pathway metabolico specifico. In pratica si nutre il sistema con un substrato marcato e si osserva quanto rapidamente e in che misura l'isotopo viene trasferito ai metaboliti a valle

Applicazioni -> Studi in vivo, studio delle alterazioni metaboliche (effetto warburg nei tumori), efficienza dei bioreattori nell'utilizzo del carbonio

L'analisi dei dati di flussonomica è complessa:
- Rilevazione MS o NMR, per distinguere la massa degli isotopologhi
- Modello matematico metabolico che ipotizza le possibili risposte metaboliche del sistema
L'integrazione di questi due elementi permette di mappare i flussi e di comprendere come il flusso di un determinato metabolita si ripartisce attraverso i pathway metabolici a valle, fornendo una visione dinamica della funzione cellulare

Metaboliti chiave:
- ATP
- acetil-CoA
- NAD+
- S-AdenosilMetionina SAM
Comprendere i livelli e i flussi di questi metaboliti permette di interpretare direttamente lo stato funzionale della cellula.


## Metabolomica Statica vs Dinamica

La comprensione della relazione tra metabolismo e funzione biologica richiede più di una semplice misurazione della quantità di metaboliti

La metabolomica classica fornisce una misura delle concentrazioni assolute dei metaboliti, misurata pero al netto di un equilibrio dinamico Formazione-Catabolismo. 
È un apporccio statico, non fornisce alcune idea di quanto velocemente il metabolita venga consumato o formato, nè quale pathway sia preferibilmente attivo.

Il tracing isotopico utilizza isotopi stabili (C-13, N-15, Deuterio), introducendo dinamicità nello studio metabolico:
- Misura l'andamento del pathway per capire se una via è arricchita in una specifica condizione
- Si introduce un substrato marcato e si monitora come l'isotopo viene incorporato nei metaboliti a valle, consentendo di capire come una perturbazione (knockout genico, sovraespressione, farmaco) influisce sul flussi metabolici
Un flusso può essere attivo ad elevata concentrazione di metaboliti, ma misurandolo possiamo identificare lo stato funzionale del pathway -> forse la concentrazione di metaboliti elevata è dovuta al fatto che il flusso è bloccato in un determinato stadio, mentre nel normale il flusso è pienamente attivo

Esempio: In S. cerevisiae, in assenza di glucosio, il PEP aumenta in concentrazione. L'aumento di PEP è dovuto all'attivazione di un flusso anaplerotico, che lo produce dall'ossalacetato tramite PEP-carbossichinasi, non dalla glicolisi