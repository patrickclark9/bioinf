Capitolo 11

**Quantitative genetics** is a branch of population genetics that deals with the inheritance of traits that are not discrete (like Mendel's pea colors) but are continuous in their variation. These are known as **quantitative traits** or complex traits.

### Key Concepts

1. **Quantitative Traits:**
    
    - These traits exhibit a continuous range of phenotypes, such as height, weight, skin color, blood pressure, or crop yield.
    - The variation is typically represented by a bell curve (normal distribution).
2. **Polygenic Inheritance:**
    
    - Quantitative traits are influenced by multiple genes, often called **polygenes** or **quantitative trait loci (QTLs)**.
    - Each gene contributes a small, additive effect to the overall phenotype.
3. **Environmental Influence:**
    
    - The final phenotype is a result of the interaction between an individual's genotype and the environment.
    - The fundamental equation in quantitative genetics is:  
          
        where:
        -  is the phenotypic value
        -  is the genotypic value
        -  is the environmental effect
4. **Phenotypic Variance ():**
    
    - The total observed variation in a trait within a population is called phenotypic variance.
    - It can be partitioned into genetic variance and environmental variance:  
          
        where:
        -  is the total phenotypic variance.
        -  is the genetic variance (variation due to differences in genotypes).
        -  is the environmental variance (variation due to environmental differences).
5. **Heritability ():**
    
    - Heritability is a key concept that measures the proportion of the total phenotypic variance () that is due to genetic variance ().
    - **Broad-sense heritability ()** is the ratio of total genetic variance to total phenotypic variance:  
        
    - **Narrow-sense heritability ()** is more commonly used, especially in breeding, as it only considers the additive genetic variance (), which is the portion of genetic variance that causes offspring to resemble their parents.  
        
    - Heritability is a population-specific measure and can change if the environment or the genetic makeup of the population changes. It does **not** indicate the degree to which a trait is genetically determined for an individual.

### Applications

- **Agriculture:** Used extensively in plant and animal breeding to select for desirable traits like increased milk production in cows, higher grain yield in crops, or faster growth rates in livestock.
- **Human Genetics and Medicine:** Helps in understanding the genetic basis of complex diseases such as diabetes, heart disease, and schizophrenia, and in assessing an individual's risk for these conditions.
- **Evolutionary Biology:** Used to study how natural selection acts on quantitative traits and how populations evolve over time.
### The Fundamental Mathematical Model

The starting point for the mathematics of quantitative genetics is partitioning the observed phenotype of an individual.

**1. Phenotypic Value (P):**  
The phenotype () is what we can measure (e.g., height, milk yield, weight). It is modeled as the sum of the genetic value () and the environmental effect ().

**2. Genetic Value (G):**  
The genetic value is not a single component. It is further broken down based on how genes act and combine. This is the most critical part for understanding breeding value.

Where:

- **A = Additive Genetic Value:** This is the sum of the individual effects of all alleles that influence the trait. These effects are "additive" because they simply add up, regardless of what other alleles are present. This is the component that is reliably passed from parent to offspring.
- **D = Dominance Deviation:** This component arises from the interaction between alleles _at the same locus_. For example, in a heterozygous individual (Aa), the phenotype might not be exactly halfway between the AA and aa phenotypes due to dominance. This effect is not passed on predictably, as a parent only passes on one allele, not its diploid combination.
- **I = Epistatic Deviation (or Interaction):** This component arises from interactions between alleles _at different loci_. For example, a gene at one locus might mask or modify the effect of a gene at another locus. Like dominance, this is not predictably inherited.

So, the full model for an individual's phenotype is:

### Population-Level Mathematics: Variance

While the equation above applies to an individual, quantitative genetics is primarily concerned with the variation _within a population_. We therefore shift from individual values to population variances.

And the genetic variance () is partitioned similarly to the genetic value:

Where:

-  = Total phenotypic variance in the population.
-  = **Additive genetic variance**. The variance due to the additive effects of alleles.
-  = Dominance variance.
-  = Epistatic (interaction) variance.

### Breeding Value (BV)

The **Breeding Value (BV)** of an individual is formally defined as its **Additive Genetic Value (A)**.

**BV = A**

**Why is only the additive part the breeding value?**  
Because an individual passes on its _alleles_, not its _genotypes_, to its offspring. Dominance and epistatic effects are results of specific combinations of alleles (genotypes). These combinations are broken down during meiosis and reformed in the offspring. The only thing that is reliably transmitted is the collection of individual alleles, whose effects are additive.

Therefore, the breeding value represents the part of an individual's genetic merit that can be passed on to its progeny and cause them to resemble the parent.

#### Mathematical Calculation of Breeding Value

Let's consider a single gene with two alleles,  and , with frequencies  and  respectively. We can assign genotypic values like this:

|Genotype|Genotypic Value (G)|
|:--|:--|
||+a|
||d|
||-a|

The population mean () is .

The **average effect of an allele** is the average deviation from the population mean for individuals who receive that allele from a parent. The average effect of substituting a  allele for a  allele is denoted by .

The breeding values for each genotype are then calculated based on the number of  and  alleles they have:

|Genotype|Genotypic Value (G)|Breeding Value (A)|Dominance Deviation (D = G - A)|
|:--|:--|:--|:--|
||+a|||
||d|||
||-a|||

**Key Insight:** The breeding value of a heterozygote () is exactly halfway between the breeding values of the two homozygotes ( and ). This is the essence of "additive" – there are no dominance interactions in the breeding value itself.

### Practical Application: The Breeder's Equation

The concept of breeding value is central to animal and plant breeding because it determines the response to selection. This is captured in the **Breeder's Equation**:

Where:

- **R = Response to selection:** The change in the population mean from one generation to the next.
    
- **S = Selection differential:** The difference between the mean of the selected parents and the mean of the original population.
    
-  **= Narrow-sense heritability:** This is the crucial link. It is defined as the ratio of additive genetic variance to the total phenotypic variance.
    

Essentially, narrow-sense heritability () tells us what proportion of the total observable variation is due to the additive genetic effects that can be passed on. It is the regression of Breeding Value on Phenotypic Value. A high  means that an individual's phenotype is a good predictor of its breeding value, and selection will be highly effective.