# Livello Data Link
### I compiti del livello
Il **livello fisico** a volte **lascia irrosolti** problemi riguardanti gli errori, disturbi occasionali e ritardi nella propagazione del segnale.

Il principale compito del livello Data Link è quello di **garantire una linea di trasmissione priva di errori NON segnalati**.

### Cosa si deve fare?
Le entità di livello Data Link per svolgere il proprio compito devono:
- **Gestire gli errori di trasmissione**
- **Regolare il flusso di trasmissione**: ovvero **sincronizzare il dispositivo fisico più veloce portandolo alla velocità del più lento**, in questo modo si evita che il mittente trasmetta una quantità di dati superiore a quella supportata dal ricevente (**buffer overflow**)
- **Framing**: determinare come i **bit del livello fisico** sono **raggruppati in *frame***

**NB.** Il livello Data Link **raggruppa i bit in frame**. In più incapsula il pacchetto ricevuto dal livello di Rete in un nuovo pacchetto detto **frame** al quale aggiunge un'**header** e un **tail** (coda). ???

### Come?
L'approcio utilizzato dal livello Data Link è il seguente:

##### In trasmissione:
1. Spezza il flusso di bit che arriva dal livello di rete in una serie di frame
2. Calcola un'apposita funzione (**checksum**) per ciascun frame
3. Inserisce il checksum nel frame
4. Consegna il frame al livello fisico, il quale lo spedisce come sequenza di bit

##### In ricezione:
1. Riceve una sequenza di bit dal livello fisico
2. Ricostruisce da essa un frame dopo l'altro
3. Per ciascun frame ricalcola il checksum
4. **Se esso è uguale a quello contenuto nel frame** quest'ultimo **viene accettato**, altrimenti viene considerato errato e quindi scartato

### Cos'è una cheksum?
Una cheksum è una **sequenza di bit** (16 o 32 normalmente) **utilizzati per verificare l'integrità del pacchetto/dato trasmesso**, costruiti sulla base dei bit del *payload* e quindi sono dei **bit ridondanti**.

Il **bit di parità** è la più semplice **forma di controllo dell'errore** (es. nella trasmissione seriale) e quindi della correttezza del payload.

**NB.** Normalmente a livello Data Link oltre ad avere un'intestazione, nel frame è presente anche una **coda** (header - payload - tail).

### Servizi offerti al Livello di Rete
##### Senza connessione e senza riscontro
- Non è stabilita alcuna connessione tra mittente e destinatario (*non si intende connessione fisica, ma un momento in cui le parti si accordano sulla trasmissione dei dati*)
- Il **mittente non attende alcun riscontro** circa l'arrivo e la correttezza dei frame trasmessi
- I **frame persi non vengono recuperati** a questo livello, sono i livelli superiori che si occupano della ricostruzione del messaggio

Questo tipo di servizio è appropriato per **canali con basso tasso di errore** o in sistemi **real-time**, in cui non c'è tempo necessario all'attessa dei riscontri. Esiste anche la possibilità che il mezzo trasmissivo sia **unidirezionale**.

![[dl-no-con-no-risc.PNG]]

##### Senza connessione ma con riscontro
- Non viene stabilita alcuna connessione tra i due partner, ma i frame ricevuti dal destinatario **vengono confermati** in senso positivo o negativo (in questo caso si ritrasmette) con delle **ACK**
- Se entro un certo intervallo di tempo la **ACK non arriva**, il mittente **rispedisce il frame**
- La perdita di una ACK positiva può causare la trasmissione di più copie dello stesso frame

![[dl-no-con-si-risc.PNG]]

Per il mittente non c'è alcuna differenza tra il secondo e il terzo caso. Nel terzo caso il destinatario riceve 2 volte lo stesso frame **senza sapere che questo è un duplicato**, questo problema viene gestito dai livelli superiori.

##### Con connessione e con riscontro
- Si apre una connessione tra trasmettitore e ricevitore
- All'interno della connessione **i frame sono NUMERATI**, il ricevitore emette riscontro per ciascun frame. La numerazione è a **modulo 2**.
-  La connessione viene chiusa

![[dl-si-con-si-risc.PNG]]

I frame vengono numerati semplicemente con **0** e **1** (a **modulo 2**) **ciclicamente**. Con questo tipo di servizio ogni frame viene ricevuto **solamente una volta** e i frame arrivano nello stesso ordine con cui sono stati trasmessi.

### Delimitazione dei frame con sequenza di CARATTERI
Ogni frame inizia e finisce con una particolare sequenza di caratteri ASCII. Solitamente:
- **Inizio** frame: **DLE (Data Link Escape)** , **STX (Start of Text)**
- **Fine** frame: **DLE** , **ETX (End of Text)**

Questi caratteri NON corrispondono ad un simbolo della tastiera e quindi NON SONO STAMPABILI.

Se nel **payload** c'è una sequenza di bit che corrisponde al **DLE** questo viene **duplicato**, chi la riceve **la interpreta come una sola**, non termina così la sincronia di comunicazione.

**Es.** In C la `\` manda a capo, se metto nella stringa `\\` ne viene visualizzata una sola.

**NB**. Le reti sono nate gradualmente, la base di partenza sono state le tecnologie che venivano utilizzate (anni 70) per collegare terminali remoti a calcolatori centrali, direttamente o via linea telefonica. In quel caso il payload non poteva contenere caratteri strani ma solo ciò che poteva essere digitato dalla tastiera.
Poi si passò a far collegare tra di loro 2 computer, che possono scambiarsi tra di loro qualsiasi sequenza di bit, in questo caso poteva capitare che nel dato era presente una DLE ETX, che farebbe perdere la comunicazione.

### Delimitazione dei frame con sequenza di BIT
Ogni frame **inizia** e **finisce** con la sequenza di bit **1000 0001 (flag byte)**.

Si pone lo stesso problema di prima, quindi:
- In trasmissione, ogni volta che il livello 2 incontra nel payload **5 bit 0 consecutivi** inserisce un **bit 1**
- In ricezione, ogni volta che il livello 2 incontra nel payload **5 bit 0 seguiti da un bit 1** quest'ultimo viene **rimosso.**

##### Esempio
Il payload da trasmettere è: 110000000001100000111
Il mittente aggiunge un bit 1 ogni 5 bit 0:	1100000**1**00001100000**1**111
Il destinatario riceve:	11000001000011000001111
Rimuove così i bit 1 che segue una sequenza di 5 bit 0: 11 00000 **1** 000011 00000 **1**111
In conclusione, otterrà quindi nuovamente: 110000000001100000111

### Errori di trasmissione
Gli errori, presenti soprattutto nelle trasmissioni telefoniche e wireless, sono dovuti a:
- **Rumori di fondo**
- Disturbi (ad es. fulmini) improvisi
- Interferenze (ad es. motori elettrici)

Ci sono due approcci al trattamento degli errori:

### Codice a CORREZIONE DELL'ERRORE
Si include nel frame abbastanza informazioni aggiuntive in modo da poter ricostruire il messaggio originario. Richiedono quindi **molti bit di controllo**.

In genere non si utilizza questo metodo poiché solitamente è **più efficiente limitarsi a *rilevare gli errori* e *ritrasmettere saltuariamente***.

Un esempio è il **codice di Hamming**.

### Codice a RILEVAZIONE DELL'ERRORE
Si include nel frame una quantità limitata di informazioni aggiunta in modo da accorgersi che c'è stato un errore. L'errore può essere **solo rilevato ma non corretto**.
Ricevendo un **not ACK** il trasmettitore puòi rimandare il pacchetto, se stiamo utilizzando servizi affidabili.

Un esempio è il **CRC**.

#### Bit di parità
Non è una forma di controllo dell'errore robusta in quanto **può rilevare solo un numero dispari di errori**. In generale per controllare la correttezza dei frame si usano codici più complessi che usano 16 o 32 bit.

Usando i bit del frame si fanno delle operazioni che rimandano una checksum, chi riceve controlla la checksum, se non torna ci sono errori del frame.

## Struttura generale di un frame
**NB**. A seconda del tipo di protocollo **può variare**. Per analisi protocollo trasmissione facciamo riferimento ad un frame con *header* e *info*.

![[struttura-frame.PNG]]

- **FLAG**: delimitatori di inizio e fine
- **Kind**: specifica se il frame è contiene dati o è di controllo
- **Seq**: è il **numero progressivo** del frame (o 0 o 1)
- **ACK**: contine informazioni relative al riscontro dei frame ricevuti
- **Payload**: contine le informazioni del frame, può corrispondere ad un intero pacchetto di rete
- **CRC**: o un qualsiasi altro metodo per il controllo degli errori

### Protocollo Simplex Stop and Wait
In questo protocollo il mittente **attende un OK** (**ACK**) **per continuare a trasmettere**, detto anche **Stop and Wait**. 
ll protocollo funziona nel seguente modo: Mando una trama, Mi fermo, Aspetto un riscontro. E continua così.

I protocolli **stop & wait** sono però **lenti** poichè costringono ad aspettare un risposta di conferma.

### Protocollo Simplex Stop & Wait per CANALE RUMOROSO
In questa tipologia di protocolli si aggiunge un **timer** il quale consente, nel caso non arrivi l'ACK entro un tot di tempo, di rimandare il frame.

##### Alcuni esempi di dialogo
*Funzionamento normale:*
![[funzionamento-normale.PNG]]
<br>
*Perdita di un frame:*
![[perdita-frame.PNG]]
<br>
*Perdita di una ACK:*
![[perdita-ACK.PNG]]
<br>

##### Sequenza protocollo Simplex Stop & Wait del MITTENTE
0. n_seq = 0;  
1. n_seq = 1 - n_seq;  
2. attende un pacchetto dal livello network;  
3. costruisce frame dati e copia n_seq in [seq];  
4. passa il frame dati al livello fisico;  
5. resetta il timer;  
6. attende un evento:  
	* timer scaduto: torna a 4)  
	* arriva frame di ack (vuoto) non valido: torna a 4)  
	* arriva frame di ack (vuoto) valido: torna ad 1)

##### Sequenza protocollo Simplex Stop & Wait del DESTINATARIO
0. n_exp = 1;  
1. attende evento;  
	* arriva frame dati valido da livello fisico:  
			2. se ([seq] == n_exp)  	
					2.1. estrae pacchetto  
					2.2. lo consegna al livello network  
					2.3. n_exp = 1 - n_exp  
3. invia frame di ack (vuoto)  
4. torna ad 1.  
	* arriva frame non valido: torna ad 1.

### Efficenza dei protocolli Stop & Wait
Prima di trasmettere un nuovo frame si deve **attendere l'ACK del precedente**.
Questo composta un utilizzo inefficiente del canale di comunicazione, che dipende da:
- Ritardo di propagazione
- Velocità di trasmissione
- Lunghezza della trama

##### Esempio
L'efficienza è la velocità effettiva con cui si riescono a trasmettere i dati rapportata alla velocità che il mezzo trasmissivo offre.

### Piggybacking
Negli esempi sopra abbiamo visto i dati viaggiare in una sola direzione e i riscontri nell'altra, **normalmente però la comunicazione è bidirezionale**, come sotto:

In questo caso il campo **kind** serve per **distinguere se il frame è di tipo dati o ACK**.

![[senza-piggybacking.PNG]]


Per migliorare l'efficienza nel trasferimento possiamo **inserire le informazioni di ACK nei frame di dati**. Questa tecnica si chiama **piggybacking**, le **informazioni di ACK in questo modo NON richiedono un apposito frame**, come sotto:

![[con-piggybacking.PNG]]

**NB1**. Piggybacking = "portare qualcosa in più"
**NB2**. I riscontri vanno sempre mandati ma non sempre abbiamo dati da mandare, se ci fosse quindi un momento in cui nessuno dei 2 ha dati da spedire si torna alla trasmissione *senza piggybacking*.

## Sliding Windows
Il piggybacking si combina bene con la modalità **sliding windows** (diversa dallo stop & wait).

##### Problema
Usando il piggybacking per quanto si può aspettare un frame su cui trasportare un ACK che è pronto e deve essere inviato?
Non troppo, poiché se l'ACK non arriva in termpo il mittente ritrasmetterà il frame anche se ciò non è necessario. Dunque si **stabilisce un limite al tempo di attesa** di un frame sul quale trasportare l'ACK, trascorso tale tempo si crea un frame apposito nel quale trasmettere solo l'ACK.

##### Soluzione
Diminuendo il numero di ACK da trasmettere, si velocizzano le operazioni di trasmissione, per cui alcuni protocolli hanno introdotto le finestre scorrevoli (**sliding windows**).

I protocolli a finestra scorrevole **stabiliscono un certo numero di frame** (*larghezza della finestra*) **che si possono inviare consecutivamente SENZA attendere l'ACK di riscontro**.

_La finestra che scorre nel flusso di dati da trasmettere, rappresenta una certa quantità di dati trasmessi ma ancora senza riscontro._

##### Caratteristiche protocolli sliding windows
- Sono **full-duplex** (per i dati), sfruttano il piggybacking e sono più robusti di quelli stop & wait.
- Ogni frame inviato ha un **numero di sequenza**, da $0$ a $2^n - 1$ (il campo **seq** è costituito da n bit)
- Ogni stazione **mantiene due finestre**, una di **trasmissione** e una di **ricezione**

#### Sliding windows: finestra di trasmissione
Ad ogni istante il **mittente mantiene una finestra scorrevole sugli indici dei frame**, e solo quelli entro la finestra possono essere trasmessi. I numeri di sequenza entro la finestra rappresentano frame da spedire o spediti, ma non ancora confermati.

*I frame dentro la finestra devono essere mantenuti in memoria per la possibile ritrasmissione; se il buffer è pieno, il livello Data Link deve costringere il livello Network a sospendere la consegna di pacchetti*

**Quando arriva la conferma di ricezione di un frame (ACK)**, la finestra si "sposta" avanti di uno, e sarà possibile ricevere un nuovo frame dal livello di rete.

#### Sliding windows: finestra di ricezione
Analogamente, il destinatario mantiene una finestra **corrispondente agli indici dei frame che possono essere accettati**.

I **frame** che arrivano **vengono memorizzati in dei buffer** in attesa di essere verificati ad inviati al livello superiore.

- Se arriva un frame il cui **indice è fuori dalla finestra** il **frame viene scartato** (e non si invia il relativo ACK)
- Se arriva un frame il cui **indice è entro la finestra**:
	1. Il **frame viene accettato**
	2. Viene spedito il relativo **ACK**
	3. La **finestra viene spostata** in avanti

**NB1**. La **finestra di ricezione può avere una dimensione diversa** rispetto alla finestra di trasmissione.

### Sliding windows: go-back-n
Se la finestra di ricezione è di un solo buffer, il destinatario accetta i frame solo nell'ordine giusto.

Se arriva un **frame** contenente **errori** (**o fuori sequenza**), dopo un time-out (o **dopo richiestra di ritrasmissione**), quindi si **ritrasmette quel frame** (o di quello mancante) **e di tutti i frame successivi** che nel frattempo potrebbero arrivare.

La finestra di ricezione è grande 1 (**i frame quindi possono essere ricevuti solo ordinati**)

![[go-back-n.PNG]]

### Sliding windows: selective repeat
Se la dimensione della finestra di ricezione è $2^n - 1$ (come quella di trasmissione), nel caso di mancato arrivo di un frame o arrivo di un frame errato, se ne **richiede selettivamente la trasmissione**, successivamente ad un time-out, ma **comunque si accettano e memorizzano frame successivi che potrebbero arrivare** (al massimo $2^n - 2$ ).

La finestra di ricezione è ampia quanto quella di trasmissione.

![[selective-repeat.PNG]]

<br>
<br>
<br>
<br>

## Sliding windows (ripasso)
Il protocollo sliding windows NON costringe il mittende ad aspettare la risposta per ogni frame trasmesso.

I protocolli sliding windows vengono utilizzati con comunicazione **full-duplex**:
Entrambe le parti contemporaneamente trasmettono dei frame dati, e ogni frame dati contiene delle informazioni di controllo che fanno capire all'altra entità che le informazioni sono state ricevute.

Protocollo HDLC: orientato alla connessione e affidabile in cui le trasme sono di vario tipo, quelle informazioni hanno 2 numeri:
1. Uno di sequenza
2. Uno di ACK = numero di sequenza della propria trama che mi aspetto di ricevere

**NB**. L'apertura della connessione avviene tramite 2 **connection request**.

*Posso aver trasmesso alcune trame senza bisogno di conferma, ma NON si può andare avanti all'infinito: in qualsiasi momento infatti, potrebbe arrivare una **conferma negativa** (o **not ACK**).*

La **finestra di trasmissione** è il numero di trame che possono essere spedite senza avere alcun tipo di riscontro

*Es. Nel protocollo HDLC la finestra di trasmissione è 7, cioè posso ricevere 7 frame senza avere riscontro, devo però tenerle in memoria nel caso dovessi ritrasmetterle.*

**Go-back-n**: NON si accettano trame fuori sequenza, la finestra di ricezione è uguale a 1 (ricevo un frame per volta)

**Selective repeat**: costringe ad avere la finestra di ricezione ampia quanto quella di trasmissione

Con **sliding windows** si intende l'idea per cui:
*È come se la finestra che scorre nel flusso di dati da trasmettere, rappresenta una certa quantità di dati trasmessi ma ancora senza riscontro.*


















<br>
<br>
<br>
<br>

### Protocollo SLIP (Serial Line Internet Protocol)
- È il **primo protocollo** Data Link utilizzato in Internet.
- È un protocollo **senza riscontro** e **senza connessione**
- I pacchetti vengono trasmessi sulla linea con uno speciale indicatore (**0xC0**) alla fine per la suddivisione

Viene ancora utilizzato a causa del **basso overhead**

### Protocollo HDLC
Prevede che le trame contenevano 2 numeri, uno di sequenza e uno di ACK. Le trame di informazioni avevano 2 numeri: NS (Numero di sequenza di questa trama), NR (Numero della prossima trama che mi aspetto di ricevere), quest'ultimo però fa anche da conferma.

### PPP (Point to Point Protocol)
- **Orientato alla connessione** e **affidabile**
- Prevede la **gestione dell'errore** e l'**autenticazione delle parti**, *per potersi collegare la controparte potrebbe chiedere "chi sei?"*
- Utilizza altri protocolli:
	- **LCP**: è il **protocollo di controllo per agganciare le linee e negoziare** delle opzioni di comunicazione
	- **NCP**: è il **protocollo di controllo di rete**, consente di negoziare le opzioni del livello di rete. *Es. Configurazione IP del router*.

### PPPoE (Point to Point Protocol over Ethernet)
Ora utilizzato al posto del PPP, è un **protocollo di tunnerling** che permette di **incapsulare il livello IP su una connessione tra 2 porte ethernet**, mantenendo le caratteristiche di un collegamento PPP.

È il protocollo normalmente utilizzato per il collegamento del router su linea DSL

**NB**. **Tunneling** = usato quando si collegano 2 porte dello stesso tipo

---
Fonti:
-   [[Livello Data Link.pdf]]
-	[[Architettura dei sistemi di elaborazione/PDF/Livello Data Link.pdf]]
-	[Dispensa prof. Bongiovanni](http://wwwusers.di.uniroma1.it/Reti1/Cap3.pdf)
-	[Riassunto prof. Lucarelli](http://www.pierolucarelli.it/reti%20informatiche/reti%20bongiovanni1/Cap3a/Cap3a.html)
-	[Riassunto prof. Lucarelli pt.2](http://www.pierolucarelli.it/reti%20informatiche/reti%20bongiovanni1/Cap3c/Cap3c.html)
-	[Dispensa UniVE](https://www.dsi.unive.it/~reti/pdf06/Reti4.pdf)