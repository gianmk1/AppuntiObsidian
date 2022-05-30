## Webapp in Python
Per fare ciò utilizzeremo principalmente **FLASK**, **REQUEST** e **SQLAlchemy**.

Un **ORM** è una libreria che permette di trattare le classi di un database come degli oggetti, così è possibile utilizzare un DB in Python senza dover passare per SQL.

**NB**. SQLlite fa in modo che un database diventi un file

Utilizzando un ORM definiamo un host e psw del DB su cui vogliamo lavorare, se l'azienda decide di spostare i database su un'altra piattaforma, grazie agli ORM è necessario solamente **cambiare host e password**, **senza dover tradurre il linguaggio SQL**.

### Richiesta HTTP
La comunicazione HTTP avviene da parte di un client verso un server.
Le richieste HTTP sono compose da:
- **header**
- **body**

All'interno dell'header è specificato il **metodo con cui viene fatta la richiesta** (es. GET, PUT, POST), l'**url**, **status**.

Anche la risposta HTTP ha al suo interno vari parametri tra cui il **status di risposta** (es. 200, 404, ...)

### Websocket VS Richista STANDARD
Con i websocket la connessione viene mantenuta aperta, quindi anche il server può inviare al client

Mentre nella richiesta standard il server può solo rispondere ad una richiesta inviata dal client

### UML
Normalmente quando si comincia a scrivere un'applicazione da 0 è consigliabile definire un modello di ciò che vogliamo realizzare.

Esiste l'**UML (unify modeling language)** che fa uso di diagrammi come **Class diagram**, ... per strutturare l'applicazione

L'UML è una formalizzazione dei classici schemi che faremmo noi su come è strutturata l'applicazione

**NB**. **Casi d'uso**: esempi di come l'utente può interagire con un'applicazione

### Architettura applicazione
1. Amministratore registra un dispositivo
2. Comincia un loop in cui il dispositivo si connette via wifi e gli viene assegnato un IP
3. Sensore chiede al backend quali parametri di configurazione deve utilizzare per le registrazioni
4. Sensore fa la misura
5. Sensore spedisce i risultati al server con un metodo POST
6. Il backend fa delle elaborazioni
7. Scrive il risultato della misura nel DB
8. Il loop ricomincia

### ERD
Associata all'applicazione dobbiamo avere quindi anche un DB che è in grado di salvare le informazioni ritornate dai sensori

La misura deve essere associata poi alle impostazioni con cui è stata fatta, queste le troviamo in un'altra tabella

**NB**. Come **primary key** utilizzeremo il **MAC address**
