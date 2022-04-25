# Modulo 1 - Difesa

### Formazione del personale
- **Security awareness**: formare il proprio personale

### Procedure di sicurezza
- Policy
- Processi di recovery
- Procedure di autorizzazione

### Security Posture
È quanto siamo "messi bene" in termini di gestione della sicurezza. Insieme di processi e awareness che un'azienda fa

### Vulnerability Management
È un **processo** di identificazione, valutazione, trattamento e segnalazione delle vulnerabilità di sicurezza nei sistemi e nel software.

- Vulnerability assessment periodici
- Risk ranking delle vulnerabilità rilevate, il rischio va comunque in funzione del sistema chestiamo utilizzando, se connesso o meno, ecc.
- Remediation devono essere periodici

### Hardening
"Indurimento del sistema", ci sono delle linee guida da seguire:
1. Minimizzare software e servizi
	Se non hai bisogno di un software o un servizio, disinstallalo, così da diminuire **superficie d'attacco**

2. Utilizzare più sistemi per servizi diversi
	Es. server per front-end, un altro per back-end, un altro per il db,... .
	
3. Cifrare le trasmissioni
	Cifrando le comunicazioni si evitano attacchi MITM. Non usare protocolli che comunicano in chiaro come TELNET.
	
4. Non usare account condivisi
	L'amministratore deve sapere la singola persona che sta accedendo/facendo/ecc.
	
5. Non fare login con root
	Meglio utilizzare il comando **sudo** per eseguire programmi con altri privilegi. Utilizzando sudo le azioni vengolo **loggate**
	
6. Manutenere gli account
	Password forti (es. > 12char), cambiate regolarmente, gli account non più utilizzati devo essere rimossi (o disabilitati)
	
7. Two-factor authentication
	Per sistemi critici l'autenticazione deve essere basata su più fattori, generalmente una password e un codice temporaneo (OTP) o l'impronta digitale.
	
8. Utilizzare il principio di "least privilege"
	Non avviare servizi con l'utente root. Dai agli utenti i privilegi minimi indispensabili. I processi NON devono essere avviati via root.
	
9. Monitorare attività di sistema
	Revisionare periodicamente i **log** di sistema ed **inviarli ad un sistema centralizzato esterno**, tipicamente un SIEM, così da evitare che vengano eliminati durante un attacco.

10. Utilizzare il firewall
	Secondo il principio "least privilege", autorizza solo le connessioni necessarie e "droppa" tutto il resto, anche se il sistema sta dietro un firewall hardware.
	
11. Cifrare i dati sensibili
	Oltre alla cifratura delle connessioni, è necessario cifrare i dati sensibili
	
### Full disk encryption
Il sistema operativo deve avere accesso ai file decifrati per poterci lavorare.
Quando accendiamo il computer e lo sblocchiamo, salviamo la chiave in ram che permette di tenere il disco sbloccato.

### OS hardening
- Aggiornamenti di sicurezza
- Aggiornament di sistema
- Aggiornamenti degli applicativi
- Rimozione servizi inutilizzati
- Segmentazione di rete e **firewalling**

##### Hardening degli account
- pwd forti
- 2 factor authentication
- scadenza della password
- **lockout** in caso di login errato
- disabilitazione per non utilizzo 

NB. può essere che ci siano degli account per i servizi sempre attivi e sempre con la stessa pwd

## Sistemi di difesa

##### Firewall
Dispositivi hardware (o software) che prevengono gli accessi non autorizzati da e verso le reti private.

Ha un **ACL** (lista di regole), ogni singola entry specifica una regola (es. blocca traffico su porta 80 verso questi server:...). Si può essere molto specifici

Siamo al livello 3/4 dell'ISO/OSI

Analizza tutti i pacchetti e blocca quelli che non rispettano le policy

##### WAF, web application firewall
Filtra e monitora il traffico http, in genere protegge le applicazioni web

Siamo al livello 7 ISO/OSI (Applicativo)

#### IDS
2 tipi di IDS:
1. **Network-based IDS**: macchina posta nella rete in modalità **promiscua**, cioè in **ascolto sul traffico**, in grado di generare alert in caso di pattern malevoli. Avvisa solamente.
2. **Host-based IDS**:

#### IPS
Evoluzione di IDS, è un sistema proattivo che **rileva e cerca di bloccare le minacce identificate**. Monitora costantemente la rete per rilevare possibili attacchi/incidenti

#### Antimalware
Software in grado di rilevare le minacce malware presenti sulla rete o sul sistema.

Gli **antimalware enterprise** hanno una console di gestione centralizzata.

#### Secure Email Gateway
es. proxmos email gateway

Un **SEG** è un dispositivo o un software utilizzato per il monitoraggio delle e-mail. **Filtra le mail indesiderate** come spam, phishing, malware ecc.

Può anche **criptare automaticamente le mail** che contengono informazioni sensibili.

<br>

# Tecniche di evasione
Il concetto principale di evasione è quello di far vedere altro agli amministratori mentre sto agendo sul sistema vittima.

### IDS evasion
1. **Obfuscation**
Dobbiamo ofuscare il traffico che facciamo passare, io sto mandando A ma in realtà l'IDS vede B. Consiste nell'**encoding** (modo di rappresentare un determinato numero di bit in base ad una codifica) del pacchetto, contenente un payload, in maniera tale che sia decifrabile solo dall'host target e non dall'ids, in genere viene utilizzata la crittografia o l'encoding Unicode.

NB. encoding : in ASCII vuol dire una cosa , in UNICODE un altro

2. **Insertion attack**
Confonde l'ids facendogli leggere pacchetti non validi, l'obiettivo è quello di "sovraccaricare l'ids"

### Firewall evasion
1. **IP address spoofing** - l'attaccante maschera il proprio ip come se fosse un host fidato. Es. prima di mandare un pacchetto modifico l'ip sorgente, ciò mi permette di entrare come "fidato" nel sistema. Questa tecnica è utilizzata anche per il **port scanning**.
2. **Bypass di siti web bloccati** - alcuni siti web permetto di navigare su altri siti web attraverso di essi, ...
3. **DNS tunneling** - tecnica che permette di inviare dati attraverso richieste DNS (che sono in genere sempre consentite). ES. faccio richiesta dns all'interno della rete aziendale, se il server dns non riesce a rispondere la richiesta dns esce all'ESTERNO, a quel punto di può fare tunneling.
4. **Firewall bypass tramite ICMP tunneling** - I pacchetti ICMP hanno header (classico) poi hanno il payload dove possiamo inserire ciò che vogliamo, il meccanismo è simile a quello del dns tunneling

##### Encoding
- Unicode
- Decimal
- Hexadecimal
- URL encode

Servono per fare evasion

NB. tool CyberChef, ha molti strumenti, tra cui la parte di encoding
NB. Quando andiamo a cercare un malware calcoliamo l'hash in locale e diamo quest'ultimo ad es. VirusTotal

### Web application security
Livello 7 ISO/OSI (applicativo)

Alcuni sigle:
WA-PT : web application penetration testing ????

OWASP, ente che si occupa per la definizione di criteri di security di **applicazioni web**

##### Metodi più utilizzati secondo OWASP 2021:
1. Broken Access Control, riuscire ad autenticarsi al sistema senza account/...
2. Cryptographic Failures, per 2 principali motivi: errore di implementazione, errore di design
3. Injection
4. ...
10. Server-Side Request Forgery

#### Broken Access Control
L' **Access Control** permette l'implementazione delle policy di accesso, ad es., facendo in modo che gli utenti non possano agire al di fuori delle autorizzazioni previste.

Questo meccanismo può essere implementato male

#### Cryptographics Failure
Cosa fare per evitare ciò:
- Determinazione dell'utilizzo della cifrature
- Cifrari sicuri
- Dati NON in chiaro
- Degradazione HTTPS, nel momento in cui il client comunica col server, se quest'ultimo non è configurato correttamente è possibile passare ad una versione https vecchia con molte vulnerabilità da sfruttare

#### Injection (OWASP 2021)
- Code injection
- SQL injection
- LDAP injection
- ...

#### Insecure Design (OWASP 2021)
C'è una differenza tra **progettazione insicura** e **implementazione insicura**.
Un design sicuro può avere difetti di implementazione che portano a vulnerabilità. Un design insicuro non può essere corretto da un'implementazione perfetta.

#### Security Misconfiguration (OWASP 2021)
- Sistemi/Applicazioni non configurati
- Feature NON autorizzate ma attive
- Account di default
- Gestioni non gestite. **try-catch**, nel momento in cui il programma non riesce a fare una determinata azione lancia un'eccezione, se questa cosa non viene gestita possono esserci delle vulnerabilità.
- Security settings in web server

#### Vulnerable and Outdated components (OWASP 2021)
Cose da non fare:
- Utilizzo di sofware DATATI
- Utilizzo di software che sappiamo essere VULNERABILI
- Componenti di terze parti non testati. Es. quando implementiamo delle libreria (di 3e parti) bisogna che questa sia testata, oppure la testiamo noi stessi.

#### Identification and authentcation failures (OWASP 2021)
Per ovviare a questo problema bisogna fare una corretta gestione delle identità,...

3 problemi riccorrenti:
- Brute forcing, bisogna prevedere quindi un lock-out dell'utente dopo un tot di login
- Gestione scorretta di SSO, SSO aiuta nella gestione della sicurezza e nel tracciamento dell'identità, una sua scorretta implementazione causa molti problemi

NB. Perchè viene preferita il SSO rispetto ai singoli account? Perchè facendo il login con SSO l'authnticate provider si occupa di verificare l'identità dell'account

Nell'SSO è fondamentale ablitare il multifactor authentication

- Information discolsure tramite URL, es. applicativi che inseriscono la password nell URL o viene gestita l'autenticazione tramite URL.

NB. Spesso si trovano anche dei form nascosti nelle pagine che hanno lo stesso problema visto sopra

#### Software and Data Integrity Failures (OWASP 2021)
Quando un applicazione si basa su librerie/plugin/moduli o CDN NON ATTENDIBILI, rischiamo di integrare vulnerabilità dentro il nostro software

#### Security Logging and Monitorign Failures (OWASP 2021)
Il LOG è fondamentale, dobbiamo essere in grado di ricostruire le azioni di un eventuale intruso

COSE DA NON FARE:
- Log salvati solo sulla macchina locale poichè possono essere distrutti/cancellati. I Log devono essere spediti in un sistema REMOTO
- Log amministrativi poco precisi, va tracciata qualsiasi cosa che fa, ad es. un amministratore, all'interno del sistema
- Log applicativi inesistenti o poco esplicativi

*Esempi di log*
LOG AMMINISTRATIVI: utente accede al sistema
LOG APPLICATIVI: l'utente è all'interno di office, l'utente invia una mail

#### Server-side Request Forgery (OWASP 2021)
Si verifica quando un'applicazione web recupera una risorsa remota senza convalidare l'url fornito dall'utente.
...
...
...

### Footprinting di inffrastruttura web
- **Server discovery**:
- **Service discovery**: per scoprire quali servizi ci sono dietro le porte aperte
- **Server identification**:
- **Hidden Content Discovery**: scoprire contenuti/funzionalità NASCOSTE che non sono raggiungibili direttamente.

### Detection di WAF e Proxy (sempre in ambito web)
Devo capire se davanti a me ho effettivamente un server o un PROXY / WAF.

**PROXY**
Tendenzialmente quando ci colleghiamo ad una rete aziendale, c'è un server proxy che rigira tutte le nostre richieste. I proxy vengono utilizzati per filtrare i contenuti web o monitorare il traffico, si utilizza anche per migliorare la gestione del traffico interno della rete: il proxy colleziona tutte le richieste uguali, lui ne fa una unica e poi la rigira a tutti gli utenti che l'hanno richiesta.

**WAF**


Proxy e waf lasciano delle tracce all'interno dei pacchetti header, con dei tool possiamo verificare questa cosa. Per waf utilizziamo **waffw00f**

Se sappiamo che abbiamo un waf davanti a noi il payload più semplice non funzionerà mai, dobbiamo utilizzare tecniche più complesse. Es. sappiamo che abbiamo davanti un waf AWS e che per questo ci sono determinati payload

##### OWASP Web Security Testing Guide
Sono delle guide da seguire per un corretto sviluppo di una Web Application stabilite dall'OWASP

Nella sezione 4 c'è la parte "testing", cioè come testare una web application

<br>
<br>

# Attività POST-ATTACCO
### Incident management (completare)
È un'insieme di processi, procedure che hanno poi delle fasi operativi.
Tutto questo processo deve avere almeno:

1. Vulnerability Handling, cioè come gestiamo una vulnerabilità nata o già esistente e utilizzata, si va quindi a rivalutare con il *risk ..., vulnerability managment* 

2. Incident Handling: 
	1. triage, cerchiamo di capire cosa sta succedendo
	2. incident response
	3. reporting and detection, stiliamo una serie di documenti su cosa è successo e perchè
	4. analisi, andiamo ad analizzare l'incidente in se, la vulnerabilità, ...

3. Artifact Handling, non serve c'è, un artifatto è un pezzo di qualsiasi cosa che è stato attaccato. es: mettono un ransomware in un server, noi facciamo il dump della ram o un immagine del disco da utilizzare come prova
4. Announcements
5. Alerts

### Post-mortem analysis
1. Stilare un Incident Report, come sono entrati, con quale vulnerabilità, cosa si può aggiornare
2. Monitoraggio Post Incident, verificare che qualcuno non stia continuano a sfruttare quella vulnerabilità
3. Aggiornare IoC (Indicatore di compromissione) di threat intelligence, nelle grandi aziende, aggiornando questi ioc con l'hash dell'attacco che abbiamo ricevuto, di un indirizzo ip malevolo, ... ,  il sistema di threat intelligence ci avvertià prima nel caso venga riproposto lo stesso attacco.
4. Identificare nuova misura di sicurezza, andiamo a cambiare le policy e la gestione della sicurezza interna dell'azienda
5. Imparare

### Digital forensics
Insieme alla parte di Post-Mortem ci sarà questa parte.

Permette l'analisi post'attacco anche nel caso in cui l'attaccante copra le proprie tracce:

Alcune procedure:
- recovery dei log
- Recovery di file elimitati
- network forensics
- dump di memoria
- dump del disco (a basso livello, copia dei bit uno ad uno tramite i settori)

NB. La prima cosa da fare in caso, ad es. di ransomware, è NON SPEGNERE il sistema, cancelleremo i dati della ram e alcuni log e non saremmo in grado da quale connessione web è arrivato il ransomware.

### Log Analysis
- Fondamentale in caso di attacco
- Procedura che andrebbe eseguita regolarmente
- SIEM, log vanno spostati su sistema esterno
- **Log applicativi**, spesso sono impossibili da controllare poichè l'applicazione è già stata scritta in un determinato modo
- **Log di sistema**
- **Log network**, inserendoci dentro la rete e snifffando