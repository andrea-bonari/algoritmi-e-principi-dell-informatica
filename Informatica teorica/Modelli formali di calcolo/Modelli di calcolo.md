>[!note]
>La fase di progettazione di un artefatto complesso si basa sull'uso di modelli. Questo ci permette di focalizzarci sugli aspetti primari del problema e permette verifiche preliminari sul funzionamento.

I modelli possono essere fisici, cioè riproduzioni in scala, oppure teorici/formali, cioè oggetti matematici che consentono una visione astratta del fenomeno modellato.

Un modello è adeguato se riflette correttamente il fenomeno modellato per gli aspetti che interessano.

### Modelli formali
>[!note]
>Per utilizzare un modello formale seguendo la seguente procedura:
>1. Formalizzazione del problema: ottenere una descrizione astratta dell'entità reale
>2. Risoluzione del problema formalizzato
>3. Interpretazione dei risultato alla luce del modello, nel contesto dell'entità reale

### Modelli dell'informatica
>[!note]
>L'informatica è una delle discipline con maggior vicinanza tra il modello e la realtà di cui si occupa. Nella sua evoluzione i primi calcolatori sono stati la materializzazione diretta del modello di calcolo.

I modelli nell'informatica hanno vantaggi come:
- Garanzie di correttezza, efficienza, robustezza, sicurezza
- Certificazione del livello di formalizzazione dell'artefatto Hardware/Software inclusa in standard

L'informatica trova applicazioni in svariati contesti perché un particolare calcolo effettuato è il modello di qualcosa reale, il successo è determinato dalla flessibilità del calcolo astratto come modello di una sequenza di ragionamenti logici.

Spesso la difficoltà risiede nel formulare il modello.

>[!example] Esempio - Formalizzazione di un ellisse:
>$$\begin{align*}
>&a,b,c,x,y,\in\mathbb{R}\\
>&ax^{2}+by^{2}=c
>\end{align*}$$

>[!example] Esempio - Formalizzazione dell'ordinamento
>Il nostro modello operativo ci dice che, dati $n$ elementi disordinati si ripete $n-1$ volte la seguente procedura:
>- Trova l'elemento più piccolo tra quelli da ordinare
>- Aggiungilo in coda agli elementi ordinati
>
>Infine si aggiunge in coda l'ultimo elemento.
>
>Formalmente, l'ordinamento è la permutazione della sequenza $a$ data tale che: $$\forall i\quad a[i]\leq a[i+1]$$
