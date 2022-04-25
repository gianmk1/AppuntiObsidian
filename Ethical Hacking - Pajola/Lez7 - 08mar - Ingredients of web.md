# Ingredienti del WEB
Solitamente noi andiamo ad exploitare il **paradigma client-server**, esistono altri tipi di paradigmi es. peer-to-peer . 

Quando parliamo di WEB abbiamo tre tipi di ingredienti base:
- IP univoco
- Porta di comunicazione
- Protocolli

Se ci fosse una comunicazione solo tramite IP, sarebbe difficile hostare più applicazioni nel dispositivo.
I protocolli vanno a definire delle regole per la comunicazione.

Solitamente accediamo ad una web app tramite browser, solitamente questi ricevono una pagina html che viene renderizzata dal browser stesso. NB. HTML non è un linguaggio di programmazione ma un **linguaggio di markup**, non ci sono operazioni logiche da eseguire ma è un linguaggio statico.

Per rendere queste web app più *appealing* si sono aggiunti dei linguaggi di programmazione che possono essere:
- **client side**, JS
- **server side**, Php, Python

Il protocollo **HTTP** permette di inviare informazioni su pagina html. Per renderlo più sicuro utilizzaimo **HTTPS**.

### I cookies

Per salvare delle informazioni delle nostre attività le web app salvano nel nostro browser dei **COOKIE**, questi possono essere dannosi nel caso un attaccante sia in grado di rubare il cookie della sessione di qualcun'altro.

Solitamente i cookie sono definiti come una serie di **campi valorizzati**.

Quando si manda una richiesta ad una web page questa risponde con dei cookie da "riempire".

### Client request
**GET**, le variabili vengono salvate nell'URL che andiamo ad inviare. Questa cosa è molto pratica ma la comunicazione è in chiaro

**POST**, ci permette di riempire questi campi nel body dell'http request

### Input validation
Quando si parla di attaccante significa che c'è qualcuno che sta mettendo un valore malevolo all'interno di un campo. Quindi non bisogna mai fidarsi degli utenti.

