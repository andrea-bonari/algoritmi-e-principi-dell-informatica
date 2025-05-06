>[!note]
>Un vettore (Array) è una struttura dati compatta in memoria in cui si accede direttamente ad ogni elemento data la sua posizione.

Se il vettore di lunghezza $n$ non è ordinato si ha che:
- Ricerca, minimo, massimo e successore sono $\mathcal{O}(n)$
- Inserimento e cancellazione costano $\mathcal{O}(n)$

Se il vettore di lunghezza $n$ è ordinato si ha che:
- Minimo e massimo sono $\Theta(1)$
- Ricerca e successore sono $\Theta(n\log(n))$
- Inserimento e cancellazione sono $\mathcal{O}(n)$

In base all'implementazione, inserimenti in un vettore pieno possono essere:
- rifiutati, con costo $\mathcal{O}(1)$
- causano una riallocazione $\mathcal{O}(n)$