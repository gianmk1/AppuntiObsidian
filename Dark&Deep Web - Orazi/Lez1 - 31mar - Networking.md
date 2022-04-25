# Data Privacy & Networking
## Internet Theory
**ISP = Internet Service Provider**, compagnie telco che interconnettono reti
- C'è una sorta di **gerarchia**
- Si cerca di coprire più collegamenti possibili fisicamente, dove non si arriva si utilizzano **collegamenti logici**

**GARR** = ISP dedicato alle istituzioni pubbliche

![[inserire schema slide]]

Nazionale -> Regionale -> Locale

## Modello ISO-OSI
Nella realtà i modelli di riferimento sono ISO-OSI e TCP-IP. Sono alla base di qualsiasi infrastruttura/sistema (solitamente in più utilizzato è quello ISO/OSI)

*Alcuni concetti:*
- Layer: ci sono diversi livelli (uno sopra l'altro) che comunicano tra di loro. L'informazione dovrà sempre scendere verso il basso per poi risalire
- Interfaccia: strumento che ci permette di interfacciarsi allo stesso layer
- Protocolli: modelli per far comunicare 2 entità diverse (allo stesso livello)
- Embedding: la PDU racchiude un pacchetto che verrà poi gestito al livello più basso

#### Livello FISICO
- È il livello più basso
- Il segnale elettromagnetico è 0 o 1
- *Come funzionano fisicamente le trasmissioni*

#### Livello DATALINK
Si basa sul primo layer per cercare di connettere e inviare frame da una parte all'altra, provvede anche a fare la **sincronizzazione** di questi, **c'è quindi un approccio all'errore.**

#### Livello NETWORK
Iniziamo a staccarci dal concetto fisico di collegamenti, parliamo di **connessioni** dove non importa più in che modo i device siano collegati ma l'importante è che lo siano

#### Livello di TRASPORTO
Parliamo di **trasferimento di dati in una maniera standardizzata**, A e B devono riuscire a comunicare in maniera efficiente. 2 protocolli sono TCP e UDP.

#### Livello di SESSIONE
*Potrebbe essere facilmente integrato al livello di trasporto.*

SESSIONE = quando io inizio a comunicare con un altra persona, all'inizio mi accordo (handshake) sulla connessione, c'è la comunicazione effettiva e infine la connessione termina

#### Livello di PRESENTAZIONE
Abbiamo dei dati (provenienti da qualsiasi applicazione) che vogliamo trasmettere.
Il dato da trasmettere viene compresso, criptato, riformattato...

#### Livello APPLICATIVO
...
...
<br>
<br>

![[schema protocols across network elements]

## Encapsulation and Decapsulation
Ogni layer (dal basso) per comunicare con quello sopra aggiunge qualcosa, cioè un **intestazione**.

## Centralization & Decentralization
- **Centralized organization**: c'è un controllo centralizzato della rete
- **Decentralized organization**: il carico è distribuito su tutti i nodi della rete

All'inizio, quando non c'era ridondanza di server, si aveva un cluster di server centralizzati in un punto, per evitare il **single point of failure** si è passati a **decentralizzare i server**.
<br>

## Application architectures
- **Client-server**
- **Peer-to-peer**: si applica al sistema decentralizzato, una rete di tanti device che comunicano tra di loro e permettono a 2 entità esterne di comunicare tra di loro
- **Ibridi**

### Architettura Client-Server
**Server**:
- **sempre UP**
- sempre uno stesso IP. 
- Molto spesso si parla di un cluster di server, sotto al singolo IP che contattiamo quindi ci può essere un cluster di server, che si dividono le richieste

**Client**:
- comunica col server
- può avere un IP dinamico
- può essere UP o DOWN
- NON comunica direttamente con altri client, la comunicazione passa sempre tramite il server

### Sistema centralizzato
**Limitazioni:**
- Possono crearsi (naturalmente o artificialmente) delle **congestioni**, una volta che la singola entità è caduta l'intero servizio è down

**Vantaggi:**
- È più semplice **rendere sicuro fisicamente**
- Ci sono delle **risorse dedicate**
- Più efficiente economicamente (fino ad un certo limite)
- Gli aggiornamenti sono più facili

**Svantaggi**:
- Se il sistema cade è completamente DOWN
- Dipendente dalla connessione internet
- Meno probabilità di backup
- **Manutenzione del server difficoltosa**

**NB**. Quando si acquista un nuovo device bisogna controllare per quanto tempo questo dispositivo verrà aggiornato. *Es. ATM che giravano su Windows XP.*
**NB**. Ultimamente le piccole/medie imprese si affidano per i server a servizi come AWS, Azure. Dove tutta la parte a basso livello (es. aggiornamenti) è gestita da quest'ultimi.

### Peer-to-peer network
- Non c'è un server sempre attivo
- I nodi sono connessi arbitratiamente
- Gli indirizzi IP cambiano
- **Molto scalabile**, se aggiungiamo nodi la rete cresce
- **Difficile da mantenere**, ogni nodo ha bisogno di qualcuno che l'amministri

### Sistema DEcentralizzato
**Limitazioni:**
- Ci possono essere problemi nella coordinazione dei nodi
- NON adatto per piccoli sistemi

**Vantaggi**:
- Minimi problemi di potenza legati alla **bottleneck**, c'è molto **load balancing** per cui la richiesta è gestita da chi è "meno occupato"
- Ogni nodo può essere controllato autonomamente

**Svantaggi**:
- Difficile raggiungere grossi risultati dal punto di vista computazionale
- Difficile applicare una regolamentazione
- Difficile capire quale nodo è caduto
- Difficile capire quale nodo ci sta rispondendo
<br>
<br>

## BitTorrent
- L'emblema delle **connessione peer-to-peer**.
- Permette agli utenti di condividere file di grosse dimensioni.
- Non c'è bisogno che questo sistema abbia grosse risorse, **è abbastanza leggero**

I file vengono **spezzettati** in frazioni e divise tra varie punti, ogni entità che vuole scaricarsi il file completo va a prendersi ogni "pezzo di file"

### Come funziona?
SEED rende disponibile al download.
Se ho tanti **SEED** a cui connettermi posso **parallelizzare la comunicazione**, instauro così più connessioni e più velocemente riesco a recuperare il file.

**TRACKER** = computer che si incarica di coordinare le comunicazioni (richieste delle frazioni di file), gestisce l'inizio del download e monitora il flusso di pacchetti. Quando si aggiungono nuovi peers è lui a gestire la connessione.

**PEERS** = chiunque si connetta per scaricare il file tramite i diversi seed, anche i peers hanno una funzione di seed perchè nel momento in cui sto scaricando il file (e ho raccolto buona parte del file) posso renderlo disponibile, diventando così un SEED.

**NB**. Il vari segmenti del file non vengono scaricati in maniera sequenziale ma **randomica** o **"dando delle priorità"**.

### Come funziona tecnicamente?
Il file viene separato in segmenti o **CHUNKS** e di ognuno di questi viene calcolato l'hash.
Un file .torrent viene distribuito ai peers, quest'ultimo contiene l'hash di ogni pezzo del file, ...

### Bit Torrent public VS private
- Se pubblico tutti possono fare download ma c'è il rischio di scaricare qualcosa di malevolo
- Se private c'è un sistema di **login**
- Entrambi:
	- Offrono un livello di criptazione, affinchè l'ISP non sia in grado di vedere ciò che viene trasferito

NB. In Italia NON viene bloccato il protocollo torrent mentre in altri paesi come la Germania sì.

### Problemi con Bit Torrent
- Energivoro a livello di banda
- Difficile da raggiungere file poco comuni, poichè pochi seed lo rendono disponibile
- Facile da capire se stiamo effettuando una connessione torrent, quindi in alcuni paesi c'è il rischio di essere sanzionati
- Single point of failure: TRACKER

### Attacchi in Bit Torrent
- **Pollution attack**: attaccante ritorna un **chunk falso**, così da compromettere il nostro file finale. La soluzione a questo è inserire questo seed all'interno di una blacklist.
- **DDOS Attacks**: l'attaccante scarica una grossa fetta di torrent files e **spoofa**, cioè manomette, i file .torrent e li fornisce ai tracker: tutti i seed/chunk del documento vengono manomessi in modo che tutte le richieste vengano inviate ad un singolo utente (o ad un ristretto gruppo di seed), quest'ultimo viene **sommerso dalle richieste e va DOWN**. Una possibile soluzione è quella di **validare il file .torrent**.
- **Bandwitch Shaping**: i pacchetti bittorrent possono essere facilmente identificabili dall'esterno e bloccati dal provider (ISP). *Es. Comcast*. Una possibile soluzione è quella di criptare il nostro traffico o criptare i pacchetti Torrent.

<br>
<br>

## CIA Triad
Fondamentale per quanto riguarda l'analisi di qualsiasi sistema connesso.
- **Confidenzialità**, solitamente è il primo da preservare. Serve a prevenire che i dati trapelino verso qualcuno che non è autorizzato
- **Integrità**, per evitare che un soggetto non autorizzato modifichi il dato
- **Disponibilità**, un attaccante non può impedire la disponibilità di un dato/risorsa

## VPN, Virtual Private Network
Si viene a creare una **connessione sicura e criptata**, si utilizza una rete privata sfruttando l'infrastruttura pubblica della rete.

Noi non ci connettiamo più direttamente al server cui vogliamo connetterci, ma passiamo per un intermediario (il server della VPN) che farà la richiesta per noi.

### Remote Access VPN
All'inizio le VPN erano utilizzate soprattutto nelle aziende, queste volevano che NON tutte le loro risorse fossero disponibili all'esterno.

La comunicazione passa sempre attraverso internet ma c'è un **TUNNEL** che maschera ciò che passa all'interno di esso.

### Site-to-site VPN
Viene fatto, solitamente sempre a livello corporate, per **collegare diverse intranet tra di loro**. 

- **Extranet based VPN**:  2 aziende diverse che cercano di connettersi tra di loro
- **Intranet based VPN**: 2 reti della **stessa azienda** che si vogliono connettere tra di loro

![[inserire immagine slide 30]]
![[inserire immagine slide 31]]

### VPN Protocols
Ci sono diversi protocolli che ruotano attorno alle VPN:
- IPsec
- ...

### IPSec
- Agisce a livello di IP
- È un protocollo che permette di **criptare** e **autenticare** la sessione
- 1a modalità: **Transport mode**, dove il messaggio all'interno del pacchetto viene criptato
- 2a modalità: **Tunneling mode**, la connessione è tra 2 gateway, l'intero pacchetto viene criptato ???

- **Connectionless integrity**: Abbiamo la certezza che il traffico non viene modificato quando la connessione viene instaurata

**Applicazioni dell'IPsec**:
- Sede esterna all'ufficio
- Accesso da remoto (passando per internet)
- ...

**Benefici dell'IPSec:**
- Forte elemento di sicurezza nella "parte centrale" della comunicazione
- È applicato sotto il **transport layer**, quelli sopra non si accorgono nemmeno del lavoro di IPSec
- Può essere utilizzato su qualsiasi device

![[immagine slide 36]]

### L2TP, Layer 2 tunneling Protocol
È un altro protocollo per le VPN, **molto veloce** ma **consuma molte risorse**.

### PPTP, Point to point Tunneling Protocol
È **molto efficiente** ma molto meno sicuro.

### OpenVPN
- Il più utilizzato attualmente
- **Opensource**
- Supportato da tutti i tipi di dispositivi
- Facile da installare (basta un eseguibile)

**NB**. Alternativa: WideGuard ma ancora poco popolare
<br>

## SSL e TLS
Secure Socket Layer, superato dallo standard TLS. Garantisce la CIA al livello di TRASPORTO, un esempio è HTTPS.

**NB**. SSL ormai è sorpassato.

##### Come si instaura la connessione tra 2 entità che vogliono comunicare via TLS?
**Handshake**, *vedi le slide su Elementi di sicurezza (ADE)*

![[inserire immagine slide 40]]

NB. Ci sono diversi attacchi che cercano di compromettere la decisione del cifrario da utilizzare. Es. si può forzare il server a comunicare solamente via SSL 3.0 (deprecato e insicuro)

### HTTPS

![[inserisci schema slide 41]]

### VPN sommario
**Vantaggi**:
- buona scalabilità
- metodo senza il quale molte comunicazioni sarebbero molto più costose o impossibili
- da accesso al controllo remoto
- fornisce un **buon livello di sicurezza**
- **anonimizzazione**, che però dipende dal server il quale ci stiamo connettendo

**Svantaggi**:
- Ci sono comunque dei modi per i quali è possibile inserirsi all'interno di un tunnel vpn
- Tante versioni e tanti protocolli portano molto spesso a problemi di incompatibilità
- Comunicazione più lenta e complessa 

**NB**. È importante utilizzare un servizio VPN che offre la **politica NO LOG**.

<br>
<br>

## Data Anonymization
L'**anonimizzazione** è un processo tale per cui noi riusciamo a rendere un documento/dato/ecc ANONIMO, dove non ci sono informazioni da proteggere e NON può più essere ricondotto ad una specifica entità.

**Perchè?**
- Proteggere le attività di un privato
- Aspetti finanziari

**Come?**
Ci sono diverse tecniche di anonimizzazione.

![[schema slide 44]]

*Quando abbiamo un servizio gratuito lo stiamo pagando tramite le informazioni che "implicitamente" forniamo.*

Se vogliamo fare un analisi su dei dati chimici non possiamo farlo a meno che noi non anonimizziamo i documenti, facendo così decadere la **clausola della privacy**.
Questo può essere applicato anche a:
- analisi di business
- ricerche
- software
- cloud storage
- ...

### Personal Data
All'interno di un dato ci possono essere diversi tipi di identificativi:
- **DIRETTI**: nome, cognome, email con nome, ...
- **INDIRETTI**: non basta coprire il nome cognome ma anche data di nascita, zip code, gender, ...
- **PSEUDONIMI**: usando pseudomici proteggiamo la privacy ma possiamo comunque utilizzare il dato

### Dati sentibili
- Dati personali sensibili:
	- possono essere causa di imbarazzo/...
	- etnia, religione, dati biometrici

- Informazioni sensibili di business
	- dati finanziari, progetti futuri
	- **versione del server che stanno utilizzando**

### Dati strutturati o liberi
- **Stuctured data**:
	- storati seguendo un metodo
	- **facilmente ricercabili**
	- JSON, XML

- **Unstructured data**
	- difficili da ricercare
	- file di testo, reports, ...


Il processo di anonimizzazione è molto complesso e soffisticato, possono esserci diverse sfaccettature rendono il dato NON più anonimo.

### Alcuni metodi per anonimizzazione
- Swapping
- Generalizzazione
- Pseudonimo
- Pertubation

<br>

## Motori di ricerca
La maggior parte delle persone utilizza come motore di ricerca **Google**.

Google è presente ovunque, la maggior parte dei servizi che utilizziamo sono tutti proprietari di google. Ha quindi una specie di monopolio.

**NB**. Una delle poche alternative valide è **DuckDuckGo**.

#### DuckDuckGO
- Fornisce solo risultati che abbiano **link HTTPS**
- Non cerca di tracciare la nostra identità
- Non ci sono cookie associati di default sul nostro browser
- Qualsiasi device, da qualsiasi parte del mondo avrà gli stessi risultati di una specifica ricerca => I **risultati NON sono condizionati dalle nostre ricerche precedenti**

**NB**. È importante differenziare i provider a cui ci affidiamo, es. invece di utilizzare GDrive possiamo utilizzare Dropbox. **Centralizzare tutto e dare tutto ad un unico host è pericoloso**.

### Internet Cookies
Un **cookie è un oggetto di testo inviato dal server al client**, è **UNIVOCO** per noi. Il nostro browser lo rimanda al/ai server nelle seguenti connessioni.

Lo scopo è quello di dare un'identità al nostro browser.

##### Come funziona?
Quando l'utente va a fare una richiesta con lo stesso cookie, il web server saprà con chi sta andando a fare la connessione (tramite il cookie).

##### All'interno di un cookie
Soltanto chi mi ha mandato il cookie è in grado di riutilizzarlo, molti cookie però settano un indirizzo di dominio per cercare di accedere ad uno specifico cookie.

![[inserire immagine cookie pag 57]]

I campi più importanti contenuti in un cookie sono:
- **Codice univoco**
- **Data creazione del cookie**
- **Dominio su cui viene utilizzato il cookie**
- **Data di scadenza del cookie**
- **HttpOnly**: il cookie può essere utilizzato solamente su connessioni web (e non, ad esempio, ssh, ...)
- **Secure**: il cookie può essere utilizzato solamente per connessioni HTTPS

### Tipologie di cookie
1. **Cookie di SESSIONE**:
	- Valido per una singola sessione
	- Per sessione si intende da quando apriamo a quando chiudiamo il browser
	- Viene salvato in RAM
2. **Persistent cookie**:
	- È salvato nell'HARD DISK
	- Viene utilizzato per più sessioni
	- Rimane nel browser fino a quando non scade o non lo cancelliamo
3. **Secure HTTPS**:
	- Utilizzato per sessioni criptate e sicure
4. **HttpOnly**:
	- Il cookie può essere utilizzato solamente via protocollo HTTP
	- Script javascript NON possono accedere a questi cookie
5. **Cookie di terze parti**:
	- Utilizzati per tracciare
	- Per **creare una profilazione**, ecco perchè a seconda delle ricerche che facciamo su google riceviamo degli annunci pubblicitari specifici
	- *Il sito che non stiamo direttamente visitando riesce comunque a tracciare la nostre informazioni*
6. **Super o Zombie Cookies**:
	- **I più pericolosi**
	- Sono dei cookie che rigerenano una volta che vengono cancellati
	- Sono inseriti a livello di rete e **sono un identificatore univoco delle nostre connessioni**
	- Vengono forniti dall'ISP (Internet Service Provider), che è quindi in grado di tracciare la nostra persona e fornire il nostro identificatore

<br>
<br>

## Cyber-Physical Systems
I **sistemi cyber-physical** sono diversi da quelli discussi fino ad ora.
È presente una **componente fisica** che può influire nella sicurezza del sistema.

*Alcuni esempi sono:*
- Macchine smart
- Centrali connesse ad internet
- e-Health devices (es. pacemaker)

C'è un **agente fisico** che è all'interno della comunicazione.

### Attack surfaces
**La superficie di attacco in questo modo SI AMPLIA.**

Possiamo andare ad attaccare sia la connessione client-server ma anche l'oggetto fisico in se, es. macchina smart, ...

La superficie di attacco si applica:
- a livello Fisico
- a livello di connessioni

### CIA Triad nell'OT
1. **Availability**
2. **Integrity**
3. **Confidentiality**

La **disponibilità** deve essere al primo posto, es. centrale nucleare connessa.


### Smart Cars Security
Il **CAN bus** è protocollo standard per la comunicazione nelle auto:
- È molto semplice
- NON è molto sicuro

### Industrial Traffic Analysis
Spesso si cerca di analizzare il traffico non protetto di un'industria esposto su internet o di misurare le attività malevole che hanno come obiettivo le attività industriali. ???

NB. **Shodan**

### Honeypot
Nell cybersecurity non abbiamo la certezza al 100% che un sistema sia sicuro.

**Si introduce un componente in più nella nostra rete che faccia da vittima per l'attaccante.**

L'**honeypot** da qualcosa da analizzare in pasto all'attaccante, è quindi volutamente vulnerabilie, in modo tale che la prima cosa che un attaccante vede quando cerca di attaccare la rete è questa.

All'interno di questo possono essere inseriti dati falsi che però simulano dei dati reali.

L'honeypoy ha come scopo quello di bloccare / limitare / rallentare l'attacco e molto spesso **logga** tutto ciò che fa l'attaccante per analizzarne il comportamento.

Molto spesso si crea una rete parallela a quella reale, con più honeypot, da rendere così il sistema il più "appettitoso" possibile.

