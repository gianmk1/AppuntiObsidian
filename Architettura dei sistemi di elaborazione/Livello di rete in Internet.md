# Livello di rete in internet

**INTERNET**: é una collezione di sistemi autonomi (AS) connessi gli uni con gli altri in cui possiamo distinguere alcune componenti:
- Dorsali (backbone) principali (Tier 1 network), realizzate con linee ad alta velocitá

-- continuazione sulla slide --

-- inserire immagini struttura di rete --

Internet è tante reti connesse per ottenerne una.

Insieme di sistemi autonomi interconnessi in cui ci sono delle aree principiali (**backbone**) perchè interconnettono ad altre reti.
Questra struttura alla fine risulta un po' *anarchica*, non c'è possibilità di controllo centralizzata.

### Intestazione del pacchetto IP
![[inserire foto pacchetto ip]]

Ogni segmento dell'unità di trasporto viene incapsulato in un *pacchetto IP*, cioè viene inserita una intestazione. 
L'intestazione IP viene organizzata in **longword** (=32bit), c'è prima il bit meno significativo.
Il primo bit trasmesso dal pacchetto è quello numero 0 (vedi foto)

- Source address: indirizzo ip del nodo della rete che ha generato il pacchetto
- Destination address: indirizzo ip del nodo della rete a cui è destinato il pacchetto
- Version: 4 bit in cui è scritta la versione del protocollo
- IHL: 4 bit, lunghezza dell'intestazione (numero che è variabile tra 0 e 15), è il numero di longword che compongono il pacchetto
- TOS (tipo di servizio richiesto): per marcare un servizio, può essere utilizzato per la gestione della qualità di un servizio dando priorità ad un certo tipo di traffico 
- Total lenght: lunghezza totale del pacchetto, quantifica in byte, il massimo è (2 alla 16) 64000byte. La misura standard di un pacchetto è 1500byte (perché questa è la dimensione massima del **payload** ??? )
- TTL (Time to Live): è un contatore che viene decrementato di 1 ad ogni passaggio di router, se arriva a 0 viene scartato. Arrivare a 0 vuol dire che il pacchetto si è perso, è in giro da troppo tempo e rischia di essere diventato obsoleto ed arrivando a destinazione può fare più male che bene. *Meglio mai che tardi*
- Protocol: contiene in forma codificata il protocollo del payload, serve a capire per chi è il pacchetto quando è arrivato a destinazione
- Header checksum: serve per verificare la correttezza dell'intestazione, errori nell'intestazione non sono accettabili. Ad ogni router (ad ogni salto (hop) quindi) la checksum va ricalcolata. Nel protocollo ipv6 questa è stata abolita
- Options: opzioni, ormai non più utilizzato

NB. I router lavorano tramite dei **buffer**, che incodano i pacchetti in entrata ed in uscita. 

**MTU**: è la dimensione massima dei pacchetti che possono passare nella rete in questione

*Riassunto:*
Version: numeri di versione del protocollo (4)
Time to live: limita numero di hop che il paccchetto può fare all'interno di una rete

#### Frammentazione IPV4 

MTU: dimensione massima accettata del pacchetto

Un pacchetto può essere **frammentato**, massimo una volta, in pacchetti di dimensione massima 576byte (dimensione minima che un ruoter deve accettare). Verrà quindi frammentato in *datagram indipendenti* (che possono arrivare in ordine casuale), il compito di ricostruire il datagram originale viene fatto tramite:

- Identification: numero che tutti i frammenti del pacchetto hanno in comune
- Fragment offset: determina in che posizione (contando i byte) va questo segmento all'interno del datagram originale
- Flags: 
	1. **DF** (don't fragments): se uguale a 1 NON si deve frammentare il pacchetto
	2. **MF** (more fragments): se uguale ad 1 il pacchetto non è ancora finito, se è 0 è l'ultimo frammento del pacchetto

Incrociando i valori dell fragments offset e del flag si capisce se un datagram è frammentato o meno.

-------

# Indirizzi IP (rivedere)
Sono 32 bit, l'**indirizzamento IP** è gerarchico, l'indirizzo è diviso in 2 campi: una porzione identifica in modo univoco la rete, e un'altra porzione identifica un nodo all'interno di quella rete.
Questa suddivisione è variabile.

**Metodo Classfull**
![[inserire schema pag2 pdf inirizzi IP]]

#### 3 classi: A, B, C

Esempio: 120.7.4.2
Rappresentazione decimale a punti, ognuno di questi numeri è un byte dell'indirizzo, è quindi una sequenza di 32bit (**0**111 1000 0000 0111 0000 0100 0000 0010).
- Il bit più significativo (il primo) è 0, identifica una rete di classe A sono solo 126, ciascuna di essa può ospitare più di 16milioni di nodi (vedi sotto)
- I primi 8 bit 
- I seguenti 24 bit quindi permettono 2^24 combinazioni


120.0.0.0 => rappresenta la rete


**NB**. Tutto ciò che comincia con 127 è riservato per la *localhost*

Quando si fa la configurazione manuale di un nodo bisogna specificare:
- indirizzo ip 

##### Cos'è una maschera di sottorete?
Ha degli 1 nella parte di indizzo che determina il numero di rete e ha degli 0 nella parte dell'indizzo che determina l'host all'interno della rete

ES. maschera di sottorete della classe B è 255.255.0.0

<br>

(riferito a schema slide 3 del pdf)

In internet tutti i nodi che appartengono ad una stessa rete fisica devono appartenere tutti alla stessa rete IP
Corrispondenza rete fisica - rete ip: 

vengono quindi sprecati degli indirizzi ip (es. multicast)
Questo ha portato nel tempo ad un altro modo di indirizzare che si chiama **classless**

NB. nel router ogni interfaccia di rete deve avere il suo indirizzo ip

### Notazione Classless
![[schema slide 4 del pdf]]

![[vedi slide 5 del pdf]]

Un prefisso lungo L: i primi L bit dell indirizzo rappresentano la rete, i rimanenti bit 

Prefisso predefinito per classe A:
Prefisso predefinito per classe B:
Prefisso predefinito per classe C: /24

Esempio CIDR (Classless Inter Domain Router), rete 184.13.12.0/22

Quali sono gli indirizzi che posso effettivamente usare in questo range?
![[vedi slide pag 6]]

*Svolgimento:*
Passo in binario, converto 152 in binario => 1001 1000

184 13 1001 10|**00 0000 0000**			-> questa è la parte variabile

Quando ho tutti 0 è l'indirizzo di rete, quando ho tutti 1 è l'indirizzo di broadcast

### Indirizzi IP speciali




-----------
# CONTINUAZIONE Livello Di Rete in Internet 20 DIC 2021

NB: protocollo = regole di comunicazione per entità di stesso livello

## NAT: Network address translation

Si utilizza per molti motivi, principalmente però:
È la tecnica utilzzata per poter continuare ad avere sempre più nodi che utilizzano indirizzamento ipv4, quando in realtà questi sono finiti da molto tempo

Serve quindi per collegare a internet una rete LAN che al suo interno utilizza indirizzi IP PRIVATI. Ciò avviene utilizzando l'indirizzo IP

<br>

*Aggiungere poi al documento Indirizzi IP:*
### Indirizzi IP PRIVATI
ICANN è un organismo internazionale incaricato di assegnare indirizzi ip e di gestire i nomi di dominio di primo livello. A sua volta questo organismo delega ad altri organi (NIC o RIR).

![[vedi immagine del planisfero suddiviso]]

ICANN ha dato a ciascun area dei blocchi di indirizzi IP, i LIR hanno a loro volta hanno suddiviso questi indirizzi tra i Provider

Ormai questi blocchi di indirizzi sono tutti esauriti; che non vuol dire che sono tutti utilizzati ma che sono stati tutti distribuiti.

L' ICANN ha riservato 3 blocchi di rete per indirizzi privati che non si collagano a internet (anche detti *not routable*). 

<br>

*Continuazione del NAT*:

Le reti private quindi ora utilizzano al loro interno indirizzi IP di tipo privati not routable.

Il NAT consente di presentatre tutti i nodi della rete IP privata con un indirizzo IP pubblico che è l'indirizzo che il router ha verso l'esterno.

L'indirizzo sorgente dei pacchetti deve quindi essere un indirizzo pubblico, le risposte arrivano al router con però l'indirizzo ip del router, come se fossero destinatia lui, ma in realtà sono indirizzati ad un nodo interno.

Una volta che arrivano tutti questi pacchetti indirizzati al router

IL **NAT** è di 2 tipologie:
1. **NAT SORGENTE**
Normalmente utilizziamo applicazioni di tipo client che si collegano a server esterni. Il router si costruisce una tabella in cui inserisce mano a mano le richieste che vengono fatte

2.

##### Alcune precisazioni prima del NAT

*Esempio:*
Ragioniamo nella situazione in cui un client vuole fare una richiesta ad un server.

NB. Posso avere molte applicazione di rete in esecuzione contemporaneamente, ognuna di essere deve poter comunicare con il TCP, ad ogni applicazione deve esserci una connessione. 
Possono esserci quindi tante applicazioni di rete, ognuna di loro collegata con un'entità di livello di Trasporto e sotto c'è l'Internet Protocol. TCP deve sapere a chi consegnare il pacchetto quando lo riceve, questa informazione è specificata nel campo *numero di porta di destinazione*.

Il numero di porta TCP è semplicemente un IDENTIFICATIVO.
*Ci sono 2 numeri di porta, quello sorgente e di destinazione.*

Il ruolo di porta sorgente e di porta destinazione cambia

Dal lato del client ci sarà un indirizzo ip e un numero di porta, dal lato del server ci sarà la stessa cosa.
Se il pacchetto viaggia da client a server, il client è la sorgente e il server è destinazione, nella risposta viceversa

**Indirizzo IP e Porta formano TSAP**

**TSAP**
Fissato il tempo, una coppia di TSAP identifica in modo univoco una connessione

<br>

Ci sono 2 applicazioni che dialogano, client e server, il server deve essere già attivo nel momento in cui il client vuole aprire il collegamento. Parte per primo e attende una richiesta. Il client parte quando vuole lui ed è lui che apre la connessione e interroga il server.

Le applicazioni di tipo server quando partono specificano il numero di porta in cui sono in **ASCOLTO**. 

##### Il numero di porta
Il numero di porta è a 16bit, le prime 1024sono chiamate *well-know-port* e sono numeri riservati ad applicazioni standard

Il numero di porta nelle applicazioni client viene assegnato dal TCP quando viene aperta la connessione, queste porte vengono anche chiamate **porte-effimere**.

Il TCP garantisce però l'unicità delle 2 TSAP , unico modo per esseri sicuri 




### Source NAT ???
es: un nodo (192.168.1.2) decide di aprire connessione con un server web (porta 80). Il TCP assegna come numero di porta privata 21023.
Il pacchetto che esce deve uscire con l'indirizzo esterno, il router oltre a cambiare l'indirizzo IP cambia anche il numero di porta (es. 14003), il server risponderà, idealmente, mandando qualcosa all'indirizzo esterno con porta 14003
Il software del router si salva questa informazione in una tabella, quindi quando riceve un pacchetto andrà a confrontare l'indirizzo esterno con quello sorgente, la porta esterna con quella sorgente e la porta di destinazione con la porta NAT

Se trova corrispondenza: porta di destinazione la sostituisce con quella privata, indirizzo di destinazione va a sostituirlo con quello privato e manda il pacchetto.

Il NAT indirizza quindi correttamente.

Se mi limitassi a sostituire l'indirizzo IP nella porta di uscita non avrei più l'univocità delle connessioni, non saprei più a quale connessione TCP appartiene.

Cosa succede se non trovo un match: vuol dire che quel pacchetto non lo dovevo ricevere e quindi lo scarto.


**Il NAT offre quindi anche una minima PROTEZIONE**, rende anche più difficile capire cosa c'è all'interno della rete.

Il source nat è trasparente, viene attivato e poi fa da solo. Permetto ai client di connetersi a server esterni

## Destination NAT ???
Permetto che un nodo qualsiasi di internet possa collegarsi ad un server che ho in esercuzione sulla mia rete.

Serve per far si che un server con indirizzo privato sia accessibile all'esterno tramite un indirizzo IP pubblico

Il router deve sapere che i router che arrivano, ad esempio, nella porta 80 vanno inoltrati, ad es, al 192.168.1.3 , se ricevi richieste sulla porta 21 vanno invece, ad es, al 192.168.1.40

Vedi meccanismo di **Port Forwarding**

---
## RIPASSO: NAT
Lo scopo principale del NAT è collegare ad internet una rete LAN che al proprio interno utilizza indirizzi IP privati.

NB. La rete potrebbe essere privata ma utilizzare comunque indirizzi IP pubblici, lì non ci sono problemi e non c'è bisogno di NAT.

Da molti anni ormai non sono più disponibili indirizzi IP pubblici.

NAT: Tutti i pacchetti che escono dalla LAN condividono un unico indirizzo IP pubblico che è assegnato all'interfaccia esterna del router ed è quella con cui il router si collega ad "internet".

I pacchetti generati avranno come indirizzo ip sorgente della stazione ma prima di uscire in internet viene sostituito con quello del router (int esterna).

Il router riceverà i pacchetti con lui come destinazione: per individuare i corretti destinatari il router tramite NAT deve costruirsi una **tabella** 
![[vedi esempio slide]]

All'apertura della connessione (tra pc e server esterno) il NAT va a aggiungere una riga alla tabella.
Il NAT al posto dell'indirizzo sorgente **mette il proprio indirizzo IP pubblico** e va a **modificare la porta sorgente** con un numero di porta (**generato al momento**) chiamato porta NAT

Il server web manderà una risposta con porte e indirizzi INVERTITI.
Il NAT controllerà se c'è qualcuno che sta aspettando quel pacchetto, vedendo se qualcuno ha aperto una connessione con il server in questione e modifica INDIRIZZO E PORTA.

-> Se non c'è corrispondenza il pacchetto viene SCARTATO.

**Source NAT**: consente a dei client interni di accedere a dei server esterni (*vedi sopra*), quello normalmente utilizzato. Serve solo abilitarlo, non configurarlo.

**Destination NAT** (o anche server virtuale): per rendere accessibili all'esterno i server in esecuzione in reti con indirizzo IP privato. Serve una configurazione statica (che può essere però anche dinamica) in cui si specifica a quale indirizzo IP locale destinare tutti i pacchetti in arrivo all'indirizzo IP pubblico del server su una determinata porta (*es. porta 80 per il server web*). 

*Se ti arrivano richieste sulla porta 80 dirottale alla porta 80 della stazione 192.168.1.5*

Vedi meccanismo **port-forwarding**.

<br>
<br>
<br>

---

# Continuazione 14gen2022

## ARP (Address Resolution Protocol)
È uno dei protocolli di controllo di internet. **È un protocollo di livello 2 (link)**, **NON** di livello 3.
È un meccanismo domanda - risposta
È una risoluzione inversa, serve per associare ad un determinato indirizzo IP, un indirizzo di livello 2 (MAC address). 

*Esempio*
router 1 riceve un pacchetto destinato al nodo 150.7.0.1, la rete in questione si raggiunge tramite l'interfaccia eth1

L'entità di livello 2 incapsulerà il pacchetto in un frame, per costruire quest'ultimo serve l'indirizzo MAC della stazione destinataria. Per ottene ciò si utilizza il protocollo ARP

La **prima volta** che si incontra un indirizzo IP e non si sa il MAC corrispondente: si manda una **ARP request**, **tramite broadcast** di livello 2, con cui si chiede quale stazione ha quel determinato indirizzo IP. La stazione corretta risponderà SOLO al mittente della richiesta.

Le **risposte** vengono mantenute memorizzate, momentaneamente, in una **cache**.

![[vedi esercitazione su kathara]]

*Comando linux: sudo tcpdump -i [SCHEDA_DI_RETE] | grep ARP*

## ICMP (internet control message protocol)
È un protocollo di livello 3, utilizzato dai router per scambiarsi informazioni e gestire la rete.
Alcuni esempi sono:
- echo request
- echo reply
- timestamp request (come una echo ma chiede anche l'orario)
- se un pacchetto viene scartato perchè superatoil TTL
- se l'header di un pacchetto non è corretto

IL messaggio ICMP è inserito nel payload del PACCHETTO e viene genrato/gestito direttamente dall'entità IP sorgente/ destinazione

Con la sezione **Control** del pacchetto verifichiamo che tipo di pacchetto è:

Il formato del pacchetto ICMP prevede:
- ...
- ...
- ...

...

## DHCP (Dynamic Host Configuration Protocol)
È un protocollo che opera al **livello Applicazione**, serve per **configurare in modo automatico le impostazioni di rete** di una stazione:
- indirizzo IP e prefisso
- indirizzo del default gateway
- indirizzo del server DNS

*Quando è possibile è meglio utilizzare la configurazione manuale che permette di associare un indirizzo IP ad una stazione. Diventa però molto difficile se siamo all'interno di una rete wifi.*

**Come funziona?**
La configurazione IP comprende:
- indirizzo IP e maschera di sottorete
- indirizzo IP gateway
- indirizzo IP di uno o più server DNS (necessario perchè difficilemente siamo in grado di utilizzare una rete senza)

Ci deve essere un server dhcp abilitato, ogni server avrà in gestione un pool (insieme) di indirizzi IP che può gestire.
La stazione che richiede una conf automatica, quando si connette alla rete dhcp manda una richiesta **DHCPDISCOVER**, mandata con un **broadcast di livello 3** (= a tutto il mondo), chi è nella rete e sente la richiesta, manda una risposta, la stazione può decidere di tenere la configurazione o scartala (DHCPREQUEST), poi il server da la conferma finale, in broadcast liv. 2, (con un DHCPACK), in questo modo gli altri possibili server dhcp capiscono che la loro offerta non è più valida.

Questa fase di richiesta esplicita server perchè potendoci essere più server DHCP al DHCPDISCOVER potrebbero rispondere più server.

Allo scadere di tempo della configurazione, la stazione dovrà richiedere esplicitamente il consenso per continuare a utilizzare tale configurazione.

**Broadcast di livello 3:**
... , La richiesta è fatta in broadcast di livello 3, la risposta del server viene mandata al livello 2 (con indirizzo MAC), poichè la stazione che richiede non ha ancora un suo indirizzo.

*Questo protocollo in conclusione lavora su più livelli, è un IBRIDO.*

## Routing in internet
Internet è una collezzione di sistemi autonomi connessi tra di loro.

NB. Col Routing gerarchico, il routing viene suddiviso: 
	- all'interno dell'area
	- tra router di confine
	Questo serve per semplificare le operazioni di routing e inoltro e la dimesione delle tabelle di routing.
Oltre a questo gli AS sono gestiti da entità/organizzazioni diverse:
possono esserci delle regole per il passaggio da un sistema autonomo all'altro, si utilizzano quindi **protocolli di tipo diversi**:

- protocolli interni a sistema autonomi: **interior gateway protocol, iGP**
- protocolli esterni a sistemi autonomi: **exterior gateway protocol, eGP**

Un insieme di router connessi sotto il controllo di uno o più operatori di rete per
conto di una singola entità amministrativa o dominio che presenta una politica di
routing comune e chiaramente definita a Internet.

I sistemi autonomi sono UNIVOCAMENTE identificati. Ogni AS deve avere almeno un router esterno, collegato agli altri router esterni (deve sapere quindi come raggiungere i diversi AS)

#### OSPF
Protocollo di **routing interno**, sta sostituendo gradualmente il RIP.
È basato sull'algoritmo **link state routing**.

Il routing interno può essere organizzato in modo gerarchico: Il Sistema Autonomo viene **suddiviso in diverse aree**, da cui una è l'area di backbone ed è connessa a tutte le altre.

![[schema ospf]]

Il vantaggio di dividere anche il routing interno facilita il routing e forwarding e limita l'algoritmo di link state. 
*L'area di backbone deve essere configurata con router potenti e collegamenti ad alta velocità.*

#### BGP
È basato sul **distance vector routing**, deve però anche:

- Gestire politiche di instradamento che potrebbero essere legate a considerazioni di carattere geopolitico. Potrebbero esserci delle direttive che vietano il passaggio per alcuni sistemi autonomi sparsi nel mondo per una maggiore sicurezza
- Mantiene (e scambia con gli altri router) non solo il costo per raggiungere le altre destinazioni, ma anche il cammino completo, risolvendo così il problema del conteggio all'infinito (il distance vector routing è quindi modificato)

*Vedi slide degli argomenti precedenti su problema conteggio all'infinito*

## IPV6, Internet Protocol Versione 6
Il progetto nasce nel 1990 da IETF con gli obiettivi di:
- supportare miliardi di nodi
- ridurre dimensioni tabelle di routing
- semplificare il protocollo
- introdurre ELEMENTI di SICUREZZA (autenticazione e privacy), inizialmente internet era limitato ad un ambito accademico, in pochi avevano accesso alla rete, non si era badato troppo all'aspetto della sicurezza
- permettere al vecchio protocollo (ipv4) di coesistere con quello nuovo (*quest'ultima però non è andata al buon fine, IPV4 e IPV6 NON sono interoperabili*)

- Gli indirizzi sono a **128bit**, il che consente di avere un numero di indirizzi (xxxxxx) per metro quadro della superficie terrestre.
- L'intestazione è semplificata (solo 7 campi) per permettere di sveltire l'inoltro
- È migliorato il supporto per le opzioni, e anche questo velocizza...
- ...

Ciò si ottiene semplificano l'intestazione MA aumentando la possiblità di aggiungere delle opzioni. Il pacchetto ipv6 è fatto da una **catena di intestazioni** e dal **payload**.

![[vedi schema]]

*La maggioranza dei pacchetti comunque è composta solo dall'intestazione base.*
*Il protocollo è più veloce, ovviamente, quando il pacchetto contiene la sola intestazione principale*

![[schema intestazione ipv6]]

- version: consente subito se il pacchetto è in versione 4 o 6
- traffic class: identifica la categoria di dati nel pacchetto, ??? utile per implementare politiche di qualità del servizio
- flow label: serve a identificare tutti i paccchetti che appartengono allo stesso flusso

**IPV6 continua ad essere un protocollo DATAGRAM**, se si volessero implementare politiche di qualità del servizio:

*es. utente sta facendo una conversazione voip e contemporaneamente sta scaricanto un torrent, si vuole dare la precedenza alla telefonica. Torrent utilizzerà la rete in modo intensivo, limitando notevolmente il traffico alla chiamata Voip. I pacchetti vengono accodati man mano che arrivano, quelli torrent satureranno il buffer. L'ipv6 ha bisogno di sapere come marcare i pacchetti*

Il concetto di flusso coindice con la quantità di dati generati da una determinata applicazione.
Nell'ipv4 non c'è modo di sapere a quale flusso un pacchetto appartiene, nell'ipv6 SI, quindi si possono stabilire politiche di servizio differenziate.

- payload lenght : lunghezza del pacchetto
- hop limit: (vecchio time to live del protocollo ipv4), quando il counter arriva a 0 il pacchetto viene scartato
- next header (sostituisce protocol di ipv4): se il pacchetto è con la sola intestazione base contiene qual'è il protocollo del paylaod (es. tcp - udp - icmp). Se c'è un intestazione di estensione, invece viene scritta la prossima intestazione (che a sua volta conterrá il protocollo o la prossima intestazione), formando così una **lista concatenata**

![[vedi schema intestazioni]]

Rispetto a IPV4 MANCA:

- manca il campo che specifica la grandezza dell'intestazione
- manca l'header checksum: poichè la checksum cambia e deve essere ricalcolata ad ogni hop, toglierli questa cosa sveltisce il processo al router
- manca la parte relativa alla frammentazione: in IPV6 la frammentazione NON viene utilizzata e ogni router deve capire qual è la MTU max del percorso e di conseguenza farà pacchetti più o meno grandi

#### MTU Path Discovery
![[schema path mtu]]

Tramite un pacchetto ICMP il router comunica al router mittente, la MTU max del pacchetto. La sorgente scopre così la dimensione massima del pacchetto che può inviare

La dimensione minima del MTU è stata ingrandita per passaggio di pacchetti con payload di 1024 byte (sempre che abbiamo una sola intestazione)

#### Formato degli indirizzi IPV6
Un indirizzo IPv6 è rappresentato usando 8 quartetti di cifre esadecimali (1 cifra esadecimale sono 4 bit), separate dal simbolo ':' , ad esempio:

*indirizzo iniziale*

Per brevità gli 0 iniziali di ogni gruppo possono essere omessi, quindi ad esempio l'indirizzo riportato sopra diventa:

*indirizzo finale*

Per omettere un gruppo di zeri consecutivi si usa il simbolo '::'

L'organizzazione degli indirizzi è gerarchica (rete - host nella rete), per sapere ciò utilizziamo un PREFISSO (NON si parla più di maschere di sottorete), a ogni rete fisica è associato un prefisso.

#### Transizione IPv4 - IPv6
Come sta avvenendo:
1. si usa principalmente l'infrastruttura ipv4 esistente
2. i protocolli coesistono
3. i nodi ipv4 restanti usano ipv6 e devono poter usare servizi ipv6

Ci sono diverse possibilità:
- **DUAL STACK**, il router deve poter interpretare entrambi i protocolli. 
questa cosa richiede doppia implementazione, e ogni nodo deve avere anche un indirizzo ipv4

- DSTM, si usa ipv6 e dove necessario, dinamicamente, si utilizzano indirizzi ipv4

- NAT-PT, una rete all'interno utilizza il protocollo ipv6 mentre quello esterno è ipv4
- **TUNNELING**: mettere in comunicazione due reti che usano ipv6, passando per un tunnel che usa ipv4 (pacchetto ipv6 viene incapsulato all'interno di un pacchetto ipv4). In questo caso solo gli end-node del tunnel devono avere l'indirizzo IPv4.

![[vedi schema tunneling]]

