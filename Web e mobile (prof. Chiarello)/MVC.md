# MVC, Model View Control
L'**MVC** è un **design pattern** molto utilizzato in programmazione.

In questo modello è prevista la **suddivisione di un'applicazione in 3 livelli distinti ma interconnessi** così da separare layer e responsabilità.

### Livelli MVC
- **Livello dati**, dove è presente la gestione della connessione col DB e delle query
- **Livello logico**, elaborazione e gestione dei dati ricevuti
- **Livello output**, si occupa dell'output finale all'utente

### Schema MVC
![[inserischi schema]]

### MODEL: livello dati
Il livello dati può essere implementato creando una classe base che **gestisce la connessione con il db e le query al database** e più classi che solitamente rappresentano i modelli di dati

**Definisce i metodi per accedere e modificare i dati**

**Classe DB**:
1. Connessione al DB
2. Gestione della connessione
3. Esecuzione della query

**Metodo Select**:
- prepare() -> prepara la tabella nel DB
- execute() -> interroga la tabella preparata

### CONTROLLER: livello logico
Il livello logico gestito da una classe di tipo Controller si realizza creando dei metodi pubblici che prendono il nome di **azioni**.

In questa fase vengono ricevuti i comandi dell'utente che vengono eseguiti richiamando il model, i risultati verranno mostrati tramite lo stato VIEW. **Gestisce l'interazione tra model e view**.

Nell'implementazione PHP questi metodi e i loro parametri vengono messi in correlazione con gli URL delle richieste HTTP

1. Collegamento al model, istanziazione oggetto DB e utilizzo dei suoi metodi
2. Costruzione della stringa SQL
3. Acquisizione dei dati
4. Restituzione dei dati tramite file JSON

### VIEW: livello utente
Si deve pensare a questo livello in termini di **output presentato o inviato dall'utente al server**. Una view NON è sempre una pagina HTML o PHP, ma può essere anche un PDF, un'immagine, un JSON,...

Il pattern MVC viene utilizzato anche per **aumentare il livello di sicurezza di un applicazione**.