# [[Ecotyper]]
## Columns

| Colonna                        | Significato                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| State_Assignment.{CellType}    | [[Ecotyper]] scompone il tipo cellulare in sottostati trascrizionali, e la colonna indica a quale stato trascrizionale è stato assegnato il campione per quel tipo cellulare, ovvero qual è il sottotipo trascrizionale dominante di quel tipo cellulare per quel dato campione. Se NaN, l'abbondanza stimata di quel tipo cellulare nel campione era troppo bassa per un'assegnazione affidabile                                                                                                        |
| State_Abundance.{CellType}_S0N | $\text{Valori}\in [0,1]$. Punteggio continuo di abbondanza per ogni singolo stato all'interno di un tipo cellulare. La somma degli stati approssima la frazione totale di quel tipo cellulare nel campione.                                                                                                                                                                                                                                                                                              |
| EcoType_Assignment             | È una singola etichetta per campione (CE1-CE10). Rappresenta la comunica multicellulare dominante. Si cercano pattern di co-occorrenza tra gli stati di tipi cellulari diversi (un certo stato S0N di fibroblasti che tende a comparire insieme ad un certo stato S0N dei macrofagi). Vengono raggruppati in 10 ecotupi conservati. La colonna dice a quale dei 10 ecotipi è stato assegnato il campione nel complesso. NaN quando nessuno ecotipo ha un punteggio significativo(?) rispetto agli altri. |
| EcoType_Abundance.CE1>10       | Punteggio continuo per ciascuno dei 10 ecotipi distinti nel campione.                                                                                                                                                                                                                                                                                                                                                                                                                                    |

Possiamo osservare una variazione degli stati trascrizionali non solo per tipo cellulare, ma all'interno dei tipi stessi. Lo stato S0 di B-Cells è trascrizionalmente diverso da S1 di B-Cells, e sono due stati caratterizzati da profili di espressione differenti.

## Step (Forse)

1. **Frazionamento** CIBERSORTx Fractions -> Stima dell'infiltrato per i 12 tipi cellulari, conta grezza, assente nel dataset
2. **Purificazione** CIBERSORTx HiRes -> Usando i frazionamenti, viene imputato un profilo di espressione per tipo cellulare per campione
3. **State Discovery** NMF -> NMF sui top 1000 geni per dispersione più elevata tra i campioni. Ogni "gene program" è uno stato cellulare (69 totali?)
4. **QC** -> Rimozione stati a bassa qualità (i NaN)
5. **Validazione** ->Validazione con dati single-cell e clinici.
6. **EcoTyping** -> Raggruppamento di stati che co-occorrono tra campioni in 10 comunità multicellulari (CE1-CE10)



> Gene Program:
> Tutti elementi non-negativi
> NMF = $$V \approx WH $$

> **Citotossico** significa una sostanza o un agente che danneggia, intossica o distrugge le cellule viventi.