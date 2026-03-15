# Coalescent Theory — Q&A Notes

---

## Q1 — Why do we sum 2Ne + 2Ne = 4Ne when coalescence time is the same?

Great question — the confusion is between **time to coalescence** and **total branch length**.

**Time to coalescence is still just 2Ne generations.** That's how far back in time you travel to reach the common ancestor. Both lineages arrive at the same ancestor at the same moment — 2Ne generations ago. You don't add them for time.

**But both branches exist *simultaneously* during those 2Ne generations.** While you're waiting 2Ne generations for coalescence, you have *two* lineages running in parallel, each independently accumulating mutations. So the total amount of evolutionary history — the sum of branch lengths — is:

```
Left branch:  2Ne generations of mutation opportunity
Right branch: 2Ne generations of mutation opportunity
─────────────────────────────────────────────────────
Total:        4Ne generations of mutation opportunity
```

Think of it like two workers each working 8-hour shifts. They both finish at the same clock time (8 hours from now), but together they've done 16 hours of work.

**Why does 4Ne matter?** It's used to calculate the expected number of nucleotide differences between two randomly sampled sequences:

> **π = 4Neμ**

where μ is the mutation rate per generation. The 4Ne comes from this total branch length — mutations can land on either branch and create a difference between the two sequences.

So in short: **2Ne = when** (coalescence time), **4Ne = how much total evolution happened** across both lineages during that time.

---

## Q2 — Expected number of mutations in a lineage in interval τ (in 2N generation units)

If time is measured in units of **2N generations**, then an interval τ represents **τ × 2N actual generations**.

The mutation rate per generation per lineage is μ, so:

$$E[\text{mutations}] = \mu \times \tau \times 2N = 2N\mu\tau$$

This is usually rewritten using **θ = 4Nμ**, the standard coalescent parameter, so:

$$2N\mu = \frac{\theta}{2}$$

$$E[\text{mutations}] = \frac{\theta}{2}\tau$$

**Intuition:** θ/2 is effectively your "mutation rate per unit of coalescent time." For every unit of τ that passes on a single lineage, you expect θ/2 mutations to land on it.

This is why for **two lineages** over a coalescent interval τ, the expected total mutations (on both branches combined) is:

$$2 \times \frac{\theta}{2}\tau = \theta\tau$$

The factor of 2 for two branches is where the full **θ = 4Nμ** naturally emerges in calculations like the expected number of pairwise differences.

---

## Q3 — Explain the mutation formula derivation step by step

**Start with real time (actual generations)**

Every generation, a mutation lands on a given lineage with probability μ. So if you watch one lineage for G actual generations, the expected number of mutations is simply:

$$E[\text{mutations}] = \mu \times G$$

**Now switch to coalescent time units**

In coalescent theory, time is rescaled so that 1 unit of τ = 2N actual generations. This is done because 2N is the natural timescale at which coalescence happens.

So if τ has passed in coalescent time, the actual number of generations that elapsed is:

$$G = \tau \times 2N$$

Substituting back:

$$E[\text{mutations}] = \mu \times \tau \times 2N = 2N\mu\tau$$

**Rewrite using θ**

θ = 4Nμ is defined as the population-scaled mutation rate — it bundles together population size and mutation rate into one number. Rearranging:

$$2N\mu = \frac{4N\mu}{2} = \frac{\theta}{2}$$

So:

$$E[\text{mutations}] = \frac{\theta}{2}\tau$$

**What this means intuitively**

- **θ/2** is your mutation rate per unit of coalescent time, per lineage
- Every tick of coalescent time τ on a single branch, you expect θ/2 new mutations
- The ½ is there because θ was defined with two lineages in mind (the 4N = 2×2N accounts for both branches), so per single lineage you take half

**Scaling to two lineages**

When you have two lineages both running for time τ (as in the pairwise coalescent), mutations can land on either branch and create a visible difference. So you double it:

$$E[\text{mutations on both branches}] = 2 \times \frac{\theta}{2}\tau = \theta\tau$$

This is why the expected pairwise difference between two sequences — where coalescence happens at time τ drawn from an exponential distribution with mean 1 — works out to exactly **θ**.

---

## Q4 — Coalescence time explanation

**The Core Question**

Pick two gene copies from a population today. How far back do you have to go until they share a common ancestor?

**Setting Up the Probability**

Each generation, every gene copy was "descended from" exactly one parent gene copy in the previous generation. There are **2N** total gene copies in the population (N diploid individuals, 2 copies each).

When your two lineages look backwards one generation, what is the chance they pick the *same* parent?

$$P(\text{coalesce in previous generation}) = \frac{1}{2N}$$

Because there are 2N possible parent copies, and both lineages must independently land on the same one.

The chance they *don't* coalesce:

$$P(\text{don't coalesce}) = 1 - \frac{1}{2N}$$

**Waiting Generation by Generation**

Each generation is an independent coin flip — either they coalesce (probability 1/2N) or they don't. You keep flipping until you get a coalescence. This is exactly a **geometric distribution**.

For a geometric distribution with success probability p, the expected waiting time is 1/p. So:

$$E[\text{generations until coalescence}] = \frac{1}{1/2N} = 2N \text{ generations}$$

**The Exponential Approximation**

When N is large, the geometric distribution is well approximated by an **exponential distribution**. In coalescent units (where 1 unit = 2N generations), the coalescence time T becomes:

$$T \sim \text{Exponential}(\text{rate} = 1)$$

meaning:

$$E[T] = 1 \text{ coalescent unit} = 2N \text{ actual generations}$$

This is the key simplification that makes coalescent theory tractable — instead of tracking discrete generations, you work with a clean exponential waiting time.

**Why Exponential and Not Something Else?**

Each generation is a Bernoulli trial with tiny probability 1/2N. Over many generations, the number of trials until the first success, scaled by 2N, converges to an exponential. This is the standard Poisson/geometric → exponential limit when:
- probability of success per trial is small
- number of trials is large

Both conditions are met when N is large, which is the biological reality for most populations.

**Intuition for the 2N figure**

| Population size (N) | Gene copies (2N) | Expected wait |
|---|---|---|
| 100 | 200 | 200 generations |
| 10,000 | 20,000 | 20,000 generations |
| 1,000,000 | 2,000,000 | 2,000,000 generations |

Larger populations → more gene copies → lower chance of randomly sharing an ancestor each generation → longer wait. This is why genetic diversity scales with population size.

**Summary**

| Quantity | Value |
|---|---|
| Coalescence probability per generation | 1/2N |
| Expected coalescence time | 2N generations |
| In coalescent time units | 1 unit |
| Distribution of coalescence time | Exponential(1) |

The exponential distribution with rate 1 in coalescent time is the single most important fact in all of coalescent theory — everything else builds on it.

---

## Q5 — Is the parameter for the exponential distribution 1/λ or 1/2Ne?

Yes, exactly — it depends on which time scale you're working in.

**In actual generations**

The coalescence rate per generation is 1/2Ne, so:

$$T \sim \text{Exponential}\left(\lambda = \frac{1}{2N_e}\right)$$

$$E[T] = \frac{1}{\lambda} = 2N_e \text{ generations}$$

**In coalescent time units** (rescaled so 1 unit = 2Ne generations)

You divide time by 2Ne, which multiplies the rate by 2Ne:

$$\lambda' = \frac{1}{2N_e} \times 2N_e = 1$$

$$T \sim \text{Exponential}(\lambda = 1)$$

$$E[T] = 1 \text{ coalescent unit}$$

So the statement "T ~ Exponential(rate = 1)" was implicitly assuming time already rescaled into coalescent units. The more precise statement is:

| Time scale | Rate parameter | Mean |
|---|---|---|
| Actual generations | 1/2Ne | 2Ne generations |
| Coalescent units | 1 | 1 unit |

They describe the same distribution — just expressed in different units.

---

## Q6 — What do we use the coalescent for?

**The coalescent is a framework for reasoning backwards in time** — instead of simulating a population forward, you start from a sample of sequences today and trace their ancestry back.

**1. Estimating Population Size (Ne)**

The expected time to coalescence is 2Ne generations. So if you measure genetic diversity in a sample, you can infer Ne.

- High diversity → long coalescence times → large Ne
- Low diversity → short coalescence times → small Ne

This lets you estimate historical population sizes from DNA alone.

**2. Detecting Population Size Changes**

If Ne changed over time (bottlenecks, expansions), the rate of coalescence changes across different time periods. This is how we know things like:

- Human populations went through a bottleneck out of Africa
- Neanderthal populations were small
- COVID-19 virus expanded rapidly

**3. Estimating Divergence Times**

When did two populations or species split? Coalescence times give you a molecular clock — more mutations separating two lineages means they coalesced (split) longer ago.

**4. Inferring Gene Flow and Population Structure**

If two populations exchange migrants, gene copies can coalesce across populations. Patterns of coalescence across groups tell you:

- Are these populations isolated or connected?
- How much migration is occurring?

**5. Building Phylogenetic Trees**

The genealogy of sampled gene copies is itself a coalescent tree. Statistical methods use the coalescent as a prior when reconstructing evolutionary trees (e.g. Bayesian phylogenetics in software like BEAST).

**6. Detecting Natural Selection**

Under neutral evolution, coalescence times follow the exponential distribution you derived. Selection distorts this:

- **Positive selection** → one lineage sweeps through the population → unusually short coalescence, low diversity
- **Balancing selection** → multiple lineages maintained → unusually long coalescence, high diversity

Deviations from neutral coalescent expectations are a signature of selection.

**7. Ancestral Sequence Reconstruction**

By tracing lineages back to the MRCA, you can statistically reconstruct what the ancestral sequence looked like — used in studies of ancient proteins, viral evolution, etc.

**Summary**

| Application | What coalescent tells you |
|---|---|
| Population size | Depth of coalescence |
| Bottlenecks/expansions | Rate changes over time |
| Divergence times | When lineages split |
| Gene flow | Coalescence across populations |
| Phylogenetics | Shape of genealogy |
| Selection | Deviations from neutral expectations |
| Ancestral reconstruction | State at the MRCA |

The unifying theme is: **the shape of a genealogy contains information about the population history that produced it**, and the coalescent is the mathematical bridge between the two.

---

## Q7 — Expected Tk — coalescence time for k lineages

**Setup: k lineages instead of 2**

With k lineages, coalescence can happen between *any pair*. The number of possible pairs is:

$$\binom{k}{2} = \frac{k(k-1)}{2}$$

Each pair has an independent coalescence rate of 1/2Ne per generation, so the total rate of *any* coalescence happening is:

$$\lambda_k = \binom{k}{2} \cdot \frac{1}{2N_e} = \frac{k(k-1)}{4N_e}$$

**Expected waiting time**

$$E[T_k] = \frac{1}{\lambda_k} = \frac{4N_e}{k(k-1)} \text{ generations}$$

In coalescent units (scaling by 2Ne):

$$E[T_k] = \frac{2}{k(k-1)} \text{ coalescent units}$$

**Intuition across k**

| k lineages | Rate | E[Tk] in coalescent units |
|---|---|---|
| 2 | 1 | 1 |
| 3 | 3 | 1/3 |
| 4 | 6 | 1/6 |
| 5 | 10 | 1/10 |

As k increases, there are many more pairs, coalescence happens very fast, and you wait very little time before the first merger. Most of the coalescent tree's *height* is spent waiting for the last two lineages to merge — that interval alone has expected length 1 (the full E[T2]).

---

## Q8 — Gene flow with coalescence — the structured coalescent

**The Core Idea**

With gene flow, two lineages can coalesce in two ways:
- Wait long enough in the same population and coalesce there
- One lineage **migrates** into the other population, and then they coalesce

So migration gives lineages an additional route to finding a common ancestor.

**The Structured Coalescent**

Imagine two populations, A and B, each of size Ne, exchanging migrants at rate m (probability per generation that a lineage moves to the other population).

At any moment, each lineage can either:
- **Coalesce** with another lineage in the same population (rate 1/2Ne)
- **Migrate** to the other population (rate m)

Two lineages in *different* populations **cannot coalesce** — they must first be brought together by migration.

**What Migration Does to Coalescence Time**

Without gene flow, two lineages from different populations can never coalesce (they are completely isolated). With gene flow:

$$E[T_{MRCA}] \approx 2N_e + \frac{1}{2m} \text{ (coalescent units)}$$

The extra 1/2m term is the waiting time for migration to bring the lineages into the same population. So:

- **High migration** → lineages come together quickly → short coalescence time → low divergence between populations
- **Low migration** → lineages rarely meet → long coalescence time → high divergence between populations

**The Parameter M = 2Nem**

Just like θ = 4Neμ bundles population size and mutation rate, the key parameter for gene flow is:

$$M = 2N_e m$$

This is the number of migrants entering a population per generation. It determines whether populations behave as:

| M value | Interpretation |
|---|---|
| M >> 1 | Many migrants per generation → populations behave like one large panmictic population |
| M ~ 1 | Moderate structure → some differentiation |
| M << 1 | Rare migration → populations nearly isolated → deep coalescence between them |

**FST and Coalescence**

Population differentiation FST has a direct coalescent interpretation:

$$F_{ST} = \frac{E[T_{between}] - E[T_{within}]}{E[T_{between}]}$$

It measures how much longer it takes two lineages from *different* populations to coalesce compared to two from the *same* population. Under the island model:

$$F_{ST} \approx \frac{1}{1 + 4N_em} = \frac{1}{1 + 2M}$$

So FST is entirely determined by M — it doesn't depend on mutation rate or population size separately.

**Visualizing the Genealogy**

Without gene flow:
```
Pop A        Pop B
  |            |
  |            |      ← lineages never meet
  |            |
```

With gene flow:
```
Pop A        Pop B
  |         → |      ← migration event
  |    \       
  |     MRCA          ← coalescence after migration
```

Migration events appear as horizontal jumps in the genealogy, after which coalescence can occur.

**Summary**

| Concept | Role |
|---|---|
| Migration rate m | How often lineages move between populations |
| M = 2Nem | Migrants per generation — key summary statistic |
| FST | Measures relative depth of between vs within coalescence |
| High M | Populations genetically similar, shallow coalescence |
| Low M | Populations diverged, deep coalescence between them |

The coalescent framework makes gene flow inference natural — you're just asking how migration changes the probability and timing of lineages finding a common ancestor.

---

## Q9 — Es and Ed in migration

**Setup**

Two populations, each size Ne, migration rate m between them. Sample two lineages — either from the **same** population or **different** populations.

**Es — Expected coalescence time, Same population**

Both lineages start in the same population. They can either:
- Coalesce immediately (rate 1/2Ne)
- One migrates out (rate m), and now they're separated

Working through the math, you have to account for the possibility of migrating out and then coming back together:

$$E_s = \frac{2N_e(1 + 4N_em)}{1+4N_em} \approx 2N_e + \frac{1}{2m}$$

Intuitively: even lineages starting together might get separated by migration before coalescing, adding extra waiting time.

**Ed — Expected coalescence time, Different populations**

Both lineages start in different populations. They **cannot coalesce until migration brings them together first**:

$$E_d = E_s + \frac{1}{2m}$$

The extra 1/2m is the additional wait for migration to bring the two lineages into the same population before the Es clock even starts.

**The Relationship**

$$E_d - E_s = \frac{1}{2m}$$

The difference between the two is purely determined by migration rate — it is the expected waiting time for a migration event to unite the two lineages.

**Connection to FST**

$$F_{ST} = \frac{E_d - E_s}{E_d} = \frac{1/2m}{E_d}$$

| Scenario | Es | Ed | FST |
|---|---|---|---|
| High migration (m large) | ≈ 2Ne | ≈ 2Ne | ≈ 0 (no structure) |
| Low migration (m small) | 2Ne + 1/2m | 2Ne + 1/m | → 1 (strong structure) |

When migration is high, Ed ≈ Es because lineages mix freely — it barely matters which population you sampled from. When migration is low, Ed >> Es because lineages from different populations take much longer to find a common ancestor.

---

## Q10 — Relationship between M and m — how to obtain M

**Recall the definitions**

- **m** = probability that a single lineage migrates to the other population per generation (raw migration rate)
- **Ne** = effective population size
- **M** = population-scaled migration rate

**The Relationship**

$$M = N_e \cdot m$$

or sometimes defined as:

$$M = 2N_e m$$

depending on whether you're working with a haploid or diploid model. In the diploid island model the standard definition is:

$$M = N_e m$$

which represents the **number of migrants entering a population per generation**.

**Why Scale by Ne?**

Just like θ = 4Neμ bundles mutation rate with population size, M bundles migration rate with population size because what matters evolutionarily is not m alone but how migration compares to drift.

- Drift acts at rate **1/2Ne** per generation
- Migration acts at rate **m** per generation

Their ratio determines population structure:

$$\frac{m}{1/2N_e} = 2N_em$$

When migration >> drift (M large), populations mix. When drift >> migration (M small), populations diverge.

**How to Obtain M in Practice**

**From FST:**

$$F_{ST} = \frac{1}{1 + 4M}$$

Rearranging:

$$M = \frac{1 - F_{ST}}{4 F_{ST}}$$

So you:
1. Measure FST from allele frequency differences between populations
2. Plug into the formula above
3. Get M directly

This is the most common practical approach — you never need to observe migration directly.

**Summary**

| Parameter | What it is | How to get it |
|---|---|---|
| m | Per-lineage migration probability per generation | Hard to measure directly |
| M = Nem | Migrants per generation, scaled | From FST = 1/(1+4M) |
| FST | Genetic differentiation | From allele frequencies in data |

M is the parameter you actually estimate from genetic data — m and Ne individually are hard to separate without additional information.

---

## Q11 — So usually FST is calculated first and M inferred?

Yes, exactly. The workflow in practice is:

**1. Collect genetic data** from individuals in multiple populations

**2. Calculate FST** from allele frequencies using observed heterozygosities:

$$F_{ST} = \frac{H_T - H_S}{H_T}$$

where HT is total heterozygosity and HS is average within-population heterozygosity

**3. Infer M** by plugging FST into:

$$M = \frac{1 - F_{ST}}{4F_{ST}}$$

**Why this direction and not the other?**

- FST is directly **observable** from genotype data
- m and Ne individually are **not directly observable** — you'd need longitudinal data tracking actual migrants across generations, which is rarely feasible
- M collapses both into one estimable parameter

**Caveat**

This approach assumes the **island model** — populations at migration-drift equilibrium, equal sizes, symmetric migration. In reality:

- Populations may not be at equilibrium (recent bottleneck, expansion)
- Migration may be asymmetric
- Population sizes may differ

So M inferred from FST is really a summary statistic under idealized assumptions, not a direct measurement of true migration. Modern methods (STRUCTURE, IMa, MIGRATE-N) use the full coalescent likelihood to get more realistic estimates.

But conceptually yes — **FST first, M second** is the standard logic.

---

## Q12 — Ed can be written as 2 + 1/(2M)

**Starting Point**

Recall from before:

$$E_d = E_s + \frac{1}{2m}$$

The goal is to rewrite the 1/2m term using M instead of m.

**Converting m to M**

The standard definition for a diploid population is:

$$M = 2N_e m \implies m = \frac{M}{2N_e}$$

So in actual generations:

$$\frac{1}{2m} = \frac{2N_e}{2M} = \frac{N_e}{M} \text{ generations}$$

Converting to coalescent units (dividing by 2Ne):

$$\frac{1}{2m} = \frac{N_e}{M \cdot 2N_e} = \frac{1}{2M} \text{ coalescent units}$$

**The Result**

$$E_d = E_s + \frac{1}{2M}$$

And it turns out that Es = 2 coalescent units always, regardless of M (because rare migration events and their associated delays exactly cancel out algebraically). So:

$$\boxed{E_d = 2 + \frac{1}{2M}}$$

**Intuition for each term**

| Term | Meaning |
|---|---|
| 2 | Expected coalescence time once lineages are in the same population (= Es, always 2 coalescent units) |
| 1/2M | Extra waiting time for migration to bring lineages from different populations together |

- Large M → 1/2M ≈ 0 → Ed ≈ Es ≈ 2 → populations behave as one
- Small M → 1/2M → ∞ → lineages from different populations take very long to coalesce

---

## Q13 — Is migration exponential or Poisson?

**Both — they are two sides of the same process.**

**Poisson — counting events in an interval**

The *number* of migration events occurring in a time interval follows a Poisson distribution. If migration rate is m per generation, then in t generations:

$$\text{Number of migrations} \sim \text{Poisson}(mt)$$

**Exponential — waiting time between events**

The *waiting time* until the next migration event follows an Exponential distribution:

$$T_{migration} \sim \text{Exponential}(m)$$

$$E[T_{migration}] = \frac{1}{m}$$

**Why they are the same process**

This is the **Poisson process** — events occur continuously and independently at a constant rate. It has a dual representation:

- Count events in a window → **Poisson**
- Wait for next event → **Exponential**

They are mathematically equivalent descriptions of the same underlying process.

**In the coalescent specifically**

At any moment a lineage faces competing exponential clocks:

| Event | Rate |
|---|---|
| Coalesce (same population) | 1/2Ne |
| Migrate to other population | m |

The minimum of two independent exponentials is itself exponential with rate equal to the **sum** of rates. So the next event — whichever happens first — occurs at rate:

$$\lambda_{total} = \frac{1}{2N_e} + m$$

This race between competing exponential clocks is the core machinery of the structured coalescent.

---

## Q14 — Scaling of time: where does the 2N conversion appear in every formula?

**The scaling definition**

1 coalescent unit = 2N actual generations, so to convert:

$$t_{\text{coalescent}} = \frac{t_{\text{generations}}}{2N}$$

which equivalently multiplies any **rate** by 2N.

**Mutation count**

In actual generations: `E[mutations] = μ × G`

Substitute G = τ × 2N:

$$E[\text{mutations}] = 2N\mu\tau = \frac{\theta}{2}\tau$$

The scaling turns the raw mutation rate μ into the per-coalescent-unit rate θ/2.

**Coalescence time itself**

Coalescence probability per generation = 1/2N, so expected wait = 2N generations.

Divide by 2N to get coalescent units:

$$\frac{2N}{2N} = 1 \text{ coalescent unit}$$

The geometric distribution (discrete generations) also becomes Exponential(λ=1) after this scaling — the 2N in the denominator of the rate 1/2N gets cancelled by the 2N scaling factor.

**Exponential rate parameter**

| Time scale | Rate λ | Mean |
|---|---|---|
| Actual generations | 1/2N | 2N generations |
| Coalescent units | 1/2N × 2N = **1** | 1 unit |

Scaling by 2N transforms a rate of 1/2N into a clean rate of 1.

**Expected Tk for k lineages**

In actual generations: $E[T_k] = \frac{4N}{k(k-1)}$

Divide by 2N:

$$E[T_k] = \frac{4N}{k(k-1) \cdot 2N} = \frac{2}{k(k-1)} \text{ coalescent units}$$

**Es and Ed**

In actual generations: $E_s \approx 2N + \frac{1}{2m}$

Divide everything by 2N:

$$E_s = 1 + \frac{1}{4Nm} = 1 + \frac{1}{2M} \approx 2 \text{ (when M is moderate)}$$

**Ed = 2 + 1/(2M)**

The 1/2m term in actual generations gets scaled:

$$\frac{1}{2m} \text{ generations} \div 2N = \frac{1}{2m \cdot 2N} = \frac{1}{4Nm} = \frac{1}{2M} \text{ coalescent units}$$

This is the key step that converts m into M in the final expression.

**Summary of what scaling does everywhere**

| Quantity | Actual generations | Coalescent units |
|---|---|---|
| Coalescence rate (2 lineages) | 1/2N | 1 |
| E[T2] | 2N | 1 |
| E[Tk] | 4N/k(k-1) | 2/k(k-1) |
| Mutation rate per lineage | μ | θ/2 |
| Migration waiting time | 1/2m | 1/2M |
| Ed | 4N + 1/2m | 2 + 1/2M |

The entire point of the 2N scaling is to make coalescence happen at rate 1 per unit time, which simplifies all the math — every other quantity then naturally expresses itself in terms of θ and M rather than the raw parameters μ, m, and N separately.

---

## Q15 — 2N scaling is valid only for diploid populations

Good catch. The **2N scaling comes from diploidy**, not from having two populations. The "2" means 2 copies per individual.

**Where the 2N comes from**

In a diploid population of N individuals, each carries 2 gene copies, so the total gene pool is:

$$\text{gene copies} = 2N$$

The coalescence probability per generation is 1/2N because there are 2N possible parents to choose from. This is entirely about **ploidy**.

**For haploid populations**

Each individual carries only 1 copy, so gene pool = N copies:

$$P(\text{coalesce}) = \frac{1}{N}$$

$$E[T] = N \text{ generations}$$

Scaling unit = **N generations**, not 2N. Everything carries through the same way but with N replacing 2N, and θ = 2Nμ instead of 4Nμ.

**General rule**

| Ploidy | Gene copies | Coalescence time | Scaling unit | θ |
|---|---|---|---|---|
| Haploid (1N) | N | N generations | N | 2Nμ |
| Diploid (2N) | 2N | 2N generations | 2N | 4Nμ |

The two populations in the structured coalescent are completely separate — that is about population structure, not ploidy. You can have a structured coalescent with haploid organisms across two populations, and the scaling unit would still be N, not 2N.

So whenever you see 2N throughout all the formulas, mentally read it as **"total gene copies in one diploid population"**, not as anything to do with the number of populations.

---

## Q16 — λ in the exponential of the coalescent is 1/2Ne only when considering 2 lineages

Yes, exactly.

**For 2 lineages:**

$$\lambda_2 = \binom{2}{2} \cdot \frac{1}{2N} = 1 \cdot \frac{1}{2N} = \frac{1}{2N}$$

In coalescent units this becomes λ = 1. This is the special case everyone quotes.

**For k lineages:**

$$\lambda_k = \binom{k}{2} \cdot \frac{1}{2N} = \frac{k(k-1)}{2} \cdot \frac{1}{2N}$$

The 1/2N is still there — it is always the **per-pair** coalescence rate. But you multiply by the number of pairs, so the total rate scales up with k.

**So more precisely:**

- **1/2N** = coalescence rate for a **single pair** of lineages, always
- **λk = C(k,2)/2N** = coalescence rate for the **whole system** of k lineages

When k = 2, C(2,2) = 1, so the two coincide and you get λ = 1/2N.

For any k > 2, the system coalesces faster than 1/2N because multiple pairs are racing simultaneously — the first pair to coalesce wins.

---

## Q17 — Segregating sites under ISM are just θ times coalescence time (tree height)

Yes, exactly. Let's build it up cleanly.

**Infinite Sites Model (ISM) assumption**

Each mutation hits a brand new site — no site is ever hit twice. So every mutation that occurs on the tree automatically becomes a **segregating site** (a position where the two lineages differ).

**For two lineages**

Mutations accumulate at rate θ/2 per lineage per coalescent unit. Over both branches simultaneously the rate is θ. The tree height (coalescence time) is T ~ Exponential(1).

So the number of segregating sites S is just mutations landing on the total branch length:

$$E[S] = \theta \cdot T$$

Taking the expectation over T:

$$E[S] = \theta \cdot E[T] = \theta \cdot 1 = \theta$$

This is why **θ is directly estimated by counting segregating sites** between two sequences.

**For k lineages (Watterson's estimator)**

With k sampled sequences the total tree has multiple intervals. The total expected branch length summed across all intervals is:

$$E[\text{total branch length}] = \sum_{i=2}^{k} i \cdot E[T_i] = \sum_{i=2}^{k} i \cdot \frac{2}{i(i-1)} = \sum_{i=2}^{k} \frac{2}{i-1} = 2\sum_{j=1}^{k-1} \frac{1}{j} = 2a_k$$

where $a_k = \sum_{j=1}^{k-1} \frac{1}{j}$ is the harmonic number.

Expected segregating sites:

$$E[S] = \theta \cdot a_k$$

Rearranging gives **Watterson's estimator** of θ:

$$\hat{\theta}_W = \frac{S}{a_k}$$

**Summary**

| Quantity | Role |
|---|---|
| ISM | Guarantees every mutation = one new segregating site |
| θ | Mutation rate scaled by population size = expected S between two sequences |
| T (tree height) | How long mutations had to accumulate |
| S = θ × T | Segregating sites = rate × time |
| Watterson's estimator | Extends this to k sequences via harmonic number |

The key insight is that under ISM, **counting mutations and counting segregating sites are the same thing** — which is what makes the coalescent so powerful for inference.

---

## Q18 — Tajima's estimator is derived from 2 lineages

Yes, exactly.

**Tajima's estimator θπ**

When you pick two sequences at random and count the differences between them, you are looking at exactly the two-lineage coalescent. Under ISM every difference is a mutation that landed on one of the two branches:

$$E[\pi] = \theta \cdot E[T_2] = \theta \cdot 1 = \theta$$

So the average pairwise difference **is** θ directly. For a sample of k sequences you average over all pairs:

$$\hat{\theta}_\pi = \frac{1}{\binom{k}{2}} \sum_{i<j} d_{ij}$$

where $d_{ij}$ is the number of differences between sequences i and j. Each pair is a two-lineage coalescent in expectation.

**Contrast with Watterson**

| Estimator | Based on | Lineages |
|---|---|---|
| θπ (Tajima) | Average pairwise differences | 2 lineages at a time |
| θW (Watterson) | Total segregating sites | Full k-lineage tree |

Both estimate the same θ under neutrality, but they weight different parts of the tree differently.

**Why this matters — Tajima's D**

Since both estimators target the same θ under neutral evolution and constant population size:

$$D = \frac{\hat{\theta}_\pi - \hat{\theta}_W}{\text{Var}} \approx 0 \text{ under neutrality}$$

Deviations signal departures from neutrality:

| D | Interpretation |
|---|---|
| D < 0 | θW > θπ → many rare variants → recent expansion or positive selection |
| D > 0 | θπ > θW → many intermediate frequency variants → balancing selection or bottleneck |

The power of Tajima's D comes entirely from the fact that the two estimators look at different parts of the coalescent tree — pairwise depths vs. total branch length — and selection or demography distorts these differently.

---

## Q19 — Heterozygosity in the coalescent as a model of genetic drift

**The Question Reframed**

Heterozygosity H is the probability that two randomly drawn gene copies from a population are **different**. In coalescent terms this is simply the probability that they have **not** coalesced before accumulating at least one mutation.

**Building it from the coalescent**

Pick two random gene copies. Two things must happen for them to be different:

1. They coalesce at some time T (exponential, rate 1 in coalescent units)
2. At least one mutation falls on the tree before coalescence

Under ISM, mutations fall at rate θ on the total branch length. Given coalescence time T, the number of mutations is Poisson(θT). So the probability of **no** mutation (identical sequences) is:

$$P(\text{identical} \mid T) = e^{-\theta T}$$

Taking the expectation over T ~ Exponential(1):

$$P(\text{identical}) = \int_0^\infty e^{-\theta t} \cdot e^{-t} dt = \int_0^\infty e^{-(1+\theta)t} dt = \frac{1}{1+\theta}$$

Therefore heterozygosity is:

$$H = P(\text{different}) = 1 - \frac{1}{1+\theta} = \frac{\theta}{1+\theta}$$

**What this means**

| Scenario | H |
|---|---|
| θ → 0 (tiny Ne or μ) | H → 0, everyone identical, drift dominates |
| θ → ∞ (large Ne or μ) | H → 1, everyone different, mutation dominates |
| θ = 1 | H = 0.5, drift and mutation balanced |

**The drift interpretation**

Genetic drift is entirely captured by the coalescence rate. Stronger drift means:
- Smaller Ne
- Faster coalescence
- Less time for mutations to accumulate before lineages merge
- Lower H

So H is the outcome of a **race between coalescence (drift) and mutation**:

```
Mutation wins     →  lineages differ    →  contributes to H
Coalescence wins  →  lineages identical →  does not contribute to H
```

θ = 4Neμ is exactly the ratio that determines who wins this race. Large Ne slows coalescence, giving mutations more time to accumulate.

**Connection to drift directly**

Without mutation (θ = 0), every pair eventually coalesces → H = 0. This is genetic drift to fixation — given enough time, all lineages trace back to a single ancestor and the population becomes monomorphic. The coalescent is just the **genealogical description of drift** — drift is what causes coalescence.

**Summary**

| Quantity | Coalescent meaning |
|---|---|
| H | Probability two lineages differ = mutation won the race against coalescence |
| 1 − H | Probability two lineages are identical = coalesced before any mutation |
| θ | Controls the balance between drift (coalescence) and mutation |
| Ne large | Slow coalescence → more H |
| Ne small | Fast coalescence → less H, drift dominates |
