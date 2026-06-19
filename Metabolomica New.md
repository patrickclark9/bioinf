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

Sorgente di ionizzazione standard è Impatto elettronico per GC-MS
## LC-MS
Si utilizza principalmente Reversed-Phase LC.
- Fase stazionaria apolare idrofobica (catene C-18 o C-8 spesso derivatizzate)
- Fase mobile -> Inizia polare acquosa, e procede verso una fase mobile più apolare (acetonitrile 0.1% acido formico)
Qui le molecole meno polari eluiscono dopo perchè la fase stazionaria è apolare, quindi formano interazioni più forti con la fase stazionaria rispetto alla mobile.
Molti metaboliti sono estremamente polari, quindi la reversed phase non fornisce risoluzione ottimale -> HILIC

Il grande sviluppo della LC in metabolomica è stato guidato dall'innovazione nei materiali delle
colonne cromatografiche (ad esempio, le particelle sub-2 micrometri utilizzate
nell'UPLC/UHPLC). Questi progressi tecnologici hanno continuamente migliorato l'efficienza di
separazione e la risoluzione analitica dei metaboliti.
ESI-LC-MS è lo standard
### HILIC
- Fase stazionaria polare
- Mobile va da apolare e procede verso una più acquosa, con aumento progressivo della componente acquosa
Si ottiene l'inverso, i composti più polari vengono trattenuti più a lungo, i meno polari eluiscono prima.
HILIC permette una maggiore separazione e risoluzione delle sostanze polari, dilazionando la loro uscita nel tempo maggiormente per una migliore analisi

## Detection MS vs NMR

La più utilizzata è la GC-MS o LC-MS:
- Ion-Trap, Q, QqQ, o Q-TOF sono comuni per quantificazione, a bassa/media risoluzione
- Orbitrap, FT-ICR-MS hanno accuratezza di massa e risoluzione molto elevata, usati in ambiti specialistici. L'elevata risoluzione permette di distinguere molecole con masse molto vicine
Spesso si usano in combinazione GC-MS e LC-MS, dipendentemente dal metabolita.

La risonanza magnetica atomica valuta un assorbimento di energia da parte dei nuclei atomici, che viene rilasciata:
- Poco sensibile, la separazione energetica tra i livelli di spin nucleare è molto ridotta, aumenta solo all'aumentare dell'intensità del campo magnetico applicato
- Necessita di strumenti che applicano campi magnetici intensi
- Molto riproducibile
- La bassa sensitività richiede quantitativo di materiale elevato, rispetto ad MS
- La preparazione del campione consiste solo nel solubilizzarlo, molto semplice, almeno rispetto a MS
- Non distruttiva
- Fondamentale nel Tracing Isotopico, molto sensibile agli isotopi pesanti
- Distingue bene gli isomeri
In genere si combinano più tecniche per combinare alta sensibilità. identificazione e dati strutturali completi

## Analisi Eluizione -> Identificazione

L'output iniziale è il cromatogramma, che visualizza i picchi dei metaboliti nel tempo: separazione cromatografica

## MS
L'analisi singolo MS genera un'analisi 2D:
- Tempo di ritenzione -> Istante di eluizione del metabolita
- m/z aprendo lo spettro a quel tempo
- Intensità del picco -> Proporzionale alla quantità di metabolita

## MS/MS
Un ulteriore livello analitico:
- m/z dei frammenti daughter -> spettro di frammentazione è unico per ogni molecola
- La configurazione tempo di ritenzione, m/z precursore, m/z frammento fornisce una impronta molecolare specifica

L'obiettivo è compilare una tabella che riporti per ciascun campione tutti questi parametri, insieme all'area sottesa al picco -> Quantificazione

### Identificazione
Per identificare, similmente alla proteomica, si utilizzano database metabolici, e si confronta metabolita incognito contro i campioni del DB. 
Si confronta tempo di ritenzione, m/z precursore e m/z daughter. Cruciale è che la metodologia cromatografica tra DB ed esperimento sia quanto più simile possibile, motivo per cui spesso si fanno database in house.

L'identificazione è più complessa per:
- Variabilità analitica-> colonne o strumenti diversi, tR diversi
- Database -> i metaboliti sono tantissimi, non sempre si ottiene un match univoco
Il picco è una variazione significativa e sostenuta del segnali di fondo.
Il picco ideale è:
- Sottile e appuntito -> simmetrico e con alta risoluzione
- Baseline stabile -> Ritorna alla baseline, non a uno superiore
- Curvo, no indentazione
Problemi:
- Forme non ideali, code
- Baseline mobile
- picchi tronchi dovuta a saturazione. Se l'intensità misurata supera il limite di saturazione dello strumento, il campione va diluito e rianalizzato
- Picchi sovrapposti:
	- In questo caso si fa deconvoluzione:
		- Si sfruttano assunzioni sulla forma ideale del picco, come la simmetria, per separare distintamente i due picchi. Le assunzioni possono non riflettere la realtà chimica, sono assunzioni puramente analitiche
Le strategie di identificazione sono:
- Standard based:
	- In house -> Confronto con standard di metaboliti precedentemente analizzati in laboratorio -> massima affidabilità
	- Esterno -> Confronto con librerie pubbliche, più comune per GC-MS, dove gli spettri sono più riproducibili
- Standard free per metaboliti non noti:
	- Sulla base dei valori di m/z e dei pattern di frammentazione si tenta di ricostruire la struttura della molecola.
	- Se il metabolita è totalmente nuovo, allora bisogna integrare tecniche non distruttive NMR
Bisogna tener conto di:
- Variazioni in frammentazione -> Energia di collisione e tipologia di frammentazione in MS/MS possono variare e produrre diversi pattern di frammenti
- Addotti -> I metaboliti possono formare addotti per sodiazione o altro, che alterano peso molecolare rispetto alla nativa. È essenziale identificare correttamente di quale ione si sta parlando prima di assegnare la massa alla molecola
La massa esatta e l'analisi del pattern di frammentazione rimangono gli strumenti principali per identificare le sostanze, anche quando si utilizzano nuovi metodi cromatografici o di
frammentazione, al fine di calcolare i valori di m/z attesi.

### Quantificazione
- Relativa -> Solo area del picco, confronta i livelli di metabolita tra diversi campioni (normalizzati per variabilità di carico)
- Assoluta -> Si vuole ottenere concentrazione assoluta (Molare, ng/mL) -> Serve una curva di calibrazione di diluizione seriale di standard puri, per correlare i picchi osservati a quelli noti
## Isomeri e Isobari
- Gli isomeri avranno stesso m/z. Per distinguerli serve una separazione cromatografica molto efficiente, poichè spesso varia il tempo di ritenzione
- Isobari -> Sostanze non correlate ma con m/z quasi identico -> in MS/MS la frammentazione avverrebbe su entrambe le molecole simultaneamente. La separazione cromatografica risolve questo problema perchè quasi sicuramente due sostanze completamente diverse avranno tempi di ritenzione diversi

File spesso proprietari -> ProteoWizard converte tra formati proprietari

