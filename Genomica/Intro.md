
# Table of Contents

1.  [Alignment](#orgc80df23):ATTACH:
    1.  [Matrici](#orge6ddc69)
        1.  [PAM](#orga167dc4)
        2.  [BLOSUM](#org12d935e)
    2.  [DotPlot](#org765a67e)
    3.  [Tipologie di Allineamento](#orgfa11368)
        1.  [Needleman-Wunsch](#orgedbe2d3)
        2.  [Smith -Waterman](#org71afa2b)



<a id="orgc80df23"></a>

# Alignment     :ATTACH:

Allineare le sequenze è importante per ottenere una comparazione diretta, oltre ad essere prerequisito per analisi più complesse contro database or per la costruzione di alberi filogenetici o identificazione di motivi funzionali
**Omologia** -> Due entità condividono la stessa origina filogenetica, da cui si sono evoluti, differenziandosi dalle altre -> **Qualitativa**
**Similarità** -> Il termine similarità ha un significato generale, utilizzato a prescindere dalla motivazione. La similarità biologica può essere dovuta ad omologia ma anche dovuta al caso, o da fenomeni di convergenza adattiva -> **Quantitative**

-   Ortologhi -> Speciazione
-   Parologhi -> Duplicazione
-   Xenologhi -> trasferimento orizzontale
    ****BioMart**** -> Raccoglimento di ortologhi e parologhi di un gene

![img](/home/patrick/org/.attach/7f/3e9447-83b3-488d-a0b9-d68f3a5d5a42/Screenshot from 2026-04-14 17-11-14.png)
**Gap Opening** -> Si apre un gap assegnando uno score negativo, la cui estensione comporta ulteriore penalità


<a id="orge6ddc69"></a>

## Matrici

1.  Identità
2.  Genetic-Code
3.  Matrice delle proprietà chimiche
4.  Matrici Empiriche
    1.  PAM
        1.  BLOSUM
            1.  Gonnet

PAM e BLOSUM si basano sulle frequenze osservate di specifiche sostituzioni amminoacidiche. La similarità tra due amminoacidi è proporzionale alla loro frequenza di sostituzione osservata.
Queste matrici si basano su evidenze biologiche, le cui differenze osservata tra sequenze omologhe negli allineamenti è dovuta solo a eventi di mutazione. Alcune di queste mutazioni hanno effetti minimi o assenti nella struttura/funzione delle proteine.

La scelta di una delle matrici è cruciale per ottenere buoni risultati.
Per sequenze meno divergenti, BLOSUM80 e PAM1 sono le migliori. BLOSUM62 e PAM120 per mediamente divergenti. BLOSUM45 e PAM250 per sequenze molto divergenti.


<a id="orga167dc4"></a>

### PAM

L'idea base delle matrici PAM nasce da studi di filogenetica molecolare su 71 famiglie di proteine con un minimo di 85% di similarità. L'assunzione di partenza è che analizzando sequenze filogeneticamente associate è possibile calcolare la percentuale di mutazioni accettate. Una unità di PAM è definita come l'1% di cambiamento di posizione di un amminoacido, cioè una sostituzione ogni 100 amminoacidi.
Si è partiti ricostruendo la sequenza ancestrale partendo da allineamento multiplo tra proteine con similarità elevata >85%.
Le sostituzioni &ldquo;accettate&rdquo; sono riportate su una matrice da cui è possibile ottenere la mutabilità relativa ($m_i$) del residuo i.
Per ogni amminoacido è quindi possibile valutare la possibilità di cambiamento.
Una volta definita la mutabilità, la domanda da porsi è qual è la probabilità che sia cambiato in j.
$$M_{ij} = m_i \cdot \frac{f_{ij}}{f_i} = \frac{f_{ij}}{f_i} \cdot \frac{f_i}{100 \cdot fp_i} = \frac{f_{ij}}{100 \cdot fp_i}$$
La probabilità che il residui i non cambi è $1-M<sub>ij</sub>$<sub>nil</sub>.
La probabilità di una mutazione dipende dal tempo trascorso dalla divergenza delle sequenze. I valori sono normalizzati per il tempo necessario ad introdurre 1 mutazione ogni 100 residui (distanza = 1PAM).
Matrici PAM con indice maggiore di 1 si ottengono moltiplicando la matrice PAM per se stessa k volte, PAM2 = PAM1 x PAM1
Le Matrici PAM si dividono in

-   Scoring
-   Substitution

Le matrici di scoring utilizzate dai programmi di allineamento sono calcolate dalle matrici di sostituzione come:
$$s(a,b) = int(10\cdot log{\frac{M(a,b)} {C(a,b)}})$$
Dove

-   s(a,b) -> score per una coppia di amminoacidi
-   M(a,b) -> probabilità di sostituzione di un amminoacido
-   C(a,b) -> probabilità di una sostituzione di un amminoacido

Il rapporto $\frac{M(a,b)}{C(a,b)}$  indica quante volte la probabilità di omologia è maggiore della probabilità casuale.


<a id="org12d935e"></a>

### BLOSUM

Le matrici BLOSUM si basano sul BLOCKS database, il quale mantiene blocchi di sequenze relazionate tra loro con un definito valore di identità amminoacidica, generalmente tra il 30% ed il 95%. A partire da ogni blocco è possibile calcolare la frequenza di sostituzione osservata e la probabilità di accoppiamento casuale
$$s(a,b) = int(10\cdot log{\frac{M(a,b)} {C(a,b)}})$$
In questo caso $M(a,b)$ si riferisce alla probabilità di sostituzione osservata per ogni blocco.

-   Per ogni allineamento nel database BLOCKS le sequenze sono raggruppate in cluster con almeno il 50% (per BLOSUM50, altrimenti 80% per BLOSUM80 ecc&hellip;) di residui identici
-   Tutte le coppie di sequenze sono comparate, e la frequenza delle coppie osservata vengono annotate
-   La frequenza attesa delle singole coppie vengono computate dalle singole frequenze amminoacidiche $$f_{A,C} = f_A \cdot f_C$$
    -   Per ogni coppia di amminoacidi lo score di sostituzione viene computato essenzialmente con $s(a,b)$.


<a id="org765a67e"></a>

## DotPlot     :ATTACH:

Il dotplot aiuta a ispezionare la relazione tra due sequenze. Aiuta ad identificare potenzialmente regioni conservate. Si ottiene in 4 maniere:

-   Diagonalmente attraverso i dot -> Match
-   Diagonalmente attraverso celle vuote -> Mismatch
-   Orizzontalmente -> Gap
-   Verticalmente -> Gap

L'allineamento viene effettuato muovendosi lungo la matrice maniera tale da utilizzare le diagonali con i punti più grandi. Questo massimizza il numero di match.
Il metodo DotPlot si utilizza sia su sequenze nucleotidiche sia su sequenze proteiche.
Poichè all'aumentare della lunghezza della sequenza aumentano anche i match spuri e quindi anche il rumore di fondo, i parametri del window size e della stringency aiutano a visualizzare meglio.
![img](/home/patrick/org/.attach/7f/3e9447-83b3-488d-a0b9-d68f3a5d5a42/Screenshot from 2026-04-15 16-21-31.png)


<a id="orgfa11368"></a>

## Tipologie di Allineamento

-   **Globale** -> L'allineamento globale tiene conto della similarità tra sequenze per l'intera lunghezza (Query Coverage 100% sempre)
-   **Locale** -> L'allineamento locale tiene conto della similarità tra sequenze soltanto per specifiche regioni simile tra parti della sequenza in analisi (Cambia il Query Coverage)

Importante considerare che **lo score di allineamento più elevato non significa necessariamente che sia biologicamente significativo rispetto ad un altro allineamento con score inferiore**.
Il tipo di allineamento (globale o locale) dipende strettamente dal caso in studio. A volte è meglio un allineamento locale, altre volte uno globale.
Considerando che il numero di allineamenti cresce al crescere della lunghezza delle sequenze, tecniche di programmazione come il dynamic programming vengono utilizzate per esplorare le possibili soluzioni al problema in un tempo ragionevole.
L'algoritmo globale **Needleman-Wunsch** e quello locale **Smith-Waterman** utilizzano questa tecnica.


<a id="orgedbe2d3"></a>

### Needleman-Wunsch

L'algoritmo di Needleman-Wunsch può essere riassunto in 3 step principali:

1.  Riempimento della matrice
2.  Calcolo dello score
3.  Allineamento

Le sequenze compongono la matrice principale e le regole di composizione sono uguali a quelle del DotPlot.
Ogni punto della matrice può essere raggiunto da 3 possibili posizioni. Si sceglie quello con lo score più elevato tra le 3 possibilità per ottenere il best alignment score per uno specifico punto.


<a id="org71afa2b"></a>

### Smith -Waterman

La Smith-Waterman la si può ottenere modificando la formula introducendo lo 0 cosiì da non avere score negativi.
L'allineamento si ricostruisce dal valore più elevato e l'allineamento termina allo 0.
Lo score sarà infatti pari al massimo tra score(x,y-1) - gap<sub>penalty</sub>, score(x-1, y-1) + substitution-score(x,y), score (x-1, y) - gap-penalty
In principio l'allineamento locale è utile per cercare similarità in un databse. Smith-Waterman è troppo lento però per identificare regioni simili ad una query in database molto grandi. L'algoritmo Smith-Waterman genera allineamenti ottimali ed esaustivi unicamente.
Per la ricerca su database si utilizzano algoritmi più complessi quali FASTA e BLAST.

