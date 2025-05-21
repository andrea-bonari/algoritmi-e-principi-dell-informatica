>[!note]
>Un mucchio (heap) è una struttura dati ad albero dove la chiave del nodo padre è sempre maggiore di quella dei figli (max-heap). In questa struttura dati non sussiste una relazione tra le chiavi di due fratelli. Se l'albero è binario parliamo di mucchi binari (binary heaps).

È possibile definire una variante in cui la chiave del padre è sempre minore di quella dei figli (min-heap).

In generale, gli heap, e in particolare gli heap binari, trovano uso per implementare code con priorità e ordinare vettori. Le operazioni su un max-heap sono `Max`, `Inserisci`, `Cancella-Max`, `Costruisci-Max-Heap`, `Max-Heapify`.

>[!tip] Costruzione di un max-heap
>È possibile costruire un max-heap da un vettore usando l'algoritmo `Costruisci-Max-Heap`:
>
>```
>Costruisci-Max-Heap(A)
>	A.heapsize <- A.length
>	for i <- floor(A.length / 2) downto 1
>		Max-Heapify(A,i)
>
>Max-Heapify(A,n)
>	l <- Left(n)
>	r <- Right(n)
>	
>	if <= A.heapsize and A[l] > A[n]
>		posmax <- l
>	else
>		posmax <- n
>	
>	if r <= A.heapsize and A[r] > A[posmax]
>		posmax <- r
>	
>	if posmax != n
>		Swap(A[n], A[posmax])
>		Max-Heapify(A,posmax)
>``` 
>Dove `Max-Heapify(A,n)` riceve un array e una posizione in esso: assume che i due sottoalberi con radice stoccata in `Left(n) = 2n` e `Right(n) = 2n + 1` siano dei max-heap. Modifica quindi `A` in modo che l'albero radicato in `n` sia un max-heap. Nel caso pessimo in un heap contenente $n$ elementi  `Max-Heapify` ha complessità $\mathcal{O}(\log(n))$. In totale `Costruisci-Max-Heap` ha complessità $\mathcal{O}(n\log(n))$.

### Code con priorità
>[!note]
>Una coda con priorità è una struttura dati a coda in cui è possibile dare una priorità numerica agli elementi all'interno. Elementi con priorità maggiore verranno estratti sempre prima di elementi con priorità minore indipendentemente dall'ordine di inserimento. L'implementazione più comune è con un max-heap.

>[!tip] Max e Cancella-Max
>`Max` e `Cancella-Max` ci permettono di esaminare ed estrarre l'elemento a priorità massima.
>
>```
>Max(A)
>	return A[1]
>
>Cancella-Max(A)
>	if A.heapsize < 1
>		return NIL
>	
>	max <- A[1]
>	A[1] <- A[A.heapsize]
>	Max-Heapify(A,1)
>	return max
>```
>
>L'ispezione è $\mathcal{O}(1)$, mentre l'estrazione costa $\mathcal{O}(\log(n))$, che è più efficace di un vettore ordinato ($\mathcal{O}(n)$).

>[!tip] Inserimento
>L'algoritmo di inserimento inserisce l'elemento `key` come ultima foglia, fa dunque scalare l'elemento fino a quando non è minore del padre. Nel caso pessimo ha complessità $\mathcal{O}(\log(n))$.
>
>```
>Inserisci(A,key)
>	A.heapsize <- A.heapsize + 1
>	A[A.heapsize] <- key
>	i <- A.heapsize
>	while i > 1 and A[Parent(i)] < A[i]
>		Swap(A[Parent(i)], A[i])
>		i <- Parent(i)
>```

### Heapsort
>[!note]
>L'algoritmo di Heapsort ordina un vettore `A` costruendo da esso un max-heap, scambiando l'elemento più grande con l'ultima foglia e decrementando la sua dimensione e riordinando l'elemento messo in testa.
>
>```
>HeapSort(A)
>	Costruisci-Max-Heap(A)
>	for i <- A.length downto 2
>		Swap(A[1],A[i])
>		A.heapsize <- A.heapsize - 1
>		Max-Heapify(A,1)
>```
>
>Questo algoritmo ha complessità $\mathcal{O}(n\log(n))$ nel caso pessimo, e necessita solamente di $\mathcal{O}(1)$ spazio ausiliario. Nel caso medio è più lento di QuickSort, tuttavia resta il vantaggio della complessità di caso pessimo garantita. Non è stabile.

