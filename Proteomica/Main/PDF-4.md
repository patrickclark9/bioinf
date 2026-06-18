Tutti gli spettrometri di massa misurano le molecole ins tati ionizzati. Tutti i valori determinati da MS sono relativi al rapporto m/z:
$m/z = (m,+(mA\cdot z)) / z$

## MALDI/TOF

Il MALDI/TOF è ottimo per il PMF (Peptide mass Fingerprinting), in quanto veloce, facile da misurare, tollerante ai sali (più rispetto agli altri metodo -> Crosta bianca), funziona relativamente bene anche con molecole a più grande peso molecolare, non ci sono limiti temporali -> Campione su supporto stabile, e genera principalmente ioni +1, rari ioni multicarica.

Il sistema presenta alcuni svantaggi -> Elevata accuratezza richiede calibrazione, MS/MS è complessa da effettuare con MALDI, il segnale può essere soppresso in miscele complesse, Le condizioni di cristallizazione influenzano i risultati.

![[Pasted image 20260618083515.png| MALDI Tryptic Digest]]

## Elettrospray
È perfetta per MS/MS, dato che può essere accoppiato direttamente a HPLC (in fase inversa), e genera ioni 2/3+.

Svantaggi -> L'introduzione di campioni è più complessa, l'analisi è più complessa dati gli ioni 2+ e 3+, one-shot analysis -> limiti di tempo, il picco sparisce, e bassa tolleranza agli agenti contaminanti.

Il 2+/3+ per peptidi triptici è molto utile, dato che la tripsina taglia il C terminale vicino a Lys e Arg, quindi ogni peptide ha un residuo basico al suo C-terminale (Lys K o Arg R), oltre ad un N-terminale libero -> Almeno due siti di protonazione

| Charge state (z) | Spacing between isotope peaks |
| ---------------- | ----------------------------- |
| 1+               | Δm = 1.0 Da                   |
| 2+               | Δm = 0.5 Da                   |
| 3+               | Δm = 0.33 Da                  |
La regola generale: $z = 1 / \Delta m_{\text{isotope}}$

## MS vs MS/MS
L'MS è un flusso:
- Produzione di Ioni
- Separazione di Ioni
- Detection
L'MS/MS:
- Produzione di Ioni
- Separazione di Ioni (selezione del parent)
- Frammentazione CID -> Generazione daughter
- Separazione degli ioni (i daughter)
- Detection

Fisicamente, MS/MS non è altro che un tandem MS - MS:
- MS1 -> Selezione dei parent -> Si selezionano ioni ad un particolare m/z. MS1 è una sorgente ionica per MS2 sostanzialmente
- Collision cell (Gas neutrale ad elevata pressione He, Ar, N2) -> Energia cinetica convertita ad Energia interna porta alla rottura di legami
- MS2 analizza gli ioni frammentati dalla collision cell
In MS1 si va a ionizzare, poi uno ione è selezionato da un particolare sistema (quadrupolo, settore magnetico, ion cyclotron resonance). Solo un tipo di ione passa nella regione della camera di collisione
In MS2, gli ioni daughter vengono rilevati, e lo spettro finale è composto dai picchi degli ioni selezionati e di tutti i suoi daughter
![[Pasted image 20260618090804.png]]

Il principio di MS/MS è reazioni filiate -> Lo spettro di un composto complesso è difficilmente interpretabile si osservano molti picchi è i più importanti corrispondono al maggior costituente, rendendo complessa l'identificazione di un preciso composto nello spettro della miscela, ma selezionando un singolo precursore e frammentadolo si ottiene uno spettro diagnostico per la struttura di una molecola.

MS/MS risulta nell'acquisizione quindi di informazioni di pseudo sequenza per molteplici peptidi prodotti dalla tripsina, in aggiunta all'informazione di massa del peptide intatto.
Serve quindi uno strumento in grado di isolare e frammentare gli ioni, oltre ad MS. 
Risulta nell'acquisizione di molteplici file ortogonali (1 spettro per peptide) - Roughly **one MS/MS spectrum per selected peptide precursor**

- **MS1** → gives **intact peptide masses**
- **MS/MS** → gives **fragment ions → sequence info**
- Done for **many peptides** in a sample
- **“intact” relative to MS/MS**, meaning it hasn’t yet been broken inside the Collision Chamber
Spesso si osservano ion series y e b  negli spettri di frammentazione di peptidi triptici MS/MS.
 The y₁ ion at 147 Da = Lys or 175 Da = Arg is characteristic (terminal basic residue from trypsin cleavage)
CID rompe legami peptidici lungo il backbone, risultanto in frammenti ionici classificati sulla base di quale terminale ritengono e quali legami sono rotti:

| Ion series | Terminus retained | Bond broken | Notes                         |
| ---------- | ----------------- | ----------- | ----------------------------- |
| **a**      | N-terminal        | Cα–CO       | = b − 28 Da (CO loss)         |
| **b**      | N-terminal        | CO–N        | Most common N-terminal series |
| **c**      | N-terminal        | N–Cα        | Less common                   |
| **x**      | C-terminal        | CO–N        | Rare                          |
| **y**      | C-terminal        | N–Cα        | Most common C-terminal series |
| **z**      | C-terminal        | Cα–CO       | Less common                   |
![[Pasted image 20260618093635.png]]
![[Pasted image 20260618093642.png]]

## Identificazione di proteine per spettrometria di massa

In generale, la tripsina digerisce una proteina in un insieme di peptidi con massa prevedibile. Il pattern specifico di masse dei peptidi è effettivamente una fingerprint unica (o quasi unica)per una proteina
![[Pasted image 20260618094554.png]]

- Protein band (SDS-PAGE)
    ↓ in-gel trypsin digest
- Peptide mixture
    ↓ MALDI-TOF MS
- Peak list (m/z values of peptide ions)
    ↓ database search (in silico digest of all proteins)
- Protein identification

Data una lista di picchi, li andiamo a confrontare confrontare contro liste di masse ioniche di peptidi generati da un database di sequenze proteiche

| Accuracy | Tolerance (Da) | Hits (example) |
|---|---|---|
| Low | 1.0 | 478 |
| Medium | 0.1 | 164 |
| High | 0.01 | 25 |
| Very high | 0.001 | 4 |
| Ultrahigh | 0.0001 | 2 |

→ **Mass accuracy is the single biggest determinant of search specificity in PMF.**

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
- **Fixed modifications**: Carbamidomethyl (C) — from iodoacetamide alkylation during gel prep. Dipende dalla tecnica utilizzata in preparazione. Possono anche non esserci modificazioni Complete/Fixed
- **Variable modifications**: Oxidation (M) — Met side-chain oxidation is common artifact
- **Mass values**: MH⁺ (monoisotopic preferred for high-res instruments)
- **Tolerance**: in Da or ppm

I dati possono essere importati da file oppure manualmente si inserisce la lista di picchi m/z nel campo query.

ProFound è molto simile. Le modificazioni parziali sono tipicamente Methionine Oxidation, ma se ne possono aggiungere altre sia in Profound sia in MASCOT
### Mascot Scoring
Score = −10 × log(P), where P = probability that the match is random.  
Scores > 50–63 are typically significant (p < 0.05) — threshold depends on database size.

### Output: Sequence Coverage Map
Matched peptides highlighted in the protein sequence. **Sequence coverage (%)** = fraction of protein covered by matched peptides.
