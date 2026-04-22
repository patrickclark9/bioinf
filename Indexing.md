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
Rimuovendo il carattere speciale la trie non avrebbe o
