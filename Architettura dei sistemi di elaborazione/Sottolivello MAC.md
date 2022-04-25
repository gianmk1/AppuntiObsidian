# Sottolivello MAC
**MAC** = **Media Access Control**
Il sottolivello MAC è il più basso del livello Data Link.

Nelle reti **broadcast** il **mezzo trasmissivo è condiviso**: **una sola stazione alla volta può trasmettere**, se più stazioni trasmettono insieme si crea una **COLLISIONE**.

**NB.** Le **PDU del livello 2 (Data Link)** si chiamano **frame**. Il payload di un frame è un **pacchetto**.

##### Esempio di collisione:
![[esempio-collisione.PNG]]

**Spiegazione:**
Le due trame (o frame) bianche si sovrappongono alla grigia, anche se si rovinano i pochi bit a inizio o fine trama, comunque quest'ultima è da buttare.

### Protocolli MAC
I **protocolli MAC** **definiscono le regole di allocazione del canale**: per poter trasmettere, le stazioni devono applicare le regole del protocollo. 

I protocolli MAC si dividono in **statici** e **dinamici**.

#### Protocolli MAC statici
Prevedono un'allocazione statica del canale, **a priori si decide quale stazione deve trasmettere e quando**. Si utilizzano 2 metodi:
1. **TDM, Time Division Multiplexing :** viene assegnato uno **slot di tempo a ciascuna stazione**, il canale viene ripartito nel tempo. *Es. rete telefonica "digitale"*.
	![[time-division-multiplexing.PNG]]
2. **FDM, Frequency Division Multiplexing :** il canale viene diviso in varie **bande di frequenza**, **si può quindi trasmettere contemporaneamente** MA a **velocità ridotta**. Per ricevere dobbiamo porci su un frequenza specifica. *Es. Trasmissioni televisive*.
	![[frequency-division-multiplexing.PNG]]
	
#### Protocolli MAC dinamici
Le precedenti tecniche non sono applicabili alle reti poiché in queste la trasmissione tende ad essere **bursty**, cioè **ad impulsi**: *i computer quando sono collegati in rete non la usano di continuo, possono passare lunghi periodi senza la necessità di trasmettere. I protocolli statici rischiano di essere inefficaci nel lungo periodo*.

Si utilizzano dei protocolli dinamici (che **si adattano alle esigenze delle stazioni**) che possono essere:
1. **Deterministici**: **NON** possono verificarsi **collisioni**
2. **A contesa (o probabilistici)**: le collisioni **potrebbero verificarsi**, si cerca però di ridurne probabilità ed effetto 

**NB**. I protocolli moderni sono **a contesa**.

### Protocollo Token Ring
È un protocollo **dinamico deterministico**.

Le stazioni sono disposte ad anello:
- Quando nessuna stazione ha bisogno di trasmettere, queste fanno **girare nell'anello** un pacchetto chiamato **token** (o gettone)
- Quando una **stazione deve trasmettere deve avere e trattenere** questo *token*, finita la trasmissione lo rilascia alla stazione successiva.

![[token-ring.png]]

È stabilito comunque un **tempo massimo di trattenuta** del token.
A tutti viene data la possibilità di parlare e sapendo il numero di stazioni nell'anello si può definire il **tempo massimo di attesa** (sapendo il numero di stazioni) con la formula:
$(n - 1) * tempoMaxTrattenuta$

**NB**. Questo protocollo era utilizzato da IBM.

### Protocolli MAC dinamici a contesa
In questa categoria rientrano i due protocolli maggiormente utilizzati nelle reti locali:
- **CSMA / CD**: rete 802.3, 802.3u e successive varianti
- **CSMA / CA**: rete 802.11

*In questi due protocolli le connesioni potrebbero avvenire, si cerca di evitarle.*

### Standard IEEE 802.x
Lo studio del sottolivello MAC si intreccia con lo studio degli standard di rete locali.

802.3 : utilizzato nelle reti cablate
802.11 : utilizzato nelle reti wireless (nelle reti locali)

**IEEE 802.x** è una famiglia di standard, soprattutto per le reti locali, che è parzialmente sovrapponibile al livello OSI:

802.2 -> LLC, dello stack OSI
802.3 -> Sottolivello MAC e livello Fisico

**NB**. *Una rete 802.3 non si può collegare facilmente ad una 802.11, a meno che non si hanno dei dispositivi appositi.*

![[standard-802x.PNG]]

## Protocollo CSMA / CD ????????????????????
Acronimo di *Carrier Server Access with Collision Detection*, in italiano *Accesso multiplo con rilevamento della portante e della collisione*.

**NB**. La **portante** è un segnale di base su cui **applicando delle varizioni** (anche dette **Modulazioni**, come la frequenza) si **determina** **se** quel segnale **sta trasmettendo 0 o 1**.

Prima di trasmettere, la stazione ascolta il canale (Fase 1: CS):
- Se è **LIBERO** **trasmette subito**
- Se è **OCCUPATO** **aspetta** che il canale si liberi e poi inizia a trasmettere

*Le collisioni però possono comunque verificarsi, poichè **il segnale ci mette del tempo a propagarsi**.*

**NB**. Per monitorare la rete e rilevare gli errori serve un **adattatore**.

#### Fase 1: CS (Carrier Sense)
Rilevazione della trasmissione: ogni **stazione** che deve trasmettere **ascolta il canale**, se è libero trasmette, se è occupato attende che il canale si liberi.
- **Se è libero trasmette**
- **Se è occupato aspetta che il canale si liberi**

![[carrier-sense.jpg]]

#### Fase 2: MA (Multiple Access)
Si possono verificare 2 problemi:
1. Una stazione A trasmette, e **prima che il suo segnale arrivi a B anche B inizia a trasmettere** (vedendo ancora il canale libero), dunque si verifica una collisione. C'è quindi un **periodo di vulnerabilità**.
2. A e B ascoltano contemporaneamente durante la trasmissione di C, e non appena quest'ultima termina **iniziano entrambe a trasmettere**: anche in questo caso si verifica una collisione
Supponiamo che **B** si metta in ascolto e attende che il canale si liberi, questo lo potrebbe fare, per esempio, anche **C**. Finito il periodo di vulnerabilità **entrambe iniziano a trasmettere** creano così una **collisione**.

![[csma-cd-collision.jpg]]

#### Fase 3: CD (Collision Detection)
La **stazione** mentre trasmette continua ad ascoltare il canale, **se rileva una collisione**:
1. **Immette** nel canale una **sequenza di JAMMING**, per dire a tutte le stazioni che c'è stata una collisione
2. **Interrompe la trasmissione** del frame, e quindi liberare il canale
3. **Riprova a trasmettere il frame dopo un intervallo casuale di tempo** scelto attraverso l'*Algoritmo di regressione binaria esponenziale*, sperando che non ci sia una nuova collisione

**NB**. Rilevare la collisione e provare gestirne gli effetti serve per **gestire gli effetti**.

## 802.3 : Carattesistiche fisiche
- Velocità **10 Mbit/s**
- Collegamenti:
	- Cavo coassiale **thick** (10base5)
	- Cavo coassiale **thin** (10base2)
	- **HUB (multiport repeater)** + **cavo UTP** (10baseT)
- Codifica di **Manchester**
- Diametro massimo **2500 metri** (il cavo coassiale tra 2 stazioni non poteva essere più lungo di 2.5km)

![[schema-rete-802-3.PNG]]

Questo standard è stato nel tempo restaurato creano varie "sottoversioni", un esempio è la 802.3u con velocità 100 Mbit/s.

##### Cavo coassiale
Un cavo coassiale è fatto da un **core metallico**, uno strato isolante, una **guaina metallica** ed un altro strato isolante. Il segnale viene preso come **differenza di potenziale** tra filo e guaina metallica.

![[cavo-coassiale.png]]

### 802.3 : Struttura del frame
I dati vengono organizzati in un **frame** (o trama) fatta da:

![[struttura-frame-802-3.PNG]]

- **Preambolo**: 7 byte tutti uguali che consentono al ricevitore di **sincronizzare il suo clock** con quello del trasmettitore, così da capire quando è 0 e quando 1 (**sincronismo di fase**).
- **Start of frame**: 1 byte delimitatore 
- **Indirizzo sorgente**: 6 byte
- **Indirizzo destinatario**: 6 byte
- **Lunghezza dei dati**: 2 byte che indicano la lunghezza dei dati trasmessi
- **Dati LLC**: anche detto **payload**, sommato al PAD, può essere di un intervallo compreso tra 46 e 1500 byte. Questo limite è impostato poiché frame troppo grandi:
	1. **Impediscono** alle altre stazioni di **trasmettere**
	2. C'è un maggior **rischio di collisione**
- **PAD**: è un "cuscinetto" che serve, nel caso di frame minori di 46 byte, a portarli alla **lunghezza di minima (64 byte)**
- **Checksum**: codice CRC per verificare l'integrità del frame

#### 802.3 : Lunghezza minima del frame
La trama 802.3 ha una lunghezza minima di 64 byte così da far durare la **trasmissione almeno 51,2µs** e **garantire così che l'eventuale collisione venga rilevata**.
Bisogna garantire che la trasmissione venga rilevata anche nel caso peggiore (2 volte il tempo di propagazione del segnale da un capo all'altro).

#### 802.3 : Algoritmo di regressione binaria esponenziale
Se la stazione mentre sta trasmettendo rileva una collisione **NON è in grado di definire quante e quali stazioni sono state coinvolte** in quest'ultima. 
Per questo, **ciascuna stazione coinvolta nella collisione**:
1. Dopo la prima collisione, **discretizza il tempo in slot di 51,2µs**
2. **Decide se provare a ritrasmettere subito o al prossimo slot di tempo**. *Es con 2 stazioni: se entrambe trasmettono subito o entrambe aspettano il prossimo slot ci sarà nuovamente una collisione, in questo caso c'è quindi un 50% di possibilità di una seconda collisione*
3. In caso di **seconda collisione** le **stazioni allargano il tempo a 4 slot**, la stazione può ora decidere se trasmettere subito, dopo 1 slot, dopo 2, slot o all'ultimo slot. La probabilità di una nuova collisione dimezza rispetto il caso precedente.
4. In caso di **n** collisioni consecutive, la **stazione sceglie casualmente nell'intervallo**
	$0 <= r <= 2^k -1$, con $k = min (n, 10)$
5. **Dopo 16 collisioni** consecutive, la **stazione rinuncia a trasmettere**

**NB**. Se avvengono molti collisioni probabilmente c'è molto traffico.

## 802.3u : Caratteristiche fisiche
- Velocità **100 Mbit/s**
- Collegamenti:
	- **HUB (multiport repeater)** + **cavo UTP** (10baseT)
- Codifica di **MLT-3**
- Diametro massimo **200** metri

Le **caratteristiche del Sottolivello MAC sono le medesime dell'802.3**, cambiano alcune caratteristiche al Livello Fisico: non c'è più supporto al cavo coassiale.

**NB**. Il diametro della rete è diminuito molto poiché il frame di 64 byte ora si trasmette ad una velocità di **5,12µs** (non più 51,2µs).

## Bridge
Sono dispositivi che operano al Livello Data Link e hanno più scopi:
1. **Interconnettere reti di tipo diverso**
2. Interconnettere reti dello stesso tipo, allo scopo di **separare i domini di collisione** e/o **aumentare il diametro massimo della rete**

##### Esempio 1 : Access Point
*Serve per mettere in comunicazione una rete 802.3 e una rete 802.11 (wi-fi)*

Se riceve un frame 802.11 indirizzato ad una stazione della rete 802.3 l'AC deve:
1. **Cambiare il formato del frame**
2. Trasmettere nella rete 802.3 **applicando il protocollo e le regole di questa rete** (CSMA/CD)

*Nel caso di un frame indirizzato ad una rete 802.11 si applica lo stesso metodo*

![[access-point.jpg]]

##### Esempio 2 : Switch
*Utilizzato per segmentare una rete 802.3 e per aumentarne il diametro*

Può essere visto come un **bridge multiporta**, serve per trasmettere da una rete A ad una rete B utilizzando le regole del **protocollo CSMA/CD**.

Alcune note:
- Quando lo si accende, finché non impera chi e dove è, trasmette in broadcast (come un hub)
- Nelle reti che utilizziamo solitamente, le stazioni vogliono comunicare con i router e i server, non tra di loro, i **flussi vanno quindi verso delle rotte privilegiate**.
- Nelle reti ci sono stazioni che generano frame con indirizzo broadcast e quindi gli switch devono trasmettere ovunque come se fossero degli hub

## Backward Learning
Nel momento in cui lo **switch** viene attivato, **costruisce le proprie tabelle di inoltro**, in base ai frame che riceve su ciascuna porta, per sapere dove trasmetterre.

Grazie a queste tabelle dopo un po'di tempo lo switch sfrutterà meglio anche la **segmentazione**.

##### Funzionamento
*Ogni frame contiene nell'intestazione l'indirizzo della stazione sorgente. Questo consente al bridge (o switch) di sapere da quale porta si può raggiungere la stazione che lo ha inviato.*

Quando un frame arriva allo switch:
- Se l'indirizzo di destinazione è nelle tabelle di inoltro, il **frame viene inviato sulla porta corrispondente**
- Se l'indirizzo di destinazione NON è nelle tabelle di inoltro, il frame viene inviato in **broadcast** su tutte le porte tranne quella di provenienza.

**Le tabelle di inoltro vengono aggiornate ogni tot minuti**, rimuovendo gli indirizzi che non sono più attivi.

##### Esempio
![[backward-learning.PNG]]

## Spanning Tree
Gli **switch** hanno un **comportamento broadcast** quando:
- **Appena accesi per imparare i percorsi**: switch e bridge trasmettono in broadcast utilizzando comunque il sottolivello MAC e attendendo che il canale sia libero per trasmettere (NB. Diverso dal broadcast del Livello Fisico)
- Il **frame contiene un indirizzo di destinazione broadcast**, per cui va mandato a tutta la rete

##### Il problema degli ANELLI
Gli switch in una rete LAN potrebbero formare degli **ANELLI (o loop)** nei collegamenti che possono provocare la trasmissione all'infinito di un frame.

A volte però gli anelli si creano:
1. **Per ridondanza**, nel caso uno switch si rompa
2. **Per errore**

Si vuole evitare quindi che l'eventuale presenza di anelli nella rete provochi problemi:
Gli switch sono quindi in grado di **"eliminare gli anelli" definendo uno Spanning Tree**, cioè un **sottoinsieme dei collegamenti**:
- **senza anelli** (i collegamenti formano quindi un **albero**) 
- che **raggiunge tutti gli switch** della rete.

##### Definire lo Spanning Tree
Per definire lo spanning tree si seguono 3 passi:
1. Definire il **root switch**, cioè lo switch con l'indirizzo MAC più basso
2. Lo spanning tree cresce aggiungendo via via gli switch che hanno distanza minore dal root
3. Le porte che non appartengono allo spanning tree vengono disabilitate

##### Funzionamento Spanning Tree
1. Gli switch **cominciano senza informazioni** o configurazione iniziale
2. Gli switch **lavorano in parallelo** tra di loro
3. Gli switch **cercano in continuazione la migliore soluzione**, adattandosi ogni volta a modifiche nella rete
4. Per fare ciò, **mandano in continuazione aggiornamenti sulla propria configurazione** contenenti:
	- Il **proprio indirizzo**
	- L'**indirizzo** di quella che **credono sia la root**
	- La **distanza tra loro e la root**
5. **Ad ogni aggiornamento** si **verifica** se c'è una **radice migliore** (quindi un indirizzo minore) o un **percorso minore**.

*All'inivio di un frame, **ogni switch lo manda soltanto agli altri che sono direttamente collegati ad esso** secondo lo Spanning Tree attuale.*

##### Esempio
![[spanning-tree.png]]

## 802.11 : La rete wi-fi
Gestire il **protocollo MAC nella rete wifi è molto più complicato** che nella rete cablata poichè:
1. Le **stazioni** possono avere **diverse aree di copertura** in relazione alla loro posizione
2. **NON è possibile rilevare collisioni mentre si sta trasmettendo**. 
	**NB**. Ascoltando il canale mentre trasmette, la stazione, sentirebbe solo la sua trasmissione.
3. Le reti wifi sono utilizzate da **dispositivi** mobili che **tendono a cambiare spesso nel tempo**

### 802.11 : Stazione nascosta
![[img-staz-nascosta.PNG]]
*Intendere l'HUB come Access Point*

La portata di un'antenna si rappresenta come una sfera, i cerchi in figura rappresentano le varie portate delle stazioni.

- A può sentire quello che l'AP (Access Point) trasmette e viceversa
- B può sentire quello che l'AP trasmette e viceversa
- A NON raggiunge B e viceversa

##### Esempio
![[img2-staz-nascosta.PNG]]
- A sta parlando con B
- C ascolta il canale e lo sente libero
- C comincia a trasmettere
- Nella zona in cui si trova B si verificherà una collisione

*La stazione A è quindi nascosta rispetto ad A*

- **B** sta "**parlando**" con l'AP
- **A** ascolta il canale e lo **sente libero**
- **A** inizia a **trasmettere**
- Nella zona in cui si trova l'AP si verifica una **collisione**

*La stazione B è quindi **nascosta rispetto ad A**.*

### 802.11 : Stazione esposta
![[img2-staz-esposta.PNG]]

- B sta trasmettendo ad A
- C vuole trasmettere a D
- **C sentirà la trasmissione di B e concluderà erroneamente di non poter trasmettere**
- Invece, essendo D fuori dalla portata di B, ed A fuori dalla portata di C, **le due trasmissioni potrebbero avvenire parallelamente senza interferenze**

 **C** è la stazione esposta nella portata di **B**

### 802.11 : Livello Fisico
**Si utilizzano bande di frequenza diverse e si usano anche delle tecniche di modulazione per variare l'ampiezza** (es. OFDM).

In 802.11 vengono usati canali la cui dimensione varia da 20 a 40 MHz:
- 802.11 b/g/n trasmettono usando bande di frequenza di circa 2.4 Ghz
- 802.11 a/n trasmettono usando bande di frequenza di circa 5 Ghz

### 802.11 : Sottolivello MAC
- Il **protocollo utilizzato è il CSMA / CA**, cercando quindi di evitare le collisioni
- La **trasmissione è affidabile** (con un ACK di risposta) **tramite ARQ** (Automatic Repeat reQuest), per evitare la perdita di frame
- I frame hanno 3 indirizzi:
	- Indirizzo sorgente
	- Indirizzo destinazione
	- Indirizzo Access Point
- I **frame indicano la propria durata con cui occuperanno il canale**, anche per ricevere l'ACK
- altro, es. Crittografia (WPA / WPA-2) 

**NB**. *Perchè nell'802.3 non è previso il riscontro e invece nella 802.11 si? Nell'**802.3** si "intercetta" la **collisione** e le stazioni **sanno che c'è stata**. Con l'**802.11** quando si trasmette un frame **non c'è modo di sapere se c'è o meno stata la collisione**: serve **quindi** un **ACK**.*

### 802.11 : CSMA / CA
![[scheme-csma-ca.PNG]]

- **Prima di trasmettere si ascolta se il canale è libero**
- Quando il canale è libero **NON si trasmette subito** ma **ogni stazione sceglie un intervallo di tempo** (**backoff**) per cui ciascuna di esse deve attendere prima di cominciare a trasmettere
- La **stazione che riceve** il frame **risponde con un ACK**

Questo **meccanismo** serve **per evitare le collisioni intervallando il tempo in cui le stazioni possono trasmettere** appena il canale è libero.

## Virtual LAN (VLAN)
Il protocollo VLAN consente di **separare la topologia fisica** della rete **dalla** sua **topologia logica**. Questo rende **possibile** **realizzare** due o **più reti virtuali separate sulla stessa infrastruttura fisica**, senza necessità di duplicazione degli apparati.

Questo può essere utile per:
- **SICUREZZA**: rendere ciascuna rete disponibile solamente ad una specifica utenza, limitando così il rischio di attacchi / fughe di dati / ...
- Non è detto che in si possa sempre separare le reti, anche per evitare la continua duplicazione degli apparecchi

![[virtual-lan.PNG]]

La Virtual LAN permette di separare la rete fisica in 2 o più virtuali in modo che **le stazioni collegate ad una VLAN non possano interagire con quelle dell'altra rete virtuale**.

### VLAN : Funzionamento
- Ogni VLAN è considerata dagli switch come una rete locale separata dalle altre
- Lo switch sa a quali VLAN appartengono le sue porte mediante una tabella nota e configurata
- I frame appartenenti ad una VLAN possono essere instradati solo sulle porte appartenenti a quella VLAN
- Lo switch mantiene tabella di instradamento separate per ogni VLAN, diventa quindi uno "switch multiplo"
- Le porte utilizzate per connettere 2 switch in cui passa il traffico di due VLAN, devono avere doppia mappatura

### VLAN : VLAN-Tagging
Quando un **frame va inoltrato verso una porta con doppia mappatura**, a esso viene **aggiunto un tag in cui si specifica la vlan di appartenenza**. Questo frame diventa di tipo **802.1Q**

![[802-1-q-frame.jpg]]

---
Fonti:
- [[Architettura dei sistemi di elaborazione/PDF/Sottolivello MAC.pdf]]
- [Dispensa prof. Bongiovanni](http://wwwusers.di.uniroma1.it/Reti1/Cap2.pdf)
- [Dispensa prof. Bongiovanni pt.2](http://wwwusers.di.uniroma1.it/Reti1/Cap4.pdf)
- [Riassunto prof. Lucarelli](http://www.pierolucarelli.it/reti%20informatiche/reti%20bongiovanni1/Cap4a/Cap4a.html)
- [Rete 802.11](http://www.benve.org/Download/Wireless.pdf)