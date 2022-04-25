# Introduzione alle reti
### Utilizzo delle reti
- **Servizi internet** (web, posta elettronica, trasferimento file...)
- **Servizi di rete locale** (autenticazione, ...)

### Organizzazione del software di rete: *stack di protocolli*
Il software di rete é organizzato in *livelli*. Ad **ogni livello é assegnato un compito specifico**. Ordinamento dal _basso_ (vicino alla macchina fisica) verso l'_alto_ (vicino all'utente).

**Compiti**:
1. di _basso livello_: svolti dall'hardware dedicato (es. scheda di rete)
2. di _alto livello_: svolti dal software

#### Perchè i livelli?
Anche un router ha diversi tipi di interfaccia fisica:
- Porte per il collegamento cablato (802.3)
- Antenna per il collegamento (802.11)
- Porta per il collegamento PPPoE alla rete telefonica

Deve quindi instradare pacchetti tra diverse linee di comunicazione.

## Definizioni:
- **Entitá**: insieme di hardware e software che realizza i compiti di un livello
- **Interfaccia**: insieme delle regole di comunicazione tra entitá di livelli *adiacenti* 
- **Protocollo**: insieme di regole di comunicazione tra entitá di pari livello
- **TCP ( o Transmission Control Protocol)**: protocollo che crea una connessione tra due host e gestisce la consegna dei _segmenti_ da un sistema all'altro
- **IP (Internet Protocol)**: protocollo che fornisce le istruzioni per il trasferimento dei dati
- **Host**: nodo della rete che ha un solo collegamento alla rete
- **Router**:è un qualsiasi nodo della rete che ha almeno 2 interfacce. Si occupa di instradare i pacchetti dati tra sottoreti. Lavora a livello logico come *nodo* interno deputato alla commutazione di livello 3 (del modello ISO-OSI)
- **Subnet (o sottorete)**: è una parte della suddivisione di una singola rete IP (la suddivisione non è visibile all'esterno)
- **Overhead**: informazioni aggiuntive necessarie per la trasmissione dell'informazione stessa. Es. *header* di un pacchetto IP

### Protocolli dell'architettura TCP/IP
![[protocolli.PNG]]
Varie tipologie di protocolli:
1. Applicazione (es. http)
2. Transporto
3. Internet
4. Link

- (2) **TCP ( o Transmission Control Protocol)**: protocollo che crea una connessione tra due host e gestisce la consegna dei _segmenti_ da un sistema all'altro
- (3) **IP (Internet Protocol)**: protocollo che fornisce le istruzioni per il trasferimento dei dati tramite l'assegnazione di un indirizzo ad ogni host

### Due modelli di riferimento per le reti
![[modelli_riferimento_reti.png]]
**Stratificazione di livelli**, *"dividi et impera"*. Livello *n* offre servizi al livello *n+1*, e usa i servizi di *n-1*.
1. **FISICO**: si occupa di trasmettere e ricevere i **bit sul mezzo trasmissivo**
2. **DATA LINK**: si occupa di gestire il **collegamento da un pc all'altro appartenti alla stessa rete LAN**. Deve garantire una linea di **trasmissione priva di errori *non segnalati***. Controlla l'allocazione dei canali in caso di transmissione *broadcast* (wifi)
	1.	*MAC*: indirizzo, determina a chi é indirizzato un "frame" di dati
	2.	*LLC*
3. **NETWORK**: controlla il funzionamento della sottorete di comunicazione, si occupa di *routing* e *forwarding*
	1. **Routing**: decidere il percorso migliore tra la sorgente e la destinazione (=*instradamento*)
	2. **Forwarding**: ricevere pacchetti e mandarlo al nodo corretto (=*inoltro*) 
4. **TRANSPORTO**: migliora le caratteristiche offerte dal livello di rete (network), es. con connessioni end-to-end
5. **SESSIONE**: definite regole per comunicazione inter-host, sessioni di lavoro
6. **PRESENTAZIONE**: rende compatibili le rappresentazione dei dati tra computer con codifica diversa, crittografia
7. **APPLICAZIONE**: livello piú vicino all'utente finale e opera direttamente sui software

**NB**. I livelli *sessione* e *presentazione* sono svolti se necessario dall'applicazione
**NB2**. Tutti i livelli, tranne forse quello *fisico*, sono soggetti a vulnerabilità.

### Servizi di un livello
I servizi che un livello offre ad uno superirore possono essere *affidabili* e *non affidabili*.
1. **Affidabili**: prevedono che l'entitá ricevente spedisca una PDU di conferma (acknowledgement,  ACK)
2. **Non Affidabili**: chi riceve non manda alcuna conferma

Possono essere poi orientati o non orientati alla connessione (*che non é il collegamento fisico*):
1. **Orientati**:
	- La connessione, una volta stabilita, svolge come un ***tubo digitale*** nel quale i dati trasmessi ***arrivano nello stesso ordine*** in cui sono partiti
	- Si tratta di una connessione point-to-point che deve essere deginita a priori
	- Analogia col sistema telefonico
2. **Non Orientati**:
	- Le PDU viaggiano indipendentemente le une dallle altre, possono prendere strade diverse ed ***arrivare in ordine diverso*** da quello di partenza (o non arrivare affatto)
	- Analogia col sistema postale

**NB1**. Servizio che é sia non affidabile che non orientato alla connessione é defininto *datagram*. 
**NB2**. TCP offre un servizio affidabile ed orientato alla connessione

### PDU (Protocol Data Unit)
![[pdu_scheme.jpg]]
**Ogni livello organizza i dati in unitá d'informazione (PDU) definite dal protocollo.** Le PDU vengono scambiate tra i vari livelli e in base a questi prendono nomi diversi:
1. **Messaggi** (livello *Applicazione*), include anche *Presentazione* e *Sessione*
2. **Segmenti** (livello *Trasporto*)
3. **Pacchetti** (livello *Rete*)
4. **Frame o Trame** (livello *Data Link*), hanno intestazione e coda per controllo dell'errore
5. **Bit** (livello *Fisico*)

Il **Payload (o Carico Utile)** è il dato da trasmettere ed è incapsulato più volte in vari tipi di pacchetti, aggiungendo dell'overhead ad ogni livello dello *stack di protocolli*.
Es. Nel livello *Data Link* il payload ha un header e un checksum finale.

### Tecnologie trasmissive della rete
1. **Broadcast**: le stazioni condividono un unico canale trasmissivo, **una sola stazione alla volta puó trasmettere**, tutte le altre *"sentono"*
2. **Point to Point**: connessione tra coppie di elaboratori, un pacchetto per arrivare alla destinazione puó attraversare piú elaboratori intermedi (routing). Non c'é bisogno di indirizzare il frame

### Differenza LAN e WAN
1. **LAN**
	- dimensione casalinga / campus
	- collegamenti gestiti da organizzazione **privata**
	- tipicamente broadcast
	- velocitá maggiore, probabilitá di errore minore
2. **WAN**
	- attraversa il suolo pubblico
	- dimensione variabile (fino "planetaria")
	- collegamenti tramite provider
	- tipicamente point-to-point
	- velocitá minori, probabilitá di errore maggiore

**NB**. Una WAN puó essere utilizzata per connettere piú LAN tra di loro

### Topologie di rete
![[topologie_rete.png]]

---
Fonti:
- [[Introduzione alle reti.pdf]]
- [Dispensa prof. Bongiovanni](http://wwwusers.di.uniroma1.it/Reti1/toc.html)
- [Modello ISO/OSI](https://www.isistassinari.edu.it/progettodicembre/reti/index.html)
- [Videolezioni prof. Wetherall](https://media.pearsoncmg.com/ph/streaming/esm/tanenbaum5e_videonotes/tanenbaum_videoNotes.html)