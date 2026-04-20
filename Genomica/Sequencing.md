

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

---

### Preparazione delle Librerie

Prima del sequenziamento, il DNA genomico deve essere preparato in una **libreria**:

1. **Frammentazione** -> il gDNA viene frammentato in pezzi corti ed uniformi (i macchinari short-read non possono leggere intere sequenze cromosomiche). Due metodi comuni:
	- **Mechanical Shearing**:
		- **Sonicazione** -> Si utilizza un sonicatore che emette
2. **Riparazione** -> le estremità dei frammenti in overhang vengono spuntate (blunting) per Fill-In ed esonucleasi
	- Le estremità spuntate vengono fosforilate, e viene aggiunto un singolo nucleotide A al 3'
	- L'attività esonucleasica rimuove nucleotidi al 5' o 3', mentre il Fill-In consiste nell'aggiunta di nucleotidi al 3' ad opera di una Polimerasi
3. **Ligazione degli adattatori** -> una ligasi lega covalentemente gli **adattatori** ai frammenti
    - Gli adattatori permettono il legame alla flow-cell e assicurano la compatibilità di piattaforma
    - Possono includere **UMI** (Unique Molecular Identifiers) per l'identificazione di varianti
4. **Selezione dei frammenti** -> durante la ligazione gli adattatori si legano casualmente. Con due adattatori A e B si ottengono combinazioni A-A, A-B, B-A, B-B. Solo i frammenti **A-B** sono utili per il sequenziamento; gli altri vengono rimossi tramite **purificazione avidina-biotina**
5. **Denaturazione** -> i frammenti selezionati vengono denaturati in ssDNA, senza necessità di clonazione o colony-picking

---

### emPCR (Emulsion-Based Clonal Amplification)

L'emPCR è il metodo di amplificazione clonale utilizzato in alcune piattaforme NGS prima del sequenziamento:
![[Pasted image 20260420155256.png]]
1. Le librerie DNA vengono mescolate a **capture beads**
2. Il tutto viene immerso in acqua contenente i reagenti PCR
3. Si aggiunge l'**emulsionante** (olio): l'acqua si diffonde in minuscole goccioline sospese nell'olio
4. Statisticamente, la maggior parte delle gocce contiene **esattamente un bead e un frammento di DNA**
5. Avviene la **PCR** all'interno dell'intera emulsione → amplificazione clonale del frammento su ogni bead
6. Si rimuove l'olio e si raccolgono i singoli bead contenenti DNA
Infinite vengono generati milioni di template amplificati su ogni bead.
Non avviene nessun clonaggio o colony-picking.

> La maggior parte dei bead non produce prodotti funzionali, ma poiché ne vengono generati un gran numero questo non costituisce un problema.


I bead vengono poi depositati in una **PicoTiter plate**, aggiunti i bead enzima, centrifugato e il sequenziamento avviene in centinaia di migliaia di pozzi di dimensioni in picolitri.
![[Pasted image 20260420115755.png]]
![[Pasted image 20260420115729.png]]
---

### Pirosequenziamento

Il pirosequenziamento è una strategia NGS completamente automatizzata, rapida, che sequenzia tra **100 e 1000 basi per volta** per lettura.
Uno dei macchinari che implementano il Pirosequenziamento è il Roche GS 454 FLX+ ed il Roche GS junior.
Il pirosequenziamento è un metodo che si basa interamente sul rilascio di PPi da parte della reazione di sintesi, motivo per cui è chiamato Sequencing-by-Synthesis.

#### Componenti della reazione

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

#### Protocollo

1. La sequenza da analizzare viene amplificata tramite PCR e denaturata a singolo filamento insieme a primer, dNTP, APS, luciferina e agli enzimi sopra elencati
2. Un **solo tipo di dNTP** viene aggiunto alla reazione per volta
    - Se non è complementare al template → nessun allungamento → l'apirasi lo degrada
    - Se è complementare → la polimerasi lo incorpora → rilascio di **PPi**
3. Il PPi viene convertito in **ATP** dall'ATP solforilasi; l'ATP fornisce energia alla luciferasi per convertire la luciferina in **ossiluciferina**, producendo un **segnale luminoso** rilevato da una camera CCD
    - Il segnale viene registrato in un **pirogramma**
    - L'**intensità** del segnale è proporzionale al numero di basi uguali consecutive incorporate nello stesso ciclo
    - **Segnale nullo** → il dNTP aggiunto non è complementare
4. L'apirasi degrada l'eccesso di dNTP non incorporato e l'ATP in eccesso prima del ciclo successivo
5. I 4 dNTP vengono aggiunti **ciclicamente** fino al completamento della sequenza

##### FlowGram
![[Pasted image 20260420153839.png]]
Viene generato dal macchinario al termine del sequenziamento.
- Ascissa -> Nucleotide passato
- Ordinata -> Intensità del segnale luminoso. Se supera una certa soglia, significa ripetizione di un nucleotide

