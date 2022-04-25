

## CONTINUARE...



# Protocollo HTTPS
In questo protocollo viene utilizzata una **chiave segreta di sessione**, queste chiavi combinano i vantaggi della crittografia simmetrica e asimmetrica.

Si usa la crittografia a chiave pubblica per scambiarsi alcuni elementi che entrambe le parti utilizzano per calcolare la chiave segreta di sessione. Dopo quando entrambe le parti hanno questa chiave si cifra i dati che si trasmettono con la crittografia simmetrica.

HTTPS è un protocollo SICURO per il web: riusciamo a ottenere l'**autenticazione del server** (il client sa con certezza con chi sta parlando) e che **gran parte del traffico trasmesso è CIFRATO**. Non totalmente poichè alcune immagini e alcuni file audio viaggiano in chiaro (HTTP).

**NB**. I browser usano una CACHE: la cache del browser è una porzione di memoria in cui vengono salvati i contenuti web. In questo modo se l'utente vuole accedere a una pagina già aperta in precedenza, si può accedervi velocemente.

Se la pagina però è cifrata, avrò una chiave diversa, e quindi la cache risulterebbe inutile.
Alcuni contenuti delle pagine https però sono trasferiti via http, e quindi memorizzati in cache.

Anche i server DNS hanno una cache, permette così di non dover ricercare l'indirizzo di un sito se è già stato cercato in precedenza.

In conclusione, non tutto il contenuto ha bisogno di essere cifrato.

*Se sto parlando con una banca è fondamentale che tutto il contenuto sia cifrato*

### HTTPS: Handshake protocol
Client e Server si scambiano i loro **nonce** e stabiliscono quale versione si SSL usare.

In https non si può cercare di riprodurre un'altra sessione, poichè la chiave segreta di sessione è cambia.

Il server invia una **catena di certificati**, in modo che il client possa verificare l'identità del server. NB. Alcuni certificati vengono memorizzati sul browser.
A questo punto il client ha ricevuto una chiave pubblica che è certo di poter abbinare al server.

Il client manda al server una **pre-master key**, cifrata con la chiave pubblica ricevuta dal server. L'unico ente in grado di decifrare questa chiave è il server tramite la propria chiave privata. Tramite qualche algoritmo entrambi si calcolano la **chiave di sessione**. La comunicazione procedere con il traffico (da entrambe le parti) cifrato tramite la chiave di sessione calcolata.

### WPA2 Home Edition
WPA2 = Wireless Protect Access 2

La versione *home edition* è quella che utilizziamo comunemente in casa.

Questo protocollo fa parte dello standard 802.11 ed è sicuro a patto di fidarci dei dispositivi che sono collegati alla stessa rete.

Nelle fasi iniziali viene definita una **chiave segreta di sessione** tra l'access-point e il client, sulla quale verrà cifrato il traffico.

NB. Però è solamente il **frame** ad essere cifrato:
se quindi l'access point si collega ad uno switch, il frame rimane cifrato finchè viaggia via wifi. L'access point deve convertire il frame col lo standard 802.3, quindi il frame 802.3 NON è cifrato. 

Comunque quando arriva al router, questo lo decifra e il pacchetto contenuto nel frame viene instadrato nella rete.

Quindi questo protocollo quindi NON SOSTITUISCE l'https.

#### Funzionamento: ????
- AccessPoint invia una NONCE (numero casuale)
- la stazione costruisce una chiave composta da vari elementi, che combinanti creano una chive di sessione. E invia all'AP il suo Nonce e il MIC (cioè un hash del nonce cifrato tramite la chiave appena calcolata)
- Ricevendo questo messaggio l'AP: si costruisce la stessa chiave, va a verificare se questo MIC è corretto, se questo è corretto vuol dire che anche la stazione si è calcolata la stessa chiave
- L'AP manda una ulteriore chiave di gruppo cifrata alla stazione
- La stazione risponde con un ACK

NB. La chiave di gruppo è quella tramite il quale vengono cifrati i messaggi broadcast


**Perchè ci dobbiamo fidare delle stazioni collegate alla stessa rete?**
Perchè un ipotetico hacker collegato alla stessa rete potrebbe ricalcolarsi la stessa chiave che un altro utente sta già calcolando. 

### WPA2 Enterprise
Si basa sull'utilizzo di certificati.
La stazione si collega con l'AP e invia il proprio certificato.

L'AP verifica la validità del certificato collegandosi a un **server radius** e successivamente viene definita una chiave segreta per la comunicazione tra il client e l'AP.

Alcuni vantaggi:
- il traffico può essere univocamente associato al certificato
- NON è possibile per altre stazioni della rete "indovinare" la chiave
- l'amministratore di rete può revocare un certificato (es. un ex dipendente)


<br>
<br>

#### Firma digitale
Se si deve firmare digitalmente un documento si deve cifrare l'***impronta*** del documento usando la propria chiave privata. 

L'impronta del documento è una sequenza di bit ricavata utilizzando una funzione hash.

Una volta ricevuto il documento firmato, chi deve verificare la validità della firma deve:
- calcolare l'impronta del mess utilizzando la stessa funzione di hash
- decifrare la firma utilizzando la chiave del mittente (pubblica)
- verificare se le due impronte sono uguali, in questo caso il messaggio è autentico

**NB**. Quando il messaggio "torna", vuol dire che questo è **autentico** e **integro** (non ha subito alterazioni)

### Funzioni di hash

**COLLISIONE**: quando 2 testi diversi hanno la STESSA impronta.

Noi partiamo da 2 insiemi: dominio e codominio, la cardinalità del dominio è maggiore del codominio, quindi è impossibile avere funzioni univoche, ci sanno quindi 2 file (o più) con stessa impronta.


*Cosa potrebbe fare un hacker per falsificare la firma digitale?*

Un hacker potrebbe provare a sotituire il messaggio mantendendo valida la firma. 
Basta sostituire il messaggio con uno che abbia lo stesso HASH.
Così la destinazione, che verificherà l'hash del messaggio, lo vedrà corretto.

**NB1**. Dato un hash è COMPUTAZIONALMENTE IMPOSSIBILE produrre un messaggio che abbia lo stesso hash.
**NB2**. Se l'algoritmo di hash è fatto bene: testi simili "cadono" su hash lontani (diversi)

<br>

--> Bisogna essere sicuri tra l'abbinamento chiave pubblica e identità del proprietario della chiave:

### Certificato digitale
**CERTIFICATO DIGITALE**: è un documento elettronico che attesta la associazione UNIVOCA tra chiave e il soggetto che rappresenta.

*Se perdo la chiave privata, il certificato associato alla identità digitale viene revocato, tutto quello firmato prima della revoca però vale.*

### Web of trust
Esiste un altro sistema per la validazione delle firme tra persone basato sulla fiducia reciproca.
Nel web of trust le persone decidono di fidarsi tra di loro.
Il web of trust viene costruito conoscendo la chiave pubblica di un altro e viceversa, a questo punto B potrebbe inviare ad A un messaggio dicendo: *C è una persona di cui mi fido e questa è la sua Chiave Pubblica,* questo messaggio deve essere firmato con la chiave di B. A si fida e si *allarga la rete*.

NB. Alcuni tool sono PGP , GnuPG , OpenPGP

<br>
<br>
<br>





## Ripasso WPA (WPA 4-way-handshake)
PTK è la chiave segreta di sessione condivisa tra l'access point e la stazione.

L'AP invia alla stazione un numero (ANonce) USATO UNA SOLA VOLTA, con lo scopo di stabilire una chiave segreta condivisa, che durerà il tempo cui la stazione sarà collegata all'AP, alla prossima sessione la chiave deve essere diversa.
*Anche la stazione invierà il suo nonce (SNonce)*
--> Proprietà della **freschezza**, evita attacchi

La stazione decide un SNonce basandosi su MAc address dell AP, ANonce ricevuta, la propria SNonce, il proprio indirizzo MAC, masterkey ricavata dalla password, tramite tutti questi costruisce una **chiave di sessione**.

La stazione invia un frame contenente: la propria SNonce e il MIC, cioè un hash della Nonce cifrato usando la chiave segreta appena calcolata (PTK)

L'AP riceve un numero in chiaro e il MIC per verificare quel numero.
AP a questo punto ha anche lui tutti gli elementi per calcolare la chiave di sessione, ed è sicuro di possedere la stessa chiave della stazione, e questo significa che la stazione **conosce la password della rete**.

A questo punto l'AP accetta la connessione con la stazione e invia a questa la **GTK** (per trasmettere in broadcast), **però CIFRATA con la chiave che entrambi conoscono.**

Stazione risponde con un ACK.

**NB**. *Il frame rimarrà cifrato fino a quando rimarrà nella rete wireless, appena entra nella rete cablata non lo è più.*

**NB**. Ci sono però 2 difetti:
- Qualsiasi altro client appartenente alla stessa rete (conosce la password) si può mettere in ascolto di tutto il traffico e così come l'AP può costruirsi la PTK della stazione che si sta collegando.
- Se siamo amministratori di una rete con molti client (personali) quando il client si scollega ha comunque la password della rete

### WPA Enterprise Edition
La versione **enterprise** si basa sull'utilizzo di **CERTIFICATI** (Certificato CA). 

Quando la stazione si collega all'AP, manda il certificato. L'AP verifica l'autenticità del certificato collegandosi ad un **server radius**. Verificato ciò, l'AP manda la chiave segreta da utilizzare per la comunicazione Client-AP

**NB1**. *Ci sono più versioni della WPA Enterprise*

<br>
<br>
<br>


## Ripasso AES
Si basa su spet successivi in cui vengono fatti sia operazioni di **sostituzione e di trasposizioni.**

La chiave segreta serve per determinare il numero di round, cioè il numero di volta che determinate operazione verranno svolte su blocchi di bit.

La prima fase dell'algoritmo richiede, dalla chiave segreta, determinare le chiavi di round.
Più lunga è la chiave e più numero di round ci saranno.

Il testo da cifrare viene diviso in blocchi di 128bit e le chiavi di round fanno uno XOR bit a bit.

**NB**. Queste sequenze di sostituzioni e trasposizioni vengono ripetute per un numero variabile di round.

Poi si comincia con le operazioni.

<br>
<br>
<br>

## RSA
È basato sulle proprietà dell'aritmetica modulare

La generazione delle chiavi parte da due numeri primi molto grandi.
Entrambi moltiplicati generano N.

Tutta la robustezza di RSA è basata sul fatto che è computazionalmente impossibile scomporre questo numero N nei due fattori primi.

