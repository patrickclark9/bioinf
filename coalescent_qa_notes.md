# Coalescent Theory & Bioinformatics — Q&A Notes

---

## Q1 — SSH: sign_and_pubkey signing failed / Permission denied (publickey)

The most common fix is to add your key to the SSH agent:

```bash
ssh-add ~/.ssh/id_ed25519
```

**Steps:**
1. Check if the agent has keys loaded: `ssh-add -l`
2. Add your key: `ssh-add ~/.ssh/id_ed25519`
3. Test connection: `ssh -T git@gitlab.com`

If the key isn't on GitLab, copy it with `cat ~/.ssh/id_ed25519.pub` and add it to **GitLab → Settings → SSH Keys**.

For multiple keys, add a `~/.ssh/config` entry:
```
Host gitlab.com
    HostName gitlab.com
    User git
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes
```

---

## Q2 — UNPROTECTED PRIVATE KEY FILE — Permissions 0755 too open

```bash
chmod 600 ~/.ssh/git_key
chmod 700 ~/.ssh
```

SSH requires private keys to be readable only by the owner (`600` = owner read/write only). Verify with `ls -la ~/.ssh/git_key` — should show `-rw-------`.

---

## Q3 — Why do we sum 2Ne + 2Ne = 4Ne when coalescence time is the same?

**Time to coalescence is still just 2Ne generations** — that is how far back you travel in time to reach the common ancestor. Both lineages arrive at the same ancestor at the same moment.

But both branches **exist simultaneously** during those 2Ne generations. While waiting, you have two lineages running in parallel, each independently accumulating mutations:

```
Left branch:  2Ne generations of mutation opportunity
Right branch: 2Ne generations of mutation opportunity
─────────────────────────────────────────────────────
Total:        4Ne generations of mutation opportunity
```

Think of it like two workers each working 8-hour shifts — they finish at the same clock time, but together they have done 16 hours of work.

4Ne is used to calculate expected nucleotide differences: **π = 4Neμ**

> **2Ne = when** (coalescence time) &nbsp;|&nbsp; **4Ne = how much** total evolution happened across both lineages

---

## Q4 — Expected number of mutations in a lineage in interval τ (in 2N generation units)

If time is measured in units of 2N generations, interval τ represents τ × 2N actual generations:

$$E[\text{mutations}] = \mu \times \tau \times 2N = 2N\mu\tau$$

Rewriting using **θ = 4Nμ**:

$$2N\mu = \frac{\theta}{2} \implies E[\text{mutations}] = \frac{\theta}{2}\tau$$

For **two lineages** over interval τ:

$$2 \times \frac{\theta}{2}\tau = \theta\tau$$

This is where the full θ = 4Nμ naturally emerges.

---

## Q5 — Explain the mutation formula derivation step by step

**1. Real time:** every generation, mutation rate is μ. Over G actual generations: `E[mutations] = μ × G`

**2. Switch to coalescent time:** 1 unit of τ = 2N generations, so `G = τ × 2N`. Substituting: `E[mutations] = 2Nμτ`

**3. Rewrite using θ:** θ = 4Nμ is the population-scaled mutation rate. Since `2Nμ = θ/2`:

$$E[\text{mutations}] = \frac{\theta}{2}\tau$$

**Why the ½?** θ was defined with two lineages in mind (4N = 2×2N), so per single lineage you take half.

**Two lineages:** mutations can land on either branch → double it → `θτ`. This is why the expected pairwise difference works out to exactly **θ**.

---

## Q6 — Coalescence time explanation

**Core question:** pick two gene copies today — how far back until they share a common ancestor?

**Probability per generation:**

There are 2N total gene copies. Two lineages each independently choose a parent:

$$P(\text{coalesce}) = \frac{1}{2N} \qquad P(\text{don't coalesce}) = 1 - \frac{1}{2N}$$

**Geometric distribution:** each generation is an independent Bernoulli trial. Expected waiting time = 1/p:

$$E[T] = 2N \text{ generations}$$

**Exponential approximation:** when N is large, the geometric converges to an Exponential. In coalescent units (1 unit = 2N generations):

$$T \sim \text{Exponential}(\lambda = 1) \qquad E[T] = 1 \text{ coalescent unit}$$

| Population size (N) | Gene copies (2N) | Expected wait |
|---|---|---|
| 100 | 200 | 200 generations |
| 10,000 | 20,000 | 20,000 generations |
| 1,000,000 | 2,000,000 | 2,000,000 generations |

Larger populations → lower chance of sharing an ancestor each generation → longer wait → more genetic diversity.

---

## Q7 — Is the parameter for the exponential distribution 1/λ or 1/2Ne?

Both — depends on the time scale:

| Time scale | Rate parameter λ | Mean E[T] |
|---|---|---|
| Actual generations | 1/2Ne | 2Ne generations |
| Coalescent units | 1 | 1 coalescent unit |

Same distribution, different units. "T ~ Exponential(rate = 1)" implicitly assumes time already rescaled into coalescent units.

---

## Q8 — What do we use the coalescent for?

| Application | What coalescent tells you |
|---|---|
| Population size | Depth of coalescence → infer Ne |
| Bottlenecks / expansions | Rate changes over time |
| Divergence times | When lineages split (molecular clock) |
| Gene flow | Coalescence across populations |
| Phylogenetics | Shape of genealogy (e.g. BEAST) |
| Selection | Deviations from neutral expectations |
| Ancestral reconstruction | State at the MRCA |

- **Positive selection** → unusually short coalescence, low diversity (selective sweep)
- **Balancing selection** → unusually long coalescence, high diversity

---

## Q9 — Expected Tk — coalescence time for k lineages

With k lineages, the number of possible pairs is:

$$\binom{k}{2} = \frac{k(k-1)}{2}$$

Total coalescence rate: $\lambda_k = \binom{k}{2} \cdot \frac{1}{2N_e} = \frac{k(k-1)}{4N_e}$

Expected waiting time in **coalescent units**:

$$E[T_k] = \frac{2}{k(k-1)}$$

| k | Rate | E[Tk] (coalescent units) |
|---|---|---|
| 2 | 1 | 1 |
| 3 | 3 | 1/3 |
| 4 | 6 | 1/6 |
| 5 | 10 | 1/10 |

As k increases, coalescence happens very fast. Most of the tree's height is spent waiting for the **last two lineages** — that interval alone has expected length 1.

---

## Q10 — Gene flow with coalescence — the structured coalescent

Two populations, each size Ne, migration rate m. Each lineage can:
- **Coalesce** with another in the same population (rate 1/2Ne)
- **Migrate** to the other population (rate m)

Lineages in **different** populations cannot coalesce until migration brings them together.

**Key parameter:** M = 2Nem (migrants per generation)

| M value | Interpretation |
|---|---|
| M >> 1 | Populations behave as one panmictic unit |
| M ~ 1 | Moderate structure |
| M << 1 | Nearly isolated, deep coalescence between populations |

**FST and coalescence:**

$$F_{ST} = \frac{E[T_{between}] - E[T_{within}]}{E[T_{between}]} \approx \frac{1}{1 + 4N_em}$$

---

## Q11 — Es and Ed in migration

**Es (same population):**

$$E_s \approx 2N_e + \frac{1}{2m} \text{ (actual generations)}$$

Even lineages starting together may be separated by migration before coalescing.

**Ed (different populations):**

$$E_d = E_s + \frac{1}{2m}$$

The extra 1/2m = waiting for migration to bring lineages into the same population.

**Key relationship:** $E_d - E_s = \frac{1}{2m}$ (purely determined by migration rate)

$$F_{ST} = \frac{E_d - E_s}{E_d} = \frac{1/2m}{E_d}$$

---

## Q12 — Relationship between M and m — how to obtain M

$$M = N_e \cdot m \quad \text{(or } 2N_em \text{ in diploid formulations)}$$

**Why scale by Ne:** what matters is migration relative to drift. Their ratio 2Nem = M determines population structure.

**Obtaining M from FST:**

$$F_{ST} = \frac{1}{1 + 4M} \implies M = \frac{1 - F_{ST}}{4 \cdot F_{ST}}$$

m and Ne individually are hard to separate — **M is the estimable quantity** from genetic data.

---

## Q13 — Usually FST is calculated first and M inferred?

Yes, exactly. Workflow:

1. Collect genetic data from multiple populations
2. Calculate FST: $F_{ST} = \frac{H_T - H_S}{H_T}$ (HT = total heterozygosity, HS = within-population)
3. Infer M: $M = \frac{1 - F_{ST}}{4 \cdot F_{ST}}$

**Caveat:** assumes the island model (equilibrium, equal sizes, symmetric migration). Modern methods (STRUCTURE, IMa, MIGRATE-N) use full coalescent likelihood for more realistic estimates.

---

## Q14 — Ed can be written as 2 + 1/(2M)

Starting from $E_d = E_s + \frac{1}{2m}$, convert m to M.

Since $M = 2N_em \Rightarrow m = \frac{M}{2N_e}$:

$$\frac{1}{2m} = \frac{2N_e}{2M} = \frac{N_e}{M} \text{ generations} = \frac{1}{2M} \text{ coalescent units}$$

Es = 2 coalescent units always, so:

$$\boxed{E_d = 2 + \frac{1}{2M}}$$

| Term | Meaning |
|---|---|
| 2 | Expected coalescence time once in same population (= Es) |
| 1/2M | Extra waiting time for migration to unite lineages |

- Large M → 1/2M ≈ 0 → Ed ≈ 2 (populations act as one)
- Small M → 1/2M → ∞ → very long wait between populations

---

## Q15 — Is migration exponential or Poisson?

**Both** — two sides of the same Poisson process:

| View | Distribution | What it describes |
|---|---|---|
| Count events in interval t | Poisson(mt) | Number of migrations in t generations |
| Wait for next event | Exponential(m) | Time until next migration |

**In the structured coalescent**, each lineage faces competing exponential clocks:

| Event | Rate |
|---|---|
| Coalesce (same population) | 1/2Ne |
| Migrate | m |

The next event occurs at combined rate $\lambda_{total} = \frac{1}{2N_e} + m$ (minimum of two exponentials = exponential with summed rate). This **race between competing clocks** is the core machinery of the structured coalescent.
