# Servlet
La cartella dove ci sono le pagine di Tomcat è ./xampp/tomcat/webapps

Servlets serve per gestire la parte di backend

In Php il codice è in chiaro nel server, le servlets vengono messi in .class (scritti in java), quindi anche se accedo il server non vedo il codice

Es. Una banca non usa mai Php

### Java
Prima della programmazione ad oggetti c'era quello procedurale (es. c): sequenza di istruzioni con all'interno delle funzioni.
Il linguaggio ad oggetti, ha appunto degli oggetti con degli attributi e dei metodi. 
Ci sono delle classi generali e delle sottoclassi che ereditano dalle precedenti.
NB. classe = oggetti

![[Vedi file esempio di tomcat (examples/servlets/helloword.html)]]

ANALISI DELLA PAGINA DI ESEMPIO:

con import: importo le librerie di tutte le classi che parlano questo argomento

`import java.io.*;`
`import javax.servlet.*;`
`import javax.servlet.http.*;`

`public class HelloWorld`: la classe si deve chiamare con lo stesso nome della servlet
`extend HttpServlet`: questa classe deve ereditare tutto ciò che è dentro HttpServlets

NB. Ereditarietà e Polimorfismo (se ho una cosa di nome HelloWorld, la posso sovrascrivere)


Una classe è suddivisa in attributi (propietà) e metodi (funzioni, è l'oggetto che ha un metodo di comportamento, mentre la funzione è assestante) 

Per spedire abbiamo 2 metodi GET e POST

GET ha bisogno di 2 oggetti `HttpServletRequest request`  e `HttpServletResponse response`, request e response sono 2 variabili

da *throws* fino alla fine dell'esempio: serve per la gestione degli errori, di solito è abbinato ad un *catch*

NB. errori in java si chiamano ECCEZIONI, che possono essere trattate

Il metodo di tipo **doGet** è di tipo VOID, quindi non restitusce nulla, spedisco e basta
Con il metodo **doPOST** invece spedisco e ricevo


=> L'output di un linguaggio lato server è una pagina html
`response.setContentType("text/html")`

Definisco oggetto di tipo `PrintWriter`  perchè l'oggetto in ouput metterò la risposta

`out.println`: ora posso cominciare a scrivere la parte in html

![[vedi slide Servlet.pdf]]

Mentre in Php il browser accede direttamente alle pagine scritte Php, con le Servlets invece si accede ad un container con le Servlets in .class

-- no slide 2 --

Web Application:
Le risorsa server-side includono:
- Classi server-side
- Java Server pages
- Risorse statiche
- Applet, Javascript

### Accesso di una Web Application:
![[schema slide 5]]

### Servlet
Una Servlet è una classe java che fornisce una risposta ad una richiesta HTTP.
In termini pratici sono classi che derivano dalla classe HttpServer (HttpServer implementa vari metodi che possiamo definire)

##### doGet()

### Gerarchia delle Servlet
Le servlet sono classi Jaava che elaborano richieste seguendo un protocollo condiviso

Gli oggetti di tipo request rispecchiano la chiamata, sono caratterizzati da varie informazioni: chi ha effettuato la request, quali parametri sono stati passati nella request, quali header sono stati passati

Gli oggetti di tipo response rappresentano le informazioni restitutite al client (dati in forma testuale,o binari, Http header, cookie)

### Ciclo di vita della Servlet
![[vedi schema]]

-- no multithreading --

#### Metodi per il controllo del ciclo di vita
- init(): viene chiamato una sola volta al caricamento della servlet
- service(): viene chiamato ad ogni HTTP request, chiama doGet o doPost a seconda del tipo di http request ricevuta
- destroy(): viene chiamato una sola volta quando la servlet deve essere disattivata, tipicamente serve per rilasciare le risorse acquisite

#### L'oggetto response
La risposta:
1. Contiene i dati restituiti dalla servlet al client:
	- p
	- c
2. Ha come tipo l'interfaccia HttpResponse che espone metodi per:
	- c
	- f

### Gestione dello status code
Esempi di status code:
- 200 OK
- 404 Page not found


### Eclipse
1. Collegare il server web all'IDE
2. Realizzare la Servlet
3. Testarla sull'IDE
4. Spostarla in un altro server web


Mettiamo il riferimento al server su eclipse: apache tomcat 8.5

Quando creiamo un file dobbiamo spuntare su "generate web.xml deploy..."
E aggiungere il progetto creato al server

Creiamo ora la servlet, selezionando i metodi che ci servono es. init, doGet,...

A questo punto avviare il server

Init viene eseguito una sola volta quando eseguito il .class

Per esportare progetto in un altro tomcat (con stessa versione, e stessa versione di java) esportare in `WAR file` con lo stesso nome del progetto

Lo sposto in `webapps` di tomcat, dopo aver avviato tomcat questo scompatterà da solo l'archivio war

Per attivare