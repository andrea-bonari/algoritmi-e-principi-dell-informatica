>[!note]
>Normalmente, una algoritmo è una sequenza deterministica di passi. Tuttavia in alcuni calcoli, come per il calcolo parallelo, il determinismo è il calcolo più comodo.

Si ricorda che non deterministico è diverso da probabilistico.
### FSA non deterministici
>[!note]
>Si ha che la funzione di transizione $\delta$ diventa $\delta: Q\times I\to \wp(Q)$, e quindi ci restituirà un insieme. Estendendo $\delta$ alle stringhe: $$\delta^{*}(q, x)=\begin{cases}
>\delta(q, \varepsilon)=\set{q}\quad\text{con } x=\varepsilon \\
>\delta(q, y\space.\space i)=\bigcup_{r\in\delta^{*}(q, y)}\delta(r,i)\quad \text{ con }x=y.i\quad i\in I
>\end{cases}$$
>E quindi formalizziamo l'accettazione di una stringa come: $$x\in L\iff (\delta^{*}(q_{0}, x)\cap F)\neq\emptyset$$

È sempre possibile ricavare un FSA-D $\mathcal{A}_{\text{d}}: (Q_{d},\space I_{d},\space \delta_{d},\space q_{0d},\space F_{d})$ da un FSA-ND $\mathcal{A}_{\text{nd}}:(Q_{n},\space I_{n},\space \delta_{n},\space q_{0n}, \space F_{n})$. Esso sarà costituito da: $$\begin{cases}
Q_{d}=\wp(Q_{n}) \\
I_{d}=I_{n} \\
\delta_{d}(q_{d},i)=\bigcup_{q_{n}\in q_{d}}\delta_{n}(q_{n},i) \\
q_{d0}=\set{q_{n0}} \\
F_{d}=\set{s\in \wp(Q_{n})\space|\space s\cap F_{n}\neq \emptyset}
\end{cases}$$
Si ha che la determinizzazione di un FSA ha un costo, alla peggio: $$|Q_{d}|=|\wp(Q_{n})|=2^{|Q_{n}|}$$

>[!example] Esempio FSA-ND riconoscitore di $L=ab^{*}$
>![[Pasted image 20250416144929.png|center]]
>In questo esempio si ha che: $\delta(q_{0}, a)=\set{q_{1},q_{2}}$ e $\delta(q_{2},b)=\set{q_{1},q_{2}}$

>[!example] Esempio
>![[Pasted image 20250416145144.png|center]]
>In questo esempio abbiamo: $$\delta(q_{0},a)=\set{q_{1},q_{2}}\qquad \delta(q_{2},b)=\set{q_{21}}$$
>Di conseguenza: $$\delta^{*}(q_{0},aa)= \delta(q_{1},a)\cup\delta(q_{2}, a)=\set{q_{11},q_{12},q_{22}}$$

### AP non deterministici
>[!note]
>Si ha che la funzione di transizione $\delta_{AP-ND}$ diventa $\delta_{AP-ND}: Q\times (I\cup\set{\varepsilon})\times\Gamma\to \wp_{F}(Q\times \Gamma^{*})$, e quindi l'AP-ND accetta una stringa $x$ se esiste una sequenza $c_{0}\stackrel{*}{\vdash}\set{c_{1},\cdots,c_{n}}$ con $c_{0}=\langle q_{0},x, Z_{0}\rangle$ e $c_{1}=\langle q, \varepsilon, \gamma\rangle\quad q\in F$.
>
>Gli AP ND sono più potenti degli AP D, questo perché sono chiusi all'unione, però non sono chiusi rispetto all'intersezione.

Siccome la famiglia di linguaggi $L_{AP-ND}$ è chiusa rispetto a $\cup$ e non rispetto a $\cap$, non può esserlo rispetto al complemento. Con gli AP ND la computazione termina sempre, ma se ho: $$\langle q_{0},x , Z_{0}\rangle= c_{0}\stackrel{*}{\vdash}\set{\langle q_{1},\varepsilon, \gamma_{1}\rangle,\langle q_{2}, \varepsilon, \gamma_{2}\rangle}\quad q_{1}\in F, q_{2}\notin F$$
Allora la $x$ è accettata nella computazione precedente, ma continua ad esserlo anche se scambio $F$ con $Q\smallsetminus F$.

### MT non deterministiche
>[!note]
>Si ha che la funzione di transizione $\delta$ diventa $\delta: Q\times I \times \Gamma^{k}\to \wp(Q\times \Gamma^{k}\times\set{\text{L},\text{S},\text{R}})$. La configurazione, transizione, sequenza di transizioni e accettazione sono definite come negli altri casi. È possibile rappresentare una computazione con un grafico ad albero che rappresenta tutte le computazioni accettanti e non accettanti.

Si ha che $x$ è accettata da una MT ND solo se esiste un calcolo che termina in uno stato di accettazione. È possibile emulare una MT ND con una MT D, per farlo si percorre l'albero delle computazioni ND per stabilire se esiste un percorso che termina in uno stato di accettazione. Nel caso di un albero normale, esistono algoritmi consolidati per effettuare questa visita.

Nel caso di un albero in cui le computazioni non terminano si costruisce una MT D che scandisce le configurazioni della ND a partire dalle più vicine a $c_{0}$.