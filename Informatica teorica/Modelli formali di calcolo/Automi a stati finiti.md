>[!note]
>Gli automi a stati finiti sono semplici modelli operativi. Funzionano a tempo discreto. Sono chiamati così perché lo stato del calcolo è definito da un insieme finito.
>Formalmente, definiamo $Q$ come l'insieme finito dei suoi stati, e $I$ come l'alfabeto dei simboli in ingresso, $\delta:Q\times I\to Q$ come funzione di transizione, che mappa lo stato corrente e un input in uno stato di destinazione, e $q_{0}\in Q$ come lo stato iniziale dell'automa.
>
>Inoltre definiamo $F\subseteq Q$ come l'insieme di stati finali.

>[!tip] Modelli operativi
>I modelli operativi di calcolo sono delle macchine astratte.

È possibile definire un FSA per riconoscere le parole di un linguaggio. Se l'automa leggendo una stringa, partendo da $q_{0}$ termina in uno stato finale, la stringa appartiene al linguaggio.
 
### Formalizzazione dell'accettazione
>[!note]
>Formalizziamo una sequenza di mosse definendo $\delta^{*}:Q\times I^{*}\to Q$, estensione di $\delta$ induttivamente:
>- Base: $\forall q\in Q,\space\delta^{*}(q,\varepsilon)=q$
>- Passo: $\delta^{*}(q,y.i)=\delta(\delta^{*}(q,y),i)\qquad i\in I,y\in I^{*}$

### FSA Riconoscitore
>[!note]
>Formalizziamo un FSA riconoscitore $(Q,I,\delta,q_{0},F)$ di un linguaggio $L$ su $I$: $$x\in L\iff \delta^{*}(q_{0},x)\in F$$
### FSA Traduttore
>[!note]
>Un FSA Traduttore da $L_{1}$ a $L_{2}$ associa un simbolo letto e uno scritto a ogni transizione:
>![[Pasted image 20250303165844.png]]
>
>Formalmente un FSA traduttore $(Q,I,\delta,q_{o},F,O,\eta)$ con $O$ alfabeto di uscita e $\eta:Q\times I\to O^{*}$. Definiamo analogamente $\eta^{*}:Q\times I\to O^{*}$: $$\begin{cases}
>\eta^{*}(q, \varepsilon)=\varepsilon \\
>\eta^{*}(q, y.i)=\eta^{*}(q,y).\eta (\delta^{*}(q,y),i)\qquad i\in I, y\in I^{*}
>\end{cases}$$
>Quindi l'intero calcolo di traduzione è formalizzato come: $$\tau(x)=\eta^{*}(q_{0},x)\iff \delta^{*}(q_{0},x)\in F$$

### Pumping lemma
>[!note]
>Il pumping lemma è la formalizzazione di un comportamento ciclico in un FSA.
>Se $\exists x\in L$ e $L$ è riconosciuto da un FSA con $|x|\geq |Q|$ allora $\exists q\in Q, w\in I^{+}$ tali che $x=ywz$ con $y,z\in I^{*}$ e $\delta^{*}(q,w)=q$, cioè esiste una sotto stringa di $x$ che viene riconosciuta dall'automa effettuando un'iterazione su un ciclo di stati.
>
>Consegue che $yw^{n}z\in L, \forall n\geq 0$, cioè è possibile effettuare zero o più interazioni del ciclo.

>[!tip] Conseguenze del pumping lemma
>Se $L=\emptyset$, $\exists x\in L\Longrightarrow \exists y\in L, |y|<|Q|$, cioè se una parola ha cicli di riconoscimento li elimino, e posso dare le $y$ all'FSA e verificare se appartengono a $L$.
>Se $|L|=\infty$, $\exists x\in L, |Q|\leq |x|< 2|Q|$, che implica che $x$ abbia un ciclo di riconoscimento.

### Linguaggi regolari
>[!note]
>La famiglia di linguaggi riconoscibili con un FSA è la famiglia dei linguaggi regolari $R$. $R$ è chiusa rispetto a $\cap,\cup,\lnot,\smallsetminus, \text{concatenazione}, *,+$.

### Intersezioni tra linguaggi
>[!note]
>Dati due automi $A_{1}:(Q_{1},I_{1},\delta_{1},q,F_{1})$ e $A_{2}:(Q_{2},I_{2},\delta_{2},s,F_{2})$, l'automa intersezione $A_{\cap}=\langle A_{1},A_{2}\rangle$ è dato da: $$\begin{align*}
>Q_{\cap}&= Q_{1}\times Q_{2}\\
>I_{\cap}&= I_{1}\cap I_{2}\\
>\delta_{\cap}(\langle q_{1},q_{2}\rangle,i)&= \langle \delta_{1}(q_{1},i),\delta_{2}(q_{2},i))\rangle\\
>F_{\cap}&= F_{1}\times F_{2}
>\end{align*}$$
>Vale: $$L(A_{\cap})=L(A_{1})\cap L(A_{2})$$

### Unione di linguaggi
>[!note]
>Dati due automi $A_{1}:(Q_{1},I_{1},\delta_{1},q,F_{1})$ e $A_{2}:(Q_{2},I_{2},\delta_{2},s,F_{2})$, l'automa unione $A_{\cup}=\langle A_{1},A_{2}\rangle$ è dato da: $$\begin{align*}
>Q_{\cup}&= (Q_{1}\times Q_{2})\cup Q_{1}\cup Q_{2}\\
>I_{\cup}&= I_{1}\cup I_{2}\\
>\delta_{\cup}(\langle q_{1},q_{2}\rangle,i)&= \begin{cases}
>\langle \delta_{1}(q_{1},i),\delta_{2}(q_{2},i)\rangle\text{ se esistono entrambi}\\
>\delta_{1}(q_1,i)\text{ oppure }\delta_{2}(q_{2},i)\text{ altrimenti}
>\end{cases}\\
>F_{\cup}&= (F_{1}\times F_{2})\cup F_{1}\cup F_{2}
>\end{align*}$$
>In alternativa è possibile applicare la legge di De Morgan: $$L_{1}\cup L_{2}=\lnot(\lnot L_{1}\cap \lnot L_{2})$$

