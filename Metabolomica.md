

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