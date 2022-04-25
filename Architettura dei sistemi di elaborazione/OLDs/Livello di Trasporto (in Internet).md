# Livello di Trasporto (in Internet)
*Per il livello di trasporto non affronteremo le problematiche deli livello di trasporto in generale, parleremo direttamente del livello di trasporto in internet (UDP e TCP).*

![[vedi slide]]

## TSAP: Transport Service Access Point
Rappresenta l'indirizzo al livello di trasporto.
TASP sorgente : identifica in modo univoco chi ha generato i dati di un segmento
TASP destinatario:

IPaddress:port number

Quando parliamo di interfaccia tra livello di trasporto e livello di applicazione, non si parla di progettisti di rete ma di progettisti di applicazione. (es. applicazione che deve funzionare in rete senza ausilio di altre applicazioni, deve usare interfaccia tra livello di trasporto e applicazione)

Le applicazioni di rete sono progettate secondo un'organizzazione **client-server**, es. usiamo il server web, il server posta, server ftp. (aclune applicazioni però come bitTorrent sono peer-to-peer). 
La regola è che il **server deve partire per primo** e mettersi in ascolto di una chiamata del client, il client cerca la connessione col server.
Chi parte per primo sceglie anche la porta in cui mettersi in ascolto

*NB.Il client fa delle richieste abbastanza semplici, il server risponde con pagine web, immagini, ... (SOLITAMENTE)*

*NB.Se si parla di applicazioni peer-to-peer: dentro queste applicazioni sono sviluppate realizzando sia un client , sia un server. Quest'ultimo rimane in ascolto cosicchè altri utenti peer-to-peer vengano a cercare contenuti tra noi.*

Le applicazioni di tipo client quando instaurano la connessione devono specificare a quale indirizzo e porta devono collegarsi; viene assegnata una porta **effimera**

## Primitive di definizione...
Come le applicazioni possono utilizzare i servizi della rete?
L'interfaccia standard tra applicazioni e i servizi di trasporto si chiama **socket**.
I socket di berkelety vengono utilizzate tramite un'insieme di primitive (cioè delle chiamate al sistema operativo), che somigliano a delle chiamate di funzione di C.

Le applicazioni non possono interagire direttamente con l'hardware, devono utilizzare delle chiamate al sistema operativo. 

**NB:** Nei computer abbiamo diversi tipi di memoria, la grande distinzione è quella tra memoria centrale e memoria di massa. Nella RAM vengono caricati i programmi per essere eseguiti.
In un computer è importante avere tanta memoria perchè sistema operativo e programmi vengono caricati in memoria, se c'è bisogno di più spazio bisogna togliere qualcosa dalla memoria RAM e scriverlo su disco.
La memoria di massa è organizzata in una struttura di file (le cartelle sono dei file speciali, che contengono un elenco di altri file), i linguaggi di programmazione devono avere la possibilità di interagire con i file, es. aprire i file in lettura o scrittura,... . 
Tutto questo per dire:


L'applicazione vede il socker come una coppia di **stream** (file), uno aperto in scrittura e uno aperto in lettura.
Scrivere in un socket corrisponde a inviare dati in rete, leggere dal socket corrispondente e ricevere dati dalla rete.

I socket di berkley consentono di trasformare le operazioni di invio dati in operazioni di scrittura su file, e l'operazione di ricezione di dati diventa un'operazione di lettura file.
In realtà questa "invenzione" fa capire bene come tutta la complessità di gestione della rete sia a carico dei livelli di trasporto, rete, datalink. Il livello applicativo ha già tutto pronto.

Nella comunicazione in rete client e server hanno comportamenti diversi:
- ...
- ...
- Aperta la connessione, alle operazioni di scrittura del 
NB. A ogni operazione di scrittura da un lato deve corrispondere un'operazione di lettura dall'altro lato.

## Principali primitive
- accept : per accettare una richiesta di connessione
- socket : crea un punto di comunicazione
- read, write : ricevono e inviano dati

## Struttura delle applicazioni
Comunicazione orientata alla connessione (TCP):
- ...
- ...
Quando si è concluso si usa una primitiva **close**

Counicazione NON orientata alla connessione (UDP):
- ...
- ...

es. il client dns fa una richiesta al server, il server risponde mandando la risoluzione dell'indirizzo. Client invia -> Server risponde , Server invia -> Client risponde, termina connessione.

## Comunicazione client-server con TCP
![[questo dal punto di vista dell'applicazione]]

Client manda la connect, manda qualcosa, il server riceve e risponde,...

Le applicazioni normalmente seguono un paradigma client-server.

In questo caso l'applicazione server deve partire per prima e mettersi in ascolto per aspettare di ricevere una richiesta di connessione dal lato client. 

NB. Le applicazioni peer-to-peer normalmente inglobano in se sia il comportamento client che quello server

NB. Interfaccia (vedi definizione su "Introduzione alle reti") SOCKET in Internet è tra il livello di Applicazione e di Trasporto, questa interfacca è composta da un insieme di primitive che somigliano a delle funzioni. Però la primitiva è all'interno del codice del sistema operativo.
L'interfaccia socket racchiude le primitive specifiche per utilizzare il servizio TCP.

NB. L'interfaccia socket: il socket viene visto come una coppia di file, uno aperto in scrittura e uno aperto il lettura. Con le stesse operazioni di scrittura e lettura che usiamo su disco, riusciamo a mandare e ricevere dati in rete.
(Tutta la complessità della trasmissione è già stata risolta a livello di Rete)

L'applicazione server poi deve aprire il server e utilizzare delle primitive per mettersi in ascolto in una specifica porta

Il server poi con una primitiva connect, specificando un indirizzo IP e una porta avvia la connessione.

NB. Se la connect parte prima che il server sia in ascolto, questa fallisce

Successivamente, quando uno trasmette, l'altro riceve e viceversa. Ovviamente l'operazione di scambio dati deve ripetersi più volte.

# UDP: User Datagram Protocol
UDP è un protocollo datagram (cioè SENZA connessione e NON affidabile)

UDP non fa nulla, l'applicazione non può usare direttamente i servizi di rete, deve per forza utilizzare un layer di trasporto

UDP è leggerissimo

L'UDP si usa in applicazioni che hanno caratterisitche particolari:
1. Applcazioni che prevedono singoli brevi scambi, es DNS (Domain Name System). DNS è un sistema, ci sono i nomi dns, i server dns e il protocollo dns, il protocollo è quello con cui i client chiedono la risoluzione di un nome. C'è quindi una domanda breve e una risposta altrettando breve.
In questo caso sarebbe superfluo utilizzare il TCP e aprire una connessione,... ci sarebbe un overhead eccessivo.

NB. La connessione è utile se mando una sequenza di segmenti, ma se io mando una sola domanda e ricevo una sola risposta, è inutile.
Sarebbe utile l'affidabilità, ma col dns, ad esempio, viene gestito dall'applicazione (e non dal livello di trasporto)

2. L'overhead della gestione della connessione provoca un rallettamento che non è accettabile dal punto di vista dell'applicazione. Un esempio è VoIP, dove la velocità è preferibile alla perdita di dati.

NB. Impiantare la gestione della perdita d'informazioni diminuisce la velocità con cui vengono ricevuti i dati. Come nel VoIP (o nello streaming video che non avviene tramite browser)

Il funzionamento è semplice, i messaggi dell'applicazione vengono semplicemente inseriti in un segmento e passati a livello di rete.
La comunicazione tra due applicazioni...

## Formato intestazione UDP
Il segmento udp ha una struttura molto semplice, al messaggio viene aggiunto una intestazione UDP formata da porta sorgente, porta destinazione , lunghezza e checksum
- ...
- ...
- ...
- ...

## TCP
Rispetto al udp svolge un lavoro compless

- Progettato per fornire (al livello superiore) un flusso di byte affidabile, da sorgente a destinazione, su una rete non affidabile.
- Protocollo affidabile e orientato alla connessione
- Il protocollo è full-duplex: contemporaneamente sarà gestita la trasmissione e la ricezione In più con gestione di ACK e di controllo del flusso: quindi una parte della connessione non può trasmettere all'altra più dati di quanti quest'ultima possa riceverne in quel momento.
- Il TCP in internet si occupa anche del **controllo della congestione**, 

### Funzionamento:
- Si ricevono i dati dall'applicazione
- I dati vengono organizzati in segmenti (dimensione massima 64Kbyte meno la dimensione di un'intestazione IP, tipicamente circa 1500byte)
- Il segmento viene consegnato al livello di rete, eventualmente ritrasmettendoli se necessario: dovrà quindi tenere in memoria tutti i pacchetti di cui non ha ancora ricevuto conferma
- Contemporaneamente, riceve segmenti dal livello di rete, eventualmente rimettendoli in ordine, eliminando buchi e doppioni
- Consegna i dati **in ordine**(rispetto a come sono stati trasmessi) al livello applicazione.

### Caratteristiche più importanti:
Il TCP usa una politica sliding windows, mentre nei protocolli datalink si numerano i frame, nel TCP non si numerano i segmenti ma **virtualmente** i byte all'interno di un segmento.
I numeri sono a 32 bit (non sono quindi infiniti, ad un certo punto vengono riutilizzati)

- Sliding windows di tipo go-back-n o selective-repeat (con timeout), cioè se non ricevo riscontro entro un certo tempo, si ritrasmette

### Formato intestazione TCP
- Porta sorgente
- Porta destinazione
- **Sequencec number: rappresenta IDEALMENTE il numero del primo byte del payload**, es. se qui c'è 500 e i dati da trasmettere sono 1000byte, questi 1000byte sono virtualmente numerati da 500 a 1499
- **ACK number: rappresenta il numero di sequenza del prossimo segmento che mi aspetto di ricevere**
- Lunghezza dell'intestazione: espresso in longword
- Checksum: un controllo sull'intestazione
- Windows size: rappresenta la dimensione della finestra di ricezione, comunica quanti byte, in quel momento, è in grado di ricevere. es. se è di 500 e la controparte deve trasmattere al massimo 500
	Il windows cambia:
	- In funzione dei dati che io invio
	- In funzione delle operazioni di lettura che avvengono al livello superiore (di applicazione)
- Urg point: se in questo segmento sono contenuti dei byte urgente, urgent point specifica il numero virtuale da cui partono questi dati. 
- Urg: se uguale a 1, nel segmento ci sono dati urgenti
- Altri flag: ACK, ... normalmente utilizzati nella gestione della connessione

## Attivazione della connessione TCP
Ripasso: il server apre il socket e si mette in ascolto, il server è li che sta aspettando una richiesta di connessione, il client invece apre il socket e fa direttamente una connect(), quando viene fatto ciò l'unità TCP del client manda dall'altra parte un segmento TCP che ha impostato ad uno il FLAG SEQ = 1 e FLACK ACK = 0

Nel TCP il valore di sequenza NON parte da 0 ma da xxx 

Chi apre la connessione dive il numero iniziale di sequenza, ma non può sapere da che numero partirà l'altro, per cui nel primo segmento SYN questa informazione non eseiste, quindi il flag ACK sarà 0

A destinazione: se c'è un'applicazione in ascolto si risponde con segmento con i flag SYN e ACK entrambi impostati a 1, altrimenti si manda un flag RST uguale a 1 per dire che non c'è nulla pronto a ricevere dati e fa crollare la connessione.

A questo punto il client può mandare i dati con ACK = y+1 e SEQ = x+1

![[vedi schema]]

# ---- 04 febbraio ----

### RIPASSO
TCP è un protocollo affidabile e orientato alla connessione che offre come servizio la possibilità di ricevere un flusso di byte ordinati, in modo analogo a quello che potrebbe avvenire su una connessione fisica, ma qui avviene su qualsiasi nodo della rete.

Il protocollo è **bidirezionale** e **full-duplex**, cioè le informazioni viaggiano in entrambe le direzioni. (entrambe trasmettono e ricevono dati, in più su **ogni connessione**, ci possono essere più connessioni TCP )

Il fatto che sia full-duplex rende complesso capire il comportamento del TCP

**NB**. Negli esempi noi vedremo però una comunicazione **simplex**, da una parte viaggiano informazioni e ACK e dall'altra parte arrivano le risposte.

Per capire il funzionamento del protocollo guardiano l'intestazione, dove troviamo;
- numero variabile di longword (prime 5 obbligatorie)
- TCP header lenght : specifica la lunghezza in longword dell'intestazione
- Checksum: per verificare l'integrità dell'intestazione
- Window Size: rappresenta la **dimensione della finestra di ricezione**, ed è utilizzato per il controllo di flusso. 
- Sequence number: numero di sequenza del primo byte contenuto nel segmento
- ACK number: ...
- Flag ACK: impostato ad 1 significa che il contenuto del campo ACK number è valido
- Flag RST: utilizzato quando si verifica un problema
- Flag SYN: usato in **apertura della connessione**
- Flag FIN: usato in **chiusura della connessione**
- Flag PSH: serve per indicare che questi dati andrebbero spediti e consegnati il prima possibile all'applicazione (diverso però dall'urgent)

NB. Un messaggio GET da browser viene inviato via PUSH

### Gestione ritardatari duplicati
Il primo che parte il server ma il primo che manda un segmento dall'altra parte è il client.

Col livello di trasporto: bisogna risolvere dei problemi dei problemi di rete, quindi possiamo immaginare un'analogia livello rete+trasporto e livello fisico+datalink . C'è una differenza però:
Il livello datalink opera sul livello fisico, bisogna gestire la comunicazione tra 2 stazioni, il frame o arriva o non arriva. Nel livello di trasporto invece posso aprire una connessione con un nodo molto vicino o molto distante, nel secondo caso i pacchetti che giarano per la rete possono essere memorizzati in dei buffer dei router.

A differenza del livello datalink, un segmento che non è ancora arrivato potrebbe essere semplicemente in ritardo, bisogna quindi **evitare di fare confuzione tra un segmento e un ritardatario duplicato**

![[vedi schema slide]]

*Se chi ha mandato il segmento SYN non riceve in tempo utile una risposta lo rimanda, potrebbe succedere però che la richiesta precedente arriva molto tempo dopo, per chi la riceve sembra leggittima, NON ha modo per sapere che quella è una vecchia richiesta. Questo è un **RITARDATARIO DUPLICATO**, poichè arrivato in ritardo e come copia di un altra richiesta.*

Per evitare confusione bisogna fare in modo che i numeri iniziali di sequenza sia univoco in un determinato intervallo di tempo, per evitare confusione tra un segmento la cui richiesta è andata a buon fine e tra un ritardatario duplicato.

NB. Abbiamo a disposizione però numeri fino a 32 bit, arrivati al numero massimo si torna a 0. **NON ho numeri iniziali illimitati**, è importante garantire che il numero iniziale di sequenza x possa ritornare dopo 2 volte il tempo di vita massimo dei segmenti.

Per garantire la correttezza dell'apertura della connessione TCP, dobbiamo essere sicuro che i segmenti arrivino in un determinato lasso di tempo, altrimenti non riusciremmo più a distingere richieste di apertura di connessione valide o da scartare.

### Numero iniziale di sequenza ISN
Come viene preso l'ISN? 
**ISN generator è un contatore a 32bit che si incrementa gradualmente di 1** . 
Quando arriva a (2^32) - 1 , riparta da 0. Il tempo da 0 allo 0 successivo è di circa 4.55 , garantendo quindi la condizione di riusabilità: dobbiamo garantire che quando un numero si ripresenta sia passato almeno il doppio del tempo di vita massimo del segmento (che aveva stesso numero)

L'uso degli ISN generator ci garantisce che il numero x potrà essere utilizzato per aprire un'altra richiesta di connessione, MA dopo un intervallo di tempo.



## Stati di connessione TCP
![[schema stati connessione tcp]]

Questo disegno è un **diagramma di transizione degli stati**.

L'entità TCP la posso vedere come un sistema di tipo ??? . 
Uno stato è una situazione in cui si trova il nostro automa, l'entità TCP si può trovare in uno di questi stati (i nodi del diagramma) mentre le frecce sono le TRANSIZIONI, ognuna è marcata da una coppia input/output : il passaggio dello stato avviene perchè il sistema è stato solleccitato da un input, e come risposta produce un output.

L'evento **LISTEN** permette il passaggio da stato chiuso ad ascolto, il **-** vuol dire che dall'altra parte non viene inviato alcun segmento

Le transizioni di stato possono dipendere da:
- eventi di protocollo: segmenti che si ricevono dall'altra parte
- eventi di interfaccia: interfaccia che fa qualcosa

Rappresentazione apertura della connessione tramite diagramma di stati:

Server: Se sono nello stato LISTEN e ricevo un segmento SYN, devo rispondere con un segmento SYN+ACK e mi porto nello stato SYN RECEIVED.

Client: Dalla parte del client invece si parte con una CONNECT e l'entità TCP va allo stato SYN SENT e rimane li finche non riceve un SYN+ACK


NB. È molto più facile progettare un software che deve fare queste operazioni, se si lavora con un modello di grafo di rappresentazione degli stati

### RIPASSO, Apertura della Connessione TCP
Utilizziamo 3 PDU invece delle sole 2 del livello datalink, c'è quindi un passaggio in più che serve per poter gestire eventuali problemi di richieste ridardatarie duplicate.

I contatori partono da valori che non sono 0 e se li devono comunicare.

**NB**. Client e server sono le due applicationi, ma lo scambio avviene tra le 2 entità TCP (quella del client e quella del server)

<br>

Il caso peggiore: si perde il primo segmento e la sua risposta.

## Chiusura della connessione TCP
*Se io mando una richiesta di chiusura della connessione e l'altra parte mi risponde con un OK, il mandante chiude la connessione ma il "secondo lato" non ha conferma di chiusura della connessione. -> Questo problema non si può risolvere, sono stati integrati dei timeout*

La connessione è full-duplex, il funzionamento normale sarebbe quello per cui ciascun lato chiude la sua connessione

#### Chiusura connessione, 4 segmenti

![[immagine chiusura connessione tcp (4 segmenti)]]

*In realtà potrebbe anche il server a decidere di chiudere la connessione*

Chi vuole chiudere la connessione manda un segmento FIN, l'altra parte manda il segmento di ACK. E il primo lo riceve. **In questo punto però il secondo può ancora inviare dati (anche nell ACK)**. Quando anche l'altra parte decide di chiudere la connessione, avviene lo stesso processo

Si identifica con una chiusura a 4 segmenti poichè : FIN -> ACK FIN->ACK

#### Chiusura connessione , 3 segmenti
Entrambe le parti decidono di chiudere insieme la connessione

<br>
<br>
<br>

Quando si manda un segmento FIN e si riceve un ACK, a questo punto è possibile continuare a ricevere dati. Per questo si implementa un timeout, dopo avere deciso di chiudere la connessione, per permettere di ricevere anche gli ultimi pacchetti. ??????

NB. Un segmento spedito dopo potrebbe arrivare prima di altri

<br>
<br>

**ACTIVE CLOSE:** ...

**PASSIVE CLOSE:** ...

*Nella slide "Stati di connessione TCP"*

##### PER IL COMPITO:
*Bisogna conoscere i protocolli di apertura e di chiusura a 3 e 4 segmenti, da questi bisogna essere in grado di ricostruire il diagramma degli stati (Slide Stati Connessione TCP). È Importante sapere i collegamenti (e come avvengono) con linea continua, NON quelli a linea tratteggiata


## Controllo di Flusso TCP
Serve per far si che chi trasmette dei dati non ne trasmetta di più di quanti possa riceverne l'altra parte.

**NB**. In queste slide gli schemi rappresentano una comunicazione **simplex**. Nella realtà però è **duplex (bidirezionale)**, entrambe le parti trasmettono e ricevono dati e ack.

Come facciamo a sapere quanto grande è la finestra di ricezione dell'altra parte?
Lo sappiamo grazie al segmento SYN che ci siamo scambiati a inizio della connessione.

![[immagine slide 26]]

*Spiegazione dell'immagine:*

Il mittente manda 2Kbyte con numero di sequenza = 0, 
la risposta per quanto riguarda il controllo del flusso: ACK = 2048 , nuova dimensione del windows size = 2048.
Se adesso il mittente manda 2048, il ricevente avrà il buffer completamente occupati, quindi manderà un ACK con ack=4096 e win=0. 
Il mittente non potrà quindi più spedire dati.
Appena il ricevente avrà di nuovo il buffer libero, manderà all'altro lato un segmento con la nuova finestra di ricezione

NB. I numeri di sequenza e di ACK (cioè i segmenti dati) hanno come numero: il numero dei dati inviati + num precedente . Solo i segmeni iniziali, come SYN hanno num di seq = 1


## TCP : Controllo della congestione
Il TCP ha una politica di ristrasmissione, quindi aspetta le conferme dei segmenti che sta trasmettendo, se non arriva in tempo utile, il segmento viene rimandato. Il tcp manda il segmento al livello di rete, che si limita ad incapsularlo in un pacchetto.

Se si verifica un fenomeno di congestione, e i router cominciano a scartare i pacchetti: vengono spedite tante copie dello stesso pacchetto. 
Si rischia quindi che ci siano in giro tanti pacchetti, ma molti sono duplicati, non più accettati, ... . Questo fenomeno continua ad autoalimentarsi.

Pacchetti che sono ancora utili si chiamano XXX (gu...)

Internet è nata in un contesto militare, poi universitario, ecc. . Col la crescita della rete si sono verificati i primi fenomeni di congestione.
Van Jacobson ha escogitato un **sistema per introdurre nel TCP il controllo della congestione**, lasciando **però inalterata la struttura dei router**.
Viene applicato quindi a livello di Trasporto.

Il sistema di controllo, prima con la TCP Tahoe, è basato su finestre scrorrevoli a dimensioni variabili.

NB. La finestra di trasmissione rappresenta la quantità di dati che posso trasmettere prima di ricevere l'ACK.

*AIMD : se tu pensi che la rete sia in grado di supportare una maggiore quantità di traffico, puoi aumentare **linearmente**, la quantità di dati da trasmettere. Se noti congestione però, devi ridurre drasticamente la trasmissione.*

##### Come fa il TCP ad avere informazioni su come sta funzionando la rete?
I sintomi che il TCP osserva sono:
- perdità di pacchetti
- ACK che arrivano in ritardo, perchè se c'è un ritardo è possibile che un segmento abbia trovato qualche problema strada facendo

![[slide pagina 30]]

**TCP Congestion windows è un parametro**, numero massimo di dati che si possono trasmettere senza ricevere un ACK. Per ogni ACK che si riceve, si incrementa di 2 in numero della congestion windows. Questo significa che a ogni RTT la dimensione della congestion windows raddoppia.

Raggiunto un valore di soglia (es. 32 kbyte), da quel momento in poi la crescita della congestion window è **lineare**, quindi per ogni ACK che si riceve, si incrementa di 1 la congestion window.

-> **La crescita è quindi prima esponenziale e poi lineare** 

**NB**: Ricordiamo però che se la congestion windows è 32K ma la controparte mi ha comunicato una finestra di ricezione di 10K, posso mandare al massimo 10K

NB. Se settato a 1 (congestion windows) si può trasmettere <=> ricevere massimo 1 segmento per volta.

**RTT:**

**Valore di Soglia**: rappresenta il momento in cui la congestion window comincia a crescere **lentamente** poichè sta crescendo **LINERMENTE**.

#### TCP Slow Start
All'inizio la connessione TCP ha una comunicazione stop & wait: apriamo una connessione, non abbiamo idea di come sia un percorso tra la sorgente e la destinazione. Finchè va tutto bene però cresciamo rapidamente.

NB. un router potrebbe essere in difficoltà poichè al centro di tanti collegamenti dovuti a tante connessioni del livello di trasporto. Sono quindi **sovraccarichi**. 

La fase di Slow Start ha l'obiettivo di ritornare il valore ottimale della congestion window

Si parte da valore basso -> se va bene, si cresce esponenzialmente -> poi crescita lenta -> quando si dimezza il valore di soglia -> abbiamo di nuovo un Slow Start

#### TCP Fast Recovery (TCP Tahoe)
I timeout sono impostati abbastanza alti. Molte volte quindi non è molto conveniente attendere i timeout, Jacobson ha quindi messo a punto questo meccanismo:

**Piuttosto che aspettare un timeout, proviamo a capire prima se ci sono dei problemi.** Cerchiamo quindi di avere un segnale prima:

Ci sono alcuni sintomi:
**ACK duplicati**, da soli però potrebbero NON essere sintomo di perdita di dati.
Sarebbe però anomalo ricevere tante volte lo stesso ACK, **se quindi l'entità TCP riceve per 4 volte consecutive lo stesso numero di ACK**, si **considera** che il **segmento** sia andato **PERSO** **e lo si ritrasmette**.

In più: si **dimezza il valore di soglia** e si **reimposta il valore di congestion windows** e **si riparte con una fase di SLOW START**. 

## TCP Reno
A differenza del TCP Tahoe. Al 4o ACK con stesso numero di ACK non si riparte con una fase di slow start ma con **INCREMENTO ADDITIVO**, cioè la congestion windows cresce di **un segmento** a ogni ACK ricevuto.

NB. **In caso di timer scaduto invece, si comporta come Tahoe**

## ECN, Explicit Congestion Notification
Bisogna che sia rupportata dal router.

Ci sono 2 flag nell'intestazione, in apertura di connessione, (CWR e ECE).
Se un router del percorso ha i **buffer riempiti oltre a una certa soglia** (e NON quando è pieno, altrimenti sarebbe troppo tardi): **manda una notifica all'entità TCP ricevente**, chi riceve questa notifica: imposta a 1 il flag ECE del segmento di risposta. Il TCP mittente comunica l'avvenuta ricezione di ECE impostando a 1 CWR.
Viene quindi applicato un meccanismo di riduzione della congestione.

<br>
<br>
<br>

## RIPASSO: es tcp dell'esame
![[farsi dare lo schema dell'es risolto da qualcuno]]

