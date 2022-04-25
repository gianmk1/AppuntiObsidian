# Architettura applicazione WEB
*Realizzazione applicazione web basata su backend scritto in Java, il frontend sarà realizzato tramite il framework Angular JS.*

Per applicazione web si intende un applicazione distribuita, che quindi consente l'accessibilità da remoto. Solitamente un applicazione web si basa sul paradigma client-server.

Il backend è l'applicazione che risiede nel server.

Le informazioni possono essere persistenti o volatili, ospitato sullo stesso server o su un altra infrastruttura

Il backend espone una serie di punti di accesso chiamate API con cui il frontend comunica per ritornare i dati.
A seconda delle necessità le chiamate possono essere di diverso tipo.
Le richieste del front end vengono accettate dal backend in accordo con le API esposte

**API** = Application Programm Interface , sono delle interfacce di accesso ad una applicazione, produce una serie di dati che poi vengono consumati dal frontend. Sono quindi dei **punti di accesso** per un applicazione

## Backend
Possono essere utilizzate varie tecnologie **Python**, C#, Java, NodeJs, Springboot

Il framework permette la definizione di logiche complesse. utilizzando i molti automatismi messi a disposizione. Permette la creazione di un backend funzionante in poco tempo.

L'applicazione sarà strutturata in **livelli**:
- Accesso al DB 
- Elaborazione ai dati
- Presentazioni dati -> API

In ordine:
1. Il **controller** si occuperà di esporre l' API
2. Il **service** conterrà tutte le logiche di business dell'applicazione
3. **Repository**

Spring initialiter permette di definire lo *scheletro* del progetto

**Postman** è un software che permette di fare delle chiamate HTTP, permette di realizzare delle specifiche chiamate con dei specifici metodi
<br>

### Livello Controller
- Creiamo una cartella **controller** al cui interno inseriamo una classe java

Per definire un controller utilizziamo @RestController , che verrà utilizzata da Springboot. Mediante ciò verranno esposte l'API

Il metodo è di tipo GET, la chiamata restituirà una stringa con il nome che abbiamo passato in input

Raggiungendo tramite browser l'indirizzo *http://localhost:8080/api/v1/test/gianmarco* ci ritornerà il risultato

Siamo quindi riusciti ad esporre un **endpoint**.
<br>

### Livello Service
Per fare ciò dobbiamo realizzare un altro metodo

**Dependecy injection**:
Nell'approccio standard del linguaggio ad oggetti, qualsiasi tipo di oggetto viene dichiarato come variabile e inizializzato. Nella **dependecy injection** la dichiarazione delle variabili viene **delegata al compilatore** e noi dobbiamo solo **marcare la classe come @Service**
<br>

### Livello Repository
Springboot ci permette di definire un accesso al database indipendente dalla tecnologia di quest'ultimo.

Nei database relazionali si definisce la struttura delle entità,... nei database NON relazionali invece no. Una tabella quindi può accettare 1 o 30 campi, non serve specificarli prima.

Nel nostro caso utilizzeremo dei database **in memory** senza dover quindi utilizzare dei server database

Per accesso ai dati Spring utilizza un componente chiamato **JPA (Java Persistance Api)**, che traduce le nostre richieste in una query.

Utilizzeremo un database in memory H2, che può avere una persistenza su file o in RAM.
Per fare ciò dobbiamo aggiungere delle dipendenze raccolta all'interno di https://mvnrepository.com/ e aggiungiamo le dipendenze:
- Spring boot starter data JPA
- Lombok
- H2
- FlywayDB

Nel file **application.properties** possiamo settare vari parametri utili a sping e verranno definiti tutti i settings per l'accesso ad database

##### Creazione di una struttura del database
Inseriamo la query per la creazione del database all'interno di un file rinominato *V1_1__create_database.sql* che servirà per la migrazione del DB.

Creiamo anche un file per inserire dei dati all'interno del DB
<br>
Fino ad ora abbiamo implementato l'accesso al database con **persistenza su file**.
Ora dobbiamo creare un'applicazione che permetta la gestione dei dati in DB
<br>

### Riassunto
Il flusso finale sarà

**Controller** > **Service** > **Repository** > **Database**

Il controller utilizzerà i metodi esposti di service, all'interno di quest'ultimo verrà gestita la connessione delle chiamate al DB. La repository effettuera le query sul DB, questa tramite processo inverso tornerà all'utente finale.

<br>
<br>

## Frontend
Come consumare le API che abbiamo messo a disposizione?

Anche per il frontend utilizziamo diverse tecnologie: Php, Html, JS o **Typescript sfruttando Angular**, questo framework:
1. Permette la scrittura di applicazioni modulari e scalabili
2. Creazione di un frontend funzionante in pochi minuti

L'applicazione creata sarà una **SPA, Single Page Application**, la pagina creata sarà quindi **unica** e il **contenuto sarà caricato dinamicamente**, JS ci permetterà di simulare un ambiente con più pagine

L'ambiente di sviluppo sfrutta la Angular Command Line, il funzionamento si basa su **npm** incluso in NodeJS.

Il concetto di npm è simile a quanto visto per la repository Maven: tutte le librerie possono essere scelte da una repo pubblica www.npmjs.com


Angular permette la creazione di un progetto **diviso in moduli**. Il package principale è **NgModule**, al cui interno i vari moduli sono i container per blocchi di codice dedicati ad un dominio, un flusso, ...

I **component** sono strutturati con:
- un **template HTML**
- classe **Typescript** per descrivere il comportamento
- **selettore CSS** che descrive lo stile

### Creazione progetto
Installiamo VScode e il plugin Angular Language Service

La struttura che andremo a realizzare sarà a livelli:
- Presentazione dei dati
- Elaborazione dei dati
- Accesso ai dati (più un recupero tramite le API realizzate)

Nella stessa cartella dove è contenuta la cartella del backend:
*ng new [nome progetto]*
*Would you like to add angular routing?*   -> Yes

La creazione di un nuovo progetto porta alla creazione di un **app-demo**

*ng serve -- open* , per avviare il progetto (all'interno della cartella angular)


Angular permette la creazione di n componenti perchè l'idea è quella di creare blocchi di codice che possono essere riutilizzati, quindi si struttura l'applicazione in **componenti riutilizzabili**

### Creazione componente home e engine
*ng generate component [nome componente]*

L'utente finale avrà la sensazione di navigare all'interno dell'applicazione, ma in realtà la pagina sarà sempre la stessa, **per specificare cosa caricare dinamicamente ad ogni indirizzo** utilizziamo il **modulo app-routing-module.ts**

Bisogna anche specificare i routing dei vari engine

### Consumo delle API
Per poter gestire le chiamate http la **libreria standard è HttpClientModule**, aggiungiamo la dipendenza nell'app module ( import { HttpClientModule } from '@angular/common/http'; )

Sarà quindi possibile utilizzare dei metodi per andare a consumare le API esposte dal backend.
**Definiamo le chiamate all'interno di un Service -> ng generate service service\engine**

L'utilizzo del service viene fatto tramite la **dependecy injection** (come visto nel backend)

**Observable** è un oggetto che viene inizializzato, si occupa di ricevere la risposta di una chiamata http e muore. Per salvare la risposta della chiamata bisogna andare a sottoscriverla con **subscribe**

**NB** Spring **blocca tutte le richieste all'end point che arrivano ad un dominio diverso** da quello del backend. Per risolvere ciò:
dobbiamo **disabilitare il CORS nel backend per accettare richieste provenienti da qualsiasi dominio**, questo **mette a rischio** la nostra applicazione a chiamate da altri non accettabili da altri siti.

### Modello per gestire le informazioni restituire
Creiamo un modello per engine e strutturiamo una lista in html con il suo specifico stile CSS

La definizione da zero di tutti gli stili di un componente è un processo lungo, per questo motivo si cerca di definire dei componenti prendendo gli stili provenienti da altri componenti

La possibilità di utilizzare degli stili definiti da altri avviene mediante l'utilizzo di altre librerie come **material.angular.io** o **primeng** (https://www.primefaces.org/primeng/setup)

Andiamo ad integrare nell'applicazione la libreria **primeng**

### Creiamo un form all'interno del dialog "New engine"
Creiamo un componente EngineForm e creiamo all'interno un template FormLayout

I **Reactive form** è un approccio **model driven**, cioè realizzo il form sulla base di un modello, nel nostro caso sarà dato dall'engine.

Per prima cosa mostriamo su console l'oggetto inserito nel form

### Scambio dato tra component
Lo scambio viene fatto attraverso un pattern che viene specificato attraverso delle direttive @Input e @Output

Con **@Input** potremmo portare dei dati dal child al padre
Con **@Output** potremmo portare dei dati dal padre al child

L'input si utilizza con le [] , es [disabled]
L'output si gestisce con le () , es (click)

