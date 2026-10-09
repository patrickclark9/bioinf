# The Lymphoid System, B Cells and T Cells: A Detailed Overview

## Table of Contents
- [[#General Overview of T Cells, B Cells and NK Cells]]
- [[#1. The Lymphoid System at a Glance]]
- [[#2. Primary Lymphoid Organs]]
- [[#3. Secondary Lymphoid Organs]]
- [[#4. Lymph and Lymphatic Circulation]]
- [[#5. Lymphocyte Development (Lymphopoiesis)]]
- [[#6. T Cells]]
- [[#7. B Cells]]
- [[#8. T–B Cooperation and the Germinal Center]]
- [[#9. NK Cells]]
- [[#10. Innate Lymphoid Cells (ILCs)]]
- [[#11. Tolerance and Immune Regulation]]
- [[#12. Clinical Relevance]]
- [[#13. Lymphocytes in Omics and Computational Work]]
- [[#14. Quick Comparison Table]]

---

## General Overview of T Cells, B Cells and NK Cells

T cells and B cells are the two main **antigen-specific lymphocytes** of the adaptive immune system, while NK cells are the main cytotoxic lymphocytes of the **innate** immune system. Each individual cell carries a single receptor specificity, and the whole population together can recognize a vast range of antigens. Both undergo **clonal selection** (the cell whose receptor matches an antigen is activated and expands), generate **immunological memory**, and are shaped by **self-tolerance** so that they normally ignore the body's own components.
![[Pasted image 20261008172030.png]]
### T cells (T lymphocytes) in general

- **Origin:** arise from bone-marrow progenitors but **mature in the thymus** (the "T" stands for thymus).
- **Type of immunity:** **cell-mediated immunity**. They act through direct contact with other cells and through secreted cytokines. They **do not produce antibodies**.
- **What they recognize:** short **peptide fragments** that have been processed inside a cell and displayed on **MHC molecules** at the cell surface. This is called **MHC restriction**.
  - **CD8⁺ T cells** see peptides on **MHC class I**, which is present on almost all nucleated cells and reports on proteins made *inside* the cell.
  - **CD4⁺ T cells** see peptides on **MHC class II**, found on professional antigen-presenting cells (dendritic cells, macrophages, B cells), which reports on material taken up from *outside* the cell.
- **Main targets:**
  - **Intracellular pathogens** that hide from antibodies: viruses, intracellular bacteria (e.g., *Mycobacterium tuberculosis*, *Listeria*), and some protozoa and fungi
  - **Infected, damaged or malignant (tumor) cells**, which CD8⁺ cytotoxic T cells kill directly
  - Indirectly, **extracellular pathogens**, because CD4⁺ helper T cells activate macrophages and provide help to B cells
- **Main roles:** killing infected or abnormal cells (CD8⁺ CTLs), coordinating the immune response (CD4⁺ helper subsets), dampening immunity to prevent damage (Tregs), and forming long-lived memory.
- **Self vs non-self:** T cells **do** discriminate non-self from self, but only at the level of **peptide–MHC complexes**. During thymic selection, cells that bind self peptide–MHC too strongly are eliminated or diverted to a regulatory fate, so mature T cells respond mainly to **foreign peptides presented on self-MHC**. A T cell cannot recognize a free, intact pathogen or a soluble antigen floating in fluid; the antigen must first be processed and presented.

### B cells (B lymphocytes) in general

- **Origin:** develop and mature in the **bone marrow** in mammals (the "B" originally came from the *bursa of Fabricius* in birds).
- **Type of immunity:** **humoral immunity**, mediated by **antibodies** (immunoglobulins) secreted into blood, lymph and mucosal secretions.
- **What they recognize:** **native, intact antigens** in their original three-dimensional shape, through the membrane-bound **B-cell receptor (BCR)**. Antigens can be proteins, polysaccharides, lipids or nucleic acids, and **no MHC presentation is needed** for recognition itself.
- **Main targets:**
  - **Extracellular pathogens** (e.g., many bacteria, free virus particles before they enter cells, parasites)
  - **Toxins** and other soluble molecules in body fluids
  - Antibodies can also **block viral entry**, tag microbes for phagocytosis (**opsonization**), activate **complement**, and protect mucosal surfaces (IgA)
- **Main roles:** after activation, B cells differentiate into **plasma cells** (antibody-secreting factories) and **memory B cells**. They also act as **antigen-presenting cells** to helper T cells.
- **Need for T-cell help:** for most protein antigens, B cells need **CD4⁺ T follicular helper cells** to undergo class switching, somatic hypermutation and affinity maturation. Some repetitive antigens (e.g., bacterial polysaccharides) can activate B cells with little or no T-cell help (**T-independent** responses), but with weaker memory.
- **Self vs non-self:** B cells with strongly self-reactive receptors are removed or edited in the bone marrow (central tolerance), and further controls act in the periphery.

### NK cells (natural killer cells) in general

- **Origin:** develop from the common lymphoid progenitor, mainly in the **bone marrow**; classed as **innate lymphoid cells** (cytotoxic group 1 ILCs).
- **Type of immunity:** **innate** cell-mediated immunity. They act **quickly and without prior sensitization**, and do not need clonal expansion before acting.
- **What they recognize:** **not a specific antigen.** They use a **balance of activating and inhibitory germline-encoded receptors**. Cells that lack normal **MHC class I** ("missing-self") or display **stress-induced ligands** ("induced-self") are killed, as are **IgG-coated** cells (via CD16, ADCC).
- **Main targets:** virally infected cells, tumor cells, stressed cells and cells that have lost MHC I.
- **Main roles:** killing via **perforin/granzymes**, producing **IFN-γ** and other cytokines that shape later adaptive responses, and regulating DCs and T cells. A subset shows memory-like behavior.
- **Self vs non-self:** healthy self cells display MHC I that engages NK **inhibitory receptors**, so they are spared; NK cells are "educated" on self MHC I to ensure this.
- See [[#9. NK Cells]] for the detailed section.

> An **antigen-presenting cell** (**APC**) or **accessory cell** is a cell that displays an antigen bound by [major histocompatibility complex](https://en.wikipedia.org/wiki/Major_histocompatibility_complex "Major histocompatibility complex") (MHC) proteins on its surface; this process is known as [antigen presentation](https://en.wikipedia.org/wiki/Antigen_presentation "Antigen presentation"). T cells may recognize these complexes using their T cell receptors (TCRs). APCs process antigens and present them to T cells.

![[Pasted image 20261008172105.png]]

While B-Cells can act as APCs (they display antigen bound on its surface), T-Cells can only recognize an antigen if bound to an APC complexed with peptides from MHC, they cannot act themselves as APCs.
### Common misconceptions to avoid

| Statement | More accurate version |
|---|---|
| "T cells do not recognize non-self antigens." | T cells **do** respond to non-self antigens, but only as **processed peptides on MHC**; they cannot see free, native antigen. |
| "T cells only deal with intracellular microbes." | CD8⁺ T cells mainly handle intracellular threats and tumor cells, but CD4⁺ T cells also coordinate responses against **extracellular** microbes and help B cells. |
| "B cells only fight extracellular microbes." | Antibodies mostly act outside cells, but they also neutralize viruses **before** cell entry, and B cells present antigen to T cells, linking both arms. |
| "B cells need MHC to recognize antigen." | The BCR binds **native antigen directly**; MHC II is needed only later, when the B cell presents peptide to a helper T cell. |
| "NK cells are just a type of T cell." | NK cells are **innate lymphocytes** with no TCR; they are CD3⁻ and use germline-encoded activating and inhibitory receptors. |
| "NK cells kill anything with MHC I missing and nothing else." | Missing-self is one trigger. NK cells also respond to **stress ligands**, **antibody-coated targets** (ADCC) and cytokines, and the final decision is a **balance of signals**. |

### In a nutshell

| | **T cells** | **B cells** | **NK cells** |
|---|---|---|---|
| **Arm of immunity** | Adaptive, cell-mediated | Adaptive, humoral (antibody-mediated) | Innate, cell-mediated |
| **Receptor** | TCR (V(D)J-rearranged) | BCR (V(D)J-rearranged) | Germline-encoded activating and inhibitory receptors |
| **What the receptor sees** | Processed peptide + MHC | Native antigen (protein, sugar, lipid, nucleic acid) | Missing-self (low MHC I), stress ligands, IgG-coated cells |
| **MHC needed for recognition?** | Yes (MHC I or II) | No | Self MHC I acts as an **inhibitory** signal |
| **Where they act** | Inside and between cells; tissues and lymphoid organs | Body fluids (blood, lymph, mucosal surfaces) | Blood, liver, uterus, tissues; lymph nodes |
| **Typical targets** | Intracellular pathogens, infected and tumor cells | Extracellular pathogens, toxins, free virus | Virally infected, tumor and stressed cells |
| **Speed of response** | Days (priming and expansion) | Days (antibodies after activation) | Hours to days; no priming needed |
| **Main output** | Cytotoxic killing, cytokines, regulation | Antibodies | Cytotoxic killing, IFN-γ and other cytokines |
| **Memory** | Memory T cells (T_CM, T_EM, T_RM) | Memory B cells and long-lived plasma cells | Limited, innate-like (adaptive NK, CIML) |

---

## 1. The Lymphoid System at a Glance

The lymphoid system is the network of **organs, tissues, vessels and cells** responsible for:

- **Producing and maturing lymphocytes** (primary lymphoid organs)
- **Filtering lymph and blood, and initiating adaptive immune responses** (secondary lymphoid organs)
- **Returning interstitial fluid to the blood** (lymphatic vessels)
- **Absorbing dietary lipids** from the gut via lacteals
- **Immune surveillance** of tissues throughout the body

It is a core component of the **adaptive immune system**, which provides antigen-specific responses and immunological memory, and it works closely with innate immunity.

### Major cell types
| Cell type | Lineage | Main role |
|---|---|---|
| T lymphocytes | Lymphoid | Cell-mediated immunity, help, regulation |
| B lymphocytes | Lymphoid | Humoral immunity (antibodies), antigen presentation |
| NK cells | Lymphoid (innate) | Cytotoxic killing of stressed/infected/tumor cells |
| Innate lymphoid cells (ILCs) | Lymphoid (innate) | Tissue-resident cytokine producers |
| Dendritic cells, macrophages | Myeloid (mostly) | Antigen presentation, support lymphoid architecture |
| Stromal cells (FRCs, FDCs) | Non-hematopoietic | Scaffold, chemokine and antigen display |

---

## 2. Primary Lymphoid Organs

Primary (central) lymphoid organs are where lymphocytes **develop and mature** independently of antigen.

### 2.1 Bone Marrow
- Site of **hematopoiesis**: hematopoietic stem cells (HSCs) give rise to all blood cells.
- The **common lymphoid progenitor (CLP)** arises here.
- **B cell development occurs entirely in the bone marrow** (in mammals) up to the immature B cell stage.
- Also houses **long-lived plasma cells** in specialized survival niches (CXCL12, IL-6, APRIL, BAFF).
- T-cell progenitors leave the marrow and migrate to the thymus.

### 2.2 Thymus
- Bilobed organ in the anterior mediastinum, largest in childhood and **involutes with age** (replaced progressively by adipose tissue).
- Organized into:
  - **Cortex**: densely packed immature thymocytes, cortical thymic epithelial cells (cTECs)
  - **Medulla**: more mature thymocytes, medullary TECs (mTECs), dendritic cells, **Hassall's corpuscles**
- Function: **T-cell maturation and selection** (see Section 5).
- mTECs express **AIRE** (autoimmune regulator), driving ectopic expression of tissue-restricted antigens for negative selection.

---

## 3. Secondary Lymphoid Organs

Secondary (peripheral) lymphoid organs are where **naive lymphocytes encounter antigen** and are activated.

### 3.1 Lymph Nodes
- Bean-shaped, located along lymphatic vessels (cervical, axillary, inguinal, mesenteric, etc.).
- **Afferent lymphatics** bring lymph in; **efferent lymphatics** carry it out. Blood enters via **high endothelial venules (HEVs)**.
- Architecture:
  - **Cortex (outer)**: B cell follicles (primary and secondary, with germinal centers), FDC networks
  - **Paracortex (T cell zone)**: T cells and dendritic cells; contains HEVs; fibroblastic reticular cells (FRCs) form conduits
  - **Medulla**: plasma cells, macrophages; medullary cords and sinuses
- Key chemokine cues:
  - **CCL19 / CCL21** → CCR7 on T cells and DCs (T zone homing)
  - **CXCL13** → CXCR5 on B cells (follicle homing)
  - **S1P** → S1PR1 (egress from nodes)

### 3.2 Spleen
- Filters **blood** (not lymph).
- **White pulp**: lymphoid tissue around central arterioles
  - **PALS** (periarteriolar lymphoid sheath): T cells
  - **Follicles**: B cells
  - **Marginal zone**: marginal zone B cells, specialized macrophages; important for responses to blood-borne, T-independent (encapsulated bacteria) antigens
- **Red pulp**: removal of old erythrocytes, iron recycling, plasma cell reservoir.
- Asplenia increases risk of infection by encapsulated organisms (*S. pneumoniae*, *H. influenzae*, *N. meningitidis*).

### 3.3 Mucosa-Associated Lymphoid Tissue (MALT)
- **GALT** (gut): **Peyer's patches** (with **M cells** sampling luminal antigen), isolated lymphoid follicles, appendix
- **BALT / NALT** (bronchus / nasopharynx): tonsils, adenoids
- **Skin-associated** and **conjunctiva-associated** tissues
- Dominant antibody isotype: **secretory IgA**.
- Central to **oral tolerance** and mucosal immunity.

### 3.4 Tertiary Lymphoid Structures (TLS)
- Ectopic lymphoid aggregates that form at sites of **chronic inflammation, autoimmunity, infection or tumors**.
- In many cancers, TLS presence correlates with **better prognosis and response to immunotherapy**.

---

## 4. Lymph and Lymphatic Circulation

- **Lymph** = interstitial fluid collected by blind-ended **initial lymphatic capillaries**, then moved via collecting vessels (with valves and smooth muscle) to lymph nodes.
- Drains ultimately into the venous system via the **thoracic duct** (left, most of the body) and **right lymphatic duct**.
- Lymph transports **antigens, antigen-carrying dendritic cells and lymphocytes** to nodes.
- **Lymphocyte recirculation**: naive lymphocytes continually migrate blood → HEV → lymph node → efferent lymph → thoracic duct → blood, scanning for cognate antigen.
- Lymphangiogenesis is driven by **VEGF-C/VEGF-D → VEGFR3**; lymphatic endothelial markers include **LYVE-1, PROX1, podoplanin**.

---

## 5. Lymphocyte Development (Lymphopoiesis)

### 5.1 From HSC to lymphoid lineages
```
HSC → MPP → LMPP → CLP ──┬──→ pro-B → pre-B → immature B → (periphery) mature B
                         ├──→ ETP → thymocytes → T cells (via thymus)
                         ├──→ NK cell progenitors
                         └──→ ILC progenitors
```
Key transcription factors: **IKAROS, PU.1, E2A, EBF1, PAX5** (B lineage); **NOTCH1, GATA3, TCF1, BCL11B** (T lineage).

### 5.2 Antigen receptor generation: V(D)J recombination
- Occurs in developing lymphocytes using **RAG1/RAG2** recombinase and **TdT** (adds N-nucleotides).
- Recombination signal sequences (RSS) with 12/23 spacers flank V, D and J segments (**12/23 rule**).
- Generates enormous receptor diversity through:
  - Combinatorial V-D-J joining
  - **Junctional diversity** (palindromic P-nucleotides, N-nucleotides, exonuclease trimming)
  - Pairing of two chains (H + L for BCR; α + β or γ + δ for TCR)
- **CDR3** is the most variable region and the primary determinant of antigen specificity.
- Defects in RAG1/2 or DNA repair factors (e.g., Artemis) cause **SCID**.

### 5.3 T-cell development in the thymus
1. **Double negative (DN1–DN4)**: CD4⁻CD8⁻; TCRβ rearrangement and pre-TCR checkpoint (**β-selection**).
2. **Double positive (DP)**: CD4⁺CD8⁺; TCRα rearrangement.
3. **Positive selection** (cortex): TCR must bind self-MHC with sufficient affinity; failure → death by neglect. Lineage commitment:
   - MHC I-restricted → **CD8⁺**
   - MHC II-restricted → **CD4⁺**
4. **Negative selection** (medulla, and cortex): thymocytes with high affinity for self-peptide/MHC undergo apoptosis (clonal deletion) or are diverted to **Treg** fate.
5. Single-positive naive T cells exit via **S1P** gradient.

Only ~2–5% of thymocytes survive selection.

### 5.4 B-cell development in the bone marrow
| Stage | Features |
|---|---|
| Pro-B | D–J rearrangement of IgH (then V–DJ); RAG, TdT active |
| Pre-B | Pre-BCR (μ heavy chain + surrogate light chain: VpreB/λ5); light chain rearrangement (κ then λ) |
| Immature B | Surface IgM; **central tolerance**: receptor editing, clonal deletion, anergy |
| Transitional → mature naive | Co-express IgM and IgD; migrate to spleen and secondary lymphoid organs |

---

## 6. T Cells

### 6.1 The T-cell receptor (TCR) complex
- **αβ TCR** (~95% of T cells) recognizes **peptide–MHC**.
- **γδ TCR** recognizes diverse ligands (non-peptide antigens, stress molecules) often independent of classical MHC.
- Associated with the **CD3 complex** (CD3γ, δ, ε, ζ) bearing **ITAMs** for signal transduction.
- **Co-receptors**: **CD4** (binds MHC II) and **CD8** (binds MHC I), both associated with **Lck**.

### 6.2 Activation: three signals
1. **Signal 1**: TCR–peptide/MHC engagement
2. **Signal 2 (co-stimulation)**: **CD28** on T cell binds **CD80/CD86 (B7)** on APC
3. **Signal 3**: **cytokines** that polarize differentiation (e.g., IL-12, IL-4, TGF-β/IL-6, IL-2)

Signaling cascade: Lck → ZAP-70 → LAT/SLP-76 → PLCγ → Ca²⁺/NFAT, PKCθ/NF-κB, Ras/MAPK/AP-1 → **IL-2** production, proliferation, differentiation.

Absence of signal 2 leads to **anergy**.

**Checkpoints (inhibitory)**: **CTLA-4** (competes with CD28 for B7), **PD-1** (binds PD-L1/PD-L2), LAG-3, TIM-3, TIGIT.

### 6.3 CD4⁺ T helper (Th) subsets
| Subset | Driving cytokines | Master TF | Key effector cytokines | Main function |
|---|---|---|---|---|
| **Th1** | IL-12, IFN-γ | T-bet (TBX21) | IFN-γ, TNF | Intracellular pathogens, macrophage activation |
| **Th2** | IL-4 | GATA3 | IL-4, IL-5, IL-13 | Helminths, allergy, IgE, eosinophils |
| **Th17** | TGF-β, IL-6, IL-23 | RORγt | IL-17A/F, IL-22 | Extracellular bacteria/fungi, mucosal defense, autoimmunity |
| **Tfh** | IL-6, IL-21, ICOS | BCL6 | IL-21, IL-4 | Help B cells in germinal centers |
| **Treg** | TGF-β, IL-2 | FOXP3 | IL-10, TGF-β, IL-35 | Suppression, tolerance |
| Th9 / Th22 | various | PU.1 / AHR | IL-9 / IL-22 | Allergy, tumor immunity / skin barrier |

### 6.4 CD8⁺ cytotoxic T lymphocytes (CTLs)
- Recognize endogenous peptides on **MHC class I** (virally infected cells, tumor cells).
- **Cross-presentation** by dendritic cells (esp. cDC1) enables priming against exogenous antigens.
- Killing mechanisms:
  - **Perforin + granzymes** (granule exocytosis → apoptosis)
  - **Fas–FasL** pathway
  - Cytokines: **IFN-γ, TNF**
- Form an **immunological synapse** with target cells.

### 6.5 Regulatory T cells (Tregs)
- **FOXP3⁺ CD25⁺ (IL-2Rα)** CD4⁺ cells; thymic-derived (tTreg) or peripherally induced (pTreg).
- Mechanisms: IL-2 consumption, CTLA-4-mediated suppression of APCs, IL-10/TGF-β/IL-35, adenosine production (CD39/CD73).
- **FOXP3 mutation → IPEX syndrome** (severe autoimmunity).

### 6.6 T-cell memory and differentiation states
| State | Markers (human) | Features |
|---|---|---|
| Naive (T_N) | CD45RA⁺ CCR7⁺ CD62L⁺ | Recirculate through lymph nodes |
| Stem-cell memory (T_SCM) | CD45RA⁺ CCR7⁺ CD95⁺ | Self-renewing, long-lived |
| Central memory (T_CM) | CD45RO⁺ CCR7⁺ CD62L⁺ | Lymph node homing, rapid proliferation |
| Effector memory (T_EM) | CD45RO⁺ CCR7⁻ | Peripheral tissue surveillance, rapid effector function |
| Tissue-resident memory (T_RM) | CD69⁺ CD103⁺ | Non-recirculating, frontline defense in tissues |
| Effector (T_EFF/TEMRA) | CD45RA⁺ CCR7⁻ | Short-lived, terminally differentiated |

### 6.7 T-cell exhaustion
- Occurs under **chronic antigen stimulation** (chronic infection, cancer).
- Features: sustained expression of **PD-1, TIM-3, LAG-3, TIGIT, TOX**; reduced cytokine production and proliferation.
- Progenitor-exhausted (TCF1⁺) cells respond to checkpoint blockade.

### 6.8 Unconventional T cells
- **γδ T cells**: epithelial surveillance, rapid responses.
- **NKT cells** (invariant NKT): recognize lipids on **CD1d**.
- **MAIT cells**: recognize microbial riboflavin metabolites on **MR1**.

---

## 7. B Cells

### 7.1 The B-cell receptor (BCR)
- Membrane-bound **immunoglobulin** (IgM/IgD on naive cells) associated with **Igα/Igβ (CD79a/CD79b)** that carry ITAMs.
- **Co-receptor complex**: CD19–CD21 (CR2)–CD81 lowers the activation threshold when antigen is coated with complement (C3d).
- Signaling: Lyn/Syk → BLNK → PLCγ2, BTK → Ca²⁺, NF-κB, MAPK.

### 7.2 Immunoglobulin structure and isotypes
- Two heavy chains + two light chains (κ or λ); **Fab** (antigen binding) and **Fc** (effector function).
- Variable (V) and constant (C) regions; hypervariable CDRs.

| Isotype | Key properties |
|---|---|
| **IgM** | First produced; pentameric in serum; potent complement activation |
| **IgD** | Co-expressed with IgM on naive B cells; role in activation/regulation |
| **IgG** (IgG1–4) | Most abundant in serum; opsonization, neutralization, ADCC, complement activation, crosses placenta (FcRn) |
| **IgA** | Dimeric secretory form at mucosal surfaces and in milk |
| **IgE** | Mast cell/basophil sensitization; allergy and anti-helminth immunity |

### 7.3 B-cell subsets
- **Follicular (B-2) B cells**: the main population; participate in T-dependent germinal center responses.
- **Marginal zone B cells**: rapid, often T-independent responses to blood-borne antigens.
- **B-1 cells**: innate-like, produce natural IgM, found in peritoneal/pleural cavities.
- **Regulatory B cells (Bregs)**: IL-10, IL-35 producing.
- **Memory B cells** and **plasma cells** (see below).

### 7.4 Activation
**T-dependent (TD) response**
1. BCR binds and internalizes antigen; processes and presents peptide on **MHC II**.
2. Cognate **Tfh cell** provides help via **CD40L–CD40**, **IL-4, IL-21**, ICOS–ICOSL.
3. B cell proliferates, forming extrafollicular foci (early plasmablasts) or entering the **germinal center**.

**T-independent (TI) response**
- **TI-1**: TLR ligands (e.g., LPS) activate B cells directly.
- **TI-2**: highly repetitive polysaccharides cross-link many BCRs. Produces mostly IgM with limited memory.

### 7.5 Somatic processes driven by AID
**Activation-induced cytidine deaminase (AID, AICDA)** underlies two key diversification processes:
- **Somatic hypermutation (SHM)**: point mutations at a rate ~10⁻³ per base per division in V regions → **affinity maturation** with selection.
- **Class-switch recombination (CSR)**: DNA recombination in switch regions to change C_H region (e.g., IgM → IgG/IgA/IgE) while keeping the same V region. Directed by cytokines (IL-4 → IgE/IgG1 in mouse; TGF-β → IgA; IFN-γ → IgG).

Defects: **Hyper-IgM syndrome** (CD40L or AID deficiency).

### 7.6 Plasma cells and memory B cells
- **Plasma cells**: antibody-secreting factories (Blimp-1/PRDM1, XBP1, IRF4); lose surface BCR and MHC II; CD138⁺, CD38^hi, CD27^hi. Long-lived plasma cells reside in bone marrow niches.
- **Memory B cells**: CD27⁺ (humans), carry mutated, often class-switched BCRs; respond rapidly and more strongly upon re-exposure.

### 7.7 Antibody effector functions
- **Neutralization** of toxins/viruses
- **Opsonization** (via Fcγ receptors)
- **Complement activation** (classical pathway)
- **ADCC** (NK cells via FcγRIIIa/CD16)
- **Mast cell degranulation** (IgE–FcεRI)
- **Mucosal protection** (IgA)
- **Passive immunity** (maternal IgG transplacental, IgA in milk)

---

## 8. T–B Cooperation and the Germinal Center

1. Naive B and T cells are primed independently (B cells by antigen in follicles; T cells by DCs in the paracortex).
2. Activated B and T cells move toward the **T–B border** (via changes in CCR7, EBI2/GPR183, CXCR5 expression) and form cognate interactions.
3. Some B cells form **extrafollicular plasmablasts** (rapid, lower-affinity antibodies); others seed **germinal centers (GCs)**.
4. **GC architecture**:
   - **Dark zone**: centroblasts, rapid proliferation, SHM (CXCR4^hi)
   - **Light zone**: centrocytes testing BCR affinity against antigen displayed on **follicular dendritic cells (FDCs)** and competing for **Tfh** help (CXCR4^lo CD83^hi)
5. Cycles of mutation and selection → **affinity maturation**.
6. Outputs: **long-lived plasma cells** and **memory B cells**.

---

## 9. NK Cells

### 9.1 Overview
- **Natural killer (NK) cells** are **innate lymphocytes**: lymphoid in origin, but they do **not** rearrange V(D)J genes and do **not** carry an antigen-specific TCR or BCR. They use **germline-encoded receptors** instead.
- Morphologically they are **large granular lymphocytes**, making up roughly 5–15% of circulating lymphocytes in humans, and are also abundant in liver, uterus (decidua), lung and lymph nodes.
- They are the **cytotoxic member of the group 1 innate lymphoid cell family** and are often described as the innate counterpart of CD8⁺ cytotoxic T cells.
- They respond within hours to days **without prior sensitization** (hence "natural" killer), providing early defense before adaptive responses are ready.
- **Main targets:** virally infected cells (especially herpesviruses such as CMV), **tumor cells**, stressed or damaged cells, and cells that have lost MHC class I expression. They also contribute to **graft-versus-leukemia** effects in transplantation.

### 9.2 Development and licensing
- Derive from the **common lymphoid progenitor** in the bone marrow; also mature in secondary lymphoid tissue and liver.
- **IL-15** (presented in trans by IL-15Rα) is essential for development, survival and homeostasis.
- Key transcription factors: **NFIL3 (E4BP4), ID2, EOMES, T-bet (TBX21), TOX**.
- **Education / licensing**: NK cells become functionally competent when their inhibitory receptors engage **self MHC class I** during maturation (e.g., KIR–HLA, NKG2A–HLA-E in humans; Ly49–H-2 in mice). This tunes responsiveness so that they tolerate healthy self cells yet react to cells that lack self MHC I.

### 9.3 Phenotype and subsets
- **Human identification:** **CD3⁻ CD56⁺** (mouse: NK1.1⁺ / NKp46⁺ / CD49b⁺, CD3⁻).

| Subset (human) | Phenotype | Location | Main function |
|---|---|---|---|
| **CD56^bright** | CD56^hi CD16^lo/⁻, CCR7⁺, CD62L⁺, NKG2A^hi, KIR^lo | ~10% of blood NK cells; enriched in lymph nodes and tissues | Cytokine production (IFN-γ, TNF, GM-CSF), immunoregulation |
| **CD56^dim** | CD56^lo CD16^hi, KIR⁺, high perforin | ~90% of blood NK cells | Cytotoxicity and ADCC |
| **Tissue-resident NK** | CD69⁺, CD103⁺/CXCR6⁺ (varies) | Liver, uterus (decidual NK), lung, gut | Local surveillance, tissue homeostasis, pregnancy support |
| **Adaptive / memory-like NK** | NKG2C⁺ CD57⁺, FcRγ-low | Expanded after HCMV infection | Faster, stronger secondary responses |

### 9.4 How NK cells decide: the balance of signals
NK activity depends on the **integration of activating and inhibitory signals**, not on a single receptor.

**Inhibitory receptors** (signal through **ITIMs** → SHP-1/SHP-2)
- **KIRs** (e.g., KIR2DL, KIR3DL) bind classical HLA-A, -B, -C
- **CD94/NKG2A** binds **HLA-E**
- **LILRB1 (LIR-1/ILT2)** binds a broad range of HLA class I
- Mouse: **Ly49** family

**Activating receptors** (signal through ITAM-containing adaptors or DAP10)
- **NKG2D** → binds stress-induced ligands (**MICA, MICB, ULBP1–6**); signals via **DAP10**
- **Natural cytotoxicity receptors (NCRs):** **NKp46, NKp30, NKp44**
- **DNAM-1 (CD226)** → binds CD155 (PVR) and CD112
- **Activating KIRs** (e.g., KIR2DS), **CD94/NKG2C**
- **CD16 (FcγRIIIa)** → binds the Fc region of **IgG**, triggering **ADCC**
- **Co-receptors:** 2B4 (CD244), NTB-A, CD2

**Recognition concepts**
- **Missing-self**: cells with reduced or absent MHC I (e.g., many virally infected or tumor cells) lose inhibitory input and are killed.
- **Induced-self**: stress-induced ligands (e.g., MICA/B) trigger activating receptors.
- **Antibody-dependent recognition**: IgG-coated targets are recognized via CD16.

**Cytokine inputs**: **IL-15, IL-2, IL-12, IL-18, IL-21, type I interferons** prime and activate NK cells.

### 9.5 Effector functions
1. **Direct cytotoxicity**
   - Form an **immunological synapse**; **lytic granules** polarize and release **perforin** and **granzymes** (A, B) → target apoptosis
   - **Death-receptor pathways:** FasL–Fas and **TRAIL**–TRAIL-R
2. **ADCC (antibody-dependent cellular cytotoxicity)** via CD16: central to the action of therapeutic antibodies such as rituximab (anti-CD20) and trastuzumab (anti-HER2).
3. **Cytokine and chemokine production:** **IFN-γ, TNF, GM-CSF**, CCL3/4/5, XCL1. These activate macrophages, promote **Th1** responses and recruit dendritic cells.
4. **Immunoregulation and crosstalk**
   - **NK–DC crosstalk**: DC-derived IL-12/IL-15/IL-18 activate NK cells; NK cells can edit immature DCs and promote DC maturation via IFN-γ/TNF.
   - NK cells can **limit T-cell responses** by killing activated T cells or competing for IL-2.
5. **Reproductive and tissue roles:** **decidual NK cells** help remodel uterine spiral arteries and support placentation.

### 9.6 Memory-like properties
NK cells lack rearranged receptors, but show forms of **innate-like memory**:
- **Adaptive NK cells**: clonal-like expansion of **Ly49H⁺ NK cells** in mouse CMV infection and **NKG2C⁺ NK cells** in human CMV infection.
- **Cytokine-induced memory-like (CIML) NK cells**: brief exposure to IL-12 + IL-15 + IL-18 yields enhanced IFN-γ responses upon restimulation.
- **Hapten- and virus-specific liver-resident NK memory** has been described in mice.

### 9.7 NK cells vs. cytotoxic T cells (CD8⁺)
| Feature | **NK cells** | **CD8⁺ CTLs** |
|---|---|---|
| Immunity | Innate | Adaptive |
| Antigen receptor | Germline-encoded (KIR, NKG2D, NCRs…); no V(D)J | TCR generated by V(D)J recombination |
| Antigen recognition | Balance of activating vs. inhibitory ligands; missing-self; IgG via CD16 | Specific peptide on MHC class I |
| MHC I effect | **Low or absent MHC I** promotes killing | **MHC I presenting peptide** is required |
| Response time | Hours to days; no prior priming needed | Days (needs priming and clonal expansion) |
| Memory | Limited / innate-like (adaptive NK, CIML) | Classical, antigen-specific memory |
| Killing machinery | Perforin, granzymes, FasL, TRAIL | Perforin, granzymes, FasL |
| Key markers | CD3⁻ CD56⁺ (CD16⁺ in the dim subset), NKp46 | CD3⁺ CD8⁺ TCR⁺ |

### 9.8 NK cells in cancer
- NK cells provide **tumor immunosurveillance** and limit **metastatic spread**; higher NK-cell infiltration correlates with better outcomes in several cancers.
- **Evasion mechanisms:** shedding of NKG2D ligands (e.g., soluble MICA), **TGF-β**-mediated downregulation of NKG2D and NKp30, upregulation of **HLA-E**/HLA-G, expression of checkpoint ligands, hypoxia and metabolic suppression in the tumor microenvironment, and NK-cell **exhaustion/dysfunction**.

### 9.9 Clinical relevance
- **Primary NK-cell deficiencies** (rare): recurrent severe **herpesvirus** infections (e.g., CD16 deficiency, *GATA2* deficiency, *MCM4* deficiency).
- **Familial hemophagocytic lymphohistiocytosis (HLH)**: defective cytotoxic granule function (*PRF1*, *UNC13D*, *STX11*, *STXBP2*) in NK and CD8⁺ T cells.
- **Haploidentical hematopoietic stem cell transplantation**: **KIR–HLA mismatch** can generate alloreactive NK cells with antileukemic activity.
- **Therapeutic strategies:** antibodies that act via **ADCC**, **CAR-NK cells** (e.g., from cord blood or iPSCs, often engineered with IL-15), **NK cell engagers** (BiKEs/TriKEs), cytokine therapy (IL-15 superagonists, IL-2), and **checkpoint blockade** targeting NK receptors (e.g., **anti-NKG2A, monalizumab**; **anti-KIR, lirilumab**).

---

## 10. Innate Lymphoid Cells (ILCs)

- **ILCs** are tissue-resident innate lymphocytes that lack antigen-specific receptors (lineage-negative) and mirror T-cell subsets in their cytokine and transcription factor profiles:
  - **ILC1** (T-bet, IFN-γ) ↔ Th1
  - **NK cells** (T-bet, EOMES; cytotoxic) ↔ CD8⁺ CTLs; see [[#9. NK Cells]]
  - **ILC2** (GATA3, IL-5, IL-13) ↔ Th2
  - **ILC3** (RORγt, IL-22, IL-17) ↔ Th17; includes **LTi cells** important for lymphoid organogenesis
- They bridge innate and adaptive immunity, especially in barrier tissues (gut, lung, skin), responding quickly to alarmins and cytokines (IL-25, IL-33, TSLP, IL-1β, IL-23).
- Unconventional T cells (γδ, NKT, MAIT) are covered in section 6.8.

---

## 11. Tolerance and Immune Regulation

| Mechanism | Description |
|---|---|
| **Central tolerance** | Clonal deletion/receptor editing in thymus (T) and bone marrow (B); AIRE-mediated antigen display |
| **Peripheral tolerance** | Anergy, deletion (Fas-mediated AICD), Treg suppression, immune-privileged sites, checkpoint receptors |
| **Ignorance** | Self-reactive cells never encounter their antigen |

Failure leads to **autoimmunity** (e.g., type 1 diabetes, rheumatoid arthritis, SLE, multiple sclerosis, myasthenia gravis).

---

## 12. Clinical Relevance

### Immunodeficiencies
- **SCID**: RAG1/2, IL2RG (X-linked, common γ chain), ADA deficiency
- **DiGeorge syndrome (22q11.2 deletion)**: thymic hypoplasia → T-cell deficiency
- **X-linked agammaglobulinemia (XLA)**: BTK mutation → absent B cells
- **CVID**, selective IgA deficiency
- **HIV/AIDS**: CD4⁺ T-cell depletion

### Malignancies of lymphoid origin
- **Leukemias**: ALL (B- or T-lineage), CLL
- **Lymphomas**: Hodgkin (Reed–Sternberg cells), non-Hodgkin (DLBCL, follicular, Burkitt, mantle cell, etc.)
- **Multiple myeloma**: malignant plasma cells
- Translocations juxtaposing oncogenes to Ig loci are common (e.g., **t(8;14) MYC–IGH** in Burkitt; **t(14;18) BCL2–IGH** in follicular lymphoma).

### Therapeutic applications
- **Immune checkpoint inhibitors** (anti-PD-1/PD-L1, anti-CTLA-4, anti-LAG-3)
- **CAR-T cells** (engineered T cells, e.g., anti-CD19, anti-BCMA)
- **Bispecific T-cell engagers** (e.g., blinatumomab)
- **NK-cell-based therapies** (CAR-NK, NK cell engagers, anti-NKG2A/monalizumab); see [[#9. NK Cells]]
- **Monoclonal antibodies** (rituximab anti-CD20, etc.)
- **Vaccines** (exploit memory and affinity maturation)
- **Immunosuppressants** (calcineurin inhibitors, mTOR inhibitors, anti-CD3, belatacept)

---

## 13. Lymphocytes in Omics and Computational Work

### Common marker genes (RNA-level, useful for annotation)
| Population | Typical markers |
|---|---|
| T cells (pan) | *CD3D, CD3E, CD3G, CD2, TRAC* |
| CD4⁺ T | *CD4, IL7R, CCR7* (naive/CM), *CD40LG* |
| CD8⁺ T | *CD8A, CD8B, GZMK, GZMB, PRF1, NKG2D* |
| Treg | *FOXP3, IL2RA, CTLA4, IKZF2* |
| Tfh | *CXCR5, PDCD1, BCL6, ICOS, CXCL13* |
| Exhausted T | *PDCD1, HAVCR2, LAG3, TIGIT, TOX, ENTPD1* |
| Naive/memory | *SELL, CCR7, TCF7, LEF1* / *CD44, IL7R, KLRB1* |
| B cells | *MS4A1 (CD20), CD79A, CD79B, CD19, PAX5, CD74* |
| Naive vs memory B | *IGHD, TCL1A, FCER2* vs *CD27, AIM2, TNFRSF13B* |
| Germinal center B | *BCL6, AICDA, RGS13, MKI67* |
| Plasma cells | *SDC1 (CD138), JCHAIN, MZB1, XBP1, PRDM1, IGHG/IGHA* |
| NK cells | *NKG7, GNLY, KLRD1, NCAM1, FCGR3A* |

### Repertoire sequencing
- **TCR-seq / BCR-seq (AIRR-seq)** profiles CDR3 sequences, V/J gene usage, clonality and diversity.
- Metrics: clonotype frequency, **Shannon/Simpson diversity**, **clonal expansion**, SHM load and **lineage trees** (B cells).
- Single-cell approaches (10x 5′ + V(D)J) pair **transcriptome with paired α/β or H/L chains**.
- Common tools: **MiXCR, Immcantation (Change-O, SHazaM, Alakazam), scirpy, scRepertoire, TRUST4, IgBLAST, VDJtools**.
- Specificity inference: **TCRdist, GLIPH2, ERGO, DeepTCR**; epitope databases such as **VDJdb, IEDB, McPAS-TCR**.

### Immune deconvolution and infiltration analysis
- Bulk RNA-seq tools estimate immune composition: **CIBERSORT(x), xCell, MCP-counter, TIMER, quanTIseq, EPIC**, and signature-based scoring (ssGSEA).
- State-/ecotype-level approaches (e.g., EcoTyper) combine cell-type abundance with transcriptional states across tumors.
- Typical readouts relate CD8⁺ T-cell infiltration, Treg fraction, B-cell/plasma cell signatures and TLS signatures to prognosis and checkpoint-therapy response.

### Other relevant data types
- **Flow/mass cytometry (CyTOF)** and **CITE-seq** for surface-protein phenotyping.
- **ATAC-seq** for chromatin accessibility in lymphocyte subsets.
- **Spatial transcriptomics** and multiplexed imaging for TLS and niche organization.

---

## 14. Quick Comparison Table

| Feature | T cells | B cells |
|---|---|---|
| **Site of maturation** | Thymus | Bone marrow |
| **Antigen receptor** | TCR (αβ or γδ) | BCR (membrane Ig) |
| **Antigen recognition** | Peptide presented on MHC (processed) | Native, soluble or surface antigen (proteins, polysaccharides, lipids, nucleic acids) |
| **Co-receptors** | CD4 or CD8 | CD19/CD21/CD81 |
| **Signaling chains** | CD3 (ITAM) | Igα/Igβ (CD79a/b, ITAM) |
| **Main immunity type** | Cell-mediated | Humoral (antibodies) |
| **Effector cells** | CTLs, Th subsets, Tregs | Plasma cells |
| **Somatic hypermutation** | No | Yes (AID-dependent) |
| **Class switching** | No | Yes |
| **Memory** | T_CM, T_EM, T_RM, T_SCM | Memory B cells, long-lived plasma cells |
| **Characteristic markers** | CD3, CD4/CD8, TCR | CD19, CD20, CD79a/b, surface Ig |
| **Selection checkpoints** | β-selection, positive/negative selection | Pre-BCR checkpoint, central tolerance |
| **Recirculation** | Naive T: blood ↔ nodes; memory subsets in tissues | Naive B: blood ↔ follicles |

---

## Key Takeaways

- The **lymphoid system** is organized into primary organs (bone marrow, thymus) for development and secondary organs (lymph nodes, spleen, MALT) for immune initiation, connected by **lymph and blood circulation**.
- **T cells** mature in the thymus, recognize peptide–MHC through the TCR, and orchestrate or execute cell-mediated immunity (helper, cytotoxic, regulatory subsets).
- **B cells** mature in the bone marrow, recognize native antigen through the BCR, and differentiate into antibody-secreting plasma cells and memory B cells, refined by **somatic hypermutation and class switching** in germinal centers.
- **T–B collaboration** (Tfh, CD40L–CD40) is central to high-affinity, long-lived antibody responses.
- **NK cells** are innate lymphocytes that kill virally infected and tumor cells by integrating activating and inhibitory signals (missing-self, stress ligands, ADCC) without prior sensitization, and they shape adaptive responses through IFN-γ.
- Tolerance mechanisms prevent autoimmunity; their failure, or malignant transformation of lymphocytes, underlies many diseases—and increasingly, these cells are therapeutic tools themselves.
