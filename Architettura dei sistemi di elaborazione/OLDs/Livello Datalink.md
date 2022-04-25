# Livello Datalink

1. Controllo degli errori
2. Controllo del flusso: chi trasmette dei dati deve stare attento a non trasmetterli più velocemente di quanto il ricevitore possa riceverli (non ha a che fare con la velocità di trasmissione dei bit) ma del passaggio al livello successivo che magari ha il buffer pieno

Il livello fisico lascia irrisolti problemi legati agli errori e siturbi occasionali
In genere al livello 2 gli errori vengoro risolti ma non è sempre così

### Cosa si può fare?
- Raggruppare i bit in frame 

### Come?
L'entità che deve 
- trasmettere spezza il flusso di bit che arriva dal livello di rete
- calcola un'apposita funzione (checksum)
- per ciscun frame ricalcolare il frame
- se esso è uguale a quello contenuto nel frame questo viene accettato, altrimenti viene scartato

Chi riceve invece deve fare il contrario

### Cos'è una chekcsum
Sono dei bit in più (16 o 32 normalmente) che dipendono dai bit del payload e quindi sono dei **bit ridondanti**

Il bit di parità e la più semplice forma di controllo dell'errore (es. nella trasmissione seriale) e quindi della correttezza del payload

![[foglio xournal]]

NB. Normalmente a livello data link oltre ad avere un intestazione nel pacchetto è presente anche una coda (header - payload - coda)

### Servizi offerti al livello di rete
Riassunto:
	- Con o senza connessione
	- Con o senza riscontro (Affidabili - Non Affidabli)

1. Senza connessione e senza riscontro:
	- non è stabilità alcuna connessione tra mittente e destinatario (non si intende connessione fisica, ma un momento in cui le parti si accordano sulla trasmissione dei dati)
	- il mittente non attende alcun riscntro circa l'arrivo e la corrrettezza dei frame trasmessi
	- i frame persi non vengono recuperati a questo livello, sono i livelli superiori che si occupano della ricostruzione del messaggio

	Questo tipo di servizio è appropriato per canali con tasso d'errore molto basso oppure in sistemi **real-time**, in cui non c'è tempo necessario all'attesa dei riscontri. Esiste anche la possibilità che il mezzo trasmissivo sia **unidirezionale**
	
	![[esempio slide della perdita di frame]]
	
2. Senza connesione ma con riscontro
	- I frame che vengono ricevuti vengono confermati con delle **ACK**, che può essere positiva o negativa, in quel caso si ritrasmette
	- se entro un certo intervallo di tempo la ACK non arriva, il mittente rispedisce il frame 
	- la perdita di un riscontro positivo causa la ricezione di più copie dello stesso frame

	![[esempio slide della perdita frame e della rispedizione]]
	
	Per il mittente non c'è differenza tra il 2o e il 3o caso, nell'ultimo caso il destinatario riceve 2 volte lo stesso frame SENZA SAPERE CHE QUESTO È UN DUPLICATO, questo problema viene gestito dai livelli superiori
	
3. Con connessione e con riscontro:
	- Si apre la connessione tra trasmettitore e ricevitore
	- All'interno della connessione i frame sono NUMERARI, il ricevitore emette un riscontro per ciascuno
	- C'è una numerazione modulo2

	![[slide esempio]]
	
	I frame vengono numerati semplicemente con 0 e 1 (a modulo 2) ciclicamente.
	È in grado di capire se c'è stata una duplicazione e quindi scarta il frame in più 
	
	Operazione di modulo: è il resto della divisione, in generale un incremento modulo n vuol dire fare +1 e tenere il resto della divisione di n
	![[appunti xournal]]
	A furia di fare +1 ad un certo punto si torna a 0
	In informatica in numeri non sono infiniti ma FINITI, |2^n|
	
4. ...

### Delimitazione dei frame 
![[vedi appunti xournal]]

I frame vengono delimitati, le modalità più usate sono:
1. Con sequenza di caratteri
2. Con sequenza di bit

Che differenza c'è tra le 2? Entrambe sono sequenze bit
È una differenza di logica

#### Delimitazione dei frame con sequenza di caratteri
Ogni frame inizia e finisce con una particolare sequenza di caratteri ASCII, di solito DLE (data link escape) STX (start of text) e DLE ETX (end of text)

Questi caratteri non corrispondono ad un simbolo della tastiera, NON SONO STAMPABILI

NB. Le reti sono nate gradualmente, la base di partenza sono state le tecnologie che venivano utilizzate (anni 70) per collegare terminali remoti a calcolatori centrali, direttamente o via linea telefonica. In quel caso il payload non poteva contenere caratteri strani ma solo ciò che poteva essere digitato dalla tastiera.
Poi si passò a far collegare tra di loro 2 computer, che possono scambiarsi tra di loro qualsiasi sequenza di bit, in quel caso può capitare che tra la trasmissione sia presente una DLE ETX, che farebbe perfere la comunicazione.

Quindi se nel payload c'è una sequenza di bit che corrisponde al DLE questo viene **duplicato**, chi la riceve la interpreta come una sola, non termina così la sincronia di comunicazione

Es. in C la `\` manda a capo, se metto nella stringa `\\` ne viene visualizzata una singola

#### Delimitazione con sequenza di bit
ogni frame inizia e finisce con la sequenza di bit 1000 0001 (flag byte).

Dobbiamo interpretare un possibile flag byte presente nel payload come carattere di fine => chi trasmette: dopo 5 bit 0 consecutivi del payload inserisce un bit 1
=> chi riceve: se dopo 5 bit 0 consecutivi c'è un bit 1, questo viene rimosso

![[inserire esempio slide 14-15]]

### Errori di trasmissione

--- completare ---

##### Bit di parità
Non è una forma robusta, può rilevare solo un numero **dispari** di errori. In generale per controllare la correttezza dei frame si usano codici più complessi che usano 16 o 32 bit

Usando i bit del frame si fanno delle operazioni che rimandano una checksum, chi riceve controlla la checksum, se non torna ci sono errori del frame.

##### Codice a correzione d'errore
Richiedono molti bit di controllo

##### Codice a rilevazione d'errore
Può solo dire se c'è l'errore, non può correggerlo.
Ricevendo un not ACK il trasmettitore può rimandare il pacchetto, dipende dal livello in cui ci troviamo.

### Struttura generale di un frame
Questa non è generale, a seconda del tipo di protocollo può cambiare
![[inserire_immagine]]

- **FLAG**: delimitatori, di inizio e fine
- **kind**: specifica se il frame contiene dati o è solo di controllo
- **seq**: è il numero progressivo del frame (o 1 o 0)
- **ack**: contiene informazioni relative al riscontro dei frame ricevuti
- **payload**: contiene informazioni del frame, può corrispondere ad un intero pacchetto di rete
- **CRC**: o un qualsiasi altro metodo per il controllo degli errori


![[Slide_pag_22]]
Perdita della sola ACK, 

### Protocollo stop & wait per canale rumoroso
Stop & wait: mando una trama, mi fermo, aspetto riscontro. E così via.
NB. Nella trasmissione senza riscontro la velocità è maggiore.

I protocolli stop & wait sono **lenti**, costringono ad aspettare una risposta di riscontro

### Efficienza protocollo stop&wait
Prima di trasmettere un nuovo frame si deve aspettare l'ack precedente.
Utilizzo inefficiente del canale di comunicazione che dipende da:
- ritardo...
- ...

*Esempio:*
![[slide numero 26]]

*Spiegazione:*
Ritardo di propagazione: il segnale ci mette del tempo prima che arrivi

Efficienza è la velocità effettiva con cui si riescono a trasmettere i dati rapportata alla veloctià che il mezzo trasmissivo offre.

100us: tempo necessario per trasmettere i dati
120us: tempo necessario perchè il destinatario riceva la trama

20us: ritardo

Per trasmettere 1000bit sono serviti 140us, la velocità effettiva cambia e l'efficienza passa al 71%

### Piggybacking
Possiamo aumentare l'efficienza, anche nel protocollo stop&wait, se immaginiamo che le trame siano contemporaneamente di controllo e di dati.

Si inseriscono le informazioni di ack nei frame dati

*Esempio con piggybacking:*
![[inserire schema pagina 31]]

*Spiegazione:*
Questa volta il tempo complessivo è 240us però non sono più stati trasmessi 1000bit ma 2000. Anche solo con questo accorgimento l'efficienza è passata al 83%

**NB**. Piggybacking = "portare qualcosa in più"

I riscontri vanno mandati sempre ma non sempre abbiamo dati da mandare, se ci fosse un momento in cui nessuno dei 2 ha dati da spedire si torna alla trasmissione senza piggybacking

### Sliding windows
Il piggybacking si combina bene con la modalità **sliding windows** (diversa dallo stop&wait).

Protocollo HDLC:
*Un vecchio protocollo chiamato HDLC, prevedeva che le trame (che erano di vari tipi) contenevano 2 numeri, uno di sequenza e uno di ACK. Le trame di informazioni avevano 2 numeri: NS e NR, NS numero di sequenza di questa trama, NR numero della prossima trama che mi aspetto di ricevece, quest'ultimo numero però faceva anche da conferma*

Finestra di trasmissione: numero di trame che si possono spedire senza ricevere alcun riscontro

##### Sliding windows: finestra di trasmissione

 --- completare ---

##### Sliding windows: finestra di ricezione
Se mi arriva qualcosa fuori sequenza la scarto e chiedo di rimandare le trame da un certo numero in poi, sarò io poi a rimettermele in ordine

La finestra di ricezione può avere varie dimensioni:
1. ...
2. ...

##### Sliding windows: go back n

 --- completare ---

##### Sliding windows: selective repeat

 --- completare ---

### Protocollo SLIP (Serial Line Internet Protocol)
Il primissimo protocollo datalink utilizzato in internet è stato lo SLIP. È un protocollo senza connessione e senza riscontro, con questo protocollo ai pacchetti venivano aggiunti dei delimitatori per dire 0xC0.

Viene ancora utilizzato a causa del basso overhead

### PPP (Point to Point Protocol)
Orientato alla connessione e affidabile prevede la gestione dell'errore e l'autenticazione delle parti. Per potersi collegare la controparte potrebbe chiederti "chi sei"

**LCP** è il protocollo di controllo per agganciare le linee e negoziare delle opzioni di comunicazioni
**NCP** è il protocollo di controllo di rete, consente di negoziare le opzioni del livello di rete. Es. configurazione IP del router

### PPPoE (Point to Point Protocol over Ethernet)
Ora viene utilizzato al posto del PPP, è un protocollo di tunneling che premette di incapsulare il livello IP su una connessione tra 2 porte ethernet.

È il protocollo normalmente utilizzato per il collegamento del router su linea DSL.

Tunneling: usato quando si collegano 2 porte dello stesso tipo, ...