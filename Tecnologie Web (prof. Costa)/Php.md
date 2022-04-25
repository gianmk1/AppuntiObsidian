Xampp è un server web in locale

In htdocs rinominare index.php


PHp è una tecnologia server side: è il server web che elabora i contenuti di questa.
2 possibilità:
- un file html con riferimento a un file php

- Il codice php è dentro il codice html

Una pagina salvata in php avrà una struttura in html con delle parti in php

Php "puro" ormai non viene più utilizzato, si preferiscono utilizzare dei framework

https://www.html.it/guide/guida-php-di-base/

È anche possibile scrivere html all'interno dei file php

- lezione 7

commenti in php sono quelli di js o con #	

Il `;` è un terminatore di istruzioni, è obbligatorio


- lezione 8

Riferimento a file su xampp

2 attributi:
- action: specifica quale file è deputato a elaborare i dati spediti
- method:

**Submit** fa partire con il metodo (in questo caso get) i dati raccolti 

Con il metodo get le informazioni che invio le visualizzo sull url.
Il metodo GET è quindi poco sicuro e non posso mandare stringhe troppo lunghe, il numero di caratteri è limitati


### Concetto di array
1. Array posizionale: gli elementi vengono individuati in base alla posizione es. `dati[1]`
2. Array associativi: invece di indicare una posizione, indico una stringa che specifica una stringa es. `dati['peso']`

Php fa molto uso di array associativi $_GET $_POST

Se ho inviato dei dati con il metodo GET, automaticamente Php mi creerà un array $_GET contenente tutti i valori inviati col form

es. $_GET['peso']

$_GET['peso'] : in Php questo è sia il riferimento che il contenuto , quindi qui prendiamo già il CONTENUTO di peso

### Variabili in PHP
In php non serve dichiarare una variabile basta scrivere es. $nome_variabile

Operatore logico combina più operandi booleani per far tornare di nuovo un valore booleano
NB. and : ritorna vero se entrambi sono veri
	
	
Anche in Php ci sono i caratteri di escape

Usiamo il `.` come operatore di **concatenazione**

##### Array
In php ci sono sia arrai posizionali che **associativi**, vedi sul documento di javascript/html/css la differenza

Negli array associativi l'elemento è identificato da un nome

Si richiama un elemento con `c = dati[nome_cella]`

Php ha molti array associativi, i più famosi sono:
- **$_GET**
- **$_POST**

get e post sono le 2 modalità possibile per inviare i dati ad un server
Quando utilizziamo uno dei 2 metodi php ci mette a disposizione il relativo array

Il nome dei moduli sarà la chiave per accedere al contenuto, 
**In PHP il nome coincide al suo contenuto**


--- 
### 12 gennaio

PHP può anche essere invocato da un html puro

Ora utilizziamo php per invocare il database

Se voglio accedere al database sql devo conoscere: nome database, credenziali dell'utente che vuole accedere

##### PHP nella sua evoluzione ad un certo punto si è trasformato **da paradigma imperativo ad oggetti**.


#### Guida su html.it
https://www.html.it/guide/guida-php-e-mysql-pratica/

*Vedi lezione 1*

Come faccio a collegarmi al database?
1. deprecato
2. sostituzione del deprecato (quella che useremo noi)
3. quello che sta prendendo piede

2. **MySQLi**: che può essere **imperativa** o ad **oggetti**. 
3. Questa mi preclude una delle due sopra, poichè utilizziamo **PDO**, completamente orientata agli oggetti. PDO fornisce un livello di astrazione per l'interazione con le basei di dati.

*Vedi lezione 2*

### Connessione imperativa
*Facciamo un esempio sia in forma procedurale che ad oggetti con MySQLi*


*Forma ad oggetti:*
```php
$mysqli = new mysqli('localhost', 'username', 'password', 'nome_database');
		if ($mysqli->connect_error) {
    		die('Errore di connessione (' . $mysqli->connect_errno . ') '
            . $mysqli->connect_error);
		} else {
			echo 'Connesso. ' . $mysqli->host_info . "\n";
		}
```

Inizializzo una variablie, per fornire una connessione devo dare diversi parametri: 'localhost' , 'password' 'nome_database' , ...

In php c'è l'operatore freccia : vai a prendermi la proprietà connect_error della variabile mysqli

Se non c'è connessione: in connect_error viene descritto l'errore

**die** : fa "finire tutto"

**connect_errno** : è il codice dell'errore

**NB**. usare una variabile con lo stesso nome del metodo/istruzione/... È ALTAMENTE SCONSIGLIATO

**host_info** : riporta alcuni parametri del tipo di connessione

**Essenziale per connessione al database:**
1. **host** : uso localhost nel caso il database sia sullo stesso server dove si trova php
2. nome utente
3. password
4. nome_database

*lezione 3*

In php istruzione viene chiamata **query** ...

*lezione 5, inserimento e lettura dei record*

*sulla cartella htdocs > esphp, troviamo i file della lezione*

Per procedimento seguire le istruzioni sul file

**Il risultato dell'interrogazione** NON è pronto ad essere visualizzato, bisogna elaborarlo prima

Una query può ritornare:
- un risultato solo (query scalare)
- una tabella (query vettoriale)
	- una delle possibili tabelle risultanti è composta da una sola colonna e una sola riga
	- una tabella composta da solo una riga e molte colonne

--> Dovrò fare cosè diverse in base a quante righe mi ritornano (tante o poche).

**Utilizzeremo i CICLI**

error() -> questo è un METODO

Ciclo whire = a priori non so quante volte verrà eseguito il ciclo, lo utilizziamo per una query vettoriale

mysqli_fetch_array() : arrivato alla fine inizializza false


**Predispozione della query** = metterla da qualche parte

**NB**. Per una query scalare, possiamo comunque utilizzare un mysqli_fetch_array 

### Connessione tramite oggetti

Sulla variabile invoco **metodi e proprietà**

**NB**. Il metodo fetch_row ritorna un **array posizionale**


# 19 gennaio
mysqli_query : Il valore di ritorno della query è una tabella ma in una forma NON immediatamente sfruttabile (es. pacco dell ikea che devo montare)

Uso il ciclo **while** quando so che la query può restituirmi più di una riga.
(Se la query è scalare non lo utilizzo)

In **mysql_query** se il secondo parametro è una select ritorna il contenuto della query, altrimenti funziona da booleano (nel caso si usi un select)

*Vedi commenti / appunti su file di esempio o info_es.txt*

PHP_SELF : modo che php vuole per fare riferimento a se stesso

--> Per ridurre i caricamenti nella pagina, cioè le richieste in stampaCitta.php possiamo utilizzare **Ajax**

# 21 gennaio
*vedi file stampaCitta.php*

Spesso c'è la necessità di selezionare più voci in diversi select ma allo stesso tempo ricordare quanto selezionato precedentemente

Per risolvere ciò ci sono 2 modi:
1. Le sessioni
2. I cookies

## I cookie
*vedi memoCookies.php e mostraCookie.php*
Da un paio di anni la commissione europea per la sicurezza della privacy
ES cookie. Se chi compra è un soggetto di periferia probabilmente dovrà spendere di più di un altra persona in una città più tranquilla

I cookie però possono agevolare in molte situazioni

Il cookie solitamente lo si imposta a INIZIO pagina, al di FUORI dell'html

cookie(nome , valore , durata (0 = finchè rimane aperta la finestra))

Un cookie è una stringa di testo memorizzata sul computer dell'utente che permette di mantenere informazioni ottenute nelle precedenti connessioni http.
Il protocollo Http e Https sono protocolli "SENZA STATO", non è in grado di sapere se è la prima, seconda o n-volte che apriamo questa pagina
Il cookie non è pericoloso per la sicurezza, è però assai pericoloso per la privacy, può essere utilizzato per reperire informazioni su chi sono io.

## Sessione
*vedi sessioneUno.php*

La **SESSIONE** è uno stato che si mantiene da quando un pagina apre a quando si chiude la finestra del browser.
Viene definito anche come l'attività svolta dalla prima volta in cui si accede a una pagina dell'applicazione, fino a quandosi chiude il browser (comprende tutte le pagine aperte nella STESSA FINESTRA del broswer)

A differenza dei cookie, la sessione viene memorizzata sul server web NON sul browser.
Per funzionare crea un SOLO cookie a cui non si accede direttamente (è solo FUNZIONALE)

Per aprire (o fatta partire) una sessione: ci sarà sempre un blocco php a inizio pagina (fuori dall'html).
Ogni volta che la pagina ha bisogno di utilizzare la sessione dovrà avere la stringa

```
<?php session_start(); ?>
```

NB. Una pagina fa partire la sessione (aprire) UNA sola volta.

Ogni sessione è identificata da un ID_SESSION, che può essere visualizzato con la funzione session_id()

# 26 gennaio
Tramite le sessioni è possibile dichiarare delle **VARIABILI di SESSIONE**.

**session_id** è una stringe identificativa della sessione (che deve essere UNIVOCA)