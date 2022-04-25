# Livello di Rete (in generale)
Lo scopo del livello di rete è quello di **controllare l'intero movimento dei pacchetti dalla sorgente alla destinazione**, che NON sono direttamente collegate, **attraversando** tanti sistemi intermedi (**router**) della subnet di comunicazione quanti è necessario.

*Differisce dal livello Data Link in quanto in quest'ultimo le informazioni vengono trasmesse da un estremo all'altro del solo canale fisico.*

Nel collegamento tra sorgente e destinazione remote i dati vengono suddivisi in **pacchetti** depositati in dei **buffer di ingresso**, l'entità di Livello di Rete prende in esame tutti i pacchetti in ingresso e decide dove inoltrarli:

*Per questo procedimento di vuole tempo: è quindi importante che i pacchetti NON rimangano a lungo nel router.*

### Compiti del Livello di Rete
- ((( Inoltrare i pacchetti lungo la subnet di comunicazione (**forwarding**) )))
- Scegliere ogni volta il cammino migliore, instradamento (**routing**)
- **Controllare la congestione** del traffico
- Inteconnettere reti diverse (**internetworking**)

![[schema-livello-rete]]

### Router
Il router ha delle linee di ingresso e di uscita.

Il router riceve i pacchetti in arrivo dalle varie linee, li esamina uno ad uno, e decide su quale linea inoltrarlo: questo avviene principalmente grazie a delle **tabella di routing**.

**NB**. **Tabella di Routing**: una tabella presente nel router che indica, per ogni possibile destinazione, quale linea di uscita utilizzare.

![[esempio tabella di routing]]

### Routing: Statico e Dinamico
Il routing può essere:
- **STATICO**: le **tabelle sono definite offline** e caricate nel router all'accensione
- **DINAMICO**: i **router stessi**, scambiandosi informazioni, **calcolano periodicamente le proprie tabelle di routing** (e quindi determinare i percorsi), in modo da tener conto di eventuali varizioni nella struttura della rete.

![[schema routing statico e dinamico]]

**NB**. **Routing** e **Forwarding**
**Routing**: determinare i percorsi migliori
**Forwarding**: prendere un pacchetto e spostarlo da un buffer in ingresso ad uno d'uscita tramite le tabelle di inoltro

*Normalmente si utilizza un mix di routing statici (nel collegamento di singole organizzazioni alla rete) e dinamici (nell'infrastruttura che collega i provider).*

### Operatività del router
Il router deve avere almeno 2 collegamenti ad Internet e deve:
1. Prendere ogni pacchetto dal buffer in ingresso
2. Esaminarlo per vedere dove è diretto
3. Consultare la propria tabella di routing
4. Depositarlo nel buffer di uscita corretto

### Tipi di servizio offerti al Livello Di Trasporto
Il **tipo di servizio offerto dal Livello di Rete al Livello di Trasporto** può essere:
- Servizio **con connessione e con riscontro** (**Circuiti Virtuali**)
- Servizio **senza connessione e senza riscontro** (**Servizio Datagram**), che è quello offerto dal **Protocollo IP**

![[schema]]

## Circuito virtuale
Servizio **con connessione e con riscontro**.

Tutti i **pacchetti sono instradati attraverso un circuito virtuale**, cioè un **percorso definito** (tramite le tabelle di routing) **al momento della connessione**, che rimane valido per tutta la durata della connessione stessa.

Tutti **i router lungo il circuito ricordano**, in un'apposita struttura dati (**tabella dei circuiti virtuali**), **la parte di loro competenza del percorso**, e cioè quale linea in entrata e quale in uscita sono assegnate al circuito.

![[schema]]

**Spiegazione:**
*A intende aprire una connessione verso B, 1 guarderà le tabelle di instradamento e vedrà che la strada corretta è verso 2, 2 si segnerà che deve andare verso 3, 3 concluderà con B.*

##### Funzionamento
L'inoltro viene fatto basandosi sulle tabelle dei circuiti virtuali, quando la connessione viene chiusa il circuito scompare definitivamente.

I **pacchetti arrivano a destinazione nello stesso ordine con cui sono stati trasmessi** e in più sappiamo che sono stiti recapitati, dato che **c'è riscontro (ACK)**.

##### Vantaggi e svantaggi
**Vantaggi**: 
- Quando si apre la connessione c'è una **fase di negoziazione**, si possono stabilire il tipo di traffico, la velocità massima di trasferimento,...
- Con la fase di negoziazione è possibile implementare facilmente delle **politiche di controllo della congestione**.
**Svantaggi**: se cade un collegamento, cade l'intera connessione.

**NB**. Quando la rete offre un circuito virtuale, i pacchetti NON sono identificati da indirizzi di destinazione ma dal circuito virtuale.

## Servizio Datagram
Servizio **senza connessione e senza riscontro**.

I pacchetti, detti **datagram**, seguono **percorsi diversi non stabiliti a priori**. Ogni **datagram** deve **contenere l'indirizzo completo del destinatario**.

![[schema]]

**Spiegazione:**
*3 fa un percorso diverso da 1 e 2, può succedere quindi che arrivi prima di 1,2 anche se spedito dopo.*

##### Funzionamento
I router attraverso i quali passa il pacchetto determinano di volta in volta come inoltrarlo basandosi sulle tabelle di routing.

##### Vantaggi e svantaggi
**Vantaggi**:
- Se un router intermedio cade, il pacchetto può seguire un percorso alternativo
**Svantaggi**:
- È **possibile che i pacchetti NON arrivino nell'ordine giusto**
- Un **pacchetto può andare perso** e i dispositivi non se ne accorgerebbero
- È più **difficile controllare la congestione della rete**

## Situazione di congestione della rete
Ogni pacchetto rimane nel router per un certo periodo di tempo, "ospitato" all'interno di un buffer.

**Situazione ideale:**
I pacchetti che vengono trasmessi sono tutti consegnati senza saturare la rete.

##### Congestione:
Una linea di uscita è troppo lenta a smaltire il traffico in quella direzione: il buffer di uscita non si svuota abbastanza rapidamente e la relativa coda si riempie.

*Se la situazione dura a lungo:*

Il router non riesce nemmeno a inoltrare i pacchetti nella linea di uscita.
I pacchetti però devono rimanere memorizzati nelle code di ingresso, che a sua volta si riempiono. Quando le entrambe le code si riempiono, il router inizia a **scartare i pacchetti** in arrivo, che vanno persi.

*I pacchetti persi vengono ritrasmessi (a livello 3 o 4) e questo contribuisce ad aumentare il traffico della rete.*

**NB1**. Ad un certo punto nella storia di Internet si verificavano continuamente congestioni: fu così necessario implementare determinati **algoritmi di controllo della congestione**, questi vengono solitamente implementati al Livello di Trasporto.
**NB2**. In generale la congestione va controllata al livello 3 e 4.

## Algoritmi di routing
La funzione principale del Livello di Rete è l'**instradamento** dei pacchetti, tipicamente facendo fare loro molto **salti** (o **hop**) da un router ad un altro.

*Recentemente si è iniziato a separare i 2 concetti di routing e forwarding.*

Il routing (instradamento) si occupa di capire quali sono le destinazioni raggiungibili e lungo quali percorsi.
Le **tabelle di routing sono prodotte attraverso degli algortmi di routing**, che possono essere statici o dinamici.

### Metriche degli algoritmi di routing
I percorsi definiti dalle tabelle di routing devono essere il più diretti / brevi possibili/...

Per realizzare un buon algoritmo di routing serve una **metrica di riferimento**, alcuni esempi di questa sono:
- **Minimizzazione del tempo** medio di recapito del pacchetto
- **Percorso più breve** in termini di router attraversati (**cammino minimo**)
- Percorso con **canali a banda maggiore**
- ...

Solitamente si sceglie come parametro quelli di **minimizzare il tempo**.

Il risultato finale del processo di routing è la creazione di una serie di informazioni locali (es. tabella di routing) in ognuno dei nodi della rete che specificano la direzione per ogni possibile destinazione.

##### Forwarding
L'inoltro (**forwarding**) avviene in modo indipendente su ciascun nodo utilizzando le informazioni prodotte dal processo di routing (es. tabelle di routing IP) e consiste nell'inoltro dei pacchetti provenienti da ciascuna linea di ingresso verso la linea di uscita corretta.

Nel momento in cui si fa il forwarding i router guardano solo la loro tabella, **non hanno una conoscenza globale della rete**, il processo deve essere quindi **snello**.

**NB**. Entrambi i processi, routing e forwarding, sono necessari per l'operatività di una rete.

## Caratteristiche degli algoritmi di routing
- **SEMPLICITÀ**
	- Implementazione **snella**, con minor possibilità di errori
	- **Utilizzo limitato di tempo e risorse** di elaborazione (CPU, Memoria)
- **ROBUSTEZZA e ADATTABILITÀ**
	- L'algoritmo deve **funzionare su una topologia di rete generica** e senza alcun vincolo sulla stessa
	- L'algoritmo deve **supportare cambiamenti di topologia** senza interrompere il funzionamento della rete (quando siamo su routing dinamico)
		- **Fault Detection**: capacità di accorgersi che qualcosa non sta funzionando
		- **Autostabilizzazione**: se qualcosa non va nella rete, nel minor tempo possibile, la rete deve trovare dei nuovi percorsi alternativi
- **OTTIMALITÀ** nella scelta dei cammini, rispetto alle metriche prescelte
- **STABILITÀ**
	La rete deve raggiungere uno stato di stabilità dove il routing non deve cambiare a meno che non ci siano variazioni nei costi / topologia
- **EQUITÀ**
	**NON devono esistere nodi "trascurati" o "danneggiati"** dalla scelta dei percorsi di instradamento
	
## Algoritmo di Dijkstra
È un algoritmo basato sul **cammino minimo**.

Inizialmente tutti i nodi (router) tranne quello di partenza sono possibili tentativi e vengono "etichettati" con costo infinito. A ogni iterazione:
- Si sceglie il nodo K a costo minore tra quelli non ancora resi definitivi
- Si vede a quale costo X possono essere raggiunti a partire da K i vicini di K che non sono ancora definitivi; se X risulta inferiore al valore indicato nell'etichetta del nodo, il nodo viene marcato come raggiungibile da K a costo X
- K viene marcato come definitivo

![[esempio algoritmo]]

-
-
-
-
-
-
-
-
-
-
-
-

## Flooding
È un algoritmo di routing in cui ogni **pacchetto viene inoltrato su TUTTE le linee eccetto quella da cui è arrivato**. In questo modo ogni pacchetto arriva ad ogni router ma si genera un numero incredibile (teoricamente infinito) di pacchetti nella rete.

**Alcuni vantaggi:**
- **NON richiede di conoscere la topologia della rete**
- Viene **utilizzato da altri algoritmi di routing** per lo scambio di informazioni tra router

**NB**. **OSPF** utilizza un algoritmo di routing che a sua volta manda alcune informazioni con **flooding (limitato)**, poichè ciascun router deve ricevere informazioni da tutti gli altri router della rete.

*Ci sono alcune tecniche per limitare il traffico generato:*
- Si inserisce in ogni pacchetto un **contatore** che viene decrementato ad ogni hop, quando il contatore arriva a 0, il pacchetto viene scartato
- Si inserisce la **coppia (Source router ID + Sequence number) in ogni pacchetto**, quando un router **riceve per la seconda volta** lo stesso pacchetto, lo **scarta**

## Distance vector routing
È un algoritmo di routing dinamico basato sul **cammino minimo**.

##### Vantaggi
- Molto **semplice da implementare** poichè non richiede che i router conoscano la topologia della rete
- Richiede scambi di informazioni solo tra **router adiacenti**.

##### Svantaggi
Presenta un problema che si chiama **problema del conteggio all'infinito**: se un router (o un collegamento) nella rete cade, prima che l'algoritmo stabilizzi la rete ci vuole molto tempo.

**NB**. Questo algoritmo sta alla base del protocollo **RIP**.

#### Caratteristiche
L'algoritmo opera in un ambiente distribuito:
- I **router** NON devono **conoscere** la topologia della rete ma **solo il "costo" per raggiungere i vicini immediati**
- I **router scambiano messaggi solo con i vicini immediati**
- Tutti i router eseguono lo stesso algoritmo in parallelo, avendo tutti lo stesso ruolo
- Sia i router che i collegamenti possono cadere: i messaggi possono andare persi

#### Esecuzione
![[schema sul foglio]]

1. Ogni router mantiene 2 strutture dati:
	- **Vicini immediati**
	- **Tabelle di routing**
2. Ogni nodo inizializza il proprio vettore delle distanze impostando a 0 la distanza da se stesso e a ∞ la distanza dagli altri
3. Ogni router misura periodicamente la distanza tra se stesso e i router adiacenti con un **echo request**
4. Il tempo necessario tra una richiesta e una risposta (**echo reply**) consente di stimare il tempo per raggiungere il router e per essere elaborato, da questo si può stimare anche la distanza.

**NB**. Questa distanza può comunque variare in base al traffico che sta più o meno gestendo il router.


-
-
-
-
-
-

#### Problema del conteggio all'infinito

-
-
-

-
-
-

## Link state routing
È un algoritmo più recente che supera il problema della lentezza di convergenza del distance vector routing.

Ogni router misura la distanza tra se stessi e i vicini immediati (**misurando** il ritardo di ogni linea), e inserisce tali informazioni in un pacchetto chiamato **link state**, che hanno intestazione con:
- Chi ha generato il pacchetto
- Il numero del pacchetto di link state

**NB**. Un pacchetto di link state contiene solo informazioni **misurate**, più precise quindi rispetto ai vettori dell'algoritmo *distance vector routing*.

##### Procedimento
1. Scoprire i vicini e identificarli tramite un **pacchetto HELLO**
2. Misurare il costo (ritardo o altro) delle relative linee (dividento il tempo di arrivo per 2)
3. Costruire un pacchetto, chiamato **link state**, con tali informazioni:
	- Identità del mittente
	- Numero di sequenza del pacchetto
	- Età del pacchetto
	- Lista dei vicini con relativi immediaati
4. I pacchetti vengono inoltrati usando il **flooding**, con riscontro (ACK). *Si implementano poi le altre caratteristiche del flooding.*
5. Previa ricezioni degli analoghi pacchetti che arrivano dagli altri router, costruisce l'**intera topologia della rete**
6. Calcolare il cammino più breve a tutti gli altri router, tramite l'algoritmo di Dijkstra
7. Infine si definiscono le tabelle di routing

**NB**. Il protocollo **OSPF** è basato sul *link state routing*.

## Routing gerarchico
Quando la rete cresce fino contenere decine di migliaia di nodi, le tabelle di instradamento diventano molto complesse.

Per ridurre tale complessità, la **rete viene divisa in zone** (o regioni) con 2 livelli di routing:
- **Routing all'interno di ogni regione**
- Routing tra tutti i **router di confine** (che sono quelli che collegano le regioni tra di loro)

I **router interni** sanno come arrivare a tutti gli altri router della regione, **quando devono spedire qualcosa a un router di un'altra regione** **sa soltanto che deve farlo prevenire al router di confine** della propria regione.

**I router di confine sanno a quale altro router di confine deve inviare i dati** perchè arrivino a destinazione. Questi mantengono al loro interno quindi:
- Le informazioni necessarie all'instradamento interno
- Indicazione degli altri router di confine 

![[foto-di-esempio]]

**NB**. Se due livelli di routing non sono sufficienti, è possibile aggiungerne un terzo.

## Internetworking
**Connetendo tra di loro reti eterogenee** si possono incontrare tali problemi:
- Difformità nei servizi offerti (circuito virtuale o datagram)
- Difformità nei formati dei pacchetti e degli indirizzi
- Difformità dei meccanismi di controllo dell'errore e della congestione
- Difformità nella dimensione max dei pacchetti
- ...

Se dobbiamo collegare reti diverse, abbiamo bisogno di **router multiprotocollo** in grado di **gestire tipi di formati diversi**.

![[esempio rete multiprotocollo]]

### Tunneling
Il **tunneling** è una **tecnica utilizzata per connettere due reti di tipo X attraversando una rete di tipo Y**.

*Esempio: Interconnettere due reti IPv6 utilizzando una rete IPv4 o viceversa*

![[funzionamento-tunneling]]

**Funzionamento:**
1. I pacchetti di tipo X in ingresso vengono incapsulati in pacchetti di tipo Y
2. Raggiungono l'estremità del tunnel
3. L'intestazione di tipo Y viene rimossa
4. I pacchetto viene immesso nella rete di destinazione



http://www.brescianet.com/appunti/newreti/routing.pdf
http://wwwusers.di.uniroma1.it/Reti1/Cap5.pdf
https://unikore.it/phocadownload/userupload/9247532e1b/Lecture_4_DG_CV.pdf
https://www.docenti.unina.it/webdocenti-be/allegati/materiale-didattico/109461
[[Livello di rete.pdf]]