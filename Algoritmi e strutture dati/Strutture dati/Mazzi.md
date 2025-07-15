>[!note]
>Un mazzo (coda a due fini, Dequeue) è una struttura dati che si comporta come un mazzo di carte, di cui ogni una contiene un elemento. È possibile aggiungere sia in testa che in coda alla struttura:
>- `PushFront(Q,e)`: inserisce l'elemento `e` in testa al mazzo
>- `PushBack(Q,e`): inserisce l'elemento `e` in coda al mazzo
>- `PopFront(Q)`: restituisce l'elemento in testa, cancellandolo
>- `PopBack(Q)`: restituisce l'elemento in coda, cancellandolo
>- `Empty(Q)`: restituisce `true` se il mazzo è vuoto

>[!tip] Implementazione con una lista doppiamente concatenata
>Si ha che `PushBack` e `PopFront` si comportano come `Enqueue` e `Dequeue` di una coda realizzata con una lista, con l'aggiunta di:
>- `PopBack(Q)`: restituisce `tail.prev` se diverso da `head`, rimuovendolo dalla lista $\mathcal{O}(1)$
>- `PushFront(Q,e)`: aggiunge l'elemento `e` in testa, aggiornando `head` e il suo successore $\mathcal{O}(1)$
>- `Empty(Q)`: restituisce `head.next = tail` $\mathcal{O}(1)$

>[!tip] Implementazione con un vettore
>Lo stoccaggio dei dati è effettuato in modo analogo alla coda semplice.
>Si ha che `PushBack` e `PopFront` si comportano come `Enqueue` e `Dequeue` di una coda realizzata con un vettore, con l'aggiunta di:
>- `PopBack(Q)`: se $n>0$, restituisce `A[tail]` corrente, decrementa `n`, decrementa `tail` $\mathcal{O}(1)$
>- `PushFront(Q,e)`: $n<l$, decrementa `head`, inserisce l'elemento `e` in `A[head]` e incrementa $n$ $\mathcal{O}(1)$
>- `Empty(Q)`: restituisce `n = 0` $\mathcal{O}(1)$

