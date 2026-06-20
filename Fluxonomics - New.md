# Fluxonomica (Metabolomica Dinamica)

> La flussonomica non misura le quantità assolute dei metaboliti, ma le **velocità (flussi)** con cui si formano e si interconvertono.

Un approccio targeted della metabolomica. → [[Metabolomica New]]

---

## Metabolomica Statica vs Dinamica

|Aspetto|Metabolomica classica (statica)|Flussonomica (dinamica)|
|---|---|---|
|**Cosa misura**|Concentrazioni assolute dei metaboliti|Velocità di formazione/consumo (flussi)|
|**Limitazione**|Le concentrazioni riflettono un equilibrio netto Formazione–Catabolismo; non rivelano la velocità né quale pathway sia preferenzialmente attivo|—|
|**Strumento**|MS o NMR diretti|Isotopi stabili (C-13, N-15, Deuterio) + MS o NMR|
|**Domanda**|_Quanto c'è?_|_Quanto velocemente si forma? Da dove viene?_|

> Una concentrazione elevata di un metabolita può significare che il flusso è **bloccato a valle**, non che sia aumentata la produzione. Solo il tracing isotopico permette di distinguere i due scenari.

**Esempio:** In _S. cerevisiae_ in assenza di glucosio, il PEP aumenta in concentrazione. Il tracing rivela che l'aumento è dovuto all'attivazione di un **flusso anaplerotico** (PEP-carbossichinasi dall'ossalacetato), non dalla glicolisi.

---

## Principio del Tracing Isotopico

Si fornisce alle cellule un substrato vitale (glucosio, glutammina) arricchito artificialmente con **isotopi stabili non radioattivi** (tipicamente ¹³C). Il ¹³C viene incorporato nei metaboliti a valle in modo proporzionale al flusso con cui il pathway si attiva. L'analisi dei rapporti tra forme non marcate e marcate fornisce informazioni quantitative sui flussi.

### Nomenclatura degli Isotopologhi

I metaboliti marcati vengono denominati in base al **numero di atomi pesanti incorporati**:

|Notazione|Significato|
|---|---|
|**M0**|Nessun isotopo marcato (forma nativa)|
|**M+1**|Un atomo marcato (es. un ¹³C)|
|**M+2**|Due atomi marcati|
|**M+N**|N atomi marcati|

> **Esempio:** Citrato M+5 = citrato con 5 atomi di carbonio marcati con ¹³C.

### Notazione del Substrato

- **U-¹³C₆-glucosio**: glucosio marcato su **tutti e 6 i carboni** (U = _uniformly labeled_)
- Si possono usare varianti di **marcatura posizionale** per isolare il flusso attraverso pathway specifici che si intersecano

---

## Comportamento Cromatografico degli Isotopologhi

Gli isotopologhi di uno stesso metabolita hanno **identico tempo di ritenzione (tR)** in cromatografia: la massa aggiuntiva del marcatore è troppo piccola per influenzare le proprietà chimico-fisiche della molecola.

La distinzione avviene **esclusivamente per MS ad alta risoluzione**, che rileva la differenza di massa tra M0, M+1, M+2, ecc.

---

## Analisi dei Dati

L'analisi flussonomica integra due elementi:

1. **Dati strumentali** (MS o NMR): rilevazione e quantificazione degli isotopologhi
2. **Modello matematico metabolico**: ipotizza le possibili risposte del sistema ai flussi

L'integrazione permette di **mappare i flussi** e capire come il carbonio (o altro elemento) si ripartisce attraverso i pathway metabolici a valle.

**Metaboliti chiave da monitorare:**

|Metabolita|Ruolo funzionale|
|---|---|
|ATP|Energia cellulare|
|Acetil-CoA|Hub del metabolismo centrale (lipidi, TCA)|
|NAD⁺|Cofattore redox|
|SAM (S-adenosilmetionina)|Donatore di metile per metilazioni epigenetiche|

Comprendere livelli e flussi di questi metaboliti permette di interpretare direttamente lo stato funzionale della cellula.

---

## Applicazioni

- Studi delle alterazioni metaboliche tumorali (es. **effetto Warburg**)
- Identificazione di flussi metabolici alternativi (reazioni anaplerotiche)
- Efficienza dei bioreattori nell'utilizzo del carbonio
- Comprensione dell'impatto di perturbazioni (knockout genico, sovraespressione, farmaci) sui flussi metabolici

---

## Protocollo Sperimentale

### Separazione delle Fonti Marcate

È cruciale **non mescolare mai fonti di carbonio marcate diverse in un unico esperimento**: la cellula non distingue ¹²C da ¹³C (il metabolismo avviene normalmente), ma il ricercatore deve attribuire univocamente la marcatura alla fonte corretta.

**Protocollo standard** (esempio glucosio + glutammina):

|Esperimento|Glucosio|Glutammina|
|---|---|---|
|**1 — Controllo M0**|Non marcato|Non marcata|
|**2 — Tracing glucosio**|¹³C-marcato|Non marcata|
|**3 — Tracing glutammina**|Non marcato|¹³C-marcata|

Solo eseguendo esperimenti separati su un identico numero di cellule è possibile tracciare e quantificare separatamente il contributo dei due pathway.

---

## In Vivo vs In Vitro

Il tracing isotopico è applicabile anche **in vivo** (gli isotopi stabili non sono radioattivi e sono generalmente sicuri):

|Fase|Procedura|
|---|---|
|**Esaurimento endogeno**|Digiuno per rimuovere le risorse metaboliche non marcate|
|**Somministrazione**|Singola iniezione o infusione costante del substrato marcato|
|**Raccolta**|Dopo un tempo prestabilito|

### Anomalia In Vivo: Riciclo della CO₂ Marcata

In vivo si osserva un'anomalia rispetto all'in vitro: **la marcatura M+1 è dominante**, particolarmente per citrato, malato e altri metaboliti del ciclo di Krebs.

|Condizione|Comportamento della CO₂ marcata|
|---|---|
|**In vivo**|La CO₂ ¹³C prodotta **non lascia il sistema**: viene **reincorporata** in reazioni anaplerotiche (es. PEP-carbossichinasi), generando metaboliti M+1|
|**In vitro**|L'ambiente è saturato con CO₂ non marcata, che diluisce rapidamente la CO₂ ¹³C endogena → l'incorporazione è trascurabile|

> Il riciclo della CO₂ in vivo è una reazione sostanziale e fondamentale, ma **invisibile in vitro**.