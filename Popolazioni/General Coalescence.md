# Population Genetics: A Coalescent Perspective

This document provides an overview of coalescent theory, its behavior in large populations, and the infinite alleles model used to understand genetic variation.

---

## 🧭 Coalescent Theory: Working Backward

**Coalescent genetics** is a core framework in population genetics that models the ancestry of genes by looking **backward in time**. Instead of simulating forward, it traces all the different versions (alleles) of a gene in a sample back to the single ancestral copy they all share.

* **Coalescent Event:** The moment when two ancestral gene lineages merge into a common ancestor.
* **Most Recent Common Ancestor (MRCA):** The single ancestral gene copy from which all gene copies in the sample are descended. The time to this point is the **TMRCA**.



The rate of these events is critically dependent on the **effective population size ($N_e$)**.

### 🌳 Coalescence in Large Populations

The rate at which lineages coalesce is **inversely proportional** to the effective population size. In a large population, the process is significantly slower.

This has two primary consequences:

1.  **Deeper Time to MRCA:** Because the probability of any two genes sharing a parent in the previous generation is very low, it takes **much longer** for lineages to find each other and merge. The gene genealogy stretches much further back in time.
2.  **Greater Genetic Diversity:** This "deeper time" provides a larger window for mutations to occur and accumulate. Since lineages remain distinct for many generations, they acquire their own unique mutations, leading to a **higher level of genetic polymorphism** (e.g., more SNPs) in the population.

This process can be visualized by comparing the gene trees of different population sizes:

* **Small Population:** The tree is "shallow" with short branches. Coalescent events happen quickly and recently.
* **Large Population:** The tree is "deep" with long branches. Coalescent events are rare and happen far in the past.

---

## 🧬 Modeling Mutation: The Infinite Alleles Model (IAM)

The **infinite alleles model (IAM)** is a mathematical model used to describe the equilibrium level of genetic variation in a population.

Its central assumption is that **every new mutation creates a completely novel allele** that has never existed before. This is a reasonable assumption for large genes, where the number of possible unique sequences is astronomically high.

The IAM describes the balance between two opposing forces:
* **Genetic Drift:** Removes variation by causing alleles to be lost by chance.
* **Mutation:** Introduces new, unique variation.

### Key Formulas

At equilibrium, the balance between these forces leads to a stable level of homozygosity ($F$)—the probability that two randomly sampled alleles are identical.

The equilibrium homozygosity is:
$$F = \frac{1}{1 + 4N_e\mu}$$

This is more simply written using the **population mutation parameter ($\theta$)**:
$$\theta = 4N_e\mu$$
$$F = \frac{1}{1 + \theta}$$

Where:
* **$N_e$** = Effective population size
* **$\mu$** = Mutation rate per gene per generation
* **$\theta$** = A measure of the population's capacity to harbor neutral genetic variation.

Conversely, the **expected heterozygosity ($H$)**, or the probability of sampling two *different* alleles, is:
$$H = 1 - F = \frac{\theta}{1 + \theta}$$

This equation links the observable genetic diversity ($H$) in a population directly to its effective size and mutation rate ($\theta$), forming a cornerstone of the **Neutral Theory of Molecular Evolution**.

## Singleton
Singleton -> Mutazione presente solo nelle foglie (rami esterni), e quindi su un singolo individuo (popolazione)

## Fst
$F_{st} = \frac{H_t - H_s}{H_t}$
Intervallo compreso tra 0,1 per questo valore. Tanto più è basso Fst, tanto minore sono le differenze dovuta al raggruppamento.
Fst = 0.04, solo il 4% della differenza è dovuta alla separazione tra gruppi.