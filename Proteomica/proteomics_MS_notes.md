# Mass Spectrometry in Proteomics – Study Notes

---

## 1. Fundamental Principle

All mass spectrometers measure molecules in their **ionized state**. The instrument always reports **m/z**, never molecular mass directly.

### The m/z Formula

$$\frac{M}{Z} = \frac{M_r + (M_a \times Z)}{Z}$$

- $M_r$ = true molecular mass
- $M_a$ = mass of the ionizing adduct (typically H⁺ in positive mode; $M_a = 1.0072$ u)
- $Z$ = charge state

**Single vs. multiple charge states** can be observed, depending on compound, ionization mode, and instrument. Work is almost always done in **positive (+) ion mode** — peptides are protonated (MH⁺) under acidic conditions.

---

## 2. Ionization Methods

### 2.1 MALDI (Matrix-Assisted Laser Desorption/Ionization)

Analyte co-crystallized with a UV-absorbing matrix. A laser pulse desorbs and ionizes the sample. Produces predominantly **singly charged (1+) ions**.

**Advantages**
- Ideal for Peptide Mass Fingerprinting (PMF) — fast, sensitive, salt-tolerant
- Works on larger MW (small intact proteins)
- Sample on stable solid support → no time constraints
- 1+ ions → simpler spectral interpretation

**Disadvantages**
- High accuracy requires careful calibration
- Difficult (but possible) to do MS/MS
- Signal suppression in complex mixtures
- Crystallization conditions influence results

---

### 2.2 ESI (Electrospray Ionization)

Sample solution sprayed through a high-voltage needle; desolvation produces **multiply charged ions** (2+, 3+, ...). Molecules compete for protons during ionization — Na⁺ competes strongly with peptides, hence the sensitivity to salt contamination.

**Advantages**
- Directly coupled online to reversed-phase LC (online separation prior to ionization)
- Sensitive
- 2+/3+ ions are excellent for MS/MS (more charge → more efficient CID fragmentation)

**Disadvantages**
- Sample introduction more complex
- Data analysis harder (must deconvolute charge states)
- One-shot analysis (time-limited once the LC run starts)
- Very low tolerance to contaminants (salts, detergents)

**Why 2+/3+ for tryptic peptides?** Trypsin cleaves C-terminal to Lys/Arg, so each peptide has a basic residue at its C-terminus plus a free N-terminus → at least two protonation sites.

---

### 2.3 Identifying Charge State from Isotope Spacing

| Charge state (z) | Spacing between isotope peaks |
| ---------------- | ----------------------------- |
| 1+               | Δm = 1.0 Da                   |
| 2+               | Δm = 0.5 Da                   |
| 3+               | Δm = 0.33 Da                  |

General rule: $z = 1 / \Delta m_{\text{isotope}}$

---

## 3. Mass Analyzers

| Analyzer | Resolution | Key Feature |
|---|---|---|
| Quadrupole (Q) | Low | Transmit, scan, or select by m/z |
| 3D Ion Trap (IT) | Low | Trap → select → fragment → scan |
| Linear Ion Trap (LIT) | Low | Higher capacity than 3D-IT |
| TOF (Time-of-Flight) | Moderate–High | Separation by flight time; reflectron improves resolution |
| FT-ICR | Very High | Ion cyclotron resonance, Fourier transform detection |
| Orbitrap (OT) | Very High | Orbital trapping; standard high-res platform |

### Common ESI Instrument Configurations

```
QQQ         Q1 (select) → collision cell (fragment) → Q3 (scan)   — quantitation
QQ-TOF      Q1 (select) → collision cell (fragment) → TOF (scan)  — high-res MS/MS
3D-IT       single ion trap: trap → select → fragment → scan
LIT         as above, linear geometry
LIT-OT      LIT (fragment) + Orbitrap (high-res scan)             — e.g. Orbitrap Velos
```

All configurations above can perform MS/MS experiments.

---

## 4. MS vs. MS/MS (Tandem Mass Spectrometry)

### MS
```
Ion production → Ion separation → Detection
```

### MS/MS (Tandem MS)
```
Ion production → Ion separation (select precursor) → Fragmentation (CID) → Ion separation → Detection
```

In a physical tandem instrument: **MS1** selects the precursor → **collision cell** (neutral gas at high pressure, e.g. He, Ar, N₂) → kinetic energy converted to internal energy → bond cleavage → **MS2** analyzes fragment ions.

### Key Glossary

| Term | Definition |
|---|---|
| **CID** | Collision-Induced Dissociation — fragmentation mechanism |
| **Precursor ion** | The parent ion selected for fragmentation |
| **Daughter ions** | Fragment ions produced by CID |
| **Tandem MS / MS/MS** | Combination of ion selection + CID + fragment analysis |

> The principle of MS/MS is **filiation reactions**: a complex mixture spectrum is difficult to interpret, but selecting a single precursor mass and fragmenting it yields a spectrum diagnostic for one molecule's structure.

---

## 5. Peptide Fragmentation and Ion Series

CID of peptides predominantly breaks **amide (peptide) bonds** along the backbone. The resulting fragment ions are classified by which terminus they retain and which bond breaks.

### Bond Cleavages and Ion Types

For cleavage between residues $i$ and $i+1$:

```
             bᵢ → ← yₙ₋ᵢ

H₂N─[AA₁]─[AA₂]─...─[AAᵢ]─┊─[AAᵢ₊₁]─...─[AAₙ]─COOH
                              ↑ bond cleavage
```

| Ion series | Terminus retained | Bond broken | Notes                         |
| ---------- | ----------------- | ----------- | ----------------------------- |
| **a**      | N-terminal        | Cα–CO       | = b − 28 Da (CO loss)         |
| **b**      | N-terminal        | CO–N        | Most common N-terminal series |
| **c**      | N-terminal        | N–Cα        | Less common                   |
| **x**      | C-terminal        | CO–N        | Rare                          |
| **y**      | C-terminal        | N–Cα        | Most common C-terminal series |
| **z**      | C-terminal        | Cα–CO       | Less common                   |

### Reading Sequence from b and y Ions

For a peptide AA₁–AA₂–...–AAₙ:

- **b₁, b₂, ..., b_{n-1}**: mass difference between consecutive bᵢ and bᵢ₊₁ = residue mass of AA_{i+1}
- **y₁, y₂, ..., y_{n-1}**: mass difference between consecutive yⱼ and yⱼ₊₁ = residue mass of AA_{n-j}

Both series read in opposite directions along the sequence — together they provide complementary partial sequence coverage.

**ESI-CID of tryptic peptides**: predominantly b and y ion series observed. The y₁ ion at 147 Da = Lys or 175 Da = Arg is characteristic (terminal basic residue from trypsin cleavage).

---

## 6. Protein Identification by Peptide Mass Fingerprinting (PMF)

### Concept
Trypsin digests a protein into a set of peptides with predictable masses. The pattern of peptide masses is effectively a "fingerprint" unique (or near-unique) to a given protein.

### Workflow
```
Protein band (SDS-PAGE)
    ↓ in-gel trypsin digest
Peptide mixture
    ↓ MALDI-TOF MS
Peak list (m/z values of peptide ions)
    ↓ database search (in silico digest of all proteins)
Protein identification
```

### Effect of Mass Accuracy on Specificity

| Accuracy | Tolerance (Da) | Hits (example) |
|---|---|---|
| Low | 1.0 | 478 |
| Medium | 0.1 | 164 |
| High | 0.01 | 25 |
| Very high | 0.001 | 4 |
| Ultrahigh | 0.0001 | 2 |

→ **Mass accuracy is the single biggest determinant of search specificity in PMF.**

### Effect of Number of Peptides

With tolerance fixed at 0.1 Da:

| Peptides queried | Hits |
|---|---|
| 1 peptide | 204 |
| 2 peptides | 7 |
| 3 peptides | 1 |

→ **More peptides = exponentially more specific identification.**

### Search Parameters (Mascot/ProFound)

- **Database**: UniProtKB/SwissProt, NCBInr, etc.
- **Taxonomy**: narrow to organism when possible (reduces search space)
- **Enzyme**: Trypsin (cuts C-terminal to Lys/Arg, not before Pro)
- **Missed cleavages**: typically 1–2 (accounts for incomplete digestion)
- **Fixed modifications**: Carbamidomethyl (C) — from iodoacetamide alkylation during gel prep
- **Variable modifications**: Oxidation (M) — Met side-chain oxidation is common artifact
- **Mass values**: MH⁺ (monoisotopic preferred for high-res instruments)
- **Tolerance**: in Da or ppm

### Mascot Scoring
Score = −10 × log(P), where P = probability that the match is random.  
Scores > 50–63 are typically significant (p < 0.05) — threshold depends on database size.

### Output: Sequence Coverage Map
Matched peptides highlighted in the protein sequence. **Sequence coverage (%)** = fraction of protein covered by matched peptides.

---

## 7. Protein Identification by MS/MS

### Why MS/MS?

PMF is limited:
- Requires relatively pure protein (gel bands)
- Cannot handle complex mixtures
- No sequence information per peptide

MS/MS provides **per-peptide pseudo-sequence information** and is compatible with complex mixture analysis (shotgun proteomics).

### Automated LC-ESI-MS/MS (Shotgun Proteomics)

#### LC Setup (nanoLC)
- Reversed-phase C₁₈ column: 15–25 cm length, 75 μm internal diameter
- Flow rate: 200–300 nL/min (T-splitter from standard HPLC pump)
- **Organic solvent gradient** (typically MeCN/water + 0.1% formic acid) elutes peptides by hydrophobicity

#### Data-Dependent Acquisition (DDA)
The mass spectrometer automatically:
1. Acquires a full MS1 scan (TIC/survey scan)
2. Selects the top-N most intense precursor ions
3. Isolates each in turn and fragments by CID
4. Acquires MS/MS spectrum for each

→ One LC run generates **hundreds to thousands of MS/MS spectra**, each (ideally) from a distinct peptide.

### Database Searching (MS/MS Mode)

Each MS/MS spectrum is searched against the database: for each candidate protein, compute theoretical b/y ions and score the match to observed ions. Mascot reports individual **peptide scores** and an overall **protein score** = sum of significant peptide scores.

### Orthogonality and Confidence

Each fragmentation spectrum is an **independent (orthogonal)** dataset tied to a specific sequence. If the probability of a random match for one spectrum is $P_1$:

$$P(\text{two random matches to same protein}) = P_1^2$$

Example: $P_1 = 5 \times 10^{-3}$ → $P_2 = 2.5 \times 10^{-5}$ — two orders of magnitude more stringent.

**Practical rule: require ≥ 2 peptides per protein for confident identification.**

### Critical Distinction

> **Protein identification ≠ Protein characterization**
> 
> Two peptides are sufficient to identify a protein, but you are characterizing only those two peptides. Highly similar sequences (isoforms, paralogs) may not be distinguishable. For detecting PTMs, extensive sequence coverage is essential.

---

## 8. Quantitative Proteomics – Isotope Labeling Strategies

### Why Label with Stable Isotopes?

Mass spectrometry is not inherently quantitative — ion signal depends on ionization efficiency, which varies by peptide and run. To compare abundance between samples A and B:
1. Label each sample with chemically identical but isotopically distinct reagents
2. Mix samples → co-analyze → heavy/light peptide pairs co-elute and are distinguished by mass
3. Quantify by peak area ratio (heavy/light)

**Mixing early** eliminates downstream analytical variability.

---

### 8.1 ICAT (Isotope-Coded Affinity Tagging)

**Reagent**: Biotin tag + linker chain (H₈ = light or D₈ = heavy, 8 Da difference) + iodoacetamide reactive group

**Target**: Cysteine residues (thiol alkylation)

**Workflow**:
```
Sample A ──[H₈-ICAT]──┐
                        ├─→ Mix → Trypsin digest → Avidin affinity purification
Sample B ──[D₈-ICAT]──┘         (captures Cys-containing peptides via biotin)
                                         ↓
                              LC-MS/MS → quantify H/D peak ratio → identify by MS/MS
```

**Pros**: Any sample type; reduces complexity (only Cys peptides analyzed); eliminates analytical variability by mixing early.

**Cons**: Covers only ~50–70% of proteins (those with ≥1 Cys); possible side reactions on other residues; losses during avidin purification; mass shift is constant (+8 Da per label), so charge-state deconvolution is straightforward.

---

### 8.2 iTRAQ (Isobaric Tags for Relative and Absolute Quantitation)

**Key innovation**: 4 reagents with **identical total mass (145 Da)** but different internal distribution — reporter group carries the mass difference (114, 115, 116, 117 Da).

| Tag | Reporter (retains charge) | Balance group (neutral loss) | Net heavy isotopes |
|---|---|---|---|
| 114 | ¹³C | ¹³C + ¹⁸O | 4 heavy atoms |
| 115 | ¹³C₂ | ¹⁸O | 3 heavy |
| 116 | ¹³C₂ + ¹⁵N | ¹³C | 2 heavy |
| 117 | ¹³C₃ + ¹⁵N | — | 1 heavy |

**Reactive group**: NHS ester → reacts with **N-terminus** and **Lys ε-amine**.

**Because the total tag mass = 145 Da for all four reagents**:
- The same peptide from each of the 4 samples has the **same precursor m/z** in MS1
- All 4 are co-isolated for fragmentation in a single MS/MS event

**MS/MS yields two types of information simultaneously**:
- **Reporter ions** (114–117 Da region): relative abundance of the peptide across 4 samples → **quantification**
- **b/y ions**: peptide sequence → **identification**

**Workflow**:
```
Sample 1 → digest → [114-tag]──┐
Sample 2 → digest → [115-tag]──┤
Sample 3 → digest → [116-tag]──┤ → Mix → SCX fractionation → nanoLC-MS/MS
Sample 4 → digest → [117-tag]──┘
```

**Pros**: 4 (or 8) samples per run; any protein (not limited to Cys); single MS/MS event yields both ID and quantification.

**Cons**: Requires MS/MS for quantification (cannot quantify from MS1); isobaric co-isolation can cause ratio compression; more complex data analysis.

---

### 8.3 SILAC (Stable Isotope Labeling by Amino acids in Cell Culture)

**Principle**: Metabolic labeling — cells grown in medium where a specific amino acid is replaced by a heavy isotope version.

**Common labels**:
- ¹³C₃-Leucine ("Leu D3") vs. normal leucine — 3 Da per Leu residue
- ¹³C₆-Arg / ¹³C₆-Lys ("heavy SILAC") — now most common

After ~5 cell doublings, essentially all proteins are fully labeled.

**Workflow**:
```
Light cells (control)           Heavy cells (stimulated)
     ↓                                ↓
  Grow 5+ doublings in             Grow in ¹³C/¹⁵N-AA medium
  normal medium                         ↓
     └──────────── Mix immediately after lysis ──────────────┘
                          ↓
               (Optional immunoprecipitation / fractionation)
                          ↓
                    LC-MS/MS
                     ↓          ↓
              Identify (MS/MS)   Quantify (MS1 peak area ratio of heavy/light pairs)
```

**Mass shift**: Variable — depends on number of labeled residues per peptide. This complicates automated peak finding but is well-handled by current software (MaxQuant, etc.).

**Pros**: No chemical modification; native peptides; minimal variability (mixed before any sample handling); quantification at the MS1 level (no co-isolation compression issue).

**Cons**: Only applicable to cultivable organisms (cells or microorganisms); typically limited to 2–3 conditions (light/medium/heavy); cannot be applied to tissues or clinical samples directly.

---

### Comparison Table

| Method | Label type | Chemistry | Coverage | N samples | Quantification |
|---|---|---|---|---|---|
| ICAT | Chemical | Cys alkylation | Cys-containing peptides | 2 | MS1 peak ratio |
| iTRAQ | Chemical | N-term + Lys | All peptides | 4 (or 8) | MS/MS reporter ions |
| SILAC | Metabolic | Amino acid incorporation | All peptides | 2–3 | MS1 peak ratio |

---

## 9. Applications

### 9.1 Classical 2D-PAGE + MALDI-TOF PMF

Proteins separated by pI (isoelectric focusing, 1st dimension) and MW (SDS-PAGE, 2nd dimension). Spots excised → in-gel trypsin digestion → MALDI-TOF PMF.

**Why SDS-PAGE is a good prep method**:
- Robust, widely available, low-tech
- Removes many contaminants during fixation/staining steps
- Analytical + micropreparative

**Limitations**:
- In-gel digestion is non-quantitative
- Peptide recovery from gel is incomplete
- Poor recovery of very hydrophobic or large proteins

**Example — E. coli adaptation to low glucose (Wick et al., Environ Microbiol 2001)**:
- 2D-PAGE of E. coli grown in normal vs. very low glucose medium → 15 differentially regulated protein spots identified by PMF
- Functional categories: metabolic enzymes + transport proteins → shift toward alternative energy sources

---

### 9.2 Gel-Free Shotgun Proteomics

Replaces gel separation with solution-phase digestion + LC fractionation + MS/MS. Enables:
- Analysis of complex proteomes (thousands of proteins per experiment)
- Quantification via SILAC, iTRAQ, or label-free methods
- Detection of low-abundance proteins

---

### 9.3 Other Fields

- **Phosphoproteomics**: Enrichment of phosphopeptides (TiO₂, IMAC) followed by LC-MS/MS; phosphorylation site localization from MS/MS
- **Ubiquitinomics**: Enrichment of ubiquitinated proteins/peptides
- **Clinical proteomics / Biomarker discovery**: Serum/plasma proteomics; comparison of patient vs. healthy cohorts
- **Proteome imaging**: MALDI of tissue sections → spatial maps of protein/peptide distribution without extraction

---

## 10. Key Conceptual Points

1. **MS always measures m/z, never mass directly** — must know z to recover $M_r$; this is trivially solved for MALDI (almost always z=1) but requires deconvolution for ESI.

2. **MALDI → 1+ ions; ESI → 2+/3+ ions** — this determines suitability: MALDI-TOF for simple PMF, ESI for online LC-MS/MS.

3. **b ions = N-terminal; y ions = C-terminal** — consecutive mass differences within one series = amino acid residue masses → sequence ladder.

4. **Mass accuracy is the dominant variable in PMF specificity** — going from 1 Da to 0.001 Da tolerance reduces false matches by two orders of magnitude.

5. **Orthogonal MS/MS datasets** — each spectrum is an independent piece of evidence; two peptides per protein gives dramatically higher confidence than one.

6. **Protein ID ≠ protein characterization** — two peptides suffice for identity, but PTM discovery requires high sequence coverage.

7. **iTRAQ is isobaric** — all four samples have the same precursor mass; quantification comes exclusively from reporter ions in MS/MS, not MS1.

8. **SILAC mixes earliest** — reduces all downstream variability; but limited to cultured organisms.

9. **ICAT selects Cys-containing peptides** — simplifies mixture but misses Cys-free proteins.

10. **Gel-free approaches** have largely superseded 2D-PAGE + MALDI for deep proteome coverage and quantification, while 2D-PAGE remains useful for visual comparison and preparative work.
