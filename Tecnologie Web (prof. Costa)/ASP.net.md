# ASP.net

È una tecnologia server side che risiede su server windows.

Noi saremo fisicamente sulla nostra macchina, ma la macchina virtuale winServer è vista come qualcosa di remoto, per comunicare con questa dobbiamo inserirla nella nostra rete remota.

Essendo una tecnologia server side, i file, devono rimanere nel server web.

Per FTP:
host: xxx.xxx.xxx.xxx
utente : utente
psw: Vicolocort0

Ci connetteremo alla radice di una directory utilizzata dal server web di windows2012

Noi non stiamo lavorando direttamente sul server, ma in remoto e poi attraverso filezilla posizioniamo i nostri file sul server. Per il motore ASP.net noi siamo degli utenti remoti

web.config (file xml) server perchè così eventuali errori possano essere visti anche per chi sta lavorando in remoto (dal proprio browser). Finito di sviluppare, dobbiamo togliere questo file, altrimenti qualsiasi utente potrebbe ricevere informazioni sensibili dal server

### Cos'è ASP.net?

ASP e ASP.net sono la stessa cosa? NO, sono due linguaggi che hanno la stessa filosofia ma sono due tecnologie distinte.

.net è la piattaforma lanciata da microsoft che server per progettare ed eseguire applicazioni INDIPENDENTI dal linguaggio, Microsoft voleva realizzare una piattaforma per cui, qualsiasi linguaggio in programmassi, diventava la stessa cosa.
*Un C, viene prodotto qualcosa, viene preso dal CLR e io vedo cosa fa quella cosa.*

Poi è nato C#:
È un linguaggio ad oggetti di microsoft, che somiglia molto a Java. È un linguaggio complesso ma potente, ben tipizzato.

### Visual Basic

Noi facciamo asp.net perchè vogliamo sfruttare la piattaforma .net e faremo degli script in Visual Basic

Visual Basic rispetto C# e Java non viene definito paradigma agli oggetti ma come **PARADIGMA agli EVENTI**: io ho una serie di oggetti, quasi sempre un blocco di codice viene eseguito in automatico quando si verifica un evento

*es. ho un form, quando clicco sul pulsante succede qualcosa, a quel pulsante viene associato qualcosa che avviene quando si verifica l'evento*

### Primo esercizio
ASP.net è html su cui vengono fatti, dal browser, eseguire degli script

**Il motore asp.net andrà vedere sulla pagina html, quali sono le cose che deve esguire lui e quali deve spedire al browser dell host.**

Un attributo fondamentale è runat="service"

.aspx è l'estensione tipica di asp.net

Per dire che deve essere asp.net (cioè l'**interprete CLR**) ad eseguire io devo mettere **runat="server"**

Sub Page_load() : questa procedura andrà a caricarsi al caricamento della pagina

Visual basic non ha le parentesi graffe, ci sono delle parola di inizio e fine

innerHTML su visualbasic funziona come su javascript, all'interno di innerHTML io posso quindi metterci dei tag html che vengono effettivamente interpretati

In VisualBasic i commenti sono solo monoriga e si fanno con un apice


ASP.net utilizza il concetto per cui: una pagina invia i dati a se stessa in automatico, per poter fare questo il form deve essere accedibile da asp.net, serve quindi runat="server"

In asp.net nei moduli del form, o utilizzo dei moduli apposta di asp.net o utilizzo quelli nativi di html

NB. Scrivendo onClick solamente l'evento avviene il locale, bisogna scrivere quindi onServerClick per far si che il server esegua la PROCEDURA all'interno

La procedura sarà nel blocco ```<script>``` .
	
	
In asp.net per salvare lo stato della pagina utilizziamo **viewstate**, e possiamo quindi sapere se la pagina è la prima volta che la pagina viene caricata o la seconda

In asp.net io posso andare a salvare delle informazioni della singola pagina e sfruttarle al ricaricamento.

In php avevamo la funzione isset(), in **asp.net abbiamo una variabile booleana automatica (view state), che se ha un valore è la prima volta che viene caricata alla pagina, altrimenti è la seconda o più**.

In asp.net l'attributo name non funziona (si utilizza **id**), quindi non possiamo usare i radio button nativi di html.

in asp.net l'**operatore di concatenazione** è **&**

<br>

# 02feb

## Viewstate
Il viewstate di una pagina asp.net è una sessione, in piccolo, non riguarda la finestra del browser, ma la pagina stessa. Tra un caricamento e l'altro è possibile salvare delle informazioni, questo fa parte del viewstate della pagina e attraverso una variabile booleana posso vedere se la pagina è la prima volta che viene caricata o meno.

Ogni pagina ha un suo viewstate.

*esercizio "statoPagina.aspx"*
La funzione Esegui viene eseguita quando clicco, diversamente da php, quindi non c'è necessità di viewstate

ASP.net sfrutta il **PostBack**, cioè la pagina elabora se stessa, la pagina manda i dati a se stessa : È false quando è la prima volta che viene caricata, True quando la pagina è già stata caricata

ViewState funziona sia come una funzione per impostare che per prelevare

NB. ASP.net NON è debolmente tipizzato come javascript e php.


Il costrutto **If** di visual basic deve terminare con **End If**

**NB**. I controlli ASP.net sono sempre binari, vanno sempre chiusi

#### Radio button

**VERSIONE 1 **

``` <asp:RadioButton>...</asp:RadioButton> ```

Dove per accomunare i vari bottoni mettiamo **groupName="..."** 

NB. Per accorciare la chiusura di un tag in asp.net possiamo mettere **/>** invece di chiudere l'intero tag con **></asp:RadioButton>**

**Versione 2**, **Lista di Radio button**

<asp:RadioButtonList> è fatto da **un controllo che ne ingloba delle altre**, come il tag ```<li>```

Seguito poi da una serie di asp:ListItem

#### Esericizio IMC in asp.net 
Non possiamo utilizzare il controllo radio-button dell html, dobbiamo utilizzare quelli di asp.net

# 09feb

## Asp.net : Postback

È possibile che **asp.net, invia eccezionale,** faccia come php di default, cioè **invii i dati ad un altra pagina anzichè a se stessa**? SI, è possibile, ma non sempre conveniente.

## Controlli di validazione
In PHP e JavaScript doveva essere compilato correttamente: casella mail -> mail. 

ASP.NET mette a disposizione una serie di controlli per validare o permettere di continuare la compilazione del form. Sono io a decidere, se l'utente, può procedere o meno.

**RequiredFieldValidator**: controllo asp.net che richiede che il campo sia compilato

Controllo **RequiredFieldValidator** fa da **validatore** per un campo che **DEVE** essere richiesto. La proprietà **ControlToValidate**, dove specifico il controllo (componenti) che deve essere controllato.

Controllo **CompareValidator** prende il valore inserito e lo compara con il valore che decidiamo noi

**ValueToCompare** : valore da controllare

**GreaterThanEgual** : maggiore o uguale


Prima dell'HTML5 ASP metteva a disposizione un controllo per andare a **sindacare** il contenuto, nel caso della **mail**, io so che è fatta in un certo modo, una **ESPRESSIONE REGOLARE**:

[] : rappresenta un carattere, quello che scrivo al suo interno sono i caratteri che possono essere inseriti e per quante volte possono essere ripetuti

In questo caso si utilizza il controllo **RegularExpressionValidator**

Per vedere tutti i messaggi di errore utilizziamo un'altro controllo: **ValidationSummary**, con attributi:

- **ShowMessageBox**: fa si che tutti gli error message di tutti i precedenti controlli siano visualizzati in una finestra di dialogo.
- **ShowSummary**: se ="false" non mostra tutti i messaggi di errore come testo nella pagina

NB. Se non metto nessuna delle 2 proprietà è come se io mettessi ShowSummary="true"

NB. Esiste un'alternativa al DropDownList che si chiama ListBox

## Data Binding
Data Binding = **associazione tra controlli**

In ASP.net oltre ad essere, come in php, **contenuto di un database**, permette di fare l'associazione tra controlli anche senza un database. 

*Scelgo una voce di una casella select e in una casella di testo mi viene immediatamente mostrata la voce selezionata. Questo NON viene fatto tramite database ma tramite **Espressioni**. L'aggiornamento avverrà appena asp.net vede un aggiornamento.*

In asp.net si definisce una **espressione** e come deve prendere i vari controlli.


Text="<%# mess %>" 			: Dentro Text mettiamo un'espressione di DataBinding. Il contenuto di questa etichetta sarà l'espressione che deriva dalla variabile mess


L'**interpretazione** è l'invocazione di un metodo, che può essere **universale** o **associato ad un singolo controllo**.

**onSelectedIndexChanged** è un evento per cui, quando cambia l'indice selezionato, abbia la procedura Cambia

Con **AutoPostBack** = True vuol dire che ogni cosa che succede quando c'è un evento (onSelectedIndexChanged) avviene un caricamento della pagina


#### Con database
Asp.net si comporta diversamente rispetto a Php. 

## Asp.net a database ASSES
L'accesso a database di tipo ACCESS da parte di asp.net avviene:
1. In modalità **connessa**, simile a quello delle altre tecnologie server-side. Attraverso un driver si apre una connessione al database, attraverso questa connessione vengono trovate tutte le risorse inerenti al db. Quando ho bisogno di qualcosa do la mia query ad un oggetto e ottengo sempre una *query in forma compressa*, ho bisogno quindi di **altre funzioni** per accedere al vero e proprio risultato della query.
2. Modalità **disconnessa**, presa da visualbasic. Io apro una connessione con il db, questo viene "succhiato" e messo nella memoria del server, la connessione effettiva col db viene interrotta e le comunicazioni avvengono esclusivamente tra **server e browser**. **NON c'è più un'accesso diretto al DB**. Le prestazioni sono quindi migliori. Ad un certo punto dovrò aggiornare il db, quindi si aprirà nuovamente la connessione per salvare i dati.


Alcune tecnologie:
- ODBC , utilizzato anche in Php
- OLE DB , non è solo database ma comprende anche altre risorse, mette a disposizione oggetti e metodi per connetersi alla risorsa e prendere dati.
- ADO.NET , sono i servizi che la piattaforma .NET mette a disposizione. Mette a disposizione vari oggetti, tra cui quelli per lavorare in modo disconesso
- JDBC , l'interfaccia standard utilizzata da JAVA.

Tutte queste sono tecnologie di accesso al database (alcune locali e altre no)

C'è un database ACCESS dal 2007 in poi e uno precedente al 2007.

OleDbCommand è l'oggetto che riceve una query, OleDbCommand è "l'ordine di esecuzione di una query", ma non da lui il risultato finito della query, ma devo utilizzare un metodo (**.ExecuteReader**)

In generale la query è formata da colonne e righe, come in Php utilizzo quindi un ciclo while (while - End while), analogamente a Php ho il metodo **read** che legge una singola riga dei dati e ritorna un booleano

dati.read() è la singola riga della tabella

dati : è la tabella
.item("NomeN") : identifica la colonna della tabella

Leggiamo la specifica riga tramite il metodo **read()**