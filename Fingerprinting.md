# Proteomica: Strategie di Analisi

---

## 1. Due Approcci Principali

| | **Top-Down** | **Bottom-Up** |
|---|---|---|
| **Oggetto di misura** | Proteine intere e loro frammenti | Peptidi derivati da digestione |
| **Applicazioni** | Struttura terziaria e quaternaria | Identificazione, quantificazione, PTM |
| **Limitazione chiave** | Le proteine grandi non eluiscono dalla colonna cromatografica | Si perde il contesto della proteina intera |
| **Diffusione** | Poco diffuso | Approccio dominante |

---

## 2. Due Scuole di Pensiero (Bottom-Up)

### 2.1 Approccio Elettroforetico (classico)
- Separazione mediante **PAGE** (mono- o bi-dimensionale)
- Processo **manuale**: l'operatore taglia ogni spot dal gel, lo lavora individualmente, poi lo analizza per MS/MS
- Laborioso e poco scalabile

### 2.2 Approccio Cromatografico (moderno)
- Separazione mediante **LC in fase liquida + ESI**
- Processo **automatizzato**: estratto proteico → digestione → HPLC → MS/MS
- Permette throughput molto superiore e analisi di miscele complesse

---

## 3. Workflow Bottom-Up

```
Campione proteico
      ↓
1. Separazione / Frazionamento proteico
      ↓
2. Proteolisi (es. tripsina → taglia dopo Lys/Arg)
      ↓
3. Separazione peptidica
      ↓
4. Ionizzazione  (MALDI · ESI · FAB · EI · CI)
      ↓
5. Analisi MS / MS/MS  (Ion trap · TOF · ...)
      ↓
6. Detezione  (MCP · Dynode-EM)
      ↓
7. Elaborazione dati
```

---

## 4. Il Problema del Frazionamento

### 4.1 Perché è Necessario

Due ragioni fondamentali:

1. **Range dinamico di espressione**: la proteina più abbondante può essere $10^{11}$ volte più abbondante della meno abbondante — strumentalmente impossibile da coprire in un'unica analisi.
2. **Velocità di acquisizione**: la raccolta degli spettri MS/MS non è abbastanza rapida da coprire tutti i peptidi in un campione complesso senza perdita.
3. **Similarità chimica**: i peptidi hanno proprietà fisico-chimiche simili, rendendo difficile la separazione cromatografica di miscele troppo complesse.

### 4.2 Esempio Quantitativo

Dato un campione relativamente semplice:

| Parametro | Valore |
|---|---|
| Numero di proteine | 5.000 |
| Frammenti peptidici attesi | ~40.000 |
| Peso molecolare medio | 30 kDa |
| Quantità minima per sequenziamento | 15 fmol / proteina |

**Caso ideale** (abbondanza uniforme):

$$15 \text{ fmol} \times 30 \text{ kDa} = 450 \text{ pg/proteina} \times 5000 = \mathbf{2.25\ \mu g\ \text{totali}}$$

**Caso reale** (range di abbondanza $10^6$):

Per ottenere 15 fmol della proteina *meno abbondante*, serve $10^5 \times$ più campione:

$$2.25\ \mu g \times 10^5 = \mathbf{225\ mg\ \text{di proteina totale}}$$

→ **Quando il campione è limitante, il frazionamento non è opzionale — è necessario per ridurre la complessità prima dell'analisi**.

---

## 5. Strategie di Frazionamento

### 5.1 Pre-digestione (Separazione della Proteina)

Si riduce la complessità a livello proteico, prima di digerire.
Separazione della proteina intatta mediante elettroforesi

| Metodo                       | Esempi                                     |
| ---------------------------- | ------------------------------------------ |
| Isolamento di organelli      | Mitocondri, nucleo, membrana plasmatica    |
| Frazionamento per solubilità | Frazione di membrana vs. frazione solubile |
| Separazione cromatografica   | Scambio cationico / anionico               |
| Separazione elettroforetica  | 1D-SDS-PAGE · 2D-PAGE (pI + MW)            |
| Affinity Chromatography      |                                            |

### 5.2 Post-digestione (Separazione del Peptide)

Si riduce la complessità a livello peptidico, dopo la digestione.

| Metodo | Note |
|---|---|
| **Cromatografia a fase inversa** (RP-HPLC) | Step finale prima dell'ingresso nello spettrometro |
| **Cromatografia multidimensionale** (MudPIT) | Es. SCX → RP; aumenta drasticamente la copertura del proteoma |

---

## 6. Quadro Riassuntivo

```
                     CAMPIONE PROTEOMICO
                           │
           ┌───────────────┴───────────────┐
     Pre-digestione                  Post-digestione
   (separa proteine)               (separa peptidi)
           │                               │
    organelli / gel             RP-HPLC / SCX-RP
           │                               │
           └───────────────┬───────────────┘
                     Proteolisi
                  (tripsina → peptidi)
                           │
                     Ionizzazione
                   (MALDI o ESI-LC)
                           │
                   MS / MS/MS
                           │
                   Identificazione
```



## Classi di esperimenti di proteomica
Il tipico esperimento di proteomica è il PEA -> Expression analysis. Analisi dell'espressione di una proteina ( o più) nei diversi campioni. La complessità del campione è elevata perchè estendiamo questa analisi a più proteine possibili. Il dettaglio analitico ovviamente è basso, si valuta solo l'espressione

Un'altro tipo di esperimento è  l'analisi di gruppi specifici di proteine. Non si lavora più su un solo campione complesso, ma su un gruppo specifico di 20-200 proteine già selezionate. (Proteine delle stessa famiglia, oppure di un organello). Il dettaglio analitico aumenta.

L'ultimo è lo studio delle modificazioni post-traduzionali, andando ad utilizzare la composizione della sequenza amminoacidica per ricercare le modificazioni. Si lavora con un basso numero di proteine, il dettaglio analitico aumenta


### Elettroforesi Bidimensionale
È una tecnica elettroforetica utilizzata nel campo della proteomica per separare miscele proteiche complesse, come ad esempio una miscela di proteine estratta da una cellula in un dato momento del ciclo cellulare.
La tecnica cosnta di due dimensioni ortogonali lungo le quali sono separate le diverse proteine. In proteomica, ortogonale si riferisce in genere alle due dimensioni lungo le quali la separazione avviene sfruttando principi fisici differenti, che non sono influenzati l'uno dall'altro.
Nel caso dell'elettroforesi bidimensionale, i principi più utilizzati solo il punto isoelettrico e il peso molecolare.

La prima dimensione utilizza solitamente un gradiente di pH ottenuto grazie a molecole anfotere, fatte migrare all'interno di un supporto costituito in gene da un gel di poliacrilammide, posto in un campo elettrico. Il campione viene caricato su gel ed il campo elettrico applicato fa si che le proteine presenti in forma ionica si muovano fino a raggiungere il punto isoelettrico proprio. Il processo si chaiam isoelettrofocalizzazione o IEF.

Durante la seconda dimensione, il campione viene trattato con SDS per conferire a tutte le proteine una carica elettrica negativa. Segue la classica SDS-PAGE, in cui le specie proteiche si dividono in funzione del loro peso molecolare.

Modificazioni post-traduzionali possono causare cambiamenti nel punto isoelettrico e/o nel peso molecolare.
La 2D-PAGE e l'analisi dell'immagine ci permettono di studiare modificazioni nella composizione del proteoma.
#### SDS-PAGE
L'SDS (dodecil solfato di sodio) è un detergente fortemento ionico che conferisce carica elettrica negativa in media ogni 2 residui amminoacidici. Le proteine trattate con SDS sono denaturate con un numero di cariche proporzionale al loro peso molecolare:
- 40kDa -> assumerà circa 180 cariche negative
- 80kDa -> assumerà circa 360 cariche negative
L'idea è la stessa della elettroforesi: Quando si applica un campo elettrico di corrente continua ad una soluzione a pH determinato, il contenuto (proteine) si muoverà verso uno dei due elettrodi (il catodo nel caso della SDS-PAGE dato che sono tutte cariche negativamente). La velocità è inversamente proporzionale al peso molecolare.
L'SDS-PAGE permette di stabilire la purezza della proteina purificata e il suo peso molecolare.

