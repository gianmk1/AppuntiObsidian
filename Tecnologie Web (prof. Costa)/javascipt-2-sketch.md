# Javascript
Linguaggio di programmazione presente nel browser

Quando visualizzo una pagina il browser potrebbe accorgersi che nella pagina è presente un blocco di codice

Nel web 2 modalità per l'interazione:
1. CLIENT SIDE; quando l'elaborazione del codice avviene sul client, ovvero nel browser della macchina che sta visulizzando la pagina (esempio javascript e i suoi framework)
2. SERVER SIDE: (la più antica nel mondo web), invio dei dati da qualche parte nel server, e specificato in quale modo. Quando l'elaborazione avviene sul server web, la pagina invia i dati a qualcuno sul server web; questi gli elabora e spedisce una risposta sottoforma di pagina html (esempio: PhP, jsp, asp.net)

Jsp è il java trasporatato nell ambiente web

I database possono essere consultati attraverso una pagina web

Javascript è principalmente client-side ma ci sono delle alcune parti che possono essere eseguite sul server

Un linguaggio è composto da parole chiave che metto insieme per svolgere un determinato compito, presenti all'interno di determinate LIBRERIE (insime di funzioni)

FRAMEWORK: ha una libreria per utilizzare un linguaggio ed è anche un ambiente di programmazione (es. jquery)
È una ambiente di supporto sul quale un software può essere realizzato

PARADIGMI di programmazione:
1. IMPERATIVO: anche i linguaggi con altri paradigmi hanno insito l'imperativo, si basa sul concetto di algoritmo. 
2. ORIENTATO AGLI OGGETTI: si basa sui concetti di CLASSE e di OGGETTO, la classe è una specie di stampo, l'oggetto è invece ottenuto dallo stampo. *Esempio:* mi chiedo cos'è un rettangolo, come lo determino? Sono 2 segmenti paralleli e 2 perpendicolari della stessa lunghezza tra loro. La classe del rettangolo implementa una serie di operazioni (METODI) che operano su degli oggetti (i rettangoli)
3. ORIENTATO AGLI EVENTI: si basa sul concetto di EVENTI, ovvero qualcosa che può succedere, in una pagina web es: muovo mouse, clicco su qualcosa,.. ; Si può associare del codice quando l'evento si verifica (esempio VisualBasic, rende semplice alcune cose, ma complicato tutto il resto)

Javascript è orientato agli EVENTI
Molti linguaggi di programmazione sono degli **ibridi**

L'argoritmo è una sequenza ordinata di istruzioni UNIVOCHE, cioè sono interpretate ugualmente da tutti (es. C)
Un linguaggio orientato agli eventi può essere comunque ad oggetti, non sono dei blocchi definiti quelli specificati 

Ajax pone una via di mezzo tra client-side e server-side

https://www.html.it/guide/guida-javascript-di-base/


JavaScript è nato ed rimasto un importante supporto ad HTML, specie con l’avvento dello standard Html5. Per questo il browser rimane per esso l’ambiente d’uso privilegiato.


Codice Javascript si può scrivere:
- in blocchi di codice nella pagina
- importare file con codice Javascript esterno

Più riesco a fare la pagina html pura (senza js) meglio è

Nei linguaggi di programmazione le funzioni e i metodi hanno un nome e una lista di parametri

### Variabile
VARIABILE: è un contenitore di un certo tipo
![[commenti nel file primoJS.js]]


`;` in C e Java è un delimitatore, in JavaScript il `;` è solamente un separatore per istruzioni scritte sulla stessa riga, non è necessario altrove

In JavaScript non esistono i tipi di variabili, una stessa variabile può essere inizializzata con qualsiasi tipo di dato. Es. `var x = 5; x = x + 1`

var x = 5		è un istruzione composita, sto dichiarando x come una variabile a cui sto inizializzando il numero 5

x = x + 1		ciò che sta a destra dell'uguale finisce nel contenitore che sta a sinistra dell'uguale; Prendi il contenuto di x, sommaci 1 e metti il tutto dentro x




**NB**. Javascript è case-sensitive, c'è distinzione tra lettere minuscole e maiuscole

Js risiede nel browser, serve a rendere la pagina html interattiva


--- vedi file .js fatti in classe ---


OGGETTO E RIFERIMENTO

Oggetto: è un qualcosa che occupa tanto posto, 

Riferimento: è quello che mi permette di raggiungere la locazione

Posso creare il riferimento prima dell oggetto, 

Abbiamo più livelli di astrazione:
html ha una struttura ad albero, javascript e css3 hanno bisogno di beccare i specifici elementi dell albero (in javascritp si chiama DOM) (in CSS si usa ID)

'document' rappresenta il body

getElementById è un metodo applicato su document che mi ritorna l'oggetto cui attributo ris

METODO: AZIONE, cose che posso fare su un oggetto, che può cambiare le proprietà dell'oggetto
Prioprietà: caratteristica di un oggetto, si possono cambiare in modo DIRETTO o GENERALE

Struttura di selezione IF, vuole una condizione che vale o true o false

3 finestre di aler:
- ...
- ...
- alert con form


span onclick="mostraS()">

studiare lezione 60
studiare lezione 64
studiare lezioni da 1 a 8 CSS3

W3C: si occupa di far standardizzare web e i browser

DOM: 

I vari tipi di nodi nell html:

**lezione 65**

getElementById()  : ritorna un solo elemento
getElementsByName()  : ritorna più elementi


ARRAY:
- posizionale : ogni elemento è identificato oltre dal nome dell'array anche dalla posizione che occupa all'interno dell'array
- **associativo**: il contenuto di ogni elemento dall'array non è identificato dalla posizione ma da un nome

il getElemetsByName() ritorna un array

document.getElementByTagName("p"); = ritorna tutti i tag p all'interno della pagina in un array

**NodeList**: lista dei nodi

getElementsByClassName = fa riferiemento all'attirbuto classe del tag html, anche questo sarà un array

#### querySelector
`querySelector()` e `querySelectorAll()`
2 metodi di document, sfruttano i selettori css3, l'argomento di entrambi è un selettore css3

var divList = document.querySelectorAll("div.messaggio"); => qui c'è un selettore di CLASSE (prendo tutti i div che hanno l'attributo class 'messaggio')

querySelectorAll() ritorna sempre un array, anche se solo di un elemento

querySelector() ritorna solo il primo elemento trovato nella pagina

es. querySelector(#esempio) , con selettore per id, corrisponde a `getElementById()`



## --- 19/11 ---

Nella pagina primoBISJS.js non c'è nulla di javascript nella pagina, devo quindi associare un evento in un altro metodo, es. con addEventListener

`document.querySelector("span").addEventListener("click", mostraS)`

querySelector(span) ritorna il primo elemento span nella pagina. in generale come argomento queryselector vuole un selettore css3

Testo:
Creare la pagina terzo.html e la relativa pagina js per acquisire mediante 2 finestre di dialogo
un numero naturele n e un saluto s. La pagina mostrerà il saluto s in 2 forme: 
s s s s (per n volte) 
s
s
...
s
(per n volte)


Nei linguaggi a paradigma imperativo c'è un teorema che dice che qualasiasi programma può essere scritto tramite 3 strutture: sequenza, selezione e iterazione

Sequenza: in ordine una dopo l'altra
Selezione: c'è una condizione, se vera faccio qualcosa, se falsa potrei fare qualcosaltro
Iterazione: c'è una condizione, è vera: eseguo qualcosa e ripeto ciò finchè questa condizione è vera, se falsa faccio qualcosaltro

Iterare = Ciclare

In generale si possono classificare i cicli in 2 famiglie:
1. Cicli a condizione: io non ho idea di quante volte avverrà l'iterazione
2. CIcli a contatore: a priori so già quante volte verrà eseguito il ciclo (es. FOR)

**NB.** Break and Continue è un modo per uscire dalla rigidità delle strutture, meglio utilizzare correttamente switch-case

#### Il ciclo FOR
3 pezzi: 

![[inserire schema ciclo for]]

Inizializzazione: inizializzazione del contatore
NB. molte volte è più comodo che il contatore parta da 0
Condizione: 
Modifica:

NB i++ è diverso da i+1

for-in e for-of

In javascript e java la capienza e la lunghezza corrispondono, l'allocazione è dinamica

L'allocazione degli array in java e javascript è DINAMICA
Per sapere quanto è lungo un'array una volta dichiarato `nome_array.length`, lo posso mettere anche nei cilci come parte di condizione


Va evitato ogg.innerHTML = ogg.innerHTML  + s in un ciclo


Creare la pagina terzoBIS.html e la relativa pagina js per acquisire mediante 2 finestre di dialogo un numero naturele n e un saluto s. si vuole un elenco numerato di n voci in cui la singola voce sia s.
Si vuole inoltre un altro elenco numerato in cui la i-esima voce sia s ripetuto i volte

esercizio terzoBIS

**Chiamata funzione**: es. mostraElenco(num,sal) 
(Funzione per creare 2 elenchi numerati. Il parametro num indica il numero di voci, Il parametro sal indica il testo (o parte di esso) delle voci)

### I form html in Javascript

vedi file primoform.html e primoform.js

Un form è composto da caselle di testo e da oggetti (chiamata caselle select o menu a discesa) poi ci sono delle voci con dei cerchietti selezionabili

Questi strumenti permettono di scegliere un UNICA opzione tra tante disponibili

Modulo è il singolo elemento del form

Ci sono poi i CHECK-BOX, qualsiasi può esserer selezionata o meno

Questi moduli vengono inseriti nel tag `form`

Form nasce con HTML1, si limitava a raccogliere informazioni e con un pulsante le si inviavano al server per poi ricevere una risposta in HTML, il tag doveva specificare: come inviare i dati e a chi inviarli (queste cosa sono rimaste in php e asp.net)

Con JS non è più il server che elabora i dati ma il browser stesso, scompaioni i 2 attributi precedenti citati e ne compaiono altri

Il tag form nasce con degli attributi per spedire e il browser li spedisce a se stesso e li elabora ricaricando la pagina. Doabbiamo dire quindi di non ricaricare la pagina

Oggetto **event**

il metodo preventDefault() dell'oggetto event impedisce il caricamento della pagina dopo che è avvenuto un evento nel form

Casella SELECT

Famiglia di radio button

attributo booleano checked

Etichetta e valore sono 2 cose diverse

In checkbox i name devono essere diversi

?? Con i checkbox il valore della voce checkata 
