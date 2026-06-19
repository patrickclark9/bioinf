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
- Targeted -> Selettiva, si concentra su specifi