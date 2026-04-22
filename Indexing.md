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
