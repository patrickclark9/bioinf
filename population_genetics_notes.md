# Population Genetics Notes

---

## Q: Wright Fisher model how does it work

# The Wright-Fisher Model

It's a foundational model in population genetics that describes how **allele frequencies change from generation to generation** due to random chance alone — a process called **genetic drift**.

## Core Idea

Imagine a population of exactly **N diploid individuals** (so 2N gene copies at any locus). Each new generation is formed by randomly sampling 2N alleles from the current generation, **with replacement**. That's it. No selection, no mutation, no migration — just chance.

## The Sampling Step

If the current frequency of allele A is *p*, then the number of A copies in the next generation follows a **binomial distribution**:

> k ~ Binomial(2N, p)

The new frequency is k / 2N. Because this is random sampling, the frequency will **drift** up or down each generation, even if nothing biologically "causes" it.

## Key Properties

**Variance of frequency change per generation:**
> Var(Δp) = p(1−p) / 2N

This tells you two critical things:
- **Small N** → large variance → drift is strong, frequencies bounce around a lot
- **Large N** → small variance → drift is weak, frequencies change slowly

**Expected frequency** stays the same: E[p′] = p. Drift has no direction, it's just noise.

## What Happens Over Time

- Allele frequencies perform a **random walk** bounded between 0 and 1
- Eventually every allele either **fixes** (reaches frequency 1.0) or is **lost** (reaches 0.0) — these are absorbing states
- The probability that allele A eventually fixes is exactly its current frequency *p*
- The expected time to fixation is on the order of **4N generations**

## Why It Matters for Your Data

Looking at your PLINK output, the Wright-Fisher model directly explains:

- **MAC = 0 in CDX, CEU, CHB** — the A allele may have been present ancestrally but was lost by drift in those populations
- **Different MAFs across populations (ACB ~7.9%, ASW ~6.8%)** — populations that diverged from a common ancestor will have drifted to different frequencies
- **NCHROBS = 2 in CHD** — with only 1 individual, you're sampling so few chromosomes that your estimate of population frequency is extremely unreliable, which is itself a manifestation of the same sampling logic

## Limitations

The model assumes:
- **Constant population size** (never true in reality)
- **Discrete, non-overlapping generations**
- **Random mating** (panmixia)
- **No selection, mutation, or migration**

Extensions like the **coalescent**, **diffusion approximations**, and **structured population models** build on Wright-Fisher to relax these assumptions — which is exactly what tools like PLINK's stratified frequency analysis are accounting for when they compute MAF per population separately.

---

## Q: How does coalescent extend Wright Fisher

# The Coalescent as an Extension of Wright-Fisher

## The Key Conceptual Flip

Wright-Fisher thinks **forward in time**: start with allele frequencies, sample the next generation, repeat.

The coalescent thinks **backward in time**: start with a sample of chromosomes today and ask *"when did these share a common ancestor?"*

These two frameworks describe the **same underlying process** — the coalescent is essentially the mathematical limit of Wright-Fisher when you look backwards.

---

## How the Connection Works

In Wright-Fisher, any two gene copies in generation *t* independently chose their parent in generation *t−1* uniformly at random from 2N chromosomes. The probability that two lineages **pick the same parent** (i.e. coalesce) is:

> P(coalescence in one generation) = 1 / 2N

This is small when N is large, so you can approximate the waiting time as an **exponential distribution**. For a sample of *k* lineages, the rate at which any pair coalesces is:

> Rate = C(k,2) / 2N = k(k−1) / 4N

This is Kingman's Coalescent (1982) — the formal limit of Wright-Fisher as N → ∞ with time rescaled in units of 2N generations.

---

## What the Coalescent Buys You

**1. It's computationally tractable**
Instead of simulating an entire population forward through time, you only simulate the ancestry of your *sample*. If you have 100 chromosomes, you track 100 lineages merging back to 1 — far cheaper than simulating millions of individuals.

**2. It produces a genealogical tree**
The output is a **gene tree** — a branching history of your sampled chromosomes. Each internal node is a coalescent event (a common ancestor). This tree has:
- **Branch lengths** proportional to time between coalescent events
- **Topology** reflecting the order ancestors were shared

**3. Mutations can be overlaid**
Under the infinite sites model, mutations fall on branches of the tree at rate θ = 4Nμ. The number of segregating sites in your sample, the site frequency spectrum, and patterns of LD all fall out naturally from the tree structure. This directly connects to what you see in your MAF data.

---

## Where Wright-Fisher Falls Short

| Problem | Wright-Fisher | Coalescent Solution |
|---|---|---|
| Only models whole populations | Needs to track all 2N copies | Only tracks sampled lineages |
| Hard to add population structure | Becomes intractable quickly | Add migration as lineages moving between populations |
| Ignores genealogical history | Frequencies only, no trees | Explicitly models ancestry |
| Statistical inference is hard | No natural likelihood | Tree topology gives a likelihood framework |

---

## Extensions the Coalescent Enables

**Population structure** — lineages can exist in different demes and migrate between them. Two lineages in different populations can only coalesce after they've migrated to the same population. This produces the **isolation-with-migration** models used to study exactly the kind of population differentiation you see in your ACB/ASW/CEU data.

**Changing population size** — if N changes over time, the coalescent rate changes accordingly. A **bottleneck** in the past means many lineages coalesce rapidly at that time point. This is the basis of methods like PSMC that reconstruct ancient population size history from a single genome.

**Recombination** — instead of a single tree, you get an **Ancestral Recombination Graph (ARG)**, where recombination events cause different parts of the chromosome to have different trees. This is what underlies modern haplotype-based methods.

**Natural selection** — under neutrality the coalescent works cleanly. Selection distorts the tree shape: positive selection creates very short, star-shaped trees (many lineages coalescing recently), while balancing selection creates unusually deep, old trees. Tests like Tajima's D are essentially asking whether your observed tree shape matches neutral coalescent expectations.

---

## Intuition for Your Population Data

When you see **MAF = 0 in CEU but ~8% in ACB** for the same SNP, the coalescent interpretation is:

- The mutation fell on a branch of the gene tree that is ancestral only to some African-ancestry lineages
- CEU lineages coalesced (found their common ancestor) before that branch existed, or the lineage carrying the mutation never migrated to that population
- The frequency difference reflects **how deep the split between populations is** and **how much drift has acted** since — both captured by the branch lengths in the coalescent tree

This is why tools like STRUCTURE, ADMIXTURE, and TreeMix are all ultimately coalescent-flavored: they're inferring the underlying genealogical process that produced the allele frequency patterns you're measuring with PLINK.

---

## Q: Molecular clock E[d]=2muts is the time wait to reach separation. What is ts

## The Molecular Clock and t_s

## The Basic Equation

$$E[d] = 2\mu t_s$$

where:
- **d** is the observed number of pairwise differences between two sequences
- **μ** is the mutation rate per site per generation
- **t_s** is what you're asking about

---

## What is t_s?

**t_s is the divergence/separation time** — the number of generations ago that two lineages split from their common ancestor.

The **factor of 2** is the key insight: after separation, mutations accumulate **independently on both lineages**. Each lineage accumulates μ mutations per generation, so together they accumulate 2μ differences per generation.

```
Ancestor
    |
    |← t_s generations
   / \
  /   \
Seq1  Seq2
```

Each branch contributes μt_s mutations, so total expected distance = **2μt_s**.

---

## Solving for t_s

$$t_s = \frac{E[d]}{2\mu}$$

You observe *d* (count the differences), you estimate μ from a known calibration point, and you recover the split time.

---

## The Coalescent Complication

This is where it connects to your earlier question. The molecular clock equation **looks simple but hides something**: two sequences sampled today don't just differ because of post-split mutations. Their total divergence is actually:

$$E[d] = 2\mu(t_s + t_{coal})$$

where **t_coal** is the additional coalescence time within the ancestral population before the split. Even if two populations split yesterday, their sampled chromosomes may trace back to a common ancestor that lived well before the split.

So naively applying the clock **overestimates t_s** unless you account for ancestral polymorphism — which is exactly what IMa, BEAST, and similar coalescent-based methods try to correct for.

This matters directly for your population data: the allele frequency differences between ACB and CEU reflect both **t_s** (when did these populations diverge) and **ancestral drift** before that split.

---

## Q: So ts is time to split essentially

Yes exactly — **t_s is the time of population/lineage splitting**.

It's the point in the past where one ancestral population became two, after which mutations accumulate independently on each lineage. That's why the factor of 2 appears — you're measuring the combined mutational divergence across **both** descending lineages since that split.

The subtle but important distinction worth keeping in mind is:

- **t_s** = when the populations split (a demographic event)
- **t_coal** = when two specific sampled lineages find their common ancestor (a genealogical event)

t_coal ≥ t_s always, because the common ancestor of two lineages must have existed either at or **before** the split. In a large ancestral population, lineages can take a long time to coalesce even before the split happened, which is the ancestral polymorphism problem mentioned earlier.

So when people say "the molecular clock dates the split between populations X and Y," what they've really measured is closer to **t_coal**, and recovering the true **t_s** requires modeling what was happening in the ancestral population — which is the hard part.

---

## Q: How is ts always smaller than tcoal

Good challenge — let me be precise about the direction of time here.

## Thinking Backwards in Time

Both times are measured as **generations ago from the present**. So a **larger value = further in the past**.

```
Past ──────────────────────────────► Present
                    
t_coal ≥ t_s

further back        split          today
    |                 |              |
  [common           [split]     [sample
  ancestor]                    seq1, seq2]
```

## Why t_coal ≥ t_s

Two lineages sampled from **different populations** today travel backwards through time. While they are in **separate populations they simply cannot coalesce** — there is no shared pool to draw a common ancestor from.

Only once you travel back past the split — into the **single ancestral population** — do they enter the same gene pool and become eligible to coalesce.

So coalescence must happen **at t_s or even further back**, hence:

> t_coal ≥ t_s

## The Extreme Cases

- **t_coal = t_s** — the two lineages coalesce immediately at the split, meaning their ancestor was right at the population boundary. Happens when ancestral N is very small.
- **t_coal >> t_s** — the ancestral population was large, so lineages floated around for a long time before finding a common ancestor. The molecular clock then badly overestimates t_s.

---

## Q: Selection, fA(t) depends exclusively on starting allele frequencies

## Allele Frequency Under Selection (Haploid)

The formula you have is the standard **deterministic selection equation** for haploids:

$$f_A(t) = \frac{f_A(0)}{f_A(0) + (1-s)^t \cdot f_a(0)}$$

where $f_a(0) = 1 - f_A(0)$, so the whole thing is indeed just a function of the starting frequency and *s*.

---

## Why it Depends Only on Starting Frequencies

The recursion each generation is:

$$f_A(t+1) = \frac{f_A(t)}{f_A(t) + (1-s) \cdot f_a(t)}$$

A has fitness 1, a has fitness (1-s), so A is favored. Each step only uses the **current frequencies** — there is no memory of how you got there. The system is fully **Markovian**, so knowing f_A(0) plus *s* completely determines the entire trajectory. No other information is needed.

---

## What the Formula Tells You

- As *t* → ∞, $(1-s)^t$ → 0, so $f_A(t)$ → 1. **A fixes deterministically.**
- The speed of fixation depends on **both** *s* and $f_A(0)$ — a rare allele even with strong selection starts very slowly
- If *s* = 0 you recover $f_A(t) = f_A(0)$ for all *t* — pure drift territory, selection does nothing

---

## The Important Caveat

This is **purely deterministic** — it ignores drift entirely. In reality especially when $f_A(0)$ is small, a beneficial allele can still be **lost by chance** before selection can "see" it. The probability of escaping loss is approximately:

$$P(\text{fix}) \approx 2s$$

for a newly arising mutation (Haldane's result). So the deterministic trajectory assumes you've already survived that early stochastic phase — which is a big assumption when the allele is rare.

---

## Q: Viability in diploids then

## Viability Selection in Diploids

In diploids you have **three genotypes** at a biallelic locus, each with their own viability (probability of surviving to reproduce):

| Genotype | Frequency | Viability |
|---|---|---|
| AA | $f_A^2$ | $w_{AA}$ |
| Aa | $2f_A f_a$ | $w_{Aa}$ |
| aa | $f_a^2$ | $w_{aa}$ |

Using Hardy-Weinberg frequencies as the starting point each generation.

---

## The Recursion

After selection, the frequency of A in the next generation is:

$$f_A' = \frac{f_A^2 \cdot w_{AA} + f_A f_a \cdot w_{Aa}}{\bar{w}}$$

where $\bar{w}$ is mean population fitness — just a normalizing constant to make frequencies sum to 1:

$$\bar{w} = f_A^2 \cdot w_{AA} + 2f_A f_a \cdot w_{Aa} + f_a^2 \cdot w_{aa}$$

The numerator counts copies of A weighted by how often they survive — AA individuals contribute two A copies, Aa individuals contribute one.

---

## Dominance Changes Everything

Unlike haploids, the **relationship between genotype and fitness** now matters. The key cases are:

**Additive** — $w_{Aa} = \frac{w_{AA} + w_{aa}}{2}$, heterozygote is exactly intermediate. Behaves most like the haploid case.

**Dominance** — $w_{Aa} = w_{AA}$, A is fully dominant. Selection acts on A even when rare because heterozygotes are already at full fitness.

**Recessivity** — $w_{Aa} = w_{aa}$, A is fully recessive. Selection **cannot see A when rare** — it only shows up in AA homozygotes which are at frequency $f_A^2$, vanishingly rare when $f_A$ is small. This massively slows fixation.

**Overdominance** — $w_{Aa} > w_{AA}$ and $w_{Aa} > w_{aa}$, heterozygote advantage. This is the **balancing selection** case — leads to a stable internal equilibrium where both alleles are maintained indefinitely. Classic example is HbS/HbA in malaria regions.

---

## Connecting to Your Earlier Data

This is directly relevant to why you see **MAF > 0 across all populations** for some SNPs but not others. A fully recessive beneficial allele can drift to loss easily when rare — it's invisible to selection. An overdominant allele like HbS gets actively maintained, so you'd expect it to show nonzero MAF across populations rather than the zeros you see in CEU/CHB for your SNP.

---

## Q: Additive case what is

## Additive Case

Set the fitnesses as:

| Genotype | Viability |
|---|---|
| AA | $1$ |
| Aa | $1 - \frac{s}{2}$ |
| aa | $1 - s$ |

Each copy of *a* subtracts $\frac{s}{2}$ from fitness — the heterozygote is **exactly halfway** between the two homozygotes. There is no dominance, each allele contributes independently and equally.

---

## The Recursion Simplifies Nicely

Plugging into the diploid recursion and expanding $\bar{w}$:

$$f_A' = \frac{f_A(1 - f_a \cdot \frac{s}{2} \cdot ... )}{\bar{w}} \approx f_A + s \cdot f_A f_a$$

for small *s*. This is essentially the **same qualitative behavior as the haploid case** — which is why the additive diploid model and haploid model are often treated interchangeably in theory.

---

## Why Additivity Matters

- Selection can **always see the allele** regardless of frequency — even when A is rare, heterozygotes Aa already have elevated fitness over aa, unlike the recessive case
- The probability of fixation for a new additive mutation is approximately $2s$, same as the haploid result
- No stable internal equilibrium — A fixes deterministically if *s* > 0, just like haploids
- The trajectory $f_A(t)$ has the same sigmoidal shape as the haploid case

So additivity is essentially the **null model of diploid selection** — it's the simplest assumption and collapses the diploid complexity back toward the haploid intuition you already have.

---

## Q: wAA etc is fitness, Vaa viability how is it calculated

## Fitness vs Viability

**Viability** is just one component of total fitness. Total fitness can be decomposed as:

$$w = V \times F$$

where **V** is viability (probability of surviving to reproductive age) and **F** is fecundity (reproductive output once you survive). In many simple models fecundity is assumed equal across genotypes, so **viability ≈ fitness**, which is why the terms get used interchangeably.

---

## How Viability is Calculated

Viability is estimated as the **ratio of observed to expected genotype frequencies** after selection has acted but before reproduction:

$$V_{AA} = \frac{\text{observed frequency of AA after selection}}{\text{expected frequency of AA under HWE}}$$

Concretely, if you genotype adults (post-selection) and newborns/zygotes (pre-selection):

$$V_{AA} = \frac{f_{AA}^{\text{adults}}}{f_{AA}^{\text{zygotes}}} = \frac{f_{AA}^{\text{adults}}}{f_A^2}$$

The denominator is the Hardy-Weinberg expectation — what you'd see with **no differential survival**. Any deviation from that ratio is attributed to viability differences.

---

## The Normalizing Step

Raw viabilities are then **rescaled relative to the best genotype** to give relative fitness:

$$w_{AA} = \frac{V_{AA}}{V_{\text{max}}}$$

so the fittest genotype always gets $w = 1$. This is just a convention to make the math cleaner — only the **ratios** between genotype fitnesses matter for allele frequency dynamics, not the absolute values.

---

## Q: Codominant is additive effect?

## Codominance vs Additivity

They are **closely related but not identical** — it depends on what you're measuring.

---

## Codominance (phenotype language)

Codominance means the heterozygote **expresses both alleles simultaneously** — neither masks the other. The classic example is ABO blood groups where AB individuals show both A and B antigens.

## Additivity (fitness language)

Additivity means the heterozygote fitness is **exactly halfway** between the two homozygotes:

$$w_{Aa} = \frac{w_{AA} + w_{aa}}{2}$$

---

## Where the Confusion Comes From

In population genetics these terms often get **used interchangeably** because:

- If phenotype is additive → each allele contributes equally → heterozygote is intermediate → fitness is intermediate → additive selection
- Codominance in phenotype **often produces** additive fitness effects

So in practice when people say codominant in a selection context they usually **mean additive**.

---

## But They Can Come Apart

If the phenotype is codominant but the fitness relationship between phenotype and survival is **nonlinear**, you can have codominant expression without additive fitness. For example:

- Heterozygote expresses both antigens (codominant phenotype)
- But having both antigens gives a **disproportionate survival advantage** → overdominance in fitness

So strictly speaking:
- **Codominance** is a statement about **phenotype expression**
- **Additivity** is a statement about **fitness values**

They coincide under the simplest assumptions, which is why the terms blur together in most textbook treatments.
