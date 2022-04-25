# HTML
Html5 è l'ultimo standard html, comporta una migliore integrazione con CSS, Javascript e HTML.

Un documento Html è sempre fatto *ad albero* composto da tag interni annidati.
- `<html>` è il tag principale
- `<!DOCTYPE html>` messo come alla prima riga dice al browser di interpretare il linguaggio con Html5
- `<meta charset="utf-8">` per dire al browser di interprentare correttamente i caratteri accentati

La rappresentazione del documento rappresente quindi una struttura **gerarchica** chiamata **DOM tree**.

**NB**. I *fratelli* in html sono sullo stesso livello e hanno lo stesso genitore
<br>

## Head e Body
Nell' `<head>` il codice inserito all'interno non viene visualizzato direttamente dal browser, fornisce informazioni aggiuntive di controllo e servizio per il browser

Nel `<body>` contiene tutto il codice che dovrà essere visualizzato sulla pagina. 

*Struttura base:*
```html
<html>
	<head>
		<title>Titolo della pagina</title>
	</head>
	<body>
	
	
	</body>
</html>
```

### Diversi tipi di tag html:
- **Binari**: necessitano dell'apertura e della chiusura (es. head, body)
- **Unari**: si aprono solamente, non hanno un tag di chiusura
<br>
- di **blocco**: creano una rottura con il tag precedente e il successivo, *mandano a capo* (es. p, ul)
- in **linea**: finchè c'è posto (nella pagina) si affiancano al precedente altrimenti vanno a capo. Possono essere integrati nel testo (es. br)

#### Alcuni tag html:
- `<br>` per andare a capo
- `<p>` crea un paragrafo e lascia un'interlinea tra il tag precendete e il succesivo
- `<h*>` per creare i sottotitoli, dall'1 al 6 corrispondono a grandezze diverse
- `<div>` per creare delle sezioni all'interno di una pagina al fine di separare le diverse aree

## I tag semantici:
Introdotti in Html5, servono per rendere più chiaro allo sviluppatore o al browser il codice.

![[tag_semantici.png]]

- `<header>` per l'intestazione della pagina
- `<nav>` rappresenta una sezione di una pagina che contiene i link
- `<section>`sezione di pagina che contiene tanti `<article>`, divide la pagina in varie parti
- `<article>`può identificare un post, un articolo
- `<hgroup>` per raggruppare i sottotitoli
- `<footer>`contiene le informazioni a piè di pagina come dati di copyright, dati di chi ha scritto i contenuti,...

**NB**. Potrebbero essere sostituiti con dei tag `<div>` con dei corrispettivi id
<br>
## Gli elenchi
- `<ul>` per creare una lista *non ordinata*
- `<ol>` per creare una lista *ordinata*

Ogni elemento della lista deve essere specificato utilizzando il tag `<li>`
<br>

## Le immagini
Posso inserire un immagine in **locale** dichiarando il suo *percorso relativo* o tramite **link esterno**. Per fare ciò si usa il tag `<img>` con alcuni attributi:
- **src**: è l'indirizzo del file che vogliamo mostrare
- **alt**: è il testo che appare se il client non carica l'immagine
- **title**: è il testo che appare se passo il cursore sopra l'immagine

```html
<img src="images/montagna.png" title="Il K2" alt="foto del K2">
```

<br>Le immagini consentite dal linguaggio html sono di tipo:
- **JPEG**: tanti colori ma c'è un'importante perdita di qualità dovuta alla compressione del file
- **PNG**: tanti colori come jpeg ma senza la compressione di quest'ultimo
- **GIF**: solamente 256 colori
<br>

## Collegamenti ipertestuali
Un collegamento ipertestuale serve per raggiungere altri documenti esterni o altre parti dello stesso documento (interni):
1. **Esterni**: lasciano la pagina, consente di navigare all'interno di un'altra pagina dello stesso sito o meno
2. **Interni**: non lasciano la pagina, la visualizzazione si sposta in un altro punto della pagina

Si utilizza il tag `<a>` per creare l'**ancora** (che può essere un teso o anche un immagine) e il tag `href` per creare il link. <br>
**Es1**. Collegamento *esterno*:
```html
<a href="https://www.facebook.com/">Facebook</a>
```
La stringa *"Facebook"* è l'**ancora** cliccabile, rimanda al medesimo sito.<br>
**Es2**. Collegamento *interno*:
```html
<a name="paesaggio">foto_di_lago</a>
<!-- Creo l'etichetta di nome paesaggio a cui rimanderà il link -->
```

```html
<a href="#paesaggio">Qui per vedere un lago</a>
<!-- Richiamo l'etichetta invisibile utilizzano #nome_etichetta -->
```
Il testo *"Qui sotto per vedere un lago"* è l'**ancora** cliccabile, rimanda all'etichetta "paesaggio".
<br>

## Le tabelle
Per le tabelle utilizziamo il tag binario e di blocco `<table>`:
- `<tr>` contiene una riga della tabella
- `<td>` definisce una cella standard, ogni `<tr>` avrà tanti `<td>` quanti il numero di colonne

**NB**. Il tag `<table>` posizione solamente gli elementi, per modificare lo stile della tabella utilizziamo un foglio di stile

*Codice:*

```html
<table>
	<tr>
		<td>Cella 1.1</td>
		<td>Cella 1.2</td>
		<td>Cella 1.3</td>
	</tr>
	<tr>
		<td>Cella 2.1</td>
		<td>Cella 2.2</td>
		<td>Cella 2.3</td>
	</tr>
</table>
```
*Risultato:*
<table>
	<tr>
		<td>Cella 1.1</td>
		<td>Cella 1.2</td>
		<td>Cella 1.3</td>
	</tr>
	<tr>
		<td>Cella 2.1</td>
		<td>Cella 2.2</td>
		<td>Cella 2.3</td>
	</tr>
</table>
<br>

## Il tag Input
Si utilizza soprattutto nei campi dei form per recuperare un valore; per specificare un determinato tipo di campo è sufficiente indicare il tipo di input.

*Sintassi:*
```html
<!-- Crea un campo di testo -->
<input type="text" name="casella">
<!-- Crea un bottone -->
<input type="button" name="bottone_1">
```

Si possono poi definire degli attributi per indicare ad esempio **nome**, **valore**,... utilizzati, ad esempio, per interagire con JavaScript.

```html
<input type="text" name="identificativo_testo" value="valore_testo">
```
<br>

## I Form
Per raccogliere i dati dell'utente si utilizzano i **form**, all'interno dei quali si possono specificare vari **moduli** che permettono l'interazione con l'utente. 

 Il tag `<form>` è un tag di blocco che quindi lascia uno spazio prima e dopo la chiusura.

### Elaborare i dati
L'elaborazione dei dati può avvenire:
1. Nel **server**, bisogna quindi specificare alcuni attributi:
	- `action` per specificare a chi inviare i dati (es. URL di una pagina che processerà i dati)
	- `method` per specificare il metodo di invio dei dati al server, **GET** o **POST**
2. Nel **client**, con JavaScript non è più il server ad elaborare i dati ma il browser stesso che **invia i dati a se stesso** e li elabora **ricaricando la pagina**.

	Utilizzando JS per evitare che la pagina venga ricaricata utilizziamo il metodo **preventDefault()** dell'oggetto event.
	
<br>
Ecco alcuni moduli che si possono inserire nei form:

#### text 
```html
<input type="text" name="nome">
<!-- Per creare una casella di testo -->
```

#### file 
```html
<input type="file" name="file_locale">
<!-- Per creare una casella di selezione di file in locale -->
```

#### checkbox 
Permette di creare un gruppo di opzioni selezionabili, ammette **scelte multiple**.

*Codice in html:*
```html
<input type="checkbox" name="pasta" value="pasta tanto bona">Pasta
<input type="checkbox" name="risotto" value=100 checked>Risotto
<input type="checkbox" name="zuppa" value="zuppa" checked>Zuppe
<!-- Gli input con l'attributo checked appaiono come già selezionati -->
<!-- I name devono essere DIVERSI -->
```

*Ecco come appare nel browser:*

<input type="checkbox" name="pasta" value="pasta tanto bona">Pasta
<input type="checkbox" name="risotto" value=100 checked>Risotto
<input type="checkbox" name="zuppa" value="zuppa" checked>Zuppe

#### Radio button
Permette di creare un gruppo di opzioni al cui interno deve essere fatta **un'unica scelta**.

*Codice in html:*
```html
<input type="radio" name="squadre" value="inter">Inter
<input type="radio" name="squadre" value="-100">Juventus
<input type="radio" name="squadre" value="1" checked>Padova 
<!-- Avendo messo lo stesso name questi 3 oggetti corrispondono alla STESSA FAMIGLIA -->
```

*Ecco come appare nel browser:*

<input type="radio" name="squadre" value="inter">Inter
<input type="radio" name="squadre" value="-100">Juventus
<input type="radio" name="squadre" value="1" checked>Padova

#### Select
Crea un menú di opzioni a scorrimento. Il tag `select` è un tag composito, ogni voce deve essere compresa all'interno di un tag `option` e il valore viene specificato con l'attributo `value`.

*Codice in html:*
```html
<select name="colori">
	<option value="red">Rosso</option>
	<option value="blu">Blu</option>
	<option value="#00ff00">Verde</option>
	<option value="1">Nero</option>
</select>
```

*Ecco come appare nel browser:*

<select name="colori">
	<option value="red">Rosso</option>
	<option value="blu">Blu</option>
	<option value="#00ff00">Verde</option>
	<option value="1">Nero</option>
</select>

<br>

## I bottoni
#### submit
Permette di creare bottoni di invio attraverso i quali viene inviato e processato il form.

#### button
Permette di creare bottoni "neutri" ai quali può essere associata un'azione mediante JavaScript.

*Codice in html:*
```html
<button>Avvia</button>
```

*Ecco come appare nel browser:*

<button>Avvia</button>

<br>

## Alcuni nuovi input in HTML5
#### Input type: color
Crea un **color picker**, quel widget utile per la selezione di un colore a partire da una palette di colori.

```html
<input type="color" name="MyBackground">
```

#### Input type: range
Questo tipo di input permette all'utente di inserire un numero tramite uno **slider**. Questo input ha una serie di attributi a disposizione come:
- **min**: per specificare il valore minimo permesso
- **max**: per specificare il valore massimo permesso
- **step:** per specificare il "salto" da un valore al prossimo nell slider

*Codice in html:*
```html
<input type="range" name="voto" min=0 max=5 step=1>
```

*Ecco come appare nel browser:*

<input type="range" name="voto" min=0 max=5 step=1>

#### Input type: search
Serve per creare un **campo di ricerca**.

*Codice in html:*
```html
<input type="search" placeholder="article,..." name="parola">
<!-- Con l'attributo placeholder un suggerimento nel box -->
```

*Ecco come appare nel browser:*

<input type="search" placeholder="article,..." name="parola">

<br>
<br>

### Unità di misura del web
1. **Assolute**:
	- Metri e i suoi multipli/sottomultipli
	- Pollici (inch) e i suoi multipli/sottomultipli
	- **Punti (pt)** 
2. **Relative**:
	- **Pixel (px)**
	- **em**: 1 em è la grandezza in punti del font, si usa per le spaziature. Utile per cambiare la spaziatura in proporzione alla grandezza del font.

1 inch = 2,52 cm &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 1 pt = 1/72 cm &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 1 mm = 3 pt<br>
	
# CSS
I fogli di stile (CSS) sono responsabili dell'aspetto della pagina e del posizionamento degli elementi all'interno della pagina.

**NB**. Html dovrebbe essere visto solamente come un linguaggio **strutturale**, alieno da qualunque scopo attinente alla **presentazione** di un documento, questo è il compito di CSS.

Per implementare un foglio di stile esterno nella pagina utilizziamo il tag `<link>` nell'*head*

```html
<head>
	...
	<link rel="StyleSheet" href="percorso_foglio_stile.css">
</head>
```

Mentre i fogli di stile interni alla pagina vengono definiti nello `<style>` sempre posto nell'head
```html
<head>
	...
	<style>
		h2 {color: red}
		li {padding-left: 50px}	
		.testo {font-family: Arial; color: brown}
	</style>
</head>
```
<br>

## Box-model
L'insieme delle regole che gestisce l'aspetto visuale degli **elementi di blocco** viene riferito al **box model**. Ogni box comprende dei componenti base, ciascuno modificabile tramite CSS.

![[box_model.png]]

- **Area del contenuto**: è la zona in cui **trova spazio il contenuto** (es. testo, immagine, video,...). Possono essere modificate le dimensioni orizzontali `<width>` e `<height>`
- **Padding**: è uno **spazio vuoto** posto tra l'area del contenuto e il bordo. Se si imposta un colore di sfondo per un elemento, esso si estende anche al padding
- **Bordo**: linea di dimensione, stile e colore variabile che circonda il padding e l'area del contenuto
- **Margine**: è uno spazio di dimensioni variabile che **separa** un elemento da un altro

**NB1**. **Box-sizing** è ...

**NB2**. Con un solo valore specificato nel *padding*, altezza e larghezza sono uguali, con 2 valori specificati, il primo specifica la *larghezza*, il secondo l'*altezza*.
<br>

## Selettori di base

#### Selettore universale
Serve a selezionare tutti gli elementi di un documento
```css
* {color: red}
```

#### Selettore di tipo
È costituito dal nome di un specifico tag. Serve a selezionare tutti gli elementi di quel tipo presenti nel documento
```css
h1 {color: red}
/* Tutti i tag h1 nella pagina diventeranno di colore rosso */
```

#### Selettore per ID
L'attributo `<id>` è utilizzato per identificare in modo univoco un **unico** elemento, può essere usato solo una volta nella pagina
```css
#tit1 {color: blue}
/* Definiamo la regola con l'etichetta '#tit1' */
```

```html
<h1 id="tit1">...</h1>
<!-- Assegnamo il colore blu ai tag che presentano l'id 'tit1' -->
```

#### Selettore di classe
Mediante una classe è possibile definire uno o più elementi a cui applicare lo stile. Viene richiamato con l'attributo `<class>`
 
```css
.testo {font-family: Arial}
/* Definiamo la classe con .nome_classe */
```

```html
<p class="testo">...</p>
...
...
<div class="testo">...</div>
...
<!-- Questi elementi utilizzano la classe "testo" -->
```
*Altro esempio:*
```css
p.testobianco {color: white;}
/* Questa regola si applica a tutti i p con la classe testo bianco */
```
<br>

## Selettori combinatori

#### Selettorore  discendente:
Seleziona un elemento che è **discendente** (contenuto al suo interno, a qualsiasi livello) di un altro elemento.

*Alcuni esempi:*
```css
nav li {color: red}
/* Solo gli "li contenuti dento "nav" verranno modificati */
```
```css
#content1 div {color-background: green}
/* Solo i "div" contenuti dentro il tag con id "content1" verranno modificati */
```
```css
.minibox div {border-radius: 10px}
/* Cambio lo stile a tutti i "div" contenuti all'interno dei tag a cui è applicata la classe ".minibox"  */
```

#### Selettore di figli: 
Consente di selezionare un elemento che è **figlio** diretto dell'elemento padre.
```html
<div id="box">
	<p>Primo paragrafo</p>
	<div>
		<p>Secondo paragrafo</p>
	</div>
	<p>Terzo paragrafo</p>
</div>
```
*In questo esempio solo il primo e il terzo paragrafo sono figli diretti di div con id=box*

```css
#box > p {color: white}
/* Questa regola modificherà il primo e terzo paragrafo */
```
<br>

## Selettori di attributo
I selettori di attributo consentono di selezionare gli elementi all'interno di una pagina in base ai loro **attributi** senza dover ricorrere ad una classe o ad un id.

#### E[attribute]
Questo selettore individua tutti gli elementi **E** che possiedono l'attributo **attribute**, indipendentemente dal contenuto dell'attributo.

*Sintassi:*
```css
elemento[attribute] {dichiarazioni;}
```

*Partiamo col definire la regola CSS:*
```css
a[title] {color: blue; text-decoration: underline}
/* Questo stile si applicherà ai tag a con attributo title */
```

*Ecco alcuni esempi a cui verrà applicata la regola sopra:*
```html
<a title='Lorem Ipsum' href='#'>Lorem Ipsum</a>
<a title="" href="#">Lorem Ipsum</a>
<a title href="#">Lorem Ipsum</a>
<a TITLE="Lorem Ipsum" href="#">Lorem Ipsum</a>
/* Nei seguenti casi il testo sarà blu e sottolineato */
```
<br>

## Pseudo-classi e pseudo-classi strutturali
Una pseudo-classe non definisce la presentazione di un elemento ma di un **particolare stato** di quest'ultimo. Possiamo quindi definire uno stile per un elemento al verificarsi di certe condizioni.

*Sintassi:*
```css
selettore:pseudo-classe {dichiarazioni;}
```

Una pseudo-classe segue senza spazi il nome del selettore e **può essere associata a tutti i tipi di selettori**.

*Alcuni esempi:*
```css
/* Pseudo-classe con elemento semplice */
a:link {color: white;}
/* Pseudo-classe con selettore discendente */
p a:link {color: white;}
/* Pseudo-classe con selettore di classe */
a.classe:hover {color: white;}
/* Pseudo-classe con selettore di id */
#id:hover {color: white;}
```

### Pseudo-classi per i link
#### :link
La pseudo-classe **:link** definisce l'aspetto di partenza dei link, ovvero quando NON sono stati visualizzati.

```css
a:link {
	color: white;
	font-weight: bold;
}
/* TUTTI i link non visualizzati saranno di colore bianco e in grassetto */
```

```css
a.classe_1:link {
	color: white;
	font-weight: bold;
}
/* SOLO i link appartenenti alla classe classe_1 saranno modificati */
```

#### :visited
La pseudo-classe **:visited** serve a modificare l'aspetto dei link quando sono stati visualizzati.

### Pseudo-classi dinamiche
Anch'esse servono ad impostare e modificare la presentazione di un particolare stato di un elemento, ma ciò avviene **in seguito ad un'azione dell utente**.

#### :hover
Questa pseudo-classe viene applicata quando si passa il cursore del mouse su un elemento *senza attivarlo*.

```css
a:hover {
	color: green;
}
/* Quando si passa il cursore sopra un qualsiasi link questo diventerà verde */
```

#### :active
La pseudo-classe **:active** serve ad impostare la presentazione di un elemento **quando e mentre esso viene attivato**.

```css
a:active {
	color: red;
}
/* Quando si clicca su un qualsiasi link questo in quell'istante diventa rosso */
```

<br>

## Pseudo-elementi
Nel momento in cui in un foglio di stile si costruisce una regola che ad essi fa riferimento, è come se nel documento venissero inseriti nuovi elementi **fittizzi**, presenti nel CSS ma non nel codice che definisce la struttura della pagina.

Essi non possono essere dichiarati da soli ma **vanno sempre collegati ad altri selettori**.

#### ::before e ::after
**::before** inserisce un altro elemento all'**inizio** del contenuto dell'elemento individuato dal selettore.
**::after** inserisce un altro elemento **dopo** il contenuto dell'elemento individuato dal selettore.

Possiamo indicare quale contenuto vada aggiunto grazie alla proprietà CSS **content** che può essere una semplice stringa, un URL che punti ad un'immagine o ad un documento, o anche **vuoto**.

*Sintassi ed esempi:*
```css
elemento::before {content: "contenuto";}
elemento::after {content: "contenuto";}
```

*Alcuni esempi:*
```css
h3::before {
	content = "";
	background: red
}
/* Aggiunte un contenuto vuoto PRIMA di tutti i tag h3 con sfondo rosso */
```

```css
h3::after {
	content = "";
	background: green
}
/* Aggiunte un contenuto vuoto DOPO di tutti i tag h3 con sfondo verde */
```

## Float e clear
### Float
Con questa proprietà è possibile spostare un elmento su uno dei lati del suo elemento contenitore. Il contenuto che circonda l'elemento scorrerà intorno ad esso sul lato opposto rispetto a quello indicato col valore **float**.

```css
selettore {flaot: valore;}
/* Esempio di sintassi */
```

**float** può assumere questi valore:
- **left**, l'elemento viene spostato a sx del box contenitore, il contenuto scorre a dx
- **right**
- **none**

Un elemento dichiarato float viene reso automaticamente di **blocco**. Più specificatamente *block-level*.

**NB**. Gli elementi di blocco utilizzano tutto il loro spazio **orizzontale** a disposizione.

### Clear
Serve ad impediare che al fianco di un altro elemento appaiano altri elementi con il float. Si applica agli elementi di blocco e **non è ereditaria.**

```css
selettore {clear: valore}
/* Esempio di sintassi */
```

**clear** può assumere questi valori:
- **none**: gli elementi float possono stare a destra e sinistra dell'elemento
- **left**: si impedisce il posizionamento a sinistra
- **right**: si impedisce il posizionamento a destra
- **both**: si impedisce il posizionamento **su entrambi i lati**

## La proprietà display


<br>

## Gestire il colore con CSS
In CSS ci sono varie notazioni per definire i colori:
1. **Con parole chiave**: `color: green`
2. **Esadecimale**: `color: #CC0000`
3. **RGB**: `color: #C00`
4. **Decimale con RGB**: `color: rgb(0%, 0%, 0%)` o `color: rgb(0, 0, 0)` 
	*es*. rgb(255, 0, 0) => rosso
5. **HSL**: definisce Tonalità (Hue), Saturazione (Saturation), Luminosità (Lightness) 

## I siti responsive
I siti **responsive** basano il posizionamento dei loro elementi *in base al dispositivo* da cui si sta visualizzando la pagina; usa una impaginazione *flessibile*.

Per sfruttare al meglio questa tecnica utilizziamo le **media queries**

Nello sviluppo di un sito responsive si parte dalla strutturazione dei contenuti per lo schermo dei **dispositivi mobile**, per poi passare ai dispositivi con schemo più ampio.

### Media queries
Le **media queries** sono dichiarazioni CSS con le quali è possibile **identificare il tipo di dispositivo** o una sua **caratteristica** allo scopo di applicare stili o condizioni differenti in base a delle regole.

**NB.** Abbiamo bisogno di *tante query quante il numero di dispositivi da definire - 1* rispetto al numeri di tipi di visualizzazioni che si vuole ottenere.

#### Come definire una media query
- Prima di tutto dobbiamo definire il **tipo di media** a cui la media query si riferisce. *Es:* `screen`, `tv`, `tty` (terminali),... 
- Si possono utilizzare poi degli **operatori logici** per strutturare una query che rispetta più condizioni per volta.
	- `and` 
	- `not`
	- `only`
- Si possono definire anche delle **caratteristiche dei media**.
	- `width`
	- `orientation`
	- `resolution` 

*Esempio di media-query:*
```css
@media screen and (width: 400px) {
	/* Dispositivi con schermo e di larghezza minima 400px */
}
```






----
Fonti:
- [Guida HTML](https://www.html.it/guide/guida-html/)
- [Guida HTML5](https://www.html.it/guide/guida-html5/)
- [Guida CSS](https://www.html.it/guide/guida-css-di-base/)
- [Guida CSS3](https://www.html.it/guide/guida-css3/)
- Siti di prova presenti nella cartella "Test Html prof.Costa"