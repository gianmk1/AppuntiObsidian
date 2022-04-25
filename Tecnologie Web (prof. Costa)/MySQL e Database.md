# MySQL e i database
Si può tradurre come "archivio"

Mysql si basa sul linguaggio SQL, c'è divisione tra data manipulation e comandi per ricercare.

L'archivio valido ordina le cose e le rende consultabili

Le operazioni tipiche di un database sono la **memorizzazione** e la **ricerca** (cioè **query**). 
I linguaggi moderni hanno un parte di linguaggio dedicata alla costruzione delle tabelle (**database di tipo relazionale**)

**Database di tipo relazionale**: il più famoso è mySQL:
Quando devo memorizzare cose utilizzo una tabella (struttura dati composta da righe e colonne). 
Nel database la prima riga dice cos'è la tipologia del dato che sta nela relativa colonna

*es*. tabella: 		idPersona		nome		cognome		dataNascita
È una tabella a 4 colonne e ogni riga a partire dalla seconda avrà dei dati coerenti alla colonna a cui appartiene

In una tabella ogni riga è un **record** (o entry).
In una tabella ogni colonna è un **campo**.

Una relazione è un'entità che lega più tabelle.
È conveniente che in una tabella ci sia un campo che ogni record memorizzato assume un valore diverso *es. IdPersona*, in nome/cognome ci potrebbero essere degli omonimi.

??? Il campo che ha funzione di distunguere ogni record si chiama **chiave primaria**

<table>
	<tr>
		<td>idScuola</td>
		<td>NomeScuola</td>
		<td>Comune</td>
	</tr>
	<tr>
		<td>XY4</td>
		<td>Severi</td>
		<td>Padova</td>
	</tr>
</table>


**Tabella di collegamento**: riporta le 2 chiavi primarie di altre due tabelle

Le relazioni fanno sì che possa considerare una tabella unica invece di 2 divise.

*Io organizzo tabelle e poi vedo le relazioni che ci sono tra queste*



#### Primo esemio:
Costruisco una tabella con Sigla e una chiamata NomeContinente

Tabella CONTINENTI:

<table>
	<tr>
		<td>Sigla</td>
		<td>NomeContinente</td>
	</tr>
	<tr>
		<td>EU</td>
		<td>europa</td>
	</tr>
	<tr>
		<td>SA</td>
		<td>sud america</td>
	</tr>
	<tr>
		<td>NA</td>
		<td>nord america</td>
	</tr>
	<tr>
		<td>OC</td>
		<td>oceania</td>
	</tr>
	<tr>
		<td>AF</td>
		<td>africa</td>
	</tr>
	<tr>
		<td>AS</td>
		<td>asia</td>
	</tr>
</table>

La colonna sigla diventa la **chiave primaria**
<br>

Tabella NAZIONI:

<table>
	<tr>
		<td>NomeN</td>
		<td>SiglaC</td>
	</tr>
</table>

La chiave primaria non può essere **NomeN**, che non è in grado di memorizzare gli stati degli usa e gli stati del mondo insieme poichè c'è lo stato - paese Georgia

**Chiave esterna**: 

Separando le tabelle in un certo modo posso "riunirle" quando ho bisogno di cercare qualcosa

Da terminale:
C:\xampp\mysql\bin\mysql -u root -p

Quando creo un database devo scegliere anche la codifica con cui il db deve memorizzare i caratteri

use nome_database;			per selezionare quale db usare

show tables;		per mostrare le tabelle 

create table nome_tabella(campo_1);		per creare tabella

nome_campo tipologia_campo			per creare riga

*è conveniente andare a capo per la leggibilità*

tee appunti; crea un file appunti nella directory dove ho lanciato il comando, con su scritto tutti i comandi e gli output ricevuti

char(2) per tipologia di dato   *caratteri* e con max 2 cifre

`,` per scrivere la riga seguente

varchar(20): ci permette di arrivare a lunghezza max di 20, ma se scrivo una parola di minor lunghezza, alloca solo il numero di caratteri necessari. Serve quindi per stringhe di **lunghezza diversa**, definisco la più lunga con varchar(max_lunghezza)

`not null`  : se lo metto DEVO dare sempre definire un valore

**QUERY**: ha più di 1 significato, il più delle volte si intende una particolare istruzione (**SELECT**), molte applicazioni invece la intendo come qualsiasi comando io scriva in un database


`describe nome_tabella` mi ritorna la struttura della tabella

`insert into Continenti values:` volgio caricare l'intero record, ogni record avrà sempre 2 (in questo caso) e 2 soli valori

es. `('AF','Africa')`

esempio di ricerca con select:
select Sigla,NomeCon from Continenti

`select * from nome_tabella` : elenca tutti i campi della tabella

`where Sigla='NA';` es. di applicazione di un filtro, con **where** filtro i dati, prendo in cosiderazione solo quella con il campo Sigla = NA

`select NomeCon from Continenti where NomeCon like 'A%' ` : l'operatore **like** si usa sui campi di tipo stringa e seleziona tutti i record il cui NomeCon che iniziano con 'A'

`select NomeCon from Continenti where NomeCon like '%ca';` : seleziona i record della tabella che finiscono con 'ca'


I comandi **alter** modifichano ciò che c'è scritto dopo
I comandi **create** creano ciò che c'è scritto dopo

`idCitta int(10) unsigned not null auto_increment` : idCitta è un intero di 10 cifre positivo non vuoto. Con **auto_increment** ogni volta che aggiunto un record lui si aggiorna incrementando di 1. Questo campo poi lo useremo come chiave primaria

`primary key (idCitta)` : metto il campo idCitta come chiave primaria

**NB**. Non ci va la virgola quando siamo all'utima parentesi tonda


Per la chiave esterna serve che il campo sia della stessa dimensione di quello a cui si vuole legare:

`Continente char(2) references Continenti(Sigla),` : per la chiave esterna utilizzo la parola **references** e poi nome_tabella(nome_campo)



`bigint` : per un intero molto grande

`foreign key (nome_campo_chiave_ext) references nome_tabella(nome_campo) `

NB. può essere, a seconda della versione di xampp, che con lo describe tabella MUL appaia solo come chiave esterna definita con foreign key ...

`insert into Citta (idCitta, NomeC, Popolazione) values` : Il mio record che inserisco sarà fatto solamente da tre valori.

**NB**: nel caso di valori interi ovviamente non metto gli apici tra il valore

Mysql potrebbe essere utilizzato senza server web, ma con quest'ultimo c'è anche la parte grafica

**NB**: per esportare db mysql su phpMyadmin > seleziona_db > esporta > esegui. Creiamo sulla nuova macchina, sempre su phpMyAdmin, un database con lo stesso nome del precedente e poi vado su *import* > scegli_file > esegui

**Engine**: è il motore di memorizzazione: da delle regole alla tabella, le più famose di **Integrità referenziale**, cioè delle regole: ???

NB: InnoDB è il motore di default

#### Integrità referenziale ???

es. non posso dare una chiave esterna con valore che non esiste nell'altra tabella
es2. se cancello record con una chiave primaria posso dire di non mantenere i dati anche nell'altra tabella collegata

Se volgio cancellare una chiave esterna prima bisogna cancellare un vincolo che viene creato

----

record e tupla non sono sinonimi, 

NB: il campo contatore ogni volta che inserisco qualcosa incrementa il valore partendo dall'ultimo dato

Il linguaggio SQL quando nato aveva una sintassi di comandi chiamata SQL-1 , poi sono uscite SQL-2 e SQL-3.
Con query complicate useremo SQL-2

La sigla where serve solo per filtrare i dati delle tabelle una volta unita

Quando ho bisogno di collegare più tabelle utilizzerò le operazioni di **JOIN**

NB in sql-1 le unioni di tabelle si facevano con where, ora con sql-2 utilizziamo **JOIN**

**NB**. Possiamo utilizzare gli operatori di comparazione nel where: and, or (anche between); nel between gli estremi sono compresi

**order by ...**, risultato della query viene ordinato in base al campo descritto, se aggiungiamo **desc** c'è l'ordinamento decrescente

### Le funzioni di aggregazione
es. `select count(nomeC) from citta` : ritorna il numero di record che hanno il campo nomeC valorizzato (nel caso di un campo null, sarebbe il numero di valori)

possiamo utilizzare `as 'Numero Città'` per cambiare nome nella query di ritorno

alcune funzioni di aggregazione: somma, media, minimo, massimo

**LE funzioni di aggregazione ritornano UN SOLO VALORE**

avg() per la media
floor() per arrotondare all'intero più vicino

Funzioni tipiche delle stringhe:
upper() per ritornare valori in MAIUSCOLO
lower() per ritornare valori in minuscolo

**update** è il comando per aggiornare/**cambiare**

NB. Per commentare: --

### inner join

Un join tra tabelle, coinvolte la chiave primaria di una tabella con quella esterna di un'altra tabella

SQL 2 prevede che gli inner join siano esplicitati

con **on** specifico le chiavi



NB. inner si può anche omettere

### legare le funzioni di aggregazione con i campi delle tabelle, QUERY ANNIDATE

le funzioni di aggregazione da sole ritornano SEMPRE un solo valore

**group by** : mette in relazione una funzione di aggregazione con un campo

QUERY ANNIDATA: una query con dentro una query (select dentro un select)


**NB.** Una query che **ritorna un solo risultato** si chiama **query scalare**.
L'opposto di scalare è VETTORIALE

**NB** proprietà **distinct**: se ci sono più record uguali ne ritorna uno solo

##### Query città meno popolata insieme al continente di appartenenza

-- abbiamo dovuto mettere join Nazioni on Nazione=NomeN perchè, nonostante NomeC, Nazione e NomeCon non siano nessun campo di nazioni, serve per individuare il campo Continente nel join seguente. In pratica ho utilizzato la "proprietà transitiva"

## GROUP by
combina le funzioni di aggregazione e le ordina rispetto un determinato campo.

#### having
Serve per filtrare (come con il where)
è praticamente il where che si usa quando c'è il group by.

Having senza group by **non esiste.**

## Concetto di variabile
quando abbiamo una query scalare possiamo creare una variabile per contenere il valore di ritorno di questa query.

per dichiarare variabile : set @nome_variabile
per vedere contenuto variabile : select @nome_variabile;


Per semplificare le query annidate (scalari) posso ridurre la sintassi creando delle varibili

In una variabile posso mettere 1 solo dato, e non esistono gli array in mysql.

Una volta usciti da mysql la variabile diventa nulla


##### Funzione ceil(), per arrotondamento dei numeri, arrotonda 

## Query vettoriale
![[vedi esempio su appunti17dic]]

*vedi commenti sul foglio appunti*

**IN** : "si trova in", "è dentro a", "se"




per ogni > quindi nel select bisogna utilizzare il group by, col group by **spesso** c'è una funzione di aggegazione


count(*) conta il numero di righe, chiave primaria

count(*) è una notazione diversa per contare il numero di righe all'interno di una tabella, si basa sui campi del join

Tabella : fotografa in quel momento lo stato delle cose, se faccio select di quella tabella mi rispecchia la situazione in quel momento, se cambio il contenuto della tabella il risultato della query rimane lo stesso (è il risultato nel momento in cui è stato invocato)


LA VISTA è diverso, è DINAMICA

Per veder il contenuto di una vista **select * from nome_vista** 
Accanto alla vista c'è anche la tabella temporanea

TABELLA TEMPORANEA : non è una tabella creata con create table .. ma è il risultato di una query

per creare tabella temporanea : create temporary table nome_tabella_temporanea as ...

NB. Se i dati della tabella a cui è associata una vista sono stati aggiornati automaticamente si aggiornano anche i dati della vista

LISTA è una specie di tabella aggiornata in modo DINAMICO


La tabella temporanea è come una variabile che si inizializza al logout
La vista invece rimane


#### Natural Join
Se devo collegare 2 tabelle **attraverso 2 campi che hanno lo stesso nome**

#### Selft join
Che potrebbero essere anche dei natural / inner join, ma vanno sotto questo nome perchè fanno dei join con **se stessa**


