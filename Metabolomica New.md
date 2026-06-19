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

> Per la **quantificazione assoluta** è indispensabile una curva di calibrazione per ciascun metabolita: si diluisce serialmente lo standard a concentrazione nota e si mette in relazione la concentrazione con l'area del picco cromatografico, da cui si interpolano i dati campione.

---

## GC-MS

### Principio

La GC separa composti **volatili**: il campione liquido viene iniettato a temperature elevate e volatilizzato immediatamente. La separazione è modulata da un **gradiente di temperatura** (non dalla composizione della fase mobile, come in LC): all'aumentare della temperatura, i composti eluiscono progressivamente.

### Derivatizzazione

La maggior parte dei metaboliti biologici **non è volatile** ed è **termolabile**. Si ricorre alla **derivatizzazione**:

1. **Essiccazione** del campione (rimozione dell'acqua)
2. **Aggiunta di agenti derivatizzanti** (es. silani → gruppi **TMS**, trimetilsilil) che reagiscono con gruppi nucleofili (ammine, ossidrili, carbossilici), rendendo le molecole più volatili e meno termolabili
3. Per gruppi carbonilici (C=O, non nucleofili): uso di **metossiamina** per stabilizzarli prima della sililazione

**Conseguenze della derivatizzazione:**

| Effetto                            | Dettaglio                                                                                                                                                      |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Modifica del PM                    | Ogni gruppo TMS aggiunto incrementa l'm/z                                                                                                                      |
| Pattern di frammentazione alterato | La GC usa **ionizzazione per impatto elettronico (EI)**, che produce ioni frammento già nella sorgente                                                         |
**Soluzione**:

**Librerie dedicate** -> Le librerie GC-MS contengono spettri di frammentazione per il metabolita **già derivatizzato**, rendendo semplice la deduzione del valore di m/z atteso (sia di ioni molecolari sia dei frammenti). anche senza standard in loco.

## LC-MS
Si utilizza principalmente Reversed-Phase LC.
- Fase stazionaria apolare idrofobica (catene C-18 o C-8 spesso derivatizzate)
- Fase mobile -> Inizia polare acquosa, e procede verso una fase mobile più apolare (acetonitrile 0.1% acido formico)