# Android Studio

Un' **ACTIVITY è una pagina**, cioè una schermata di un'app.

Si parte dal layout, poichè il nostro layout della schermata è l'**input e output**.

L'activity è tutta scritta in XML
Il movimento e le azioni è fatto in JAVA

La **VIEW** è qualsiasi oggetto che mettiamo nel layout (es. text box , bottone , immagine , ...)

Il layout è come io metto gli oggetti nella schermata:
- constraint layout
- linear layout : in orizzontale o verticale
- table layout : organizza in tabella

Devo definire prima il **constraint layout** (lato to lato)

Ogni oggetto ha tante proprietà che vengono definite nel file XML

Nel nome, **@+** identifica che questo oggetto lo si va a prendere nelle risorse

### Esercizio CALCOLATRICE
File importanti:
- mainactivity.java
- activity_main.xml
- string.xml : qui vado a definire tutte le varibili di tipo stringa, Android da errore se vado a dichiarare direttamente la stringa all'interno dell'oggetto


Quando si definisce un layout bisogna definire i nomi degli oggetti e il loro **TIPO**

**AndroidManifest.xml** è come l'index, rappresenta la prima activity

Dobbiamo usare variabili:
- di **lavoro**, cioè quelle che utilizziamo
- **collegate agli oggetti**, quelle che prendolo l'oggetto del layout

# RIASSUNTO
### Activity
Un'**activity** è una pagina, cioè una qualsiasi schermata di un app.
Tramite l'activity l'utente immette degli input e consulta gli output ritornati.

In un app l'utente può visualizzare diverse schermate creando uno **stack di activity** in cui l'utente può muoversi.

### Service
Un **service** rappresenta un lavoro che viene svolto interamente in background senza bisogno di interazione diretta con l'utente. Una volta lanciati diventano indipendenti dall'activity.

Le activity sono scritte in **XML**, mentre le azioni che vengono richiamate sono scritte in classi **JAVA**.

### View
Con **view** (o **vista**) intendiamo un **qualsiasi elemento/oggetto che appare in un'interfaccia utente**. La sottoclasse **ViewGroup** (o **LAYOUT**) fornisce dei **contenitori invisibili** che contengono altre view.

Questo si traduce in una struttura ad albero di view.

### Layout
Con il termine layout si definiscono tutte le **ViewGroup** che **determinano il posizionamento, cioè la struttura, dei wigdet (singole view) all'interno della schermata**.

Alcuni tipi di layout sono:
- **Linear layout**, contiene un insieme di elementi che si distribuiscono **dall'alto verso il basso** o da **sinistra verso destra**
- **Table layout**, inquadra gli elementi in una tabella
- **Relative layout**, gli elementi si posizionano in relazione l'uno all'altro permettendo un layout molto **responsivo** (simile a **Constraint layout**)

#### AndroidManifest.xml
Il file **AndroidManifest.xml** raccoglie informazioni dettagliate riguardo l'applicazione come *nome del package*, *nome dell'applicazione*, *nome delle activity presenti*,...

#### activity_main.xml
Il file **activity_main.xml** rappresenta l'activity principale del programma, può essere inteso com l'**index**, **contiene tutti gli oggetti della parte grafica**.

#### MainActivity.java
Il file **MainActivity.java** contiene il programma principale dell'applicazione.
Il codice al suo interno determina il comportamento della nostra applicazione.

**NB**. Ogni attività ha un file **activity**, per la struttura e **java** per il comportamento.

<br>

### API, Application Programming Interface
Le **API** sono un insieme di definizioni e protocolli con i quali vengono realizzati e integrati software applicativi. Funge quindi da **elemento di intermediazione** tra il client e le risorse web che si vogliono richiamare.

### REST, REpresentational State Transfer
In un'applicazione rest, il client **invia una chiamata HTTP ad un URL** (o **endpoint**) specificando un **metodo**, il server esegue la funzionalità collegata all'endpoint e risponde (solitamente con dati in formato JSON)

Un API REST comporta una **comunicazione client-server STATELESS**, dove **ogni richiesta viene trattata come indipendente dalle altre**, il server non tiene memoria delle informazioni di stato.

**NB**. Il server non si serve di informazioni relative a richieste precedenti.

### Richiesta ASINCRONA
In questo caso l'applicazione **client invia una richiesta** e in seguito **continua l'esecuzione del codice**, **ignorando lo stato di avanzamento** della richiesta. Pertanto il thread che ha avviato la richiesta non viene bloccato in attesa della risposta del server.

**NB**. Durante una **richiesta SINCRONA si attende la risposta** prima di avanzare con l'esecuzione del programma.

### Extend VS Implemets in Java
- **Extends** indica che si sta craendo una **sottoclasse** della classe base che si sta estendendo
- **Implements** indica che si sta **utilizzando gli elementi di un'interfaccia Java** nella classe

**NB**. **@Override** permette di ridefinire un metodo della classe padre