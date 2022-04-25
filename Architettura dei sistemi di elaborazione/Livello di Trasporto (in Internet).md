# Livello di Trasporto (in Internet)
<br>

## TSAP, Transport Service Access Point
Un **TSAP rappresenta un'indirizzo di livello di trasporto**.
- Il **TSAP destinazione** serve per identificare **univocamente** a chi sono **destinati i dati** contenuti in un segmento.
- Il **TSAP sorgente** serve per identificare **univocamente** chi ha **generato i dati** contenuti in un segmento.

Il TSAP ha forma: **IPaddress:PortNumber** dove:
- ***IP Address*** è l'indirizzo del nodo in cui è in esecuzione l'applicazione
- ***Port Number*** è un **numero a 16bit** che server a identificare in modo univoco

**NB.** *Quando parliamo di interfacce tra livello di trasporto e applicazione, NON si parla di progettisti di rete ma di progettisti di applicazione.*

Le applicazioni di rete sono progettate secondo il paradigma **CLIENT-SERVER** (es. server di posta, web, ftp,...) alcune applicazioni però si basano sul paradigma **peer-to-peer** (es. bitTorrent).

#### Paradigma CLIENT-SERVER
Il **server deve partire per PRIMO** e **mettersi in ascolto** di una chiamata del client, il client invece cerca la connessione col server.

Le richieste del client solitamente sono abbastanza semplici, il server invece risponde con pagine web, immagini, video,...

**NB.** Per i servizi standard di Internet vengono utilizzate le cosidette **"well known ports"**, numeri predefiniti e riservati, fino a **1024**.

Le applicazioni di tipo client quando instaurano la connessione devono specificare a quale indirizzo e porta voglioni collegarsi; **il loro numero di porta viene assegnato dall'entità di trasporto**, in questo caso si parla di **porte locali o EFFIMERE**.

#### Paradigma peer-to-peer
Le applicazioni peer-to-peer invece sono sviluppate realizzando sia client sia server, Questo rimane in ascolto cosicchè altri utenti peer-to-peer vengano a cercare contenuti tra noi.
<br>

## Primitive di definizione del servizio: interfaccia Socket
*Come fanno le applicazioni ad utilizzare i servizi della rete?*
L'**interfaccia standard tra livello applicazione e di trasporto** si chiama **SOCKET**.

*Le applicazioni NON possono interagire direttamente con l'hardware ma devono utilizzare delle chiamate al sistema operativo.*
Questi socket, detti **socket di Berkeley**, vengono utilizzati tramite un'insieme di **PRIMITIVE**, cioè delle **chiamate al sistema operativo** che somigliano a delle chiamate di funzione in C.

L'applicazione vede il socket come una **coppia di stream**, cioè una coppia di **file**, uno aperto in **scrittura** e uno aperto il **lettura**. Scrivere nel socket corrisponde a inviare dati in rete, leggere dal socket corrisponde a ricevere dati dalla rete.

*Grazie ai socket di Berkeley riusciamo a capire come tutta la complessità di gestione della rete sia a carico dei livelli di trasporto, di rete, datalink. Il livello applicativo ha già tutto pronto.*

#### Comunicazione client - server
1. Il **server deve partire per primo**, aprire il socket specificando un numero di porta e **mettersi in ascolto** per attendere connessioni dai client
2. Il **client** deve partire dopo il server, **aprire il socket specificando IP e porta del server aprire la connesione**
3. Aperta la connessione, **all'operazione di "scrittura"** nel socket da parte di una delle 2 applicazioni **deve corrispondere una operazione di "lettura"** da parte dell'altra.
<br>

### Principali primitive
- **socket**: crea un punto di comunicazione
- **connect**: stabilisce una connessione attiva con il server remoto; specifica l'indirizzo IP e porta remoti, sceglie indirizzo IP e porta locali
- **bind**: specifica indirizzo e porta locale da associare ad un socket
- **listen**: pone il socket in modo passivo
- **accept**: accetta una richiesta di connessione
- **read, write**: ricevono e inviano dati
- **sendto, recvfrom**: inviano e ricevono dati specificando l'indirizzo IP (servizio datagram)
- **close**: chiude il socket
<br>

### Struttura delle applicazioni
- **Struttura client/server ORIENTATA alla connessione (TCP)**:
	- Server: socket -> bind -> listen -> accept ----- (read -> write) -> close
	- Client: socket -> connect	--------------------- (read -> write) -> close
- **Struttura client/server NON ORIENTATA alla connessione (UDP)**:
	- Server: socket -> bind -> recvfrom -> sendto -> close
	- Client: socket -> bind -> sendto -> recvfrom -> close

*NB. La comunicazione tramite UDP è molto più immediata. Es: client fa richiesta dns al server, il server risponde mandado la risoluzione dell'indirizzo.*
*Schematicamente: client invia -> server risponde , server invia -> client risponde , termina la connessione.*
<br>

### Comunicazione Client-Server con TCP
![[comunicazioneClient-Server.png]]

*NB. Se la connect parte prima che il server sia in "ascolto", questa FALLISCE!*
<br>

## UDP, User Datagram Protocol
*Alcune caratteristiche*:
- **UDP è un protocollo datagram**, quindi **NON ORIENTATO ALLA CONNESSIONE** e **NON AFFIDABILE**.
- È utlizzato da applicazioni che prevedono **semplici scambi domanda/risposta** (es. **DNS**), oppure da **applicazioni per cui la velocità è preferibile alla perdita di dati** (es. **VoIP**), dove il TCP porterebbe un **eccessivo overhead**
- Ha un funzionamento semplice, i **messaggi dell'applicazione vengono semplicemente inseriti in un segmento** e passati a livello di rete.
- La comunicazione tra 2 applicazioni avviene sempre tramite una coppia di TSAP


**NB**. La connessione è utile se si manda una sequenza di segmenti, ma nel caso si debba mandare una sola domanda e si debba ricevere una sola risposta (es. DNS), è inutile. Potrebbe essere utile l'affidabilità, ma col DNS, viene gestita dall'applicazione (e non al livello di trasporto).

### UDP: Formato intestazione
![[intestazioneUDP.png]]

## TCP, Transmission Control Protocol
*Rispetto all'UDP svolge un lavoro complesso. Alcune caratteristiche:*
- È progettato per **fornire** (al livello superiore) un **flusso di byte affidabile**, da sorgente a destinazione, **su una rete NON affidabile**
- È un protocollo **AFFIDABILE** e **ORIENTATO ALLA CONNESSIONE**
- È un **protocollo full-duplex**: **contemporaneamente sarà gestita la trasmissione e la ricezione**, in più con:
	- **Gestione di ACK**
	- **Controllo del flusso**: la controparte della connessione non può trasmettere all'altra parte più dati di quanti quest'ultima possa riceverne in quel momento
- Il TCP si occupa anche del **controllo della congestione**

#### TCP: Funzionamento
1. Si ricevono i dati dall'applicazione
2. I **dati vengono organizzati in segmenti di dimensione max 64.000byte** (meno la dimensione di un'intestazione IP, tipicamente 1500byte)
3. Il **segmento viene consegnato al livello di rete**, eventualmente ritrasmettendolo se necessario: dovrà quindi **tenere in memoria tutti i pacchetti di cui non ha ancora ricevuto l'ACK**
4. Contemporaneamente, **riceve segmenti dal livello di rete**, eventualmente **riordinandoli**, eliminando buchi e doppioni
5. **Consegna i dati ORDINATI** (rispetto a come sono stati trasmessi) al livello applicazione

*NB. Negli esempi che vedremo più avanti la comunicazione sarà simplex: da una parte viaggiano le informazioni e dall'altra le ACK.*

#### TCP: Caratteristiche fondamentali
- **Ogni byte del flusso TCP è numerato VIRTUALMENTE con un numero d'ordine a 32bit**, usato sia per il controllo del flusso che per la gestione dell'ACK
- Un segmento TCP NON può superare i 65.535byte
- Un **segmento TCP è formato da un header e dai dati da trasportare**. L'header è costituito da una parte fissa di 20byte e da una parte opzionale.

#### TCP: Controllo del flusso
Il **TCP usa una politica sliding windows di tipo go-back-n (o selective-repeat) con timeout**, quindi se entro un tot di tempo non si riceve il riscontro, si ritrasmette.

**NB.** Mentre nel livello datalink venivano numerati i frame, nel TCP ogni byte del segmento è numerato virtualmente.

### TCP: Formato intestazione
![[intestazioneTCP.png]]

- **Porta sorgente**
- **Porta di destinazione**
- **Sequence number**: rappresenta il **numero del primo byte del payload**. Es. Se è di 500 e i dati da trasmettere sono 1000byte, questi 1000byte sono virtualmente numerati da 500 a 1499
- **ACK number**: rappresenta il **numero di sequenza del primo byte del prossimo segmento che mi aspetto di ricevere**
- Lunghezza dell'intestazione: espresso in longword
- Checksum: per controllare l'intestazione
- **Window size**: rappresenta la **dimensione della finestra di ricezione: comunica quanti byte,** in quel momento, **è in grado di ricevere**. Es. se è di 500byte la controparte può trasmettere al massimo 500byte. Il window size cambia:
	- in funzione dei dati che vengono inviati
	- In funzione delle operazioni di lettura che avvengono al livello superiore (applicazione)
- **Urgent point**: se in questo segmento sono contenuti dei byte urgenti, urgent point specifica il numero virtuale da cui partono questi dati
- **Flag URG**: impostato a 1, nel segmento ci sono dati urgenti
- Flag ACK: impostato a 1 significa che il contenuto del campo ACK number è valido
- Flag RST: utilizzato quando si verifica un problema
- **Flag SYN**: usato in **apertura della connessione**
- **Flag FIN**: usato in **chiusura della connessione**
- Flag PSH: serve per indicare che questi dati andrebbero spediti e consegnati il prima possibile all'applicazione

**NB.** Un messaggio GET da browser viene inviato via PUSH.
<br>

## Attivazione della connessione TCP
- Quando il **segmento SYN (con seq = x) arriva** a destinazione, l'entity di livello di trasporto lato **server**:
	- **Se c'è un processo in ascolto** sul port number in questione **risponde** con segmento di conferma con **flag SYN a ACK importati a 1**
	- **Altrimenti** invia un segmento con **flag RST a 1** per rifiutare la connessione
- Quando l'**entità TCP lato client riceve il segmento SYN di conferma**, considera la **connessione aperta** e **risponde** con un segmento **ACK** che può già contenere dei dati
- Alla ricezione di questo 3o segmento, **anche l'entità TCP lato server considera la connessione aperta**. Ora il **client può mandare i dati con ACK = y + 1 e SEQ = x + 1**

**NB0.** I contatori partono da valori che non sono 0 e se li devono comunicare.
**NB1.** Quando l'entità TCP del client manda fa la connect, invia dall'altra parte un segmento TCP che ha flag SEQ = 1 e flag ACK = 0.
**NB2.** Chi apre la connessione decide il numero iniziale di sequenza, ma non può sapere da che numero partirà l'altro, per cui nel primo segmento SYN questa informazione non esiste e il flag ACK sarà a 0.
<br>

## Apertura della connessione TCP
![[apertura-connessione-tcp.png]]

## Gestione dei ritardatari duplicati
Col livello di trasporto bisogna risolvere dei problemi di rete, possiamo quindi immaginare un'analogia livello Rete+Trasporto e livello Fisico+Datalink. Però c'è una differenza:
- Il livello datalink opera sul livello fisico, bisogna gestire la comunicazione tra 2 stazioni, il frame o arriva o non arriva a destinazione.
- Nel livello di trasporto posso aprire la connessione con un nodo molto vicino o molto distante, nel secondo caso i pacchetti che girano per la rete possono essere memorizzati in vari buffer di diversi router.

*Se chi ha mandato il segmento SYN non riceve in tempo utile una risposta lo rimanda, potrebbe succedere però che la richiesta precedente arriva molto tempo dopo, per chi la riceve sembra leggittima, NON ha modo per sapere che quella è una vecchia richiesta. Questo è un **RITARDATARIO DUPLICATO**, poichè arrivato in ritardo e come copia di un altra richiesta.*

A differenza del livello datalink, un segmento che NON è ancora arrivato potrebbe essere semplicemente in ritardo, bisogna quindi **evitare di fare confusione tra un segmento e un ritardatario duplicato**.

Per evitare di fare confusione bisogna fare in modo che i **numeri iniziali di sequenza (ISN) siano univoci in un determinato intervallo di tempo**.

**NB1.** **Non abbiamo a disposizione però numeri infiniti, ma numeri fino a 32bit, arrivati al numero massimo si torna a 0**. È importante garantire che il numero iniziale di sequenza x possa essere riutilizzato dopo 2 volte il tempo di vita max dei segmenti.
**NB2.** Per garantire la correttezza dell'apertura della connessione TCP, dobbiamo essere sicuri che i segmenti arrivino in un determinato lasso di tempo.
**NB3.** Il caso peggiore è quando si perde il primo segmento e la sua risposta.
<br>

## Numero iniziale di sequenza ISN
*Come viene preso l'ISN?*
**ISN generator è un contatore a 32bit che si incrementa gradualmente di 1.** Quando arriva a 2³² - 1 riparte da 0. Il **tempo da 0 allo 0 successivo è di circa 4.55 ore**. 

Quando si apre una connessione gli ISN possono essere riutilizzati solo se si è sicuri che non esistano più in rete vecchi segmenti con gli stessi numeri nè come numero di sequenza nè come numero di conferma.
<br>

## Chiusura connessione TCP
Il rilascio della connessione avviene considerando la connessione full-duplex come un coppia di connessioni simplex indipendenti, e si svolge:
1. Quando una della parti non ha più nulla da trasmettere, invia un segmento FIN
2. Quando il FIN viene confermato, la connessione in uscita viene rilasciata
3. Quando anche l'altra parte completa lo stesso procedimento e rilascia la connessione nell'altra direzione, la connessione full-duplex termina

*Se io mando una richiesta di chiusura della connessione e l'altra parte mi risponde con un OK, il mandante chiude la connessione ma il "secondo lato" non ha conferma di chiusura della connessione e potrebbe continuare a inviare dati. -> **Questo problema non si può risolvere, sono stati integrati dei timeout***

### Chiusura connessione TCP: 4 segmenti
![[chiusura-connessione-tcp-4.png]]

1. Chi vuole chiudere la connessione manda un segmento FIN
2. La controparte risponde con un ACK
3. Il primo riceve l'ACK ma **il secondo può ancora inviare dati (anche nell'ACK)**
4. Il secondo decide di chiudere la connessione, avviene quindi lo stesso processo

Si identifica con una chiusura a 4 segmenti poiché: FIN -> ACK , FIN -> ACK

### Chiusura connessione TCP: 3 segmenti
*Entrambe le parti decidono di chiudere insieme la connessione.*

![[chiusura-connessione-tcp-3.png]]

**ACTIVE CLOSE - PASSIVE CLOSE**
<br>

## Stati di connessione TCP
![[stati-connessione-tcp.png]]

Questo disegno è un **diagramma di trasizione degli stati**.
- **STATO**: è una **SITUAZIONI in cui si trova il nostro automa**, l'entità TCP si può trovare in uno di questi stati (i nodi del diagramma).
- **FRECCIA**: sono le **TRANSIZIONI**, ognuna è marcata da una coppia input/output: il passaggio dello stato avviene perchè è stato sollecitato da un input e, come risposta, ritorna un output.

L'evento **LISTEN** permette il passaggio da stato chiuso ad ascolto.
**NB**. Il **-** vuol dire che dall'altra parte non viene inviato alcun segmento.

Le trasizioni di stato possono dipendere da:
- **eventi di protocollo**: segmenti che si ricevono dall'altra parte
- **eventi di interfaccia**: l'interfaccia fa qualcosa

*Rappresentazione apertura della connessione tramite diagramma di stati:*
- Server: Se sono nello stato LISTEN e ricevo un segmento SYN, devo rispondere con un segmento SYN+ACK e mi porto nello stato SYN RECEIVED.
- Client: Dalla parte del client invece si parte con una CONNECT e l'entità TCP va allo stato SYN SENT e rimane li finche non riceve un SYN+ACK

**NB**. È molto più facile progettare un software che deve fare queste operazioni, se si lavora con un modello di grafo di rappresentazione degli stati
<br>

## TCP: Controllo del FLUSSO
![[controllo-flusso-tcp.png]]

*A cosa serve il controllo del flusso?*
**Permette che chi trasmette i dati non ne invii più di quanti possa riceverne la controparte.**

**Window Size**: serve per comunicare alla controparte la dimensione (in byte) della propria finestra di trasmissione.
Se si comunica una window size = 0, significa che NON si possono ricevere dati; in questo caso, nel momento in cui si ha nuovamente spazio, lo si deve comunicare alla controparte in modo da sbloccare la comunicazione.

**NB.** In queste slide gli schemi rappresentano una comunicazione **simplex**, nella realtà è **duplex (bidirezionale)**, dove entrambe le parti trasmettono e ricevono dati e ACK.

*Come facciamo a sapere quanto è grande la finestra di ricezione dell'altra parte?*
Grazie al segmento SYN che ci siamo scambiati a inizio della connessione.

*Spiegazione dello schema:*
- Il mittente manda 2Kbyte con numero di sequenza = 0, 
- La risposta per quanto riguarda il controllo del flusso: ACK = 2048 , nuova dimensione del windows size = 2048.
Se adesso il mittente manda 2048, il ricevente avrà il buffer completamente occupati, quindi manderà un ACK con ack=4096 e win=0.  Il mittente non potrà quindi più spedire dati.
- Appena il ricevente avrà di nuovo il buffer libero, manderà all'altro lato un segmento con la nuova finestra di ricezione

**NB.** I numeri di sequenza e di ACK (cioè i segmenti dati) hanno come numero: il numero dei dati inviati + num precedente . Solo i segmeni iniziali, come SYN hanno num di seq = 1 .
<br>

## TCP: Controllo della congestione
Il **TCP ha una politica di ristrasmissione**, quindi **aspetta le conferme dei segmenti che sta trasmettendo**, se non arrivano in tempo utile, il segmento viene rimandato.

*In caso di fenomeno di congestione, i router comincierebbero a scartare i pacchetti: verrebbero così spedite tante copie dello stesso pacchetto. Si rischia che in giro ci siano tanti pacchetti, ma MOLTI DUPLICATI NON PIÙ VALIDI... Questo fenomeno continuerebbe ad autoalimentarsi.*

**Van Jacobson** ha escogitato un **sistema per introdurre nel TCP il controllo della congestione**:
- basato su **finestre scorrevoli a dimensione variabile**
- **senza modificare la struttura di router**

##### Come fa il TCP a capire qual è lo stato della rete?
I sintomi che il livello TCP osserva sono:
- L'eventuale **perdita di pacchetti**
- Gli **ACK che arrivano in ritardo**: se c'è un ritardo è possibile che un segmento abbia trovato quale problema durante la strada
<br>

## Controllo della congestione TCP Tahoe
- Per limitare il formarsi di code nei router, i trasmettitori utilizzano una **congestion window (cgwd) di dimensioni variabili**
- implementa **AIMD (Addictive Increase, Multiplicate Decrease)**

**NB. AIMD**: se tu pensi che la rete sia in grado di supportare una maggiore quantità di traffico, puoi **aumentare linearmente**, la quantità di dati da trasmettere. Se noti congestione però, devi **ridurre drasticamente** la trasmissione.*

![[congestion-window-tcp.png]]

### Tahoe: Congestion Window (cgwd)
La **congestion window** rappresenta il **numero massimo di dati che si possono trasmettere senza ricevere un ACK**, e quindi **senza causare una congestione**.

*Questo valore viene gestito in questo modo:*
1. Il **valore iniziale è pari alla dimensione del massimo segmento usato nella connessione**
2. **Ogni volta che un ACK** torna indietro in tempo: la **finestra raddoppia fino a un valore threshold** (inizialmente pari a **64.000byte**), la crescità è quindi **ESPONENZIALE**
3. **Passato il valore di soglia**, per ogni ACK che si riceve, **la cgwd aumenta LINEARMENTE di 1**
4. Quando si **verifica un timeout** per un segmento:
	1. **Il valore di soglia viene impostato a METÀ della dimensione della congestion window**
	2. La **dimensione della cgwd** viene impostata alla quella del massimo segmento usato nella connessione (**valore iniziale**)

**NB1.** La crescita è prima esponenziale e poi lineare.
**NB2.** Il **valore di soglia** rappresenta il momento in cui la cgwd comincia a crescere lentamente (linearmente).
<br>

### TCP Tahoe: Slow start
*All'apertura della connessione, il TCP ha una comunicazione stop&wait e non abbiamo idea di come sia il percorso tra la sorgente e la destinazione. Quindi, finchè va tutto bene, cresciamo rapidamente.*

La **fase di Slow Start ha l'obiettivo di ritornare il valore ottimale della congestion window**.

**Si parte da valore basso** -> se va bene, si cresce esponenzialmente -> poi crescita lenta -> quando si dimezza il valore di soglia -> abbiamo di nuovo un Slow Start
<br>

### TCP Tahoe: Fast recovery
I **timeout (sintomo di congestione) sono impostati con valori abbastanza alti**. Per cui, piuttosto che aspettarne uno, **conviene cercare di capire prima se ci sono dei problemi nella comunicazione**: gli **ACK DUPLICATI sono interpretati come sintomi di una possibile perdità di pacchetti**.

*Sarebbe anomalo ricevere tante volte lo stesso ACK, per cui:*
**Se l'entità TCP riceve per 4 volte consecutive lo stesso ACK**:
- si considera il segmento perso e lo **si ritrasmette**
- si **DIMEZZA il valore di soglia** e si **reimposta la cgwd, ripartendo con la fase di SLOW START**
<br>

### TCP Reno
- In caso di timer scaduto, si comporta come Tahoe.
- **Se l'entità TCP riceve per 4 volte consecutive lo stesso ACK**:
	- si considera il segmento perso e lo **si ritrasmette** (senza aspettare il timeout)
	- si **DIMEZZA il valore di soglia** e si **reimposta la cgwd al valore di soglia attuale**
	- si inizia con una **FASE di INCREMENTO ADDITIVO**, dove la **cgwd cresce di un segmento ad ogni ACK ricevuto**

**NB.** A differenza del Tahoe, non si riparte con una fase di slow start.
<br>

### ECN, Explicit Congestion Notification
- Richiede modifiche sia al TCP che all'IP
- Il router deve supportare questa tecnologia

Ci sono 2 flag nell'intestazione, in apertura di connessione, (**CWR** e **ECE**).

Se un router del percorso ha i **buffer riempiti oltre a una certa soglia** (e NON quando è pieno, altrimenti sarebbe troppo tardi): **manda una notifica all'entità TCP ricevente**. 
Chi riceve questa notifica: **imposta a 1 il flag ECE del segmento di risposta**. Il TCP mittente comunica l'avvenuta ricezione di ECE impostando a 1 CWR.
Viene quindi applicato un meccanismo di riduzione della congestione.