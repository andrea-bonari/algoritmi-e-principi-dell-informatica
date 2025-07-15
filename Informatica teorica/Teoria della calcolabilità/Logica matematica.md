>[!note]
>La logica è un formalismo universale alternativo al linguaggio naturale. Ha come vantaggio di non essere ambigua, e ha la possibilità di dimostrare in modo automatico delle proprietà desiderate.

In questo corso useremo la logica per specificare dei linguaggi formali, usando la logica monadica del primo e secondo ordine, e per specificare il comportamento I/O di programmi.

### Logica monadica del primo ordine
>[!note]
>Consideriamo la logica del primo ordine con predicati su una sola variabile (MFO), questa consente di descrivere parole su un alfabeto $I$. Sia $a\in I$ una lettera predicativa per ogni simbolo di $I$, una formula $\varphi$ è:
>- $a(x)$: il predicato $a$ applicato ad una variabile
>- $x<y$
>- $\lnot\varphi$: negazione logica della formula
>- $\varphi\land\varphi$: congiunzione (and booleano) di due formule
>- $\forall x\space(\varphi)$: quantificatore universale
>
>Dove il dominio delle variabili è un sottoinsieme finito di $\mathbb{N}$ da pensare come posizioni, e $<$ corrisponde alla relazione di minore tra le posizioni.
>
>Dati $w\in I^{+}$ e $V_{1}$ insieme delle variabili, un assegnamento è una funzione $v_{1}:V_{1}\to\set{0,1,\cdots,|w|-1}$.

>[!tip]
>Definiamo alcune relazioni:
>$$\begin{align*}
>\varphi_{1}\lor\varphi_{2}&\equiv \lnot(\lnot\varphi_{1}\land\lnot\varphi_{2})\\
>\varphi_{1}\Rightarrow\varphi_{2}&\equiv \lnot\varphi_{1}\lor\varphi_{2}\\
>\exists x(\varphi)&\equiv \lnot\forall x(\lnot\varphi)\\
>x=y&\equiv \lnot(x<y)\land\lnot(x>y)\\
>x\leq y&\equiv \lnot(y<x)
>\end{align*}$$
>Definiamo inoltre:
>- Costante $0$: $x=0\equiv \forall y(\lnot(y<x))$
>- Funzione successore $S(x)$: $s(x)=y\equiv (x<y)\land\lnot\exists z(x<z\land z<y)$
>- Costanti $1,2,\cdots$: rispettivamente $S(0),S(S(O)),\cdots$

Si ha che $a(x)$ è vera se e solo se l'$x$-esimo elemento di una parola $w\in I^{*}$ è $a$.

Usiamo inoltre le seguenti abbreviazioni convenienti:
- $y=x+1$ indica $y=S(x)$, generalizzando, se $k\in\mathbb{N},\space k>1$ indichiamo $y=x+k$.
- $y=x-1$ indica $x=S(y)$, cioè $x=y+1$, così come $y=x-k$ indica $x=y+k$
- $\text{last}(x)$ indica $\lnot\exists y\space (y>x)$

Definiamo il linguaggio definito da una formula come: $$L(\varphi)=\set{w\in I^{+}\space|\space \exists v:\space w,v\models \varphi}$$con $\varphi$ formula chiusa.

I linguaggi esprimibili con MFO sono chiusi per unione, intersezione e complemento, tuttavia sono strettamente meno potenti degli FSA. Inoltre si ha che i linguaggi definiti da una formula MFO non sono chiusi rispetto alla $*$ di Kleene, e quindi un MFO è in grado di definire i linguaggi star-free, cioè linguaggi ottenuti per unione, intersezione, concatenazione e complemento di linguaggi finiti.

### Logica monadica del secondo ordine
>[!note]
>La logica monadica del secondo ordine (MSO) permette di quantificare predicati del primo ordine, e quindi ammettiamo formule come $\exists X\space(\varphi)$ con $X$ appartenente all'insieme dei predicati monadici. Per convenzione si usano le maiuscole per indicare variabili con domini l'insieme dei predicati monadici, e le minuscole per indicare variabili in $\mathbb{N}$.
>
>L'assegnamento di variabili del secondo ordine (insieme $V_{2}$) è una funzione $v_{2}: V_{2}\to\wp(\set{0,1,\cdots,|w|-1})$.

### Teorema di Büchi-Elgot-Trakhtenbrot
>[!note]
>Data una MSO $\varphi$, si può sempre costruire un FSA che accetta esattamente $L(\varphi)$. La classe dei linguaggi definibili tramite MSO coincide con REG.

Per convertire da FSA a MSO seguo il seguente approccio:
- Per ogni $q\in Q$ del FSA definiamo una variabile $X_{q}$, che rappresenta l'insieme di posizioni di una stringa accettata dove l'automa si trova in $q$. L'automa non è in due stati contemporaneamente, quindi per ogni coppia $X_{i}$ e $X_{j}$ abbiamo $\lnot\exists y\space (y\in X_{1}\land y\in X_{j})$
- L'FSA parte da $q_{0}$, cioè $\forall x\space(x=0\Rightarrow x\in X_{q_{0}})$ delle posizioni dei caratteri letti dall'FSA partendo da $q$.
- Ogni transizione $\delta(q_{i},a)=q_{j}$ diventa $\forall x,y\space (y=x+1\Rightarrow(x\in X_{i}\land a(x)\land y\in X_{j}))$
- L'accettazione tramite $\delta(q_{i},a)\in F$ diventa $\forall x\space(\text{last}(x)\Rightarrow\bigvee_{\delta(q_{i},a)\in F}(x\in X_{i}\land a(x)))$

### Logica come formalismo per definire le proprietà dei programmi
>[!note]
>La logica può essere usata come specifica per algoritmi, come algoritmo di ricerca e ordinamento. In generale sono presenti delle precondizioni (insieme di condizioni che devono essere vere prima dell'esecuzione di un programma $P$) affinché sia vero un insieme di fatti (postcondizioni) dopo l'esecuzione.