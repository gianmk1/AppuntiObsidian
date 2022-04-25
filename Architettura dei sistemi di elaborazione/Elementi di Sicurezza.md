# Elementi di sicurezza informatica
## Threat model
La sicurezza di un sistema è determinata da molteplici elementi e per ottenerla è necessario analizzare tutte le possibili minacce.

**La sicurezza complessiva di un sistema è determinata dal suo anello più debole.**
<br>

## Principi di confusione e diffusione
- **CONFUSIONE**: la relazione tra la chiave e il testo cifrato deve essere quanto più complessa e scorrelata possibile
- **DIFFUSIONE**: è la capacità dell'algoritmo di distribuire le correlazoini statistiche del testo lungo tutto l'alfabeto utilizzato dall'algoritmo di cifratura rendendo quanto più difficile possibile un attacco statistico
<br>

## Crittografia SIMMETRICA (a chive segreta)
![[crittografia-simmetrica.png]]

- Per ogni coppia di entità si utilizza la **stessa chiave** (**segreta e condivisa**) per cifrare e decifrare il testo
- **Svantaggio**: la **distribuzione** della chiave è **problematica**
- **Vantaggio**: le **prestazioni** run time sono **elevate**
- Gli algoritmi si basano su **trasposizione e sostituzione** dei bit
- Alcuni es. **AES**

### AES, Advanced Encrypt Standard
![[schema-aes.png]]

- Si basa su **step successivi** in cui vengono fatte **operazioni di sostituzione e trasposizione**
- La **chiave segreta serve per determinare il NUMERO di ROUND**, cioè il numero di volte che determinate operazioni dovranno essere svolta sui blocchi di bit
- Il **testo viene diviso in BLOCCHI di 128bit** (le chiavi di round fanno uno XOR bit a bit ???)
- **Fase 1**: dalla chiave segreta bisogna determinare le **chiavi di round**, più lunga è la chiave e più round ci saranno
<br>

## Crittografia asimmetrica (a chiave pubblica)
![[crittografia-asimmetrica.png]]

- **Ogni entità possiede 2 chiavi**, una **privata** ed una **pubblica**. Per ottenere la **CONFIDENZIALITÀ**, i messaggi vengono cifrati con la chiave pubblica del destinatario e decifrati con la sua chiave privata.
- **Vantaggio**: la **distribuzione della chiave pubblica è semplice**, anche se può essere necessario verificare l'associazione chiave pubblica - entità corrispondente (**certificati, web of trust**)
- **Svantaggio**: le **prestazioni** run time sono **basse**
- Gli algoritmi si basano su proprietà dell'**aritmetica modulare**
- Alcuni es. **RSA**

### RSA
- È basato sulle proprietà dell'**aritmetica modulare**
- La generazione delle chiavi **parte da 2 numeri primi molto grandi**, che **moltiplicati generano N**
- La robustezza di RSA si fonda sul fatto che è **computazionalmente impossibile scomporre N nei 2 fattori primi**
<br>

## Chiave segreta di sessione
- **Combina i vantaggi della crittografia asimmetrica e simmetrica**
- Usando la **crittografia asimettrica si realizza** un **"canale sicuro"** tramite il quale si determina una chiave segreta, su cui successivamente si basa la comunicazione
- **Nel definire la chiave segreta si utilizzano degli elementi** (nonce, timestamp, contatori) **per garantire la FRESCHEZZA** e impedire attacchi di replica
<br>

## Firma digitale
![[firma-digitale.png]]

*Nel caso si debba firmare digitalmente un documento si deve cifrare l'**impronta** del documento usando la propria chiave privata. Bisogna garantire l'AUTENTICITÀ del file ricevuto.*

L'**impronta (fingerprint) del documento è una sequenza di bit ricavata utilizzando una funzione di hash**.

Una volta ricevuto il documento firmato, *chi deve verificare la validità della firma* deve:
- **Calcolare l'impronta del messaggio** utilizzando la stessa funzione di hash
- **Decifrare la firma utilizzando la chiave pubblica del mittente**
- **Verificare se le due impronte digitali sono uguali**, in questo caso il messaggio è autentico.

**NB**. Il messaggio verificato certifica l'**AUTENTICITÀ** e l'**INTEGRITÀ (= non ci sono state alterazioni)** di ciò che abbiamo ricevuto.
<br>

## Funzioni di hash
Una **funzione di hash è una funzione NON INVERTIBILE che mappa una stringa di lunghezza arbitraria in una lunghezza predefinita**

*Noi partiamo da 2 insiemi: dominio e codominio, la cardinalità del dominio è maggiore del codominio, quindi è impossibile avere funzioni univoche, ci sanno quindi 2 file (o più) con stessa impronta.*

- Dato un hash **deve essere COMPUTAZIONALMENTE IMPOSSIBILE ritornare la stringa originaria**
- **Messaggi simili devono produrre hash molto diversi** (molto distanti)

*Cosa potrebbe fare un hacker per falsificare la firma digitale?*

Un **hacker** potrebbe provare a sotituire il messaggio mantendendo valida la firma. 
Basta **sostituire il messaggio con uno che abbia lo stesso hash**.
Così la destinazione, che verificherà l'hash del messaggio, lo vedrà corretto e lo considererà autentico.
<br>

## Certificato digitale
**CERTIFICATO DIGITALE**: è un documento elettronico che **attesta la associazione UNIVOCA** tra **chiave** e il **soggetto** che rappresenta.

*Se perdo la chiave privata, il certificato associato alla identità digitale viene revocato, tutto quello firmato prima della revoca però vale.*

**CERTIFICATE AUTHORITY**: è un **soggetto di terze parti abilitato** (e riconosciuto) **ad emettere certificati** digitali tramite una procedura di certificazioni.
<br>

## Web of Trust
**Nel web of trust le persone decidono di fidarsi tra di loro.**

Si **parte dalla conoscenza "diretta"** di una persona e della sua **chiave pubblica**, si firma un certificato per questa persona e **si accettano tutti i certificati firmati da membri del web of trust**.
<br>
<br>

## Protocollo HTTPS
**TLS: Transport Layer Security**

**HTTPS = HTTP + TLS**

![[tls.png]]

In questo protocollo viene utilizzata una **chiave segreta di sessione**, questa chiave combina i vantaggi della crittografia simmetrica e asimmetrica.

*Si usa la crittografia a chiave pubblica per scambiarsi alcuni elementi che entrambe le parti utilizzano per calcolare la chiave segreta di sessione. Dopo, quando entrambe le parti hanno questa chiave, si cifra i dati che si trasmettono con la crittografia simmetrica.*

HTTPS è un **protocollo SICURO** per il web:
- Riusciamo a ottenere l'**autenticazione del server**
- Gran parte del **traffico trasmesso è CIFRATO**

**NB1**. Solitamente non tutto il traffico è cifrato, es immagini/video/audio... . Alcuni contenuti delle pagine https quindi sono trasferiti via http (e possono essere memorizzati nella cache del browser)

**NB2**. Anche i server DNS hanno una cache che permette di non dover ricercare l'indirizzo di un sito se è già stato risolto in precedenza

### HTTPS: handshake protocol
![[https.png]]

1. Client e server si **scambiano** i loro **nonce (= dei numeri)** e **stabiliscono** quale **versione di TLS** (o SSL) utilizzare
2. Il **server invia una catena di certificati**, in modo che il client possa identificarne l'identità. Il **client inoltre riceve la chiave pubblica del server**.
3. Il **client invia** una **pre-master key** cifrata **utilizzando la chiave pubblica del server** (crittografia asimmetrica)
4. **Utilizzando la pre-master key e i 2 nonce**, **entrambe** le parti si **calcolano** la **chiave segreta di sessione**
5. La **comunicazione ora verrà cifrata utilizzando la chiave segreta di sessione** calcolata (crittografia simmetrica)

**NB**. In https NON si può cercare di riprodurre un'altra sessione poiché la chiave segreta di sessione cambia.
<br>
<br>

## WPA2 Home Edition
- **WPA: Wireless Protect Access**
- Questo protocollo fa parte dello standard 802.11 ed **è sicuro a patto di fidarci degli altri device collegati alla stessa rete**

Nelle fasi iniziali viene definita una **chiave segreta di sessione** tra l'Access Point e il client, sulla quale verrà cifrato il traffico.

**NB1**. Solamente **il frame è cifrato e rimane cifrato fino a quando viaggia via wifi**. L'AP poi deve convertire il frame con lo standard 802.3, quest'ultimo NON è più cifrato. Inoltre il router lo decifra comunque quando lo instrada nella rete.
**NB2**. Questo protocollo NON sostituisce l'HTTPS
<br>

### WPA2 4-way-handshake
![[wpa2-handshake.png]]

**PTK** è la **chiave segreta di sessione condivisa** tra l'AP e la stazione.

1. L'**AP invia alla stazione un nonce** (ANonce) **USATO UNA SOLA VOLTA** alla Stazione.
2. La **Stazione decide un nonce** (SNonce) e **tramite**: **ANnonce**, **SNnonce**, **indirizzi MAC** di entrambi i device e **password** della rete, **calcola la chiave di sessione**.
3. La **Stazione invia (IN CHIARO) il suo SNonce e il MIC**, cioè un **hash della Nonce cifrato** usando la chiave segreta appena calcolata (PTK)
4. L'**AP ha tutti gli elementi per calcolare la PTK e, verificando il MIC della Nonce**, è sicuro di possedere la stessa chiave della stazione: questo significa che la **stazione conosce la password della rete**.
5. L'**AP** accetta la connessione e invia alla Stazione la **GTK** (utilizzata per le trasmissioni broadcast) **cifrata con la chiave segreta di sessione**.
6. Stazione risponde con un ACK

**NB**. Il **nonce viene UTILIZZATO UNA SOLA VOLTA**, questo implica la **proprietà della FRESCHEZZA**.

**Ci sono 2 difetti:**
- **Qualsiasi altro client, appartenente alla stessa rete, può mettersi "in ascolto"** del traffico e, come l'AP, costruirsi la PTK della stazione che sta cercando di connettersi
- Se siamo amministratori di una rete con molti client, abbiamo bisogno eventualmente di rimuovere l'accesso ad una stazione (senza dover cambiare psw ogni volta)
<br>

## WPA2 Enterprise
La versione **enterprise** si basa sull'utilizzo di **CERTIFICATI** (Certificato CA). 

1. Quando la **stazione si collega all'AP, manda il certificato**. 
2. L'**AP verifica l'autenticità del certificato** collegandosi ad un **server radius**.
3.  Verificato ciò, l'**AP manda la chiave segreta** da utilizzare per la comunicazione Client-AP.
<br>
<br>

## VPN, Virtual Private Network
![[vpn-esempio.png]]

Con VPN si intende una rete privata che però è virtuale poiché invece come collegamento si utilizza l'infrastruttura di Internet (che è condivisa).
Vogliamo quindi una rete privata su SCALA MONDIALE.

**NB**. È possibile creare una rete privata FISICA, questo però è molto dispendioso (bisogna pagare il provider internet) e molto spesso non è fattibile.

### Come funziona una VPN?
La comunicazione avviene tramite un **tunner over IP** (ricorda il tunneling ipv4):
**Tutti i pacchetti che devono andare da A a B devono passare per questo tunnel**.

Il **tunnel end-point** **incapsula tutti i pacchetti in uscita nel payload** di pacchetti che hanno come destinazione l'altro end-point.

**NB**. A questo punto però NON è ancora garantita la confidenzialità delle informazioni trasmesse. (*vedi sotto*)

### Protocollo IPSEC tunnel
Il protocollo IPsec si basa sulla crittografia a chiave segreta.

![[pacchetto-ipsec.png]]

**Encrypted** è il pacchetto che deve attraversare il tunnel e che verrà incapsulato come payload nel nuovo pacchetto.

*Qui ipotizziamo di dover trasmettere un'intestazione TCP e un payload.*

- Il **pacchetto viene cifrato con crittografia mediante chiave segreta** condivisa tra i 2 end-point
- Viene **inserito un ESP header**
- C'è una **nuova intestazione IP (in CHIARO)**, con indirizzo di destinazione dell'altro end-point
- Alla fine del pacchetto c'è una sezione **Authentication HMAC** dove si **applica una funzione di hash** al pacchetto **e la si cifra con la chiave segreta condivisa**

*Un hacker può anche manomettere il pacchetto, ma, facendo ciò, non ritornerà più il codice di autenticazione.*