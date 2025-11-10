# 🧬 MACS2 Peak Calling

**MACS2 (Model-based Analysis for ChIP-Seq)** is a popular bioinformatics tool used to identify **peaks** — regions of the genome where proteins (like transcription factors or histone marks) are **enriched in ChIP-seq data**.

---

## 📈 What is “Peak Calling”?

In ChIP-seq (Chromatin Immunoprecipitation followed by sequencing), you sequence DNA fragments that were bound by a protein of interest.  
The result: **millions of short reads** aligned to the genome.

But not all regions are equally bound — some areas have **many reads piled up** (meaning the protein binds there), while others have few or none.

**Peak calling** = finding those **enriched regions (peaks)** that stand out from background noise.

---

## ⚙️ What MACS2 Does

MACS2 processes your aligned reads (from a `.bam` file) and uses statistical modeling to identify peaks.

1. **Input data:**
   - Experimental ChIP-seq sample (`-t sample.bam`)
   - Optional control (input DNA) sample (`-c control.bam`) → helps MACS2 estimate background noise.

2. **Statistical modeling:**
   - Models read distribution using a **Poisson** or **dynamic local lambda** model.
   - Estimates **fragment length (d)** and **shift size**.

3. **Peak detection:**
   - Finds regions with **significantly more reads** than expected by chance.
   - Reports peaks with **p-value**, **q-value (FDR)**, and **fold enrichment**.

---

## 🧩 Basic Command

```bash
macs2 callpeak -t ChIP.bam -c Input.bam -f BAM -g hs -n sample_name --outdir peaks/

```

# 🔁 Bidirectional Enhancers

**Bidirectional enhancers** are regulatory DNA elements that can **activate transcription in both directions**, enhancing transcription of genes (or noncoding RNAs) located on **either side**.

---

## 🧬 1. What Is an Enhancer?

An **enhancer** is a DNA region that increases transcription of a gene, often by recruiting transcription factors (TFs) and coactivators like **Mediator** or **p300**.  
Enhancers can act:
- Upstream or downstream of a gene,  
- Far away (thousands of base pairs),  
- In either orientation.

---

## 🔁 2. What Makes an Enhancer *Bidirectional*?

A **bidirectional enhancer** shows **balanced transcription initiation** in both directions from a central point — generating **two short, unstable eRNAs (enhancer RNAs)** going opposite ways.

These **eRNAs**:
- Are **noncoding** and **unstable**,
- Are markers of **active enhancer function**,
- Are **transcribed symmetrically** on both DNA strands.

🧩 **Bidirectional enhancers = active enhancers with divergent eRNA transcription.**

---

## 🔬 3. How They’re Detected Experimentally

| Technique | Detects | Bidirectional Enhancer Signal |
|------------|----------|-------------------------------|
| **CAGE** | 5′ RNA ends | Two opposing peaks |
| **GRO-seq / PRO-seq** | Nascent RNA | Divergent short transcripts |
| **ChIP-seq (H3K27ac, H3K4me1)** | Histone marks | High enrichment |
| **ATAC-seq / DNase-seq** | Open chromatin | Nucleosome depletion center |

Enhancers are typically defined by **bidirectional eRNA transcription + enhancer histone marks (H3K4me1, H3K27ac)**.

---

## 🧭 4. Biological Role

Bidirectional enhancers:
- Mark **active enhancer regions**,
- Promote **enhancer–promoter looping**,
- Fine-tune **gene expression**.

**eRNAs** may:
- Recruit **Mediator/BRD4**,  
- Stabilize **DNA loops**,  
- Regulate **Pol II pausing/release**.

---

## 🧠 5. Example (Human Genome)

At enhancer regions controlling genes like **MYC** or **IFNB1**, we see:
- H3K27ac / H3K4me1 enrichment,
- Strong **bidirectional eRNA transcription** (in GRO-seq),
- Physical contact with promoter (Hi-C / 3C).

---

## 🧰 6. Computational Identification

Integrate:

```text
GRO-seq signal → divergent transcription
+ H3K27ac ChIP-seq → enhancer mark
+ ATAC-seq / DNase-seq → open chromatin
  ```



![[Screenshot 2025-10-15 at 09.28.44 2.png]]

- In Enhancer, la striscia stretta indica che c'è un promotore, linea non in grassetto = non trascritto
- Da qui si vede che p53 lega enhancer in maniera statisticamente significativa in questo caso



### Odd Ratio
prodotto delle diagonali delle tabelle di contingenza.
Se il prodotto è compreso tra 0 e 1 l'associazione è negativa, >1 positiva
Marginali -> somma delle caselle della tabella di contingenza


# 🔢 Fisher’s Exact Test in R

```r
# Define counts
a <- 62240
b <- 12013797
c <- 1822408
d <- 2723880833

# Create a 2x2 contingency table
cont_table <- matrix(c(a, b, c, d), ncol = 2, nrow = 2, byrow = TRUE)

# View the table
cont_table

fisher.test(cont_table)
-----
Error in fisher.test(cont_table) : 
  'x' has entries too large to be integer
-----


chisq.test(cont_table)
-----
	Pearson's Chi-squared test with Yates' continuity correction

data:  cont_table
X-squared = 351615, df = 1, p-value < 2.2e-16
-----
```


Stima di regioni non a e non b dell'implementazione di Fisher di Bedtools:
- Nr. di overlap ridondante
- Distribuzione Ipergeometrica
	- Serie di operazioni in più 

```
# Number of query intervals: 8636
# Number of db intervals: 44459
# Number of overlaps: 660
# Number of possible intervals (estimated): 5452881
# phyper(660 - 1, 8636, 5452881 - 8636, 44459, lower.tail=F)
# Contingency Table Of Counts
#_________________________________________
#           |  in -b       | not in -b    |
#     in -a | 660          | 7976         |
# not in -a | 43799        | 5400446      |
#_________________________________________
# p-values for fisher's exact test
left	right	two-tail	ratio
1	0	0	10.203
```
p-value per $\alpha$ a destra, sinistra, doppio intervallo (sinistra / destra), odd-ratio
p-value per intervallo di confidenza unilaterale o bilaterale
arricchimento della sequenza di legame di p53 e di CTCF per le regioni in overlap che legano sia p53 sia CTCF.



