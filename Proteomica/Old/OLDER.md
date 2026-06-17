## Classi di esperimenti di proteomica
Il tipico esperimento di proteomica è il PEA -> Expression analysis. Analisi dell'espressione di una proteina ( o più) nei diversi campioni. La complessità del campione è elevata perchè estendiamo questa analisi a più proteine possibili. Il dettaglio analitico ovviamente è basso, si valuta solo l'espressione

Un'altro tipo di esperimento è  l'analisi di gruppi specifici di proteine. Non si lavora più su un solo campione complesso, ma su un gruppo specifico di 20-200 proteine già selezionate. (Proteine delle stessa famiglia, oppure di un organello). Il dettaglio analitico aumenta.

L'ultimo è lo studio delle modificazioni post-traduzionali, andando ad utilizzare la composizione della sequenza amminoacidica per ricercare le modificazioni. Si lavora con un basso numero di proteine, il dettaglio analitico aumenta


### Elettroforesi Bidimensionale
È una tecnica elettroforetica utilizzata nel campo della proteomica per separare miscele proteiche complesse, come ad esempio una miscela di proteine estratta da una cellula in un dato momento del ciclo cellulare.
La tecnica cosnta di due dimensioni ortogonali lungo le quali sono separate le diverse proteine. In proteomica, ortogonale si riferisce in genere alle due dimensioni lungo le quali la separazione avviene sfruttando principi fisici differenti, che non sono influenzati l'uno dall'altro.
Nel caso dell'elettroforesi bidimensionale, i principi più utilizzati solo il punto isoelettrico e il peso molecolare.

La prima dimensione utilizza solitamente un gradiente di pH ottenuto grazie a molecole anfotere, fatte migrare all'interno di un supporto costituito in gene da un gel di poliacrilammide, posto in un campo elettrico. Il campione viene caricato su gel ed il campo elettrico applicato fa si che le proteine presenti in forma ionica si muovano fino a raggiungere il punto isoelettrico proprio. Il processo si chiama isoelettrofocalizzazione o IEF.

Durante la seconda dimensione, il campione viene trattato con SDS per conferire a tutte le proteine una carica elettrica negativa. Segue la classica SDS-PAGE, in cui le specie proteiche si dividono in funzione del loro peso molecolare.

Modificazioni post-traduzionali possono causare cambiamenti nel punto isoelettrico e/o nel peso molecolare. Si riconoscono i "train" in proteine estensivamente modificate.
La 2D-PAGE e l'analisi dell'immagine ci permettono di studiare modificazioni nella composizione del proteoma.

Un altro problema è gli spot messi vicino l'una all’altra che hanno diverso pI ma uguale massa. Questi spot sono dovuti a modificazioni post traduzionali. Quindi alla stessa altezza di massa abbiamo spot che si mettono vicine. È la stessa proteina ma con modifiche quindi co esistenza di specie con livelli di modificazioni diverse.
Con l'image analysis si va a identificare gli spot, gel-to-gel-matching, assenza/presenza di spot, up/down regolazione, analisi statistiche.
#### SDS-PAGE
L'SDS (dodecil solfato di sodio) è un detergente fortemento ionico che conferisce carica elettrica negativa in media ogni 2 residui amminoacidici. Le proteine trattate con SDS sono denaturate con un numero di cariche proporzionale al loro peso molecolare:
- 40kDa -> assumerà circa 180 cariche negative
- 80kDa -> assumerà circa 360 cariche negative
L'idea è la stessa della elettroforesi: Quando si applica un campo elettrico di corrente continua ad una soluzione a pH determinato, il contenuto (proteine) si muoverà verso uno dei due elettrodi (il catodo nel caso della SDS-PAGE dato che sono tutte cariche negativamente). La velocità è inversamente proporzionale al peso molecolare.
L'SDS-PAGE permette di stabilire la purezza della proteina purificata e il suo peso molecolare.

## Gel-Based Proteomics

1. Stabilire mappe reference
	- Frazione Organellare
	- Frazione solubile
2. Differenze qualitative
	- Comparazione di genotipi
	- Comparazione di differenti organelli
3. Differenze quantitative
	- Risposta ai farmaci
	- Cambiamenti durante la malattia
	- Risposta a stimoli
**Tecnica Gel per singolo campione** -> Tessuti -> Elettroforesi 2D -> Staining del gel -> Matching dei gel -> Comparazione degli spot

Il volume dello spot lo otteniamo da analisi dell'immagine come somma dei pixel all'interno dei confini dello spot. Si normalizza poi $\frac{\text{Spot volume}}{\text{volume totale degli spot su gel}}$
![[Pasted image 20260617085517.png]]

Con più replicati biologici controllo/trattato -> Analisi statistica.

Problema:  2D-Electrophoresis:
Variazioni Gel-to-Gel  nel profilo della proteina:
Prima dimensione:
- Reidratazione non uniforme degli strip IEF
- Perdita di proteina durante l'uscita dal gel IEF
- Quantitativo di campione preso da IEF è differente per campione
- Streaking orizzontale di alcuni spot proteici
Seconda dimensione:
- Differenze/difetti nel settaggio del gel
- Streaking verticale
Effetti della variazione -> 
Gel-to-Gel problematico
inaccuratezza nella quantificazione delle proteine

Come limitare gli effetti delle variazioni?
- Repliche biologiche
- Repliche tecniche
- Tanti gel -> 3 biologiche + 3 tecniche per biologica = 18 gel totali
Ma questo incrementa costi in reagenti e tempo