****- Genoma mitocondriale per la variazione nella popolazione femminile
- Cromosoma Y per variazione nel sesso maschile
- L'**aplotipo** (dal greco ἁπλόος contratto ἁπλοῦς haplóos=singolo o semplice) è un gruppo di varianti [alleliche](https://it.wikipedia.org/wiki/Allele "Allele"), lungo un [cromosoma](https://it.wikipedia.org/wiki/Cromosoma "Cromosoma") o un segmento cromosomico, che in genere vengono ereditati insieme. Per un'altra definizione l'aplotipo è un insieme di [marcatori genetici](https://it.wikipedia.org/wiki/Marcatori_genetici "Marcatori genetici") presenti su un singolo cromosoma, che vengono ereditati insieme; i marcatori possono essere un gruppo di varianti alleliche, un gruppo di [STR](https://it.wikipedia.org/wiki/Microsatelliti "Microsatelliti"), o un gruppo di [SNP](https://it.wikipedia.org/wiki/Polimorfismo_a_singolo_nucleotide "Polimorfismo a singolo nucleotide")

- Intolleranza al lattosio: può essere derivata dal silenziamento, o dal danneggiamento all'intestino (esempio) (alcool), quindi la lattasi viene sintetizzata ma non in quantità abbondanti e non nei compartimenti corretti dell'intestino
- Microsatelliti hanno molte copie di una stessa variante allelica
- Si definiscono **microsatelliti** (o _**Short Tandem Repeats**_ o **STR**, conosciuti anche come _**Simple Sequence Repeats**_ o **SSR**, o come _**Short Tandem Repeat Polymorphism**_ o **STRP**) [sequenze ripetute](https://it.wikipedia.org/wiki/Sequenze_ripetute "Sequenze ripetute") di [DNA non codificante](https://it.wikipedia.org/wiki/DNA_non_codificante "DNA non codificante") costituiti da unità di ripetizione molto corte (1-5 bp) disposte secondo una [ripetizione in tandem](https://it.wikipedia.org/wiki/Ripetizione_in_tandem "Ripetizione in tandem"), utilizzabili come marcatori molecolari di [loci](https://it.wikipedia.org/wiki/Locus_\(genetica\) "Locus (genetica)"). La loro presenza nel [genoma umano](https://it.wikipedia.org/wiki/Genoma_umano "Genoma umano") non influisce per più del 3%, ma si pensa che comunque essi svolgano una funzione essenziale per la struttura dei [cromosomi](https://it.wikipedia.org/wiki/Cromosomi "Cromosomi").
- Microsatelliti ultime 8 generazione (25 anni per generazione)
- Accumulo di mutazioni negli spermatozoi dato che si dividono, mentre gli ovociti sono fissi dalla nascita
- Segmento duplicato per duplicazione può evolvere in nuove funzioni
- Tante Copy Number Variation nel genoma
- Il mapping delle short reads portava similarità schimpanzè umano al 99%
- Usando long reads, la percentuale scende, le copy number variations non si allineano tutte su uno stesso gene (come con le short reads), ma si allinea solo una copia, riducendo la similarità
- Copie di geni, delezioni, mutazioni aumentano la disparità

- Mutazione forza creatrice di diversità
- Ricombinazione forza mescolatrice
- Vicino ai centromeri non ricombinano

- Mutazione o si fissa o viene persa per deriva genetica
- Deriva genetica cancella varietà esistente
- Fitness del gene: Codominanza, OverDominance, Underdominance, simple negative/positive selection basata sull'allele

- Coefficiente s della fitness impatto sulla fitness di omozigosi dominante / omozigosi recessiva / eterozigosi
- Dal sequenziamento, se equilibrio di hardy weinberg non viene rispettato, ovvero si ha una deviazione significativa rispetto alla regola, allora il frammento viene eliminato

- **Coefficiente di Inbreeding**: $\frac{2fAfa-fAa}{2fAfa}$
	- Stima di Eterozigoti $fAa = 2fAfa(1-F)$ oppure $1-\frac{H_{Osservata}}{H_{Atteso}}$


- **Deriva Genetica**-> Variazione delle frequenze alleliche dovuta al caso, con fine ultimo molto probabilmente la perdita di un allele (carattere). Genetic Drift avviene su tutto il genoma. Non ha una direzione verso un allele o un altro. Influenzata dalla taglia della popolazione. Riduzione di diversità. A causa della deriva genetica, un allele viene fissato o viene eliminato prima o poi.
	- La selezione è specifica per un gene (il resto segue altre leggi casuali)
	- Si cercano loci outlier rispetto al genoma per la selezione
	- Modello Wright-Fisher:
		- Popolazione Aploide
		- Generazioni discrete
		- Approssimabile per sistemi biallelici
		- Frequenza di A in Generazione T rimane della stessa frequenza
			- 60/40 gen 1 -> 60/40 gen 2 -> 60/40 gen 3 .....
		- Col tempo le frequenze alleliche possono cambiare a causa del drift
		- Effective population Size: Insieme di individui che modellano la popolazione reale
		- Se un allele sparisce, sparisce fondamentalmente per sempre -> Mutazioni troppo rare per compensare la deriva genetica
		- Ne (Effective population size) -> Modello generale, N si può comportare come Ne.
			- Una popolazione Census di 1000 si può comportare come come una popolazione effective di 100
			- Tipicamente per homo sapiens Ne (effective) = 1/3 di N (census)
		- **Casi Particolari di Deriva Genetica**:
			- Bottleneck -> Riduzione della popolazione, la popolazione ricresce, ma la variabilità non torna facilmente, e viene persa
			- Effetto Fondatore -> Piccola popolazione colonizza una nuova area, la variabilità rimane bassa
		- Negli umani, l'effetto della selezione non è stato probabilmente molto ampio, ha avuto più effetto la deriva
		- In casi in cui la popolazione è molto piccola, ha subito effetto fondatore, la deriva è molto più forte della selezione, e quindi l'effetto della selezione viene annullata, poichè le fluttuazioni sono troppo elevate perchè la selezione abbia effetto
	- $\frac{1}{2N}$ che un allele venga fissato. Se la popolazione è finita, prima o poi uno degli alleli, anche se sono numerosi, verrà fissato.
	- Tasso di sostituzione e divergenza di specie:
		- $2N\mu \cdot \frac{1}{2N} = \mu$ | Numero atteso di mutazioni che verrà fissato ad ogni generazione
		- 2 N è 2N poiche 1N va verso homo sapiens, 1N va verso scimpanzè
			- Divergenza di Specie


## Coalescenza
- Si ritorna indietro, fino a trovare un ancestore comune.
	- Il risultato è un unico individuo, l'ancestore comune
	- ![[Screenshot 2025-11-03 at 11.31.29.png]]
	- $\frac{1}{2N}$ la probabilità che abbiano un ancestore comune nella generazione immediatamente precedente
	- Una generazione = $2N$. $N$ Generazioni $2N \cdot N$ 

 The theory's logic is based on tracing the **genealogy of genes** (or "gene trees"), not the genealogy of individuals.

1. **Working Backward:** Imagine you have a sample of gene copies from a population. In the generation immediately before, some of those copies might have come from the same "parent" gene. If you keep tracing these lineages backward, they will randomly merge one by one.
    
2. **Coalescent Events:** Each time two lineages merge into a common ancestor, it's called a **coalescent event**.
    
3. **The MRCA:** This process continues until all lineages in the sample have merged into the single MRCA.
    
4. **Influence of Population Size:** The rate at which these events happen depends heavily on the **effective population size (Ne​)**.
    
    - In a **small population**, lineages find a common ancestor relatively quickly just by chance. The time to the MRCA is shorter.
        
    - In a **large population**, lineages are more likely to come from distinct parents each generation, so it takes much longer for them to coalesce. The time to the MRCA is longer.
        

The probability that any two lineages coalesce in a single preceding generation (in a simple, idealized population) is 1/(2Ne​).

---

## 🔑 Key Concepts

Coalescent theory connects several key genetic concepts:

### Gene Genealogy (Gene Tree)

This is the branching, tree-like diagram that represents the ancestral relationships of the gene copies in your sample. It shows which lineages coalesced and when. The specific shape and branch lengths of this tree are the random outcome of genetic drift over time.

### Time to Most Recent Common Ancestor (TMRCA)

This is the total time (usually in generations) from the present-day sample back to the single ancestral gene copy from which all others are descended. Scientists can estimate the TMRCA by:

- **Counting Mutations:** Assuming mutations occur at a relatively constant rate (the "molecular clock"), the number of genetic differences (mutations) between two sequences is proportional to the time they have been evolving separately. More differences imply a more ancient TMRCA.
    
- **Using Population Size:** The TMRCA is statistically dependent on the effective population size (Ne​).
    

### Effective Population Size (Ne​)

This is one of the most important parameters in population genetics. It's not the same as the census (total) population. Instead, it's the size of an _ideal_ population (with random mating, etc.) that would experience the same amount of genetic drift as the _real_ population. Coalescent theory provides the main framework for **estimating Ne​ from genetic data**.

---

In large population ($N\rightarrow \infty$), the probability of not finding a common ancestor in 2Nt generations is: $e^{-t}$ an exponential distribution.
$r = 2Nt$, $r$ nr of generations.

For $N$ generations, we exprect $\Theta = 4N\mu$ number of mutations separating 2 gene copies.

For a lineage of length $t$ we expect $2N\mu t$ mutations. If sample size = 2, then $4N\mu t$.
Because the expected coealescence time is 1, the number of mutations separating two gene copies is $4N\mu \rightarrow \Theta$. $\Theta$ is the difference between two individuals

The more the differences, the larger the distance of two individuals from MRCA (Most Recent Common Ancestor).

$4N\mu$ is also the difference between individuals. The difference between two individuals because its the number of differences starting from MRCA between two individuals.
**IMPORTANTE QUESTO CAPITOLO**

Nr of mutations in an entire lineage is $\frac{\Theta}{2} \cdot t$
**Infinite Site Models**
**Tajima estimators**
n(n-1)/2 -> n(n-1) rimuove la diagonale della matrice. Tra le due triangolari ne serve solo una, o superiore o inferiore. Quindi viene diviso per due.
[[General Coalescence]]




