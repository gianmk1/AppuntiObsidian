Guide html:
-	html https://www.html.it/guide/guida-html/
-	html5 https://www.html.it/guide/guida-html5/
-	css https://www.html.it/guide/guida-css-di-base/
-	css3 https://www.html.it/guide/guida-css3/

Differenza tra html e html5, la 5 è l'ultimo standard. Vedere link per differenze.

Documento html è sempre fatto ad albero, i tag interni sono annidati

- <html> è il tag principale
	
- come prima riga dire al browser di interpretare com html5 (<!DOCTYPE html>)
	
- nella head mettiamo le cose per spiegare la pagina (tutto ciò che è dichiarativo, title della pagina)
- nel body mettiamo quello che vedo
	
- per andare a capo si usa il tag <br>
	
	-- vedere appunti sui commenti dei file di prova --
	
- il tag <p> lascia una spaziatura tra il precedente tag e il successivo
	
- 6 tipologie di sottotitoli <h*>, più piccolo è il numero e più grande è il testo
	
- <ul> lista non ordinata
	
- <ol> lista ordinata
	
- i Fogli di stile (CSS) sono repsonsabili dell'aspetto della pagina e del posizionamento degli elementi all'interno della pagina
	
- Siti *RESPONSIVE* basano il posizionamento dei loro elementi in base al dispositivo da cui si sta visualizzando la pagina
-  HTML dovrebbe essere visto semplicemente come un linguaggio **strutturale**, alieno da qualunque scopo attinente la **presentazione** di un documento, questo è il compito di CSS
	
- DOM = gerarchia degli elementi all'interno di una pagina
	
- fratelli su html sono sullo stesso livello e hanno lo stesso genitore
	
- Selettore di TIPO: individua tutti i tag di quel tipo e li modifica es. h1 {color: red} 
	
- Selettore per ID
	
- Fogli di stile incorporato esiste solo nella pagina in cui è scritto 
	
- BOX SIZING:
	
![[inserire_foto_sul_desktop_(box model)]]
	
	- Padding: è un ulteriore spazio tra il testo e il margine
	- content-box
	- border-box
	
	
	# ----- 03/11-----
	
	
- Il percorso specificato nell'immagine deve essere quello relativo, quando siamo su un server non sappiamo qual è ogni volta la radice
	
- URL: percorso unico per raggiungere una risorsa (protocollo usato + luogo dove si trova la risorsa)
	
### Collegamenti ipertestuali
	
Un collegamento ipertestuale è la via per raggiungere altri dovumenti (esterni) o altre parti dello stesso documento (interni)
	
	ESTERNI: lasciano la pagina, può essere sempre del mio sito o di qualsiasi del mondo
	INTERNI: non abbandono la mia pagina
	
- href : per collegamento ipertestuale esterno
	
- tag <a> per creare l'*ancora*
	
### Le Tabelle

Devo specificare un certo numero di righe e colonne
	
	<table> : tag binario e di blocco per dire: inizia un tabella, è unico
	
		<tr> : per specificare il numero di righe, tanti tr quanti i numeri di righe
			
		<td> : per tabella rettangolare : ogni <tr> avrà tanti <td> quanti il numero di colonne
			
			
NB: <table> posiziona solamente gli elementi, per modificare lo stile della tabella utilizziamo un foglio di stile


			

Per iplementare un foglio di stile esterno all pagina nella pagina:
			tag <link>
			
<link rel="stylesheet (per dire al browser di interpretare questo file come un foglio di stile)" href="percorso per il foglio di stile">
			
			
### Unità di misura delle pagine web
			
1. **Assolute**: 
	- metri e i suoi sottomultipli o multipli
	- pollici (inch) e i suoi multipli
	- **punti (pt)**
 
2. **Relative**:
	- **pixel (px)** :
	- **em** : 1 em è la grandezza in punti del font, si usa per le spaziature. utile per cambiare la spaziatura in proporzione alla grandezza del font
			
1 inch = 2,52cm
1 punto = 1/72 di inch
1 mm = 3 punti

			
			
### Selettore di ID
			
			
### ----- 05/11 -------
			
			

# I siti responsive
			
Il sito si adatta alle dimensioni della finestra del browser. 
Lo facciamo utilizzando i fogli di stil
--- vedi pagina fatta in classe ---
		
Il foglio si stile sarà suddiviso in 3 sezione. Come  fa a capire il browser come disporre il sito? Tramite le **media-query**
			
Pagina di default di un sito web è index.html
			
		-	<section> : contiene tanti article, es. parte di pagina con molti articoli dentro
		-   <article> : anche l'articolo ha dei tag strutturali per definire come è fatto, ed ha un corpo
			
			
		- <header> : per intestazione pagina, possiamo metterci dento i titoli
			
		- <div> : 
		- <nav> :
			
	Tipi di immagini per siti web, tutti a 3 sono poco onerose in fatto di spazio:
			
		- PNG (tanti colori come jpeg, ma non c'è compressione del jpg => no perdita qualità)
		- JPEG
		- GIF (solo 256 colori)
	

Devo scegliere dei caratteri abbastanza diffusi e non diversi l'uno dall'altro in quanto dimensioni
			
		2 tecniche per indicare i colori (vedi lezioni su guida html):
			
			--- inserire schemi dal sito html ---
			
	1. **RGB** (combinazioni di rosso, verde, blu)
			- posso utilizzare rgb: 100%, 100%, 100%
			- oppure rgb: 255, 255, 255
			- oppure esadecimale es #9933cc
	 # --- ripassare notazione esadecimale + passaggio da rgb a esacedimale---			
			cifre: 0,9
			lettere: A, F
			16 alla 4a
			
	2. **HSL** , vedi schema su guida html
		
### Selettore combinatorio
			
			
# ----- 10/11 ------

		Mediaquery: dichiarazioni, quella parte all'interno dei selettori si verifica solo a certe condizioni
			
		Tante media query - 1 rispetto a quello che si vuol ottenere
			
		
			
Valore border-box in css:
			
- Selettori discendenti:
			
- Figlio: è subito al livello sotto

- Discendente: contenuti dentro altri tag a sua volta contenuti dentro altri tag

- controllare definizione tag inline
			
- con 1 solo valore specificato nel padding altezza e larghezza sono uguali
			con  2 il primo specifica la larghezz, il secondo la altezza
			
			
Nel padding possiamo definire 1, 2 o 4 valori: **non 3**. es. padding-lef, padding-right
			
- SELETTORE DI PSEUDOCLASSE
			
- border è una definizione di stile che può avere tante definizioni al suo interno
			
### impostare suggerimenti su notead++ (es. border)
			
Quando scrivo i fogli di stile questi si riferiscono alla visualizzazione più piccola, nel caso non siano specificate delle media-query. Si parte dal descrivere la visualizzazione poi si passa alla media e alla grande
			
Definire cos'è **section::after** usato in xResponsive
			
			
Per media query vedi xResponsive.css 
			
::after è uno pseudo elemento: genera e inserisce un contenuto dopo un dato elemento
			
### Media query
Dichiarazioni CSS con le quali è possibile identificare il tipo  di dispositivo o una sua caratteristica allo scopo di applicare stili differenti in base a delle regole
			
- width è una delle più utilizzate
			
@media screen and (width: 400px) {
/* regole CSS */
}
		
	Qui sopra: condizioni: schermo e larghezza di **ALMENO** 400px
			

Gli elementi float vengono resi automaticamente di blocco
			
#### Float e clear
			
Il tag section pur essendo strutturale è un tag INLINE
			
			
#### Proprietà display
			inline
			block
			inline-block
			
#### selettore di pseudoclasse
			
			
#### Selettore di pseudoelemento
			
#### i form