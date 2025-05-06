>[!note]
>Una pila (Stack) è una struttura dati con le seguenti operazioni:
>- `Push(S,e)`: aggiunge un elemento in cima alla pila
>- `Pop(S)`: restituisce l'elemento in cima alla pila cancellandolo
>- `Empty(S)`: restituisce `true` se la pila è vuota
>
>Questa struttura dati astratta può essere realizzata usando una lista semplicemente connessa o un vettore.

>[!tip] Implementazione con una lista
>Se lo stoccaggio dati è nella lista, le operazioni diventano:
>- `Push(S,e)`: inserisci in testa alla lista $\mathcal{O}(1)$
>- `Pop(S)`: restituisce il primo elemento della lista, cancellandolo dalla stessa $\mathcal{O}(1)$
>- `Empty(S)`: controlla se il successore della testa è NIL $\mathcal{O}(1)$

>[!tip] Implementazione con un vettore
>Se lo stoccaggio dati è nelle celle di un vettore, viene mantenuto l'indice della cima della pila (Top of Stack, `Tos`), le operazione diventano:
>- `Push(S,e)`: se c'è spazio, incrementa `ToS` e salva `e` in `A[ToS]`. Se c'è spazio allora $\mathcal{O}(1)$, altrimenti può rifiutare $\mathcal{O}(1)$ o riallocare $\mathcal{O}(n)$
>- `Pop(S)`: restituisce `A[ToS]` corrente, e decrementa `A[ToS]` $\mathcal{O}(1)$
>- `Empty(S)`: Restituisce `ToS = 0` $\mathcal{O}(1)$
>
>Non ha nessun vantaggio rispetto all'implementazione a pila, ma se si rialloca allora si ha uno svantaggio. Tuttavia non avere dati in memoria coesi penalizza le caches, quindi può valer la pena di usare un vettore se non ci sono troppe riallocazioni.

