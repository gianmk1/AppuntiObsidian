# Javascript
**Javascript** è un linguaggio di programmazione presente nel browser, serve per rendere la pagina **interattiva** Quando visualizzao una pagina web quest'ultimo potrebbe accorgersi che nella pagina è presente un blocco di codice.

Ci sono 2 modalità di interazione nel browser web:
1. **CLIENT SIDE**: quando l'elaborazione del codice avviene sul client, ovvero nel browser della macchina che sta visualizzando la pagina (*es. Javascript e i suoi framework*)
2. **SERVER SIDE**: i dati vengono inviati da qualche parte nel server specificandone la modalità. L'elaborazione quindi avviene sul web, il server elabora i dati e spedisce una risposta sottoforma di pagina Html (*es. PhP, Jsp, asp.net*)

**NB**. I database possono essere consultati attraverso una pagina web
**NB2**. Javascript è principalmente *client-side* ma ci sono alcune parti che possono essere eseguite sul server

##### Alcune definizioni:
- **LIBRERIA**: una libreria è una **collezione di funzioni specializzate** per un determinato compito, tramite il codice decidiamo dove, quando e quali funzioni richiamare.
- **FRAMEWORK**: è una **ambiente di programmazione** predisposto alla realizzazione di un'applicazione, dove noi *inseriamo il codice al suo interno*. È definito anche come un **insieme di librerie**, con una **nuova sintassi** del linguaggio.
<br>

### Paradigmi di programmazione
In informatica un paradigma di programmazione un insieme di strumenti concettuali forniti da un linguaggio per la stesura del codice. Stili di programmazione diversi si traducono in codici software diversi. Possono essere di vari tipi:
1. **IMPERATIVO**: si basa sul concetto di **algoritmo**, vedi sotto
2. **ORIENTATO AGLI OGGETTI**: si basa sul concetto di **classe** e **oggetto**
3. **ORIENTATO AGLI EVENTI**: si basa sul concetto di **evento**, ovvero qualcosa che può succedere. Si può associare del codice quando l'evento si verifica. Es. in una pagina web: muovo mouse, clicco su qualcosa,... (*es. Visual Basic, Javascript*)

**NB**. Molti linguaggi di programmazione sono degli **ibridi** tra le varie categorie.
<br>

##### Alcune definizioni:
- L'**algoritmo** è una **SEQUENZA ORDINATA di istruzioni UNIVOCHE**, cioè sono interpretate ugualmente da tutti (*es. C*).
- **OGGETTO**: è un insieme di **attributi** (o *proprietà*) e **metodi**; Gli **attributi** definiscono le caratteristiche dell'oggetto, cioè lo **stato**. I **metodi** invece definiscono le *operazioni eseguibili* sull'oggetto (ovvero il comportamento).
- **CLASSE**: è un **modello che definisce il tipo di oggetto**, cioè un modello per tutti gli oggetti dello stesso tipo. **Descrive gli attributi e i metodi** degli oggetti della classe.

**NB**. La classe è lo **"stampo"** per creare gli oggetti. Un oggetto è un **esemplare** (o istanza) della classe.
<br>

## Implementare Javascript
Javascript è nato e rimasto un importante supporto ad HTML, soprattutto con l'avvento dello standard HTML5. Per questo motivo il browser rimane per esso l'ambiente d'uso privilegiato.

Il codice HTML si può scrivere:
- In blocchi di codice **interni** alla pagina
- Importando un file **esterno** con codice Javascript
	```js
	<script src="file_js.js"></script>
	```
	
**NB**. È importante scrivere una pagina HTML più *pura* possibile (senza js)
<br>

## Variabile
La **variabile** è un contenitore di dati di un certo tipo situato in una porzione di memoria.

```c
/* Solitamente le variabili sono di varie tipologie: */

int a			// Variabile per contenere interi
float b			// Variabile per contenere reali coficica a singola precisione
double c		// Variabile per contenere reali codifica a doppia precisione
char d = 'A'	// Variabile per contenere un carattere, Inizializzata con valore 'A'
bool a			// Variabile che può assumere i valori TRUE o FALSE
```

**In Javascript** però **non esistono tipi di variabili**, una stessa variabile può essere inizializzata con qualsiasi tipo di dato.

*Alcuni esempi:*
- `var x = 5` è un **istruzione composita**, sto dichiarando `x` come una variabile a cui sto inizializzando `5`
- `x = x + 1`  è un'operazione di **assegnazione**, ciò che sta a dx del `=` finisce nel contenitore che sta a sx (`x`); Allo stesso tempo sto sommando `1` al contenuto di `x`

*Alcune note:*
- Il nome della variabile non deve coincidere con una delle parole chiave del linguaggio
- Non può contenere i caratteri  `-`, `?`, `.` e lo spazio

##### Costante
Possiamo anche dichiarare delle costanti con `const PIGRECO = 3.14`
<br>

## Conversioni tra tipi di variabili
È importante **evitare le conversioni implicite** di JavaScript che sono spesso fonte di bug. Per convertire esplicitamente un valore ricorriamo ad alcune funzioni:

La funzione **parseInt** converte una stringa in un valore intero. *Es:*
``` javascript
parseInt("12")		// ritorna 12
parseInt("12ab")	// ritorna 12
parseInt("12.5")	// ritorna 12
```
Se inseriamo un secondo parametro, indichiamo la base del sistema di rappresentazione numerica utilizzato. *Es:*
``` javascript
parseInt("12", 8)	// Il valore 12 nel sistema numerazione in base 8, cioè 10
```
<br>

La funzione **parseFloat** restituisce un valore numerico considerando l'eventuale virgola. *Es:*
```js
parseFloat("12")	// ritorna 12
parseFloat("12.5")	// ritorna 12.5
```
<br>

## Commenti e punto-virgola
In JavaScript, a differenza di altri linguaggi di programmazione (*es. C*), il `;` fa solamente da **separatore** per istruzioni scritte sulla stessa riga.
<br>

In JS esistono 2 tipi di commenti:
1. **per singola riga**:
	 ```javascript 
	 // Questo è un commento
	 ```
2. **multiriga**:
	
	```javascript
	/* Questo è un commento multiriga.
	Seconda riga di commento. */
	```

<br>

## If, if-else e switch-case
``` javascript
if (condizione) {
	// Istruzioni
}
```

``` javascript
if (condizione) {
	// Istruzioni
} else {
	// Istruzioni 2
}
```

``` javascript
if (condizione_1) {
	// Istruzioni
} else if (condizione_2) {
	// Istruzioni 2
} else {
	// Istruzioni 3
}
```

```js
switch (espressione) {
	case espressione1:
		istruzioni1;
	break;
	case espressione2:
		istruzioni2;
	break;
	// ...
	default:
		istruzioni4;
	break;
}
```
<br>

## I cicli
In generale si possono classificare i cicli in 2 famiglie:
1. **A condizione**: dove non si sa quante volte avverrà l'iterazione
2. **A contatore**: dove a priori si sa già quante volte verrà eseguito il ciclo (*es. Ciclo FOR*)

**NB**: Ciclare = **Iterare**

### I cicli for
```js
for (inizializzazione, condizione, modifica) {
	// istruzioni
}
```
- **Inizializzazione**: si inizializza (e si può anche dichiarare) il **contatore**
- **Condizione**: è l'espressione booleana che viene valutata prima di eseguire il codice, se è falsa si esce dal ciclo
- **Modifica**: avviene al termine di ciascuna iterazione (la classica è l'incremento del contatore *es. i++*)
<br>

#### for-in
Sfruttando questa variante non abbiamo bisogno di specificare nè la lunghezza dell'array nè l'istruzione di modifica della condizione.

*Esempio di for-in:*
```js
var quantita = [12, 34, 45, 7, 19];
var totale = 0;
var indice;
for (indice in quantita) {
	totale = totale +  quantita[indice];
}
```
JS rileva che la variabile `quantita` è un array ed assegna ad ogni iterazione alla variabile `indice` il valore dell'indice corrente.

#### for-of
Con questa variante non abbiamo bisogno di dichiarare una variabile `indice` ma ne utilizziamo una che contenga il `valore` della cella specifica dell'array.

*Esempio di for-of:*:
```js
var quantita = [12, 34, 45, 7, 19];
var totale = 0;
var valore;
for (valore of quantita) {
	totale = totale +  valore;
}
```
Ad ogni iterazione JS assegna alla variabile `valore` il contenuto di ciscun elemento dell'array.
<br>

## While e do-while
```js
while (condizione) {
	// Istruzioni
}
```

```js
do {
	// istruzioni
}
while (condizione)
```
<br>

### Break e Continue
Sono due modalità utilizzate per uscire dalla rigidità delle strutture, meglio non abusarne. Piuttosto utilizzare l'istruzione **switch-case**.
<br>

## Array
Gli **array** consentono di associare più elementi ad un unico nome di variabile; sono divisi in **celle** e permettono di non dover definire più variabili e semplifica alcune operazioni.

#### Definire gli array
In Java e JavaScript la capienza e la lunghezza degli array corrispondono e quindi l'allocazione è **dinamica**.

*Definizione di un array **vuoto***:
```js
var voti = []
```
*Definizione dell'array e del suo contenuto*:
```js
var giorniDelWeekend = ["sabato", "domenica"]
```
*Definizioni di un array con elementi di vario tipo:*
```js
var myArray = [123, "stringa", true, null];
```

#### Richiamare un elemento dell'array
La numerazione degli indici dell'array parte da **zero**. Per richiamare ad esempio il secondo elemento dell'array facciamo:

```js
var secondo_elemento = myArray[1]
```

#### Verificare lunghezza array
Per sapere quanto è lungo un'array dopo averlo dichiarato utilizziamo la proprietà **lenght**.

```js
var lunghezza_array = nome_array.length
// Inizializzo la variabile 'lunghezza_array' con il valore numerico della lunghezza dell'array
```
```js
console.log(nome_array.length)
// Scrive un messaggio nella console con la lunghezza dell'array
```
<br>

## Funzioni in JS
L'utilizzo di una funzione all'interno di uno script prevede 2 fasi:
1. **Dichiarazione** (o definizione)
2. **Invocazione** (o chiamata), in cui il blocco di codice viene eseguito.  

### Dichiarazione 
```js
function nome(argomenti) {
	// istruzioni
}
```
**NB.** Gli **argomenti** sono una lista opzionale di variabili separati da virgole che verranno utilizzate all'interno del corpo della funzione.

### Invocazione
```js
nome(valori);
```

**NB**. Gli eventuali valori inseriti nella chiamata vengono *passati, cioè assegnati* ai corrispondenti argomenti della dichiarazione della funzione.

#### Return
Consente di terminare e restituire un valore al codice che l'ha chiamata. Ci consente di assegnare ad una variabile restituito da una funzione.

##### Esempi di funzioni in JavaScript:
```js
// Dichiarazione:
function somma(x, y) {
	var z = x + y
	return z
}

// Passiamo tramite la chiamata i valori che da sommare

// Invocazione:
var risultato = somma(5, 4)
```

### Variabili locali e globali
Le variabili dichiarate all'interno di una funzione sono dette **locali**. 
Le variabili dichiarate fuori da qualsiasi funzione sono dette **globali**,  poichè accessibili da qualsiasi punto dello script, anche all'interno di funzioni. 

Se all'interno di una funzione dichiariamo una variabile con lo stesso nome di una locale, il riferimento alla variabile sarà inteso come il **riferimento alla variabile locale**.

#### Let
Lo scope di una variabile **let** è limitato al blocco di codice, all'istruzione o all'espressione in cui viene utilizzata.

*Esempio:*
```js
var x = 0
for (let i = 0; i < 10; i++) {
	x = x + i
}
```

### Alcune funzioni predefinite:

#### parseInt e parseFloat
*Vedi sopra alla sezione "Conversioni tra tipi di variabili"*

#### isNaN e isFinite
La funzione **isNaN()** prende un argomento e restituisce **true** se il suo valore è NaN, cioè NON è un valore numerico valido, altrimenti **false**.

**isFinite()** restituisce **true** se il valore del suo argomento è diverso da **Infinity** e da **NaN**
<br>

## Pop-up e finestre di dialogo
Quelli che descriviamo qui sotto sono alcune metodi dell'oggetto **window**:

#### alert()
Visualizza una finestra modale con messaggio e pulsante OK
```js
window.alert("Questo è un messaggio");
```

#### confirm()
Visualizza una finestra modale con messaggio e due pulsanti: uno per la conferma e uno per l'annullamento. Il pulsante restituisce un **valore booleano** che rappresenta **true** o **false**

```js
if (window.confirm("Confermi l'eliminazione?")) {
	// Se la risposta è affermativa...
}
```

#### prompt()
Chiede l'inserimento di un valore che viene catturato e restituito

```js
var nome = window.prompt("Inserisci il tuo nome");
if (nome != null) {
	// Inizializzo 'nome' col dato inserito dall'utente
	// Se la variabile 'nome' NON è vuota...
}
```
<br>

## DOM
**Document** è un **oggetto** che **rappresenta il documento HTML** caricato nella finestra corrente. La struttura di questo oggetto è nota con il nome di **DOM**.

Il DOM fornisce una rappresentazione del documento come una **composizione gerarchica** di oggetti chiamata **DOM tree**. La radice di questo albero è l'**oggetto document**.
I diversi tipi di **nodi** presenti nel DOM tree sono:
- **document**: costituisce la **radice dell'albero**, normalmente è uno solo
- **elemento**: individua un tag HTML come ad esempio `<body>`, `<div>`
- **attributo**: corrisponde ad un attributo HTML come ad esempio `src` del tag `<img>`
- **testo**: corrisponde al contenuto testuale di un nodo 
<br>

## Selezionare gli elementi del DOM
Il DOM consente anche di manipolare questi oggetti tramite JavaScript.
Possiamo accedere agli elementi della pagina utilizzando diversi criteri:

### getElementById
È un **metodo** applicato su document che mi **ritorna l'oggetto** (rappresentate un nodo), che ha l'attributo **id** con il valore specificato.

*Esempio:*
```html
<p id="p_uno">Questo è un paragrafo</p>
<!-- Definiamo un elemento con un certo valore per l'attributo ID -->
```

```js
var p = document.getElementById("p_uno")
// Restituisce un oggetto che rappresenta l'elemento con valore ID 'p_uno'
```

**NB**. getElementById ritorna un solo elemento

#### Altri metodi simili:
- **getElementsByName**: restituisce l'elenco dei nodi della pagina il cui valore dell'attributo **name** corrisponde a quello del parametro
- **getElementsByTagName**: restituisce l'elenco di tutti i nodi di una pagina in base al loro tag
- **getElementsByClassName**: otteniamo tutto l'elenco di nodi a cui è stato assegnato un determinato valore come attributo **class**

Questi metodi possono ritornare più elementi, ovvero un elenco di oggetti detto **NodeList**, cioè una struttura dati simile ad un **array**, anche se questo dovesse contenere un solo elemento.

*Alcuni esempi:*
```js
document.getElementsByTagName("p")
// Ritorna tutti i 'p' all'interno della pagina in un'array
document.getElementsByClassName("nome_classe")
// Ritorna tutti gli elementi che hanno come attributo la classe 'nome_classe'
```


### querySelector e querySelectorAll
Tramite questi due metodi possiamo **selezionare gli elementi** di una pagina **utilizzando i selettori CSS**.

**querySelector()** restituisce il primo elemento trovato nella pagina
**querySelectorAll()** restituisce l'elenco di tutti gli elementi individuati dal selettore in un array

*Alcuni esempi:*
```js
var divList = document.querySelectorAll("div.messaggio")
// Restituisce l'elenco dei div di classe messaggio
```

```js
var p = document.querySelector("#mioParagrafo")
// Seleziona l'elemento con id 'mioParagrafo'
// Risulta come alternativa a getElementById()
```
<br>






### Metodo e proprietà
<br>

### Oggetti e Riferimenti
<br>

### innerHTML
<br>

### addEventListener
<br>







---
[Guida JavaScript](https://www.html.it/guide/guida-javascript-di-base/)