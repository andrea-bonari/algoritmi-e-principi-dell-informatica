>[!note]
>Una coda (Queue) è una struttura dati con le seguenti operazioni:
>- `Enqueue(Q,e)`: aggiunge `e` alla fine della coda
>- `Dequeue(Q)`: restituisce l'elemento all'inizio della coda, cancellandolo dalla stessa
>- `Empty(Q)`: restituisce `true` se la coda è vuota
>
>Come nel caso della pila, è possibile realizzare una coda sia con una lista che con un vettore.

>[!tip] Implementazione con una lista
>Se lo stoccaggio dei dati è effettuato negli elementi di una lista, teniamo traccia dell'ultimo elemento della lista (oltre al primo) con un puntatore `tail`. Le operazioni diventano:
>- `Enqueue(Q,e)`: inserisci l'elemento `e` in coda alla lista, aggiornando `tail` $\mathcal{O}(1)$
>- `Dequeue(Q)`: restituisci l'elemento in testa se diverso da `NIL`, cancellandolo e aggiornando `head` $\mathcal{O}(1)$
>- `Empty(Q)`: Restituisci `head = tail` $\mathcal{O}(1)$

>[!tip] Implementazione con un vettore
>Se lo stoccaggio dei dati è effettuato nelle celle di un vettore $A$ lungo $l$, teniamo traccia della posizione dove va inserito un nuovo elemento e di quella dell'elemento più vecchio con due indici `tail` e `head` e del numero di elementi contenuti `n`. Gli indici vengono incrementati di $\mod l$:
>- `Enqueue(Q,e)`: se $n<l$, inserisci l'elemento in `A[tail]`, incrementa $n$ e `tail` $\mathcal{O}(1)$
>- `Dequeue(Q)`: se $n>0$, restituisci `A[head]` corrente, decrementa `n`, incrementa `head` $\mathcal{O}(1)$
>- `Empty(Q)`: restituisci `n = 0` $\mathcal{O}(1)$
>
>Per ampliare lo stoccaggio è necessaria un allocazione fresca e copia degli elementi estraendoli con `Dequeue(Q)` $\Theta(n)$
