>[!note]
>Dato un problema, si concepisce un algoritmo che lo risolve, ne valutiamo la complessità e, se la complessità è soddisfacente, lo implementiamo.
>
>Per valutare la complessità ci serve rappresentare l'algoritmo in una qualche forma.

### Pseudocodice
>[!note]
>Ogni algoritmo è rappresentato con una procedura. Si usano operatori aritmetici come nel C e assegnamento `<-`. Per i commenti mono riga si usa `▷`. Si hanno inoltre disponibili i costrutti di controllo `while`, `for` e `if-else`. Tutte le variabili sono locali alla procedura descritta, e il loro tipo non è esplicito. La notazione degli array è identica al C, con la differenza che gli indici iniziano da `1`. Inoltre sono disponibili anche i sotto-array `A[i..j`. Sono presenti anche aggregati eterogenei (come gli struct in C), con la differenza che una variabile di tipo aggregato è un puntatore alla struttura. Il passaggio parametri ad una procedura è effettuato, per tipi non aggregati per copia, mentre per tipi aggregati per riferimento.
>
>Lo pseudocodice è eseguito dalla macchina RAM, e assumiamo che un singolo statement di assegnamento tra tipi base è tradotto in un numero costante $k$ di istruzioni dell'assembly RAM.

Adottiamo il criterio di costo costante per l'esecuzione dei nostri algoritmi. Ogni statement semplice di pseudocodice è eseguito in $\Theta(k)$. Focalizzeremo la nostra analisi sulla complessità temporale degli algoritmi.

Si ha che il costo totale $T(n)$ con un equazione di ricorrenza è pari a: $$T(n)=\begin{cases}
\Theta(1)&\text{ se }n<c \\
D(n)+a T\left( \frac{n}{b}\right)+C(n)&\text{ altrimenti}
\end{cases}$$

### Calcolo della complessità degli algoritmo ricorsivi
>[!note]
>Sono possibili 3 tecniche principali:
>- Sostituzione
>- Esame dell'albero di ricorsione
>- Teorema dell'esperto (master theorem)
>
>Usiamo come caso di studio la ricerca binaria, cioè il problema di cercare in un vettore lungo $n$ come quello di cercare nelle sue metà superiori e inferiori. Abbiamo che il costo della suddivisione è costante $D(n)=\Theta(1)$, il costo di ricombinazione è costante, cioè sappiamo che una delle due metà non contiene per certo l'elemento cercato $C(n)=\Theta(1)$. Quindi esprimiamo la complessità come: $$T(n)=\Theta(1)+T\left(\frac{n}{2}\right)+\Theta(1)$$

>[!tip] Metodo di sostituzione
>Il metodo di sostituzione si articola in tre fasi:
>- Intuire una possibile soluzione
>- Sostituire la presunta soluzione nella ricorrenza
>- Dimostrare per induzione che la presunta soluzione è tale per l'equazione/disequazione delle ricorrenze.

>[!tip] Albero di ricorsione
>L'albero di ricorsione fornisce un aiuto per avere una congettura da verificare con il metodo di sostituzione, o un appiglio per calcolare la complessità esatta. È una rappresentazione delle chiamate ricorsive, con la loro complessità. Ogni chiamata costituisce un nodo in una sorta di albero genealogico: i chiamati appaiono come figli del chiamante. Ogni nodo contiene il costo della chiamata, senza contare quello dei discendenti.
>
>Per esempio, l'albero $T(n)=T\left( \frac{n}{3}\right)+ T\left(\frac{ 2n}{3}\right)+n$:
>![[Pasted image 20250430190201.png|center]]
>
>L'albero ha la ramificazione a profondità massima posta all'estrema destra del disegno precedente. Sappiamo che essa ha profondità $k$ che ricaviamo ponendo $\frac{2^{k}}{3^{k}}n=1$. Facendo un po di algebra ricaviamo $(\log_{2}(3)-1)k=\log_{3}(n)$, e quindi $k=c\log_{3}(n)$. Quindi il costo pessimo per il contributo di un dato livello è l'$n$ del primo livello, e quindi $T(n)=\Theta(n\log(n))$.

>[!tip] Master theorem
>Data una ricorrenza nella seguente forma: $$T(n)=a T\left(\frac{n}{b}\right)+f(n)\qquad a\geq1,b>1$$
>Confrontiamo $a^{\log_{b}(n)}=a^{\frac{\log_{a}(n)}{\log_{a}(b)}}=n^{\log_{b}(a)}$. Se abbiamo che:
>- $a\geq1$ costante
>- $f(n)$ sommata, non sottratta
>- Legame tra $n^{\log_{b}(a)}$ e $f(n)$ polinomiale
>
>Nel caso $f(n)=\mathcal{O}(n^{\log_{b}(a)-\epsilon})$ per un qualunque $\varepsilon>0$, allora la complessità risultante: $$T(n)=\Theta(n^{\log_{b}(a)})$$
>Nel caso $f(n)=\Theta(n^{\log_{b}(a)})$, la complessità risultante: $$T(n)=\Theta(n^{\log_{a}(b)}\log(n))$$
>Nel caso $f(n)=\Omega(n^{\log_{b}(a)+\epsilon})$ per un qualunque $\epsilon<1$, e vale $af\left( \frac{n}{b}\right)< cf(n)$ per un qualunque $c<1$, la complessità risultante: $$T(n)=\Theta(f(n))$$

### Insertion sort
>[!note]
>
>```
>InsertionSort(A)
>	for i <- 2 to A.lenght
>		tmp <- A[i]
>		j <- i - 1
>		while j >= 1 and A[j] > tmp
>			A[j+1] <- A[j]
>			j <- j - 1
>		A[j + 1] <- tmp
>```
>
>Si ha che, seleziono un elemento e lo reinserisco nella porzione di vettore già ordinato, al suo posto. Si ha nel caso ottimo $T(n)=\Theta(n)$, nel caso pessimo $T(n)=\Theta(n^{2})$ e nel caso medio $\mathcal{O}(n^{2})$. La complessità spaziale $S(n)=\Theta(1)$. L'algoritmo è stabile.
>>[!tip]- Visualizzazione
>>![[insertion.webp]]

>[!tip]
>Contando le azioni di confronto e scambio generiche di un vettore ricaviamo un albero con tante foglie quante permutazioni del vettore da ordinare. Assumendo che la struttura sia la più compatta possibile, la lunghezza del più lungo dei percorsi radice-foglia è il numero massimo di confronti che devo fare per ordinare un vettore, allora l'altezza dell'albero in questo caso è $\log_{2}$ del numero delle sue foglie: $$\log(n!)\simeq n\log(n)-\log(e)n+\mathcal{O}(\log_{2}(n))$$
>Quindi la complessità migliore ottenibile è $\mathcal{O}(n\log(n))$.

### Merge Sort
>[!note]
>```
>Merge(A,p,q,r)
>	len1 <- q - p + 1
>	len2 <- r - q
>	Alloca(L[1..len1+1])
>	Alloca(R[1..len2+1])
>	
>	for i <- 1 to len1
>		L[i] <- A[p + i - 1]
>	
>	for i <- 1 to len2
>		R[i] <- A[q + i]
>	
>	L[len1 + 1] <- ∞
>	R[len2 + 1] <- ∞
>	i <- 1
>	j <- 1
>	
>	for k <- p to r
>		if L[i] <= R[j]
>			A[k] <- L[i]
>			i <- i + 1
>		else
>			A[k] <- R[j]
>			j <- j + 1
>
>MergeSort(A,p,r)
>	if p < r - 1
>		q <- floor((p + r)/2)
>		MergeSort(A,p,q)
>		MergeSort(A,q+1,r)
>		Merge(A,p,q,r)
>	else
>		if A[p] > A[r]
>			tmp <- A[r]
>			A[r] <- A[p]
>			A[p] <- tmp
>```
>
>L'algoritmo `Merge` alloca due array ausiliari, grossi quanto le parti da fondere, più alcune variabili ausiliarie di numero fissato, quindi ha complessità spaziale $\Theta(n)$.
>Tralasciando le porzioni sequenziali, l'algoritmo `Merge` è composto da $3$ cicli, due per copiare le parti da fondere ($\Theta(n)$), e uno che copia in $A$ gli elementi in ordine ($\Theta(n)$). Quindi `Merge` è $\Theta(n)$. Il costo quindi è: $$T(n)=2T\left(\frac{n}{2}\right)+\Theta(n)$$
>>[!tip]- Visualizzazione
>>![[merge.webp]]

### Quick Sort
>[!note]
>Quicksort è un algoritmo di ordinamento senza spazio ausiliario, e applica un il principio divide-et-impera ad una slice `A[lo..hi]`. In questo caso scegliamo un elemento `A[p]` detto pivot come punto di suddivisianoe, e sposta gli elementi di `A[lo..hi]` in modo che tutti quelli di `A[lo..p-1]` siano minori o uguali al pivot, e quindi si ordina `A[lo..p-1]` e `A[p+1..hi]` con quicksort
>```
>QuickSort(A,lo,hi)
>	if lo < hi
>		p <- Partition(A,lo,hi)
>		Quicksort(A,lo,p-1)
>		Quicksort(A,p+1,hi)
>```
>
>Abbiamo diversi schemi di partizione:
>```
>PartitionLomuto(A,lo,hi)
>	pivot <- A[hi]
>	i <- lo - 1
>	
>	for j <- lo to hi - 1
>		if A[j] <= pivot
>			i <- i + 1
>			Scambia(A[i],A[j])
>	
>	Scambia(A[i + 1], A[hi])
>	return i + 1
>	
>PartitionHoare(A,lo,hi)
>	pivot <- A[lo]
>	i <- lo - 1
>	j <- hi + 1
>	
>	while true
>		repeat
>			j <- j -1
>		until A[j] <= pivot
>		
>		repeat
>			i <- i + 1
>		until A[i] >= pivot
>		
>		if i < j
>			Scambia(A[i], A[j])
>		else return j
>```
>
>In entrambi i casi il calcolo di `Partition` ha complessità temporale $\Theta(n)$ con $n$ lunghezza del vettore su cui deve operare la partizione. La complessità di Quick Sort risulta quindi: $$T(n)=T\left(\frac{n}{a}\right)+ T\left(n- \frac{n}{a}\right)+ \Theta(n)$$
>Dove $a$ dipende da "quanto bene" `Partition` ha suddiviso il vettore. Quindi ha come caso pessimo $\Theta(n^{2})$, caso ottimo $\Theta(n\log(n))$ e caso medio $\Theta(n\log(n))$. Quick Sort non è stabile.
>
>>[!tip]- Visualizzazione
>>![[quick.webp]]

### Counting Sort
>[!note]
>```
>CountingSortNonStabile(A)
>	Ist[0..k] <- 0
>	
>	for i<- 0 to A.length - 1
>		Ist[A[i]] <- Ist[A[i]] + 1
>	
>	IdxA <- 0
>	for i <- 0 to k
>		while Ist[i] > 0
>			A[idxA] <- i
>			idxA <- idxA + 1
>			Ist[i] <- Ist[i] - 1
>
>CountingSortStabile(A)
>	B[0..A.length - 1] <- 0
>	Ist[0..k] <- 0
>	
>	for i <- 0 to A.length - 1
>		Ist[A[i]] = Ist[A[i]] + 1
>	
>	sum <- 0
>	for i <- 0 to k
>		sum <- sum + Ist[i]
>		Ist[i] <- sum
>	
>	for i <- A.length - 1 to 0
>		idx <- Ist[A[i]]
>		B[idx - 1] <- A[i]
>		Ist[A[i]] <- Ist[A[i]] -1
>```
>
>Il Counting Sort è un algoritmo che non si basa sul confronto diretto di elementi di un vettore. Ne esiste una versione stabile e non stabile. Consideriamo $k$ valore massimo degli elementi. Si ha che la complessità temporale è dominata dall'ultimo ciclo: $\mathcal{O}(n+k)$
>
>>[!tip]- Visualizzazione
>>![[counting.webp]]

