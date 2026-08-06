# Forze di Interazione Molecola-Target

## Introduzione
Il target dei farmaci è nella maggioranza dei casi rappresentato da macromolecole. Il legame farmaco-target è governato da diverse forze di interazione intermolecolari, di intensità e natura molto diverse tra loro.

---

## 1. Legami Ionici / Salini / Elettrostatici

- **Natura**: i più forti tra i legami intermolecolari; avvengono tra gruppi di carica opposta.
- **Dipendenza dalla distanza**: la forza è inversamente proporzionale al quadrato della distanza tra i gruppi carichi, e decresce più lentamente rispetto alle altre interazioni.
- **Ambiente**: la forza dell'interazione è maggiore in ambienti idrofobici, dove la costante dielettrica ε è più bassa.
- **Formula**:

$$F(r) = k \cdot \frac{q_A q_B}{r^2_{AB}} \qquad k = \frac{1}{4\pi\epsilon}$$

- **Rilevanza**: sono le interazioni più importanti nella fase iniziale, quando il farmaco entra nel sito di binding.

---

## 2. Legami Idrogeno

- **Forza**: variabile, 16–60 kJ/mol. Più deboli dei legami salini, ma più forti delle van der Waals.
- **Meccanismo**: coinvolgono un idrogeno già legato a un atomo (donatore) e un eteroatomo ricco di elettroni, N o O (accettore).
- **Direzionalità**: interazione tra orbitali, fortemente direzionale. Orientamento ottimale: il legame X–H punta direttamente al lone-pair su Y, con angolo X–H···Y idealmente di 180° (range accettabile 130–180°).

| Categoria | Esempi |
|---|---|
| **Accettori buoni** | Ioni carbossilati, fosfato, ammine terziarie |
| **Accettori moderati** | Acidi carbossilici, ammidi ossigenate, chetoni, esteri, eteri, alcoli |
| **Accettori deboli** | Zolfo, fluoro, cloro, anelli aromatici, ammidi azotate, ammine aromatiche |
| **Donatori buoni** | Ioni aminio HNR₃⁺ |

---

## 3. Interazioni di Van der Waals

- **Forza**: deboli, 2–4 kJ/mol.
- **Meccanismo**: avvengono tra regioni idrofobiche del farmaco e del target; regioni transienti di densità elettronica alta/bassa generano dipoli temporanei.
- **Dipendenza dalla distanza**: richiedono forte prossimità tra farmaco e sito di binding; l'interazione decade rapidamente con la distanza.
- **Rilevanza**: il contributo complessivo (sommato su molti contatti) è cruciale per il binding complessivo.

---

## 4. Interazioni Dipolo-Dipolo

- **Condizione**: richiedono che sia il farmaco sia il sito di binding possiedano momenti dipolari permanenti.
- **Meccanismo**: i dipoli si allineano quando il farmaco entra nel sito di legame, orientando la molecola — utile se anche gli altri gruppi funzionali si posizionano correttamente rispetto alle loro regioni di binding.
- **Dipendenza dalla distanza**: decresce più rapidamente delle interazioni elettrostatiche, ma più lentamente delle van der Waals.

---

## 5. Interazioni Ione-Dipolo

- **Meccanismo**: la carica di una molecola interagisce con il momento dipolare di un'altra.
- **Forza**: maggiore delle interazioni dipolo-dipolo.
- **Dipendenza dalla distanza**: decresce meno rapidamente con la distanza rispetto alle dipolo-dipolo.

---

## 6. Interazioni a Dipolo Indotto

- **Meccanismo**: la carica di una molecola induce un dipolo in un'altra.
- **Esempio tipico**: interazione tra ioni ammonio quaternari e anelli aromatici (interazione catione-π). L'acetilcolina forma questo tipo di interazione con il suo sito di legame.

---

## 7. Desolvatazione

- Le regioni polari del farmaco e del target sono solvatate prima dell'interazione farmaco-target.
- La desolvatazione, necessaria per permettere il legame, **richiede energia**.
- Perché il legame sia favorevole, l'energia di stabilizzazione guadagnata dal binding deve superare il costo energetico della desolvatazione.
- Una possibile strategia è la rimozione di gruppi polari dal farmaco — ma un'eccessiva rimozione compromette la solubilità.

---

## 8. Interazioni Idrofobiche

- **Rilevanza**: particolarmente importanti, aumentano significativamente l'energia di legame.
- **Meccanismo entropico**:
  1. Le molecole d'acqua formano attorno alle regioni idrofobiche uno strato di solvatazione molto ordinato → **entropia negativa**.
  2. Quando le regioni idrofobiche di farmaco e target interagiscono tra loro, lo strato di solvatazione si riduce, liberando le molecole d'acqua dal reticolo ordinato.
  3. Questo rilascio produce un **aumento entropico netto**, che favorisce termodinamicamente il binding.

---

## Riepilogo Comparativo

| Interazione | Forza relativa | Decadimento con la distanza |
|---|---|---|
| Ionica/salina | Molto forte | Lento (1/r²) |
| Legame idrogeno | Forte-moderata (16-60 kJ/mol) | Direzionale, media |
| Ione-dipolo | Moderata | Medio |
| Dipolo-dipolo | Moderata-debole | Più rapido delle elettrostatiche |
| Van der Waals | Debole (2-4 kJ/mol) | Molto rapido |
| Dipolo indotto | Debole | Rapido, richiede vicinanza |
| Idrofobica | Contributo entropico rilevante | Dipende dal contatto di superficie |
