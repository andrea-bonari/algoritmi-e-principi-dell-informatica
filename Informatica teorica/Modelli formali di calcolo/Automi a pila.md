>[!note]
>Aggiungendo all'organo di controllo di un FSA una memoria a impilamento con funzionamento Last In First Out si ottiene un Automa a pila. L'automa a pila compie una mossa in funzione di:
>- Simbolo letto dalla cima della pila
>- Stato corrente nell'FSA che costituisce l'organo di controllo
>- Simbolo letto dal nastro d'ingresso
>L'automa a pila passa alla configurazione successiva:
>- Cambiando stato nell'OC
>- Sostituendo al simbolo in cima alla pila una stringa $\alpha$ di simboli
>- Spostando la testina di lettura
>- Se l'automa è traduttore, scrivendo una stringa
>
>![[Pasted image 20250310185230.png|center]]

Per convenzione si etichettano gli archi con formato: $$\langle\text{lettera input},\text{cima della pila letta / scritta in fondo alla pila}\rangle$$
Inoltre consideriamo la pila inizializzata con $Z_{0}$ per marcare il fondo.

### Automa riconoscitore
>[!note]
>Un automa è detto riconoscitore se la stringa $x$ in ingresso è accettata se l'automa scandisce completamente $x$, e lo stato dell'OC è di accettazione.

### Automa traduttore
>[!note]
>Un automa è detto traduttore se, all'accettazione della stringa, il nastro di scrittura contiene la sua traduzione al termine del calcolo $\tau(x)$. Se $x$ non è accettata la traduzione è indefinita $\tau(x)=\perp$
>