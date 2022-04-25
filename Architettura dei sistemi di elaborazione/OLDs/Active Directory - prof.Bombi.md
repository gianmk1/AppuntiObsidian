# Active Directory
Un dominio Windows consente un **single sign-on o SSO**, io ho le mie credenziali e con queste posso accedere su qualsiasi dispositivo della rete (a seconda dei ruoli).

Se la persona non lavora in una singola postazione, questo SSO semplifica di molto gli accessi, anche all'amministratore di rete.

Amministrare un dominio Windows consente di amministrare gli utenti in **modo CENTRALIZZATO**.

In realtà nel momento in cui si vanno a definire gli utenti si possono anche definire accessi/permessi/funzionalità specifici per **gruppi di utente**, quindi si possono dare o ampliare che determinati gruppi di utenti possono fare.

#### Alcune caratteristiche:
- **DOMINIO WINDOWS**: è un insieme di computer logicamente collegati e gestitti da uno o più **domain controller**.

- Un **domain controller** è un computer in cui è installato una versine di Windows Server e su cui sono attivati i servizi di Active Directory

- Active Directory è una directory in cui sono ragistrati gli oggetti che compongono il dominio, a partire dai computer e dagli utenti.

- La directory è memorizzata nel Domain Controller

NB. La directory registra diversi tipi di **oggetti** come: **utenti**,**gruppi**,**computer**,...

Per tutti questi oggetti è possibile specificare dei ruoli, ogni tipo di oggetto si porta le proprie impostazioni. La directory quindi è un **elenco di oggetti strutturati**.


Active Directory rispetta lo standard **LDAP**. Che è possibile utilizzare anche in Linux.

#### Tipi di operazioni svolte su A.D.
**!!!** La directory è utilizzata principalmente in **LETTURA**. Ovviamente possiamo aggiungere utenti, modificare ruoli, ... , ma la maggior parte delle operazioni che vengono svolte sono svolte in lettura.

**NB.** Viceversa nei database sono frequenti le operazioni in lettura quanto quelle in scrittura.

#### Gestione centralizzata

L'infrastruttura di Active Directory consente la gestione centralizzata degli utenti e della sicurezza:
- **SSO** (Single Sign On)
- **Gestione delle politiche di sicurezza per l'intera organizzazione**, assegnando permessi a:
	- utenti
	- computer
	- gruppi
	- unità organizzative


Perchè l'azienda investe su un dominio Windows?
*Per avere la gestione centralizzata degli utenti. Il dominio inoltre può gestire poche decine di utenti ma anche migliaia di utenti.*

L'idea è quella di **gestire centralmente** quello che succede nel sistema.

NB. Aggiungendo un computer al dominio, anche questo viene visto da Active Directory (oltre che l'utente).

### La struttura
La struttura della directory si chiama **SCHEMA**

### Gruppi e unità organizzative
Oltre agli utenti e ai computer ci sono i **gruppi** e le **unità organizzative**.

Ci sono dei gruppi predefiniti, altri invece si possono facilmente creare. Questi gruppi successivamente possono essere organizzati come vogliamo. 

*Es1: possiamo configurare una connessione automatica a un drive di rete (es. Z).*
*Es2: ci sono poi degli **spazi condivisi (o share)** in cui si possono inserire delle directory, e per i vari gruppi di utenti impostare i permessi.*

NB. *Discuti le modalità di gestione del dominio windows?*

*Es3: dal punto di vista di una azienda, ci possono essere degli utenti che hanno bisogno di lavorare assieme e di condividersi dei file. Possiamo mettere tutti gli utenti che lavorano nel marketing nello stesso gruppo, e condividere a questo gruppo il disco di rete.*

- **Gruppi**: sono oggetti di active directory che si utilizzano per impostazioni di sicurezza, impostando policy di accesso comuni a gruppi di utenti o computer. **All'interno del gruppo gli utenti sono TUTTI UGUALI.**

- Le **unità organizzative** (strutturate ad albero) si impostano per esigenze amministrative e consentono ad esempio di delegare ad un utente la gestione, eventualmente parziale, dell'unità organizzativa.

### Albero e Foresta
NB. Inizialmente quando nacque Active Directory, prevedeva un solo domain controller, ora ce ne possono essere più di uno.


Si parte con un **domain controller**, a questo possono essere aggiunti sottodomini a formare un albero (che hanno anche loro un domain controller).

I sottodomini ereditano lo schema del dominio "padre" 


Nel momento in cui un server è un sottodominio di un altro server. Così facendo **l'uno si fida dell'altro**. C'è quindi la proprietà della **TRANSITIVITÀ.**

VS

Invece la foresta si ottiene collegando 2 alberi, però con una **one way trust**. 
*Esempio: nwtraders si fida di contoso*


### Replice
Il domain controller deve garantire la **fault tolerance**, se il dominio è in un unica rete LAN si utilizza quindi un **cluster**, i server all'interno hanno ognuno una propria copia di active directory e c'è un **costante aggiornamento l'uno con l'altro.**

**Load balancing**: mano a mano che le richieste arrivano queste vengono smistate ad uno dei server nel cluster.

**NB**. Se anche si ha un dominio piccolo bisogna sempre avere almeno un **cluster** di 2 server.

### Sites
Il dominio potrebbe essere su più reti locali, in quel caso ogni sito deve avere una copia della directory.

I siti consentono di distribuire geograficamente la repliche del domain controller. 
In questo modo ogni computer del dominio ha un controller nella propria rete LAN.
Le repliche appartenenti allo stesso sito sono in cluster, hanno collegamenti veloci e possono di fatto avere esattamente la stessa versione della directory.

**site link** = le linee che collegano i siti
**site link bridgeheads** = collegamenti ridondanti che consentono di evitare *single point of failure nella sincronizzazione*

### Roaming profile
Ci sono una serie di personalizzazioni dette **PROFILO UTENTE**, che solitamente vengono memorizzate in locale, questo solitamente comprende: *sfondo, cartella home, cookie del browser, ...*.

Il **roaming profile** permette che il profilo utente venga condiviso in rete e quindi l'utente lo ritroverà su ogni computer del dominio.
Per fare ciò bisogna:
- creare sul server un cartella in cui verranno poi creati i profili utente
- In gestione dell'utente, scheda "profile" modificare la directory del profilo.

### Permessi
Ci sono due categorie di permessi:
- i permessi di **share** (di condivisione)
- i permessi **NTFS**

*Quello che viene fatto se siamo in un dominio è creare comunque delle condivisioni, che però non risiedono sul computer dell'utente, ma dove è in esecuzione il domain server o su un altro server ancora. In questo caso i permessi di share devono essere NEUTRI, cioè tutti possono fare tutto. E per restringere i permessi, l'amministratore utilizza quelli NTFS.*

Nella gestione di un dominio complesso, è opportuno assegnare i permessi ai gruppi e non ai singoli utenti (piuttosto creiamo un gruppo con un solo utente).

Se a me si applicano 2 regole (essendo in 2 gruppi), si applica quella più restrittiva (**i permessi negati valgono di più di quelli assegnati**).

### Group Policy Objects
Con questo **tipo di oggetti** è possibile:
- abilitare/disabilitare applicazione
- impostare la connessione automatica a risorse condivise
- impostare l'esecuzione automatica di script/programmi

*Es. togliere il task-manager a tutti gli utenti di un unità organizzativa

