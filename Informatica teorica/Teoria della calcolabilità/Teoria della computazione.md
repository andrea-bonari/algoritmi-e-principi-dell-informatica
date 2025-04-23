>[!note]
>Formalizziamo un calcolo come un problema per capire se $x\in L$, o di calcolare $y=\tau(x)$. Queste due formulazioni sono definite come:
>- Sapendo $y=\tau(x)$, definisco $\tau(x)=1\iff x\in L$ e $\tau(x)=0\iff x\notin L$.
>- Avendo $\mathcal{M}$ che risolve $s\in L$, definisco $L_{\tau}=\set{x‡y\space |\space y=\tau(x)}$, poi per tutte le possibili stringhe $y$ chiedo a $\mathcal{M}$ se $x‡y\in L_{\tau}$. Se $\tau(x)$ è definita, prima o poi la macchina risponderà positivamente.

>[!tip] Tesi di Church-Turing
>Nel 1933, Gödel e Herbrand individuano un insieme di funzioni sugli interi che appaiono definire ciò che può essere calcolato manualmente.
>Nel 1936, Alonso Church definisce un altro sistema basato su funzioni ricorsive, il $\lambda$-calcolo, anch'esso in grado di descrivere tutte le funzioni "calcolabili operativamente".
>Sempre nel 1936, Turing definisce quella che è la MT a nastro singolo tentando di fornire un formalismo per rappresentare tutto ciò che è "effettivamente calcolabile".
>Kleene, Turing e Church dimostrano che i tre formalismo citati sono equivalenti, cioè definiscono lo stesso insieme di problemi.
>
>Di conseguenza, tutti i problemi calcolabili operativamente sono descritti da una MT.

Turing definisce computable una funzione che può essere calcolata da una procedura eseguita da una macchina, senza necessità di intervento esterno, e che dà risultato in tempo finito.

### Enumerazione algoritmica
>[!note]
>Definiamo la enumerazione $\mathcal{E}$ di un insieme, cioè la corrispondenza biunivoca tra i suoi elementi e quelli di $\mathbb{N}$, è quindi una mappa: $\mathcal{E}: L\to \mathbb{N}$. Diciamo che $\mathcal{E}$ è effectively computable se esiste un algoritmo (o una MT) che la calcola.

>[!example] Esempio enumerazione algoritmica di $L=\set{a^{*}b^{*}}$
>Si ha che $\mathcal{E}$ etichetta le stringhe in ordine crescente di lunghezza, e se hanno la stessa lunghezza, etichetta in ordine lessicografico: $$\varepsilon\mapsto 0,\space a\mapsto 1,\space b\mapsto2,\space aa\mapsto 3,\space ab\mapsto 4,\space bb\mapsto 5,\space aaa\mapsto 6, \space\cdots$$

>[!example] Dimostrazione
>Consideriamo le MT a nastro singolo, con alfabeto $A=\set{0,1, \text{␢}}$ e $Q=\set{q_{0}, q_{1}}$. Osserviamo quali sono le possibili $\delta$ di queste MT. È possibile contare il numero di $\delta$ possibili e sapere quante MT a $2$ strati e $2$ lettere di alfabeto esistono.
>
>In generale ho $|C|^{|D|}$ funzioni $f: D\to C$. Facendo i conti con $\delta:Q\times A\to (Q\times A\times\set{\text{R},\text{S},\text{L}})\cup\set{\perp}$ abbiamo che, con $|Q|=2$ e $|A|=3$ ci sono $(2\cdot3\cdot3+1)^{2\cdot 3}=19^{6}$ possibili funzioni $\delta$ per MT a $2$ stati e $2$ lettere.
>
>Scegliendo un ordine arbitrario per l'insieme $\set{\text{MT}_{0},\cdots,\text{MT}_{19^{6}-1}}$, e allo stesso modo ordino le $(3\cdot3\cdot3+1)^{3\cdot3}=28^{9}$ MT. Numerando gli insiemi uno dopo l'altro ottengo un'enumerazione $\mathcal{E}:\text{MT}\to\mathbb{N}$.

Si ha che $\mathcal{E}$ è algoritmica, e quindi è possibile scrivere un programma che, data $\delta$ mi fornisce il suo numero. Si ha che $\mathcal{E}(\mathcal{M})$ è detto numero di Gödel di $\mathcal{M}$, e $\mathcal{E}(\cdot)$ è detta gödelizzazione.

Definiamo $f_{i}$ come la funzione calcolata dall'$i$-esima MT. Si ha che $f_{i}(x)=\perp$ se e solo se $\mathcal{M}_{i}$ non si ferma quando riceve in ingresso $x$.

### Macchina di Turing universale
>[!note]
>Si ha che esiste almeno una Macchina di Turing universale (MTU), cioè una MT che calcola $g(i, x)=f_{i}(x)$. La MTU non sembra essere dello stesso tipo delle altre $\mathcal{M}_{i}$, perché $f_{i}(\cdot)$ è funzione di una variabile, mentre $g_{i}(\cdot,\cdot)$ di due, tuttavia è possibile provare il contrario ricordando che $\mathbb{N}\times\mathbb{N}$ è enumerabile. È quindi possibile riformulare $g(i,x)=\hat{g}(n)=g(d^{-1}(n))$ tale per cui $g(i, x)=\hat{g}(d(i,x))$. La MTU lascia sul nastro $f_{i}(x)\iff M_{i}$ termina la computazione su $x$.

### Definizione e risoluzione dei problemi
>[!note]
>Si ha che $f: \mathbb{N}\to \set{0,1}\subseteq\mathbb{N}$, e quindi che: $$|f:\mathbb{N}\to\mathbb{N}|\geq|f:\mathbb{N}\to\set{0,1}$$
>Sappiamo anche che $|f:\mathbb{N}\to\set{0,1}|=2^{\aleph_{0}}=|\mathbb{R}|$. Quindi esistono almeno $2^{\aleph_{0}}$ funzioni, tuttavia esistono solo $\aleph_{0}$ MT, e quindi gran parte delle funzioni non è risolvibile algoritmicamente.
>
>Si ha inoltre che un problema definito su un linguaggio, a sua volta è definito sull'alfabeto $A$, che a sua volta è sottoinsieme di $A^{*}$, che è numerabile. Sappiamo quindi che: $$\text{problemi risolvibili}\subseteq\text{problemi definibili}$$
>Consideriamo ora una funzione: $$g(i, x)=\begin{cases}
>1\quad\text{se } f_{i}(x)\neq\perp \\
>0\quad\text{se } f_{i}(x)=\perp 
>\end{cases}$$
>Si ha che non esiste una MT che calcola $g$.

La non calcolabilità di $g$ ci dice che, nella pratica:
- Non esiste un compilatore che possa dirci che il nostro programma andrà in loop su un dato input
- Non possiamo costruire l'antivirus definitivo che sia in grado di capire a priori se un programma è malevolo
- Non possiamo "creare un programma per tentativi ciechi" controllando solo a posteriori che sia quello corretto

Nel contesto della calcolabilità: posso sapere che esiste una MT che risolve il problema, anche se non sono in grado di dire quale sia tra le possibili. Supponiamo di avere una funzione $f$ di cui non siamo in grado di trovare un algoritmo che la calcola. Un modo di dimostrare che è calcolabile senza eseguire un algoritmo è:
- mostrare che $f$ appartiene ad un insieme di funzioni $\mathfrak{F}$
- mostrare che per ogni elemento di $\mathfrak{F}$ esiste una MT che lo calcola

In un problema con risposta binaria per ogni input so a priori che è "si" o "no", e quindi che è risolvibile

>[!tip] Teorema di Cantor
>Si ha che: $$|S|<2^{|S|}=|\wp(S)|$$
>Dimostriamo che esiste una $f:S\to\wp(S)$ iniettiva, ma non suriettiva. Esiste una $f$ iniettiva, per esempio $f$ mappa $x\in S$ in $\set{x}\in\wp(S)$. Non esiste una $f$ suriettiva, consideriamo $T=\set{x\in S,\space x\notin f(x)}$. Supponiamo per assurdo, che esista una $f$ suriettiva, e quindi $T=f(x)$ dato che $T\in\wp(S)$ per costruzione: $$\begin{align*}
>x\in T\iff x\in f(x)&\text{ per ipotesi}\\
>x\in T\iff x\notin f(x)&\text{ per la defizione di }T\\
>\end{align*}$$
>Che è assurdo.

>[!example] Dimostrazione
>Supponiamo che esista, e sia calcolabile una: $$g(i, x)=\begin{cases}
>1\text{ se } f_{i}(x)\neq\perp \\
>0\text{ se } f_{i}(x)=\perp
>\end{cases}$$
>Allora è calcolabile anche un: $$h(x)=\begin{cases}
>1\text{ se }g(x,x)=0 \\
>\perp\text{ altrimenti}
>\end{cases}$$
>Se $h$ è calcolabile, esiste una $x_{h}$ tale che $f_{x_{h}}=h$. A questo punto calcoliamo $h(x_{h})$.
>Se $h(x_{h})=1$, dato che $f_{x_{h}}=h$ si ha che $f_{x_{h}}(x_{h})=1$. Tuttavia per la definizione di $h$ abbiamo che $g(x_{h},x_{h})=0$, ma quindi per definizione di $g$, $f_{x_{h}}(x_{h})=\perp$ che è assurdo.
>Se $h(x_{h})=\perp$, dato che $f_{x_{h}}=h$ si ha che $f_{x_{h}}(x_{h})=\perp$. Tuttavia per la definizione di $h$ abbiamo che $g(x_{h},x_{h})=1$, ma quindi per definizione di $g$, $f_{x_{h}(x_{h})}\neq\perp$ che è assurdo.
>
>Intuitivamente, se ho un programma $g(i,x)$ in grado di dire se un generico altro programma $f_{i}$ termina, posso usarlo per costruire un altro programma $h$ che fa sempre sbagliare $g(i,x)$ nel determinare se quest'ultimo termina.
>

### Decidibilità e semidecidibilità
>[!note]
>Considerando un problema con risposta binaria, quindi quelli che richiedono di calcolare una certa $f:\mathbb{N}\to\set{0,1}$, la interpretiamo come funzione caratteristica di $S$: $$1_{S}=\begin{cases}
>1\text{ se }x\in S \\
>0\text{ se }x\notin S
>\end{cases}$$
>Definiamo $S$ come ricorsivo o decidibile se e solo se la sua funzione caratteristica è calcolabile.
>Definiamo $S$ come ricorsivamente enumerabile (RE) o semidecidibile se e solo se:
>- $S$ è l'insieme vuoto
>- $S$ è l'immagine di una funzione totale e calcolabile $g_{S}$
>- $S=I_{g_{S}}=\set{y\space|\space y=g_{S}(x)\quad x\in\mathbb{N}}$ cioè $S=\set{g_{S}(0),g_{S}(1),\cdots}$ da cui il nome ricorsivamente enumerabile
>
>Il termine semidecidibile deriva dal fatto che:
>- Se $y\in S$, enumerando gli elementi di $S$ prima o poi trovo un valore di $x\in\mathbb{N}$ tale per cui $y=g_{S}(x)$
>- se $y\notin S$, non sono mai certo di poter rispondere "$y$ non appartiene a $S$" enumerando, potrei non aver ancora trovato $x\in\mathbb{N}$ tale per cui $y=g_{S}(x)$
>
>Si ha che $\text{Decidibilità}\Rightarrow\text{Semidecidibilità}$. Si ha inoltre che $S$ è ricorsivo se e solo se sono ricorsivamente enumerabili sia $S$ che il suo complemento $\bar{S}=\mathbb{N}\smallsetminus S$. Si ha quindi che gli insiemi decidibili sono chiusi rispetto al complemento.

>[!example] Dimostrazione
>Se $S$ è vuoto, allora è RE per definizione. Assumendo $S\neq\emptyset$, e costruendo una funzione totale e calcolabile di cui $S$ è immagine, $\exists k\in S\Longrightarrow 1_{S}(k)=1$, definiamo $g_{S}$ come: $$g_{S}:\begin{cases}
>g_{S}(x)=x\text{ se }1_{S}(x)=1 \\
>g_{S}(x)=k\text{ se }1_{S}(x)=0
>\end{cases}$$
>Si ha che $g_{S}$ è calcolabile, totale e $I_{g_{S}}=S$, e quindi $S$ è RE.

>[!tip]
>È equivalente dire che:
>- $S$ è ricorsivamente enumerabile
>- $S$ è il dominio $D_{h}$ di una funzione parziale calcolabile $S=\set{x\space |\space h(x)\neq\perp}$
>- $S$ è il codominio $I_{g}$ di una funzione parziale calcolabile $S=\set{x\space|\space x=g(y)\space y\in\mathbb{N}}$

Consideriamo $S=\set{x\space |\space f_{x}(x)\neq\perp}$, cioè il dominio $D_{h}$ della funzione $h(x)=f_{x}(x)$ che è calcolabile e parziale. Abbiamo quindi che $S$ è RE, e la sua indicatrice: $$1_{S}(x)=\begin{cases}
1\text{ se }f_{x}(x)\neq\perp \\
0\text{ se }f_{x}(x)=\perp
\end{cases}$$
Non è calcolabile, e dunque $S$ non è decidibile.

Si ha quindi che: $$\wp(\mathbb{N})\subset\text{RE}\subset\text{RIC}$$
### Definizione delle $S$ calcolabili e totali
>[!note]
>Dato un insieme $S$ per cui, se $i\in S$, allora $f_{i}$ è calcolabile e totale, e se $f$ è totale e calcolabile allora $\exists i\in S\space |\space f_{i}=f$, allora $S$ non è ricorsivamente enumerabile

>[!example] Dimostrazione
>Ipotizziamo che $\exists 1_{S}(i)$ calcolabile. Definiamo $h(x)=\set{f_{x}(x)+1\text{ se }1_{S}(x)=1,\space 0\text{ altrimenti}}$. Ho che $\forall x \space h(x)\neq f_{x}(x)$. $h(x)$ è calcolabile, ma diversa da tutte le calcolabili, che è assurdo.

Non è possibile, con un formalismo RE, definire l'insieme di tutte e sole le $f$ calcolabili totali. Non posso in nessun modo descrivere com'è fatto l'insieme di tutti e soli i programmi che terminano sempre.

### Teorema di Kleene
>[!note]
>Sia una funzione $t(\cdot)$ totale e calcolabile. È sempre possibile trovare una $f_{p}\quad p\in\mathbb{N}$ tale che $f_{p}=f_{t(p)}$. La funzione $f_{p}$ è detta punto fisso di $t(\cdot)$.

>[!example] Dimostrazione
>Dato un parametro $u\in\mathbb{N}$ definiamo una MT $\mathcal{M}_{u}$ che calcola sull'ingresso $x$:
>- Calcola $f_{u}(u)=z$
>- Se e quando il calcolo precedente termina, calcola $f_{z}(x)$
>
>La definizione è effettiva, quindi esiste una MT $\mathcal{M}_{u}$ che la calcola. Costruita $\mathcal{M}_{u}$, ne calcoliamo il suo numero di G̈ödel. Chiamiamo $g(u)$ la funzione che costruisce $\mathcal{M}_{u}$ e calcola il numero di Gödel. Abbiamo quindi: $$f_{g(u)}(x)=\begin{cases}
>f_{z}(x),\quad z=f_{u}(u)\text{ se }f_{u}(u)\neq\perp \\
>\perp\text{ altrimenti}\end{cases}$$
>Sappiamo che, data la $g(\cdot)$ totale e calcolabile di cui sopra, e data una $t(\cdot)$ totale e calcolabile, anche la composizione $t(g(\cdot))$ lo è. Chiamiamo $v$ il numero di Gödel di $t(g(\cdot))=f_{v}(\cdot)$. Costruiamo ora $\mathcal{M}_{v}$, cioè $\mathcal{M}_{u}$ come prima, per il caso $u=v$, ottenendo: $$f_{g(v)}(x)=\begin{cases}
>f_{f_{v}(v)}(x)\text{ se }f_{v}(v)\neq\perp \\
>\perp\text{ altrimenti}
>\end{cases}$$
>Ricordando che $t(g(\cdot))=f_{v}(\cdot)$ è totale e calcolabile, otteniamo che $f_{g(v)}(x)=f_{f_{v}(v)}(x)$. Sostituendo $f_{v}(\cdot)$ con $t(g(\cdot))$ al secondo membro abbiamo $f_{g(v)}(x)=f_{t(g(v))}(x)$. Quindi $g(v)$ è il punto fisso di $t(\cdot)$.

### Teorema di Rice
>[!note]
>Sia $F$ l'insieme di funzioni computabili e $S$ l'insieme degli indici delle MT che calcolano le funzioni di $F$, si ha che $S=\set{x\space |\space f_{x}\in F}$ è decidibile se e solo se $F=\emptyset$ o $F$ è l'insieme di tutte le funzioni computabili.

>[!example] Dimostrazione
>Supponiamo, per assurdo, che $S$ sia decidibile, e $F$ sia non vuoto e diverso dall'insieme di tutte le funzioni computabili. Consideriamo: $$1_{S}=\begin{cases}
>1\text{ se }f_{x}\in F \\
>0\text{ altrimenti}
>\end{cases}$$
>Essa è calcolabile per l'ipotesi appena fatta. Quindi possiamo calcolare:
>- Il più piccolo $i\in\mathbb{N}$ tale che $f_{i}\in F$, cioè $i\in S$
>- Il più piccolo $j\in \mathbb{N}$ tale che $f_{i}\notin F$, cioè $j\notin S$
>
>Per quanto detto, $h_{S}(x)=\set{i\text{ se }f_{x}\notin F,\space j\text{ altrimenti}}$ è a sua volta calcolabile e totale. Applicando il teorema di Kleene alla funzione totale e calcolabile $h_{S}(x)$ otteniamo che esiste un punto fisso $f_{\bar{x}}$ tale per cui $f_{\bar{x}}=f_{h_{S}(\bar{x})}$. Arriviamo alla contraddizione, assumendo:
>- $h_{S}(\bar{x})=i$: per definizione di $h_{S}(\cdot)$ abbiamo che $f_{\bar{x}}\notin F$, ma da quanto appena detto per il teorema di Kleene, $f_{\bar{x}}=f_{h_{S}(\overline{x})}=f_{i}$ da cui, per come definito $i$, $f_{i}\in F$, che è assurdo.
>- $h_{S}(\bar{x})=j$: per definizione di $h_{S}(\cdot)$ abbiamo che $f_{\bar{x}}\in F$, ma da quanto appena detto per il teorema di Kleene $f_{\bar{x}}=f_{h_{S}(\bar{x})}=f_{j}$ da cui, per come definito $j$, $f_{j}\notin F$, che è assurdo.

Dire se un generico problema è (semi)decidibile o meno è un problema indecidibile. Tuttavia il teorema di Rice ci consente di mostrare che un teorema non è decidibile.

### Tecnica di riduzione
 >[!note]
 >Se sono in grado di risolvere $y\in S'$ (cioè calcolare $1_{S'}(\cdot)$) e voglio risolvere $x\in S$, se ho una funzione $t$ calcolabile e totale tale per cui $x\in S\iff t(x)\in S'$, riduco il calcolare $x\in S$ a $t(x)\in S'$
 
