>[!note]
>Un dizionario è una struttura dati astratta che contiene elementi accessibili direttamente, data la loro chiave. Nei nostri esempi assumiamo che le chiavi siano numeri naturali. Le operazioni supportate da un dizionario sono `Insert`, `Delete` e `Search`.

Nel caso in cui le possibili chiavi siano un numero limitato, un'implementazione di un dizionario è un vettore di puntatori. Le chiavi vengono usate come indice del vettore, e le operazioni sul dizionario sono implementate come:
- `Insert(D,e)`: `D[e.key] <- e`
- `Delete(D,e)`: `D[e.key] <- NIL`
- `Search(D,e.key)`: `return D[e.key]`

Per ciascuna di queste operazioni si ha complessità computazionale $\Theta(1)$ e complessità spaziale $\mathcal{O}(|D|)$, con $|D|$ dominio delle chiavi.

### Tabella hash
>[!note]
>Una tabella hash implementa un dizionario con una complessità in memoria pari al numero di chiavi $m$ per cui è effettivamente presente un valore. Tipicamente si prealloca uno spazio per $m$ chiavi, e si usa come indice della tabella il risultato del calcolo di una funzione della chiave detta funzione di hash $h(\cdot):D\to\set{0,\cdots,m-1}$.
>
>Idealmente $h$ mappa ogni chiave su un distinto elemento del suo codominio, tuttavia ciò è impossibile chiamiamo quindi collisione i casi in cui, date due chiavi $k_{1},k_{2}$ con $k_{1}\neq k_{2}$ abbiamo che $h(k_{1})=h(k_{2})$.

>[!tip] Metodo dell'indirizzamento chiuso
>Nel metodo dell'indirizzamento chiuso (anche chiamato open hashing o chaining) ogni riga della tabella (bucket) contiene la testa di una lista al posto del puntatore ad un singolo elemento. Nel caso di collisione l'elemento nuovo viene aggiunto in testa alla lista ($\Theta(1)$). Per cercare/cancellare un elemento di chiave $k$ è necessario cercare nell'intera lista di quelli del bucket $h(k)$.
>
>Nel caso pessimo tutti gli elementi collidono, dando origine ad una lista lunga $m$ elementi, e quindi `Insert`/`Delete`/`Search` costeranno $\mathcal{O}(m)$. Definiamo quindi il fattore di carico: $$\alpha= \frac{n}{m}\qquad 0\leq \alpha\leq \frac{|D|}{m}$$
>Se assumiamo che una scelta di $h$ fa si che ogni chiave abbia la stessa probabilità $\frac{1}{m}$ di finire in una qualsiasi delle $m$ celle (Ipotesi di Hashing Uniforme Semplice, IHUS), allora la lunghezza media di una lista è il fattore di carico $\alpha$, il tempo medio per cercare una chiave (presente o non presente) è $\Theta(1+ \alpha)$. Se il fattore di carico non è eccessivo tutte le operazioni sono $\mathcal{O}(1)$ in media.
>
>Si ha che il numero medio di tentativi prima di trovare un elemento desiderato è: $$\frac{1}{\alpha}\log\left(\frac{1}{1-\alpha}\right)$$

>[!tip] Metodo dell'indirizzamento aperto
>Nel metodo dell'indirizzamento aperto (anche chiamato open addressing o closed hashing), in caso di collisione si seleziona secondo una regola deterministica l'indirizzo di un altro bucket di destinazione (procedimento di ispezione). Nel caso non si trovino bucket vuoti l'inserimento può fallire ($\Theta(m)$), si rialloca una tabella più grande, vuota, e si reinseriscono tutti gli elementi della vecchia nella nuova (ricalcolando la loro hash), incluso il nuovo ($\Theta(n)$).
>
>Si modifica inoltre la procedura di ricerca, affinché, se l'elemento non viene trovato nel suo bucket, essa effettui la stessa ispezione. La cancellazione è effettuata inserendo un opportuno valore (tombstone) che non corrisponde a nessuna chiave.

### Procedure di ispezione

>[!note] Ispezione lineare e clustering
>Il metodo di ispezione più semplice è l'ispezione lineare. Dato $h(k,0)=a$ il bucket dove avviene la collisione al primo ($i=0$) tentativo di inserimento, si sceglie $h(k,i)=a+c\cdot i\text{ mod } m$ come bucket candidato per l'$i$-esimo inserimento.
>
>Tuttavia se ci sono molte collisioni su un dato bucket, peggiorerà la probabilità di collisione in tutte le vicinanze. Questo fenomeno è detto clustering primario delle collisioni. Per alcune scelte di $h$, il peggiorare delle prestazioni dovuto al clustering dell'ispezione lineare è molto forte. È possibile avere clustering di dimensione logaritmica nella dimensione della tabella, effettuando rehashing molto prima che sia piena.

>[!note] Ispezione quadratica
>Per mitigare il fenomeno del clustering è possibile utilizzare il criterio di ispezione quadratica, dove $h(k,i)=a+c_{1}i+c_{2}i^{2}\text{ mod }m$. Questa formula rimuove il clustering primario, tuttavia chiavi con la stessa posizione iniziale generano ancora più clustering: hanno la stessa sequenza di ispezione.

>[!example] Dimostrazione
>Si ha che $h(k,i)=a+ \frac{1}{2}i + \frac{1}{2}i^{2}$ genera tutti i valori in $[0,m-1]$. Supponiamo per assurdo che esistono $0<p<q<m-1$ tali che: $$\frac{1}{2}p+ \frac{1}{2}p^{2}= \frac{1}{2}q+ \frac{1}{2}q^{2}\text{ mod } m\Longrightarrow p + p^{2}= q+ q^{2}\text{ mod } 2m$$
>Fattorizzando abbiamo: $$(q-p)(p+q+1)=0\text{ mod }2m$$
>Se $q-p=0\text{ mod } 2m$ si ha $q=p$, che è assurdo. Se $p+q+1=0\text{ mod }2m$ dati i range possibili $0<p<q<m-1$ la somma è compresa tra $[1,2m-1]$, che è assurdo. Abbiamo quindi che $(q-p)(p+q+1)=0\text{ mod }2m$, ma $q-p\neq0\text{ mod }2m$ e $p+q+1\neq0\text{ mod }2m$, e quindi almeno uno tra $q-p$ e $p+q+1$ è dispari. Essendo $m=2^{x}$ solo il fattore pari può essere multiplo di $2m$, ma $(q-p)\leq m-1$ e $(p+q+1)\leq 2m-2$, che è assurdo.

### Doppio hashing
>[!note]
>Definiamo $h(k,i)=h_{1}(k)+h_{2}(k)i\text{ mod }m$. Allora il passo di ispezione dipende dalla chiave. Per essere sicuro di ispezionare tutti i bucket $h_{2}(k)$ deve essere coprimo con $m$. Per $m=2^{x}$ basta fare si che $h_{2}$ generi solo numeri dispari, mentre se $m$ è primo basta fare sì che $h_{2}$ generi un numero minore di $m$.

### Funzioni di hash

>[!note] Metodo della divisione
>È un metodo semplice: $$h(k)= k\text{ mod } m$$
>Normalmente ha una distribuzione non uniforme e va evitato se $m=2^{i}$, tuttavia ha distribuzione quasi uniforme se $m$ è primo vicino ad una potenza di due.

>[!note] Metodo della moltiplicazione
>Un altro metodo semplice è: $$h(k)=\lfloor m(ak-\lfloor ak\rfloor)\rfloor\qquad \alpha\in\mathbb{R}$$
>In questo caso, la dimensione della tabella $m$ non è critica. Una scelta possibile per $\alpha$ è $\frac{\sqrt{5}-1}{2}$, rappresentato a virgola fissa. Un modo pratico di calcolare $h(k)$ in C, nota la larghezza di parola del calcolatore $w$ è calcolare $2^{w}ak$, moltiplicare per $k$ e troncare. Per esempio per parole di $32b$:
>```C
>(uint32_t)(k * (double)ALPHA * ((uint64_t)1 << 32)))
>```

>[!note] Hashing universale
>Si può dimostrare che $h_{a,b}(k)= ((ak+b)\text{ mod }p)\text{ mod }m$ con $p>m$ primo, per qualunque $a,b\in\mathbb{Z}\smallsetminus\set{0}$ distribuisce uniformemente le chiavi nella tabella.

>[!note] Hashing crittografico
>Consideriamo il caso in cui il codominio di $h(\cdot)$ sia enorme. Con una buona $h$ che rispetti l'IHUS servono moltissime chiavi prima di vedere una collisione, Non potrò mai materializzare la tabella di hash, ma l'hash di un valore funge da etichetta unica del valore stesso. È importante che non si possano trovare collisioni o preimmagini in tempo utile. Esempio possono essere `SHA-2-256` con $D=\set{0,1}^{2^{64}}$.

