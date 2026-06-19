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

**2. Standard-free** (per metaboliti non noti)

- **In silico database generation**: sulla base di m/z e pattern di frammentazione si tenta di ricostruire la struttura
- **De novo elucidation**: se il metabolita è totalmente nuovo, si integrano tecniche non distruttive come **NMR**

### Considerazioni per il Confronto

**Variazioni in frammentazione MS/MS**

- Energia di collisione e modalità di frammentazione possono variare tra strumenti → producono pattern di frammenti diversi
- Il confronto richiede **stessa energia di frammentazione**, stessa metodica e durata simili

**Addotti**

- I metaboliti possono formare addotti (es. sodiazione [M+Na]⁺) che alterano il m/z rispetto alla massa nativa
- Occorre identificare correttamente la tipologia di ione prima di assegnare la massa molecolare

**Drift del tempo di ritenzione**

- Colonne o strumenti diversi, o usura della colonna, causano variazioni di tR → rende difficile il confronto diretto con librerie esterne

> La **massa esatta** e il **pattern di frammentazione** rimangono gli strumenti principali per l'identificazione, anche quando si cambiano metodi cromatografici o di frammentazione, calcolando i valori di m/z attesi.

---

## Quantificazione

|Tipo|Metodo|Output|
|---|---|---|
|**Relativa**|Solo area del picco, normalizzata per variabilità di carico|Confronto dei livelli tra campioni|
|**Assoluta**|Curva di calibrazione con diluizioni seriali di standard puri|Concentrazione assoluta (molare, ng/mL)|

---

## Isomeri e Isobari

|Caso|Problema|Soluzione|
|---|---|---|
|**Isomeri**|Stesso m/z → indistinguibili per MS|Separazione cromatografica efficiente: spesso il tR differisce|
|**Isobari**|Sostanze non correlate con m/z quasi identico → in MS/MS la frammentazione coinvolgerebbe entrambe simultaneamente|Separazione cromatografica: molecole diverse hanno quasi certamente tR diversi|

---

## Formati File

I file raw degli strumenti sono spesso in formato **proprietario**. **ProteoWizard** (msConvert) converte tra formati proprietari e formati aperti (es. mzML, mzXML).