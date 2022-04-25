# Livello di rete

![[vedi slide]]

Ha un ruolo cruciale, è qui che si introduce la possibilità di inoltrare i pacchetti da sorgenti a destinazioni che non sono direttamente collegate. 
Nel collegamento tra sorgente e destinazione remote i dati suddivisi in pacchetti depositati in dei **buffer d'ingresso**, l'entità di livello 3 prende in esame tutti i pacchetti in ingresso e decide dove inoltrarli.

Per questo procedimento ci vuole del tempo: è importante quindi che i pacchetti non rimangano a lungo nei router

### Compiti
1. Instradare i pacchetti lungo la sotto-rete di comunicazione 
2. Controllare la congestione del traffico
3. Interconnettere reti diverse (internetworking)

![[inserisci schema slide]]

Ogni router ha alcune linee di ingresso e di uscita...
Deve decidere su quale linea inoltrare ogni singolo pacchetto

**Tabella di routing**: una tabella che indica, per ogni possibile destinazione, quale linea in uscita utilizzare

### Routing statico / dinamico

Il routing può essere:
1. **Statico**: le tabella sono definite offline e caricate nel router all'accensione. 
2. **Dinamico**(o adattivo): i router stessi, scambiandosi informazioni, sono in grado di determinare quali sono i percorsi e, di conseguenza, costruirsi da se le proprie tabelle. I router si adattano da soli alla nuova situazione (es. nuovo dispositivo, ecc.) in un tempo abbastanza breve da quando c'è la nuova situazione.


NB routing e forwarding
inoltro / forwarding = prendere un pacchetto e spostarlo da un buffer in ingresso ad uno d'uscita tramite le tabelle di inoltro
ruoting = determinare i percorsi

![[inserisci schema (nuvole)]]

Normalmente è utilizzato un MIX di routing statici e dinamici

### Operatività del router
Il router deve avere almeno 2 collegamenti ad internet.
Il router deve prendere un pacchetto dal buffer di ingresso e indirizzarlo nella direzione corretta.

### Tipi di servizio
Il tipo di servizio offerto dal livello di rete al livello di trasporto può essere:
- servizio con connessione e con riscontro (circuiti virtuali)
- servizi senza connessione e senza riscontro (servizio datagram)

Una connessione di livello 3 consiste nel definire un percorso da una sorgente ad una destinazione. Questo percorso verrà utilizzato da tutti i pacchetti che appartengono a quella connessione.

### Circuito virtuale

![[inserirsci schema slide]]

*Spiegazione:*
A intende aprire una connessione verso B, 1 guarderà le tabelle di instradamento e vedrà che la strada corretta è verso 2, 2 si segnerà che deve andare su 3, 3 conclude con B.

??? Quando la rete offre un circuito virtuali i pacchetti non sono identificati da indirizzi di destinazione ma dal circuito virtuale
I pacchetti arrivano a destinazione nello stesso ordine con cui sono stati trasmessi e in più sappiano che sono stati recapitati (dato che c'è riscontro)


Lo svantaggio è che se cade un collegamento è caduta la connessione, potrebbe comportare la perdita del lavoro fatto.

Un vantaggio è che quando si aprono le connessioni si possono negoziare le caratteristiche, si può dichiarare che tipo di traffico passerà per il circuito virtuale


### Rete datagram

Servizio datagram è NON AFFIDABILE e NON ORIENTATO alla connessione.

![[inserisci schema slide]]

*Spiegazione:*
3 fa un percorso diverso da 1 e 2, può succedere quindi che arrivi prima di 1/2 anche se magari spedito prima.

Può anche succedere che un pacchetto vada perso senza che i dispositivi ne vengano a conoscenza 

Il servizio datagram messo in relazione con algoritmi di tipo dinamico è in grado di mandare i pacchetti nonstante ci siano cambiamenti all'interno della rete, però è più difficile controllare la **congestione**.


### Situazione di congestione della rete

![[inserisci schema (iperbole, ...)]]

Una rete non può consegnare più pacchetti di quelli che è in grado. Se la rete può consegnare 1000 pacchetti al secondo non ne può trasmettere 1200,...

Situazione ideale: I pacchetti che trasmettono vengono tutti consegnati fino a saturare la rete, sarebbe desiderabile che questa curva si approssimasse.

Congestione: ...

*esempio:*
Se una linea di uscita è troppo lenta a smaltire il traffico in quella direzione, il buffer di uscita non si svuota abbastanza rapidamente e la relativa coda si riempie

Se si riempie anche la coda di INPUT il router comincia a scartare i pacchetti poichè non può più riceverne
 
**NB**. Ad un certo punto nella storia di internet si verificavano continuatamente congestione, per cui furono implementati determinati algoritmi. 
Esistono algoritmi di controllo della congestione che di solito vengono implementati al livello 4 (livello di trasporto).

In generale la congestione va controllata tra il livello 3 e 4

----

# Algoritmi di routing
Le tabelle di routing sono prodotte attraverso degli algoritmi di routing.
Il routing, come abbiamo visto, può essere di tipo statico o dinamico.

La funzione principale del livello di rete è l'instradamento dei pacchetti tipicamente facendo fare loro molti salti (hop) da un router all'altro.

**NB**. Il **routing** (**instradamento**) si occupa di capire quali sono le destinazioni raggiungibili e lungo quali percorsi.

L'algoritmo di routing ha come scopo quello di fare in modo che i router abbiamo delle tabelle .

Questi percorsi devono essere tecnicamente più diretti/brevi possibili, in realtà per realizzare un buon algoritmo di routing serve una **metrica di riferimento**, alcuni esempi di questa sono:
- minimizzazione del tempo medio di recapito del pacchetto
- percorso più breve in termini di router attraversati
- cercare i percorsi che utilizzano i canali con **banda più larga**

Solitamente si sceglie come parametro quelli di **minimizzare il tempo**.

...

Nel momento in cui si fa il forwarding i router guardano solo la loro tabella, non hanno una conoscenza globale della rete (non sanno cosa c'è oltre), deve essere quindi un processo **snello**.

Ambedue i processi (forwarding e routing )però sono necessari ...

### Caratteristiche degli algoritmi di routing
NB. Ci sono modi migliori e peggiori per scrivere un programma. Un algoritmo di routing scritto male potrebbe compromettere la funzionalità/velocità della rete

Questi algoritmi devono quindi essere:

- **SEMPLICI**:
	- implementazione **snella**, con minore possibilità di errori
	- utilizzo limitato di tempo e risorse di elaborazione (CPU, memoria)

- **ROBUSTEZZA e ADATTABILITÀ**
	- l'algoritmo deve funzionare su una topologia di rete generica e senza alcun vincolo sulla stessa
	- l'algoritmo deve **sopportare cambiamenti** di topologia senza interrompere il funzionamento della rete (quando siamo su routing dinamico)
		- **Fault Detection**: capacità di accorgersi che qualcosa non sta funzionando
		- **Autostabilizzazione**:  se qualcosa non va nella rete, nel minor tempo possibile, devo trovare dei nuovi percorsi 

NB. robustezza = in grado di funzionare indipendentemente dalla rete in cui mandato in esecuzione

- **OTTIMALITÀ**: ...
 
- **STABILITÀ**: se non cambia nulla, le tabelle non devono cambiare

- **EQUITÀ**: tutti i nodi devono avere le stesse possibilità nella scelta dei percorsi di instrdamento. Non devono esistere nodi "trascurati o danneggiati" dalla scelta dei percorsi di instrdamento

### Algoritmo di Dijkstra (rivedere)
Descrizione: ...

![[inserisci disegno della rete presente sulle slide (a-b-c-d-e-...)]]
![[schema su foglio]]

*Basandoci sul disegno sopra:*

Le lettere sono i router
I numeri identificano un possibile "costo" per percorrere tale tratta
Percorso = **cammini**

I percorsi con anelli devono essere scartati.

In generale non si può calcolare il percorso solo sommando i costi, poichè molto dispendioso computazionalmente, ecco perchè l'algoritmo di dijkstra: ...

L'algoritmo di Dijkstra si basa sul principio di **...** che dice: prendendo lo schema sopra, se F è nel cammino ottimo tra A e G, allora il tratto tra A ed F è anche il cammino migliore tra A e F.

Dal punto di vista algoritmico tutti i nodi della rete devono essere marcati con un'indicazione (provenienza e costo), tranne in quello da cui parto.

Scegliamo il nodo a costo **minimo** e **massimo**.

Alla fine ci troveremmo con un *albero* che parte dal nostro punto di partenza.

Ora si crea la tabella, in questo caso di C:
Punto | uscita
a |	1
b | 1
c | -
d | 1
e | 2
f | 2
g | 2

**NB**. OSPF utilizza l'algoritmo di Dijkstra per la costruzione delle tabelle. Quindi l'algoritmo di dijkstra può essere utilizzato sia nel routing statico che dinamico.

### Flooding
È un algortimo di routing in cui: se si riceve un pacchetto su una linea **lo si manda su tutte le altre linee** (viene **inoltrato** su tutte le linee, tranne che in quella da cui l'ha ricevuto), in questo modo ogni pacchetto arriva ad ogni router della rete ma si genera un numero incredibile di pacchetti nella rete (pacchetto arriva troppe volte).

- **NON richiede** di conoscere la topologia della rete
- È utilizzato da altri algoritmi di routing per lo scambio di informazioni tra router

Es. OSPF utilizza un algoritmo di routing che a sua volta manda alcune informazioni con un flooding (limitato), poichè ciascun router deve ricevere informazioni da tutti gli altri router della rete.

Ci sono delle tecniche per limitare il traffico generato:
- Si inserisce in ogni pacchetto un **contatore** che viene decrementato ad ogni hop, quando il contatore arriva a 0 il pacchetto viene scartato.
- si inserisce la coppia...



### Distance vector routing
È un algoritmo di routing dinamico basato sul **cammino minimo**. È un algoritmo molto semplice da implementare poichè non richiede che i router conoscano la topologia della rete, richiede scambi di informazione solo tra **router adiacenti.**

I router NON conoscono la topologia della rete, solo i router adiacenti ad esso.

Sta alla base del protocollo **RIP**.

**NON** gode della proprietà di **autostabilizzazione**

Presenta un problema che si chiama **problema del conteggio all'infinito** : se un router sparisce dalla rete, prima che l'algoritmo distance vector stabilizzi la rete ci vogliono molti passaggi **????**

Caratteristiche alla base:
- i router non devono conoscere topologia della rete ma solo il "costo" per raggiungere i vicini
- I router scambiano messaggi solo con i vicini imminenti
- Tutti i router 
- ...
- ...
- ...

Esecuzione:

![[vedi schema sul foglio]]

Ogni router mantiene 2 strutture dati: vicini immediati e tabella di instradamento.

Ogni router misura (periodicamente) la distanza tra se stesso e i router adiacenti con un *echo request*, dividendolo /2 si ottiene il tempo.
Il tempo necessario tra una richiesta di echo e una risposta (echo reply) consente di stimare il tempo per raggiungere il router e per essere *elaborato.* e si stima anche la distanza.

Questa distanza comunque può variare in base al traffico che sta più o meno gestendo il router.

Sempre periodicamente il router manda agli altri un **vettore di distanza**, contenente la distanza (**misurata** o **stimata**) dal router a tutti i nodi della rete.

*Esempio:*
A, sulla base dei vettori distanza ricevuti da B e C, calcolerà il proprio vettore distanza (che alla prossima iterazione invierà agli altri) e la tabella di routing. Le distanze che A calcola per D, E, F,... sono STIMATE sulla base delle distanza date da B e C.

*Distanze stimate in quale modo?*


*Considerazioni:*
- Non sempre queste distanza stimate sono corrette.
- L'algoritmo è molto SEMPLICE da applicare

![[vedi esercizi]]

##### Problema del conteggio all'infinito
![[vedi slide]]

Ad ogni iterazione qualcuno sempre più si propaga, la distanza cresce di 1 ad ogni scambio dei vettori distanza. E nel frattempo il routing continua ad essere "sballato".
I router continuano a credere di poter fare una strada sbagliata.

Ecco perchè questo algortimo di routing (distance-vector routing) seppur molto semplice (ottimo per l'overhead) NON viene più utilizzato.
Al suo posto si preferisce utilizzare il **link state routing**

### Link state routing
Ogni router misura la distanza tra se stessi e i vicini immediati, queste informazioi vengono inserite in un pacchetto chiamato di **link state**, che hanno intestazione con: 
- chi ha generato il pacchetto
- il numero del pacchetto di link state

NB. un pacchetto di link state contiene solo informazioni **misurate**, più precise quindi rispetto ai vettori dell'algoritmo *distance vector routing*

Questi pacchetti quando vengono ricevuti si controlla se è la prima volta che lo ricevo, se è così lo inoltro a tutta la rete, altrimenti lo ignoro.
Una volta che un router ha ottenuto tutti gli altri pacchetti di link state della rete ha la possibilità di costruire la topologia della rete, applicare quindi l'algoritmo di Dijakstra e in conclusione trovare le tabelle di routing.

### Routing gerarchico
Come sono organizzati i router in una tabella molto grande

Nel caso di rete molto grandi bisogna ridurre la complessità delle tabelle di routing e dell'algoritmo che le gestisce. 
La rete viene quindi divisa in zone (o regioni) e ci sono 2 livelli di router:
- interno alla regione
- di confine (o esterno), collega tra di loro le regioni

Un router interno deve avere delle tabelle che consentono l'instradamento all'interno della regione e in più deve conoscere i router di confine

I router di confine sanno quali sono glia altri router di confine per permettere il passaggio dela pacchetto da una rete all'altra

![[inserisci foto di esempio]]

### Internetworking
NB. Il livello di rete deve inoltrare i pacchetti, controllare o meno la congestione e consentire il collegamento tra reti diverse.

In generale se dovessi collegare reti eterogenee potrei incontrare questi problemi:
- difformità nei servizi offerti (circuito virtuale o datagram)
- difformità nei formati dei pacchetti e degli indirizzi
- ...
- ...

In generale se dobbiamo collegare reti diversi avremmo bisogno di router multiprotocollo in grado di gestire tipi di formati diversi (es. passare da rete IP a rete OSI)

Un modo che viene utilizzato è il **tunneling**, si usa quando si voglioni collegare due reti dello stesso tipo passando attraverso una rete di tipo diverso.

Es. 2 reti IPV6 collegate attraverso una rete IPV4, le 2 estremità del tunnel devono essere in grado di operare in entrambi i protocolli

Tunnel n-point prende pacchetto ipv6 e nell'intestazione gli cambia l'indirizzo di sorgente e destinazione in versione 4, per esempio. Poi verrà "aperto" e si prenderà il payload contenuto in ipv6 ????



