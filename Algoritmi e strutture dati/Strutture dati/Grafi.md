>[!note]
>La struttura dati più naturale per rappresentare un insieme di oggetti legati da una generica relazione tra loro è il grafo. Formalmente un grafo è una coppia $G=(V,E)$ con $V$ un insieme di nodi ed $E$ un insieme di archi. Se un grafo ha $|V|$ nodi esso ha al più $|V|^{2}$ archi.
>
>Due nodi collegati da un arco si dicono adiacenti. Un cammino tra due nodi $v_{1}$ e $v_{2}$ è un insieme di archi di cui il primo ha origine in $v_{1}$, l'ultimo termina in $v_{2}$ e ogni nodo compare almeno una volta come destinazione di un arco e come sorgente.
>
>È possibile implementare un grafo con una lista di adiacenza o matrice di adiacenza.
>
>Una lista di adiacenza è un vettore di liste lungo $|V|$, indicizzato dai nomi dei nodi. Ogni lista contiene i nodi adiacenti all'indice della sua desta. Ha complessità spaziale $\Theta(|V|+|E|)$. Per determinare se un arco appartiene al grafo ha complessità $\mathcal{O}(|V|)$, e per determinare il numero di archi $o_{e}$ uscenti di un nodo ha complessità $\mathcal{O}(o_{e})$.
>
>Una matrice di adiacenza è una matrice di valori booleani $|V|\times|V|$ con righe e colonne indicizzate dai nomi dei nodi. La cella alla riga $i$ colonna $j$ contiene $1$ se l'arco $(v_{i},v_{j})$ è presente nel grafo, $0$ altrimenti. Ha complessità spaziale $\Theta(|V|^{2})$. Per determinare se un arco appartiene al grafo ha complessità $\mathcal{O}(1)$, e per determinare il numero di archi $o_{e}$ uscenti di un nodo ha complessità $\mathcal{O}(|V|)$.

Un grafo è detto orientato se la coppia di noti che costituisce un arco è ordinata, o in altre parole se ciò che collega i nodi ha un verso. Un grafo orientato viene rappresentato indicando gli archi come frecce che puntano al secondo nodo della coppia. In un grafo non orientato, l'insieme di archi può essere rappresentato in modo compatto dato che se $(v_{1},v_{2})\in E$, allora anche $(v_{2},v_{1})\in E$.

Un grafo è detto connesso se esiste un percorso per ogni coppia di nodi.
Un grafo è detto completo se esiste un arco per ogni coppia di nodi.
Un percorso è un ciclo se il nodo di inizio e di fine coincidono, un grafo privo di cicli è detto aciclico.

Nei grafi non orientati, siccome la matrice di adiacenza è simmetrica rispetto alla diagonale posso stoccarne solo metà, mentre nelle liste di adiacenza posso stoccare solo uno dei due archi raddoppiando il tempo di ricerca per un nodo adiacente.

>[!tip] Visita in ampiezza
>Come per le visite degli alberi, è possibile stampare i nodi in una visita di un grafo, `VisitaAmpiezza` si può quindi trasformare in algoritmo di ricerca. Ha complessità totale $\mathcal{O}(|V|+|E|)$.
>
>```
>VisitaAmpiezza(G,s)
>	for each n in V except s
>		n.color <- white
>		n.dist <- infinity
>	
>	s.color <- grey
>	s.dist <- 0
>	Q <- 0
>	Enqueue(Q,s)
>	
>	while !isEmpty(Q)
>		curr <- Dequeue(Q)
>		for each v in curr.adiacenti
>			if v.color = while
>				v.color <- grey
>				v.dist <- curr.dist + 1
>				Enqueue(Q,v)
>		curr.color <- black
>```
>
>È anche possibile visitare in profondità, dove, diversamente dalla visita in ampiezza visitiamo prima i nodi adiacenti a quello dato, e poi il nodo stesso.

>[!tip] Componenti connesse
>È detta componente connessa di un grafo $G$ un insieme $S$ di nodi tali per cui esiste un cammino tra ogni coppia di essi, ma nessuno di essi è connesso a nodi non in $S$. Individuare le componenti connesse in un grafo equivale ad etichettare i nodi con lo stesso valore se appartengono alla stessa componente. Ha complessità $\mathcal{O}(|V|+|E|)$.
>
>```
>ComponentiConnesse(G)
>	for each v in V
>		v.etichetta <- -1
>	eti <- 1
>	for each v in V
>		if v.etichetta = -1
>			VisitaEdEtichetta(G,v,eti)
>			eti <- eti + 1
>```
>
>Dove il metodo `VisitaEdEtichetta` funziona come `VisitaAmpiezza` o `VisitaProfondità` ma imposta a `eti` il campo `etichetta` del nodo visitato.

>[!tip] Ordinamento topologico
>Dato un grafo orientato, definiamo il predecessore di un nodo $v$ un nodo $u$ tale per cui esiste un cammino da $u$ a $v$.
>Un valore utile da calcolare per un grafo orientato aciclico è il cosiddetto ordinamento topologico. L'ordinamento topologico è una sequenza di nodi del grafo tale per cui nessun nodo compare prima di un suo predecessore. L'ordinamento topologico non è unico.
>
>Se il grafo non è connesso le componenti connesse possono essere ordinate in qualunque modo l'una rispetto all'altra.
>
>```
>VisitaProfOT(G,s,L)
>	s.color <- grey
>	for each v in curr.adiacenti
>		if v.color = white
>			VisitaProfOT(G,v,L)
>	s.color <- black
>	PushFront(L,s)
>
>OrdinamentoTopologico(G)
>	for each v in V
>		v.color <- white
>	
>	for each v in V
>		if v.color = white
>			VisitaProfOT(G,v,L)
>	return L
>```

>[!tip] Algoritmo di Dijkstra
>L'algoritmo di Dijkstra trova, dato un grafo orientato e un suo nodo $s$ i percorsi più previ da un nodo a qualunque altro. Funziona sia su un grafo classico che su un grafo pesato.
>
>Funziona inserendo ogni $v\in V\smallsetminus\set{s}$ in un insieme $Q$, dopo aver impostato il suo attributo distanza a $\infty$ e il `v.pred` a `NIL`. Inserisco $s$ in $Q$ dopo aver impostato `s.dist <- 0` e `s.pred <- NIL`. Quindi, fino a quando $Q$ non è vuoto, estraggo il nodo `c` con `dist` minima e controllo per ogni adiacente `a` se hanno distanza minore di `c.dist + peso(c,a)`. Se questo accade imposto `a.pred <- c` e `a.dist <- c.dist + peso(c,a)`.
>
>È possibile migliorare la complessità memorizzando l'insieme $Q$ come una coda con priorità usando un min-heap. Questo algoritmo ha complessità $\mathcal{O}((|E|+|V|)\log(|V|))$.
>
>```
>DijkstraQueue(G,s)
>	Q <- 0
>	s.dist <- 0
>	
>	for each v in V
>		if v != s
>			v.dist <- infinity
>			v.pred <- NIL
>		AccodaPri(Q,v,v.dist)
>	
>	while Q != 0
>		u <- CancellaMin(Q)
>		for each v in u.succ
>			ndis <- u.dist + peso(u,v)
>			if v.dist > ndis
>				v.dist <- ndis
>				u.prev <- u
>				DecrementaPri(Q,v,ndis)
>```

>[!tip] Algoritmo di Floyd
>Dato un grafo orientato, in cui ogni nodo ha un solo successore, l'algoritmo di Floyd determina, a partire da un nodo iniziale se il cammino genera un ciclo. Ha complessità $\Theta(2(T+C)-r)$, dove $T$ è la lunghezza della coda che precede il ciclo, $C$ è la lunghezza del ciclo e $r= T\text{ mod }C$.
>
>```
>FloydLT(G,x)
>	t <- x.succ
>	l <- x.succ.succ
>	
>	while l != t
>		t <- t.succ
>		l <- l.succ.succ
>	
>	T <- 0
>	t <- x
>	
>	while l != t
>		t <- t.succ
>		l <- l.succ
>		T <- T + 1
>	
>	l <- t
>	C <- 0
>	while l != t
>		l <- l.succ
>		C <- C + 1
>	
>	return T,C
>```

