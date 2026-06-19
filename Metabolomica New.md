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
Analisi dell'intero tessuto o dell'intero campione biologico.
Si distinguono due tipologie di analisi
- Untargeted (screening): Non è un'analisi selettiva, non si focalizza su specifici metaboliti
	- L'analizzatore (spesso MS) scansione un intero range di massa m/z d'interesse, senza preselezionare alcun valore
	- Profilo metabolico globale
	- Prevalentemente qualitativo, semi-quantitativo
	- L'identificazione dei metaboliti corrispondenti ai picchi viene effettuata a posteriori (es. MS/MS) per confronto con standard noti o librerie spettrali
- Targeted -> Selettiva, si concentra su specifiche molecole
	- Quantifica un insieme specifico e conosciuto di metaboliti (spesso coinvolti in un pathway)
	- Necessità di standard puri (metaboliti puri di interesse) e caraterrizazione spettrale (analisi dello standard, per conoscerne tempo di ritenzione, m/z del parent e daughter), ed una curva di calibrazione utilizzando diluizione seriali dello standard (stabilisce una relazione lineare tra concentrazione del metabolita e area sottesa al picco)
	- Si lavora in selettività, solo specifici m/z (noti grazie all'analisi dello standard)
	- Misurando l'area sottesa al picco del metabolita nel campione e usando la curva di calibrazione è possibile dedurre con precisione la sua concentrazione
## Workflow
- Estrazione è selettiva -> polarità dei metaboliti diversa
	- Estrazione sequenziale -> prima molecole polari, poi apolari. Esistono metodi onnicomprensivi, ma preferiscono molecole polari
- L'estrazione avviene in cellule attive -> Necessità di quenching -> fermare l'attività enzimatica che può alterare il profilo metabolico
	- Congelamento ultrarapido -> Azoto liquido -> Campioni solidi, Il campione viene portato rapidamente a temperature criogeniche, bloccando attività enzimatica. Il campione ormai duro viene polverizzato meccanicamente
	- Denaturazione con solventi organici freddi -> Si utilizzano solventi organici per denaturare le proteine, disattivando gli enzimi (metanolo freddo), lisi cellulari si effettua utilizzando sonicatori o frullatori a temperature basse 
	- Acidi o buffer specifici (acido perclorico), o buffer che aiutano a solubilizzare e portare in soluzione i metaboliti desiderati

2 Variabilità da tener conto:
1. Analitica -> Errore strumento o protocollo
2. Biologica -> Differenze naturali. Ancora più accentuata in metabolomica. I metaboliti, essendo avalle del flusso informazionale cellulare, tendono a mostrare una maggiore dispersione nel livello di concentrazione rispetto a proteine

Bisogna ottenere un numero di campioni statisticamente significativo per assicurare  una adeguata potenza statistica.

Quenching -> Rimozione proteine (centrifugazione), rimuove pellet proteico e lascia una fase liquida contenente il metaboloma -> Estrazione selettiva, frazionamento e purificazione dell'estratto, si utilizza LC o GC spesso.

Queste fasi sono seguita da analisi spettrometrica di massa e analisi dei risultati.

### Detection
Dipende da origine del metaboloma (intracellulare o extracellulare)
- Intracellulare  separa biomassa dal sovranatante-> Si separa per centrifugazione, metanolo/acqua fredda per estrarre il metaboloma e indurre quenching. Ulteriore centrifugazione per rimuovere le proteine
- Extracellulare è il sovranatante-> Separato dalle cellulare tramite centrifugazione, estrazione avviene aggiungendo metanolo freddo per indurre precipitazione delle proteine. Centrifugazione ulteriore per la rimozione

Per campioni solidi o ambientali, il campione viene analizzato in toto -> Disomogeneizzato (azoto liquido, meccanicamente (afrullatori et al) in presenza di solventi freddi)