Tutti gli spettrometri di massa misurano le molecole ins tati ionizzati. Tutti i valori determinati da MS sono relativi al rapporto m/z:
$m/z = (m,+(mA\cdot z)) / z$

## MALDI/TOF

Il MALDI/TOF è ottimo per il PMF (Peptide mass Fingerprinting), in quanto veloce, facile da misurare, tollerante ai sali (più rispetto agli altri metodo -> Crosta bianca), funziona relativamente bene anche con molecole a più grande peso molecolare, non ci sono limiti temporali -> Campione su supporto stabile, e genera principalmente ioni +1, rari ioni multicarica.

Il sistema presenta alcuni svantaggi -> Elevata accuratezza richiede calibrazione, MS/MS è complessa da effettuare con MALDI, il segnale può essere soppresso in miscele complesse, Le condizioni di cristallizazione influenzano i risultati.

![[Pasted image 20260618083515.png| MALDI Tryptic Digest]]

## Elettrospray
È perfetta per MS/MS, dato che può essere accoppiato direttamente a HPLC (in fase inversa), e genera ioni 2/3+.

Svantaggi -> L'introduzione di campioni è più complessa, l'analisi è più complessa dati gli ioni 2+ e 3+, one-shot analysis -> limiti di tempo, il picco sparisce, e bassa tolleranza agli agenti contaminanti.

Il 2+/3+ per peptidi triptici è molto utile, dato che la tripsina raglia il C terminale vicino a Lys e Arg, quindi ogni peptide ha un residuo basico al suo C-terminale, oltre ad un N-terminale libero -> Almeno due siti di protonazione

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
- MS1 -> Selezione dei parent 
- Collision cell (Gas neutrale ad elevata pressione He, Ar, N2) -> Energia cinetica convertita ad Energia interna porta alla rottura di legami
- MS2 analizza gli ioni frammentati dalla collision cell

Il principio di MS/MS è reazioni filiate -> Lo spettro di un composto complesso è difficilmente interpretabile, ma selezionando un singolo precursore e frammentadolo si ottiene uno spettro diagnostico per la struttura di una molecola.