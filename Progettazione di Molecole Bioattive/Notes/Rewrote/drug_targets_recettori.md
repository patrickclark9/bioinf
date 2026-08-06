# Drug Targets: Recettori

## Introduzione
I recettori sono proteine globulari che agiscono come ricevitori di segnali per la cellula, localizzati principalmente nella membrana cellulare. Ricevono messaggeri chimici da altre cellule e trasmettono il messaggio all'interno della cellula, provocando una risposta cellulare.

- Recettori differenti sono specifici per differenti messaggeri chimici.
- Ogni cellula possiede un range di recettori di membrana che la rende sensibile e responsiva a specifici messaggeri chimici.

---

## Messaggeri

| Tipo | Caratteristiche |
|---|---|
| **Neurotrasmettitori** | Rilasciati da un neurone, attraversano la sinapsi e si legano a un recettore su una cellula target (muscolo o altro neurone). Basso tempo di vita; responsabili della comunicazione tra cellule individuali. |
| **Ormoni** | Rilasciati da una cellula o una ghiandola; si legano a recettori ovunque nell'organismo. |

> A differenza di un substrato enzimatico, i messaggeri chimici **attivano** i recettori senza provocare una reazione chimica.

---

## Meccanismo generale

1. Il recettore contiene un **dominio di binding**, riconosciuto dal messaggero.
2. Il legame ligando–sito di binding provoca un **cambiamento conformazionale** del target (*induced fit*).
3. Questo innesca un effetto a cascata, la **trasduzione del segnale**: il segnale si propaga all'interno della cellula senza che il ligando vi entri.
4. Il ligando non provoca alcuna reazione chimica e non si lega permanentemente: una volta rilasciato, il messaggero rimane inalterato.

### Sito di binding
- Equivalente concettualmente al sito attivo di un enzima; spesso idrofobico, composto da amminoacidi che legano il messaggero.
- Inizialmente **non** è perfettamente complementare al messaggero: il legame stesso induce il cambiamento conformazionale che lo rende complementare (**Induced Fit**), massimizzando le interazioni ligando-sito di binding.
- L'alterazione conformazionale genera gli effetti a catena della trasduzione del segnale.
- Le interazioni coinvolte nel binding sono: legami ionici, legami idrogeno, interazioni di Van der Waals.

### Equilibrio forza del legame
L'interazione deve essere:
- **abbastanza forte** da trattenere il ligando il tempo necessario alla trasduzione del segnale;
- **abbastanza debole** da permetterne il rilascio.

> Se il ligando non viene rilasciato, si comporta da **antagonista**, bloccando il sito di binding.

![[Pasted image 20260806083142.png]]
![[Pasted image 20260806083128.png]]

---

## Tipi di recettori e tempi di risposta

| Tipo di recettore | Tempo di risposta |
|---|---|
| Canali ionici | Millisecondi (ms) |
| G-protein coupled | Secondi (s) |
| Kinase-linked | Minuti |
| Intracellulari | Ore |

---

## 1. Canali Ionici

- La proteina recettrice è parte integrante di un canale ionico, formando con esso un complesso.
- Il legame del messaggero causa un cambiamento conformazionale (*induced fit*) che apre o chiude il canale.
- I canali sono specifici per determinati ioni, che li attraversano secondo gradiente di concentrazione.
- Possono polarizzare/depolarizzare membrane nervose o attivare/disattivare reazioni enzimatiche intracellulari.
- Il legame tra ligando e proteina provoca apertura/chiusura del canale, permettendo o impedendo il passaggio degli ioni.
- **Canali cationici** (K+, Na+, Ca2+) → eccitatori, depolarizzano.
- **Canali anionici** (Cl-) → inibitori, iperpolarizzano.

![[Pasted image 20260806084447.png]]![[Pasted image 20260806084454.png]]
![[Pasted image 20260806084615.png]]![[Pasted image 20260806084621.png]]![[Pasted image 20260806084645.png]]

### Effetti caratteristici
- Bassi tempi di risposta.
- Ideali per la trasmissione nervosa.
- Il binding del messaggero permette il flusso ionico attraverso la membrana.
- La trasduzione del segnale **coincide** con il flusso ionico stesso.
- La concentrazione ionica intracellulare si altera, modificando la chimica cellulare.

---

## 2. Recettori G-protein Coupled (GPCR)

- Il legame del ligando apre un sito di binding per la **proteina G**, che viene legata, destabilizzata e "splittata" all'interno del recettore.

![[Pasted image 20260806085407.png]]![[Pasted image 20260806085415.png]]

- Cascata tipica: lo split della proteina G attiva un enzima di membrana; il legame della proteina G a un sito allosterico sull'enzima ne provoca il cambiamento conformazionale e l'attivazione.

![[Pasted image 20260806085636.png]]
La proteina G nello stato di riposo si trova sotto forma di trimeto $\alpha\beta\gamma$ con GDP legato al sito specifico su subunità $\alpha$.
Il cambiamento conformazionale indotto dal legame di un agonista coinvolge il dominio citoplasmatico del recettore, con elevata affinità per il trimero.
L'associazione provoca il rilascio del GDP e la sua sostituzione con GTP, sostituzione che provoca la dissociazione del trimero in $\alpha$-GTP e $\beta\gamma$, che sono le forme attive della proteina G, che si diffondono nella membrana e legano canali ionici o enzimi, provocandone attivazione/inattivazione. Il processo termina con idrolisi del GTP a GDP nella subunità $\alpha$, che possiede attività GTP-asica. Questa quindi si dissocia dall'effettore e si ricongiunge alla subunità $\beta\gamma$, terminando il ciclo. La regolazione dell'azione GTP-asica da parte dell'effettore implica che l'attivazione di quest'ultimo tende ad essere autolimitante.
Questo meccanismo porta ad un'amplificazione del segnale, in quanto un singolo complesso agonista-recettore può attivare parecchie proteine G per volta, ognuna associata con l'enzima effettore per tempi sufficienti alla formazione di molecole di prodotto. Tipicamente è un secondo messaggero, per cui si verifica una seconda amplificazione prima che sia evidente la rispsota cellullare finale.
Ci sono _differenze molecolari_ tra le varie proteine G: queste differenze danno origine a tre principali classi di proteine ( **G s ![{\displaystyle G_{s}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2cae10c18b60e8086af35b09bf4539346df236b8)** , **G i ![{\displaystyle G_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0dd9fe8d455762608cc4e0a946b452492790ee5f) ** e **G q ![{\displaystyle G_{q}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/aa833656caf1493595e18fd39600427f4505f9f5)** ), che sono selettive sia per i recettori sia per gli effettori con i quali si accoppiano. Le proteine G s ![{\displaystyle G_{s}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2cae10c18b60e8086af35b09bf4539346df236b8) e G i ![{\displaystyle G_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0dd9fe8d455762608cc4e0a946b452492790ee5f) promuovono rispettivamente la stimolazione e l'inibizione dell'enzima **[adenil ciclasi](https://it.wikipedia.org/wiki/Adenil_ciclasi "Adenil ciclasi")**, e un simile controllo bidirezionale è attivo su altri effettori, come la **[fosfolipasi C](https://it.wikipedia.org/wiki/Fosfolipasi_C "Fosfolipasi C")**.
## Struttura
I GPCR sono costituiti da una singola catena polipeptidica formata anche da 1100 residui. La caratteristica strutturale è rappresentata da 7 $\alpha$-eliche transmembrana (tant'è che i GPCR sono anche detti "recettori a 7 eliche transmembrana"), con un dominio extracellulare N-terminale di lunghezza variabile e un dominio intracellulare C-terminale.
![[Pasted image 20260806095343.png]]
I GPCR vengono divisi in tre distinte famiglie che condividono la stessa struttura eptaelicale ma differiscono per vari aspetti, principalmente per la lunghezza della sequenza N-terminale e la localizzazione del sito di legame per l'agonista.
- La famiglia **A**, a cui appartiene la rodopsina, è di gran lunga la più numerosa e comprende la maggior parte dei recettori per le monoamine e i neuropeptidi.
- La famiglia **B** è costituita dai recettori della secretina, del glucagone e della calcitonina.
- La famiglia **C** è costituita principalmente dai recettori metabotropici del glutammato e dai recettori sensibili al $Ca^{2+}$ .
### Sito di legame del ligando (varia per classe di recettore)
| Classe | Ligando          | Sito di legame                                                  |
| ------ | ---------------- | --------------------------------------------------------------- |
| A      | Monoammine       | Tasca nelle eliche transmembrana                                |
| B      | Ormoni peptidici | Eliche transmembrana + loop extracellulare + catena N-terminale |
| C      | Ormoni           | Loop extracellulari + catena N-terminale                        |
| D      | Glutammato       | Catena N-terminale                                              |
![[Pasted image 20260806085648.png]]
### Ligandi tipici
Circa il **30%** dei farmaci ha come target i recettori accoppiati a proteine G. Ligandi tipici: monoammine, nucleotidi, lipidi, ormoni, glutammato, Ca2+.

### Cristallografia e template strutturali
- La rodopsina è un recettore visivo appartenente alla stessa famiglia evolutiva di molti GPCR.
- Essendo una proteina di membrana, la sua cristallizzazione è complessa; per questo è stata inizialmente cristallizzata la **batteriorodopsina**, usata come template per ricostruire la struttura di recettori in altre specie.
- Più recentemente sono state cristallizzate la **rodopsina bovina** e il **recettore beta_2 adrenergico**, offrendo template più accurati per il drug design.

![[Pasted image 20260806091021.png]]

L'immagine mostra come i diversi recettori accoppiati a proteine G si sono evoluti da un antenato comune:
- L'albero si dirama nelle principali categorie recettoriali: endoteline, tachichinine, monoammine, opsine/rodopsine.
- Ogni **tipo di recettore** si suddivide ulteriormente in **sottotipi recettoriali** specifici.
- Ad esempio, dal ramo delle monoammine si diramano i recettori muscarinici, istaminici, alfa-adrenergici, dopaminergici e beta-adrenergici.
- Questi si suddividono a loro volta in sottotipi molto specifici, come D1A, D1B, D2, D3, D4, D5 per i dopaminergici, oppure H1 e H2 per gli istaminici.

### Distribuzione tissutale dei sottotipi
I tipi di recettori e i loro sottotipi non sono distribuiti equamente tra i tessuti. La selettività del target porta a selettività tissutale:

| Tessuto                  | Sottotipo recettoriale                       |
| ------------------------ | -------------------------------------------- |
| Cuore (muscolo)          | $\beta_1$ adrenergico                        |
| Muscolo bronchiale       | $\alpha_1$ e $\beta_2$ adrenergico           |
| Tratto gastrointestinale | $alpha_1$, $alpha_2$ e $\beta_2$ adrenergico |
| Tessuto adiposo          | $\beta_3$ adrenergico                        |

---

## 3. Recettori Kinase-Linked

- Sono recettori bifunzionali recettore/enzima, spesso attivati da ormoni.
- Costituiscono un sistema integrato recettore+enzima: il recettore lega il messaggero, provocando un *induced fit*.
- Il cambiamento conformazionale apre il sito attivo intracellulare, catalizzando una reazione all'interno della cellula.

### Recettori tirosina-chinasi

![[Pasted image 20260806093341.png]]![[Pasted image 20260806093350.png]]![[Pasted image 20260806093407.png]]

- Il legame di EGF al recettore causa un cambiamento conformazionale che apre e permette l'azione dei domini tirosina-chinasi.
- Il sito attivo su una prima metà del dimero catalizza la fosforilazione dei residui di tirosina sull'altra metà.
- La **dimerizzazione** del recettore è cruciale: le regioni fosforilate agiscono da siti di binding per altre proteine ed enzimi.
- Il risultato è l'attivazione di proteine di segnale ed enzimi a valle, trasducendo il messaggio all'interno della cellula.

---

## 4. Recettori Intracellulari

- I messaggeri chimici devono attraversare la membrana cellulare, quindi devono essere **idrofobici**.
- Sono spesso ormoni steroidei, ormoni tiroidei o retinoidi.
- Gli ormoni steroidei sono molecole lipofiliche; tutti, eccetto il calcitriolo, condividono la struttura comune del **ciclopentanoperidrofenantrene**. Il precursore è il **colesterolo**.

![[Pasted image 20260806094459.png]]![[Pasted image 20260806094510.png]]

- Gli ormoni steroidei e tiroidei, spesso legati a proteine plasmatiche, hanno un tempo di vita abbastanza elevato (ore).
- Gli ormoni peptidici e le catecolammine sono solubili e trasportati disciolti nel plasma, con tempo di vita basso.

![[Pasted image 20260806094734.png]]![[Pasted image 20260806094704.png]]
