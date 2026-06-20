

# Introduzione

La metabolomica si concentra sullo studio e l'analisi di tutti i metaboliti presenti in un sistema biologico in un dato momento.
La metabolomica colma il divario tra genotipo e fenotipo:
- Non c'è relazione lineare tra mRNA e proteina. Inoltre la proteina può essere presente ma inattivata da modificazioni post-traduzionali
- La quantificazione e l'identificazione di metaboliti ci fornisce il readout funzionale del sistema. Lo studio del metaboloma ci dice cosa sta succedendo a livello fisiologico

## Specificità
Il metaboloma è eterogeneo e variegato (zuccheri, lipidi, ecc...) rispetto al proteoma.

In metabolomica si applicano classiche sorgenti di ionizzazione hard, poichè la frammentazione che inducono possono essere specifiche e riproducibili, cruciale per identificare metaboliti piccoli.

## Approcci
- Bulk -> Tradizionale, lavora sul metaboloma completo e aggregato di tutto il campione
- Spaziale/Single-cell -> Innovativi che permettono di analizzare il metaboloma spaziale o a livello della singola cellula

- Statica -> Analisi di un preciso stato metabolico
- Dinamica (Flussonomica) -> Analisi dinamica utilizzando metaboliti precursori marcati con isotopi stabili, per tracciare il percorso e la velocità con cui le molecole fluiscono attraverso le vie metaboliche.

Il metaboloma è l'indicatore ultimo dello stato funzionale di un sistema biologico. È la prova che una cascata di eventi si è effettivamente attivata.

I metaboliti sono indicatori essenziale dello stato funzionale della cellula, disregolazioni si manifestano rapidamente in variazioni del contenuto di specifici metaboliti
Stanno acquisendo capacità come biomarcatori. La loro alterazione può indicare uno stato patologico prima che si manifestano cambiamenti a livello proteico o genico.

Il metabolismo è centrale nella regolazione epigenetica. Fenotipo e Genotipo sono fortemente influenzati dall'ambiente esterno, ed il metabolismo è il meccanismo attraverso cui il sistema si adatta e risponde ai segnali ambientali.

Ad esempio, la S-adenosilmetionina SAM è uno dei principali donatori di metile per la metilazione del DNA.

## Problema
Il numero di metaboliti in un organismo ecede di gran lunga quello delle proteine e dei geni.
I metaboliti possono essere endogeni -> prodotti ciclicamente da anabolismo e catabolismo
Possono derivare dalla dieta/farmaci o altro.
Sono tanti >200.000, ed eterogenei (3.000 classi chimiche diverse).

![[Pasted image 20260619093720.png]]

Attualmente non è possibile analizzare il metaboloma completo con un unico sistema cromatografico, si ricorre alla separazione in comparti:
- Si analizza il Metaboloma idrofilico
- Si analizza separatamente il comparto dei lipidi
Si ottengono quindi più estratti dallo stesso campione biologico.
Abbiamo bisogno di sistemi che soddisfano esigenze contrastanti:
- Risoluzione e accuratezza -> Bisogna spingere la risoluzione al massimo perchè molecole diverse possono avere valori di m/z identici o molto simili. L'accuratezza è necessaria per distinguere queste molecole
- Ampio Range Dinamico -> La concentrazione dei metaboliti varia enormemente ma la bassa concentrazione nonb è indice di scarsa importanza funzione. Bisogna spingere la sensibilità del sistema per rilevare anche i metaboliti meno abbondanti
Alta risoluzione e alta sensibilità contemporaneamente non è semplice
Sono necessari sistemi High throughput, poichè spesso l'analisi richiede un numero elevato di campioni N, con elevata automazione e grande velocità di analisi.

La concentrazione non è correlata all'importanza funzionale.
Non esiste un'unica tecnica in grado di visualizzare l'intero metaboloma in un solo esperimento. 
La MS deve affrontare requisiti contrastanti.
## Tecnologie
- NMR -> Prevalente in passato, ma aveva bassa sensibilità, richiedendo grandi quantitià di campione
- La spettrometria di massa (soprattutto avanzamenti di questa, con velocità di scansione aumentata e maggiore risoluzione) ha permesso di identificare metaboliti a livelli di concentrazione più bassi, spingendo lo sviluppo della disciplina

## Lipidomica
È una disciplina a se stante, dato che richiedono metodi particolari date le loro caratteristiche chimiche (apolarità, richiedono HPLC diversi). La metabolomica generale ha beneficiato maggiormente dalle tecniche MS applicate a molecole più polari e reattive.
![[Pasted image 20260619094140.png]]

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

Quenching -> Rimozione proteine (centrifugazione), rimuove pellet proteico e lascia una fase liquida contenente il metaboloma -> Estrazione selettiva, frazionamento e purificazione dell'estratto, si utilizza LC o GC spesso. Esempio usare cloroformia in seconda estrazione per ottenere il metaboloma lipofilico.

Queste fasi sono seguita da analisi spettrometrica di massa e analisi dei risultati.

### Detection
Dipende da origine del metaboloma (intracellulare o extracellulare)
- Intracellulare  separa biomassa dal sovranatante-> Si separa per centrifugazione, metanolo/acqua fredda per estrarre il metaboloma e indurre quenching. Ulteriore centrifugazione per rimuovere le proteine
- Extracellulare è il sovranatante-> Separato dalle cellulare tramite centrifugazione, estrazione avviene aggiungendo metanolo freddo per indurre precipitazione delle proteine. Centrifugazione ulteriore per la rimozione

Per campioni solidi o ambientali, il campione viene analizzato in toto -> Disomogeneizzato (azoto liquido, meccanicamente (afrullatori et al) in presenza di solventi freddi), si raccoglie il lisato post-centrifugazione che contiene i metaboliti

## Separazione cromatografica
Passaggio obbligatorio nel workflow metabolomico -> Risolve risoluzione e distinzione tra metaboliti diversi, che pur avendo lo stesso PM devono essere analizzati separatamente. Il tempo di ritenzione in colonna permette la distinzione. Un altro aspetto è la duilizione temporale, che diluisce nel tempo l'ingresso dei vari metaboliti verso la sorgente di ionizzazione di MS. L'intera massa di metaboliti contemporaneamente sarebbe impossibile da analizzare, dato che MS/MS richiede un certo tempo strumentale per l'acquisizione

Se l'obiettivo è la quantificazione assoluta, è indispensabile utilizzare una curva di calibrazione per metabolita -> Standard puro diluito serialmente a concentrazione nota, poi si relazionano i due dati: concentrazione nota dello standard e area sottesa al picco cromatografico generato, da cui possiamo interpolare i dati
### GC-MS

La GC è importante in metabolomica, limitata però a sostanze volatili -> Iniettore a temperature elevate, immediata volatilizzazione del campione liquido iniettato.
Nella GC l'interazione dei composti con la fase stazionaria è modulata dalla temperatura.
Non si varia la composizione chimica della fase mobile, si applica invece un gradiente di temperatura, che aumentando, favorisce l'eluizione dei vari composti.

La maggior parte dei metaboliti nei campioni biologici non è volatile.
Derivatizzazione -> Si asciuga il campione (rimozione acqua). Dopodichè si utilizzano silani (agenti derivatizzanti), aggiungono gruppi (ad esempio trimetilsilil o TMS) a gruppi funzionali di metaboliti al campione secco, rendendo le molecole più volatili e meno termolabili. I silani reagiscono con gruppi nucleofili (ammine, ossidrili, carbossilici). In assenza di questi e presenza di carbonilici ad esempio (C=O) si usa metossiamina per stabilizzare i gruppi funzionali e derivatizzarli.
Ovviamente derivatizzazione ha conseguenze -> Modifica del peso molecolare, TMS aggiunto e quindi m/z; La GC utilizza impatto elettronico, la quale produce inevitabilmente ioni frammento direttamente nella sorgente. Le librerie per GC-MS contengono già lo spettro di frammentazione atteso per il metabolita già derivatizzato con uno specifico agente. Queste librerie sono robuste e validate, rendendo possibile la consultazione della libreria per dedurre il valore di m/z atteso sia di ione molecolare che dei frammenti

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
Si confronta tempo di ritenzione, m/z precursore e m/z daughter. Cruciale è che la metodologia cromatografica tra DB ed esperimento sia quanto più simile possibile, 

L'identificazione è più complessa per:
- Variabilità analitica-> colonne o strumenti diversi, tR diversi (drift di tR dovuto a variazione strumentale)
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
	- In silico database generation
	- Sulla base dei valori di m/z e dei pattern di frammentazione si tenta di ricostruire la struttura della molecola.
	- De novo elucidation -> Se il metabolita è totalmente nuovo, allora bisogna integrare tecniche non distruttive NMR
Durante il confronto bisogna tener conto di:
- Variazioni in frammentazione -> Energia di collisione e tipologia di frammentazione in MS/MS possono variare e produrre diversi pattern di frammenti -> Si necessita di metodica di frammentazione uguale, stessa energia di frammentazione e durata di frammentazione simile per confrontare spettri MS/MS
- Addotti -> I metaboliti possono formare addotti per sodiazione o altro, che alterano peso molecolare rispetto alla nativa. È essenziale identificare correttamente di quale ione si sta parlando prima di assegnare la massa alla molecola

**2. Standard-free / putative identification** (per metaboliti non noti)

Se non otteniamo un match (metabolita sconosciuto o non esiste uno standard commerciale), la **massa esatta** e il **pattern di frammentazione** rimangono gli strumenti principali per l'identificazione, anche quando si cambiano metodi cromatografici o di frammentazione, calcolando i valori di m/z attesi.

- **MS1 → formula molecolare (candidati), non struttura**
- **MS2 → pattern di frammentazione**  
    → ricostruiamo la struttura analizzando:
    - frammenti (picchi)
    - gap (perdite neutre: H₂O, CO₂, ecc.)
- **Similarity searching**  
    → cerchiamo pattern di frammentazione simili  
    → indica **stesso scaffold chimico con modificazioni** (es. glicosilazione)
- **In silico fragmentation prediction**  
    → confronto con spettri teorici generati computazionalmente
- **De novo elucidation**  
    → integrazione con tecniche come **NMR**

Nello standard-free spesso si sfruttano algoritmi di machine learning e banche dati esterne per definire la struttura molecolare del metabolita incognito a partire dai soli dati strumentali.

La massa esatta e l'analisi del pattern di frammentazione rimangono gli strumenti principali per identificare le sostanze, anche quando si utilizzano nuovi metodi cromatografici o di
frammentazione, al fine di calcolare i valori di m/z attesi.

### Quantificazione
- Relativa -> Solo area del picco, confronta i livelli di metabolita tra diversi campioni (normalizzati per variabilità di carico)
- Assoluta -> Si vuole ottenere concentrazione assoluta (Molare, ng/mL) -> Serve una curva di calibrazione di diluizione seriale di standard puri, per correlare i picchi osservati a quelli noti
## Isomeri e Isobari
- Gli isomeri avranno stesso m/z. Per distinguerli serve una separazione cromatografica molto efficiente, poichè spesso varia il tempo di ritenzione
- Isobari -> Sostanze non correlate ma con m/z quasi identico -> in MS/MS la frammentazione avverrebbe su entrambe le molecole simultaneamente. La separazione cromatografica risolve questo problema perchè quasi sicuramente due sostanze completamente diverse avranno tempi di ritenzione diversi

File spesso proprietari -> ProteoWizard converte tra formati proprietari
### Deconvoluzione degli Addotti

La sorgente MS può produrre vari addotti a partire dalla stessa molecola. La deconvoluzione mira a identificare queste forme derivanti da un unico analita per evitare di contarle come metaboliti distinti.
Ad ogni tempo di ritenzione, si ricercano feature separate da differenze di massa dati dalle diverse forme adduttive.

### Isotopologhi
Gli isotopologhi sono problematici -> Sono molecole di struttura identica ma con distribuzione isotopica differente.
La de-isotopizzazione è il processo di ricerca dei picchi corrispondenti a isotopologhi della stessa molecola.
All'interno di ogni spettro, si ricercano masse separate da sostituzioni isotopiche conosciute
La capacità di distinguere isotopologhi è fondamentale e viene sfruttata quando il sistema viene arricchito artificialmente con isotopi più pesanti (flussomica).

### Allineamento
L'allineamento è necessario quando si confrontano più campioni. Anche tentando di mantenere costanti le condizioni cromatografiche, piccoli shift nei tempi di ritenzione si verificano inevitabilmente tra le iniezioni.
L'allineamento corregge questi scostamenti, sincronizzando i picchi attraverso tutti i campioni in modo che la matrice di dati sia corretto.

### QA/QC

Per garantire riproducibilità e accuratezza, è essenziale implementare diversi fattori di controllo:
- Replicati -> Replicati tecnici dello stesso campione per valutare la variabilità strumentale e analitica
- Randomizzare l'ordine dei campioni di analisi per evitare bias sistematici (Deriva strumentale, effetto carry-over) influenzino i risultati
- QC -> Blanks -> fondamentali per valutare e sottrarre il background strumentale ed eventuale contaminazione
	- Standard -> Iniezione periodica di standard a concentrazione nota per monitorare le prestazioni dello strumento
- QA -> Ispezione manuale della qualità dei dati generati dal software, verificando forma dei picchi, stabilità della baseline e coerenza degli spettri di massa
### Normalizzazione
Mira a ridurre variabilità biologica e analitica. Dipende da molti fattori -> metodologia comune di normalizzazione in campioni cellulari è la normalizzazione rispetto al contenuto proteico. Si quantifica il pellet proteico e la quantità di metaboliti ritrovata viene normalizzata rispetto alla quantità di proteina iniziale, fungendo da misura del volume cellulare o della biomassa 
L'output finale è una tabella completa che riporta i parametri identificativi (Nome, tR, m/z
Parent/Daughter) e le aree dei picchi normalizzate per tutti i campioni, pronta per l'analisi statistica.
# Fluxonomica

Un approccio della metabolomica Targeted è la flussonomica, assistita da isotopi stabili.
L'obiettivo principale della flussonomica non è misurare le quantità assolute ma misurare le velocità (i flussi) con cui i metaboliti si formano e si interconvertono
- Monitoraggio -> Si monitora l'incorporazione di marcatori isotopici lungo un pathway metabolico specifico. In pratica si nutre il sistema con un substrato marcato e si osserva quanto rapidamente e in che misura l'isotopo viene trasferito ai metaboliti a valle

Applicazioni -> Studi in vivo, studio delle alterazioni metaboliche (effetto warburg nei tumori), efficienza dei bioreattori nell'utilizzo del carbonio

L'analisi dei dati di flussonomica è complessa:
- Rilevazione MS o NMR, per distinguere la massa degli isotopologhi
- Modello matematico metabolico che ipotizza le possibili risposte metaboliche del sistema
L'integrazione di questi due elementi permette di mappare i flussi e di comprendere come il flusso di un determinato metabolita si ripartisce attraverso i pathway metabolici a valle, fornendo una visione dinamica della funzione cellulare

Metaboliti chiave:
- ATP
- acetil-CoA
- NAD+
- S-AdenosilMetionina SAM
Comprendere i livelli e i flussi di questi metaboliti permette di interpretare direttamente lo stato funzionale della cellula.

Nella separazione cromatografica, i diversi isotopologhi hanno identico tempo di ritenzione nella colonna, perchè la massa del marcatore è troppo piccola per influenzare le proprietà chimico-fisiche della molecola.
Tramite MS ad alta risoluzione possiamo distinguere i diversi isotopologhi mer masse molecolari differenti.

I diversi componenti vengono chiamati M0, M1, M2, M3 ecc... in base al numero di isotopi marcati presenti. M0 = 0, M1 = +1 carbonio marcato, M2 = +2 carboni marcati
Citrato M5 = citrato a 5 atomi di carbonio marcati.
## Metabolomica Statica vs Dinamica

La comprensione della relazione tra metabolismo e funzione biologica richiede più di una semplice misurazione della quantità di metaboliti

La metabolomica classica fornisce una misura delle concentrazioni assolute dei metaboliti, misurata pero al netto di un equilibrio dinamico Formazione-Catabolismo. 
È un apporccio statico, non fornisce alcune idea di quanto velocemente il metabolita venga consumato o formato, nè quale pathway sia preferibilmente attivo.

Il tracing isotopico utilizza isotopi stabili non radioattivi (C-13, N-15, Deuterio), introducendo dinamicità nello studio metabolico:
- Misura l'andamento del pathway per capire se una via è arricchita in una specifica condizione
- Si introduce un substrato marcato e si monitora come l'isotopo viene incorporato nei metaboliti a valle, consentendo di capire come una perturbazione (knockout genico, sovraespressione, farmaco) influisce sul flussi metabolici
Un flusso può essere attivo ad elevata concentrazione di metaboliti, ma misurandolo possiamo identificare lo stato funzionale del pathway -> forse la concentrazione di metaboliti elevata è dovuta al fatto che il flusso è bloccato in un determinato stadio, mentre nel normale il flusso è pienamente attivo

Esempio: In S. cerevisiae, in assenza di glucosio, il PEP aumenta in concentrazione. L'aumento di PEP è dovuto all'attivazione di un flusso anaplerotico, che lo produce dall'ossalacetato tramite PEP-carbossichinasi, non dalla glicolisi

## Tracing Principi
- Fonte marcata -> Si fornisce alle cellule un substrato vitale (glucosio, glutammina) arricchito artificialmente al 100% con C13 o altro
- U-13C6 -> Glucosio marcato su tutti e 6 i carboni, U sta per ubiquitaria
- Il C13 viene incorporato nei metaboliti a valle di un pathway in modo direttamente proporzionale al flusso con cui quel pathway si attiva
- Gli isotopomeri vengono distinti dalla MS in base all'aumento di peso molecolare
L'analisi dei rapporti tra molecola non marcato e forme marcate ci fornisce informazioni quantitative sui flussi metabolici e sulla modificazione dell'utilizzo del metabolismo
Il tracing è fondamentale per identificare flussi metabolici alternativi come reazioni anaplerotiche.
Si possono usare varianti di marcatura posizionale per isolare e quantificare il flusso attraverso specifici pathway che si intersecano
È cruciale non mescolare mai le fonti di carbonio marcate in un unico esperimento:
-  Necessità: La cellula non distingue tra C12 e C13, quindi il metabolismo avviene
normalmente. Tuttavia, i ricercatori devono utilizzare i traccianti separatamente per poter
attribuire univocamente la marcatura all'una o all'altra fonte.
 -  Protocollo: Su un identico numero di cellule, si eseguono tre esperimenti separati:
	1. Glucosio e Glutammina non marcati (Controllo M0).
	2. Glucosio marcato e Glutammina non marcata.
	3. Glucosio non marcato e Glutammina marcata.
Solo in questo modo, analizzando la massa finale (MS), si è in grado di tracciare e quantificare
separatamente il contributo del metabolismo del glucosio da quello della glutammina.

Il tracing è effettuabile anche in vivo oltre ache in vitro. L'uso di isotopi non radioattivi è abbastanza sicuro poichè non dovrebbe produrre effetti dannosi all'organismo.
L'esaurimento delle risorse endogene viene effettuate mediante digiuno, mentre la somministrazione viene effettuata o tramite singola iniezione oppure a infusione costante. Si attende un tempo prestabilito prima della raccolta dei campioni.

In vivo si osserva una anomalia rispetto all'in vitro -> La marcatura +1 è dominante, particolarmente per Citrato e Malato e altri del ciclo di Krebs.

La CO2 marcata M+1 in vivo non lascia il sistema ma viene reincorporata nei metaboliti, partecipando alle vie anaplerotiche, come la PEP carbossichinasi, producendo metaboliti marcati +1. In vitro l'ambiente è spesso saturato con CO2 non marcata, che diluisce rapidamente la CO2 marcata endogena, rendendone trascurabile l'incorporazione.
Quindi in vivo la CO2 marcata endogena è una reazione sostanziale e fondamentale nel contesto in vivo, ma invisibile in vitro.