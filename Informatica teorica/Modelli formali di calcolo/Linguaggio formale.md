>[!note]
>Un linguaggio è uno strumento per esprimere modelli. Ogni linguaggio è definito su un alfabeto, che è un insieme finito di simboli.

### Stringhe su un alfabeto
>[!note]
>Una stringa è una sequenza ordinata e finita di elementi dell'alfabeto.
>Definiamo la lunghezza di una stringa come il numero di elementi. (Si usa il simbolo della norma $|\space|$). Definiamo anche una stringa nulla $\varepsilon$ di lunghezza nulla ($|\varepsilon|=0$).
>
>Infine definiamo $A^{*}$ come l'insieme di tutte le stringhe (inclusa $\varepsilon$) su $A$.

L'operatore di concatenazione è il simbolo $.$. L'operazione di concatenazione è binaria, associativa e non commutativa, di conseguenza, dato un alfabeto $A$, allora $(A^{*},.)$ è un monoide libero con elemento neutro $\varepsilon$.

### Linguaggio su un alfabeto $A$
>[!note]
>Un linguaggio $L$ su un alfabeto $A$ è un sottoinsieme di $A^{*}$. Notiamo che se $|A|<\infty$, non necessariamente $|L|<\infty$. A seconda dell'alfabeto scelto, un linguaggio può modellare moltissime cose.

Siccome i linguaggi sono insiemi valgono le operazioni insiemistiche come $\cup,\cap,\smallsetminus$. Inoltre il complemento $\lnot L=\overline{L}$ è definito rispetto ad $A^{*}$, quindi $\lnot=A^{*}\smallsetminus L$.

>[!tip] Operazione concatenazione tra linguaggi
>Dati $L_{1}$ su $A_{1}$ e $L_{2}$ su $A_{2}$, $L_{1}.L_{2}$ definito su $A_{1}\cup A_{2}$ è: $$L_{1}.L_{2}=\set{x.y\space|\space x\in L_{1},y\in L_{2}}$$
>Dato $L^{n}$ con $n\in\mathbb{N}$, esso è la concatenazione di $L$ con se stesso $n$ volte. In modo compatto: $$\begin{cases}
L^{0}=\set{\varepsilon} \\
L^{n}=L^{n-1}.L
\end{cases}$$

>[!tip] Operatore $+$
>L'operatore $+$ indica stringhe fatte concatenando uno o più elementi dell'insieme. Per estensione: $$L^{*}=\bigcup_{n=0}^{\infty} L^{n}\qquad L^{+}=\bigcup_{n=1}^{\infty}L^{n}$$

L'intersezione tra linguaggi ci indica la compatibilità tra linguaggi, mentre la concatenazione di linguaggi consente di descrivere più agevolmente formati complessi.

Un linguaggio può essere usato per definire l'insieme di soluzioni di un problema, e per esprimere un problema stesso.

### Traduzioni
>[!note]
>Una traduzione è una mappa $\tau(\cdot):L_{1}\to L_{2}$, cioè mette in corrispondenza parole di due linguaggi.

### Famiglia di linguaggi
>[!note]
>Una famiglia di linguaggi è un insieme $\mathbb{L}$ i cui elementi sono linguaggi. È chiusa rispetto ad un'operazione $\star$ se $\forall L_{1},L_{2}\in L\quad L_{1}\star L_{2}\in L$.