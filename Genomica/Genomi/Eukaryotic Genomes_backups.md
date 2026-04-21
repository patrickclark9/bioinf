---
publish: true
---
## Eukaryotic Genomes

Il genoma eucariotico, a differenza degli altri, è diviso in un insieme di molecole di DNA lineari, ognuna contenuta in un cromosoma.

Questo è l'unico pattern conosciuto:

- Almeno 2 cromosomi
- Tutti lineari

I cromosomi sono sempre più piccoli delle molecole di DNA che contengono; il cromosoma medio umano possiede appena 5 cm di DNA. Di conseguenza è necessario un sistema di impaccamento adeguato. È chiaro che il sistema di impaccamento ha un'influenza chiave sui processi coinvolti nell'espressione genica.

---

### Cromatina

L'arrangiamento spaziale della cromatina all'interno dello spazio confinato del nucleo rimane non completamente chiaro. Quello che si sa è che ogni cromosoma occupa il proprio spazio (detto "**territorio del cromosoma**"). Scoperta avvenuta grazie al _chromosome staining_.

All'interno di ogni territorio cromosomico, la cromatina si folda in molteplici loop e segrega in due compartimenti:

- **Compartimento A** — Clusterizzazione attorno al nucleolo e a corpi nucleici (Regioni _Permissive_)
- **Compartimento B** — Associate a LAD (Lamina Associated Domain) nella parte periferica del nucleo (Regioni _Repressive_)

Le interazioni cromatiniche avvengono principalmente intracromosoma. La preferenza per interazioni interne al cromosoma tra regioni etero- ed eu-cromatiniche (compartimento A e B) risultano nella formazione dei **TAD** (Topologically Associated Domains), demarcati da elementi arricchiti con CTCF/Cohesin. All'interno delle TAD la cromatina si ripiega ulteriormente a formare _loop regolatori_, facilitando interazioni _close proximity_ tra promotori ed enhancer.

La **CCC** (Chromosome Conformation Capture) è la tecnica utilizzata per studiare le interazioni all'interno dei TAD. A partire da questa sono state sviluppate altre tecniche (4C, 5C, Hi-C).

Il confine di una TAD è delimitato dagli **insulator**, sequenze di 1–2 kb di lunghezza che fiancheggiano la TAD, determinando la presenza di un dominio funzionale.

> **Positional Effect** — Un gene clonato inserito in una regione a cromatina altamente compressa renderà il gene inattivo. Inserendolo in cromatina meno compressa (più aperta) permetterà l'espressione del gene. Quando fiancheggiato da un insulator, l'espressione sarà sempre elevata, poiché l'insulator determina e stabilisce un dominio funzionale nel sito di inserzione.

#### Eterocromatina

- **Costitutiva** → Permanente. Tipica di telomero e centromero e alcune regioni di altri cromosomi. Esempio fondamentale è il cromosoma Y, quasi completamente costituito da eterocromatina costitutiva dato lo scarsissimo numero di geni presenti su di esso.
- **Facoltativa** → Non permanente. Contiene geni inattivi in alcune cellule ed in alcuni periodi del ciclo cellulare. Il compattamento della cromatina non permette ai macchinari di trascrizione e traduzione di accedere ai siti necessari per l'espressione genica.

#### Eucromatina

L'esatta organizzazione del DNA all'interno dell'eucromatina non è nota, ma al microscopio elettronico sono visibili avvolgimenti (loop) di DNA all'interno delle regioni eucromatiniche, ogni loop tra 40 e 100 kb di lunghezza e predominantemente in forma di fibra cromatinica di 30 nm.

I loop di DNA tra i punti di legame nella matrice nucleare sono detti **domini strutturali**.

Un **dominio funzionale** viene identificato trattando una regione di cromatina con la **DNasi I** (deossiribonucleasi I) che non riesce ad accedere alle strutture più compatte del DNA.

#### Istoni

Tutti gli istoni sono soggetti a modifiche post-traduzionali, principalmente nelle code. Le maggiori modifiche post-traduzionali sono **acetilazione, metilazione, fosforilazione** e **ubiquitinazione**.

Le modificazioni istoniche hanno ruoli nella riparazione del DNA, la replicazione, splicing alternativo, regolazione della trascrizione e condensazione cromosomica.

|Stato|Caratteristica|
|---|---|
|**Eucromatina** (attiva)|Alti livelli di acetilazione; trimetilazione H3K4, H3K36, H3K79|
|**Eterocromatina** (repressa)|Bassi livelli di acetilazione; alta metilazione H3K9, H3K27, H4K20|

Le modifiche istoniche possono influenzare positivamente o negativamente modifiche in altri siti:

- Ubiquitinazione di H2BK123 → influenza **positivamente** la metilazione di H3K79 e H3K4
- Fosforilazione di H3S10 → influenza **negativamente** la metilazione in H3K9

#### Chromatin Remodelling

L'accessibilità del DNA in forma nucleosomica può essere modulata sfruttando enzimi che utilizzano l'energia rilasciata dall'idrolisi dell'ATP per alterare la struttura nucleosomica. L'apertura della struttura cromatinica si ottiene attraverso:

- Nucleosome sliding
- Unwrapping (dissociazione del contatto nucleosoma-DNA)
- Nucleosome Eviction
- Sostituzione di istoni (es. H2A con H2Avar a formare il dimero H2Avar-H2B)

---

## Dimensioni del Genoma Eucariotico

Le dimensioni di un genoma eucariotico sono estremamente variabili in base all'organismo.
Esiste overlap tra il genoma eucariotico più piccolo e il genoma procariotico più grande. Infatti S.cerevisiae ha un genoma di soli 12.1Mb, 3 volte più grande di quello di E.coli ma più piccolo di _Sorangium cellulosum_ (14,8 Mb) 
Una parte cruciale è l'**assenza di correlazione tra numero di geni e complessità apparente dell'organismo**. Esistono piante con genomi aploidi ben più grandi di quello umano, oltre a presentare poliploidicità.

Due fattori chiave:

- I geni eucariotici sono **interrotti** (introni)
- Presenza di **DNA ripetitivo**

Definendo la complessità di un organismo come il numero di possibili stati trascrittomici, con un modello semplice in cui un gene può trovarsi in due stati (acceso o spento), un genoma con N geni può codificare per $2^N$ stati differenti. Comparando _Homo sapiens_ a _Caenorhabditis elegans_:

$$\frac{2^{21000}}{2^{20000}} = 2^{1000} = 10^{300}$$

La densità genica (coding genes) **aumenta al diminuire della complessità** dell'organismo:

- _S. cerevisiae_ ≈ 70%
- _C. elegans_ ≈ 15%
- _H. sapiens_ ≈ 1%

---

### Densità

Il genoma eucariotico presenta molta meno densità di geni rispetto ai procarioti, soprattutto per gli organismi più complessi. _Saccharomyces cerevisiae_ e _Drosophila melanogaster_ presentano densità geniche più elevate rispetto a piante e uomo.

---

### Base Composition

I genomi eucariotici presentano meno variabilità in contenuto in GC. Tutti gli eucarioti si attestano attorno al 35–40% di contenuto in GC.

---

## Isocore

L'ultracentrifugazione del genoma dei mammiferi ha portato alla scoperta di una compartimentalizzazione del genoma in un piccolo numero di famiglie non-satellite, chiamate **isocore**.

Queste sono caratterizzate da differenti livelli in GC ed una base composition abbastanza omogenea. Sono state divise in 5 famiglie distinte:

1. **L1** e **L2** → Basso contenuto in GC
2. **H1**, **H2** e **H3** → Alto contenuto in GC

Le isocore ricche in GC sono correlate con:

- Più alta densità genica (i 2/3 dei geni protein-coding si concentrano nelle famiglie H2 e H3, che rappresentano solo il 15% del genoma)
- Replicazione all'inizio del ciclo cellulare
- Regioni trascrizionalmente attive della cromatina

Le isocore hanno dimensioni maggiori di 300 kb e sono correlate con bande ad alta e bassa risoluzione.

---

## Isole CpG

I dinucleotidi CpG si osservano con frequenza inferiore all'atteso all'interno dei vertebrati. Ad esempio in _Homo sapiens_ si osservano solo con frequenza pari a 1/5 dell'atteso. Ciò è dovuto alla tendenza della citosina a **deaminazione spontanea**:

- Citosine **non metilate** deaminano in **uracile** → riconosciuto e sostituito con citosina dal sistema di riparazione (uracil-DNA glicosilasi → escissione dell'uracile → BER pathway)
- Le CpG presentano **metilazione in posizione 5** della citosina → deaminazione spontanea in **timina** → non riconosciuta come errore (base canonica del DNA)

Nel genoma si ritrovano cluster chiamati **isole CpG** che non presentano metilazione, con elevato contenuto in GC e bassa soppressione CpG. Tipicamente hanno lunghezza di 1 kb e presentano overlap nella regione del promotore per il 60–70% dei geni umani.

La metilazione della citosina nell'isola permette il legame di **HDAC**, che comporta l'impaccamento della cromatina e quindi la **soppressione del gene**. Di conseguenza la **non-metilazione** è associata con uno stato trascrizionalmente attivo.
Possiamo individuare le isole CpG attraverso la seguente formula:

$$\text{CpG Obs/Exp} = \frac{f(CG)}{f(C) \cdot f(G)}$$
Di base troviamo un'isola CpG in base ai seguenti parametri:
$$L > 200bp$$ $$C+G \% > 50\%$$$$CpG \space Obs/Exp > 0.6$$

---

## Gene

La definizione di gene è molto complessa, dato che possiamo osservare:

- Siti alternativi di inizio della trascrizione
- Siti alternativi di terminazione
- Trascritti alternativi (splicing alternativo)
- Geni in overlap o innestati all'interno di altri geni
- Sequenze enhancer che agiscono come promotori per alcune isoforme di splicing
- Alcuni trascritti possono essere **ncRNA** (non-coding RNA)

Un gene umano ha una struttura altamente complessa:

- **Zona distale** → Sequenze regolatorie (enhancer-silencer) e TAD boundary element
- **Zona prossimale al TSS** → Sequenze regolatorie, siti di binding di proteine PcG, segnali epigenetici (metilazione del DNA, modificazioni istoniche), isole CpG
- **Sequenza del gene** → Dal sito di inizio della trascrizione; preceduto dal promotore con TATA box e CCAAT; sequenza di esoni ed introni variabile; siti di splicing multipli; sequenze intreasoniche o introniche di regolazione dello splicing
- **3' UTR** → Elementi ricchi in AU, siti di binding per miRNA, SE CIS, sito di legame per la catena di poli-A
	- SE CIS -> I SE CIS sono cluster densi di enhancer in una corta regione di DNA che può essere legata da numerosi attivatori proteici e sono associati con livelli elevati di espressione genica.
![[Screenshot from 2026-04-18 10-38-41.png]]
![[Screenshot from 2026-04-18 10-38-48.png]]

## Fase intronica
La fase intronica descrive dove esattamente un introne interrompe la reading frame di un gene. L'introne può cadere anche in mezzo ad un codone, dividendolo.
In fase 0, l'introne si trova esattamente tra due codoni. Splicing di questo introne non disrompe l'integrità del codone (ATG \[Introne] CTG)
In fase 1, l'introne interrompe il codone dopo il primo nucleotide. Quando l'mRNA subisce splicing, il primo nucleotide dall'esone a monte deve collegarsi con i prossimi due nucleotidi dell'esone sucessivo per completare il codone (A \[introne] TG).
In fase 2, è uguale alla fase 1 ma due nucleotidi a monte devono collegarsi con l'ultimo nucleotide dell'esone successivo (AT \[introne] G).
Se un introne in fase 1 effettua splicing in un sito in fase 2 si avrà misallineamento della fase e quindi un frameshift.
Un esone è detto simmetrico se fiancheggiato da introni in stessa fase da entrambi i lati.

---

## Maturazione dei trascritti e Splicing
I trascritti di Pol II subiscono maturazione, ovvero l'azione dello splicing, del capping e della poliadenilazione.
Lo splicing va a rimuovere la componente intronica, mentre capping aggiunge un cap al 5' (m7g) ed al nucleotide successivo/ 2 nucleotidi successivi, mentre la poliadenilazione consiste nell'aggiunta di un tratto poliadenilico al 3' immediatamente dopo il 3'UTR.
Capping e poliadenilazione sono essenziali per l'esportazione del mRNA all'interno del citoplasma. Stabilizzano la molecola consentendo il passaggio nucleo->citoplasma. Ovviamente nei procarioti questi due passaggi non sono necessari perchè non va attraversata alcuna membrana.

Lo splicing alternativo sono eventi di splicing differenti dalla semplice rimozioni delle porzioni introniche e dell'aggancio delle porzioni esoniche.
Esistono diversi possibili eventi di splicing alternativo:
- Alternative 5' SS (Siti di splicing alternativi al 5')
- Alternative 3' SS (Siti di splicing alternativi al 3')
- Mutually Exclusive Exons
- Cassette Exons (Esoni facoltativi)
- Intron Retention
- Alternative Promoters
- Alternative Polyadenilation
Possono avvenire anche diversi eventi alternativi per uno stesso trascritto.
L'esone è detto facoltativo se non sempre presente, costitutivo se sempre presente.
Lo splicing avviene attraverse due macchine macromolecolari dette Spliceosoma maggiore e Spliceosoma minore.
I modelli Exon e Intron definition illustrano come il macchinario di splicing riconosce accuratamente un target.
- **Modello Exon Definition** -> Il macchinario si assembla sull'esone riconoscendo i siti di splicing attorno ad un esone. Regolatori dello splicing come SR (serine-arginine rich) e altre proteine si legano all'ESE reclutando snRNP U1 (small nuclear RiboNucleoProtein, complessi ribonucleoproteici) e U2AF (fattore ausiliario a U2) al sito di splicing al 3', che poi recluta U2 snRNP al punto di ramificazione
- **Modello Intron Definition** -> Le sequenze ISR (Intronic Splicing Regulator) vengono riconosciute dai regolatori di splicing, che reclutano snRNP U1 e U2AF al 5' e 3'.
![[Pasted image 20260418170628.png]]
