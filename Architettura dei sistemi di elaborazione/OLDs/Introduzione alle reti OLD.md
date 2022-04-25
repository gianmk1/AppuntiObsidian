# Introduzione alle reti

1. Application
2. Transport
3. Network
4. Data Link
5. Fisico

Stratificaioni di livelli, *"dividi et impera"*
Livello offre servizi al livello n+1, e usa il servizi di n-1, si verifica *overhead* (vedi sotto)

## Definizioni:
- *Entitá*: insieme di hardware e software che realizza i compitidi un livello
- *Interfaccia*: insieme delle regole di comunicazione tra entitá di livelli adiacenti 
- *Protocollo*: regole di comunicazione tra entitá di pari livello
- *Overhead*: 
- *PDU (Protocol data unit)*: ogni livello organizza i dati in unitá, definite dal protocollo. Hanno nomi specifici ai diversi livelli:
	1. messaggi (applicazione)
	2. segmenti (transporto), anche detto payload **???**
	3. pacchetti (rete)
	4. frame o trame (data link), hanno intestazione e coda (per controllo dell'errore)

		--INSERIRE IMMAGINE--

- *Router* : é un qualsiasi nodo della rete che ha almeno 2 interfacce ed é disposto a svolgere una funzione di inoltro, con software di rete implementato fino al livello 3
- *Host*: nodo della rete che ha un solo collegamento alla rete 

### Compiti
1. di *Basso livello* : svolti da hardware dedicato (es. scheda di rete)
2. di *Alto livello* : svolti dal software

### Protocolli
![[protocolli.PNG]]
1. Applicazione (es. http)
2. Transporto
3. Internet
4. Link

### Livelli ISO/OSI
1. application
2. presentation
3. session
4. transprt
5. network
6. data link
7. fisico

--PEZZO MANCANTE--
1. FISICO: 
2. DATA LINK: si occupa della gestione del flusso e degli errori, deve garantire una linea di trasmissione priva di errori _non segnalati_. Controllo allocazione del canale nel caso di *broadcast* (wifi)
	- MAC (indirizzo, determina a chi é indirizzato un "frame" di dati)
	- LLC
3. RETE: controlla il funzionamento della sottorete di comunicazione, si occupa di _routing_ e _forwarding_
	- *routing*: decidere percorso tra sorgente e destionazione (=inoltro)
	- *formarding*:  ricevere pacchetti e mandarli nella direzione corretta (=instradamento)

NB. 
Livello LINK (host to network) svolge gli stessi compiti di *fisico* + *data link*
Livello INTERNET corrisponde al livello di *network*

Livello di TRANSPORTO é il primo in cui é possibile ad un collegamneto fisico tra 2 nodi non collegati. 

Livello SESSIONE: comunicazione inter-host, sessioni di lavoro
Livello PRESENTAZIONE: rappresentazione dei dati, crittografia.
Questi 2 livelli sono svolti, se necessario, dalla applicazione.

### Servizi di un livello
I servizi che un livello offre ad uno superirore possono essere *affidabili* e *non affidabili*.
1. **Affidabili**: prevedono che l'entitá ricevente spedisca una PDU di conferma (acknowledgement,  ACK)
2. **Non Affidabili**: chi riceve non manda alcuna conferma

Possono essere poi orientati o non orientati alla connessione (che non é il collegamento fisico):
1. **Orientati**:
- Analogia col sistema telefonico
2. **Non Orientati**:
- PDU viaggiano indipendentemente le une dallle altre, possono prendere strade diverse ed arrivare in ordine diverso da quello di partenza (o non arrivare affatto)
- Analogia col sistema postale

NB. Servizio che é sia non affidabile che non orientato alla connessione é defininto *datagram*. 
TCP offre un servizio affidabile ed orientato alla connessione

#### Tecnologie trasmissive della rete
1. *Broadcast*: 
2. *Point to Point*: non c'é bisogno di indirizzare il frame

### Differenza LAN e WAN
1. **LAN**
	- dimensione casalinga / campus
	- maggiore velocitá di trasmissione
	- meno probabilitá di errori
2. **WAN**
	- attraversa il suolo pubblico
	- dimenzione variabile (fino "planetaria")
	- collegamenti tramite provider
	- velocitá minori, probabilitá di errore maggiore

**NB**. Una WAN puó essere utilizzata per connettere piú LAN tra di loro

### Topologia di rete

-- INSERISCI IMMAGINE --



ISO/OSI | TCP/IP
--------|--------
Application|Application
Presentation|
Session|
Transport|Transport
Network|Internet
Data Link|Link
Fisico|Link

![[modelli_riferimento_reti.png]]

----

# Livello fisico

### Segnali (livello FISICO)
Un segnale è una grandezza fisica che varia nel tempo alla cui variazione è associato un contenuto di informazione. Es. tensione elettrica variabile tra -5V e 5V

#### Trasmissione dei segnali
*Si parte da un qualcosa che varia*. Quando il segnale viene trasmesso questo si propaga ad una certa velocità. Ci vuole un tempo *finito* perché il segnale si propaghi.

#### Analisi armonica: il LA del diapason
Il LA ha una frequenza costante di 440Hz, il suo **spettro**...

**Spettro**: i segnali possono essere visti come somma di tante componenti sinusoidali, ciascuna con *frequenza diversa* (multiple di una frequenza "base"), hanno *ampiezze diverse* e possono avere fasi diversi. L'analisi armonica consiste nel studiare queste sinusoidi
![[immagine sinusoide]]

### Un segnale e il suo spettro di frequenze
![[immagine spettro segnale]]

#### Banda passante

I mezzi trasmissivi hanno una **banda passante**: il mezzo trasmissivo riesce a trasportare le componenti di frequenza di un segnale fino a (es. 10mHz), e quelle sopra le taglia. 
Dobbiamo capire se la banda passante del dispositivo è coerente con lo spettro del nostro segnale

Ci deve essere coerenza tra la banda del segnale che voglio trasmettere e la banda passante del mezzo trasmissivo.

![[inserire foto della slide n39]]

### Teorema di Nysquist

Il massimo bit rate di un canale di comunnicazione dotato di una banda passante da 0Hz a B Hz (passa-basso di banda B) che trasporta un segnale consistente di V livelli discreti è:

![[inserire formula]]

(logaritmo base 2 di 2)

Questo non tiene conto del rumore, che può disturbare ulteriormente il segnale.

Legame tra banda passante del mezzo trasmissivo e velocità di trasmissione.
Poca banda comporta poca velocità di trasmissione
