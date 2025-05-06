>[!note]
>Le strutture dati nascono dall'esigenza di rappresentare collezioni di elementi in modo più organizzato. Le strutture dati possono usare delle chiavi (cioè etichette) per identificare un oggetto.

Le operazioni tipiche sulle strutture dati sono:
- `Search(S,k)`: restituisce il riferimento ad `e` con `e.key = k` in `S`, `NIL` se `k` non è contenuto in `S`.
- `Minimum(S)`: se le chiavi sono ordinate, restituisce `e` con la chiave minima
- `Maximum(S)`: se le chiavi sono ordinate, restituisce `e` con la chiave massima
- `Successor(S,k)`: restituisce `e` tale che `e.key` è la più piccola tra le chiavi `> k`
- `Predecessor(S,k)`: restituisce `e` tale che `e.key` è la più grande tra le chiavi `< k`
- `Insert(S,e)`: Inserisce un oggetto `e` nella struttura
- `Delete(S,e)`: Cancella un oggetto `e` dalla struttura