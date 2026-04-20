---
publish: true
---


# Metodi di Sequenziamento

---

## Phred Score

L'algoritmo **Phred** assegna un punteggio di probabilità di accuratezza di identificazione di ogni base durante la lettura dei tracciati elettroforetici prodotti dal sequenziamento.

$$\text{Phred score} = -10\log_{10} P$$

Dove $P$ è la probabilità di errore.

| Phred Score | Accuratezza | Probabilità di errore |
| ----------- | ----------- | --------------------- |
| 50          | 99,999%     | 1 su 100.000          |
| 10          | 90%         | 1 su 10               |
| 0           | 0%          | Certezza di errore    |

> Inizio e fine di un elettroferogramma non sono di qualità elevata. Per basi non riconosciute dal sequenziatore (`N`) non viene assegnato alcun Phred score.

Al termine dell'analisi, Phred genera un file in cui ad ogni base è assegnato il corrispondente punteggio.

---

## Metodo Sanger (Metodo Enzimatico)

Il metodo Sanger si basa sull'utilizzo di **nucleotidi dideossi (ddNTP)** modificati, che non sono in grado di formare legami fosfodiesterici, causando la terminazione della sintesi. Rispetto ai normali dNTP, i ddNTP perdono il gruppo -OH sia al 2' che al 3'.

### Componenti della reazione

- Template a singolo filamento di DNA
- Primer
- DNA Polimerasi
- dNTP (i 4 normali)
- ddNTP (marcati radioattivamente o per fluorescenza)

### Protocollo
![[Pasted image 20260420155402.png]]
1. Il campione viene diviso in **4 reazioni separate**, ciascuna contenente polimerasi e i 4 dNTP
2. Ad ognuna viene aggiunto **un solo ddNTP** (uno per reazione), in quantità stechiometricamente inferiori per permettere una elongazione adeguata prima della terminazione
3. L'incorporazione casuale del ddNTP interrompe l'elongazione, generando una serie di **frammenti di lunghezza diversa**, ognuno terminante in corrispondenza della base del ddNTP aggiunto
4. I frammenti vengono separati su **gel di poliacrilammide-urea** (risoluzione di 1 nt)
5. Le 4 reazioni vengono caricate su pozzetti vicini e le bande visualizzate sotto luce UV o su lastra autoradiografica
6. La sequenza viene letta direttamente dal gel o dalla lastra (dipende se marcati radioattivamente o per fluorescenza)

### Automazione

La metodica è stata progressivamente affinata e automatizzata. I sistemi moderni utilizzano **96 capillari** e consentono di ottenere circa **100.000 bp per run**.

---

## NGS (Next Generation Sequencing)

Le tecnologie NGS eseguono un elevatissimo numero di sequenziamenti in parallelo (**alto parallelismo**). Ne esistono svariate versioni che utilizzano reazioni chimiche e strategie differenti.

I vantaggi principali presentati da NGS sono:

1. Non è richiesto clonaggio classico dei frammenti di DNA da sequenziare
2. L'utilizzo di micro o nano reattori normalmente immobilizzati su un supporto solido permette un elevato livello di parallelizzazione
3. La determinazione della sequenza non richiede il passaggio limitante della separazione elettroforetica: i nucleotidi incorporati vengono simultaneamente identificati durante la sintesi


### Preparazione delle librerie

Prima del sequenziamento, il DNA genomico deve essere preparato in una **libreria**:

1. **Frammentazione** -> il gDNA viene frammentato in frammenti di dimensioni appropriate in funzione della tecnologia usata e dell'applicazione. Due metodi comuni:
	- **Mechanical Shearing**:
		- **Sonicazione** -> Si utilizza un sonicatore che emette onde acustiche a bassa frequenza per tagliare il campione
		- **Nebulizzazione** -> Si utilizza un gasso in compressione, forzando una soluzione di acido nucleico attraverso un piccolo foro nel nebulizzatore. Il livello di frammentazione viene controllato dalla pressione del gas
	- **Enzymatic Digestion**:
		- Alternativa al Mechanical Shearing in cui si utilizza una endonucleasi per tagliare entrambi i filamenti o singoli filamenti creado dsBreakage. Per evitare base-bias, si utilizzano enzimi con meno specificità di taglio oppure un insieme di endonucleasi di diversa tipologia
2. **Ligazione degli adattatori** —  gli **adattatori** vengono legati alle librerie preparate
    - Gli adattatori sono usati per l'amplificazione clonale e per il sequenziamento stesso

### Note sull'Amplificazione Clonale

L'amplificazione clonale si rende necessaria per ottenere un segnale misurabile (intensità della luce, variazione di pH, ecc.) durante il sequenziamento. Tuttavia può introdurre problemi:

- **Distorsioni** a causa di errori nella fase di amplificazione
- **Non uniformità** nella scelta degli stampi (contenuto in GC e altre caratteristiche rendono alcuni frammenti più suscettibili ad amplificazione)
- **Impossibilità di rilevare** modificazioni del DNA quali la metilazione

> Le tecnologie di terza generazione sono in grado di sequenziare singole molecole di DNA senza amplificazione, superando questi limiti.

---

## Pirosequenziamento (454/Roche)

Il pirosequenziamento è una strategia NGS completamente automatizzata, rapida, che sequenzia tra **100 e 1000 basi per volta** per lettura.
Uno dei macchinari che implementano il Pirosequenziamento è il Roche GS 454 FLX+ ed il Roche GS junior.
Il pirosequenziamento è un metodo che si basa interamente sul rilascio di PPi da parte della reazione di sintesi, motivo per cui è chiamato Sequencing-by-Synthesis.
### Preparazione delle Librerie e Titolazione
![[Pasted image 20260420165104.png]]
Prima del sequenziamento, il DNA genomico deve essere preparato in una **libreria**:

1. **Frammentazione** -> il gDNA viene frammentato per nebulazione o sonicazione.
2. **Ligazione degli adattatori** -> una ligasi lega covalentemente gli **adattatori** ai frammenti
3. **Selezione dei frammenti** -> durante la ligazione gli adattatori si legano casualmente. Con due adattatori A e B si ottengono combinazioni A-A, A-B, B-A, B-B. Solo i frammenti **A-B** sono utili per il sequenziamento; gli altri vengono rimossi tramite **purificazione avidina-biotina**. L'adattatore B è **biotinilato**: la purificazione con **streptavidina** cattura selettivamente tutti i frammenti contenenti B (A-B e B-B).
4. **Denaturazione** -> i frammenti catturati vengono denaturati. Si rilascia il filamento privo di B (ovvero il filamento con adattatore A del frammento A-B), ottenendo **ssDNA con adattatore A** a un'estremità → pronto per l'emPCR.

---

### emPCR (Emulsion-Based Clonal Amplification)
![[Pasted image 20260420155256.png]]

L'emPCR è il metodo di amplificazione clonale utilizzato in piattaforme NGS di 
pirosequenziamento prima del sequenziamento:
1. Le librerie DNA vengono mescolate a **capture beads** (microbiglie ad agarosio a cui vengono legate singole molecole di DNA)
2. Il tutto viene immerso in acqua contenente i reagenti PCR
3. Si aggiunge l'**emulsionante** (olio): l'acqua si diffonde in minuscole goccioline sospese nell'olio. L'amplificazione avviene nelle micelle, che contengono i reagenti necessari per PCR
4. Statisticamente, la maggior parte delle gocce contiene **esattamente un bead e un frammento di DNA**
5. Avviene la **PCR** all'interno dell'intera emulsione → amplificazione clonale del frammento su ogni bead. L'amplificazione genera un milione di molecole identiche sulla superficie di ogni bead
6. Si rimuove l'olio e si raccolgono i singoli bead contenenti DNA

Non avviene nessun clonaggio o colony-picking.

> La maggior parte dei bead non produce prodotti funzionali, ma poiché ne vengono generati un gran numero questo non costituisce un problema.


I bead vengono poi depositati in una **PicoTiter plate**, aggiunti i bead enzima, centrifugato e il sequenziamento avviene simultaneamente in centinaia di migliaia di pozzetti di dimensioni in picolitri.
![[Pasted image 20260420115755.png]]

![[Pasted image 20260420115729.png]]

---
### Componenti della reazione

| Componente                 | Ruolo                                              |
| -------------------------- | -------------------------------------------------- |
| DNA Polimerasi             | Catalizza l'aggiunta dei dNTP                      |
| ATP solforilasi            | Converte il PPi rilasciato in ATP                  |
| Luciferasi                 | Converte la luciferina in ossiluciferina (→ luce)  |
| Apirasi                    | Degrada il dNTP non incorporato e l'ATP in eccesso |
| Adenosinsolfofosfato (APS) | Substrato per l'ATP solforilasi                    |
| Luciferina                 | Substrato per la luciferasi                        |
| Primer                     | Devono essere adeguati per il macchinario          |
| dNTP                       | TTP, GTP, CTP, e Adenosin-α-tio-trifosfato         |

> ⚠️ Al posto dell'ATP normale si usa l'**Adenosin-α-tio-trifosfato**: è riconosciuto dalla polimerasi ma non dalla luciferasi, così da verificare la complementarietà dell'adenina senza produrre un segnale luminoso spurio (e continuo).

### Protocollo

1. La sequenza da analizzare viene amplificata tramite PCR e denaturata a singolo filamento insieme a primer, dNTP, APS, luciferina e agli enzimi sopra elencati
2. I bead ottenuti da emPCR vengono depositati su un apposito vetrino dove vengono alloggiate in micropozzetti di dimensioni appropriate
3. Un **solo tipo di dNTP** viene aggiunto alla reazione per volta
    - Se non è complementare al template → nessun allungamento → l'apirasi lo degrada
    - Se è complementare → la polimerasi lo incorpora → rilascio di **PPi**
4. Il PPi viene convertito in **ATP** dall'ATP solforilasi; l'ATP fornisce energia alla luciferasi per convertire la luciferina in **ossiluciferina**, producendo un **segnale luminoso** rilevato da una camera CCD (charged coupled device)
    - Il segnale viene registrato in un **pirogramma**
    - L'**intensità** del segnale è proporzionale al numero di basi uguali consecutive incorporate nello stesso ciclo
    - **Segnale nullo** → il dNTP aggiunto non è complementare
5. L'apirasi degrada l'eccesso di dNTP non incorporato e l'ATP in eccesso prima del ciclo successivo
6. I 4 dNTP vengono aggiunti **ciclicamente** fino al completamento della sequenza

### FlowGram
![[Pasted image 20260420153839.png]]
Il FlowGram viene generato dal macchinario al termine del sequenziamento.

- **Ascissa** → nucleotide passato (ciclo)
- **Ordinata** → intensità del segnale luminoso; se supera una certa soglia indica la ripetizione di un nucleotide (omopolimero)
### Lunghezza delle Read
![[Pasted image 20260420170811.png]]

La lunghezza delle read dipende strettamente dalla quantità di **omopolimeri** (es. `AAA`, `GGG`) nella sequenza: più omopolimeri sono presenti, più basi vengono incorporate per ciclo, risultando generalmente in read più lunghe.

> Un sequenziamento Illumina produrrebbe un grafico piatto, poiché nella preparazione della libreria le read vengono uniformate ad una stessa lunghezza.

### Formato 454 SFF

I file **Standard Flowgram Format (SFF)** sono l'equivalente 454 dei file ABI del cromatogramma Sanger. Contengono:

- FlowGram
- Sequenza chiamata
- Qualità
- Qualità raccomandata e adaptor clipping

I clipping raccomandati sono forniti dal macchinario 454, tenendo conto della qualità e della sequenza dell'adattatore.

Il file `.sff` può essere convertito in formato **FASTA**:

- L'header sarà nella forma `>seq_name description`
- Le informazioni sulla qualità, se disponibili, vengono esportate in un **secondo file FASTA parallelo** con lo stesso ordine delle sequenze, ma contenente i valori di qualità al posto delle basi

---
## Illumina

### FlowCell

La flowcell di Illumina possiede **8 canali** e presenta sulla sua superficie un gran numero di **oligonucleotidi complementari agli adattatori**. È un ambiente contenuto, quindi non è necessario operare in camere pulite. Il sequenziamento avviene interamente all'interno della flowcell.
#### Preparazione della Libreria Illumina
1. **Frammentazione** -> il gDNA viene frammentato in frammenti di dimensioni appropriate. 
2. **Riparazione** -> le reazioni di taglio generano un mix di protrusioni al 5' e 3' quindi le estremità dei frammenti devono essere riparate. Le estremità in overhang vengono spuntate (Blunting) da una esonucleasi e "riempite" (Fill-In) da una DNA polimerasi
	- Overhang al 5' vengono riempiti da DNA polimerasi
	- Overhang al 3' vengono rimossi da una 3'->5' esonucleasi
	- Le terminazioni al 5' del DNA spuntato (post-Blunting) vengono fosforilate da una chinasi
	- Le terminazioni al 3' del DNA spuntato vengono adenilate (A-Tailing), necessario per la ligazione T->A
3. **Ligazione degli adattatori** -> due adattatori **identici** vengono ligati ad entrambe le estremità, così che gli oligonucleotidi della flowcell possano riconoscerli. Gli adattatori sono **non complementari alle loro terminazioni**, formando una struttura a **Y** che previene la self-ligazione. Questa struttura a Y viene persa dopo l'amplificazione.
	- Possono includere unique molecular identifiers UMI che aiutano nella identificazione di varianti
### Formazione dei Cluster (Bridge PCR)

1. Le singole molecole di libreria si **ibridizzano** agli oligonucleotidi della flowcell
2. Le molecole legate vengono estese da una **polimerasi**
3. Il dsDNA viene **denaturato**: il template originale viene scartato, il filamento neosintetizzato rimane legato alla flowcell
4. Il filamento si ripiega su un **oligonucleotide adiacente** formando un **ponte**
5. Il primer ibridizzato viene esteso → **ponte a dsDNA**
6. Il ponte viene denaturato → **due copie** legate covalentemente alla flowcell
7. Si ripetono gli step 4–6 finché non si formano più ponti simultaneamente → **cluster clonale**
8. Tutti i ponti vengono denaturati e i **filamenti in reverse vengono rimossi** → rimane un cluster di soli filamenti forward

### Sequenziamento per Sintesi (SBS)

9. Vengono aggiunti **Fl-NTP** (nucleotidi trifosfato marcati a fluorescenza) e una polimerasi
    - I Fl-NTP sono **terminatori reversibili**: bloccano la sintesi dopo l'incorporazione e portano un segnale fluorescente per identificare la base aggiunta
10. Dopo l'incorporazione, il sequenziatore rileva il **segnale fluorescente**
11. Il **gruppo terminatore** e il **colorante fluorescente** vengono rimossi per consentire l'aggiunta del nucleotide successivo
12. Il processo si ripete per **25–150 cicli** per determinare la sequenza

### 4-Channel SBS vs 2-Channel SBS

![[Pasted image 20260420185242.png]]![[Pasted image 20260420185301.png]]
In SBS a 4 canali, 4 immagini sono necessarie per catturare la tinta fluorescente unica per ogni base.
In SBS a 2 canali, 2 immagini sono richieste per determinare tutte e 4 le chiamate ad una base