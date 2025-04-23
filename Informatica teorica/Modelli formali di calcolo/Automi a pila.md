>[!note]
>A differenza di un FSA, dove la memoria dello stato del calcolo è finita, un automa a pila (AP o PDA, Push-Down Automaton) dispone di una memoria a impilamento con funzionamento Last In First Out (LIFO), cioè:
>- La pila può crescere all'infinito
>- Si può accedere alla sola cella in cima, e leggere la cima della pila lo cancella
>
>![[Pasted image 20250415153726.png|center]]

Un automa a pila compie una mossa in funzione di:
- Simbolo letto dalla cima della pila
- Stato corrente nel FSA che costituisce l'organo di controllo
- Opzionalmente, simbolo letto dal nastro di ingresso

Un automa a pila passa alla configurazione successiva:
- Cambiando stato nell'organo di controllo
- Sostituendo al simbolo in cima alla pila una stringa $\alpha$ di simboli (anche nulla)
- Spostando (opzionalmente la testina di lettura)
- Se l'automa è traduttore, scrivendo una stringa (anche nulla)

Per convenzione si etichettano gli archi con formato: $$\langle\text{lettera input},\space\text{cima della pila letta/scritta in fondo alla pila},\space\text{lettera in output}\rangle$$Inoltre consideriamo la pila inizializzata con $Z_{0}$ per marcare il fondo.

### Automa riconoscitore
>[!note]
>In un automa riconoscitore a pila, la stringa $x$ in ingresso è riconosciuta (accettata) se l'automa scandisce completamente $x$, e una volta scandita tutta lo stato dell'organo di controllo è accettazione.
>Formalmente, un automa riconoscitore a pila $(Q,I,\Gamma,\delta,q_{0},Z_{0},F)$ è composto da:
>- $Q,I,q_{0},F$ come negli FSA
>- $\Gamma$ alfabeto di pila
>- $Z_{0}\in \Gamma$ simbolo iniziale di pila
>- $\delta$ funzione di transizione con $\delta:Q\times(I\cup\set{\varepsilon})\times\Gamma\to Q\times \Gamma^{*}$

>[!example] PDA riconoscitore di $\set{a^{n}b^{n}\space|\space n>0}$
>![[Pasted image 20250415155824.png|center]]

>[!example] Esempio parentesi tonde ben formate
>![[Pasted image 20250415160044.png|center]]

### Automa traduttore
>[!note]
>In un automa traduttore, se la stringa è accettata, il nastro di scrittura contiene la sua traduzione al termine del calcolo $\tau(x)$. Se la $x$ non è accettata la traduzione è indefinita: $\tau(x)=\perp$.
>Formalmente, un automa traduttore a pila $(Q,I,\Gamma,\delta,q_{0}, Z_{0}, F, O, \eta)$ è composto da:
>- $Q, I, \Gamma, \delta, q_{0}, Z_{0}, F$ come nei AP riconoscitori
>- $O$ come negli FSA traduttori
>- $\eta$ funzione di traduzione con $\eta: Q\times(I\cup\set{\varepsilon})\times \Gamma\to O^{*}$

### Stato di un AP
>[!note]
>Definiamo lo stato di un AP come $c=\langle q,x, \gamma, z\rangle$, con:
>- Stato dell'organo di controllo $q\in Q$
>- Stringa ancora da leggere $x\in I^{*}$
>- Stringa dei caratteri in pila $\gamma\in \Gamma^{*}$ (per convenzione cresce da sinistra a destra)
>- Se l'AP è traduttore, la stringa scritta in output $z\in O^{*}$

### Transizione tra configurazioni
>[!note]
>Definiamo una transizione tra due stati $c$ e $c'$ con l'operatore $\vdash$: $$c\vdash c': \langle q,\space x,\space \gamma,\space  z\rangle\vdash\langle q',\space x',\space \gamma',\space z'\rangle$$
>Per comodità, sia $\gamma=\beta\space.\space A$, cioè una sequenza di simboli con $A$ in cima.
>Se l'input è consumato, allora lo suddividiamo in $x=i\space.y$. La funzione di trasmissione $\delta(q,i,A)$ restituisce $\langle q', \alpha\rangle$, e quindi l'output associato è $\eta(q,i,A)=w$. Di conseguenza, $x'=y$, $\gamma'=\beta\alpha$ e $z'=z\space.\space w$.
>Se l'input non è consumato, allora la funzione di transizione $\delta(q, \varepsilon, A)$ restituisce $\langle q', \alpha\rangle$, e l'output associato è $\eta(q, \varepsilon, A)=w$. Di conseguenza $x'=x$, $\gamma'=\beta\alpha$ e $z'=z\space.\space w$.
>
>È necessario che: $$\forall q, A\quad \delta(q, \varepsilon, A)\neq \perp\space\Longrightarrow\space \forall i\quad \delta(q,i, A)=\perp$$
>In caso contrario l'automa a pila è non deterministico.
>
>Definiamo infinite $\stackrel{*}{\vdash}$ come chiusura riflessiva e transitiva $\vdash$.
>
>

In questo modo formalizziamo l'accettazione: $$x\in L\iff c_{0}=\langle q_{0},x, Z_{0}\rangle\stackrel{*}{\vdash}c_{f}=\langle q, \varepsilon, \gamma\rangle\quad q\in F$$
E la traduzione: $$x\in L\land[z=\tau(x)]\iff c_{0}=\langle q_{0},x, Z_{0}, \varepsilon\rangle\stackrel{*}{\vdash}c_{f}=\langle q, \varepsilon, \gamma, z\rangle\quad q\in F$$
### Famiglia dei linguaggi riconoscibili dagli AP
>[!note]
>Definiamo la famiglia dei linguaggi riconosciuti dagli AP deterministici come $L_{AP}$. Si ha che $L_{AP}$ non è chiusa rispetto all'unione e all'intersezione, ma è chiusa rispetto al complemento.

### Pumping lemma per AP
>[!note]
>$$\exists k\geq 1\qquad x=pvcws\in L_{AP}\quad|x|\geq k, \space|vcw|\leq k,\space|vc|\geq 1\iff \forall n\in \mathbb{N}\quad pv^{n}cw^{n}s\in L_{AP}$$

