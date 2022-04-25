# RIPASSO

L'apertura della connessione normale della TCP avviene con SYN (con valore x),
a questo si risponderà con un segmento SYN con numero di sequenza y e numero di ack X + 1. Il client risponderà con un ACK

Initial sequence number: ciascun unità TCP lo preleva da un isn gnerator, cioè un processo che conta +1 , viene incrementato periodicamente, è una volta arrivato a contenere 32 bit tutti uguali a 1 , il nuovo +1 riporterà tutto a 0.

Una volta che un numero iniziale di sequenza verrà riutilizzato: sarà passato abbastanza tempo per cui le richieste avvenute con lo stessso numero di sequenza...

*Cosa succede se il client manda una richiesta SYN con num di sequenza X e non ottiene risposta? Genera una seconda richiesta, ovviamente con un num di sequenza diverso. Se questa va a buon fine: il server risponde con un flag SYN e il client risponde a sua volta con un ACK. A questo punto la connessione è aperta...*

Se server risponde con SYN = x e ACK = x + 1

**La situazione peggiore è quando si perde una richiesta e la sua risposta**

....

Per essere sicuri che X non sia ancora attivo, bisogna essere sicuri che il conteggio duri un intervallo di tempo maggiore di (2 * tempo di vita massimo di un pacchetto). 

<br>
<br>
<br>

- Il numero di ACK è il numero di sequenza del prossimo segmento che mi aspetto di ricevere.
- Il numero di sequenza è il numero del segmento corrente

Convenzionalmente all'inizio si considerà che il segmento SYN misuri 1 , ma per sapere quale sarà il prox numero di sequenza ...

*Esempio:*
-> SYN seq = 10
<- SYN seq = 50 ack = 11
-> seq = 11 ack = 51 (lunghezza 1000byte)
<- seq = 51 ack 1011 (lunghezza 500byte)
	Il prossimo numero di sequenza che mi aspetto è 1011
-> seq = 1011 ack =551

*Non si fa di volta in volta un +1 , ma si fa **+lunghezzaSegmento** *


NB. Nel protocollo HDLC (del livello datalink) i contatori crescono di 1, e quando si parla di dimensione della finestra di trasmissione (che è 7) si intende lo spazio per contenere 7 PDU.

Invece quando qui si dice window size = 5000 , vuol dire che si possono riceve al massimo segmenti che sommati siano 5000.