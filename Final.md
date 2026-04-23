
# Applicazioni di NGS

Alcune applicazioni delle piattaforme NGS sono:
## Sequenziamento DNA
- Risequenziamento Genomico (SNP, GWAS)
- De-novo sequencing
- Identificazioni di varianti strutturali del genoma
- Interazioni della cromatina 3D
- Epigenomica (stato cromatinico e metilazione)
- Metagenomica (analisi tassonomica di campioni ambientali)
## Sequenziamento RNA
- Analisi qualitativa e quantitativa del trascrittoma
- Identificazione e caratterizzazione di miRNA e altri ncRNA
- RNA Editing
- Metatrascrittomica (analisi funzionale di campioni ambientali)

## Genome Resequencing

Consiste nel sequenziare nuovamente l'intero genoma di una specie di cui si ha un genoma di reference, permettendo l'indetificazione di varianti come SNP, indel, e varianti strutturali

## Whole Genome Sequencing
Processo in cui si va a determinare l'intera sequenza del DNA di un genoma di un organismo , incluso cromosomale e mitocondriale.


## Target Enrinchment

L'arricchimento consiste nel catturare, o arricchire, specifiche regioni di interesse, che possono essere esoni, ncRNA, o specifici geni, prima del sequenziamento.
Le tecniche presentate sono utilizzate per l'arricchimento di DNA genomico, quindi non utilizzate per l'arricchimento di ncRNA. 
Per ncRNA si utilizzano tecniche differenti data la loro complessa e diversificata struttura.

### Array Hybridization
Approccio che consiste nell'utilizzare probe, piccoli olignonucleoitidi sintetici,  su un vetrino (array). DNA genomico viene introdotto sull'array, dove DNA target legherà i probe complementari sull'array, mentre il DNA non target viene rimosso. Il DNA catturato viene poi sequenziato
### In Solution Hybridization
Il metodo più comune utilizzato oggi. I probe vengono biotinilati (taggati), ed inseriti insieme al DNA genomico in soluzione. Dopo ibridizzazione, vengono utilizzati bead con streptavidina che lega la biotina, tirandosi i probe target in complesso con DNA di interesse, permettendo di rimuovere il resto del materiale genomico. 

### Molecular inversion probe
Oligonucleotide a singolo filamento prodotto cosi che le terminazioni siano complementari al DNA target. Quando si lega il probe, si inverte e forma un cerchio attorno al target. Una reazione di gap-filling e ligazione chiudono il cerchio. Solo i probe circolarizzati vengono sottoposti a PCR.
![[Pasted image 20260423183843.png]]

## Varianti strutturali
Varianti strutturali identificabili da seconda generazione:
- Mutazioni puntiformi
- Indel
- Delezioni omozigoti -> Copy Number variation
- Delezioni emizigoti -> Copy Number Variation
- Gain ->  Copy number Variation
- Punto di breakpoint di Traslocazioni
- Patogeni

Si sequuenziando e allineando i dati contro un genoma di riferimento al fine di creare un file BAM pronto per essere utilizzato. Nel variant calling di Varianti ereditarie, si fa utilizzo di 3 BAM, proband BAM, Madre BAM e Padre BAM. Si fa un joint-variant calling, in cui vengono analizzate SNV/Indel/SV/CNV. Segue un filtro di rimozione di artefatti, e conferma con una review manuale.
Per de Novo alterazioni bisogna rimuovere anche i falsi positivi.
Variant calling si può fare anche per varianti somatiche, utilizzando un BAM per Tumore ed un altro per controllo (normale).
Si cercano SNV/Indel/SV/CNA somatiche, si rimuovono gli artefatti, e si conferma manualmente che sia una variante.
Linee guida e standard per l'identificazione di varianti genetiche sono ancora in sviluppo. WES e WGS producono molti dati su numerose varianti genetiche, la maggior parte delle quali, nel contesto di uno studio su una particolare malattia, non sono rilevanti, dato che non hanno effetto funzionale sulle proteine o a livello sistemico. Da notare è che tutti presnetiamo un gran numero di varianti genetiche ereditarie e de novo mutazioni, ma una piccola frazione di queste effettivamente impatta la funzione proteica o sistemica (ad esempio mutazioni non senso).
L'annotazione di varianti ha come obiettivo produrre metadati ausiliari per variant call putative grezze filtrate per qualità, al fine di approfondire le varianti che probabilmente hanno un impatto funzionale o sistemico.