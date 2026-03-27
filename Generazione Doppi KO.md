
=== 1. Selezione dei Target e Progettazione della Libreria

- *Identificazione dei geni:* Sono stati selezionati *258 geni SLC espressi* nella linea cellulare HCT 116 (soglia di espressione > 1 trascritto per milione - TPM).

- *Progettazione degli sgRNA:* Sono state progettate guide specifiche per ogni gene (3 sgRNA per gene nel sistema Cas12a e 6 per gene nel sistema Cas9).

- *Combinazioni:* Gli sgRNA sono stati accoppiati in tutte le combinazioni possibili, generando una libreria di oltre un milione di coppie di guide per interrogare *33.153 combinazioni SLC-SLC* uniche.

- *Controlli:* Sono stati inclusi sgRNA mirati a recettori olfattivi (OR) per misurare l'effetto dei singoli knockout e coppie di geni con letalità sintetica già nota come controlli positivi.

  

=== 2. Trasduzione Lentivirale e Selezione

- *Produzione virale:* Le librerie combinatorie sono state clonate in vettori lentivirali e prodotte in cellule HEK293T.

- *Infezione pooled:* La popolazione di cellule HCT 116 è stata trasdotta con la libreria virale in modalità "pooled" (miscela totale).

- *Controllo dell'integrazione (MOI):* Si è utilizzato un *MOI (Molteplicità di Infezione) di circa 0,5*. Tale parametro è fondamentale per garantire statisticamente che ogni cellula integri stabilmente nel proprio genoma *una sola coppia di sgRNA*.

- *Selezione cellulare:* Le cellule trasdotte sono state sottoposte a selezione con *puromicina* per 5 giorni per eliminare i cloni privi di integrazione plasmidica.

  

=== 3. Monitoraggio della Fitness e Raccolta Dati

- *Crescita:* Le cellule sono state mantenute in coltura per un periodo fino a *5 settimane*.

- *Campionamento temporale:* Sono stati effettuati prelievi di campioni cellulari a intervalli regolari (tipicamente alle settimane 1, 2, 3 e 5) per monitorare l'evoluzione della popolazione.

- *Estrazione del DNA:* Per ogni intervallo, è stato estratto il DNA genomico (gDNA) dalla popolazione totale.

  

=== 4. Quantificazione e Analisi Statistica

- *Sequenziamento (NGS):* Le sequenze degli sgRNA sono state amplificate tramite PCR e contate mediante sequenziamento Illumina.

- *Calcolo dell'LFC:* L'abbondanza di ogni coppia di guide è stata confrontata con quella del plasmide iniziale per determinare il *Log2 Fold Change osservato* ($L F C_"obs"$).

- *Determinazione dell'interazione (dLFC):*

    - *LFC_exp:* Calcolato come somma degli effetti dei singoli knockout.

    - *dLFC:* Calcolato come differenza tra $L F C_"obs"$ e $L F C_"exp"$.

- *Scoring:* Un'interazione è stata definita *letalità sintetica* se il $d L F C$ era inferiore a -0,3 e statisticamente significativo ($p_"adj" < 0,1$), indicando che il doppio knockout era più deleterio della somma dei singoli effetti.


[Nature Doppio KO](https://www.nature.com/articles/s41467-025-67256-9)
[PMI -  CRISPR CAS 9 Double Knockout](https://pmc.ncbi.nlm.nih.gov/articles/PMC12691371/#abstract2)
