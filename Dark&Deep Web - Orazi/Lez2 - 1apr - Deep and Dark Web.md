# Deep and Dark Web
*Parlando della rete web utilizziamo la metafora dell'* **ICEBERG**: 
1. PUBLIC web: quello indicizzato e che utilizziamo tutti i giorni
2. DEEP web : percorsi che non vengono indicizzati dai motori di ricerca
3. DARK web: le risorse non sono accessibili da un normale browser (e dai classici protocolli)

## Deep WEB
- È una parte del world wide web, gli indirizzi non vengono indicizzati dai motori di ricerca.
- Spesso viene richiesta un **autenticazione** per accedere a queste pagine
- In realtà **la maggior parte dei contenuti disponibili in Internet NON è indicizzata dai motori di ricerca**, circa il **99%**

*NB. All'interno delle aziende ci sono i SEO che hanno come compito quello di indicizzare il più possibile il proprio sito web.*

Il web che conosciamo ha circa 4.5 miliardi di siti web indicizzati, nel deep web si stima questo valore sia maggiore di 400/500 volte.

## Come funzionano i motori di ricerca?
*Ci sono dei componenti:*
1. **WEB CRAWLER**: è un programma che si inserisce partendo dalla pagina web e insegue tutti gli indirizzi correlati a questa pagina.  Il file **robots.txt** contiene dei tag che permettono di indicizzare meglio il sito.

	**NB**. Solitamente durante un penetration testing è uno dei primi file che si cerca.

2. **INDEXER**: è un grosso database che cerca di tenere traccia di tutto quello che il web crawler trova, quindi **pagina, collegamenti per arrivare alle pagine, ...**

3. **SEARCHER**: 
	- Componente che cerca all'interno delle liste che sono contenute nell'indexer
	- Sfrutta il database dell'indexer e cerca di formare un **ranking**
	- È il primo componente che invochiamo quando facciamo una ricerca

	NB. Google fu il primo ad utilizzare un metodo di ranking basato sulle ricorrenze del sito
	

## Surface web VS Deep web
- Nel **SURFACE WEB** :
	-  domini e gli indirizzi sono **sempre gli stessi**
	-  ci sono **collegamenti tra le pagine**
- Nel **DEEP WEB**:
	- gli indirizzi spesso vengono generati **randomicamente** per rendere più difficile l'accesso.
	- le pagine solitamente non ne richiamano altre, **NON ci sono collegamenti ad altre pagine**

## Deep web CONTENT
- **DYNAMIC CONTENT**: Non c'è un dominio fisso ma si cerca di rendere difficile la ricerca all'interno di esse
- **UNLINKED CONTENT**: Le pagine NON sono linkate tra di loro: il **web crawler** non è quindi in grado di indicizzare il sito
- **CONTEXTUAL CONTENT**: le pagine cambiano in base a chi siamo (indirizzo IP, navigazione precedente, ecc.)
- **LIMITED ACCESS CONTENT**: sono presenti **molti CAPTCHA per prevenire l'utilizzo dei BOT**. Viene anche settato uno **specifico header (No-Cache Pragma)** che dice al browser di NON tenere in cache la pagina.
- **SCRIPTED CONTENT**: i contenuti spesso sono generati tramite script
- **Non-HTML/Text Content**: solitamente NON si carica testo HTML, ma si caricano piuttosto immagini/video, sempre per rendere difficile l'indicizzazione e ricerche
<br>
<br>

## Dark Web
- Per accedere al dark web bisogna utilizzare un determinato protocollo per accedere ai dati. 
- Il focus è quello dell'**ANONIMIZZAZIONE**
- NON tutto quello che c'è nel dark web è illecito
- Sono presenti molte informazioni nell'ambito della ricerca
- Sono presenti molte **guide per hacking / virus / ...**

Il mondo web è collegato con le cryptovalute poichè sono **difficilmente tracciabili**.

*Alcuni esempi:*
- **Freedom hosting**, era uno dei siti che produceva più traffico. L'FBI è riuscito a bloccare il sito tramite una vulnerabilità di Firefox 17 (su cui era basato TOR). Iniettando il malware su TOR è riuscita a tracciare delle transizioni.
- **Silkroad**, chiuso grazie ad un CAPTCHA non completamente anonimizzato

![[immagine vari market del dark web]]

#### Aspetti legali del dark web
- **GIORNALISMO**
- MERCATI LEGALI
- SOCIAL MEDIA
- MINORANZE REPRESSE

### Zero-Days vulnerabilities
Sono delle vulnerabilità di grossa entità che vengono scoperte prima che gli sviluppatori ne vengano al corrente. Molto utili per compiere attacchi (anche difficili da bloccare)

C'è quindi, appena la vulnerabilità viene resa pubblica, una **corsa al fixing**.

Nel dark web c'è un mercato anche per queste vulnerabilità zero-day

*Esempio: StuxNet*

NB. Un lavoro molto diffuso è quello del **bugbunty** che cerca di trovare vulnerabilità e bug all'interno di siti / sistemi

![[immagine slide ZERODIUM]]
<br>
<br>

## Cos'è TOR?
- È un browser basato su Firefox che **riesce a supportare la onion routing**
- Sviluppato dall'US intelligence
- Prima release pubblica nel 2004

Circa 4milioni di persone utilizzano TOR, e sono solo il 0.02% della popolazione mondiale che accede ad internet.

**TOR è lo standard più utilizzato** per mantenere la comunicazione privata.

## Uso classico di Internet
Internet è un "mondo molto aperto", quindi possiamo sniffare i paccheti che girano e capire molto da quest'ultimi. Le informazioni viaggiano attraverso diversi router.

Ci sono gli **header** dei pacchetti che descrivono quest'ultimi.
Ogni computer ha associato un proprio indirizzo IP, e può essere IPv4 o IPv6.

I pacchetti passano per molti router e quindi **non conosciamo il percorso che questi fanno**.

![[immagine internet e attaccante slide 29]]

Un attaccante, prendendo il controllo di un router, potrebbe sniffare il traffico.

## Come funziona invece TOR?
TOR utilizza la stessa infrastruttura fisica di Internet ma è un traffico nascosto.

I route che compongono la TOR network sono degli **onion router** che i volontari del progetto mangengono.
I pacchetti passano sempre da router normali, ma anche per questi **onion router**.

Ci sono **7000 onion router**.

### Funzionamento

![[immagine slide 34]]

Supponiamo che in una tor network Alice voglia comunicare con Bob.
La TOR network fa si che **il traffico che si scambiano PASSA SEMPRE PER ALMENO 3 ROUTER ONION**.

I router onion si chiamano:
- **guard router**
- **middle router**
- **exit router**

I router vengono decisi preventivamente all'instauramento della connessione. 

Il messaggio viene criptato con la chiave pubblica del router 3, il tutto viene criptato con la chiave del 2, e di nuovo viene tutto criptato con la chiave dell 1.

Il messaggio viene spedito, quando arriva al router 1, questo è in grado di **decriptare il primo strato della risorsa**, ma ci sono ancora 2 layer di cifratura.
Questo router sa solo **da chi arriva il pacchetto e a chi deve mandarlo**.

*Il router 2 toglie un altro strato della cipolla. Questo sa che il pacchetto proviene da router 1 e che è diretto a router 3.* **NON sa che il pacchetto proviene da Alice**.

*Il router 3 farà la stessa cosa.*

Ad ogni step sappiamo:
- Lo **step precedente**
- Il **prossimo step**

##### Problema: comprire l'ultimo step
Ci potrebbe essere un problema all'ultimo step, dove il messaggio sarebbe in chiaro. La soluzione è quella di **criptare l'ultimo strato del messaggio (quello dopo l'exit node) con la chiave pubblica di Bob**.

**NB**. Ci sono molti più guard e middle router, poichè l'exit ruoter è quello più a rischio legalmente parlando.

Possiamo utilizzare **HTTPS** o una **VPN**.


### Chi possiede i nodi?
- Volontari
- Spesso università e istituzioni
- È più semplice fare da middle o da guard
- C'è bisogno di una connessione stabile
- Essere exit node porta a problemi legislativi

### Distribuzione dei nodi
![[inserisci immagine slide 44]]

### Servizi NASCOSTI di Tor
Non ci sono dei servizi in chiaro con cui raggiungere i domini in più **NON C'È un SERVIZIO DNS**.

Tutti i server sono identificati da una stringa alfanumerica randomica con **.onion** alla fine. --> Non c'è alcun link tra server name e server address

### Anonimità in Tor
Raggiungere la perfetta anonimizzazione è impossibile. Molto spesso i metodi di pagamento possono essere un problema (anche tramite criptovalute), una semplice vulnerabilità poi potrebbe comportare la perdita dell'anonimizzazione.

**NB**. Anche piattaforme come Wordpress e Joomla portano spesso vulnerabilità.

### Detection by protocol
Il **protocollo TOR non è infallibile**: è possibile "fare detect" ma **non c'è un vero e proprio metodo per evitare** che questo traffico venga riconosciuto.

### Come nascondere i propri servizi nel dark web?
*2 modalità*:
1. **NO spiders allowed**: i crawler non funzionano in questa rete poichè non riescono nemmeno ad accedere al dark web e i link sono delle semplici stringhe alfanumeriche randomiche
2. **Can't reach them**:
	- No DNS
	- ...

### Svantaggi di TOR
- Il processo di encryption comporta un **rallentamento della rete**, anche questa è una vulnerabilità poichè potrebbe esporci ad una traffic analysis
- Anche se l'Onion protocol sembra sicuro, non lo è al 100%, ci possono sempre essere bug
- Il **traffico TOR non può essere bloccato** a meno che non si stoppi l'intero servizio Tor (come in Cina)
- È possibile (anche se difficile) ricostruire il percoso all'indietro