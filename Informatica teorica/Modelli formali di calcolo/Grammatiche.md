>[!note]
>A differenza dei modelli di linguaggio/calcolo visti finora, che definiscono un linguaggio tramite l'elaborazione della stringa che gli appartiene, la grammatica o sintassi è un modello generativo. In generale, è un insieme di regole per generare frasi di un linguaggio.
>
>Formalmente, una grammatica è una quadrupla $G=\langle V_{t}, V_{n}, P, S\rangle$, composta rispettivamente da:
>- Un alfabeto o vocabolario terminale $V_{t}$
>- Un alfabeto o vocabolario non terminale $V_{n}$
>- Un alfabeto o vocabolario $V=V_{n}\cup V_{t}$
>- Un assioma o simbolo iniziale $S\in V_{n}$
>- Insieme delle produzioni sintattiche o regole di riscrittura $P\subseteq V_{n}^{+}\times V^{*}$
>
>

Le regola di una grammatica descrivono un "oggetto principale" come un insieme ordinato di "componenti". La descrizione è fornita fino ad arrivare al livello di dettaglio desiderato. Spesso si tende a chiamare lessico la descrizione grammaticale delle singole parole, sintassi quella della loro composizione.

Per semplicità di notazione, indicheremo gli elementi $p\in P\quad p=\langle \alpha, \beta\rangle$ come $p=\alpha\to \beta$.

### Regole di derivazione
>[!note]
>Definiamo la relazione di derivazione immediata $\underset{G}{\Rightarrow}$ per una grammatica $G=\langle V_{t}, V_{n}, P, S\rangle$ come $\alpha\underset{G}{\Rightarrow} \beta$ se e solo se $\alpha\in V^{+}, \beta\in V^{*}$ e $\alpha=\alpha_{1}\alpha_{2}\alpha_{3}\quad \beta=a_{1}\beta_{2} \alpha_{3}\quad \alpha_{2}\to \beta_{2}\in P$. Dove non ambiguo, è possibile omettere il pedice $G$ che indica la grammatica. Inoltre definiamo $\stackrel{*}{\Rightarrow}$ come la chiusura riflessiva e transitiva di $\Rightarrow$. Il linguaggio $L(G)$ generato dalla grammatica $G$ è l'insieme di tutte e sole le stringhe $x$ di soli caratteri di $V_{t}$ tali che $S\stackrel{*}{\Rightarrow} x$.

>[!example] Esempio linguaggio generatore di $L(G)=\set{a^{*}b^{*}c^{*}}$
>Definiamo la grammatica $G=\langle \set{a,b,c},\set{S,A,B,C},S,P\rangle$ con $P=\set{S\to A, A\to aA, A\to B, B\to bB, B\to C, C\to cC, C\to \varepsilon}$.
>Si ha che una possibile derivazione è: $$S\Rightarrow A\ \Rightarrow aA \Rightarrow aaA \Rightarrow aaB \Rightarrow aaC \Rightarrow aacC \Rightarrow aaccC \Rightarrow aacccC \Rightarrow aacccC \Rightarrow aaccc$$
>Un altra possibile derivazione è: $$S \Rightarrow A \Rightarrow B \Rightarrow bB \Rightarrow bC \Rightarrow b$$
>Quindi il linguaggio generato è $L(G)=\set{a^{*}b^{*}c^{*}}$.

>[!example] Esempio linguaggio ben parentetizzato
>Si ha $G=\langle \set{a,b}, \set{S}, S, \set{S\to aSbS, S\to \varepsilon}\rangle$. Si discerne che genera un linguaggio di coppie di $a$ e $b$ ben parentetizzate.

### Espressività delle grammatiche
>[!note]
>È possibile categorizzare le grammatiche in base alla loro espressività. Per farlo si usa la gerarchia di Chomsky:
>
>| Tipo | Nome                      | Limitazione                                                                                                 |
>| ---- | ------------------------- | ----------------------------------------------------------------------------------------------------------- |
>| 0    | Non limitate              | nessuna                                                                                                     |
>| 1    | Monotone (non-decreasing) | $$ \|\alpha\|\leq \|\beta\| $$                                                                                |
>| 1    | Dipendenti dal contesto   | $$\alpha= \gamma A s\quad \beta= \gamma \chi \delta\qquad \chi\neq \varepsilon\text{ o } S\to \varepsilon$$ |
>| 2    | Libere dal contesto       | $$\alpha=1$$                                                                                                |
>| 3    | Regolari                  | Di forma $A\to a,\space A\to aA$ oppure $A\to a,\space A\to Aa$ con $a\in V_{t}$ e $A\in V_{n}$             |

>[!tip] Conversione FSA - Grammatiche regolari
>Per passare da un FSA ad una grammatica poniamo $V_{n}=Q$, $V_{t}=I$ e $S=\langle q_{0}\rangle$. Si ha che per ogni $\delta(q, i)=q'$ aggiungiamo $\langle q\rangle\to i\langle q'\rangle$ all'insieme $P$, e se $q'\in F$ per una data $\delta(q,i)=q'$, aggiungiamo anche $\langle q\rangle \to i$ all'insieme $P$. È dimostrabile per induzione che $\delta^{*}(q_{0}, x)=q'$ se e solo se $\langle q_{0}\rangle\Longrightarrow x\langle q'\rangle$.
>
>Viceversa, per passare da una grammatica ad un FSA ND, poniamo $Q=V_{n}\cup\set{q_{f}}$, $I=V_{t}$ e $F=\set{q_{f}}$. Abbiamo che se $A\to bC\in P$ allora $\delta(A,b)=C$, e se $A\to b\in P$ allora $\delta(A,b)=q_{f}$.

>[!tip] Grammatiche libere dal contesto e AP-ND
>I linguaggi generati dalle grammatiche libere dal contesto coincidono con i linguaggi riconosciuti dagli AP non deterministici. Le dimensioni fisiche della funzione di rete dipendono dalle dimensioni fisiche dei fasori.

>[!tip] Grammatiche non limitate e MT
>Le grammatiche non limitate corrispondono alla MT. Emuliamo una MT $\mathcal{M}$ a nastro singolo con una grammatica $G$ non ristretta. Considerato che $G$ può "manipolare" solo elementi di $V_{n}$, faccio in modo che generi stringhe della forma $x \diamond X$, con $\diamond\in V_{n}, x\in V_{t}^{*}$ e $X$ che è costituita da coppia non terminali degli elementi di $X$.
>
>Si ha che le grammatiche di tipo $1$ corrispondono a un sottoinsieme delle MT di cui è certo che terminino sempre.


