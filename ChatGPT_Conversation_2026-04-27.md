# Transcriptome Assemblers Overview

**Date:** 2026-04-27
**Source:** [chat.openai.com](https://chatgpt.com/c/69ef7dd1-e488-83eb-8aa8-5b3643e35242)

---

### **You**

what do we use Trinity, Cufflinks etc Transcriptome assemblers for

---

### **ChatGPT**

Tools like Trinity and Cufflinks are used in RNA-seq analysis to reconstruct transcripts—basically figuring out what RNA molecules are present in a sample and in what form.
But they’re not identical in purpose, and that distinction matters.

What transcriptome assemblers are for
At a high level, these tools help you:
1. Rebuild full transcripts from short reads
RNA-seq gives you millions of short fragments. Assemblers stitch them together to reconstruct:

full-length mRNAs

splice variants (isoforms)

non-coding RNAs

2. Discover new transcripts and isoforms
Especially important when:

the genome is incomplete

annotations are poor

you're working with non-model organisms

They can reveal:

novel genes

alternative splicing patterns

3. Quantify expression at transcript level
They estimate how much each transcript is expressed (not just gene-level counts).

Trinity vs Cufflinks (key difference)
Trinity

De novo assembly

Does NOT need a reference genome

Builds transcripts purely from read overlaps (k-mers / de Bruijn graphs)

Best for:

non-model organisms

missing or poor genome assemblies

👉 Output: a reconstructed transcriptome FASTA

Cufflinks

Reference-guided assembly

Requires aligned reads (e.g., from HISAT2/TopHat)

Reconstructs transcripts based on genome coordinates

Also quantifies expression (FPKM)

👉 Best for:

well-annotated genomes (human, mouse, etc.)

refining gene models and isoforms

Where they fit in a pipeline
Typical workflows:
De novo (no genome)
RNA-seq → Trinity → transcriptome → annotation → expression analysis
Reference-based
RNA-seq → align (HISAT2) → Cufflinks → transcript models → differential expression

Important nuance (often misunderstood)
They are not just for expression analysis.
Their primary role is structure reconstruction (what transcripts exist), while quantification is secondary.

Modern note
Some pipelines now favor faster/alternative tools like:

StringTie (successor to Cufflinks)

Salmon / Kallisto (quantification without full assembly)

One-line takeaway
Transcriptome assemblers are used to reconstruct and characterize the full set of RNA transcripts (including isoforms) from sequencing data, either with or without a reference genome.

If you want, I can map this directly to your current RNA-seq workflow (especially if you're using PLINK/scikit-allel downstream—you might be mixing genomics and transcriptomics steps).

---

### **You**

differential expression in the sense of which isoforms are expressed or actual gene expression

---

### **ChatGPT**

Short answer: both exist—but they are different analyses, and people often conflate them.

1) Gene-level differential expression (most common)
This is the “classic” DE analysis:

You collapse all transcripts (isoforms) of a gene into one value

Then test if the total expression of the gene changes between conditions

Typical tools:

DESeq2

edgeR

👉 Answers:

“Is gene X up/downregulated?”

👉 Ignores:

which isoform is responsible

2) Isoform / transcript-level differential expression
Here you treat each transcript separately:

Each isoform gets its own expression estimate

You test which isoforms change between conditions

Tools:

Cufflinks / Cuffdiff

Salmon + downstream tools like sleuth

Kallisto

👉 Answers:

“Isoform A increases, isoform B decreases”

3) Differential transcript usage (DTU) ← most precise concept
This is where things get interesting:

Total gene expression may stay the same

But the relative proportions of isoforms change

Example:

Condition A: 90% isoform 1, 10% isoform 2

Condition B: 20% isoform 1, 80% isoform 2

Gene-level DE → no change

Isoform usage → major change

Tools:

DRIMSeq, DEXSeq, IsoformSwitchAnalyzeR

👉 Answers:

“Splicing regulation changed”

Why this distinction matters
Because different biology is captured:

Gene-level DE → transcriptional regulation

Isoform-level DE / DTU → alternative splicing regulation

If you only do gene-level analysis, you can completely miss isoform switching.

Where assemblers fit (linking back to your question)
Tools like Trinity and Cufflinks:

reconstruct isoforms → necessary for isoform-level analysis

provide transcript models → used for quantification

But:

DE testing itself is usually done after, with specialized statistical tools

Practical takeaway
If you had to choose:

Most studies → gene-level DE (robust, simpler)

If you care about splicing → isoform-level or DTU (harder, noisier, more informative)

If you tell me your dataset (organism + depth + paired-end or not), I can tell you whether isoform-level analysis is actually worth it—because in many datasets it’s statistically shaky.

---

### **You**

So a standard pipeline of QC -> STAR -> featureCunts -> Deseq2 for gene expression, introduce something like cufflinks to quantify isoforms  so QC -> STAR -> Cufflink -> (mapper isoform aware) -> differential analysis of isoforms

---

### **ChatGPT**

You’re close, but that pipeline has a conceptual mismatch. Cufflinks doesn’t replace the aligner or sit between two mapping steps—it uses an alignment to assemble/quantify transcripts. Also, you don’t run a second “isoform-aware mapper” after it.
Let’s straighten it out.

Your gene-level pipeline (already correct)

QC → STAR → featureCounts → DESeq2

✔ Produces gene-level DE
✔ Robust, standard

What changes for isoform-level analysis
You don’t insert a second mapper—you change how you quantify expression after alignment.

Option A — “classic” Cufflinks-style (older, less used now)

QC → STAR

→ Cufflinks (assemble + quantify transcripts)

→ Cuffmerge (merge assemblies across samples)

→ Cuffdiff (isoform-level differential expression)

✔ Does transcript reconstruction + quantification
❗ Less used today (statistically weaker, slower)

Option B — modern and preferred (no assembly step)

QC → Salmon or Kallisto

→ transcript-level counts

→ DE at transcript level (e.g. sleuth / tximport + DESeq2)

✔ No alignment needed (or optional lightweight alignment)
✔ Much faster and often more accurate for isoforms

Option C — hybrid (keep STAR, but quantify isoforms)
If you want to keep your existing alignment:

QC → STAR

→ StringTie (modern replacement for Cufflinks)

→ transcript abundances

→ downstream DE / DTU analysis

✔ Good compromise
✔ Uses genome alignment + isoform-aware quantification

The key correction to your idea
You wrote:

QC → STAR → Cufflinks → (mapper isoform aware) → differential analysis

❌ Problems:

Cufflinks already uses the STAR alignment → no second mapper needed

There is no “mapper isoform aware” step after Cufflinks

Differential analysis is done on counts/abundances, not by remapping

Clean corrected pipelines
Gene-level
QC → STAR → featureCounts → DESeq2
Isoform-level (reference-based)
QC → STAR → StringTie → transcript quantification → DE / DTU
Isoform-level (best modern approach)
QC → Salmon/Kallisto → transcript quantification → DE / DTU

Subtle but important point

featureCounts → gene counts (loses isoform info)

Salmon/StringTie → transcript counts (preserves isoforms)

Once you collapse to gene counts, you cannot recover isoform-level information.

Practical advice (based on real workflows)
If your goal is isoforms:

Don’t bolt Cufflinks onto a gene-level pipeline

Instead, switch quantification strategy entirely

👉 Most people today would go:

Salmon → tximport → DESeq2 (gene-level and transcript-level possible)

If you want, I can sketch a pipeline tailored to your data (read length, strandedness, organism), because isoform analysis can fall apart quickly if the setup isn’t right.

---

### **You**

then salmon/kallisto/cufflinks whatever are only used in isoform quantification>

---

### **ChatGPT**

Not quite—they’re mainly designed for transcript/isoform-level quantification, but they’re not limited to that. The distinction is about what resolution you keep, not a strict “isoform-only” vs “gene-only” split.

What these tools fundamentally do
Tools like:

Salmon

Kallisto

Cufflinks

👉 estimate expression at the transcript level first
That’s their core job.

But here’s the key point
➤ You can always go down in resolution (transcript → gene)
From transcript abundances, you can:

sum transcripts belonging to the same gene

perform gene-level DE

Example workflow:

Salmon → transcript counts → tximport → gene counts → DESeq2

✔ You get gene-level results
✔ While still retaining isoform information if needed

➤ But you cannot go up (gene → transcript)
If you start with:

featureCounts

👉 you’ve already:

collapsed reads onto genes

lost isoform resolution

❌ No way back to isoforms

So the real classification
Gene-centric tools

featureCounts
→ directly produce gene counts
→ no isoform detail

Transcript-centric tools (Salmon, Kallisto, Cufflinks)

produce transcript-level estimates

can be used for:

isoform DE ✅

DTU analysis ✅

gene-level DE (after summarization) ✅

Where Cufflinks differs slightly

Cufflinks also:

reconstructs transcripts (not just quantifies)

while Salmon / Kallisto:

rely on a reference transcriptome

don’t assemble new isoforms

Practical takeaway

These tools are not only for isoform analysis

They are isoform-aware quantifiers that:

preserve more information upfront

give you flexibility later

👉 Think of them as:

“high-resolution quantification tools” rather than “isoform-only tools”

What most people do today
Even for gene-level DE:

Use Salmon

Then summarize to genes

Then run DESeq2

Because:
✔ fast
✔ accurate
✔ future-proof (you can still analyze isoforms later)

One-line answer to your question
❌ No — they are not only for isoform quantification
✔ They quantify at the transcript level, but can be used for both isoform and gene-level analyses

If you want, I can show you exactly how tximport aggregates Salmon output into DESeq2-ready gene counts—that’s usually the missing conceptual bridge.

---

### **You**

show tximport

---

### **ChatGPT**

Here’s the practical bridge from transcript-level quantification (e.g. Salmon) to gene-level DE with DESeq2 using tximport.

Minimal working example (R)
1. Install & load packages

\`\`\`
Rif (!requireNamespace("BiocManager", quietly = TRUE))  install.packages("BiocManager")BiocManager::install(c("tximport", "DESeq2", "readr"))library(tximport)library(DESeq2)library(readr)
\`\`\`

2. Prepare your inputs
A) Salmon output files
After running Salmon, each sample has:

\`\`\`
sample1/quant.sfsample2/quant.sf...
\`\`\`

Create a named vector:

\`\`\`
Rsamples <- c("sample1", "sample2", "sample3", "sample4")files <- file.path("salmon", samples, "quant.sf")names(files) <- samples
\`\`\`

B) Transcript → gene mapping (CRUCIAL STEP)
You need a table mapping transcripts to genes.
Example (tx2gene.csv):

\`\`\`
TXNAME,GENEIDENST00001,ENSG00001ENST00002,ENSG00001ENST00003,ENSG00002
\`\`\`

Load it:

\`\`\`
Rtx2gene <- read\_csv("tx2gene.csv")
\`\`\`

👉 You can generate this from:

GTF (e.g. using biomaRt, GenomicFeatures)

Ensembl annotation

3. Import with tximport

\`\`\`
Rtxi <- tximport(files,                type = "salmon",                tx2gene = tx2gene,                countsFromAbundance = "lengthScaledTPM")
\`\`\`

What this does:

Reads transcript-level estimates

Aggregates them to gene-level counts

Corrects for transcript length bias

4. DESeq2 pipeline

\`\`\`
R# sample metadatacoldata <- data.frame(  row.names = samples,  condition = c("ctrl", "ctrl", "treated", "treated"))dds <- DESeqDataSetFromTximport(txi,                               colData = coldata,                               design = ~ condition)dds <- DESeq(dds)res <- results(dds)head(res)
\`\`\`

5. Output
You now have:

gene-level differential expression

derived from transcript-aware quantification

Important knobs (people often miss these)
countsFromAbundance options:

\`\`\`
R"no"                # raw estimated counts"scaledTPM"         # scaled TPM"lengthScaledTPM"   # BEST default (accounts for transcript length)
\`\`\`

👉 Use "lengthScaledTPM" in most cases

If you ALSO want isoform analysis
Just skip aggregation:

\`\`\`
Rtxi <- tximport(files, type = "salmon", txOut = TRUE)
\`\`\`

Now:

rows = transcripts

you can do transcript-level DE (less robust)

Conceptual summary

Salmon → transcript abundances

tximport → aggregates to genes

DESeq2 → statistical testing

Common mistakes (worth avoiding)
❌ Wrong or missing tx2gene → garbage gene counts
❌ Mixing transcriptome versions (Salmon index ≠ annotation)
❌ Using featureCounts + tximport together (redundant / wrong logic)

If you want, I can show:

how to generate tx2gene from a GTF cleanly

or how to keep both gene-level and isoform-level analyses in the same pipeline without duplicating work

---

### **You**

but if i need DE only, not interested in which isoform is expressed, just that the gene is expressed, using Salmon/Kallisto looks slower and less accurate, since at least kallisto employs pseudoalignment that even if fairly accurate, is not a full replacer for STAR

---

### **ChatGPT**

That’s a very common intuition—but it’s a bit outdated and slightly off in a couple of key ways.
Short version:
If you only care about gene-level DE, using Salmon or Kallisto is not slower and is often just as accurate (sometimes more) than a STAR + featureCounts pipeline.

1) Speed: this part is actually backwards

Salmon/Kallisto → much faster (minutes per sample)

STAR + featureCounts → slower (full alignment + counting)

Why:

Pseudoalignment avoids base-by-base alignment

Works at the transcript compatibility level instead of exact mapping

👉 In practice, Salmon is usually faster than STAR, not slower.

2) Accuracy: where your concern is valid (but nuanced)
You’re right that:

pseudoalignment ≠ full alignment

But the key question is:
does that difference matter for gene-level DE?
Evidence from benchmarks (what people actually see)

For gene-level counts, Salmon/Kallisto:

are highly concordant with STAR-based pipelines

sometimes outperform them due to better bias correction

They explicitly model:

GC bias

fragment length bias

sequence-specific bias

👉 These are things a simple STAR → featureCounts pipeline does not correct.

3) Where STAR still wins
Your instinct is correct in certain cases:
Use STAR if you need:

splice junction discovery

novel transcript detection

variant calling (RNA-seq SNPs)

fusion detection

genome-centric analyses

👉 Pseudoalignment tools cannot replace this.

4) For pure gene-level DE (your use case)
You have two solid options:
Option A — classic

STAR → featureCounts → DESeq2

✔ Very robust
✔ Well understood
✔ Slightly simpler conceptually

Option B — modern (increasingly standard)

Salmon → tximport → DESeq2

✔ Faster
✔ Bias-aware
✔ Keeps isoform info (even if you don’t use it)

5) The real tradeoff (this is the important part)
It’s not:

alignment vs pseudoalignment

It’s:

genome-based counting vs transcript-aware quantification

Subtle but important difference

featureCounts

assigns reads to genes

struggles with multi-mapping reads

discards ambiguity

Salmon/Kallisto

probabilistically assign reads across transcripts

then aggregate to genes

handle ambiguity more gracefully

👉 This can actually improve gene-level estimates.

6) When your pipeline choice actually matters
Differences show up more when:

many paralogous genes

lots of isoforms

short reads

low-quality annotations

Otherwise:
👉 results are usually very similar

7) Practical recommendation (no fluff)
If your goal is strictly:

“Which genes are differentially expressed?”

Then:

Your STAR → featureCounts → DESeq2 pipeline is perfectly valid

Switching to Salmon is optional, not required

But:
👉 It’s not less accurate
👉 It’s not slower
👉 It’s often more statistically principled

Bottom line

❌ “Pseudoalignment is less accurate for DE” → oversimplified

✔ “It trades exact alignment for probabilistic assignment, often without loss of DE accuracy”

If you want, I can show you a side-by-side comparison (same dataset through STAR vs Salmon) so you can see how similar the DE results actually are—that’s usually what convinces people.

---

### **You**

certain tools report as aligner a BWA - a burrows-wheeler aligner. Isn't burrows-wheeler an indexing strategy for database

---

### **ChatGPT**

You’re picking up on a real subtlety in terminology. Burrows–Wheeler isn’t an aligner itself—it’s a data transformation/indexing strategy. But tools like BWA use it as the core of how they enable fast alignment, which is why they’re called aligners.

What Burrows–Wheeler actually is
The Burrows–Wheeler transform (BWT):

Rearranges a string (e.g. a genome) into a form that is:

highly compressible

efficiently searchable

By itself:

❌ does not align reads

❌ does not map sequences

👉 It’s just a clever way to index text

How it becomes an “aligner”
Tools like BWA combine:

BWT + FM-index

fast substring lookup in the genome

Search algorithms

find where a read could map

Scoring / heuristics

allow mismatches, gaps, etc.

👉 Together, this pipeline performs alignment

Why people call it a “Burrows–Wheeler aligner”
Because:

The core data structure enabling fast mapping is BWT-based

It distinguishes these tools from older approaches (like hash tables)

So:

“Burrows–Wheeler aligner” =
an aligner that uses a BWT/FM-index under the hood

Analogy (quick intuition)

BWT = a super-efficient index in a book

BWA = the full system that:

uses the index

finds matching passages

decides the best match

Related tools
Other aligners using similar ideas:

Bowtie

Bowtie2

They also rely on BWT/FM-index structures.

Important distinction (ties back to RNA-seq)

BWA:

mainly for DNA-seq (no splicing awareness)

STAR:

not BWT-based

optimized for splice junctions

👉 That’s why you wouldn’t use BWA for RNA-seq alignment.

Bottom line
✔ You’re correct: Burrows–Wheeler is an indexing/search strategy
✔ But in practice, tools that use it to perform mapping are called aligners

If you want, I can walk through how BWT + FM-index actually finds a match step-by-step (it’s surprisingly elegant and shows why it’s so fast).

---

### **You**

but FM-index is full index in minute space, and its mainly mapping. Aligning != mapping

---

### **ChatGPT**

You’re absolutely right to draw that distinction—mapping and alignment are not the same thing. But in practice, most modern “aligners” (especially BWT/FM-index–based ones) do both, just in different stages.

Mapping vs alignment (clean distinction)
Mapping

Find candidate locations in the reference where a read could originate

Typically:

fast

approximate

may allow mismatches implicitly

👉 This is where the FM-index shines:

extremely memory efficient

very fast substring search

Alignment

Compute the exact base-to-base correspondence:

mismatches

insertions/deletions

Produces:

CIGAR strings

alignment scores

👉 Requires dynamic programming (e.g. Smith–Waterman–like steps)

What BWT/FM-index tools actually do
Take BWA:
Step 1 — Mapping (FM-index)

Use BWT + FM-index to:

rapidly find candidate genomic positions

allow mismatches via backtracking or seeding

Step 2 — Alignment (extension)

For each candidate:

run a local alignment step

compute exact match with gaps/mismatches

👉 This is often called “seed-and-extend”

Why the terminology gets blurred
Historically:

Early tools:

mapping and alignment were more separate concepts

Modern tools:

bundle both steps into one pipeline

So:

“aligner” = tool that outputs full alignments, even if internally it starts with mapping

Where your statement is exactly correct

“FM-index is mainly mapping”

✔ Yes. The FM-index:

supports fast pattern matching

does not compute alignments by itself

Where the nuance comes in

“Aligning ≠ mapping”

✔ Conceptually true
❗ But most tools:

map first using FM-index

then align locally

So:

FM-index ≠ aligner

but BWT-based aligners use FM-index as their mapping engine

Contrast with pseudoalignment (important connection)
Tools like:

Kallisto

Salmon

👉 Stop at the mapping-like stage:

identify compatible transcripts

do NOT perform base-level alignment

This is why:

they’re not considered full aligners

Big picture
StepFM-index roleNeeded forMapping✅ core toolall alignersAlignment❌ separate stepfull alignment tools

Bottom line

✔ FM-index = mapping/search engine

✔ Alignment = additional refinement step

✔ Tools like BWA combine both → hence called “aligners”

If you want, I can break down exactly how backtracking in the FM-index allows mismatches—that’s the part where “mapping” already starts to blur into approximate alignment.

---

### **You**

why is burrows wheeler not used for RNA

---

### **ChatGPT**

It’s not that Burrows–Wheeler isn’t used for RNA—it’s that plain BWT/FM-index aligners struggle with spliced reads, which is the defining feature of RNA-seq.

The core issue: splicing breaks contiguity
RNA-seq reads often:

span exon–exon junctions

skip introns entirely

So a read might look like:

\`\`\`
[exon1]----[exon2]
\`\`\`

But in the genome:

\`\`\`
[exon1]------intron------[exon2]
\`\`\`

👉 That read is not contiguous in the genome

Why this is a problem for BWT/FM-index
The Burrows–Wheeler transform + FM-index are designed for:

fast substring matching in a continuous sequence

They work best when:

the read ≈ a substring of the reference (with small mismatches)

❌ But spliced reads:

are split across distant genomic regions

require “jumps” over introns

What happens with a DNA aligner like BWA

It tries to align the read contiguously

Fails or:

soft-clips part of the read

produces suboptimal alignments

👉 It doesn’t model splicing

What RNA-seq aligners do differently
Tools like STAR:

explicitly search for splice junctions

allow:

large gaps (introns)

split alignments

They:

detect exon boundaries

align reads in pieces

Important nuance (this is where it gets interesting)
BWT is not fundamentally incompatible with RNA-seq.
In fact:

TopHat

HISAT2

👉 do use BWT/FM-index
But they add:

splice-aware logic

hierarchical indexing (in HISAT2)

junction discovery steps

So why people say “BWT isn’t used for RNA”
What they really mean is:

“Simple BWT aligners like BWA aren’t suitable for RNA-seq”

✔ Correct
❌ But misleading if taken literally

Big picture
Tool typeUses BWTSplice-awareRNA-seq suitableBWA✔❌❌Bowtie2✔❌❌ (alone)HISAT2✔✔✔STAR❌✔✔

Why STAR often wins anyway
Even though HISAT2 uses BWT:

STAR uses a different strategy (suffix arrays + seed stitching)

optimized for:

very fast splice junction detection

high sensitivity

👉 That’s why STAR is often preferred

Bottom line

✔ BWT/FM-index = great for contiguous sequence matching

❌ RNA-seq reads are often non-contiguous (spliced)

✔ Therefore, you need splice-aware extensions

So:

BWT isn’t “not used”—it just needs extra machinery to handle RNA biology

If you want, I can show how a split alignment is actually represented in a BAM (CIGAR strings like 50M100N50M)—that’s where the limitation of plain BWT becomes very concrete.

---

### **You**

what is bowtie2 used for, i only used to map chip-seq reads to reference

---

### **ChatGPT**

That’s actually a perfect use case—you’ve already seen exactly what Bowtie2 is best at.
But its role is broader than just ChIP-seq.

What Bowtie2 is fundamentally for
Bowtie2 is a general-purpose DNA read aligner that:

maps sequencing reads to a reference genome

allows mismatches and small indels

uses a Burrows–Wheeler transform + FM-index for speed and memory efficiency

👉 Think: short-read genomic alignment where splicing is NOT involved

Typical use cases
1) ChIP-seq (what you did)
✔ Ideal use case

reads come from DNA fragments

no splicing

need accurate genomic positions

2) ATAC-seq / DNase-seq

open chromatin assays

similar logic to ChIP-seq

✔ Bowtie2 works very well

3) Whole-genome / targeted DNA sequencing

resequencing

variant discovery (sometimes)

✔ though often replaced by BWA for variant calling

4) Metagenomics (sometimes)

mapping reads to microbial references

✔ depending on pipeline

Where Bowtie2 is NOT appropriate
RNA-seq (important)
❌ Not splice-aware

cannot handle exon–exon junctions

will misalign or soft-clip reads

👉 That’s why people use:

STAR

HISAT2

Bowtie vs Bowtie2 (quick distinction)

Bowtie

very fast

no gaps (or very limited)

Bowtie2

supports indels

more flexible

better for real-world data

Why Bowtie2 is still widely used in ChIP-seq
Because it hits a sweet spot:

fast enough

accurate enough

handles:

small indels

sequencing errors

produces clean, reliable alignments for peak calling

Subtle but important detail
In ChIP-seq, you usually care about:

where fragments came from (peaks)

not:

base-perfect alignment across splice junctions

👉 So Bowtie2 is perfectly matched to the biological question

One-line summary
Bowtie2 is a fast, general-purpose DNA aligner for mapping short reads to a genome when splicing is not involved—making it ideal for ChIP-seq, ATAC-seq, and similar assays.

If you want, I can compare Bowtie2 vs BWA vs STAR in terms of scoring models and when one subtly outperforms the others—that’s where the interesting tradeoffs show up.

---
