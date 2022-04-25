# Tool di crittografia pt.2

Ci sono scenari in cui il messaggio può essere in chiaro ma non sappiamo la sorgente!

**Message authentication**: sono dei payload che andiamo adattaccare ai nostri messaggi, che contengono delle informazioni: es. il messaggio è stato o meno modificato nella trasmissione , la sorgente , ...

Solitamente si utilizzano le **hash funtions** per aggiungere il payload al messaggio da inviare.

Tramite un Messagge Authentication Code algorithm ritorniamo un payload da attaccare al messaggio. Il destinatario ricalcolerà il payload del messaggio e lo comparerà con il payload attaccato al messaggio.

NB. L'output deve avere sempre la **stessa dimensione**
NB1. Una funzione di hash basilare è il **MODULO**

Queste funzioni dovrebbero essere irreversibili, possono esserci poi delle collisioni, cioè tanti input vengono mappati nello stesso output.

Come exploitiamo le funzioni di hash?
- Cryptoanalisi
- Bruteforce

Lo SHA è l'algoritmo più utilizzato, nelle sue molteplici varianti.

### Numeri randomici
In **informatica NON esiste la randomicità**, per la crittografia quindi si creano degli algoritmi **pseudorandomici**. Solitamente questi algoritmi utilizzano un **SEED**.

SEED : definisce la randomicità 

*Se sappiamo il generatore utilizzato e riusciamo a ricostruire il seed, possiamo riprodurre completamente il numero delle chiavi utilizzate.*

Gli algoritmi NON devono essere uniformi.

