>[!note]
>Gli automi a stati finiti sono dei semplici modelli operativi di calcolo. Modellano il calcolo come una serie di passi discreti da una condizione (stato) alla successiva. Gli FSA hanno memoria del calcolo formata da un insieme finito di stati.
>Formalmente, è costituito da:
>- L'insieme finito dei suoi stati $Q$
>- L'alfabeto dei simboli in ingresso $I$
>- Una funzione di transizione, che mappa una coppia in uno stato di destinazione $\delta:Q\times I\to Q$
>- Stato iniziale dell'automa $q_{0}\in Q$
>- L'insieme di stati finali $F\subseteq Q$

È possibile usare un FSA per riconoscere le parole di un linguaggio. Se l'automa, leggendo una stringa, partendo da $q_{0}$ termina in uno stato finale, la stringa appartiene al linguaggio.
 
### FSA Riconoscitore
>[!note]
>Possiamo formalizzare l'accettazione di un linguaggio $L$ su $I$, da parte di un FSA $(Q,I,\delta,q_{0},F)$ come: $$x\in L\iff \delta^{*}(q_{0},x)\in F$$
>Dove $\delta^{*}:Q\times I\to Q$, è una sequenza di mosse, estensione di $\delta$ induttivamente definita come: $$\begin{cases}
>\forall q\in Q\quad \delta^{*}(q,\varepsilon)=q \\
>\delta^{*}(q,y.i)=\delta(\delta^{*}(q,y),i)\qquad i\in I, y\in I^{*}
>\end{cases}$$

>[!example] Esempio
>Di seguito un FSA riconoscitore per un linguaggio $L=\set{\text{stringhe che cominciano con 01}}$
>![[Pasted image 20250414164539.png|center]]

>[!example] Esempio
>Di seguito un FSA riconoscitore del linguaggio degli identificatori del linguaggio c. Si ha che $L_{\text{id}}$ è definito su $I=\set{a,b,\cdots,z,A,B,\cdots,Z,0,1,\cdots,9,\_}$:
>![[Pasted image 20250414165157.png|center]]
### FSA Traduttore
>[!note]
>Un FSA traduttore da $L_{1}$ a $L_{2}$ associa un simbolo letto e uno scritto a ogni transizione.
>![[Pasted image 20250414170231.png|center]]
>Formalmente un FSA traduttore è una $7$-upla $\mathcal{A}$ $(Q,I, \delta, q_{0},F,O,\eta)$ , dove:
>- $(Q, I, \delta, q_{0}, F)$ sono come nell'FSA riconoscitore
>- $O$ è l'alfabeto di uscita
>- $\eta:Q\times I\to O^{*}$ è la funzione di traduzione.
>
>Formalizziamo, analogamente a $\delta^{*}$, $\eta^{*}:Q\times I^{*}\to O^{*}$ come successione di traduzioni di elementi, e quindi come traduzione di stringhe: $$\begin{cases}
>\eta^{*}(q,\varepsilon)=\varepsilon \\
>\eta^{*}(q,y.i)=\eta^{*}(q,y)\space.\space \eta(\delta^{*}(q,y),i)\qquad i\in I, >y\in I^{*}
>\end{cases}$$
>Di conseguenza l'intero calcolo della traduzione è formalizzato come: $$\tau(x)=\eta^{*}(q_{0},x)\iff \delta^{*}(q_{0},x)\in F$$

>[!example] Esempio
>Di seguito un FSA traduttore che traduce da $L_{1}$ a $L_{2}$, entrambi definiti su $\set{0,1}^{*}$, con un numero di $O$ pari, aventi funzione di traduzione $\tau$ che dimezza gli $0$ e raddoppia gli $1$.
>![[Pasted image 20250414170712.png|center]]
### Pumping lemma
>[!note]
>Il pumping lemma è la formalizzazione di un comportamento ciclico in un FSA, cioè l'esistenza di un ciclo percorribile $0,1,2,\cdots,n$ volte.
>Il pumping lemma afferma che se $\exists x\in L$, dove $L$ è un linguaggio riconosciuto da un FSA, con $|x|\geq |Q|$ (dove $Q$ è l'insieme degli stati), allora esistono $q\in Q$ e $w\in I^{+}$ tali che $x=y.w.z$ con $y,z\in I^{*}$ e $\delta^{*}(q,w)=q$, cioè esiste una sottostringa di $x$ che viene riconosciuta dall'automa effettuando un'iterazione su un ciclo di stati.
>
>Dal pumping lemma consegue che $y.w^{n}.z\in L\quad \forall n\geq0$, che segue dal poter effettuare zero o più iterazioni del ciclo.
>
>$$\exists x\in  L_\text{FSA}\space |x|\geq |Q|\Longrightarrow \exists u,v,w\in I \quad|\quad x= u.w.z\quad |uv|\leq n,\space v\neq\varepsilon\quad\forall k\in\mathbb{N}\quad u.v^{k}.w\in L_\text{FSA}$$


Si può dire, con la condizione $L=\emptyset$, se $\exists x \in L$ allora $\exists y\in L\quad |y|<|Q|$, cioè che se una parola ha "cicli di riconoscimento" è possibile eliminarli, ed è possibile dare in pasto le $y$ all FSA e verificare se almeno una appartiene a $L$. 

Inoltre si può dire, se $|L|=\infty$, allora $\exists x\in L\quad |Q|\leq |x|<2|Q|$, cioè $x$ ha un ciclo di riconoscimento.

>[!tip] Limitazioni degli FSA
>Un FSA non può riconoscere un linguaggio $L=\set{a^{n}\space .\space b^{n}\quad n\geq0}$.
>Per dimostrarlo, sia $x\in L$ con $x=a^{m}\space.\space b^{m}\quad \frac{m}{2}>|Q|$. Applicando il pumping lemma si ha che $x=y\space .\space w\space .\space z$, con una $w$ tra le seguenti forme:
>- $w=a^{k}$, pompando $w$ ottengo $\forall r\in\mathbb{N}\quad a^{m-k}b^{r\cdot k}b^{m}\in L$ che è assurdo.
>- $w=b^{k}$, pompando $w$ ottengo $\forall r\in\mathbb{N}\quad a^{m}b^{r\cdot k}b^{m-k}\in L$ che è assurdo.
>- $w=a^{k}b^{h}$, pompando $w$ ottengo $\forall r\in\mathbb{N}\quad a^{m-k}(a^{k}b^{h})^{r}b^{m-h}\in L$ che è assurdo.

### Linguaggi regolari
>[!note]
>La famiglia di linguaggi riconoscibili con un FSA è detta famiglia dei linguaggi regolari $R$ o REG. Si ha che $R$ è chiusa rispetto a $\cup,\cap,\lnot,\smallsetminus,\space.\space,*,+$. 

>[!tip] Famiglie di linguaggi
>Una famiglia di linguaggi è un insieme i cui elementi sono linguaggi $L=\set{L_{i}}$. $L$ è chiusa rispetto ad un operazione binaria $\star$ se $\forall L_{1},L_{2}\in L$ vale $L_{1}\star L_{2}\in L$.

### Intersezioni tra linguaggi regolari
>[!note]
>Dati due FSA riconoscitori:
>![[Pasted image 20250415150142.png|center]]
>È possibile ottenere il riconoscitore del linguaggio intersezione facendoli funzionare insieme, con la condizione che di effettuare una transizione solo se c'è in entrambi:
>![[Pasted image 20250415150333.png|center]]
>Formalmente, dati due FSA $\mathcal{A}_{1}: (Q_{1},I_{1},\delta_{1},q,F_{1})$ e $\mathcal{A}_{2}: (Q_{2},I_{2},\delta_{2},s, F_{2})$, si ha che l'automa intersezione $\mathcal{A}_{\cap}=\langle\mathcal{A}_{1},\mathcal{A}_{2}\rangle$ è dato da:
>- Insieme degli stati $Q_{\cap}=Q_{1}\times Q_{2}$
>- Alfabeto $I_{\cup}=I_{1}\cup I_{2}$
>- Funzione di transizione $\delta_{\cup}(\langle q_{1},q_{2}\rangle, i)=\langle\delta_{1}(q_{1},i),\space\delta_{2}(q_{2},i)\rangle$
>- Insieme degli stati finali $F_{\cap}=F_{1}\times F_{2}$
>
>Inoltre si ha che: $$L(\mathcal{A}_{\cap})=L(\mathcal{A}_{1})\cap L(\mathcal{A}_{2})$$

>[!example] Esempio
>Dati due FSA:
>![[Pasted image 20250415152122.png|center]]
>Si ha nel FSA intersezione che lo stato in rosso non è raggiungibile dallo stato iniziale e quindi può essere eliminato, e che con la costruzione a punto fisso a partire da $\langle s_{0},t_{0}\rangle$ non viene neppure aggiunto:
>![[Pasted image 20250415152258.png|center]]

### Unione di linguaggi regolari
>[!note]
>Formalmente, dati due automi $\mathcal{A}_{1}:(Q_{1},I_{1},\delta_{1},q,F_{1})$ e $\mathcal{A}_{2}:(Q_{2},I_{2},\delta_{2},s,F_{2})$, l'automa unione $\mathcal{A}_{\cup}=\langle \mathcal{A}_{1},\mathcal{A}_{2}\rangle$ è dato da:
>- Insieme degli stati $Q_{\cup}=(Q_{1}\times Q_{2})\cup Q_{1}\cup Q_{2}$
>- Alfabeto $I_{\cup}=I_{1}\cup I_{2}$
>- Funzione di transizione $\delta_{\cup}(\langle q_{1},q_{2}\rangle, i)=\begin{cases}\langle\delta_{1}(q_{1},i),\space\delta_{2}(q_{2},i)\rangle\text{se esistono } \delta_{1}(q_{1},i)\text{ e } \delta_{2}(q_{2},i)\\\delta_{1}(q_{1},i)\text{ oppure } \delta_{2}(q_{2},i)\text{ altrimenti}\end{cases}$
>- Insieme degli stati finali $F_{\cup}=(F_{1}\times F_{2})\cup F_{1}\cup F_{2}$
>
>In alternativa è possibile applicare la legge di De Morgan: $$L_{1}\cup L_{2}=\lnot(\lnot L_{1}\cap \lnot L_{2})$$

### Complemento di linguaggi regolari
>[!note]
>Si ha che in ogni FSA esiste uno stato non accettante implicito, detto stato di errore. Aggiunto quello è possibile scambiare gli stati finali $F$ e gli stati non finali $Q\smallsetminus F$.

