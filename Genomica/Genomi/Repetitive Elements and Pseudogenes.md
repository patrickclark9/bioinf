---
publish: true
---
# Pseudogeni

Gli pseudogeni sono sequenze nucleotidiche che assomigliano ad un gene normale, ma non trascrivono per nessun RNA o proteina funzionale. Derivano da geni normali, quindi possono essere visti come rimasugli di geni antichi, persi durante l'evoluzione.

A volte un gene perde funzione, diventando uno pseudogene, per una semplice mutazione. Una volta persa la funzione, lo pseudogene degraderà ulteriormente accumulando mutazioni finché non sarà più possibile riconoscerlo.

---

## Tipi di Pseudogeni

### Pseudogeni Convenzionali (Non-Processed)

Si formano quando un gene perde funzione a causa di mutazione. Si distinguono in due sottotipi:

#### Pseudogeni Duplicati

Si formano quando un membro di una famiglia multigenica perde funzione a causa di mutazione. Questi eventi solitamente **non sono deleteri** perché altri geni della stessa famiglia rimangono attivi e la funzione non viene persa.

Non è raro che uno pseudogene di questo tipo sia pseudogene in un organismo ma un gene funzionale in un altro.

> **Esempio**: la δ-globina è attiva negli umani, ma è uno pseudogene nel topo.

#### Pseudogeni Unitari

Provengono sempre da mutazioni, ma **non appartengono ad una famiglia multigenica**: la perdita di funzione non viene compensata dall'attività di altri geni. Sono molto rari, poiché la perdita di funzione totale di un gene è spesso letale. Sono conosciuti meno di 50 negli esseri umani.

> **Esempio**: _L-gulono-γ-lactone oxidase_ — permette di sintetizzare acido ascorbico, ma è diventato pseudogene in tutti gli Haplorhini (il gruppo di primati che include gli umani).

---

### Pseudogeni Processati

Si formano attraverso un processo che **non coinvolge mutazione**. Derivano dall'mRNA di un gene: viene sintetizzato il cDNA corrispondente, che si reinserisce nel genoma.

Poiché sono copie dell'mRNA, presentano due caratteristiche che li rendono non funzionali:

- **Assenza di introni** del gene originale
- **Assenza delle sequenze upstream** (regolatorie) necessarie per il controllo dell'espressione genica

---

## Elementi Correlati

- **Geni troncati** — hanno perso una parte più o meno significativa al 5' o al 3' del gene
- **Frammenti genici** — piccole regioni isolate all'interno del gene

# Elementi Ripetuti

Le analisi genomiche di umani ed altri eucarioti hanno mostrato come gran parte delle sequenze che compongono il genoma siano **elementi ripetitivi**.
Le ripetizioni giocano un ruolo cruciale in molti processi biologici. Ripetizioni come promotori ed enhancer regolano l'espressione genica essendo siti di legame per fattori di trascrizione e proteine regolatorie.
Sono anche importanti elementi strutturali, nei centromeri e nei telomeri, necessari per la stabilità del cromosoma.
Le ripetizioni inoltre guidano l'evoluzione, tramite duplicazioni, ricombinazioni e processi di trasposizione.

![[Pasted image 20260419164208.png]] ![[Pasted image 20260419164225.png]]

---

## Classificazione

Gli elementi ripetitivi si classificano lungo due assi indipendenti:

**Per frequenza:**

- **Moderatamente ripetitivi**
- **Altamente ripetitivi**

**Per distribuzione:**

- **Interspersi** → le unità ripetitive sono sparse nel genoma in maniera apparentemente casuale
- **Tandem Repeat** → le unità ripetitive sono disposte una accanto all'altra a formare un array

![[Pasted image 20260419213451.png]]

---

## Tandem Repeats

Le ripetizioni tandem sono spesso chiamate **"satellite"** o variazioni di questo termine. Il nome deriva dal fatto che frammenti di DNA contenenti ripetizioni tandem formano **bande "satellite"** quando il DNA viene centrifugato a gradiente di densità.

### DNA Satellite

|Localizzazione|Elemento|Lunghezza totale|
|---|---|---|
|**Telomero**|Minisatellite `TTAGGG`|Qualche kb|
|**Centromero**|DNA satellite (es. DNA alfoide)|Diverse Mb|

### Minisatelliti e Microsatelliti

Pur non formando bande satellite durante la centrifugazione, altri due elementi tandem importanti sono i **minisatelliti** e i **microsatelliti**.

|Elemento|Dimensione del cluster|Unità ripetitiva|Localizzazione prevalente|
|---|---|---|---|
|**Minisatelliti**|Fino a 20 kb|Fino a 25 bp|Telomeri e regioni subtelomeriche|
|**Microsatelliti**|Solitamente < 150 bp|≤ 13 bp (tipico)|Distribuiti nel genoma|

Il microsatellite più comune è la ripetizione tandem di `AC`, ma sono frequenti anche i **trinucleotidi**.

> Non si sa se i microsatelliti abbiano una funzione biologica. Si sa che si formano per un errore di replicazione detto **slippage**, e potrebbero essere semplicemente il prodotto inevitabile della replicazione del genoma.

![[Pasted image 20260419170900.png]]
# Elementi Trasponibili (Trasposoni)

Le **ripetizioni tandem** si formano principalmente per _slippage_, nel caso di microsatelliti, o eventi di ricombinazione.

Le **ripetizioni intersperse**, invece, non possono essersi formate così: sono sparse lungo il genoma anche in posizioni estremamente distanti dalla sequenza originale, e non presentano alcuna ripetizione locale. La via più frequente per la loro formazione è la **trasposizione**, e molte ripetizioni intersperse hanno un'intrinseca attività trasposizionale.

> La trasposizione è una caratteristica tipica dei virus, che sono in grado di inserirsi nel genoma cellulare e muoversi al suo interno. Alcune sequenze intersperse sono sicuramente discendenti da virus trasponibili.


![[SmartSelect_20260419_181619_Moon+ Reader Pro.jpg]]

---

## Tipi di Trasposizione

|Tipo|Meccanismo|Effetto sul copy number|
|---|---|---|
|**Conservativa**|Escissione dalla posizione originale e reinserzione altrove|Nessun incremento|
|**Replicativa**|La copia originale rimane; una copia viene inserita in una nuova posizione|Incremento → possibile proliferazione nel genoma|

---

## Classificazione dei Trasposoni

```
Trasposoni
├── Intermedio a RNA (Retrotrasposizione)
│   ├── NON codificano per Trascrittasi Inversa
│   │   └── Famiglia non Virale
│   │       └── Retropseudogeni (processed pseudogeni) → Alu
│   └── Codificano per Trascrittasi Inversa
│       └── Famiglia Virale
│           ├── Con LTR (elementi retrovirus-like)
│           │   └── Retrovirus endogeni (HERV/RTLV, THE-1)
│           └── Senza LTR
│               └── Retrotrasposoni → LINE-1
└── Intermedio a DNA (RARO)
    └── Trasposoni con intermedio a DNA
```

---
## Famiglie di Trasposoni

![[Pasted image 20260419181329.png]]
Solo una piccolissima parte dei memtri delle famiglie di Trasposoni sono in grado di trasposizione. Molti hanno perso questa capacità dopo aver acquisito mutazioni che ne hanno causato l'inattivazione, e molti sono copie troncate.
Nell'immagine sono riportate sottoclassi delle 4 famiglie più importanti, insieme alla dimensione in bp.



---

## Retrotrasposizione

Il processo che richiede un intermedio ad RNA è detto **retrotrasposizione**:

1. La sequenza genomica endogena viene trascritta in RNA
2. L'RNA viene retrotrascritta a dsDNA dalla trascrittasi inversa
3. Il dsDNA si reintegra nel genoma (stesso o diverso cromosoma)

**Differenza con i retrovirus**: nei retrotrasposoni la molecola di RNA viene trascritta da una sequenza **endogena**; nei retrovirus da una sequenza **esogena**.

Gli RNA trasposoni sono comuni negli eucarioti, molto meno nei procarioti.

---

## Retroelementi con LTR
Gli RNA Trasposoni sono ulteriormente classificabili in base alla presenza di LTR o meno.
Le **LTR** (Long Terminal Repeats) sono caratteristica comune dei retroelementi virali e hanno un ruolo centrale nel processo di retrotrascrizione a dsDNA.
Questi virus sono membri di una superfamiglia di elementi che includono elementi LTR endogeni.
### Famiglie principali

#### Ty1/copia

I primi due retroelementi endogeni isolati furono **Ty1** (_S. cerevisiae_) e **copia** (_D. melanogaster_). Sono così simili da essere raggruppati nella famiglia **Ty1/copia**.

- **Non possiedono** un equivalente del gene _env_ → non sono in grado di formare particelle virali infettive
- **TyA** (_S. cerevisiae_) è molto simile a _gag_ e _pol_
- **TyB** codifica per una poliproteina che include la trascrittasi inversa

#### Ty3/gypsy

- **Possiedono** una forma di _env_ → sono in grado di produrre virus infettivi
- Sebbene classificati come retroelementi endogeni, le versioni infettive vengono considerate retroelementi virali

---

## Retrovirus Endogeni (ERV)

I retroelementi LTR compongono una parte significativa di molti genomi eucariotici, particolarmente nelle piante (es. mais), e sono componente importante anche di vertebrati e invertebrati.

Negli umani e altri mammiferi, molti elementi LTR sembrano retrovirus decaduti piuttosto che trasposoni attivi. Questi sono chiamati **retrovirus endogeni (ERV)** e compongono il **9% del genoma umano**. Contengono copie dei geni _gag_, _pol_ ed _env_, ma la maggior parte presenta mutazioni e delezioni che li rendono non funzionanti.

### HERV-K

Un'eccezione rilevante è rappresentata dalle **HERV-K** (Human Endogenous RetroVirus K):

- Possiedono sequenze funzionali
- Osservando le HERV-K in individui diversi, sembrano essere retrotrasposoni **ancora attivi**
- Alcune copie di RNA di HERV-K possono generare **particelle virali** in grado di muoversi tra le cellule

> Trascritti e proteine di HERV-K sono stati osservati nel cervello di pazienti affetti da **sclerosi laterale amiotrofica (SLA)** e dalla malattia neurodegenerativa di **Lou Gehrig**.

--- 


# Elementi senza LTR (Retroposoni)

Non tutti i trasposoni hanno elementi LTR. Nei mammiferi, i più importanti retroelementi non-LTR, detti **retroposoni**, sono i **SINE** (Short Interspersed Repeats) e i **LINE** (Long Interspersed Repeats).

|Elemento|Copie nel genoma umano|% del genoma|
|---|---|---|
|**SINE**|> 1.700.000|14%|
|**LINE**|~ 850.000|20%|

---

## LINE (Long Interspersed Repeats)

Esistono diverse famiglie di LINE. La più importante è **LINE-1**, l'unica in grado di trasporre attivamente; le altre famiglie sono composte da residui antichi inattivi.

### Struttura di LINE-1

- Lunghezza (copia intera): ~6,1 kb
- Due geni, uno dei quali codifica per una poliproteina simile al prodotto del gene _pol_
- Nessuna LTR
- Il 3' è demarcato da una coda di **poli(A)** (poli(T) nel filamento antisenso)
- Al 5' è presente un UTR che contiene un promotore bidirezionale per Pol II
- ORF1 codifica per una RNA Binding Protein
- ORF2 codifica per una poliproteina con dominio endonucleasico e dominio di Trascrittasi Inversa
### Funzione
L'inserzione di LINE1 nel DNA durante la retrotrasposizione risulta in un TSD (Target Site Duplication), fiancheggiante la nuova inserzione
### Troncamento

La trascrittasi inversa codificata da LINE spesso non completa la copia del DNA a partire dal trascritto RNA, causando la **perdita di parte del 3'**. Questo evento è talmente comune che:

> Su ~500.000 copie totali di LINE-1 nel genoma umano, solo **80–100 hanno lunghezza piena**. La dimensione media di una copia è solo ~900 bp.

![[Pasted image 20260419192722.png]]
### Ciclo di Retrotrasposizione
![[Pasted image 20260419193106.png]]


---

## SINE (Short Interspersed Repeats)

I SINE sono molto più corti dei LINE (100–400 bp) e **non contengono geni propri**: non producono trascrittasi inversa e dipendono da quella sintetizzata dal LINE-1 per la trasposizione. Alu o SVA possono co-optare per la ORF1 e ORF2 di LINE-1 e quindi retrotrasporsi.

### Elemento Alu

Il SINE più comune negli umani è **Alu**, con circa **1,2 milioni di copie**.

- Struttura: due metà, ciascuna una sequenza simile di ~120 bp, con un'inserzione di 31–32 bp nella metà destra
- Equivalente murino: **B1** (~130 bp), corrispondente ad una singola metà di Alu
- Alcuni elementi Alu possono essere copiati ad RNA, permettendo ulteriore proliferazione


**Origine**:  le Alu derivano dal gene **7SL RNA**, coinvolto nel movimento delle proteine all'interno della cellula. L'equivalente B1 nei topi suggerisce che la prima Alu si sarebbe formata per trascrizione inversa di una molecola di 7SL RNA e sua integrazione nel genoma.
![[Pasted image 20260419193540.png]]
#### Alu Attive
Su più di 1 milione di Alu presenti nel genoma umano, pochissime sono in grado di creare copie, anche se la maggior parte genera trascritti.
Dopo l'inserzione in un nuovo locus, i fattori che rendono una Alu attiva sono le sequenze fiancheggianti che influenzano il promotore, creando una corta regione unica. 
Elementi attivi hanno sequenze abbastanza simile alla sequenza Alu consensus, e possiedono una lunga e quasi-perfetta coda di poli(A).
Gli elementi attivi degradano rapidamente a causa della degradazione della coda di poli(A), con basi eterogenee che si accumulano in questa regione, oltre ad accumulo di mutazioni nella sequenza Alu stessa, portando a divergenza dal consesus.
Almeno uno di questi cambiamenti altera l'attività della Alu, attraverso interferenza con svariate proteine che si legano all'RNA nella ribonucleoproteina.
#### Esonizzazione delle Alu
![[Pasted image 20260419213141.png]]

### Elemento SINE-VNTR-Alu
Un altro elemento non autonomo è lo SVA. Elementi SVA sono composti da altre ripetizioni, contenenti:
- Ripetizione CCCTCT
- 2 Sequenze Alu-like
- Sequenza VNTR
- Regione SINE-R -> Omologo al gene env e alla sequenza LTR di retrovirus umani endogeni
- Sequenza di poli(A)
![[Pasted image 20260419193555.png]]
### Origine dei SINE in generale

Altri SINE derivano da geni per **tRNA** che, come il 7SL RNA, vengono trascritti da **Pol III** negli eucarioti. Questo suggerisce che qualcosa nel meccanismo di Pol III rende queste molecole prone ad occasionale conversione a retrotrasposone.

### Retrotrasposizione dei SINE
![[Pasted image 20260419193633.png]]
---

## Implicazioni Patologiche

La trasposizione di elementi LINE e SINE è un evento raro, ma con conseguenze potenzialmente gravi. È stata osservata in colture cellulari umane e di topo.

La scoperta di inserzioni di LINE-1, Alu e altri SINE all'interno di **geni protein-coding** è stata associata a disordini ereditabili:

> **Emofilia** — il gene _factor VIII_ subisce un'inserzione di una sequenza LINE-1 che previene la sintesi della proteina anticoagulante.

Da questa scoperta, oltre **25 malattie** sono state associate a inserzioni di LINE-1, inclusi alcuni cancri. Nuovi esempi che coinvolgono i SINE vengono tuttora scoperti.

---

## Retroelementi non-LTR nei Procarioti

Pochi retroelementi non-LTR sono conosciuti per i genomi procariotici, con copy number molto più bassi rispetto agli omologhi eucariotici. La loro distribuzione è estesa tra batteri ed archea, ma è **ceppo-specifica** (alcuni ceppi li possiedono, altri no).

Il tipo più comune di retroelemento procariotico è il **retrone**: una sequenza di ~2 kb che include il gene per la trascrittasi inversa.

---
# DNA Trasposoni

Non tutti i trasposoni richiedono un intermedio a RNA. I **DNA trasposoni** sono in grado di trasporre in maniera diretta DNA → DNA, senza intermedio trascrizionale.

---

## DNA Trasposoni nei Procarioti

I DNA trasposoni sono componenti importanti del genoma procariotico. Le principali classi sono:

- **Insertion Sequences (IS)**
- **Tn3-Type**
- **Fagi trasponibili**

### Insertion Sequences (IS)

Le IS sono gli esempi più semplici di DNA trasposoni procariotici.

|Caratteristica|Dettaglio|
|---|---|
|Dimensione|0,7 – 2,5 kb|
|Contenuto genico|Uno o due geni, tra cui quello per la **trasposasi**|
|Struttura terminale|Coppie di **ripetizioni invertite** al 5' e al 3'|
|Modalità di trasposizione|Conservativa o replicativa|
|Copy number (E. coli)|30–50 IS di diversi tipi (varia per specie e ceppo)|

### MITE (Miniature Inverted Repeat Transposable Elements)

Alcuni frammenti IS procariotici hanno perso l'abilità di trasporre e sono chiamati **MITE**. Il termine è generico per trasposoni DNA antichi troncati; furono scoperti per la prima volta nelle piante.

---

## DNA Trasposoni negli Eucarioti

I DNA trasposoni sono molto più rari negli eucarioti rispetto ai procarioti. Solo il **3,7% del genoma umano** è composto da DNA trasposoni.

**Caratteristiche comuni a tutti i DNA trasposoni eucariotici:**

- Composti da **ripetizioni terminali invertite**
- Contengono il gene per la **trasposasi**, che catalizza l'evento di trasposizione

La maggior parte di questi elementi è **inattiva**, per uno di questi motivi:

- Il gene della trasposasi è non funzionale
- Le sequenze terminali — essenziali per la trasposizione attiva — mancano o sono mutate

### Esempi notevoli

#### Piante — Ac/Ds e Spm (mais)

Nelle piante i DNA trasposoni attivi sono molto più comuni che negli animali. Gli elementi **Ac/Ds** e **Spm**, entrambi trovati nel mais, sono esempi classici. La **pigmentazione variegata nei noccioli del mais** è causata da eventi di trasposizione in cellule somatiche che interrompono geni della pigmentazione in maniera casuale.

#### D. melanogaster — Elemento P

L'elemento P è specifico di _Drosophila melanogaster_ ed è stato scoperto incrociando **femmine di laboratorio** con **maschi wild-type**. La progenie risultava sterile.

La causa è la seguente:

1. Le femmine di laboratorio non possedevano l'elemento P
2. I maschi wild-type lo possedevano, fiancheggiato da inverted terminal repeats
3. L'incrocio causa l'**attivazione** degli elementi P ereditati dal maschio nelle uova
4. Gli elementi attivati traspongono in nuove posizioni, interferendo con geni essenziali → sterilità della progenie

![[Pasted image 20260419192644.png]]