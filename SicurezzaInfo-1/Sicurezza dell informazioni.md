# Concetti cyber secutiry

### Computer security
è l'insieme di misure e controlli che garantiscono **confidenzialità**, **integrità** e **disponibilità** delle risorse dei sistemi...

- **Confidenzialità**: informazioni (o sistemi) confidenziali rimangono tali, pertanto non accessibili a soggetti non autorizzati
- **Integrity**: le informazioni e i programmi sono modificati solo con metodi autorizzati. L'integrità dei sistemi invece si riferisce allo scopo di un determinato sistema, garantendo che esso possa eseguire solo le azioni per cui è stato programmato.
- **Avalibility**: garantisce che i sistemi siano disponibili, che funzionino e che il servizio che offrono non sia negato agli utenti non autorizzati. Es. se il sistema viene attaccato deve avere una **copia**

**NB**. **Ransomware**: malware che cifra i contenuti del disco e ne chiede il riscatto

#### Risorse di sistema e Asset

Risorse di sistema: CPU, RAM, disco rigido

**Asset**: risorse in generali, che possono essere:
- Hardware: computer, server, modem, firewall (fisici), antenne
- Software: sistemi operativi, applicazioni (tool di attacco o di difesa, ma anche una normale applicazione)
- Dati: dove vado a salvare l'informazione stessa 
- Rete: rete LAN e rete WAN, router

##### Terminologia 2/3
- Attacco: qualsiasi azione volta a collezionare, distruggere o degradare i sistemi informatici o l'informazione stessa. 
- Security policy: criteri di sicurezza che hanno lo scopo di mantenere un determinato livello di sicurezza. Vengono dai cyber-security manager, es. password di almeno 12 caratteri, password da cambiare ogni 90gg, ecc.
- Minaccia: quando un sistema ha un'informazione che interessa all'attaccante. Qualsiasi circostanza o evento che può impattare negativamente su un sistema informatico o un'informazione
- Vulnerabilità: in un sistema operativo, processo, policy o implementazione che può essere sfruttata per un attacco

L'attacco è l'azione effettiva, la minaccia è più a livello teorica, solitamente l'attacco si basa su una mincaccia

#### Attacchi e provenienza
L'attacco può essere passivo o attivo; esterno o interno
- Attacco attivo: tentativo di alterare le risorse di sistema o l'operatività di essa
- passivo
- interno
- esterno

### Schema
![inserire schema pdf]
Risk e Assets sono i 2 elementi principali, le minacce incrementano il rischio che si pone sull'asset.

### Minacce, Attacchi e Asset
- Asset; è una risorsa, importante per il propietario
- Minaccia: si concretizza nel momento in cui un sistema elabora informazioni che hanno un valore per un attaccante
- Attacco: quando si ha una minaccia e l'attacante riesce a sfruttare una **vulnerabilità**. Es. software vecchio

### Conseguenze alle minacce e attacchi
![[vedi schema]]

DISCLOSURE = quando si scopre una vulnerabilità

**Responsible disclosure**: quando appena trovo una vulnerabilità, non la rendo pubblica ma contatto il proprietario del sistema e gli do il tempo per sistemare la vulnerabilità, dopo posso diffondere l' accaduto

**Non-Repudation**: il sistema non può negare di avere ricevuto un'informazione, server soprattutto per i sistemi di LOG

### Requisiti funzionali
Un requisito funzionale è un requisito necessario per permettere ai sistemi di eseguire le operazioni per i quali sono stati programmati

- **Access Control**: permette l'accesso solo agli autorizzati
- **Awareness and Training**: spiegare al personale i rischi associati alla sicurezza
- **Audit and Accountability**: tracciare e monitorare le azioni degli utenti per permettere analisi in caso di attacco (i cosidetti LOG), il tracciamento è necessario anche per rispondere alle leggi
- **Certificaitions, Accreditations, ...**: Es. ISO 27-2001, effettuare deli assessment periodici sui sistemi e sulle reti per garantire i **criteri minimi di sicurezza**
- **Configuration Management**: riguarda la gestione delle configurazioni, avere una **baseline** minima di sicurezza, mantenere un elenco delle configurazioni dei vari applicativi
- **Contingency Planning**: stabilire dei piani in caso di emergenza, se mi attaccano e non ho un piano, non si agisce correttamente
- **Identification and Authentication**: serve per identificare gli utenti che hanno accesso ad un sistema, in molti sistemi è essenziale che l'utenza sia nominale
- **Incident Response**: stabilire un quadro operativo per le azioni in risposta all'emergenza: preparazione personale, detection del problema, piani di recovery post-incidente
- **Maintence**: manutenzione ordinaria e straordinaria sui sistemi
- **Media protection**: proteggere i media (documenti, foto,...) sia digitali che cartacei. Limitare l'accesso ai solo utenti autorizzati.


Contingency Planning (1) VS Incident Response (2):
es. se arriva un alluvione e mi allaga il data-center cosa faccio
es2. Risposta ad un attacco informatico 

- **Physical and ...**: limitare l'accesso **fisico** alle strutture e ai sistemi. Tracciare gli utenti autorizzati
- **Planning**: avere una documentazione per rispondere a delle situazioni (di emergenza e non)
- **Personal Security**: 1. Trasferimenti e licenziamenti devono rimuovere gli accessi non più necessari 2. Se sono AD ho un accesso alle informazioni molto più elevato a un dipendente di più basso livello
- **Risk assessment**: effettuare test periodici per mitigare i rischi, bisogna mantenere il rischio il più basso possibile
- **System and service acquisition**: allocare sufficienti risorse per rispondere adeguatemente ai requisiti di sicurezza. *Es.* un firewall sottodimensionato 
- **System comunication protection**: protezione della trasmissione (criptazione)
- **System integration integrity**: 


### Principi fondamentali di security design
Disegno di un sistema di sicurezza:
- **Economy and mechanism**: devo avere un sistema quando più semplice possibile, così mi è più facile difenderlo
- **Fall-safe default**: bisogna bloccare tutto e concedere esplicitamente l'accesso a specifiche risorse. Es. facciamo delle autorizzazioni per white-list
- **Complete mediation**: l'accesso deve essere concesso da un sistema ad hoc, senza l'utilizzo di cache, che deve essere aggiornato...
- **Open design**: il disegno di un meccanismo di sicurezza dovrebbe essere **aperto**, permettendo così ad altri ricercatori di sicurezza di verificare la bontà dei controlli 
- **Separation of privilege**: è un principio che va adottato per separare i privilegi. Utenti dello stesso sistema non hanno gli stessi privilegi
- **Least privilege**: ogni processo.... Se sono utente della banca e devo fare un bonifico non devo aver bisogno di entrare nel back-end del sistema...
- **Least common mechanism**: implementazione deve evitare l'utilizzo di funzioni in comune tra diversi utenti. Es. 
- **Psychological acceptability**: implica che i meccanismi di sicurezza non interferiscano con le attività dell'utente e rispettino
- **Isolation**: 
	1. sistemi ad accesso pubblico isolati dai dati/sistemi critici. Es. un azienda ha un sito pubblico per clienti e una intranet per i dipendenti
	2. Processi e file degli utenti isolati gli uni dagli altri se non esplicitamente concessi
	3. L'accesso ai sistemi di sicurezza deve essere isolato

- **Modularity**: le funzioni di sicurezza sono separate e l'architettura è modulare. 
- **Layering**: es. fallimento del firewall non compromette funzionamento di altri cosa


### Superficie di attacco

*La superficie di attacco dipende...*

Se ho un sistema completamente isolato

Le superfici di attacco sono di vari tipi:
- **Human**; vulnerabilità create dalle persone
- Software: vulnerabilità delle applicazioni, librerie,...
- Network: vulnerabilità presenti nella rete, internet,.. SI considerano anche le vulnerabilità dei protocolli


### Strategie di sicurezza
2 modi:
- Security policy: definizione di un documento che racchiude varie regole che devono essere seguite (es. cambio password ogni 90gg). Questi documenti vanno scritti dal team di cybersecurity e dal team a cui è rivolto questo documento => non bisogna ostacolare il lavoro altrui.

	Quando andiamo a disegnare una security polici dobbiamo considerare:
	- **Facilità di utilizzo**: (es. utilizzare psw di 40 caratteri)
	- **Costo della sicurezza**: dobbiamo valutare se il costo della sicurezza è maggiore del costo di un eventuale incidente, in quel caso bisogna modificare qualcosa

- Secutiry implementation: se il l'implementazionee non è fatta correttamente si creano dei bug, e quindi delle vulnerabilità
	Le implementazioni sono divise in 4:
	- **Prevention**: se faccio prevenzione nessun attacco riesce ad entrare nel sistema "idealmente" (es. cifrando il traffico rendo confidenziale il messaggio, )
	- **Detection**: es. un sistema IDS (Instrusion detection System, llivello 3 ISO/OSI, analizza il traffico di rete) è in grado di rilevare un'intrusione in un sistema o rete. Non agisce, rileva e basta.
	- **Response**: è la fase di risposta ad un attacco (in maniera difensiva), intesa come mitigazione. Es. attacco DoS posso mitigarlo con CDN e Firewall, così da distribuire il traffico per far riprendere il servizio
	- **Recovery**: è la fase post-attacco, es. **recovery**, utilizzo di un backup che mi permetta di ripristinare lo stato del sistema


### Alcuni standard
- **NIST**: national istitute of standards and technology, ente che emette molti standard dove definiscono alcune regole da utilizzare, es. come gestire le password, sviluppo del codice sicuro. Questi standard vengono rivisti ogni tot di tempo

- **ISO**: anche lui definisce degli standard es. ISO-27001: simile ad alcuni NIST che definisce come il nostro sistema deve essere gestito per lavorare in sicurezza

L'ISO permetta anche una **certificazione**, degli enti esterni tramite dei controlli certificano che il nostro sistema è congruo all'ISO-27001. Queste procedure sono lente e molto stringenti

Un altro stanard è il PCI-DSS che tratta il sistema di pagamento, oppure PDS2
NB. GDPR