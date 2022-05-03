# Injection Attacks
Le injection accadono perchè c'è un interazione tra il sistema e l'utente.
Più l'applicazione è complessa più possibili vulnerabilità verranno introdotte.

**Tutti i meccanismi di contatto tra applicazione e utente sono possibili vulnerabilità**.

L'attaccante inserisce un input non valido e il programma viene eseguito in modo anomalo.
L'**attaccante vuole far eseguire il programma in un modo per il quale non è stato pensato**.

### Code Injection
L'idea dell'attaccante è quello di inserire, all'interno di un input, uno **script nel linguaggio utilizzato dal programma**, che verrà eseguito lato server.

*Esempio: funzione **eval** di Php, perchè esistono funzioni come eval? Quando bisogna lavorare con gli input spesso si incotrano caratteri strani da "pulire".*

### CLRF, Carrige Return and Line Feed
Il browser manda delle richieste al server, per separare le richieste si utilizza questo tipo di separatori, per capire quando inizia una richiesta e quando ne finisce un'altra.

Possiamo quindi mandare una richiesta url http e con un separatore, può inserire un log falso.
In questo modo stiamo **manomettendo i log di un server**.

### Cross-Site Scripting (XSS)
**Inserire degli script malevoli all'interno di un server web.**
JS viene eseguito dal client.

Se un attaccante riesce a manomettere una pagina inserendo un codice javascript, quando il browser caricherà la pagina e troverà questo codice, lo andrà ad eseguire.

**XSS è una delle vulnerabilità più diffuse.**

### E-Mail Header Injection
Quando andiamo a inserire: nome-cognome-messaggio, **possiamo inserire a livello del messaggio degli header SMTP per**, ad esempio, **farsi inviare tutte le mail registrate al server.**

### OS Command Injection
Invece di inviare degli script **andiamo ad inviare dei comandi bash** che verranno eseguiti dal server.

*Esempio: Un'applicazione che ci ritorna il ping, se facciamo un injection possiamo eseguire altri comandi, es. http://..../ping.php?address=8.8.8.8%2dls*

### SQL Injection
Tutte le informazioni nel web vengono immagazzinate all'interno di database.
Tramite le **SQL Injection possiamo andare a modificare la query originaria** ritornando, ad esempio, tutte le password o tutti i database

Possiamo andare a inserire un injection, es. **1=1 --'**