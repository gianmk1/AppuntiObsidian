# Active Directory
*Alcune definizioni:*

- Un **Dominio Windows** è un insieme di computer logicamente collegati e "gestiti" da uno o più domain controller.
- Un **Domain Controller** è un computer in cui è installata una versione di Windows Server su cui sono attivi i servizi di Active Directory
- **Active Directory** è una directory in cui sono registrati gli oggetti che compongono il dominio, a partire dai computer e dagli utenti. Questa directory è memorizzata nel Domain Controller

### Gestione centralizzata
Amministrare un dominio Windows consente di gestire gli utenti in modo CENTRALIZZATO.
- Single Sign ON o SSO, con le mie credenziali possono accedere a "qualsiasi" dispositivo della rete (in base ai miei permessi)
- Gestione delle politiche di sicurezza per l'intera organizzazione, assgnando permessi a:
	- Utenti
	- Computer
	- Gruppi
	- Unità organizzative 

### La directory
La directory registra diversi tipi di **oggetti** come: utenti, gruppi, computer, UO. Per tutti questi oggetti è possibile specificare dei ruoli, ogni tipo di oggetto si porta le proprie impostazioni.

La struttura della directory si chiama **SCHEMA**, ed è estendibile.

La directory quindi è un **elenco di oggetti strutturato**.

#### Operazioni su A.D.
La directory è utilizzata principalmente in **LETTURA**. Possiamo aggiungere utenti, modificare ruoli,... ma la maggior parte delle operazioni che vengono svolte sono di lettura.

Viceversa, nei database sono frequenti le operazioni di scrittura quanto quelle in lettura.
<br>

### Gruppi e Unità Organizzative
Oltre agli utenti e ai computer ci sono i **gruppi** e le **unità organizzative**.
*Ci sono dei gruppi predefiniti, altri invece si possono facilmente creare. Questi gruppi successivamente possono essere organizzati come vogliamo.* 

- **GRUPPI**: sono oggetti di Active Directory che si utilizzano per impostazioni di sicurezza, impostando policy di accesso comuni a gruppi di utenti o computer. **All'interno del gruppo gli utenti sono TUTTI UGUALI.**

	*Ad esempio: Tutti gli utenti del gruppo "marketing" hanno accesso a una determinata condivisione sul server.*

- **Unità Organizzative**: (strutturate ad albero) si impostano per esigenze amministrative e consentono, ad esempio, di delegare ad un utente la gestione, eventualmente parziale, dell'unità organizzativa. Le UO sono strutturate ad albero (**gerachia di contenitori**)
<br>

### Alberi e Foreste
*Quando nacque Active Directory, questa prevedeva un solo Domain Controller, ora ce ne possono essere più di uno.*

##### Alberi
Al dominio principale (e il suo Domain Controller) possono essere aggiunti dei sottodomini (avendo a loro volta un Domain Controller), a formare un albero.

I sottodomini ereditano lo schema del dominio "padre", che potranno successivamente modificare.

**Tra dominio principale e sottodomini si determina la "two ways implicit trust"**, per cui un utente di un qualsiasi dominio dell'albero può accedere agli altri. Così facendo l'uno si fida dell'altro per la **proprietà TRANSITIVA**.

##### Foreste
Una foresta è formata da 2 o più alberi collegati tra di loro, **un'eventuale relazione di fiducia però deve essere esplicitata** ("explicit one way trust")
<br>

### Repliche
*Il Domain Controller ha il controllo centralizzato dell'intera rete, è opportuno quindi evitare di avere un "single point of failure".*

Viene definito un **CLUSTER**, un insieme di server all'interno della stessa rete, che hanno ciascuno una propria copia di Active Directory e sono **in costante aggiornamento tra di loro,** con lo scopo di garantire:
- **Fault Tolerance**
- **Load Balancing**: man mano che le richieste arrivano, queste vengono smistate ad un server del cluster (per ridurre il carico su ciascun server)

**NB**. Un dominio anche piccolo ha sempre bisogno di avere un cluster di almeno 2 server.
<br>

### Sites
*Il dominio potrebbe essere esteso su più rete locali, in questo caso ogni sito deve avere una copia della directory.*

**I sites consentono di distribuire geograficamente le repliche del domain controller.**

Le repliche appartenenti allo stesso sito sono in cluster, hanno collegamenti veloci e possono di fatto avere esattamente la stessa versione della directory.

La strategia di replica tra i controllori in siti diversi specifica ogni quanto tempo va effettuata la sincronizzazione della directory.

- **Site link**: le linee che collegano i siti
- **Site link bridgeheads**: sono collegamenti ridondanti che consentono di evitare *single point of failure* nella sincronizzazione
<br>

### Roaming Progile
I profili utente sono una serie di personalizzazioni che solitamente vengono memorizzate in locale, alcuni esempi possono essere: *sfondo, cartella home, cookie del browser,...*

Il **roaming profile** permette che il profilo utente venga condiviso in rete e che quindi l'utente possa ritrovarlo in qualsiasi computer del dominio lui acceda.
*Per abilitare il roaming profile bisogna:*
- Creare sul server una cartella in cui verranno poi creati i profili utente (con permesso di share read+write per tutti)
- In gestione utente, scheda *profile* modificare la directory del profilo in 
	*\\\\[nomeServer]\PROFILES\%username%*
<br>

### Permessi
I permessi determinano come gli utenti possono interagire con le risorse del dominio e vengono assegnati dal proprietario della risorsa.

Nella gestione di un domino complesso, è conveniente assegnare i permessi a gruppi di utenti e NON a singloli utenti, (piuttosto creiamo un gruppo per un singolo utente).

Ci sono 2 categorie di permessi:
- I permessi di **share** (di condivisione)
- I permessi **NTFS**

*Nel caso volessimo rendere disponibile un disco di rete agli utenti, dobbiamo impostare i permessi di share di questo come NEUTRI (tutti possono fare tutto) e restringerli nel caso utilizzando i permessi NTFS*

Se a un utente si applicano 2 regole (essendo in 2 gruppi), a quest'ultimo viene applicata quella **più restrittiva**: **i permessi NEGATIVI valgono di più di quelli ASSEGNATI**.
<br>

### Group Policy Objects
I **group policy objects (GPO)** si applicano alle Unità Organizzative e possono essere utilizzati per la gestione della sicurezza.

Con questo tipo di oggetti è possibile:
- Abilitare / Disabilitare delle applicazioni
- Impostare la connessione automatica a risorse condivise
- Impostare l'esecuzione automatica di script/programmi
- ...

*ES: tramite i GPO possiamo togliere il task-manager a tutti gli utenti di un UO.*