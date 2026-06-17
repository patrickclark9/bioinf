# TOF
Il TOF a differenza degli altri metodi di separazione, che separano nel tempo, è una separazione nello spazio.
Nel TOF non applichiamo nessun tipo di forza, ma la separazione è legata al diverso tempo di percorrenza degli ioni, che dipende a sua volta da m/z su uno spazio definito che è la distanza.
TOF ha varie caratteristiche:
- Risoluzione elevata
- Range di massa elevato
- Separazione basata sulla diversa energia cinetica di ciascuno ione
Se $v=\frac{d}{t}$, otteniamo una relazione che lega m/z al tempo, tenendo fisso il resto.
MALDI/TOF è stato lo standard per analisi proteomica per molto tempo. MALDI produce ioni anche a partire da grandi molecole, e TOF ha range di massa molto ampio. Gli ioni arrivano all'analizzatore però non uno per volta, ma in tempi diversi a causa della loro velocità iniziale. Velocità iniziale elevata -> Tempo di percorrenza più breve.
Il TOF quindi non lavora in scansione ma su tutto ciò che è presente.
Data una sorgente di ionizzazione, l'applicazione di un potenziale di accelerazione (accelerazione qui è costante), gli ioni vengono lasciati andare alla deriva -> drift-period, dove la velocità degli ioni è costante. Gli ioni si separano perchè avranno Velocità iniziali differenti in base alla loro massa.


![[Pasted image 20260617110315.png]]
$$E_P = qU ;\space q = ze$$
U è la differenza di potenziale -> Voltaggio di accelerazione, forza del campo elettrico applicato nella zona source, di partenza. è costante, tutti gli ioni vengono spinti dalla identica ddp U.
q è la carica elettrica totale dellone -> +1, +2, +3 ecc...
e è la carica elementare (la carica di un singolo protone o elettrone, $1.602\times 10^{-19}Coulomb$)
La formula $E_P​=qU$ descrive l'**energia potenziale elettrica** che lo strumento fornisce allo ione.

Il principio fisico su cui si basa il TOF è la conservazione dell'energia: nel momento in cui lo ione viene accelerato, tutta questa energia potenziale si converte in **energia cinetica** (l'energia del movimento, la cui formula è $E_C​=\frac{1}{2}​mv^2$, dove m è la massa e v la velocità).
$$E_K = \frac{1}{2}mv^2, v=\text{velocity of ion in drift region}$$
$$E_P = E_K \rightarrow qU = \frac{1}{2}mv^2$$
Il tempo di percorrenza è una variabile che dipende unicamente dalla massa.
**In sintesi:** Poiché il voltaggio U è fisso e uguale per tutti, l'energia impartita allo ione dipende solo dalla sua carica q. A parità di carica, uno ione con una massa (m) più piccola raggiungerà una velocità (v) maggiore e arriverà al rivelatore in un tempo più breve. Ecco come il TOF riesce a misurare il tempo di volo per ricavare il famoso rapporto **m/z** (massa su carica)!

$v=\frac{d}{t}$,, dove v = velocità dello ione, d = durata del drift, e t tempo di volo.
Il tempo di volo sarà $$t = \frac{d}{\sqrt{2U}}\sqrt{\frac{m}{q} }$$ ed $$m=\frac{2qU}{d^2}t^2$$
Differenziando l'equazione della massa: $$dm=\frac{2qU}{d^2}2tdt$$
$$\frac{m}{dm} = \frac{t^2}{2tdt} \rightarrow \frac{m}{dm} = \frac{t}{2dt}$$
Si ottiene il resolving power di TOF: $$\text{Resolving Power} \rightarrow \frac{m}{\Delta m} = \frac{t}{2\Delta t}$$
Sostanzialmente, variazioni in massa sono legate alla variazione nel tempo. La capacità risolutiva è povera -> il rapporto tra massa e variabilità di essa descrive la capacità di separazione di masse vicine tra loro.
La risoluzione è legata la focalizzazione del fascio ionico avente uguale massa. Se fascio a uguale massa è focalizzato entro intervalli di tempo molto ridotti -> Elevata risoluzione.
Ma ioni con la stessa massa avranno tempi diversi a causa di tempi di partenza differenti -> Nel TOF tutti gli ioni con stessa massa partono in maniera diversa e avranno tempi di percorrenza differenti. Ampliamento quindi dellla banda ionica -> Risoluzione va a picco.
Fattori che determinano la focalizzazione:
- Ioni generati nell'ordine di nanosecondi -> Due ioni identici hanno punti di partenza differenti, non percorrono quindi la stessa distanza **position spread**
- Possono essere generati con direzioni diverse -> stesso campo di accelerazione le molecole non vanno nello stesso verso **direction spread**
- Energia Cinetica diversa
Tutto questo va a de-focalizzare il fascio ionico, costituito da un'unica molecola di m/z definito, riducendo la risoluzione.