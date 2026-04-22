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

Un indice per il cromosoma 1 umano può occupare fino a 12GB di spazio. In questi casi, una soluzione pratica per ridurre lo spazio utilizzato è saltare l'aggiun
