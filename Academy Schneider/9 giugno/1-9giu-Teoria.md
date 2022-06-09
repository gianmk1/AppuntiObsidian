# Indutrial Cyber Security - Teoria
*Esempio: in un impianto petrolchimico ci sono dei processi che devono rimanere sempre attivi, qualsiasi variazione potrebbe provocare un'esplosione.*

Cyber Security nel mondo industriale significa mettere in atto dei sistemi di sicurezza per tutelare i lavoratori, l'ambiente ed evitare perdite economiche (più o meno ingenti).

## Scenario attuale
Gli attacchi ai sistemi industriali sono sempre più in crescita, attacchi ad impianti fisici hanno spesso lo scopo di **creare dei danni fisici** come **incendi, allagamenti,...**

I sistemi IoT sono device che mandano dei segnali utilizzando Internet a dei sistemi di controllo, **sistemi collegati ma distribuiti**.

OT = sistemi e reti per far funzionare un impianto, fino a qualche anno fa **erano isolati**, oggi non è più così ma si sta convergendo verso software opensource e hardware commerciale.

## Da dove vengono le minacce
**NB**. I threat intelligence sono le attività di ricerca di possibili attacchi per andare ad individuare delle possibili minacce.

1. Malware as a Service
2. Hacking as a Service
3. Crimeware as a Service
4. Fraud as a Service

Gli attacchi possono essere non soltanto legati a delle richieste di riscatto ma anche legate a dei gruppi (es. Anonymous, Killnet).

## OT - Operational Technology
Reti e sistemi che hanno a che fare con degli impianti, l'obiettivo è quello di mantenere l'impianto attivo e in sicurezza

## IT - Informational Technology
Reti e sistemi con lo scopo di mantenere processi attivi, mantenere la confidenzialità delle informazioni.

## IT vs OT
Nel mondo IT la confidenzialità è al primo posto, seguita da integrità e disponibilità.

Nel mondo OT invece la **disponibilità va al primo posto** seguita da integrità e confidenzialità. Il sistema deve funzionare sempre e deve avere ridondanze.

## Performance nel mondo OT
Nel mondo OT, a differenza di quello IT:
- **Tempo di risposta è un fattore critico e deve essere immediato**
- Circolano informazioni di dimensione limitata
- Funzionamento continuo
- Interruzioni intollerabili
- Il riavvio potrebbe non essere accettabile
- Test consentiti solo in ambito non di produzione
- **Importante documentare tutto quello che viene fatto**, es. cambio di versione di un software,... Anche dopo l'aggiornamento di un sistema bisogna **ri-certificare un sistema**
 - Sistemi operativi embedded
 - **Sistemi legacy**: devono durare anche 15 anni senza che vengano modificati
- Le risorse di calcolo sono limitate

**NB**. **HSE** ---> Protezione dell'ambiente, delle persone e della salute

### Falsi miti sulla sicurezza industriale
1. *Non siamo connessi ad internet*
2. *Abbiamo un firewall*
3. *La nostra struttura non è un bersaglio*
4. ...

1. Spesso non si ha una conoscenza approfondita dell'impianto industriale, **potrebbero esserci dei collegamenti ad internet** senza che noi lo sappiamo
I punti di accesso poi non interessano solo la connessione Internet, è possibile trasmettere un malware anche grazie ad una pendrive o ad un PC già infetto.
Un altro punto di attacco possono essere la **rete di sorveglianza** che spesso non è isolata dalle altre.
**NB**. In un'azienda ci sono vari "layer": OT, IT, ...

2. Anche i firewall hanno delle vulnerabilità e soprattuto capita che questi **vengano configurati in maniera non sicura (porta lasciate aperte in modo non controllato,...)**

3. Tutte le aziende che producono sistemi di controllo industriale sono **obbligate le vulnerabilità trovate nei loro sistemi**, oltre ad aiutare gli utilizzatori questo però aiuta anche i possibili attaccanti.
*Vedi sito ICS-CERT*


**NB**. Un **sistema di safety** va a leggere i dati critici all'interno di un impianto. Quando rileva che i valori stanno andando sopra una certa soglia **avverte il personale** e **può anche spegnere la macchina**.
Se questi sistemi vengono messi fuori servizio i **danni possono essere molto ingenti.**

## Obiettivi attacco cyber
1. **Ottenere informazioni**
2. **Prendere il controllo di un impianto**
	1. Fermarlo
	2. Creare danni (incendi, allagamenti,...)

### 3 ASSI
Quando si fa cyber security in ambienti industriale solitamente porta a **muoversi in 3 assi**: **Tecnologie**, **Processi** e **Persone**. 

**NB**. A priori è necessario costruire un piano di gestione degli incidenti o degli attacchi.

**Walling** è uno specifico phishing fatto alle persone apicali all'interno di un'azienda.

### Principali punti di accesso critici
- Firewall non configurati
- Phishing
- Links ai database
- Accessi dei fornitori (supporto tecnico), una VPN non rende il collegamento sicuro poichè comunque è possibile trasmettere un virus se la macchina è infetta.
- Accesso remoto ai dispositivi RTU
- DDOS, spesso tramite botnet, serve per mettere fuori uso un server/...

**NB**. **NERC**, ente di standardizzazione statunitense.

##### Difesa nella cyber security
Se un impianto va protetto bisogna mettere a disposizione un bugdet consistente.

Inoltre bisogna **implementare degli standard**, cioè delle raccolte di indicazioni che consentono di **muoversi in modo organizzato e strutturato** e non per tentativi o per sentito dire.

1. **Policy** = documenti ad alto livello
2. **Standard**
3. **Guidelines / Procedure** = indicano come le idee iniziali e gli standard devono essere applicate all'interno dell'azienda (sonn **molto specifiche**)

### Standard
Sono diversi gli enti che emettono questi standard. Alcuni di questi possono essere **enisa**, **NIST**, **NERC**,...

##### IACS
Tipicamente un azienda è divisa in
- **External Zone** (IT)
- **Corporate** (IT), tutta la parte di gestione degli utenti, degli accessi web, delle mail, degli AP all'interno della struttura
- **Process Zone** (OT)
	- **Control Zone** (OT)
- **Safety Zone** (OT), opzionale *vedi sopra* -> IEC 61508

#### ISO 27001
Standard essenziale nel mondo IT, relativo alla **gestione, custodia e amministrazione dei dati**.

#### GDPR
Documento che specifica **come, per quanto tempo, con che gestione devono essere mantenuti i dati**.

Il GDPR spesso entra anche nel mondo OT, come nel caso dei **sistemi di videosorveglianza**.

#### IEC 62443
Standard essenziale nel mondo OT, relativo alla sicurezza della strutture industriali.

#### IEC 61508
Riguardante i **sistemi di safety**

##### NIS
Legge entrata in vigore nel 2016, le società che si occupano di trasporti, energia, acqua, porti,... sono considerate **servizi essenziali**. Questa legge si concentra su queste strutture.

<br>

# IEC 62443
Questo standard è composto da 14 pubblicazioni su 4 livelli

1. **Generale**
2. **Policies e Procedure**, serie di documenti tipicamente in carico al proprietario dell'infrastruttura, es. come selezionare i fornitori/system integrator,... 
4. **Sistema**, come disegnare i sistemi, come fare un **risk assesment**, come implementare le **misure di sicurezza**
5. **Componenti**, come i componenti devono essere disegnati e prodotti in azienda

**NB**. **Maturity Level** = livello di maturità cyber dell'azienda
**NB**. I **COMPONENTI sono delle unità minimali che messi insieme compongono un SISTEMA**

Quando si progetta un sistema bisogna considerare la sua globalità, *il sistema è tanto sicuro quanto lo è il suo punto più debole*.

### Concetti di riferimento
Impostare un progetto di cyber security vuol dire procedere a step:
1. **Assesment**, per capire quali sono le vulnerabilità della macchine all'interno dei nostri sistemi.
2. **Implement**, disegnare in maniera corretta il nostro sistema
3. **Maintain**, stipulare un piano di "manutenzione" del sistema

### DMZ
Perchè serve una **DMZ** per mettere in sicurezza un impianto?

Tutto il traffico dall'OT all'IT e viceversa deve terminare nella DMZ, questa logica serve per **evitare un passaggio livello diretto** dal mondo industriale a quello enterprise.
La DMZ viene poi delimitata da un Firewall Nord (verso IT) e un Firewall Sud (verso OT)

Alcuni livelli all'interno di una struttura aziendale:
Livello 0 : rete di strumenti e sensori
LIvello 1 : rete di controllo locale in impianto
Livello 2 : rete di supervisione
Livello 3 : rete di gestione operazionale
**Livello 3.5** : rete dove sono presenti i sistemi tipici della cyber security

### Zone
Definire una zona vuol dire delimitare il **gruppo di assets con lo stesso livello di sicurezza**. Ogni zona può connetersi ad un altra **tramite un SOLO conduit**.

### Conduit
**È il collegamento tra una zona e l'altra**. Questo deve essere fatto implementato dei sistemi che analizzano il traffico (**IDS**). 

**NB**. Il passaggio da una zona all'altra deve essere possibile tramite un **singolo conduit**.

### Difesa di profondità
Più stati di difesa ci sono e più l'attaccante viene limitato e scoraggiato nell'attacco.

<br>

### Linee guida di una DMZ
1. Il traffico viene filtrato sia in ingresso che in uscita dalla DMZ
2. Deve limitare al minimo necessario lo scambio di informazioni (es. non deve essere possibile consltare le mail nella rete OT)
3. Soltanto gli IP in whitelist possono transitare attraverso il firewall
4. Firewall deve eliminare i pacchetti con indirizzi anonimi
5. I server devono essere **"hardenizzati"** e **manuntenuti** (sempre passando per la DMZ).
6. I sistemi di controllo industriale non devono avere accesso diretto ad internet

### Modello di Sicurezza
La **difesa in profondità (= Defense in Depth)** fa parte dai concetti di utilizzare questo si sta disegnando la rete di un'azienda. 

- Lettore di badge (**livello fisico**)-> limitare accesso fisico le persone non autorizzate
- **Policy e procedure** -> come devono essere le psw, definire i backup, i restore, ...
- **Progettazione dell'architettura della rete**
- **Sicurezza sugli host** -> antivirus, firewall, blacklisting, whitelisting, sandbox
- **Sicurezza dell applicazioni** -> software aggiornato, verifica dell'input dell'utente, gestire il patching

### Quali sono le minacce?
- Hackivisti
- **Criminali**
- **Insider** -> persone all'interno dell'azienda che passano informazioni
- **Spionaggio** 
- Terrorismo -> gli attacchi hanno lo scopo di creare DANNI o mettere in down dei servizi
- Guerra

<br>

### Security Level
All'interno dell'**IEC 62443** sono stati definiti vari **security level**:
- **SL1**, 
- **SL2**
- **SL3**, attacchi più strutturati e con quantità di risorse maggiore
- **SL4**, associazioni finanziate da stati esteri, organizzazioni di guerra cibernetica

### SIL
Classifica che identifica la percentuale di un sistema di mantenersi attivo in base a determinate condizioni.

Più è alto il scurity level più il sistema è in grado di resistere ad attacchi o rimanere disponibile

### Definire un security level
Vengono valutate le seguenti caratteristiche:
- Come viene gestito e controllato l'accesso alle macchine
- Come vengono tracciate le attività dell'utente
- Quali sono i sistemi di controllo delle informazioni
- Quali sono i protocolli di comunicazione
- Come è stata definita l'archiettura del sistema
- Come il sistema è in grado di reagire in confronti di un'attacco (**logcollector**, **log-analisys**)
- Come sono gestite le ridondanza sulla rete e sugli host

Quando si fa una **compliance** per verificare a quale Security Level si appartiene bisogna verificare ciascuno dei requisiti di ogni sezione vista sopra.

**NB**. Le VLAN **segregano in maniera LOGICA le varie aree**, per adottare uno standard di sicurezza maggiore è consigliabile **segregare anche in modo FISICO**.

#### SL2
Oltre alla segmentazione orizzontale dell'SL1 vengono inseriti dei **IDS**, cioè dei sistemi che messi a ridosso della DMZ che ascoltano il traffico e vedono se ci sono o meno anomalie.

**NB**. Per alcune settimane ascoltano solamente il traffico per **creare una BASELINE del traffico**, in seguito il traffico passante verrà confrontato con questa baseline.

Il passaggio da un SL1 ad un SL2 comporta elevati costi e molte risorse.

#### SL3
Viene definito un **timestamp**, in questo modo tutte le macchine sono **sincronizzate tra di loro**, se vado a leggere i LOG posso correlare gli eventi tra le varie macchine.

Inoltre è presente un monitoraggio continuo che tiene sottocontrollo quello che avviene nell'impianto ed è pronto a segnalare eventuali anomalie.

<br>

L'obiettivo è quello di realizzare un progetto che mostri da un lato quali possono essere i possibili danni a cui l'azienda potrebbe incorrere. Dall'altra parte i costi che devo affrontare per realizzare un determinato sistema (SL1, SL2,...), bisogna quindi **capire qual è il Security Level più adatto per l'azienda**.

<br>
<br>

## Come disegnare un'architettura di rete?
Definire le zone all'interno di un impianto è un punto abbastanza critico. Ci sono varie metriche con cui possiamo delimitare le varie zone, es. tipo di processo, prodotto, ...

Questo passaggio può richiedere molto tempo, soprattutto perchè c'è bisogno di "intervistare" gli operativi e il personale abituale.

## Tipi di DMZ
**ES**. Con firewall NORD e SUD al cui interno possono essere presenti i server che si occupano delle patch o aggiornamenti dei sistemi.

<br>

## Sicurezza dei prodotti
Nonostante i prodotti obsoleti o non aggiornati possono comunque mantenere uno standard di sicurezza elevato adottando l'azienda di Firewall, IDS, DMZ,...

Quando invece devo partire da 0 posso andare a scegliere dei sistemi che hanno **embedded** dei sistemi indirizzati alla sicurezza.

Questi prodotti **devono essere CERTIFICATI**. A livello normativo sarà introdotto a breve dei requisiti di certificazione obbligatori.

Nello standard IEC 62443, i prodotti vengono certificati su 2 metodologie:
- Come deve essere fatto il prodotto
- Come il prodotto ha al suo interno degli standard di sicurezza

1. Deve avere un obiettivo finale
2. Come è sviluppato il software
3. Come è sviluppato l'hardware
4. Come software, hardware e firmware comunicano tra di loro
5. Valutazione sull'hardware
6. Verifica di funzionamento

Superati questi livelli, **ad ogni vulnerabilità riscontrata sul sistema**, questa deve essere segnalata e l'**azienda produttrice deve prendersi carico di questa e fornire tempestivamente una patch**.

**NB**. Può essere certificato anche un sistema nel suo insieme. Se anche una sola componente di questo sistema viene modificata bisogna ri-certificare l'intero sistema.

<br>
<br>

# Cyber Security in Italia
Secondo la direttiva NIS è stato stabilito quali sono gli enti italiani a quali è affidata la sicurezza informatica del paese.

2 sono le aree di interesse:
- **Operatori di servizi essenziali (ESO)** -> energia, trasporti, banche, sanità,... , questi enti devono sottostare a precise regole e standard riguardanti la cybersecurity
- ...

Alcuni obblighi per gli ESO sono:
- Risk managment
- Mitigazione degli impatti
- Notificare al ministero evenutali attacchi cyber

<br>

# Realizzare un progetto di cybersecurity
1. **Assesment**, può essere fatto a livello passivo o attivo. Questo permette anche di capire quanto sono o meno compliance ai vari security level.
2. **Defence in Depth** (Studio)
3. **Implementazione**
4. **Monitoraggio**
5. **Manutenzione continua**

Il tutto deve essere accompagnato da un piano di informazione che comprenda tutti i dipendenti.