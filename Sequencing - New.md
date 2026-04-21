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

### Note sull'Amplificazione Clonale

L'amplificazione clonale si rende necessaria per ottenere un segnale misurabile (intensità della luce, variazione di pH, ecc.) durante il sequenziamento. Tuttavia può introdurre problemi:

- **Distorsioni** a causa di errori nella fase di amplificazione
- **Non uniformità** nella scelta degli stampi (contenuto in GC e altre caratteristiche rendono alcuni frammenti più suscettibili ad amplificazione)
- **Impossibilità di rilevare** modificazioni del DNA quali la metilazione

> Le tecnologie di terza generazione sono in grado di sequenziare singole molecole di DNA senza amplificazione, superando questi limiti.

---

## Pirosequenziamento (454/Roche)

Il pirosequenziamento è una strategia NGS completamente automatizzata e rapida, che sequenzia tra **100 e 1000 basi per lettura**. Si basa interamente sul rilascio di PPi durante la reazione di sintesi (**Sequencing-by-Synthesis**).

Macchinari che implementano il pirosequenziamento: **Roche GS 454 FLX+** e **Roche GS Junior**.

### Preparazione della Libreria

![[Pasted image 20260420165104.png]]

1. **Frammentazione** — il gDNA viene frammentato per nebulizzazione o sonicazione
2. **Ligazione degli adattatori** — una ligasi lega covalentemente gli adattatori A e B ai frammenti
3. **Selezione dei frammenti A-B** — la ligazione è casuale e genera combinazioni A-A, A-B, B-A, B-B. L'adattatore B è **biotinilato**: la purificazione con **streptavidina** cattura i frammenti contenenti B (A-B e B-B); gli altri vengono scartati
4. **Denaturazione** — i frammenti catturati vengono denaturati, rilasciando il filamento privo di B → si ottiene **ssDNA con adattatore A** pronto per l'emPCR

```
Ligazione casuale:   A-A   A-B   B-A   B-B
                                 |
              Purificazione streptavidina-biotina
              (cattura tutto ciò che contiene B)
                                 |
                          A-B       B-B
                                 |
                           Denaturazione
                                 |
                   ssDNA [A]————————
                   (input per emPCR)
```

### emPCR (Emulsion-Based Clonal Amplification)

![[Pasted image 20260420155256.png]]

1. Le librerie ssDNA vengono mescolate a **capture beads** (microbiglie ad agarosio a cui vengono legate singole molecole di DNA)
2. Il tutto viene immerso in acqua contenente i reagenti PCR
3. Si aggiunge l'**emulsionante** (olio): l'acqua si diffonde in minuscole goccioline sospese nell'olio. L'amplificazione avviene nelle micelle
4. Statisticamente, la maggior parte delle gocce contiene **esattamente un bead e un frammento di DNA**
5. Avviene la **PCR** all'interno dell'intera emulsione → amplificazione clonale del frammento su ogni bead (~1 milione di copie identiche per bead)
6. Si rimuove l'olio e si raccolgono i singoli bead contenenti DNA

Non avviene nessun clonaggio o colony-picking.

> La maggior parte dei bead non produce prodotti funzionali, ma poiché ne vengono generati un gran numero questo non costituisce un problema.

I bead vengono depositati in una **PicoTiter Plate** insieme ai bead enzima, centrifugati, e il sequenziamento avviene simultaneamente in centinaia di migliaia di pozzetti da picolitri.

![[Pasted image 20260420115755.png]] ![[Pasted image 20260420115729.png]]

### Componenti della reazione

|Componente|Ruolo|
|---|---|
|DNA Polimerasi|Catalizza l'aggiunta dei dNTP|
|ATP solforilasi|Converte il PPi rilasciato in ATP|
|Luciferasi|Converte la luciferina in ossiluciferina (→ luce)|
|Apirasi|Degrada il dNTP non incorporato e l'ATP in eccesso|
|Adenosinsolfofosfato (APS)|Substrato per l'ATP solforilasi|
|Luciferina|Substrato per la luciferasi|
|Primer|Devono essere adeguati per il macchinario|
|dNTP|TTP, GTP, CTP e Adenosin-α-tio-trifosfato|

> ⚠️ Al posto dell'ATP normale si usa l'**Adenosin-α-tio-trifosfato**: è riconosciuto dalla polimerasi ma non dalla luciferasi, così da verificare la complementarietà dell'adenina senza produrre un segnale luminoso spurio.

### Protocollo di Sequenziamento

1. I bead ottenuti da emPCR vengono depositati nella PicoTiter Plate nei micropozzetti
2. Un **solo tipo di dNTP** viene aggiunto alla reazione per volta:
    - Se non complementare → nessun allungamento → l'**apirasi** lo degrada
    - Se complementare → la polimerasi lo incorpora → rilascio di **PPi**
3. Il PPi viene convertito in **ATP** dall'ATP solforilasi; l'ATP fornisce energia alla luciferasi per produrre **luce** dalla luciferina, rilevata da una camera **CCD**
    - L'**intensità** del segnale è proporzionale al numero di basi uguali consecutive incorporate nello stesso ciclo
    - **Segnale nullo** → il dNTP aggiunto non è complementare
4. L'apirasi degrada l'eccesso di dNTP non incorporato e l'ATP prima del ciclo successivo
5. I 4 dNTP vengono aggiunti **ciclicamente** fino al completamento della sequenza

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

### Preparazione della Libreria

1. **Frammentazione** — il gDNA viene frammentato in frammenti di dimensioni appropriate
2. **Riparazione delle estremità** — le reazioni di taglio generano un mix di protrusioni; le estremità vengono riparate:
    - Overhang al 5' → riempiti da **DNA polimerasi** (Fill-In)
    - Overhang al 3' → rimossi da una **3'→5' esonucleasi** (Blunting)
    - Terminazioni al 5' → **fosforilate** da una chinasi
    - Terminazioni al 3' → **adenilate** (A-Tailing), necessario per la ligazione T→A
3. **Ligazione degli adattatori** — due adattatori **identici** vengono ligati ad entrambe le estremità, così che gli oligonucleotidi della flowcell possano riconoscerli. Gli adattatori sono **non complementari alle loro terminazioni**, formando una struttura a **Y** che previene la self-ligazione. Questa struttura a Y viene persa dopo l'amplificazione.

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

#### Formazione dei Cluster
1. Più di 150 di singole molecole si ibridizzano ai primer oligonucleotidici della flow cell
2. Le molecole legate vengono poi estese da una polimerasi
3. La molecola a doppio filamento viene denaturata, ed il template viene scartato, mentre il filamento di nuova sintesi rimane legato alla superficie della flowcell
	- Le singole molecole rimangono legate alla flowcell in un pattern casuale
4. I singoli filamenti si ripiegano su primer adiacenti e formano un ponte
5. Il primer ibridizzato viene esteso dalla polimerasi, formando un ponte a doppio filamento
6. Il ponte a doppio filamento viene denaturato, portando a formazione di due copie legate covalentemente ai primer
7. Si ripetono step 4-6 finchè non si formano più ponti contemporaneamente
8. Si denaturano tutti i ponti e vengono rimossi i filamenti in reverse, lasciando un cluster con solo i filamenti in forward
9. Ai filamenti viene aggiunto un Fl-NTP (nucleotidi trifosfato marcati a fluorescenza) ed una polimerasi
10. I Fl-NTP sono nucleotidi modificati che terminano la sintesi e portano un segnale fluorescente per identificare la base aggiunta
11. Dopo l'incorporazione del Fl-NTP nella catena, il sequenziatore rileva il segnale fluorescente emesso
12. Una volta registrata la fluorescenza, il gruppo terminatore ed il colorante fluorescente vengono rimossi dal Fl-NTP per consentire l'aggiunta del nucleotide successivo
13. Il processo si ripete per 25-150 cicli per determinare la sequenza