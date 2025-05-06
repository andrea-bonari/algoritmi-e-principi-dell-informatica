>[!note]
>Una lista semplicemente connessa (Linked List) stocca gli elementi sparsi in memoria. Quindi ogni elemento ha un riferimento al successivo.

Se la lista di lunghezza $n$ non è ordinata:
- Ricerca, minimo, massimo, successore sono $\mathcal{O}(n)$
- Inserimento è $\mathcal{O}(1)$
- Cancellazione è $\mathcal{O}(n)$ se l'elemento va trovato, $\mathcal{O}(1)$ se si ha un riferimento alla posizione di inserimento

Se la lista di lunghezza $n$ è ordinata:
- Uno dei due tra minimo e massimo è $\Theta(1)$, l'altro $\Theta(n)$. Se si ha un puntatore accessorio ad entrambi gli elementi sono entrambi $\Theta(1)$
- Ricerca e successore sono $\mathcal{O}(n)$
- Inserimento e cancellazione sono $\mathcal{O}(n)$

### Liste doppiamente concatenate
>[!note]
>Una lista doppiamente concatenata (Double Linked List), è simile alle liste semplicemente connesse, con l'aggiunta che ogni elemento ha un riferimento al precedente. Si comporta come una lista semplice, tranne per la cancellazione: cancellare un elemento fornito alla `Delete(L,e)` per riferimento è $\mathcal{O}(1)$: 
>```
>e.prev.next <- e.next
>e.next.prev <- e.prev
>```

