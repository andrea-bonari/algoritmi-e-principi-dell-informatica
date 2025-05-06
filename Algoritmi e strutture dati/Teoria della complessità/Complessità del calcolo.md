>[!note]
>La complessità del calcolo ci permette di razionalizzare i concetti di costo di una computazione (tempo e memoria), e misura e confronto del costo di soluzioni ad un problema.

Per la tesi di Church-Turing, un problema è calcolabile o meno indipendentemente dallo strumento usato. Non si ha una "tesi di Church-Turing" della complessità. Ci serve uno strumento per valutare la complessità temporale e spaziale che tralasci "considerazioni superflue" e utilizzabile per la maggioranza dei modelli di calcolo.

### Complessità temporale e spaziale
>[!note]
>Data la computazione $c_{0}\stackrel{*}{\vdash}c_{r}$ di $\mathcal{M}$, la complessità temporale di è $\mathit{T}_{\mathcal{M}}(x)=r$ se $\mathcal{M}$ si ferma in un dato $c_{r}$, $\infty$ altrimenti. La complessità spaziale è definita come $\mathit{S}_\mathcal{M}(x)=\sum\limits_{j=1}^{k}\max_{i\in\set{0,\cdots,r}}(|a_{ij}|)$ con $|a_{ij}|$ lunghezza del contenuto del $j$-esimo nastro alla mossa $i$-esima, cioè la somma delle quantità di nastro occupate, per ogni nastro. 
>
>Sotto opportune ipotesi, è possibile semplificare da $\mathit{T}_\mathcal{M}(x)$ e $\mathit{S}_\mathcal{M}(x)$ a $\mathit{T}_\mathcal{M}(n)$ e $\mathit{S}_\mathcal{M}(n)$, dove $n$ è la lunghezza dell'input. Generalmente scegliamo, sia per $\mathit{T}_\mathcal{M}(\cdot)$ che per $\mathit{S}_\mathcal{M}(\cdot)$:
>- Caso pessimo: $\mathit{T}_\mathcal{M}(n)=\max\limits_{x, |x|=n}\mathit{T}_\mathcal{M}(x)$
>- Caso ottimo: $\mathit{T}_\mathcal{M}(n)=\min\limits_{x, |x|=n}\mathit{T}_\mathcal{M}(x)$
>- Caso medio: $\mathit{T}_\mathcal{M}(n)=\sum\limits_{x, |x|=n}\text{Pr}(\mathcal{X}=x)\mathit{T}_\mathcal{M}(x)$

Introduciamo una notazione per indicare il comportamento asintotico di una funzione:
- Notazione $\mathcal{O}$-grande per il limite asintotico superiore
- Notazione $\Omega$-grande per il limite asintotico inferiore
- Notazione $\Theta$-grande per il limite asintotico sia superiore che inferiore

### Notazione $\mathcal{O}$-grande
>[!note]
>Definiamo $\mathcal{O}(g(n))$ come l'insieme di funzioni $f(n)$ con dominio in $\mathbb{N}$: $$\mathcal{O}(g(n))=\set{f(n)\space|\space \exists c>0, n_{0}>0 \text{ tali che }\forall n>n_{0}\quad f(n)\leq c\cdot g(n)}$$

È comune usare $f(n)=\mathcal{O}(g(n))$ al posto di $f(n)\in\mathcal{O}(g(n))$ come abuso di notazione.

Se $\lim_{n\to\infty} \frac{f(n)}{g(n)}=0$ allora $f(n)\in \mathcal{O}(g(n))$.
### Notazione $\Omega$-grande
>[!note]
>Definiamo $\Omega(g(n))$ come l'insieme di funzioni $f(n)$ con dominio in $\mathbb{N}$: >$$\Omega(g(n))=\set{f(n)\space|\space \exists c>0, n_{0}>0 \text{ tali che }\forall n>n_{0}\quad f(n)\geq c\cdot g(n)}$$

Si ha che se e solo se $f(n)\in\mathcal{O}(g(n))$ allora $g(n)\in\Omega(f(n))$.

### Notazione $\Theta$-grande
>[!note]
>Definiamo $\Theta(g(n))$ come l'insieme di funzioni $f(n)$ con dominio in $\mathbb{N}$: >$$\Theta(g(n))=\set{f(n)\space|\space \exists c_{1}>0,c_{2}>0 n_{0}>0 \text{ tali che }\forall n>n_{0}\quad c_{1}g(n)\leq f(n)\leq c_{2}\cdot g(n)}$$

Si ha che l'appartenenza a $\Theta(f(n))$ è una relazione di equivalenza sull'insieme di funzioni.
Si ha che inoltre che $f(n)\in\Theta(g(n))$ se e solo se $f(n)\in\mathcal{O}(g(n))\land f(n)\in\Omega(g(n))$.

Se $\lim_{n\to \infty} \frac{f(n)}{g(n)}=c$ con $c\neq0$ e $c\neq\infty$, allora $f(n)\in\Theta(g(n))$.

>[!tip]
>Spesso è necessario trovare un compromesso spazio-temporale per la risoluzione di un problema.
>
>In generale si ha che:
>- $\mathit{S}_\mathcal{FSA} (n)\in\Theta(1)$ e $\mathit{T}_\mathcal{FSA}\in\Theta(n)$
>- $\mathit{S}_\mathcal{ADP} (n)\in\mathcal{O}(n)$ e $\mathit{T}_\mathcal{ADP}\in\Theta(n)$
>- $\mathit{S}_\mathcal{M}(n)$ non potrà mai essere minore di $\Theta(n)$

### Teoremi di accelerazione lineare
>[!note]
>Si ha che:
>- Se $L$ è accettato da una MT $\mathcal{M}$ a $k$ nastri in $\mathit{S}_\mathcal{M}(n)$, per ogni $c\in\mathbb{Q},c>0$ posso costruire una MT $\mathcal{M}'$ a $k$ nastri con $\mathit{S}_{\mathcal{M}'}(n)<c\cdot \mathit{S}_\mathcal{M}(n)$
>- Se $L$ è accettato da una MT $\mathcal{M}$ a $k$ nastri in $\mathit{S}_\mathcal{M}(n)$, posso costruire una MT $\mathcal{M}'$ a $1$ nastro (non nastro singolo) con $\mathit{S}_{\mathcal{M}'}(n)=\mathit{S}_\mathcal{M}(n)$
>- Se $L$ è accettato da una MT $\mathcal{M}$ a $k$ nastri in $\mathit{S}_\mathcal{M}(n)$, per ogni $c\in\mathbb{Q},c>0$ posso costruire una MT $\mathcal{M}'$ a $k=1$ nastri con $\mathit{S}_{\mathcal{M}'}(n)<c\cdot \mathit{S}_\mathcal{M}(n)$
>- Se $L$ è accettato da una MT $\mathcal{M}$ a $k$ nastri in $\mathit{T}_\mathcal{M}(n)$, per ogni $c\in\mathbb{Q},c>0$ posso costruire una MT $\mathcal{M}'$ a $k+1$ nastri con $\mathit{T}_{\mathcal{M}'}(n)=\max(n+1, c\cdot \mathit{T}_\mathcal{M}(n))$

>[!example] Dimostrazione
>Dimostriamo il primo teorema:
>
>Scegliamo un fattore di compressione intero $r$ tale che $r\geq c$. Per ognuno degli $i$ nastri di $\mathcal{M}$, considero l'alfabeto $\Gamma_{i}$ e costruisco $\Gamma_{i}'$ di $\mathcal{M}'$ creando un elemento in $\Gamma_{i}'$ per ogni $s\in\Gamma_{i}^{r}$. Costruiamo quindi l'OC di $\mathcal{M}'$ in moto tale per cui:
>- Calcoli con i nuovi simboli sui nastri emulando le mosse di $\mathcal{M}$ spostando le testine sui nastri di $\mathcal{M}'$ ogni $r$ movimenti di $\mathcal{M}$
>- Memorizzi la posizione della testina "all'interno" dei nuovi simboli degli alfabeti di nastro $\Gamma$, usando gli stati.
>
>Dimostriamo il quarto teorema:
>
>Usiamo un approccio simile a quello precedente: codifichiamo in modo compresso i simboli dell'alfabeto $\mathcal{M}$ e calcoliamo sui simboli compressi. Dobbiamo considerare che la compressione è fatta a runtime: il minimo costo per effettuare la compressione è lineare nel numero di simboli da comprimere.
>
>Comprimendo $r$ simboli in uno, nel caso pessimo, possono servirmi $3$ mosse $\mathcal{M}'$ per emularne $r+1$ di $\mathcal{M}$.

### Macchina RAM
>[!note]
>La macchina RAM ha un nastro di lettura In e uno di scrittura Out come nella MT. Assumiamo il programma cablato nell'OC, così come la logica del program counter. La RAM è dotata di una memoria ad accesso a indirizzamento diretto $M[n]\quad n\in\mathbb{N}$ al posto dei nastri di memoria: l'accesso non necessita di scorrimento delle celle. Le istruzioni di un programma usano come primo operando sorgente e come operando destinazione $M[0]$. Ogni cella contiene un intero $x\in\mathbb{N}$.

Definiamo L'instruction set e semantica pseudo-RTL:

| Istruzione | Semantica                                |
| ---------- | ---------------------------------------- |
| `LOAD X`   | $M[0]\leftarrow M[X]$                    |
| `LOAD= X`  | $M[0]\leftarrow X$                       |
| `LOAD* X`  | $M[0]\leftarrow M[M[X]]$                 |
| `STORE X`  | $M[x]\leftarrow M[0]$                    |
| `STORE* X` | $M[M[X]]\leftarrow M[0]$                 |
| `ADD X`    | $M[0]\leftarrow M[0]+M[X]$               |
| `SUB X`    | $M[0]\leftarrow M[0]-M[X]$               |
| `MUL X`    | $M[0]\leftarrow M[0]\times M[X]$         |
| `DIV X`    | $M[0]\leftarrow M[0] \div M[x]$          |
| `HALT`     | $-$                                      |
| `READ X`   | $M[X]\leftarrow\text{In}$                |
| `READ* X`  | $M[M[X]]\leftarrow\text{In}$             |
| `WRITE X`  | $\text{Out}\leftarrow M[X]$              |
| `WRITE= X` | $\text{Out}\leftarrow X$                 |
| `WRITE* X` | $\text{Out}\leftarrow M[M[X]]$           |
| `JUMP L`   | $\text{PC}\leftarrow L\text{ se }M[0]=0$ |
| `JZ L`     | $PC\leftarrow L$                         |

### Limite del criterio di costo
>[!note]
>Si ha che copiare/spostare/scrivere/leggere un intero $i$ costa tanto quanto il suo numero di cifre in base $b$: $\log_{b}(i)=\Theta(\log(i))$.
>Il costo delle operazioni aritmetico/logiche elementari dipende dall'operazione, definendo $d=\log_{2}(i)$ si ha che:
>- Le addizioni e sottrazioni al bit costano $\Theta(d)$
>- Le moltiplicazioni, scolasticamente, costano $\Theta(d^{2})$
>- Le divisioni, scolasticamente, costano $\Theta(d^{2})$
>
>Le istruzioni `JUMP` e `HALT` sono a costo costante.

### Tesi di correlazione polinomiale
>[!note]
>Risolvere lo stesso problema con macchine diverse può dare luogo a complessità diverse. In generale non esiste un modello migliore in assoluto.
>
>Sotto "ragionevoli" ipotesi di criteri di costo, se un problema è risolvibile da $\mathcal{M}$ in $\mathit{T}_\mathcal{M}(n)$, allora è risolvibile da qualsiasi altro modello $\mathcal{M}'$ in $\mathit{T}_{\mathcal{M}'}=\pi(\mathit{T}_\mathcal{M}(n))$ dove $\pi(\cdot)$ è un opportuno polinomio.

Si ha che, per la MT a $k$ nastri e RAM:
- La MT impiega al più $\Theta(\mathit{T}_\mathcal{RAM}(n))$ per simulare una mossa della RAM
- Se la RAM ha complessità $\mathit{T}_\mathcal{RAM}(n)$, essa effettua al più $\mathit{T}_\mathcal{RAM}(n)$ mosse
- La simulazione completa della RAM da parte della MT costa al più $\Theta((\mathit{T}_\mathcal{RAM}(n))^{2})$, e quindi il legame tra $\mathit{T}_\mathcal{RAM}(n)$ e $\mathit{T}_\mathcal{MT}(n)$ è polinomiale.
