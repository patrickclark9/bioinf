# Indexing

L'indicizzazione rappresenta una delle sfide più grandi per effettuare ricerca e trova la regione mappata con elevata accuratezza.

Gli indici possono essere invertiti (parola -> locazione), o forward (locazione -> parola).
 Algoritmi efficienti di indicizzazione sono essenziali per organizzare efficientemente  le sequenze del genoma di riferimento e le short read in memoria, oltre a consentire pattern di ricerca veloci.
 Molte strutture dati sono state proposte per l'utilizzo come indice:
 - Hash Tablke
 - Suffix tree
 - Suffix Array
 - Burrows-Wheeler Transform
 - Full-text minute space index

Banalmente, avendo un indice T ed una query Q:
- Spezziamo la query in sottostringe definite
- Si esplora l'indice T per vedere se le sottostringhe sono presenti
- Se presenti, si estende per vedere se l'intera sequenza ha un match

Un indice per il cromosoma 1 umano può occupare fino a 12GB di spazio. In questi casi, una soluzione pratica per ridurre lo spazio utilizzato è saltare alcune sottostringhe durante la creazione dell'indice. Includere ogni 4a sottostringa ad esempio può ridurre 12GB a 8GB per il cromosoma 1.
L'indice può essere rappresentato in una varietà di maniere incluse liste ordinate, hash table e alberi.

## Hash Table

Si costruisce una struttura stile dizionario in cui ogni sottostringa è una chiave a cui corrispondono i valori delle posizioni in cui quella chiave appare.

## Trees and Tries

Un'idea potrebbe essere costruire un indice usando sottostringhe di lunghezza 2 con un intervallo di 2, quindi skip ogni altra sottostringa.
La lista ordinata può essere convertita in una trie, che mapperà la sottostringa alla loro posizione (offset).
Ogni trie ha le seguenti proprietà:
- Ogni Arco è etichettato con un carattere da un dato alfabeto
- Ogni Nodo ha un singolo arco uscente corrispondente ad un carattere dell'alfabeto
- Ogni Chiave (sottostringa di lunghezza 2) viene estesa lungo un percorso partendo dalla radice
Un'altra idea è non utilizzare lunghezze fisse. In questo caso utilizziamo i suffissi invece di sottostringhe di lunghezza prefissata.
Prendendo T = abaaba$, in cui $ segna il termine del suffisso. Tutte le sottostringhe e le trie corrispondenti evidenzieranno un percorso, da cui possiamo trovare il suffisso più lungo ed il suffisso più corto.
Rimuovendo il carattere speciale la trie non avrebbe ogni suffisso rappresentato da un path dalla radice alla foglia.
Ogni nodo etichettato con una stringa si estende per tutti i caratteri che appaiono lungho un cammino dalla radice fino al nodo stesso.
La suffix-trie è una struttura dati ideali per controllare rapidamente che un pattern sia o non sia presente in un testo.

Si può usare una suffix trie anche per controllare che una stringa sia il suffisso di un testo o quante volte una particolare sottostringa viene trovata in un testo.

Se andiamo a collassare tutti i percorsi non ramificati e concatenando le etichette, si ottiene un albero in cui ogni foglia è etichettata con un offset del corrispondente suffisso.

La logica rimane uguale ai suffix trie, ad eccezione che ora bisogna tener conto del fatto che lungo alcuni archi solo una porzione dei caratteri di un etichetta combacieranno.

Una comune applicazione degli alberi suffix dell'analisi dei genomi è trovare la più comune subsequenza tra due sequenze.

## Suffix array
I suffix array invece offrono una soluzione più compatta per rappresentare i suffissi del testo. Specifica un ordine lessicografico ordinando i suffissi derivati dal testo T. Poichè non è necessario un ulteriore albero per la rappresentazione, utilizza vastamente meno memoria (12GB per il genoma umano contro i 47GB del suffix tree)


## Burrows Wheeler Transform

La BW è una permutazione reversibile di una stringa. Ha tre importanti feature che la rendono ideale per creare compatte e facili da esplorare rappresentazioni di dati genomici.
- Può essere compressa
- Può essere invertita per ricostruire la stringa originale
- Può essere usata come indice
Prendendo la stringa originale, si aggiunge $ alla fine della stringa e si ordina per carattere nel test (T-Ranking)
L'ordine del ranking viene mantenuto tra la prima colonna e l'ultima colonna.
Si prende poi la colonna F e la colonna L e si organizzano i caratteri in ordine di apparizione.
Il mapping LF può essere usato per ricostruire il testo originale dalla sua trasformata in BW.
Si inizia a leggere dalla destra nella stringa T e ci si muove verso sinistra.

Inizio nella prima riga -> F deve avere $. L contiene un carattere appena prima di $. es a0
a0: LF dice che questa  occorenza di a è la prima a in F. Si salta alla riga che inizia con a0. L contiene il carattere appena prima di a0, b0.
Si ripete per b0 ottenendo a2. Si ripete per a2 ottenendo a1, per a1 si ottiebe b1, per b1 si ottiene a3, per a3 si ottiene $, quindi termina l'algoritmo.

Possiamo quidi usare il mapping LF per trovare una stringa in una BWT. es. sottostringa aba in BWT  o bba, che non risulterà in alcun match.

La BWT è molto compatta, ma ha svantaggi. Ad esempio, la difficoltà nel trovare dove i match sono nel genoma, oltre ad alcuni problemi di prestazioni.
Combinare la BWT con strutture dati ausiliari come l'FM index (Full text index in Minute space), può aiutare.
Le componenti dell'FM index utilizzate per allineare read al genoma sono Tally, Checkpoints e suffix arrays index.
Tally-> conta le occorrenze di un carattere dall'inizio della colonna L. Per conservare spazio, solo un sottoinsieme di tally vengono memorizzate come checkpoint, salvati in intervalli regolari