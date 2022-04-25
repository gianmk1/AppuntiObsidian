# Sottolivello MAC

MAC = Media Access Control
È il sottolivello più basso del livello datalink.

NB. Con il broadcast solo una stazione per volta può trasmettere, se più stazioni trasmettono insieme si crea una **COLLISIONE**

Le PDU del livello 2 (datalink) si chiamano **frame**
Il payload di un frame è un pacchetto

![[schema della collisione]]

*Spiegazione:* Le due trame bianche si sovrappongono (anche se di poco) alla grigia, anche si rovianano pochi bit a inizio o fine trama, comunque quest'ultima è da buttare

I protocolli MAC definiscono le regole di allocazione del canale: se vogliamo transmettere quali regole dobbiamo utilizzare (es. quali devono utilizzare le stazioni):

Protocolli MAC si dividono in **statici** e **dinamici**:

#### Protocolli MAC Statici
- **Statici**: allocazione statica del canale, a priori si decide quale stazione deve trasmettere e quando. Può essere fatta assegnando ad ognuno uno slot di tempo (TDM, time division multiplexing: il canale viene ripartito nel tempo, un esempio è la rete telefonica "digitale").
	Poi c'è  il FDM, allocazione statica del canale diviso in bande di frequenza, possiamo trasmettere però a velocità ridotta. Per ricevere ovviamente dobbiamo porci su una frequenza specifica
	
#### Protocolli MAC Dinamici
Le precedenti tecniche non sono applicabili alle reti, perchè in queste la trasmissione tende ad essere **bursty**, cioè ad impulsi, disomogeneo: i computer quando sono collegati in rete non la usano in continuo, possono passare lunghi periodi senza la necessità di trasmettere. I protocolli statici rischiano di essere inefficati nel lungo periodo magari non ho possibilità di trasmettere... oppure trasmetto e tengo occupato il canale al posto degli altri inutilmente

![[vedi schemi multiplexing - FDM - ...]]

![[grafico blu-rosso-verde]]
Spiegazione: 
entrambe le stazioni hanno una velocità massima di trasmissione, non sempre però trasmettono a questa velocità. Sommando i 2 segnali si vede che la velocità massima che si ottiene è minore della loro singola velocità X 2


Con protocolli MAC dinamici si cerca di assegnare il canale alle stazioni le quali hanno bisogno in quel momento. 
Ci saranno dei momenti ovviamente in cui molte stazioni dovranno trasmettere

Tutto ciò porta ad utilizzare protocolli **dinamici** (adattarsi alle esigenze delle stazioni) che possono essere:
- **deterministici**: non possono verificarsi collisioni
- **a contesa** (o probabilistico): le collisioni potrebbero verificarsi, si cerca di ridurre la probabilità e l'effetto

**NB**. I protocolli moderni sono solo **a contesa**.

##### Token Ring
È un **protocollo dinamico deterministico**, stazioni disposte ad anello, quando nessuna ha bisogno di trasmettere le stazioni fanno girare nell'anello un pacchetto chiamato **token**, quando una deve trasmettere deve avere e trattenere questo "gettone", quando ha finito di trasmettere lo ripassa.

È stabilito comunque un **tempo massimo** di trattenuta del token.
A tutti viene data la possibilità di parlare e sapendo il numero di stazioni nell'anello possiamo sapere il **tempo max di attesa**, con la formula: 
`(n-1)*tempomax_trattenuta`

**NB**. Questo protocollo era utilizzato da IBM
<br>

#### Protocolli MAC dinamici a contesa
2 protocolli molto utilizzati nelle rete locali:
- CSMA/CD (rete 802.3 e 802.3u e successive varianti)
- CSMA/CA (rete 802.11), usato nelle reti wireless

In questi 2 le collisioni potrebbero accadere, si cerca però di evitarle.

### Standard IEEE 802.x
![[vedi schema sulla slide]]

In realtà lo studio del sottolivello mac si intreccia con lo studio degli standard di rete locali.

802.11 utilizzato nelle reti wireless quando parliamo di reti locali
802.3

802.11 e 802.3 sono standard che occupano sotto livello fisico e sottlivello MAC

IEEE 802.X è una famiglia di standard, soprattutto per le reti locali, che è parzialmente sovrapponibile al livello OSI:

802.2 -- LLC (dello stack OSI)
802.3 -- Sottolivello MAC e Livello FISICO

Una rete 802.3 non si può collegare facilmente ad una 802.11, a meno che non si hanno dei dispositivi appositi

### 802.3: caratteristiche fisiche
È stato "restaurato", quando è nato la velocità di 10Mbit/s era molto. Per cui sono state fatte altre "sottoversioni", la 802.3u è quella che attualmente va per la maggiore (100 Mbit/s)


- velocità 10 Mbit/s
- collegamenti:
	- cavo coassiale thick (10base5), non di facile installazione
	- cavo coassiale thin (10base2)
	- hub (multiport repeater) + cavo UTP (10 base T)
- codifica di Manchester (modo di codificare i bit)
- diametro massiamo della rete 2500m


Le nuove forme di cablaggio sono state aggiunte via a via, un cavo coassiale è fatto da un core metallico, uno strato di isolante, una guaina metallica e un altro strato di isolante.
Il segnale è preso come differenza di potenziale tra il filo e la guaina metallica.

Il cavo coassiale tra 2 stazioni non poteva essere più lungo 2.5km

Queste caratteristiche descritte sopra sono tutte di livello FISICO

**NB**. Lo standard 802.3 ha preso le caratteristiche di una trasmissione wireless alle isole hawaii e ha preso il nome di ethernet ???


### Come funziona il protocollo CSMA/CD
*Carrier Server Multiple Access with Collision Detection*, in italiano: Accesso multiplo con rilevamento della portante e della collisione

NB.		La portante è un segnale di base su cui applicando delle variazioni (anche 						            dette MODULAZIONI, *es.* di Frequenza) si determina se quel segnale sta 	            trasmettendo 0 o 1. 

Prima di trasmettere, la stazione ascolta il canale:
- Se è LIBERO trasmette subiot
- Se è OCCUPATO la stazione deve aspettare che il segnale si liberi e poi può trasmettere

Le collissioni però comunque possono verificarsi poichè: il segnale ci mette del tempo a propagarsi. Ecco 2 situazioni per le quali avviene comunque una collisione:

1. Detto **CS?**.  Il segnale ci mette del tempo a propagarsi. A potrebbe aver già iniziato a trasmettere ma B potrebbe a sua volta cominciare a trasmettere poichè vede il canale ancora LIBERO. C'è un PERIODO di VULNERABILITÀ. 
2. Detto **MA?**. Supponiamo che B si metta in ascolto, in attesa che il canale si liberi, questo lo fa, per esempio, anche C. Finito il periodo di vulnerabilità entrambe iniziano a trasmettere, creando così una COLLISIONE

##### Cos'è allora il /CD?
La stazione mentre trasmette continua ad ascoltare il canale, se rileva una collisione: 
1. Immette nel canale una sequenza di jamming
2. Interrompe la trasmissione del frame
3. Riprova a trasmettere il frame dopo un intervallo casuale di tempo scelto con l'*algoritmo di regressione binaria esponziale*.

NB. C'è un dispositivo che rileva le collisioni

*Spiegazione:*

2. Se c'è una collisione è inutile continuare a trasmettere, quindi liberiamo il canale.
3. La stazione si fa carico di ritrasmettere il frame, dopo un intervallo casuale di tempo, nella speranza che non succeda di nuovo una collisione.

NB. Rilevare la collisione e in un qualche modo gestirla serve per **gestirne gli effetti**.

1. La sequenza di jamming serve per dire a tutti che c'è stata una collissione e che biognerà ritrasmettere.

### La TRAMA
I dati sono organizzati in una **trama** fatta di:

![[inserisci schema trama]]

1. parte iniziale di 8 byte: servono a stabilire il **sincronismo di fase**, cioè a sapere l'esatta posizione di dove cominciano i bit; a capire dove sono i salti di fase, così da capire quando è 0 e quando 1.

	NB. **Periodo di cifra**: a metà del periodo di cifra c'è sempre un **salto di fase**
	![[inserisci schema]]
2. 6 byte dell'indirizzo sorgente
3. 6 byte dell'indirizzo di destinazione. Siamo in un mezzo broadcast dove la trama viene "sentita da tutti" ma ascoltata solo dall'indirizzo di destinazione
4. 2 byte che indicano la lunghezza dei dati
5. Dati LLC o anche detti Payload, con dimensione max di 1500 byte e min di 46 byte. C'è un max di 1500byte perchè frame troppo grandi **impediscono** alle altre stazioni di trasmettere e c'è un maggior rischio di collisione. NB. Min e Max sono riferiti a Payload+PAD
6. PAD è un "cuscinetto" che serve nel caso di invio di trame di dimensioni troppo piccole (<46byte)
7. in coda c'è una cheksum per verificare l'integrità del frame

*Perchè la trama non può essere più corta?*
Serve per far durare la trasmissione almento 51,2 us e garantire che l'eventuale collisione venga rilevata. Bisogna che la trasmissione sia abbastanza lunga da essere rilevata anche nel caso PEGGIORE cioè 2 stazioni agli estremi opposti 

![[vedi schema sulla slide]]

Il tempo necessario a rilevare collissione nel caso peggiore possibille è 51,2us.
NB Nell 802.3 con i ripetitori al massimo possiamo avere una rete di diametro 2.5km.

### Algoritmo di regressione binaria esponenziale
Se la stazione stava cercando di trasmettere e rileva una collisione non è in grado di sapere quante e quali stazioni sono state coinvolte nella collisione.
Ciascuna delle stazioni coinvolte nella collisione quindi:
- dopo la prima collisione **discretizza** il tempo in **slot** di 51.2 us
- decide se provare a trasmettere subito o al prossimo slot, vuol dire che (es. 2 stazioni) se entrambe trasmettono subito o entrambe aspettano il prox slot: ci sarà una seconda collisione, in questo caso c'è quindi il 50% di possibilità di una seconda collisione
- In caso di seconda collisione le stazioni allargano il tempo a 4 slot (la stazione può quindi decide di trasmettere subito, dopo 1 slot, dopo 2 slot o all'ultimo slot), la probabilità di una nuova collisione quindi dimezza rispetto al caso precedente
- in caso di n collisioni consecutive sceglie casualmente nell'intervallo
	- ![[vedi_formula_sulla_slide]]
- dopo 16 collisioni consecutive, la stazionerinuncia a trasmettere 

NB. Se ci sono tante collisioni porbabilmente avvengono perchè c'è molto traffico


### 802.3u: caratteristiche fisiche
- velocità di 100Mbit/s
- collegamenti:
	- hub (multiport repeater) + cavo UTP (10 base T)
- codifica di MLT-3
- diametro massimo 200 metri

Le caratteristiche del sottolivello MAC sono le medesime dell 802.3, cambiano però alcune cose al livello fisico.
Non supporta più il cavo coassiale.
Il diametro della rete è diminuito molto poichè la trama di 64 byte ora si trasmette in 5.12us (non più in 51.2us).

*Invece di abbandonare l'802.3 a suo tempo si è deciso di migliorarlo*
*NB.* L'hub trasmette a tutti, si parla sempre quindi di una trasmissione broadcast

#### Bridge
È un dispositivo che opera al livello 2 e ha vari scopi:
1. l'interconnesione di reti diversi
2. interconnettere reti dello stesso tipo, allo scopo di separare i domini di collisione e/o comunque ...

Un esempio della prima tipologia è l'ACCESS POINT:

#### Access Point
Per mettere in comunicazione una rete 802.3 e una rete 802.11 (wifi)

Se riceve un frame 802.11 indirizzato ad una stazione della rete 802.3 deve:
- cambiare il formato del frame
- trasmettere nella rete 802.3 applicando il protocollo e le regole di questa rete  (CSMA/CD)

Con un frame indirizzato a rete 802.11 viceversa

### Segmentazione
Cos'è e come funziona

## Switch
Può essere visto come un bridge multiporta. Serve per:

Switch deve trasmettere da rete A a rete B utilizzando le regole del protocollo CSMA/CD. Una volta che il frame ha raggiunto lo switch sarà quest'ultimo a trasmettere all'altra rete

Alcune note:
- Quando si accende lo switch, finche non impara chi e dove è, trasmettere in broadcast (come un hub)
- Nelle reti che utilizziamo noi solitamente le stazioni vogliono comunicare con i router e i server, non tra di loro. **I flussi vanno verso delle rotte privilegiate**
- Nelle reti ci sono continui stazioni che generano frame con indirizzo broadcast e quindi gli switch devono trasmettere ovunque come se fossero hub.

### Backward learning
Gli switch hanno delle **TABELLE DI INOLTRO** per sapere dove trasmettere, in base al frame che riceve su ciascuna porta. Si parla di **transparent bridge** quando ...

Queste tabelle quando lo switch viene accesso sono VUOTE, lo switch impara grazie ai frame che riceve. Grazie a questo dopo un pò di tempo sfrutterà meglio la **segmentazione**.

NB Lo **switch** non deve essere configurato dall'amministratore di rete

Ogni frame contiene nell'intestazione l'indirizzo della sorgente


Mano a mano che le stazioni trasmettono il frame può aggiungere la conoscenza di dove sono quelle stazioni alle proprie tabelle di inoltro

Quando un frame arriva allo switch, se l'indirizzo MAC è nelle tabelle questo frame viene mandato alla porta corretta, altrimenti viene mandato a tutti.

Le tabelle vengono periodicamente (ogni qualche minuto) aggiornate rimuovendo gli indirizzi che non sono più attivi.

## Spanning Tree
Gli switch hanno un comportamento broadcast quando:
1. quando vengono accessi (per imparare i percorsi), che comunque è diverso dal broadcast di livello 1 es. cavo coassiale, hub,... : switch e bridge trasmettono in broadcast utilizzando comunque un sottolivello MAC e attende che il canale sia libero per trasmettere
2. Il frame contine un indirizzo di broadcast, per cui va mandato a tutta la rete

<br>

Gli switch in una rete potrebbero formare degli ANELLI nei collegamenti.
![[inserire schema]]

Questi anelli provocano potenzialmente la trasmissione all'infinito del frame. Gli anelli possono comunque esserci per vari motivi:
1. Per ridondanza, nel caso uno switch si rompa
2. Per errore

Si vuole evitare quindi che l'eventuale presenza di anelli nella rete provochi problemi. Gli switch sono quindi in grado di "eliminare" gli anelli ... creando lo **spanning tree**

![[inserire schema con esempio di "eliminazione"]]

Per determinare lo spanning tree gli switch seguono varie fasi:
1. Si cerca di capire qual è il **root switch**, lo switch con l'indirizzo MAC più basso 
2. ...
3. ...
4. Gli switch più vicini alla radice cominciano 
5. ...

Gli switch mandano in continuazione aggiornamenti ...

![[esercizio esempio su classroom di snapping tree]]

