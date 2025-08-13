---
publish: true
---
# Cinetica degli Enzimi
Uno dei fattori che modificano la velocità di una reazione catalizzata da un enzima purificato è la concentrazione del substrato \[S].
Gli studi sull'effetto del substrato vengono complicati ulteriormente dal fatto che la concentrazione di S varia durante il corso di una reazione, man mano che il substrato viene convertito in prodotto. Per eliminare questo problema, si può valutare $V_0$ la velocità iniziale.
In una tipica reazione l'enzima è presente in quantità nanomolari, mentre \[S] può essere 5 o 6 ordini di grandezza più elevato. Se si monitora solo l'inizio della reazione, in un tempo in cui solo una piccola percentuale del substrato è convertita in prodotto, \[S] può essere considerata approssimativamente costante. $V_0$ può essere quindi studiata come funzione di \[S].
L'effetto della variazione di \[S] su $V_0$ quando la concentrazione dell'enzima viene mantenuta costante:
- Per concentrazioni basse di substrato $V_0$ aumenta praticamente in modo lineare con l'aumento di \[S]
- Per concentrazioni elevate di substrato $V_0$ aumenta in misura sempre minore in funzione dell'aumento di \[S]
- Alla fine si arriva ad un punto di cui gli aumenti di velocità iniziale in funzione di \[S] diventano sempre di entità minore
- Nella regione più piatta della curva, la velocità si avvicina alla velocità massima $V_{max}$. 

Il complesso ES è quindi la chiave per la comprensione del comportamento cinetico degli enzimi.

Secondo Michaelis e Menten:
- La prima tappa è la combinazione enzima-substrato reversibile, formando il complesso ES velocemente e reversibilmente $$E+S \leftrightarrow^{k_1}_{k_{-1}} ES$$
- Il complesso ES si decompone poi in una seconda tappa più lenta, che produce enzima libero ed il prodotto della reazione P: $$ES \leftrightarrow^{k_2}_{k_{-2}} E+P$$
- Questa reazione è più lenta e quindi limita la velocità della reazione complessiva. La velocità della reazione complessiva deve quindi essere proporzionale alla concentrazione delle specie chimiche che reagiscono nella seconda tappa, cioè ad ES

In qualsiasi reazione catalizzata, l'enzima è presente in due forme, e quella libera E e quella combinata con substrato ES.
Se \[S] è bassa, la maggior parte dell'enzima sarà nella forma libera. La velocità quindi è proporzionale a \[S] dal momento che in base all'equilibrio man mano che \[S] tende ad aumentare viene favorita la formazione del complesso ES.
La velocità iniziale massima della reazione catalizzata ($V_{max}$) si osserva quando praticamente tutto l'enzima è presente nella forma di complesso ES e la concentrazione di E libero diventa trascurabile. In queste condizione l'enzima è saturo di substrato, e quindi ulteriore substrato non avrà effetti sulla velocità di reazione.
Questo rimane vero solo se la concentrazione di S rimane elevata abbastanza da saturare l'enzima.
Man mano che si forma il prodotto ed il complesso ES si dissocia, gradualmente parte dell'enzima torna ad essere libero e pronto ad una nuova reazione catalitica.
L'effetto saturante del substrato è una proprietà dei catalizzatori enzimatici ed è responsabile del plateau della curva. Chiamato anche cinetica di pre-saturazione.

Quando l'enzima si mescola con un grande eccesso di substrato, vi è un periodo iniziale, chiamato stato pre-stazionario, durante il quale avviene la formazione di ES. In genere questo periodo è troppo breve per poter essere osservato, poichè dura solo microsecondi.
La reazione raggiunge rapidamente lo stato stazionario, in cui \[ES] rimane approssimativamente costante nel tempo.
Gli enzimi sono potenti catalizzatori presenti in concentrazioni inferiori a quelle del substrato. Una volta superata la fase pre-stazionaria, il prodotto P viene generato alla stessa velocità con cui viene consumato S solo se la concentrazione dell'intermedio ES rimane costante. La $V_0$ misurata in genere riflette lo stato stazionario, anche se $V_0$ è limitata ai primi istanti della reazione. 
Questa viene chiamata **cinetica dello stato stazionario**.

## Equazione di Michaelis Menten
L'equazione venne formulata sulla base dell'ipotesi che la tappa limitante di una reazione enzimata fosse la demolizione del complesso ES per formare enzima libero e prodotto:
$$V_0 = \frac{V_{max}[S]}{K_m+[S]}$$
$K_m$ -> Costante di Michaelis Menten

Includendo anche lo stato stazionario precedente:
La derivazione inizia con le due reazioni di base di formazione e di demolizione del complesso ES.
Nei primi momenti della reazione la concentrazione del prodotto \[P] è molto bassa e quindi possiamo semplificare l'equazione supponendo che la velocità di reazione P->S inversa sia trascurabile.
La reazione complessiva si riduce a $$E+S \leftrightarrow^{k_1}_{k_{-1}}ES \rightarrow^{k_2} E+P$$
$V_0$ dipende dalla demolizione di ES per dare origine al prodotto e quindi è direttamente proporziale a \[ES $$V_0 = k_2 [ES]$$
Il termine \[ES] non è facilmente misurabile. 
\[ES] può essere approssimato:
\[E] è trascurabile rispetto a \[S] dato che \[S] è sempre molto più grande della concentrazione dell'enzima.
$[E_t]$ rappresenta la concentrazione di enzima totale, ovvero \[ES] + \[E], enzima libero + impegnato con il substrato.

Si ottengono quindi le seguenti equazioni per approssimare $V_0$ data la difficile misurazione di \[ES:

Velocità di Formazione di ES: $k_1([E_t] - [ES]) [S]$
Velocità di Demolizione di ES: $k_{-1}[ES] + k_2 [ES]$

Bisogna ora fare un'assunzione, ovvero che la velocità iniziale della reazione riflette uno stato stazionario in cui \[ES] è costante; in queste condizioni, la velocità di formazione di ES diventa uguale a quella della sua demolizione. Questa assunzione si chiama **assunzione dello stato stazionario**:
$$k_1 ([E_t] - [ES]) [S] = k_1[ES] + k_2 [ES]$$
con il termine $\frac {(k_1+k_2)}{k_1}$ detto Costante di Michaelis $K_m$ si può risolvere l'equazione per \[ES] ed ottenere: $$[ES] = \frac{[E_t][S]}{K_m+[S]}$$
quindi:
$$V_0 = \frac{k_2[E_t][S]}{K_m+[S]}$$
Che può essere ulteriormente semplificata dato che la velocità massima viene raggiunta quando tutto l'enzima è stato saturato. In condizioni di saturazione \[ES diventa uguale ad \[Et] e quindi $$V_{max} = k_2[E_t]$$
Sostituendo Vmax a \[Et]
$$V_0 = \frac{V_{max}[S]}{K_m + S}$$
Che è l'quazione di Michaelis-Menten, ovvero l'equazione della velocità di reazione a singolo substrato catalizzato da un enzima, ovvero la relazione quantitativa tra velocità iniziale, velocità massima e la concentrazione iniziale del substrato, termini tra loro correlati dalla costante di Michaelis $K_m$, misurata con la stessa u.m della concentrazione.
Dall'equazione di Michaelis-Menten si osserva che se $V_0$ è uguale a $\frac{1}{2}V_{max}$:
$$\frac{V_{max}}{2} = \frac{V_{max}[S]}{K_m + [S]}$$
$$K_m = [S]$$
Utile questa definizione per definire Km come equivalente alla concentrazione del substrato a cui V0 è la metà di Vmax.

Michaelis-Menten descrive la cinetica di tutti gli enzimi che presentano una relazione di tipo iperbolico tra velocità della reazione catalizzata e concentrazione del substrato.
Molti enzimi che seguono cinetica di Michaelis Menten hanno meccanismi di reazione abbastanza diversi e quelli che catalizzano reazione con sei o otto tappe identificabili hanno molto spesso il comportamento tipico dello stato stazionario.
Vmax e Km possono variare considerevolmente passando da un enzima all'altro, il che è una grossa limitazione per questo tipo di approccio allo studio della cinetica dello stato stazionario.
Questi sono parametri che si possono determinare sperimentalmente, ma non sono identicativi del numero e della velocità o natura chimica delle tappe attraverso cui avviene la reazione. La cinetica dello stato stazionario rappresenta comunque un sistema standard per valutare caratterizzare e confrontare l'efficienza catalitica di enzimi diversi.

### $K_m$
$K_m$ può variare considerevolmente da un enzima ad un altro, anche per substrati diversi di uno stesso enzima.
$K_m$ non è indicativo dell'affinità di un enzima per il suo substrato. $K_m$ dipende da aspetti specifici del meccanismo di reazione, come il numero e le velocità relative delle tappe della reazione.
Per una reazione a due tappe, $K_m$ si esprime come:
$$K_m = \frac{k_2+k{-1}}{k_1}$$
Se $k_2$ è la costante che limita la velocità, si ha che $k_2<<k_1$ e $K_m$ si riduce a $k_{-1}/k_1$ che viene detta costante di disassociazione $K_d$ del complesso ES.
Quando si verificano queste condizioni $K_m$ rappresenta una misura dell'affinità dell'enzima per il suo substrato nel complesso ES.
Questa situazione non si applica per la maggior parte degli enzimi.
In alcuni casi si ha che $k_2>>k_{-1}$ e quindi $K_m = k_2/k_1$.
In alcuni casi k2 e k-1 sono simili e $K_m$ diventa ancora più complessa diventando una funzione dalle tre costanti di velocità.
Michaelis Menten e la saturazione da substrato degli enzimi restano valide, ma $K_m$ non può essere considerata come indicazione per l'affinità del substrato.
Sono frequenti i casi in cui le reazioni procedono per molte tappe dopo la formazione di ES e $K_m$ diventa una funzione molto complessa di numerose costanti di velocità.
I valori di $V_{max}$ variano considerevolmente passando da un enzima all'altro.
Se un enzima reagisce con un meccanismo a due tappe, secondo Michaelis-Menten, la $V_{max}$ equivale a $k_2 [E_t]$ e $k_2$ diventa la costante che limita la velocità.
Il numero delle tappe della reazione e l'identità di quella che limitano la velocità della reazione variano da enzima a enzima.

Considerando $EP \rightarrow E +P$, diventa la tappa limitante della velocità.
Quando $[P]$ è bassa, la reazione può essere scritta come: $$E+S \leftrightarrow^{k_1}_{k_{-1}} ES \leftrightarrow^{k_2}_{k_{-2}} EP \leftrightarrow^{k_3} E+ P $$
In questo caso la maggior parte degli enzimi è a saturazione nella forma EP e $V_{max}$ diventa uguale a $k_3[E_t]$.
$k_{cat}$ è la costante di velocità generale necessaria per descrivere la tappa che limita la velocità di una reazione catalizzata da un enzima in condizioni di saturazione.
Se la reazione è costituita da diverse tappe e una di queste è chiaramente quella limitante, $k_{cat}$ diventa uguale alla costante di velocità della tappa limitante.
Mentre in alcune equazioni la tappa limitante è evidente, in equazioni in cui le tappe limitanti sono molteplici, $k_{cat}$ può diventare una funzione complessa delle costanti di velocità delle varie tappe della reazione.
$k_{cat} = V_{max}/[E_t]$  per Michaelis-Menten, quindi $V_0 = \frac{k_{cat}[E_t][S]}{K_m + [S]}$
$k_{cat}$ è una costante del primo ordine espressa come reciproco del tempo. 
$k_{cat}$ viene chiamata anche numero di turnover ed equivale al numero di molecole di substrato che vengono convertite in prodotto nell'unità di tempo da una singola molecola enzimatica quando l'enzima è saturo con il substrato.

Il modo migliore per confrontare l'efficienza catalitica di enzimi diversi o dello stesso enzima con substrati diversi è paragonare il rapporto $k_{cat}/K_m$ delle due reazioni.
Questo parametro è chiamato costante di specificità, è la costante di velocità della conversione di E+S in E+P. 
Quando $[S]<< K_m$:
$$V_0 = \frac{k_{cat}}{K_m} [E_t][S]$$
In questo caso la velocità inziale dipende dalla concentrazione dei due reagenti, Et ed S. Questa è quindi una reazione del secondo ordine e la costante $k_{cat}/K_m$ è una costante di secondo ordine espressa in $m^{-1}s^{-1}$.
Esiste un limite superiore al valore della costante $k_{cat}/K_m$ imposto dalla velocità con cui i due reagenti diffondo l'uno verso l'altro nelle soluzione acquose. Questo limite controllato dalla diffusione varia da $10^8 \space a \space 10^9 m^{-1}s^{-1}$ e molti enzimi hanno valori di costante di specificità compreso in questo intervallo. Si può dire che questi enzimi hanno raggiunto la perfezione catalitica.

Nella maggior parte delle reazioni enzimatiche partecipano due substrati e si formano due prodotti. Queste reazioni includono, ad esempio, il trasferimento di gruppi funzionali o reazioni redox. Un esempio è la reazione catalizzata dall'esochinasi, in cui un gruppo fosfato viene trasferito dall'ATP al glucosio ATP+glucoio -> ADP + glucosio-6-fosfato

Anche per le reazioni con due substrati si può applicare Michaelis-Menten, considerando un valore di  $K_m$ per ciascun substrato.
Le reazione bi-bi (due substrati-due prodotti) seguono diversi meccanismi:
1. Formazione di un complesso ternario, dove entrambi i substrati si legano contemporaneamente all'enzima
	1. L'ordine di legame può essere casuale o ordinato
2. Meccanismo a Ping-Pong, o doppio spiazzamento
	1. Il primo substrato si lega, viene trasformato, ed un intermedio covalente si forma con l'enzima
	2. Questo intermedio reagisce poi con il secondo substrato per formare il secondo prodotto
	3. Il substrato A e B non sono mai legati contemporaneamente sull'enzima

Per descrivere queste reazione si usa la nomeclatura di Clealand, dove:
- I substrati sono indicati con A, B, C ecc...
- I prodotti sono indicati con P, Q, S ....
- Enzima come E, e le sue forme modificate come F, G ecc...
- Viene anche utilizzata una rappresentazione grafica con:
	- Linee orizzontali -> sequenza della reazione
	- Linee verticali -> legami e rilasci
	- Biforcazioni -> legami o rilasci casuali

Michaelis Menten può fornirci solo poche informazioni sul numero di passaggi ed intermedi di una reazione enzimatica, ma può essere utilizzata per distinguere i meccanismi di reazione che hanno un intermedio ternario e quelli che non lo hanno, come i meccanismi a ping pong.
La cinetica dello stato stazionario può aiutare a distinguere anche tra legame ordinato o casuale dei substrati e dei prodotti in reazioni con intermedi ternari.

### pH ed attività enzimatica
L'attività enzimatica dipende fortemente dal pH. Ogni enzima ha un pH ottimale, cioè un intervallo di pH in cui la sua attività catalitica è massima.
Al di fuori di questo intervallo, l'attività enzimatica diminuisce fino a cessare del tutto se il pH è troppo acido o troppo basico
Il pH può alterare la struttura tridimensionale dell'enzima, denaturandolo.
Inoltre le catene laterali degli amminoacidi sono sensibili a cambiamenti del pH, dato che la variazione modifica la carica elettrica di queste catene. Ad esempio, la rimozione di un protone dalle catene laterali da His può causare l'eliminazione di una interazione ionica essenziale per la stabilizzazione della conformazione dell'enzima. Meno comuni sono casi in cui la dipendenza dal pH è data dalla titolazione (il rilascio o il legame di un protone) di un gruppo appartenente al substrato.

[[Glicolisi]]