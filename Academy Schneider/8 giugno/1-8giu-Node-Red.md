# Node-RED
Si tratta di un tool grafico per connettere l'Internet of Things.

**Industrial Internet of Things** è un evoluzione dell'*internet delle cose* che riguarda i **processi industriali** e mira a rendere questi ultimi più efficaci e sicuri.

*Esempio: Un interruttore prima si occupava solo di aprire e chiudere un circuito elettrico, ora un interruttore smart è in grado anche di fornire, per esempio, il numero di manovre effettuate, la temp a cui lavora....*

La raccolta è l'analisi di tutti questi dati ci permette di eseguire una **manutenzione predittiva**.

### Struttura industriale
Le applicazioni industriali sono organizzate in 3 livelli (a partire dal basso):
1. Dispositivi connessi che lavorano sulla macchina (**connected products**)
2. PLC, controllori, PC industriali (**control layer**)
3. Elaborazione e analisi dei dati (**analytics & service**)

**NB**. **IIoT Edge Box** = pc industriale di Schneider
**NB2**. Un **PLC** è un **Controllore Logico Programmabile**, si occupa delle automazione della macchine, è in grado di attuare azioni sul campo in modo molto rapido, ha dei **BUS** dedicati alla comunicazione

### NODE.js
Node-RED è basato sul framework Node.js, questa piattaforma è basata sull **JavaScript V8 Engine**.

**NB**. **npm** è il package manager di Node.js

### Node Red
Nasce con l'idea di gestire il mondo dell'IoT tramite il paradigma dei **flussi di dati**.
Può essere visto come un **ponte** tra il mondo OT e IT.

**OT**: insieme di hardware e software che attua il monitoraggio e il controllo di dispositivi fisici e processi

I flussi creati in Node RED sono memorizzati utilizzando JSON, per poi essere salvati, esportati, analizzati,...

**Nei flussi viaggiano messaggi trasmessi in formato JSON**, noi li componiamo tramite una GUI, ma questi verranno poi convertiti in JSON.
Ciascun messaggio, in ciascun nodo cui passa, può essere modificato, manipolato,...

##### Messaggi Node Red
- **Payload**: il dato che viene trasportato dal messaggio
- **Topic**: nome della variabile che rappresenta quel dato
- **_msgid**: stringa univoca che identifica ogni singolo nodo

**Possiamo simulare l'arrivo** di un dato tramite un nodo di nome **inject** che si collegera ad uno di tipo **debug**.

<br>

Una volta realizzato il flusso di nodi, possiamo mandarlo in esecuzione tramite il comando **deploy**, che trasforma i flussi grafici realizzati nell'interfaccia web in veri e propri programmi.

##### Nodi speciali
Questi nodi sono messi a disposizione da Node Red per realizzare delle dashboard, in modo da poter visualizzare i dati raccolti all'interno di un'interfaccia web.

**NB**. La finalità di Node Red non è quella comunque di realizzare queste dashboard.

##### Nodo SEModbusRead
Si tratta di un nodo proprietario Schneider Electric e serve per controllare un PLC (collegato tramite un cavo ethernet).

**NB**. L'indirizzo del campo server sarà quello del PLC con cui vogliamo comunicare tramite il protocollo Modbus.

Esiste anche la controparte **SEModbusWrite** per poter **"scrivere" sul PLC**

##### Nodo Function
Tramite un codice Javascript si prende il contenuto del payload del messaggio inviato e lo si elabora tramite il codice.

<br>

All'interno della sottocartella **node_modules** in **.node-red** sono presenti tutti i moduli installati nella nostra macchina.

