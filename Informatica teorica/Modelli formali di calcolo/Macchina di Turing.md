>[!note]
>Una macchina di Turing (MT) è un modello di calcolo basato su gli automi a pila, ma con $k$ nastri di memoria.
>![[Pasted image 20250416132712.png|center]]
>$\newcommand{\blank}{\text{␢}}$
>Per convenzione storica e semplicità di formalizzazione, i nastri sono sequenza infinite di celle di cui:
>- Solo una quantità finita è inizializzata con un valore sensato
>- Le celle restanti contengono uno spazio vuoto o il valore blank $\blank$
>
>Tutte le testine possono scorrere su nastri o rimanere ferme

La transizione di un MT avviene in funzione di:
- Lettura del carattere sotto la testina del nastro di input
- Lettura dei caratteri sotto le testine dei nastri di memoria
- Stato dell'organo di controllo

E può effettuare come azioni:
- Cambiare lo stato dell'organo di controllo
- Scrivere un carattere su ogni nastro di memoria
- Scrivere un carattere sul nastro di output
- Spostare le testine di memoria e ingresso: una posizione a sinistra $L$, destra $R$ o ferme $S$
- Spostare la testina di output: una posizione a $S$ e $R$, se si sposta si scrive sempre una lettera o un $\blank$.

Per convenzione si etichettano gli archi con formato: $$\langle i,\space (A_{1},\cdots, A_{k}) / w, \space (A_{1}',\cdots, A_{k}'),\space (m_{\text{in}}, m_{1},\cdots, m_{k}, m_{k+1}) \rangle$$
Con $m_{\text{in}}\in\set{\text{L},\text{S},\text{R}}$ mossa della testina di input, $m_{1\cdots k}\in\set{\text{L},\text{S},\text{R}}$ mosse delle memorie e $m_{k+1}\in\set{\text{S},\text{R}}$ mossa della testina di output. Inoltre consideriamo la pila inizializzata con $Z_{0}$ per marcare il fondo.

### TM riconoscitore
>[!note] 
>La funzione di transizione di una TM riconoscitore è definita come: $$\delta: Q\times(I\cup\set{\blank})\times \Gamma^{k}\to Q\times \Gamma^{k}\times \set{\text{L},\text{S},\text{R}}^{k+1}$$

>[!example] Esempio riconoscitore di $L=\set{a^{n}b^{n}c^{n}\space|\space n>0}$
>![[Pasted image 20250416135822.png|center]]
### TM traduttore
>[!note]
>La funzione di traduzione di una MT traduttore è definita come: $$\eta: Q\times (I\cup \set{\blank})\times \Gamma^{k}\to (O\cup\set{\blank})\times\set{\text{S},\text{R}}$$

### Configurazione e transizione di una TM
>[!note]
>Di base, tutti i nastri di memoria sono pieni di $\blank$, tranne nella posizione iniziale della rispettiva testina, dove c'è $Z_{0}$. Si ha inoltre come stato iniziale dell'organo di controllo $q_{0}$, e la strina di ingresso $x$ è scritta a partire della $0^{a}$ cella del nastro di ingresso, seguita e preceduta da $\blank$. Mentre il nastro di uscita è riempito con $\blank$.
>
>Come per gli FSA e gli AP, gli stati di accettazione sono $F\subseteq Q$. Per convenzione, la $\delta$ e $\eta$ non sono definite a partire dagli stati finali: $$\forall q\in F\quad \delta(q,\cdots)=\perp\quad \eta(q,\cdots)=\perp$$
>
>Una stringa $x$ in ingresso è accettata se e solo se in un numero finito di transizioni, la macchina si ferma in $q\in F$.

### Proprietà di una TM
>[!note]
>Si ha che una TM è chiusa a $\cup$, $\cap$, $.$, $*$, ma non al complemento.

### Modelli equivalenti
>[!note]
>È possibile costruire modelli di calcolo equivalenti alla MT, tra cui:
>- Una MT con nastro bidimensionale
>- Una MT con $k$ testine per nastro
>- Un AP con due pile
>
>Se un modello di calcolo può simulare una MT viene detto Turing completo. Una MT è in grado di simulare il comportamento di una macchina di Von Neumann. La differenza principale tra loro è la modalità di accesso alla memoria.

>[!tip] MT a nastro singolo
>Una particolare variante della MT è quella a nastro singolo, dove input, output e memoria sono tutti nello stesso nastro. È in grado di emulare una MT a $k$ nastri.
