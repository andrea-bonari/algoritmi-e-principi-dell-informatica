>[!note]
>Un albero è una struttura dati versatile costituito da un insieme di nodi e di archi che li collegano. Ogni nodo ha al più un arco entrante, ma un numero arbitrario di archi uscenti. Sono una rappresentazione efficiente per insiemi di dati ordinati.
>![[Pasted image 20250514160715.png|center]]

Definiamo la radice come il nodo dell'albero privo di arco entrante, una foglia come un nodo senza archi uscenti, un padre di un nodo $n$ il nodo da cui l'arco entrante in $n$ ha origine, e figlio di un nodo $n$ il nodo in cui uno degli archi uscenti da $n$ termina.

Definiamo inoltre il livello come la distanza, in numero di archi, di un nodo dalla radice, e un albero completo, come un albero in cui tutti i livelli hanno tutti i nodi tranne l'ultimo.

>[!tip] Albero binario
>Definiamo un albero binario come un albero in cui ogni nodo ha al più due figli.
>
>Dando una sua definizione ricorsiva, un albero è formato da un nodo radice a cui sono collegati due alberi, il sottoalbero destro e quello sinistro. Un albero può essere vuoto. Similmente per quanto fatto per le tabelle hash, indicizzeremo i nodi con una chiave.
>
>Dato un nodo `A`, `A.left` è il riferimento al figlio sinistro, `A.right` al destro, `A.p` è un riferimento al padre, `A.key` è la chiave. Inoltre ogni albero `A` ha un riferimento `A.root` alla radice.
>
>È possibile utilizzare un vettore per contenere le chiavi. Questo approccio è molto efficiente se l'albero è completo. Si ha che la radice dell'albero è stoccata nella prima posizione del vettore. Dato un nodo contenuto in posizione $i$ il suo figlio sinistro è in posizione $2i+1$, il destro in $2i+2$. Inoltre il padre del nodo stoccato in posizione $i$ si trova in posizione $\lfloor \frac{i-1}{2}\rfloor$.

Su di un albero è possibile effettuare operazioni di inserimento, ricerca e cancellazione di nodi. L'operazione caratteristica degli alberi è il cosiddetto attraversamento o visita per enumerare le chiavi contenute.

### Vista di alberi binari
>[!note]
>La definizione degli algoritmi di visita è ricorsiva, il fattore discriminante tra essere è l'ordine in cui i nodi vengono visitati. Gli algoritmi sono rispettivamente la visita in ordine, anticipata e posticipata, e tutti e tre hanno complessità temporale $\Theta(n)$.
>```
>InOrder(T)
>	InOrder(T.left)
>	Print(T.key)
>	InOrder(T.right)
>
>PreOrder(T)
>	Print(T.key)
>	PreOrder(T.left)
>	PreOrder(T.right)
>
>PostOrder(T)
>	PostOrder(T.left)
>	PostOrder(T.right)
>	Print(T.key)
>```

### Alberi binari di ricerca
>[!note]
>Definiamo un albero binario di ricerca (BST) come un albero binario per cui per ogni nodo `x` vale:
>- Se `y` è contenuto nel sottoalbero sinistro di `x`, allora `y.key <= x.key`
>- Se `y` è contenuto nel sottoalbero destro di `x`, allora `y.key >= x.key`
>
>Inserimenti e cancellazioni devono preservare questa proprietà. Inoltre una visita in ordine del BST stampa le chiavi in ordine.

>[!tip] Ricerca su BST
>Questo algoritmo ha complessità $\mathcal{O}(h)$ con $h$ altezza dell'albero. Nel caso ottimo (albero ben bilanciato) diventa $\mathcal{O}(\log(n))$, mentre nel caso pessimo (albero degenere in lista) diventa $\mathcal{O}(n)$.
>
>```
>Ricerca(T,x)
>	if T=NIL or T.key = x.key
>		return T
>	
>	if T.key < x.key
>		return Ricerca(T.right, x)
>	else
>		return Ricerca(T.left, x)
>```

>[!tip] Minimo e massimo su BST
>L'elemento con chiave minima (o massima) è quello più a sinistra (o destra) del BST. Ciascuno dei due algoritmi ha complessità $\mathcal{O}(h)$.
>
>```
>Min(T)
>	cur <- T
>	
>	while cur.left != NIL
>		cur <- cur.left
>	
>	return cur
>
>Max(T)
>	cur <- T
>	
>	while cur.right != NIL
>		cur <- cur.right
>	
>	return cur
>```

>[!tip] Successore su BST
>Il successore di un elemento `x` è l'elemento `y` con la più piccola chiave `y.key > x.key` presente nel BST. Nel cercarlo sono possibili due casi:
>- Il sottoalbero destro di `x` non è vuoto: il successore è il minimo di quel sottoalbero $\mathcal{O}(h)$
>- Il sottoalbero destro di `x` è vuoto: il successore è il progenitore più prossimo a `x` per cui `x` appare nel suo sottoalbero sinistro $\mathcal{O}(h)$
>
>```
>Successore(x)
>	if x.right != NIL
>		return Min(x.right)
>	
>	y <- x.p
>	while y != NIL and y.right = x
>		x <- y
>		y <- y.p
>	
>	return y
>```

>[!tip] Inserimento su BST
>L'inserimento di un nuovo elemento deve rispettare la proprietà fondamentale del BST. Assumendo che il BST non debba contenere duplicati, cerchiamo l'elemento che vogliamo inserire nel BST, e se non lo troviamo lo inserisco al posto del NIL trovato $\mathcal{O}(h)$
>
>```
>Inserisci(T,x)
>	pre <- NIL
>	cur <- T.root
>	
>	while cur != NIL
>		pre <- cur
>		if x.key < cur.key
>			cur <- cur.left
>		else
>			cur <- cur.right
>	
>	x.p <- pre
>	
>	if pre = NIL
>		T.root <- x
>	elseif x.key < pre.key
>		pre.left <- x
>	else
>		pre.right <- x
>```

>[!tip] Cancellazione su BST
>La strategia di cancellazione di un elemento da un BST dipende dal numero di figli dell'elemento in questione.
>Nel primo caso l'elemento non ha figli, ed è sufficiente eliminarlo dall'albero deallocandolo e impostando il puntatore del padre a NIL.
>Nel secondo caso l'elemento ha un figlio. In questo caso l'elemento viene sostituito dal figlio nel suo ruolo nell'albero.
>Nel terzo casi l'elemento ha due figli. Copiamo quindi il valore del suo successore su di esso ed elimino il successore.
>
>```
>Cancella(T,x)
>	if x.left = NIL or x.right = NIL
>		da_canc <- x
>	else
>		da_canc <- Successore(x)
>	
>	if da_canc.left != NIL
>		sottoa <- da_canc.left
>	else
>		sottoa <- da_canc.right
>	
>	if sottoa != NIL
>		sottoa.p <- da_canc.p
>	
>	if da_canc.p = NIL
>		T.root <- sottoa
>	elseif da_canc = da_canc.p.left
>		da_canc.p.left <- sottoa
>	else
>		da_canc.p.right <- sottoa
>	
>	if da_canc != x
>		x.key <- da_canc.key
>	
>	Free(da_canc)
>```

Nel migliore dei casi $h=\log(n)$, mentre nel peggiore $h=l$. È dimostrabile che l'altezza attesa di un BST è $\mathcal{O}(\log(n))$ se le chiavi inserite hanno distribuzione uniforme.

>[!tip] Albero bilanciato
>Un albero è bilanciato se, per ogni nodo, le altezze dei due sottoalberi differiscono al più di $1$.

### Alberi Rosso-Neri
>[!note]
>Un albero rosso-nero è un BST i cui nodi sono dotati di un attributo aggiuntivo detto $\text{colore}\in\set{\text{rosso},\text{nero}}$, e soddisfacente le seguenti proprietà:
>- Ogni nodo è rosso o nero
>- La radice è nera
>- Le foglie sono nere
>- I figli di un nodo rosso sono entrambi neri
>- Per ogni nodo dell'albero, tutti i cammini dai suoi discendenti alle foglie contenute nei suoi sottoalberi hanno lo stesso numero di nodi neri.
>
>Chiamiamo, per comodità, altezza nera di un nodo $x$ il valore $\text{bh}(x)$ pari al numero di nodi neri, escluso $x$ se è il caso, nel percorso che va da $x$ alle foglie.
>
>Per convenzione i dati sono mantenuti unicamente nei nodi interni, le foglie sono tutte `NIL`. Per semplicità, tutte le foglie sono fisicamente rappresentate da un singolo nodo, il cui unico riferimento `T.nil` è conservato nella struttura dati.
>Il padre del nodo radice punta anch'esso a `T.nil`.

Tutte le operazioni che non vanno a modificare la struttura dell'albero sono identiche ai BST.

È necessario essere in grado di ribilanciare l'albero con modifiche solamente locali.

>[!tip] Proprietà di buon bilanciamento
>Un albero RB con $n$ nodi ha altezza massima $2\log(n+1)$. Di conseguenza le operazioni che restano invariate tra RBT e BST sono $\mathcal{O}(2\log(n+1))$ .

>[!example] Dimostrazione
>Dimostriamo per induzione che un sottoalbero con radice $x$ ha almeno $2^{\text{bh}(x)}-1$ nodi interni.
>
>Per il caso base (altezza $0$), $x$ è una foglia e il sottoalbero contiene almeno: $$2^{\text{bh}(x)}-1=2^{0}-1=0\text{ nodi interni}$$
>Per il passo, dato $x$ entrambi i suoi figli hanno altezza nera $\text{bh(x)}$ o $\text{bh}(x)-1$. Dato che l'altezza dei figli è minore di quella di $x$, i loro sottoalberi hanno almeno $2^{\text{bh}(x)-1}-1$ nodi interni. L'albero radicato in $x$ contiene quindi almeno: $$2^{\text{bh}(x)-1}-1+2^{\text{bh}(x)-1}-1+2=2^{\text{bh(x)}}\text{ nodi interni}$$
>Si ha che almeno metà dei nodi su un qualunque percorso radice-foglia sono neri. L'altezza nera della radice è almeno $\frac{h}{2}$, e per quanto detto prima il sottoalbero radicato in essa contiene almeno $2^{\frac{h}{2}}-1$ nodi. Risolvendo $h$ per $n\geq 2^{\frac{h}{2}}-1$ si ha: $$h\leq2\log(n+1)$$

>[!tip] Rotazione BST
>La rotazione è un operazione locale a due nodi di un BST che cambia il livello a cui sono situati due nodi senza violare le sue proprietà.
>```
>LeftRotate(T,x)
>	y <- x.right
>	x.right <- y.left
>	
>	if y.left != T.nil
>		y.left.p <- x
>	y.p <- x.p
>	
>	if x.p = T.nil
>		T.root <- y
>	else if x = x.p.left
>		x.p.left <- y
>	else
>		x.p.right <- y
>	
>	y.left <- x
>	x.p <- y
>```
>La definizione del metodo `RightRotate` è analoga.

>[!tip] Inserimento RBT
>L'inserimento procede ad inserire il nuovo elemento come se l'albero fosse un semplice BST salvo l'assegnamento del valore dei sottoalberi del nodo `T.nil` al posto di `NIL` se viene inserito come una foglia, l'assegnamento del valore del genitore del nodo a `T.nil` al posto di `NIL` se il nodo è inserito come radice, e infine colorare il nodo appena inserito di rosso. Definiamo quindi un metodo `RiparaRBInserisci(z)` che, dato il nodo inserito `z`, con `z.p` figlio sinistro (o destro) del nonno di `z`: ci sono 3 casi a seconda del colore dello "zio" e della posizione di `z` rispetto a `z.p`. L'intera riparazione prende al più $\mathcal{O}(\log(n))$, e l'inserimento, comprensivo di riparazione è $\mathcal{O}(\log(n))$.
>
>```
>RiparaRBInserisci(T,z)
>	while z.p.color = red
>		if z.p = z.p.p.left
>			y <- z.p.p.right
>			if y.color = red
>				z.p.color <- black
>				y.color <- black
>				z.p.p.color <- red
>				z <- z.p.p
>			else
>				if z = z.p.right
>					z <- z.p
>					LeftRotate(z)
>				z.p.color <- black
>				z.p.p.color <- red
>				RightRotate(z.p.p)
>		else
>			y <- z.p.p.left
>			if y.color = red
>				z.p.color <- black
>				y.color <- black
>				z.p.p.color <- red
>				z <- z.p.p
>			else
>				if z = z.p.left
>					z <- z.p
>					RightRotate(z)
>				z.p.color <- black
>				z.p.p.color <- red
>				LeftRotate(z.p.p)
>	T.root.color <- black
>```

>[!tip] Cancellazione RBT
>La cancellazione procede a cancellare il nuovo elemento come se l'albero fosse un semplice BST salvo l'uso di `T.nil` al posto di `NIL` e l'invocazione di una procedura che ripara eventuali violazioni delle proprietà RB. Nel caso sia eliminato un nodo rosso, non è necessario alcun cambiamento, tuttavia se il nodo eliminato è nero `RiparaRBCancella(x)`, dato il nodo `x` presente al posto di quello cancellato `z` ripristina le proprietà. La procedura complessiva di cancellazione da alberi RB è $\mathcal{O}(\log(n))$.

