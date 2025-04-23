>[!note]
>Un linguaggio è uno strumento per esprimere modelli. Ogni linguaggio è definito su un alfabeto, che è un insieme finito di simboli.

>[!example] Esempi di linguaggio
>Lingue naturali: Italiano, Francese, Inglese, Giapponese
>Linguaggi sintetici: C, Java, XML, JSON
>Linguaggi grafici: cartelli stradali, simboli di lavaggio negli indumenti
>Linguaggi acustici: musica, fischi degli arbitri sportivi

>[!example] Esempi di alfabeto
>Alfabeto latino: $\set{a,b,c,\cdots,z}$
>Binario: $\set{0,1}$
>

Un linguaggio può essere usato per definire l'insieme di soluzioni di un problema, e per esprimere un problema stesso.

### Stringhe
>[!note]
>Definiamo una stringa come una sequenza ordinata e finita di elementi di un alfabeto $A$. Riguardante ad una stringa definiamo:
>- Lunghezza di una stringa, cioè il numero di elementi come: $|a|$
>- Stringa di lunghezza nulla $\varepsilon$, con $|\varepsilon|=0$
>- Insieme di tutte le stringhe (inclusivo di $\varepsilon$) su $A$: $A^{*}$
>- Operatore di concatenazione $.$ (omissibile)

Siccome l'operatore di concatenazione $.$ è binario, associativo e non commutativo, si può costruire il monoide libero dell'alfabeto $A$, $(A^{*},\space .\space)$ con elemento neutro $\varepsilon$.

### Linguaggio su un alfabeto $A$
>[!note]
>Un linguaggio $L$ su un alfabeto $A$ è un sottoinsieme di $A^{*}$, e quindi un insieme di parole di $A$.

>[!example] Esempio
>L'italiano è un linguaggio su $A=\set{a,b,c,\cdots,z,\_}$.
>I file PDF sono un linguaggio su $A=\set{0,1}$.
>I numeri in base $4$ sono un linguaggio su $A=\set{0,1,2,3}$.
>Il DNA è un linguaggio codificabile su $A=\set{C,G,A,T}$.

Notiamo che se $|A|<\infty$, non necessariamente $L<\infty$.

Siccome i linguaggi sono insiemi valgono le operazioni insiemistiche come $\cup,\cap,\smallsetminus,\lnot$. In particolare il complemento $\lnot L=\bar{L}$ è definito rispetto ad $A^{*}$, cioè: $\lnot L=A^{*}\smallsetminus L$.

### Concatenazioni tra linguaggi
>[!note]
>Dati un linguaggio $L_{1}$ su $A_{1}$, e un linguaggio $L_{2}$ su $A_{2}$, si ha che $L_{1}.L_{2}$ definito su $A_{1}\cup A_{2}$ è: $$L_{1}.L _{2}=\set{x.y\space |\space x\in L_{1}, y\in L_{2}}$$
>Si ha inoltre che dato un linguaggio $L$ e $n\in\mathbb{N}$, $L^{n}$ è definita come la concatenazione di se stesso $n$ volte: $$\begin{cases}
>L^{0}=\set{\varepsilon} \\
>L^{n}=L^{n-1}.L
>\end{cases}$$
>Definiamo inoltre l'operatore $+$ di un alfabeto, che indica stringhe fatte concatenando uno o più elementi dell'insieme. Per estensione ai linguaggi definiamo: $$L^{*}=\bigcup_{n=0}^{\infty}L^{n}\qquad L^{+}=\bigcup_{n=1}^{\infty}L^{n}$$

Nella pratica, l'intersezione tra linguaggi indica la compatibilità tra di loro, mentre la concatenazione di linguaggi consente di descrivere più agevolmente formati complessi.

>[!example] Esempio di concatenazione
>$$\begin{align*}
>&L_{1}=\set{0,1}^{*}\quad L_{2}=\set{a,b}^{*}\\
>&L_{1}.L_{2}=\set{\varepsilon, 0,1,0a,011b,0aba,\cdots}
>\end{align*}$$
>In questo esempio $a_{1}\notin L_{1}.L_{2}$ perché la concatenazione non è commutativa.

>[!example] Esempio di concatenazione
>Sia un alfabeto $A=\set{0,1}$, allora $A^{+}=\set{0,1,00,01,10,\cdots}$. Per quanto riguarda ai linguaggi:
>- Formato di pacchetto di dati su una rete $L_{\text{header}}.L_{\text{dati}}.L_{\text{trailer}}$
>- Archivio di dati tar o zip: $L_{\text{indice}}.L_{\text{file}}^{n}$

### Traduzioni
>[!note]
>Una traduzione è una mappa $\tau(\cdot):L_{1}\to L_{2}$, cioè mette in corrispondenza parole di due linguaggi.

### Famiglia di linguaggi
>[!note]
>Una famiglia di linguaggi è un insieme $\mathbb{L}$ i cui elementi sono linguaggi. È chiusa rispetto ad un'operazione $\star$ se $\forall L_{1},L_{2}\in L\quad L_{1}\star L_{2}\in L$.