
## 5. Analizzatore di Massa: TOF (Time-of-Flight)

### 5.1 Principio Generale

|Aspetto|Altri analizzatori|TOF|
|---|---|---|
|Tipo di separazione|Nel **tempo**|Nello **spazio** (distanza fissa)|
|Forza applicata durante il drift|Sì|No — gli ioni sono in deriva libera|
|Modalità di acquisizione|Scansione|Tutto simultaneamente (snapshot)|

Il TOF misura il **tempo impiegato da uno ione per percorrere una distanza fissa** (drift region). Ioni con massa diversa acquistano velocità diverse e arrivano al rivelatore in tempi diversi → separazione per m/z.

> **Accoppiamento naturale:** MALDI/TOF è stato a lungo lo standard della proteomica. MALDI ionizza anche macromolecole intatte, e TOF ha un range di massa teoricamente illimitato.

---

### 5.2 Fisica del TOF

#### Conservazione dell'energia

Nella zona sorgente tutti gli ioni vengono accelerati dallo **stesso potenziale U** (costante). L'energia potenziale acquisita si converte interamente in energia cinetica:

$$E_P = qU \qquad E_K = \frac{1}{2}mv^2$$

$$E_P = E_K \Longrightarrow qU = \frac{1}{2}mv^2$$

dove $q = ze$ , $U$ = voltaggio di accelerazione, $m$ = massa, $v$ = velocità nella drift region.
$q$ è la carica elettrica totale dello ione -> +1, +2, +3 ecc...
$e$ è la carica elementare (la carica di un singolo protone o elettrone, $1.602\times 10^{-19}Coulomb$)

La formula $E_P​=qU$ descrive l'**energia potenziale elettrica** che lo strumento fornisce allo ione.


> Poiché U è uguale per tutti, a parità di carica uno ione con massa minore raggiunge velocità maggiore → arriva prima al rivelatore.

#### Tempo di volo

Da $v = d/t$ e dall'equazione sopra si ricava:

$$\boxed{t = \frac{d}{\sqrt{2U}}\sqrt{\frac{m}{q}}}$$

Invertendo per ottenere la massa:

$$m = \frac{2qU}{d^2},t^2$$

Il tempo di volo è dunque una misura diretta di $\sqrt{m/q}$ — da $t$ misurato si risale a $m/z$.

---

### 5.3 Resolving Power

Differenziando $m = \frac{2qU}{d^2}t^2$:

$$dm = \frac{2qU}{d^2}\cdot 2tdt$$

Dividendo membro a membro:

$$\frac{m}{dm} = \frac{t}{2dt} ;\Longrightarrow; \boxed{R = \frac{m}{\Delta m} = \frac{t}{2\Delta t}}$$

**Interpretazione:** la risoluzione di massa dipende direttamente dalla precisione temporale $\Delta t$. Per separare due masse simili occorre che il fascio ionico di ciascuna massa arrivi al rivelatore entro un intervallo di tempo $\Delta t$ il più stretto possibile → **focalizzazione del fascio ionico**.
![[Pasted image 20260617151250.png]]

---

### 5.4 Problemi: De-focalizzazione del Fascio Ionico

In pratica, ioni con la **stessa** m/z non arrivano tutti nello stesso istante, causando allargamento della banda ionica e perdita di risoluzione. Le cause sono tre:

| Effetto                    | Causa                                                                                                                                           | Conseguenza                                       |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| **Position spread**        | Ioni formati in posizioni diverse nella sorgente → diversa distanza percorsa nella zona di accelerazione                                        | Diversa energia cinetica acquisita                |
| **Direction spread**       | Ioni emessi con direzioni diverse → componente assiale della velocità variabile. Raggiungono l'uscita ma impiegano più tempo (turn-around time) | Tempi di transito diversi anche a parità di massa |
| **Energy/Velocity spread** | Energia cinetica iniziale (pre-accelerazione) variabile                                                                                         | Velocità di partenza non uniformi                 |

Tutti e tre i fenomeni **ampliano la distribuzione temporale** degli ioni a massa uguale → $\Delta t$ aumenta → $R$ diminuisce.
$\Delta t$ è dato quindi dalla somma del tempo trascorso nella regione **source** (formazione dello ione, position spread, velocity spread, direction spread) e il tempo trascorso nel **drifting tube** (position spread, velocity spread), oltre al response time del detector (dovrebbe essere circa costante).

---

### 5.5 Soluzioni Tecniche per la Focalizzazione

#### 1. Dual Stage Extraction - Position Spread

Anche detta focalizzazione spaziale di Wiley-McLaren. Si applica l'accelerazione in **due stadi** invece di uno:

- **Stadio 1:** campo più debole vicino alla sorgente → corregge le differenze di posizione e di energia cinetica iniziale
- **Stadio 2:** campo più intenso → accelerazione finale uniforme

La correzione del primo stadio è dipendente dalla massa, compensando esattamente il position spread per ciascuna specie.
Avendo due stadi di accelerazione indipendenti, è possibile "modulare" le tensioni in modo che gli ioni partiti da posizioni leggermente diverse (e che quindi subiscono potenziale diverso) convergano temporalmente _esattamente_ nel punto in cui si trova il rivelatore.

#### 2. Time-Delayed Extraction (DE) - Velocity Spread

Si introduce un **ritardo** ($\sim$ nanosecondi (MALDI)–microsecondi (ESI)) tra l'ionizzazione e l'applicazione del campo di accelerazione:

- Durante il ritardo, gli ioni con velocità iniziale maggiore si allontanano di più dalla sorgente 
- Quando il campo viene applicato, gli ioni più veloci (più lontani) si trovano in una regione a potenziale inferiore → ricevono meno energia → arrivano al rivelatore insieme agli ioni più lenti
- Risultato: **compressione temporale** della distribuzione → riduzione del position e del velocity spread tra ioni con lo stesso m/z che lasciando la sorgente

#### 3. Reflectron

Specchio elettrostatico posto in fondo alla drift region, formato da **elettrodi a potenziale crescente** con segno opposto al campo di accelerazione.

```
Sorgente ──────────────► Reflectron ──────────────► Rivelatore
         drift region 1              drift region 2
```

**Meccanismo di correzione:**

|Ione|Velocità|Penetrazione nel reflectron|Percorso extra|Effetto|
|---|---|---|---|---|
|Più veloce (più energetico)|Alta|Maggiore|Più lungo|Rallentato|
|Più lento (meno energetico)|Bassa|Minore|Più corto|Meno rallentato|

I due ioni, pur entrando in tempi diversi, escono dal reflectron e arrivano al rivelatore **contemporaneamente** → focalizzazione indipendente dalla posizione di partenza.

> Il voltaggio del reflectron è **superiore** al potenziale di accelerazione iniziale e di **segno opposto**: tutti gli ioni vengono decelerati, invertiti ed espulsi, ma con percorsi diversi in funzione della loro energia.

#### Configurazione Ottimale: Dual Stage Reflectron

La combinazione di **dual stage extraction + time-delayed extraction + reflectron** massimizza la focalizzazione del fascio ionico su tutte e tre le cause di spreading, consentendo la massima risoluzione raggiungibile in un TOF.

---

### 5.6 Riepilogo: Problema → Causa → Soluzione

| Problema                                  | Causa fisica                                 | Soluzione                             |
| ----------------------------------------- | -------------------------------------------- | ------------------------------------- |
| Position spread                           | Ioni formati in punti diversi della sorgente | Dual stage extraction + TDE           |
| Direction spread                          | Emissione in direzioni diverse               | TDE (compressione temporale parziale) |
| Energy spread                             | Diversa $E_K$ iniziale                       | TDE + Reflectron                      |
| Spreading residuo (indipendente da massa) | Imperfezioni del campo                       | Reflectron                            |