- Bias di PCR sui livelli di duplicazione, non sono le regione ripetute, che se amplificate, non hanno esattamente lo stesso inizio e la stessa fine
- bowtie2 da priorità all'allinemento delle estremità
- ![[Screenshot 2025-10-08 at 09.15.41.png]]
	- Blocco spesso: Esoni
	- Assenza di blocco o blocco stretto: Introni
	- Freccia: Forward o Reverse
	- Blocchetti leggermente più sottili: 5' e 3' UTR
```
samtools coverage -m -r chr17:29,227,337-29,228,565 Bowtie2_on_data2.bam 
```

 - Mean Coverage: Nr di letture di una posizione/ Totale delle letture

## MACS2
- PeakCalling
- d: Center of Peak != center of read mapping
- Distanza tra due picchi
- ottenere la regione genomica che corrisponde al sito di legame di p53
- Sposto i due picchi ottenendo un picco che ha come peak esattamente d
- Un picco su IGV è il risultato di due picchi, uno in forward uno in reverse
- Si trasformano in un picco unico, calcolando la distanza d tra i due picchi (intesi i centri)
- MACS2 Scorre sul genome con dimensioni di finestra pari a $2\cdot d$ per cercare picchi candidati
- Per ***ogni*** picco, si utilizza il controllo per calcolare $\lambda$, parametro della distribuzione di Poisson, ovvero il valore atteso
- Ipotesi nulla: L'input in maniera statisticamente significativa ci sono più read rispetto al precipitato  
	- ci si aspetta che il numero di read del precipitato sia > rispetto controllo

[[SysBio Theory]]


- Istone H3 -> Se MONOmetilato su K4 (Lys-4) -> Indica un enhancer

BIAS -> Deviazione sistematica casuale dalla realtà, non è noise.
Errore sistematico costante.
- 15 - 20% hanno + siti di legame (2 e 3 sommati)
- TOMTOM utilizzabile con qualsiasi sequenza (proteina, DNA)
![[Screenshot 2025-10-27 at 15.54.14.png]]


Regioni sovrapposte tra due esoni di due geni, Esempio Htra2 e quello successive, possono avere reads sovrapposte tra i due esoni. Queste reads possono essere assegnate ad entrambe o a nessuna delle due. (Generalmente nessuna delle due e vengono perse quelle reads)![[Screenshot 2025-11-05 at 09.58.00.png]]
Unstranded: 983
Fw Strand: 891
Rev Strand: 910

In questo caso le read in sovrapposizione STAR ha rimosso le Read. Infatti in unstranded le read sono 983, che non è la somma di Fw Strand e Rev Strand.
In Fw e Reverse non ha rimosso alcuna read ovviamente perchè non si sovrappone. Utile ispezionare il gene precedente/successivo.
