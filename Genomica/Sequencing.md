## Phred Score
L'algoritmo Phred assegna un punteggio di probabilità di accuratezza di identificazione di ogni base mentre legge i tracciati elettroforetici prodotti dal sequenziamento.

Di base inizio e fine di un elettroferogramma non sono di qualità elevata.

Phred applica metodi statistici per esaminare l'andamento delle 4 basi nella regione che precede e segue ogni picco.

$$Phred\_score = -10\log_{10} P$$
Dove P è la Probabilità di errore.
Al termine dell'analisi phred genera un file a cui ogni base è assegnato il corrispondente Phred-score.
Un phred score di 50 corrisponde al 99.999% di probabilità che la base sia stata correttamente assegnata.
Un phred score di 10 corrisponde al 90%.
Un phred score di 0 corrisponde alla certezza che la base sia sbagliata.

Per basi non riconosciute dal sequenziatore ("N"), non viene assegnato alcun phred.

---
## Metodo Sanger
Il metodo Sanger è anche detto metodo enzimatico poichè richiede l'utilizzo di un enzima.
Si basa sull'utilizzo di nucleotidi modificati ddNTP. I nucleotidi dideossi- non sono in grado di formare legami fosfodiesterici, marcando l'interruzione della reazione di sintesi. Perdono -OH al 2' (come i dNTP) e 3'.

Il protocollo classico richiede:
- Template a singolo filamento di DNA
- Primer
- DNA Polimerasi
- dNTP
- ddNTP
I ddNTP vanno marcati radioattivamente o per fluorescenza per visualizzare le bande dei frammenti di DNA neosintetizzato dopo aver effettuato l'elettroforesi.

Il campione viene diviso in 4 reazioni separate, ognuna delle quali contiene la Polimerasi e i 4 dNTP. Ad ognuna di queste reazioni viene aggiunto **solo** 1 dei ddNTP, in quantità stechiometricamente inferiori maniera tale da permettere una elongazione del frammento di DNA adeguata.
L'aggiunta del ddNTP causa la terminazione prima del raggiungimento della fine dello stampo, dando origina ad una serie di frammenti di DNA di lunghezza diversa interrotti in corrispondenza dell'integrazione del ddNTP. L'integrazione del ddNTP è ovviamente casuale.
I frammenti generati vengono fatti correre su gel di poliacrilammide-urea, che permette la separazione di essi con risoluzione di 1nt. Ognuna delle 4 reazioni viene fatta correre su pozzetti vicini, dopodichè le bande sono visualizzate sotto luce UV o lastra autoradiografica, e la sequenza viene letta direttamente su lastra o gel, a seconda del tipo di marcatura.

La metodica è stata in seguito affinata per facilitare la reazione ed automatizzarla, rendendola molto più rapida.
Attualmente i più moderni utilizzano 96 capillare e consentono di ottenere circa 100.000bp per run.


### NGS
Le tecnologie NGS sono in grado di effettuare un elevatissimo numero di sequenziamenti contemporaneamente, motivo per cui sono chiamate anche ad alto parallelismo.
Ne esistono svariate versioni che utilizzano reazioni chimiche e strategie differenti.
#### Pirosequenziamento
Il pirosequenziamento è una strategia NGS molto rapida ma in grado di sequenziare tra le 100 e le 1000 basi per volta.
È un metodo enzimatico completamente automatizzato, permette il sequenziamento della catena complementare.
1. La sequenza da analizzare viene amplificata tramite PCR, e viene incubata a singola elica insieme a:
	- Primers adeguati
	- dNTP
	- Adenosinsolfofosfato (ASP)
	- Luciferina
	con Enzimi:
	- DNA polimerasi
	- ATP solforilasi
	- luciferasi
	- apirasi
2. Un solo tipo di dNTP viene aggiunto alla reazione per volta. Se non combacia al template, l'allungamento non avviene ed il nucleotide viene degradato dalla apirasi, in caso di complementarietà, la polimerasi ne catalizza l'aggiunta con liberazione di PPi
3. Il PPi poroddot viene rilevato da una camera fotosensibile CCD (charge coupled device) producendo un segnale luminoso. Utilizzando ASP come substrato, la solforilasi catalizza la conversione del PPi in ATP, il quale fornisce energia per la conversione della luciferina in ossiluciferina da parte della luciferasi. Il segnale luminoso viene catturato da un pirogramma. La presenza del segnale conferma l'appartenenza del nucleotide nella posizione analizzata della catena. L'intensità del segnare sarà proporzionale al numero di ripetizione della base lungo lo stesso filamento. Impulso doppio o triplo è indice di inglobamento nello stesso ciclo di 2 dNTP uguali (ripetizione della stessa base 2 o 3 volte sul template). Segnale nullo  indica che il dNTP aggiunto in quel ciclo non è complementare
4. L'apirasi degrada l'eccesso di dNTP non incorporato, e l'eccesso di ATP prodotto dalla solforilasi. Solo quando l'eccesso viene rimosso completamente si può aggiungere un secondo dNTP per far progredire la reazione di polimerizzazione. Si ritorna allo step 1.
5. Si aggiungono ciclicamente quindi tutti e 4 i dNTP fino al completamento della sequenza. Non può essere usato l'ATP ovviamente, ma si usa Adenosin-$\alpha$ -tio-trifosfato, analogo riconosciuto dalla polimerasi ma non dalla luciferasi, così da verificare la complementarietà della adenina senza produrre un continuo segnale luminoso che non deriverebbe dalla reazione di conversione a pirofosfato ma dall'aggiunta di ATP utilizzato direttamente dalla luciferasi
#### Preparazione delle librerie
- Il gDNA (genomic DNA) viene frammentato in pezzi più corti ed uniformi. Il macchinario, specie se a short-read, non può leggere intere sequenze cromosomiche da inizio a fine (eccetto t2t)
- Dopo la frammentazione, il DNA viene riparato all'estremità
- Un enzima ligasi lega covalentemente gli adattatori preparati al frammento di DNA creando una molecola completa di libreria
	- Gli adattatori possono legare le sequenze alla flow-cell ed assicurarsi compatibilità di piattaforma. Possono includere unique molecular identifiers UMI che aiutano nella identificazione di varianti
- Durante la ligazione, gli adattatori si legano in maniera casuale. Supponendo 2 adattatori, potremmo avere sequenze A-A, A-B, B-A, B-B.
	- Per il sequenziamento sono necessarie solo le sequenze A-B, di conseguenza andiamo a rimuovere tutti gli altri frammenti e isoliamo con purificazione avidina-biotina.
- I frammenti selezionati vengono denaturati e separati in due filamenti, portando alla formazione del sstDNA senza clonazione e colony-picking
#### emPCR
Emulsion Based Clonal amplification:
- Gli adattatori contenenti le librerie DNA vengono mescolati a capture bead
- Questi vengono immersi in una emulsione acqua in olio, contenente reagenti PCR
- 