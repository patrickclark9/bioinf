

# Strategies
## Clone-by-Clone Vector

La strategia Clone-by-Clone Vector è una strategia di physical mapping, dove vengono prodotti serie di cloni (contig) in overlap, ognuno dei quali controlla una lunga, contigua regione del genoma di partenza.
Per la strategia shotgun, ogni clone mappato è subclonato in librerie più piccole, dalle quali si ottengono casualmente read delle sequenze.
Nel caso di BAC, tipicamente richiede la generazione di diverse migliaia di read per clone.
Il dataset risultante di sequenze viene poi utilizzato per assemblare la completa sequenza del clone.

Il sistema BAC utilizza il fattore di fertilità circolare F di E.coli che può stabilmente trasportare frammenti di DNA di dimensioni elevate >300Kb.
Il vettore BAC si basa su un plasmide mini-F, che mantiene il clone BAC in singola copia o con copy number molto basso per cellula batterica, riducendo il numero di eventi di ricombinazione in elementi genomici virali e incrementando la stabilità del genoma clonato.

Il vettore P1 per l'introduzione di DNA ricombinante in E.coli tramite tecniche di elettroporazione deriva dal batteriofago P1.
P1-derived Chromosomes (PAC) possono trasportare pezzi di DNA con una dimensione di inserzione di 130-150Kb.

### Minimal Tiling Path
Il più piccolo numero di cloni che coprono l'intera regione d'interesse/cromosoma rappresentata dalla mappa fisica è chiama Minimum Tiling Path.
La determinazione del più piccolo set di cloni che copre una intera regione è cruciale nel Clone-by-Clone (hierarchical). 
In questo protocollo, prima si costruisce la mappa fisica, poi i cloni nel MTP vengono sequenziati uno a uno.
Questa strategia è stata usata per sequenziare il genoma di A.thaliana, H.sapiens e altri.
Ultimamente in Whole-Genome Shotgun si utilizza un MTP derivato da una mappa fisica per validare e migliorare la qualità dall'assemblaggio.

#### Marker e Mappe
Un marker è un sito unico nel genoma, tipicamente una sequenza. I marker sono utilizzati nella costruzione delle mappe.
Una mappa fornisce una guida per esperimenti di sequenziamento mostrando le posizioni dei marker genomici (geni e altro).

Per convenzione si dividono i metodi di mapping del genoma in 2 categorie:
- Genetic Mapping -> Si basa sull'utilizzo di tecniche genetiche per costruire mappe che mostrano la posizione dei geni ed altre sequenze sul genoma. Le tecniche genetiche includono cross-breeding, o l'esaminazione delle genealogie (pedigree) per gli umani.
- Physical Mapping -> Tecniche di biologia molecolare per esaminare le molecole di DNA direttamente per costruire mappe mostrando le posizioni di sequenze, inclusi geni
###  Genetic mapping
Una mappa genetica (linkage map) mostra la locazione relativa dei marker genetici (riflettendo siti di varianti genomiche) su un cromosoma.
Si basa sul linkage genetico -> Più vicini due marker sono su un cromosoma, più tenderanno a segregare insieme.
Studiando i pattern di ereditarietà possono essere stabiliti l'ordine relativo e la locazione dei marker genetici lungo un cromosoma.
I geni sono marker genetici, ma non sono ideali per il mapping. In genomi grandi, una mappa basata solo sui geni non sarà molto dettagliata. Inoltre nei genomi eucari