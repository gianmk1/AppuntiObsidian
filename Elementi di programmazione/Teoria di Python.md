**NB**. Gli appunti seguiranno il testo consigliato nella lezione 1.

# Teoria di Python
Alcune caratteristiche di Python:
- **sintassi semplice**, è molto user-friendly ma è molto facile anche uscire dalle regole
- **è molto veloce ad interagire con i numeri**, una tabella in excel è molto più facile gestirla con python che con excel
- **enunciati**, cioè le parole chiavi, nomi variabili, ecc. sono molto semplici
- il tipo delle variabili lo decide il compilatore, quindi **non posso dichiarare una variabile senza darle un valore iniziale**
- è difficile capire quando una variabile viene dichiarata e quando viene utilizzata. NON c'è più distinzione tra dichiarazione e assegnazione

Python non richiede la dichiarazione, come in C, di un main. Il main è direttamente tutto il programma scritto.
In questo modo però *se voglio dichiarare una classe devo esplicitarlo*.

**NB**. Quando abbiamo programma multi-file bisogna stare attenti con i nomi delle variabili.

In C le stringhe sono un'array di caratteri. In python invece si possono **utilizzare le stringhe in modo molto più efficiente.**

Python è utilizziato soprattutto in ambito **data-science**, devo catalogare vari tipi di dati nel modo in cui voglio io, gestendo a "basso livello".

# CAP 1
## Errori
Gli errori possono essere:
1. **In "compilazione"**, cioè abbiamo scritto qualcosa di sbagliato
2. **In esecuzione**, durante l'esecuzione si è verificato qualcosa di sbagliato (es. divisione per 0)

Alcuni esempi di errori:
- di **SINTASSI**
- di **I/O input-output**

## Gestione I/O
**OUTPUT** -> stampare a video qualcosa
**INPUT** -> dare un dato che sia scelto dall'utente finale (e non dal programmatore)

Per fare un ouput solitamente si utilizza **print**.
Quando stampiamo più oggetti con print, questi vengono stampati con un separatore (di default è lo spazio).

*Esempio di output:*

```python
print("testo", "di", "prova", end="")
print("ciao")

# In questo modo l'ouput sarà:
# testo di provaciao


print("testo", "ciao", "prova", sep="-")

# In questo modo l'output sarà:
# testo-ciao-prova
```

*Esempio di input:*

```python
nome = input("Come ti chiami? ")

# "Come ti chiami?" viene definito prompt, o suggerimento
```

L'input ritorna un valore, cioè quello scritto dall'utente. Questo valore lo posso memorizzare all'interno di una variabile.

NB. Ciò che l'**utente inserisco sarà sempre e solo una STRINGA**.

#### Operazioni tra stringhe
```python
str1 = "ciao1" + "ciao2"
print(str1)

# Ritorna 
# ciao1ciao2
```

- **.capitalize()** , mette il primo carattere della stringa in maiuscolo
- **.isdigit()** , controlla se la stringa è un numero
- **.splitline()** , stacca le rine quando trova un a capo
- **.split()** , stacca le stringhe mediante il separatore che noi scegliamo: ogni parola viene messa all'interno di un array
- **.strip()** , toglie tutti gli spazi **all'inizio e alla fine**

*Alcuni esempi:*
```python
testo = "prova di testo con spazi"
testo.split()		# Output: ["prova", "di", "testo", "con", "spazi"]
```

## CASTING
Ovvero modellare. Fare il cast significa prendere un'oggetto e modellarlo in un altro modo.

```python
x = int(y)
```

**NB1**. Non possiamo fare un cast tra un numero col la virgola e un numero interno poichè il cast taglierebbe tutta la parte decimale del numero.
**NB2**. Se facciamo un cast da stringa a numero python ritorna errore.

## NB. Alcune precisazioni
Python in realtà **NON** è un linguaggio compilato, poichè non viene creat un altro file in linguaggio macchina, ma il sorgente viene letto e "compilato" (che è per lo più il controllo della sinstassi e della scrittura del codice) ed **eseguito immediatamente**.

NB. Come funziona la **compilazione**:
1. Codice sorgente scritto dal programmatore
2. Compilazione del codice sorgente
3. Risultato in un file scritto in linguaggio macchina
4. Per avviare il programma si utilizza il file in linguaggio macchina

## Commenti
I **commenti documentazione** di solito di mettono a inizio programma nel main.
All'interno si mette l'HEADER con:
- Autore
- Nome programma
- Descrizione del programma

NB. In python NON si possono fare i commenti multiriga, per questo vengono utilizzate le """ che sono delle stringhe multiriga

```python
"""
Autore: xxx
Programma: nome.py
Programma di prova...

"""

# Le stringhe multiriga sono a tutti gli effetti delle stringhe

```

## Variabili
I tipi di variabili in python sono:
- **Interi**, tipo int -> 10 , 5, -6, ...
- **Decimali**, tipo float (virgola mobile) -> 0.2, -123213.3, ...
- **Stringhe**, tipo str -> *qualsiasi cosa basta che sia un carattere ASCII* es. "come stai?"
- **Booleano**, tipo bool -> 0, 1, True, False
- **Char**, tipo char -> 'a' , 'g'

NB. In python non si specifica mai la tipologia della variabile, ma si utilizza quando vogliamo fare un **CAST** (*vedi sopra*)

**I numeri hanno un limite**, l'intero e i float hanno come estremi: -2³¹ <-> 2³¹ . Se usciamo da questo intervallo python non ce lo dice, superato l'intervallo si taglia la fine e si riparte dall'inizio.

**NB1**. piGreco è un numero irrazionale, in uncomputer non possiamo memorizzare infinite cifre dopo una virgola: anche con questo genere di numeri dobbiamo stare attenti a quanto/quando tagliare i numeri

**NB2**. In C si usano le "" per le stringhe e '' per i caratteri. In python (anche se non necessario) conviene mantenere la convenzione.

## I caratteri di Escape
Nelle stringhe possiamo scrivere tutto quello che vogliamo, se all'interno di questa vogliamo che qualcosa non venga considerato come carattere "normale".

Il **backslash \\** viene considerato come carattere speciale. 

*Alcuni tipi di caratteri di escape*:
- **\n** -> per andare a capo
- **\t** -> per tabulare
- **\b** -> backslash, per cancellare il carattere subito prima. *es. ciao\b -> cia*

NB1. TAB sono 4 spazi
NB2. Se voglio scrivere backslash (\\) all'interno di una stringa ne devo scrivere 2: \\\

Anche le **virgolette** (singole e doppie) all'interno di una stringa hanno bisogno dei caratteri di escape.

## Le stringhe
In python le **stringhe sono delle variabili a tutti gli effetti** (a differenza di C, ...)

**CONCATENAZIONE**:
```python
stringa = "ciao" + " " + " Marco"
# Output: ciao Marco

stringa2 = "Ciao"*2
# Output: CiaoCiao

```

La concatenazione può essere utilizzata anche con le varibili (che deve essere di tipo stringa), conviene quindi esserne certi facendo un cast. *es. str(variabile)*

### Estrarre un CARATTERE da una stringa
```python
str = "myfile.txt"

# Per contare il numero di caratteri in una stringa
len(str) 	# Output: 10 (intero)


# Per ritornare uno specifico carattere della stringa
str[8] 		# Output: 'm'


# Per ritornare l'ultimo carattere di una stringa
str[len(str) - 1]	# Output: 't'


str[len(str) - 1]	# Output: IndexError


# Shortcut per ritornare l'ultimo carattere:
str[-1]		# Output: 't'


# Shortcut per ritornare il primo carattere:
str[-len(str)]		# Output: 'm'

```

### Estrarre una STRINGA da una stringa
```python
str = "myfile.txt"

# Prende dal carattere con indice 0 a quello con indice 9
str[0:10]		# Output: myfile.txt


str[2:6]		# Output: file

# NB. L'ultimo indice, come nella funzione range, viene escluso


# Prendere dall'inizio all'indice specificato:
str[:6]			# Output: myfile


# Prendere da un indice fino alla fine:
str[4:]			# Output: e.txt


# Prende gli ultimi 3 caratteri:
str[-3:]		# Output: txt



# NB. Queste sono operazioni valide per Array

```

### Verificare se una stringa è presente all'interno di un'altra stringa
```python
file = "myfile.txt"


# Verificare se una stringa è presente all'interno di un'altra stringa
"txt" in file
# "in" è un operatore logico
# Ritorna True o False


# Verificare se un elemento è all'interno di un'array
array = []
elem in array
# Ritorna True o False

```

## Operazioni aritmetiche
- Cambio del segno, a -> -a
- Sottrazione, a - b
- Addizione, a + b
- Moltiplicazione, a * b
- Divisione, a / b
- **Quoziente**, a // b . Anche detta **divisione intera**
- **Resto**, a % b, **restituisce il RESTO di una divisione (non la parte intera)**
- **Potenza**, a ** b , che corrisponde a^b

**NB1**.  In C la divisione tra due interi ritorna sempre un interno, viene troncata la parte decimale. In python invece se la divisione richiede un float python lo utilizza. L'operazione **quoziente ritorna sempre la PARTE INTERA di una divisione**.

**NB2**. Il % si utilizza anche per identificare se un numero è PARI o DISPARI

## Operazioni con tipi diversi
Dobbiamo sapere molto bene come si comporta il python in questa situazione.
Non richiedendo la specifica del tipo della variabile solitamente ritorna problemi in queste situazioni.

```python
# Alcune situazioni e cosa ritorna python

2.5 - 2 -> float 0.5
3.0 - 2 -> flaot 0.0
2.5 ** 2 -> float n
2 + 5 -> int 7
```

## Le LIBRERIE
Le librerie sono delle collezzioni di funzioni, già create da altri programmatori, che possiamo utilizzare.

#### Come si importano le librerie?
*Ci sono **4 modi** per importare le librerie:*

```python
import [nome_libreria]
# Per importare TUTTE LE FUNZIONI di una libreria

from math import sqrt
# Per importare dalla libreria math solo la funzione "sqrt"

from math import *
# Per importare TUTTO da math
# NB. È diverso da "import math". Permette di importare tutta la libreria senza dover aver bisogno di specificare il nome della libreria prima della funzione

import math as m
# Per richiamare tutte le volte la libreria math col nome "m"
```
<br>

#### Alcune librerie importanti
- **math**, libreria matematica (con seno, coseno, tangenti,...)
``` python
math.sqrt(10, 2)
# Radice di 10 in base 2
# Se abbiamo fatto "import math"

sqrt(10, 2)
# Se abbiamo fatto "from math import *" o "from math import sqrt"

m.sqrt(10, 2)
# Se abbiamo importato la libreria con "import math as m"
```

#### Scrivere una libreria
I nostri file possono essere delle librerie che importiamo nel nostro codice.

Per importare **file locali**:
```python
import prova
```

NB. prova == prova.py . Essendo in locale dobbiamo **specificare il percorso della libreria** o mettere la libreria e il codice in cui la richiamiamo nella stessa variabile.

**NB1. Se dichiariamo 2 volte le stesse cose succede un casino**
**NB2. Se importiamo 2 volte le stesse librerie non sappiamo cosa l'interprete eseguirà**
Quando importiamo librerie nostre: lasciamo sempre il nome o mettiamo un alias

Se abbiamo progetti in più file, è importante importare la libreria in un unico file (solitamente nel main).
<br>

## Assegnazioni abbreviate
```python
a = a + 3 ---> a += 3
a = a - 3 ---> a -= 3
a = a * 3 ---> a *= 3
a = a / 3 ---> a /= 3
```

## String FORMATTING pt1
```python
nome = "marco"
cognome = "rossi"

"1.		nome:marco		cognome:rossi	"
"1.		nome:filippo	cognome:bianchi	"

# Per avere una stringa impaginata correttamente:

stringa = "%6s" % nome
# in questo caso l'allineamento parte da DX
# output: " marco" , solo 1o spazio vuoto rimanente

# % -----> impaginazione
# 6 -----> numero di caratteri MAX che la stringa può avere
# s -----> tipo della variabile (dopo il 2o %), s sta per stringa
# % -----> indica la variabile successiva
# nome --> variabile da sostituire



stringa = "%-10s" % nome	
# in questo caso l'allineamento parte da SX
# output: "filippo   "



stringa = "%-5d%-11s" % (numero, nome)
# output: "1     marco      "

```

## String FORMATTING pt2
```python
var = "marco"

print("Ciao, %s, benvenuto!" % var)
# Questo era il metodo precedente

# Possiamo utilizzare questo nuovo metodo:

print(f"Ciao, {var}, benvenuto! {var2}")
# Questa "f" fa capire a python che la stringa è formattata
# La variabile va messa tra { }
```

## Cicli
Solitamente si utilizza un ciclo WHILE per fare in modo che il programma non venga chiuso ma sia l'utente a scegliere se chiuderlo o meno.

### Ciclo FOR
```python
for i in range(4):
	pass

# range(4) restituisce un array composto da 0, 1, 2, 3



arr = ["ciao", "prova", "come"]
for i in arr:
	pass

# i sarà ciascun elemento dell'array




for indice,valore in enumerate(arr):
	print(i)
	
# indici ---> [0, 1, 2]
# valori ---> ["ciao", "come", "va"]

# solitamente:
# i per indice
# k per valore

```

**NB1**. Al posto delle parentesi in python per delineare un ciclo utilizziamo le tabulazioni.

*Alcune parole chiave:*
- **pass**, serve per dire di NON fare nulla
- **continue**

La funzione **enumerate** restituisce 2 array, quello con gli indici e quello con i valori.

#### CONTEGGIO degli INDICI e altri esempi
```python
for i in range(1,4):
	pass

# range(1,4) resituisce un array composto da 1,2,3



for i in range(var1, var2):
	pass

# bisogna stare attenti che var1 e var2 siano DIVERSE



for i in range(0, 2, 0.5):
	pass

# range(1,4) resituisce un array composto da 0, 0.5, 1, 1.5



for c in "ciao come va?":
	pass

# l'array sarà: c, i, a, o, ' ', c, o, m, e, ' ', v, a, ?

```

#### Ciclo FOR all'INDIETRO
```python
for i in range (10, 0, -1):
	pass

# [10, 9, 8, 7, 6, 5, 4, 3, 2, 1] , ovviamente lo 0 NON lo si prende altrimenti avremmo ritornato 11 valori (e non 10)
```

<br>

## LISTE
Una lista in Python è un array. In Python, a differenza degli altri linguaggi, non dobbiamo definire i tipi valori che conterrà la lista.
**Possiamo avere diversi tipi di dati all'interno della stessa lista/array.**

**NB**. In Python gli array **NON HANNO DIMENSIONE FISSA**.

```python
lista = []				# per definire una lista vuota
```

**NB**. In Python la lista si definisce con [ ] .

### Metodi per gli array
- **.append()**, aggiunge come ultimo elemento della lista
- **.clear()**, azzera
- **.pop()**, rimuove l'ultimo
- **.reverse()**, inverte
<br>

## if-else
In programmazione gli IF si utilizzano solamente per fare delle decisioni.

```python
if (condizione):
	espressione

# nella condizione ci può essere un'operazione, un cast, ...
# basta che il risultato sia True o False



if (condizione):
	espressione
else:
	espressione2



if (condizione):
	espressione
elif (condizione2):
	espressione2
else:
	espressione3
```

### Operazioni logiche
- Uguale , ==
- Diverso , !=
- Maggiore , >
- Minore , <
- bool(0) == false
- bool(!=0) == true
- AND , &&
- OR, ||

#### Altri operatori logici
- **is** --> controllo con l'operatore successivo
- **in** --> controllo di contenimento

## While
*È importante che la condizione del ciclo venga modificata all'interno del ciclo stesso.*
```python
while <False/True>:
	<codice>
	
# NB. Se non si modifica la condizione del while all'interno del ciclo while stesso, questo si tramuterà in un LOOP INFINITO
	
```

### Break
Il **break** mi fa uscire dal ciclo, in qualunque momento venga letto, **senza guardare la condizione**.
<br>

## LEGGERE e SCRIVERE su file in python
*Bisogna dichiarare una **variabile di tipo file**, questa variabile è collegata all'indirizzo di memoria del file cui le abbiamo assoiato.*

**STREAM** = una serie di valori che entra a NON finire

Possiamo specificare la **modalità con cui apriamo i file**: lettura o scrittura.

La funzione close scrive/esegue tutto il codice che abbiamo scritto all'interno del file. Se non scriviamo il close probabilmente il codice NON funzionerà.

**NB.** Quando apriamo un file con open, **IL FILE VIENE SOVRASCRITTO**.

Possiamo aprire più volte il file (nel caso dovessimo chiuderlo a metà codice e poi riaprirlo)

```python
# Apri "myfile.txt" in modalità LETTURA
file = open("myfile.txt", 'r')

# Apri "myfile.txt" in modalità SCRITTURA
file = open("myfile.txt", 'w')

# Scriviamo sul file
file.write("Ciao sto scrivendo del codice")

# Leggiamo il file e lo mettiamo dentro la variabile "testo"
testo = file.read()
# Ouput: "Prima linea\nSeconda linea\nTerza linea"

# Bisogna sempre chiudere la stream
file.close()
```
*Quando chiamiamo il **.write** il file non viene scritto fino a quando non chiamiamo il **.close**, le informazioni scritte col write vengono quindi **temporaneamente** memorizzate in un'altra locazione.*

**NB**. Bisogna **chiamare il close** anche quando si apre il file in **modalità lettura**.

<br>
<br>

## I Dizionari
**Il dizionario è un collegamento tra 2 elementi**. In python ci è utile perchè mette in collegamento 2 elementi (di qualunque tipo)

#### Ripasso

```python
first = [1,2,3]
second = first

first[0] = 4

print(first)
print(second)

# Output:
# ["4","2","3"]
# ["4","2","3"]

# Verrà cambiato sia il valore di "first" che di "second"
# NB. Nonostante i puntatori in python NON esistano, come vediamo sopra 
# verrà modificato sia "first" che "second"
```

**NB1**. Per gli array in python, fare un **=**, corrisponde a **fare un PUNTATORE**.
**NB2**. Questo esempio sopra NON vale per variabili e stringhe

I dictionary hanno comunque, come gli array, **indici**, ma questo non è più 0,1,2 ma un **elemento che noi scegliamo**.

CHIAVE <--> VALORE

```python
# Dizionario
# [key : valore , key2 : valore2 , ...]

# Array
# [0 : valore1 , 1 : valore2]
```

**NB**. Gli array (liste) possono essere visti come un tipo di dizionario, dove l'indice è un numero che incrementa di 1 a partire da 0.

**Nel dictionary ad ogni indice c'è una coppia CHIAVE <-> VALORE**.

<br>
<br>

#### Tuple
Le Tuple sono **array NON MODIFICABILI**, solitamente si usano con 2 elementi.

*In python le tuple si dichiarano con le parentesi tonde.*

```python
tupla = ("chave", "valore")
```

### Dictionary
Un dizionario è una struttura dove un **nome (CHIAVE) è collegato ad un VALORE.**

*Come si definiscono:*
```python
dizionario = {
	"marco" : 12332,
	"caio" : 432894,
}


# Per prendere un valore da un dizionario, utilizziamo la CHIAVE
dizionario["marco"]		# Output: 12332


```

Conviene che le chiavi siano sempre dello stesso tipo, **possibilmente a stringhe**.

*Come si utilizzano i dizionari?*
```python
# Ritorna tutte le coppie chiave-valore del dizionario
dizionario.items()

# Ritorna tutte le chiavi del dizionario
dizionario.keys()

# Ritorna tutti i valori del dizionario
dizionario.values()

# Diamo una chiave e toglie la coppia chiave-valore specificata
dizionario.popitem("chiave")

# Dando la chiave ritorna il valore
dizionario.get("chiave")

```

<br>
<br>

##  Le FUNZIONI
Le funzioni in programmazioni sono delle funzioni matematiche, intesi come pezzi di codice.

Una funzione ha parametri: **????**
- **Parametri**, che possono essere infiniti
- **Argomenti opzionali**, di cui devo specificare il nome

*I parametri possono essere:*
- **Posizionali**: i primi ad essere scritti
- **Nominali**: anche detti di default

La particolarità delle funzioni è che è definita per quasiasi sia la x io dia come input.
- Posso avere più input
- Gli input possono essere nominati o meno, **per primi vanno sempre gli elementi SENZA NOME**

```python
print("Ciao", end="-", sep=" ")

# Il "ciao", cioè il parametro va sempre all'inizio
# "end" è un argomento opzionale
```

### Definire una funzione
```python
def funzioneDiProva(amount, percent):
	"""Funzione custom, testo di spiegazione
	testo spiegazione
	"""
	
	return amount * percent / 100

	# amount e percent sono dei PARAMETRI

```

**NB**. Possiamo creare una documentazione della nostra funzione, sempre come prima riga della nostra funzione.

In python una funzione può ritornare un valore o meno a piacimento, noi NON dobbiamo specificarlo. È buona norma, all'interno della documentazione della funzione, specificare se questa ritorna o meno un valore.

### Richiamare una funzione
```python
# In questo caso la funzione ritorna un intero, lo possiamo memorizzare all'interno di una variabile
interesse = funzioneDiProva(1000, 5)
```

**PARAMETRI** = valori da dare quando richiamiamo una funzione
**RITORNO** = valore di ritorno di una funzione
**ESPRESSIONI** = operazioni all'interno di una funzione

<br>

### Funzione MAIN
È una **variabile di sistema**, che vengono definite con i **doppi underscore**.

```python
def __main__():
	"""Funzione main dello script"""
	
```

In C la funzione MAIN è la funzione da cui parte il codice.

In Python la funzione MAIN è utile quando abbiamo un progetto multifile. Il compilatore di python riconosce la pagina dove è presente la funzione main come la parte principale del codice, e quindi come **punto di partenza di esecuzione del codice**.

*Esempio:*
```python
if __name__ == "__main__":
	main()
	
# Se il nome della funzione è main, allora ESEGUO IL NAME
```

Le funzioni e variabili con il doppio underscore davanti e alla fine sono **funzioni di sistema**.

**NB**. Esistono anche le **variabili di sistema**.
<br>

###  Parametri di default

```python
# Dobbiamo fare una funzione che scrive all'interno di un file

def scrittura(stringa, nome_file):
	file = open(nome_file. 'w')
	file.write(stringa)
	file.close()

scrittura("ciao")	
```

*Questa funzione scriverà solo sul file che abbiamo specificato all'interno. Mettendo un **secondo parametro** (nome_file) possiamo specificare il file su cui scrivere.*

A questo punto però dobbiamo **sempre specificare il nome del file**, per ovviare a questo problema possiamo utilizzare un **default**.

```python
# In questo modo quando chiamo la funzione posso specificare (o meno) nome_file, di default sarà testo.txt

def scrittura(stringa, nome_file="testo.txt"):
	file = open(nome_file. 'w')
	file.write(stringa)
	file.close()

scrittura("ciao")
```
<br>

### Funzioni ricorsive
Le **funzioni ricorsive** rimandano indietro e fanno rifare tutto.

Una funzione è ricorsiva quando **all'interno del corpo della funzione è richiamata la STESSA FUNZIONE**.

**NB**. La chiamata alla stessa funzione deve essere **preceduta dal return**. NON facendo il return, il compilatore non capisce che quella funzione è finita.

```python
def funzione_ricorsiva():
	return funzione_ricorsiva()
```

Una **funzione ricorsiva è sempre traducibile in una funzione NON ricorsiva**, es. con un while. Si preferisce utilizzare le funzioni ricorsive perchè sono più veloci da scrivere. **NON è detto però il contrario.**

``` python
# Esempio: funzione fattoriale
5! = 5 	*	4!
			4! = 4	*	3!
						...
```

Nelle **funzioni ricorsive** deve esserci un **CICLO**, bisogna essere sicuri che la funzione ricorsiva che stiamo scrivendo vada bene per ogni iterazione del ciclo.

Nelle funzioni ricorsive si **va all'indietro**. *Per sapere cos'è 3! devo prima sapere 2!.*

*Nelle funzioni ricorsive ci sono 2 punti fondamentali:*
1. Il **PASSO RICORSIVO** = **riconoscere lo schema** che bisogna fare ogni volta che si chiama la funzione ricorsiva. Nel passo ricorsivo bisogna **modificare il parametro per arrivare al caso base**.

2. Il **CASO BASE**, o anche **punto di stop** è il punto in cui il compilatore deve fermarsi e NON richiamare più la funzione ricorsiva. *Nell'esempio del fattoriale, l'1 è il caso base.*

**NB1**. Il **LOOP INFINITO** è un errore ricorrente quando si scrivono funzioni ricorsive. 
**NB2**. In alcune funzioni **potrebbe essere utile fare 2 casi base**, cioè 2 punti di stop.

```python

# Esempio della funzione FATTORIALE

def funzione_ricorsiva(parametro):
	# Caso base, ovviamente con un IF
	if parametro == 1:
		return 1

	# Passo ricorsivo
	# MODIFICARE IL PARAMETRO PER ARRIVARE AL CASO BASE
	return parametro * funzione_ricorsiva(parametro - 1)
	# Tradotto sarebbe: return 5 * 4!
```

*Perchè dovrei utilizzare una funzione ricorsiva?*
- Più elegante
- Più facile da scrivere
- *Più facile da capire cosa fa la funzione*

Dal punto di vista del computer però **le funzioni ricorsive sono molto più pesanti e dispendiose di risorse**, lo stack viene continuamente riempito e fino a che non arrivo alla fine della funzione ricorsiva ci sono **molte chiamate di funzione in SOSPESO**.

### Esempi di chiamata di funzione
1. **Classico**
```python
def funzione():
	...
	...
	

funzione()
```
2. Come **dato**
```python

def molt(num1, num2):
	return num1 * num2

# Posso utilizzare "operazione" come funzione
def calcolatrice(num1, num2, operazione):
	return operazione(num1, num2)
	
calcolatrice(4, 5, molt)

```

**NB**. Mettendo il nome di una funzione **senza parentesi**, è come se utilizzassimo un **puntatore.**

3. **Copia funzione**, in questo modo posso **creare un ALIAS** alla funzione.
```python
# In questo modo creo un ALIAS alla funzione
rinomino = calcolatrice

rinomino(4, 5, molt)
```

### Funzione MAP
**map**(funzione, iterable, ...)

La funzione **map** fa la **mappatura**. Prende **come input una funzione ed una lista** (o più), per ogni elemento della lista *(iterable)* viene applicata la funzione indicata. Avremo come **output una nuova lista**.

```python
words = ["432", "23", "467876"]

map(int, words)

```

<br>

## Eccezioni
Un'**eccezione** è un errore logico che viene fuori durante l'esecuzione del programma e viene mostrato dal compilatore.

*Esempio: 5 / 0 (divisione per 0)*

*Alcune eccezioni:*
- **NameError**, il valore non si sa cos'è
- **ValueError**, solitamente avviene nei cast

### Costrutto TRY - EXCEPT
**TRY**: prova ad eseguire il codice,... se non funzione **except**

**NB**. È buona norma mettere **meno codice possibile** all'interno di un try.

*Sintassi base:*
```python
try:
	int("st")
except:
	print("Qualcosa è andato storto!")
	# Ricorsa l'else dell'if
	# Qualsiasi sia l'errore, viene ritornata questa stringa
```

All'interno di un try posso verificarsi vari tipi di errori. Possiamo creare **diversi except** per **diversi errori**.

```python
try:
	int("st")
except NameError:
	print("Hai fatto un name error!")
except ValueError:
	print("Hai fatto un name error!")
except:
	print("Qualcosa è andato storto!")
	# Ricorsa l'else dell'if
	# Qualsiasi sia l'errore, viene ritornata questa stringa
```

**NB.** È possibili intercettare più eccezioni per volta: `except (NameError, ValueError):`

Esiste anche il **finally**, che esegue SEMPRE il suo blocco di codice.
```python
try:
	int("st")
except:
	print("Qualcosa è andato storto!")
finally:
	print("Questa stringa verrà stampata in ogni caso!")
```

**NB**. Nel caso si verifichino più errori, verrà eseguita l'eccezione del primo errore trovato (*nell'esempio sopra sarebbe NameError*)

##### Lanciare errori
In python possiamo anche lanciare degli errori, server quando stiamo scrivendo degli oggetti esterni (librerie), in modo da liberarsi dal problema di dover gestire gli errori.

```python
raise ValueError
```
<br>

## Funzioni: alcune specificazioni
Ai parametri posizionali posso riferirmi **sia per posizione che per nome**.

```python
def prova(name1 = "", name2 = ""):
	pass


# I primi parametri che scrivo sono sempre POSIZIONALI
def positional(pos1, pos2)

# Mettiamo voglia dare la facoltà all'utente di decidere se usare posizione o nome:
# Per prima cosa mettiamo sempre i posizionali standard, tutti i parametri 
# dopo lo / potranno essere posizionali o nominali
def positional(pos1, pos2, /, pos_or_name = "", pos_or_name2 = ""):
	pass

# NB. Per forzara i parametri come NOMINALI, al posto dello / utilizziamo l'*

# Definiti per posizione
positional(33, 55, ciao, prova)
# Definiti per nome
positional(33, 55, pos_or_name2 = "testo", pos_or_name = "prova")

```

*Per riferirmi **solo tramite nome**:*
```python
def positional(*, name1 = "", name2 = ""):
	pass

positional(name2 = "ciao", name1 = "testo")
# Posso definire i parametri SOLO TRAMITE NOME
```

#### Capire il tipo di variabili di una funzione
- **:str** , **:int** , ... specificano che tipo di variabile deve essere il parametro
- La **->** mi specifica il **valore che ritorna la funzione.**
```python
def annotation(par1:str, par2:int) -> str:
	"""Documentazione funzione"""
	pass
```

**NB.** Queste sono solo annotazioni, **nessuno vieta all'utente** di inserire un intero all'interno di par1, quindi di **inserire un tipo di variabile diverso da quello definito**.

#### Definire una funzione con INFINITI valori POSIZIONALI 
Possiamo utilizzare gli array per inserire un **numero infinito di parametri posizionali**
```python
def array(*elem_to_print):
	pass

# Il parametro elem_to_print è un ARRAY e saranno tutti parametri posizionali nella funzione
```

#### Gerarchia dei parametri
1. Parametri **posizionali**
2. **Un solo elemento array**
4. Parametri **nominali**

Oppure al posto dei parametri nominali possiamo mettere un **DICTIONARY**

```python
def gerarchia(pos, pos2, *elem_to_print, name=""):
	pass

gerarchia(45, "ciao", "primo val", "secondo val", "terzo val", name="testo")
# I primi 2 sono posizionali, gli altri andranno tutti all'interno del parametro *elem_to_print
```

#### Dictionary come parametro
```python
def dictionary(pos, pos2, *elem_to_print, **dictionary):
	pass

dictionary(24, "ciao", "val1", "val2", ciao="ciao2", test="test2")
```

`ciao="ciao2"` sarà il **primo elemento del dictionary**.

**NB**. Le funzioni, anche quando non specifichiamo un valore di ritorno, **ritornano sempre un valore None**.
<br>
<br>

## Le CLASSI
Python è un linguaggio orientato agli oggetti. 
**Un oggetto è un qualsiasi tipo di variabile che possiamo definire in qualsiasi modo noi vogliamo**. La classe è il tramite per definire l'oggetto.

Le **CLASSI** sono un **"tipo astratto"**, stiamo defininendo una "classe di oggetti".
*Es. classe persona, questa ha un nome, un'altezza, un'età, ...


##### Attributi GLOBALI (o Statici)
```python
class Persona:
	# la classe persona potrebbe avere attributi globali, a cui devo per forza 				
	# dare un valore di default:
	altezza = 180
	eta = 20
	nome = "vuoto"
```

Definita in questo modo, tutti gli oggetti Persona hanno queste variabili come default.
Come faccio a specificare tutte le caratteristiche di una persona specifica?
**Usiamo un COSTRUTTORE**, che costruisce un oggetto nel modo in cui lo richiedo.

`def __init__()` , **come primo parametro potrebbe esserci SEMPRE SELF**, dopodichè possiamo inserire i classici parametri che vogliamo

```python
class Persona
	braccia = 2		# Questa sarà comune a tutti gli oggetti Persona


	def __init__(self, altezza:int, eta:int, nome:str):
		pass
```

**NB**. `braccia = 2` è una **variabile globale**, tutte gli oggetti appartenenti alla classe Persona avranno questa variabile.

#### Costruzione di un oggetto
```python
class Persona
	braccia = 2


	def __init__(self, alt:int, eta:int, nome:str):
		pass

# In questo modo CHIAMIAMO IL COSTRUTTORE, non devo inserire self
persona1 = Persona(190, 2, "gianmarco")		
```

**self** è un **puntatore** che si riferisce all' "oggetto su cui stiamo facendo il punto" (= **genitore**), cioè *persona1*

> Dobbiamo impostare i **parametri dati come attributi dell'oggetto**

```python
class Persona
	braccia = 2


	def __init__(self, alt:int, e:int, n:str):
		self.altezza = alt
		self.eta = e
		self.nome = n
	
```


#### Accedere agli attributi di un oggetto
```python
persona1.braccia
persona1.altezza
```

*braccia* è un **attributo** di persona1

**NB**. `oggetto.__doc__` mi ritorna la documentazione che abbiamo scritto di una classe

```python
class Persona
	braccia = 2


	def __init__(self, alt:int, e:int, n:str):
		self.altezza = alt
		self.eta = e
		self.nome = n
	
	def sleep(self, time):
		print(f"Ciao, {self.nome}, hai dormito per {time} ore")
		
		
# Chiamiamo la funzione
persona1.sleep(8)
		
```

#### Attributi BLOCCATI ALL'ESTERNO
```python
class BankAccount:
	
	def __init__(self, initial_amount):
		self.balance = initial_amount
		
		
		
conto = BankAccount(5000)

# Possiamo ritornare l'ammontare
conto.balance
```

*Vogliamo rendere degli attributi NON accessibili dall'esterno:*

Per fare ciò basta mettere un **` _ `** prima della variabile da nascondere:
```python

class BankAccount:
	
	def __init__(self, initial_amount):
		self._balance = initial_amount
		
		
		
conto = BankAccount(5000)
```

In questo modo NON posso più fare `conto.balance` o `conto._balance`

La variabile NON è più accessibilie **sia il lettura che in scrittura**.

##### Setter
Esistono anche i setter che permottono delle **modifiche controllate**, non impediamo così la modifica ma la controlliamo.

```python
def set_balance(self, new_balance):
	pass
```

#### Programmazione con le classi
- **NON bisogna mai fare tutto sullo stesso file**, il main deve importare il file delle classi.
- Il nome del file della classe si scrive sempre col nome con la prima lettera maiuscola, es. Animal
- Quando si importa una libreria/classe propria **NON bisogna scrivere il nome dell'estensione**

#### Classi DERIVATE e MADRI
La **classe derivata prende gli attributi della classe madre.**

> La **classe derivata** è sempre **più piccola** di quella madre

Solitamente le classi derivate hanno lo stesso costruttore di quella madre.

**NB.** Vedi progetti lezione del 9 aprile 2022

**NB**. Importare sempre e solo le classi derivate, non le madri (poichè saranno già importate da quelle derivate)

### Attributi classe in SOLA LETTURA
**INCAPSULARE le variabili**: le posso gestire ma non modificare ciò che c'è all'interno.

Per fare ciò:
1. Definire privati gli attributi (con l' `_`)
2. Fare una funzione che mi ritorni il valore che io voglio, anche detti i **getter**

*Ecco un esempio:*
```python
def get_author(self):
	return self._author
```

### Scope
Lo **scope** è il pezzo di codice in cui variabili/funzioni/oggetti sono visibili dagli altri.

*Esempio:*
```python
class Persona
	braccia = 2


	def __init__(self, alt:int, e:int, n:str):
		self.altezza = alt
		self.eta = e
		self.nome = n
	
```

**Solo all'interno della classe è visibile "braccia"**. Per vedere lo scope dei vari elementi utilizziamo l'indentazione.

**NB**. *"alt" sarà visibile solo all'interno del costruttore*

### NameSpace
**Il name space della funzione "sleep" è "Persona".** "sleep" è posseduto da "Persona".
```python
class Persona
	braccia = 2


	def __init__(self, alt:int, e:int, n:str):
		self.altezza = alt
		self.eta = e
		self.nome = n
	
	def sleep(self, time):
		print(f"Ciao, {self.nome}, hai dormito per {time} ore")
		
		
# Chiamiamo la funzione
persona1.sleep(8)
		
```
<br>

### Classe PRIVATA
In questo modo l'intera classe non sarà accessibile al di fuori di essa.
Per fare ciò, come con gli attributi privati, utilizziamo l' `_`

```python
class _Persona
	braccia = 2


	def __init__(self, alt:int, e:int, n:str):
		self.altezza = alt
		self.eta = e
		self.nome = n
	
	def sleep(self, time):
		print(f"Ciao, {self.nome}, hai dormito per {time} ore")
```

### Importare una sola funzione da una classe
```python
turn_on_extern = Computer.turn_on()

# In questo modo mi copio la sola funzione "turn_on" della classe Computer
```

<br>

## Matrici
Anche detti **array 2 dimensioni**.
In alcuni linguaggi di programmazione sono così utilizzati che vengono gestiti molto meglio rispetto python.

In python non sono gestiti direttamente ma dobbiamo definirlo noi.
*array2d = [][] NON è accettato da python*

**Servono 2 indici per prendere un singolo elemeto di una matrice**
array_2d[2][1] , per prendere un elemento dalla matrice

**NB. Prima si dichiara la RIGA e poi la COLONNA**

```python
array2d = []

# Inserisco array all'interno della prima cella dell'array
array2d.append(['x', 'y', 'z'])
array2d.append('x', 'a', 'b')
```

Il risultato di sopra sarà:
['x', 'y', 'z']
['x', 'a, 'b']


## FORME CONTRATTE
**IF, versione estesa:**
```python
counter = 0
if bool:			# condizione
	counter += 1		# espressione 1
else:
	counter -= 1		# espressione 2

```

**IF, versione contratta:**
```python
espressione1 if condizione else espressione2

count += 1 if bool else counter -= 1
```

**NB**. Nel caso utilizzassimo la forma contratta **non possiamo non mettere l'ELSE** (che abbia una dichiarazione finita, NO operazioni)

---

**Array2d versione estesa:**
```python
for i in range(3):
	for j in range(3):
		array = []
		array.append(j)
		array2d.append(array)
```

**Array2d versione contratta:**
```python

espressione for i in <array> # (range, ...)

array2d = [[' ' for i in range(3)]]		# metto lo spazio vuoto per 3 volte
# Risultato: [[' ', ' ', ' ']]

array2d = [[' ' for i in range(3)] for i in range(3)]
# Risultato: [[' ', ' ', ' '], [' ', ' ', ' '], [' ', ' ', ' ']]
```


<br>

## Inner Classes, classi PRIVATE
**Inner Classes** = *classi all'interno di altre classi*. Che è **diverso da classi madri e figlie**

**Inner classes** sono delle classi dichiarate all'interno di altre classi in modo da poterle "rendere private"

Se definiamo la classe Account in questo modo, dal file NON main possiamo richiamare direttamente Account
```python
class Banca:
	def __init__(self):
		self.accounts = []		# collezione di account, 
	
class Account:
	pass

```

Per **"rendere la class Account privata"** devo:
```python
class Banca:
	def __init__(self):
		self.accounts = []		# collezione di account, 
	
	class Account:
		pass

```

Le **inner classes** vengono utilizzate molto nelle strutture dati, vedi *esercizio 2 - 20apr* 

## Classe Enumerazioni (Enum)
**Enumerazione**, nei linguaggi di programmazione ENUM è dichiarata come una struttura, in python è **dichiarata come classe in una libreria esterna** che si chiama **Enum** (= classe python)

```python
import enum

class Color(Enum):
	ORANGE = 1  # attributi
	BLU = 2
	RED = 3
	BLACK = 4
	
# Serve per rendere i nostri attributi delle variabili
Color.ORANGE

# Possiamo fare delle comparazioni
Color.BLACK.value < Color.BLU

# Possiamo ad un oggetto dargli il numero dell'ID
ogg_color = Color(2)
# Abbiamo così creato un oggetto colore di tipo BLU
```

- L'**enumerazione** è una sorta di variabile che prende dei valori che definiziamo noi all'interno di una classe.
- La classe ENUM ci permette di **specificare dei tag ad un ID** e **rendere i nostri attributi delle variabili**
- Possiamo anche utilizzare questo per l'importazione dei dati da JSON
- **È CONSIGLIATO FARE LA CLASSE ENUM IN UN FILE A PARTE**

![[vedi esercizio 23 apr]]

In questo modo posso craere un'unica classe "Oggetto generico" e **do il tipo tramite enumerazione**

## JSON
I file JSON sono file di testo **formattati**.
Tutto si basa su dizionari e array
Un file JSON dato non dovrebbe andare modificato

Il JSON è in un **file di testo formattato** viene utilizzato per la gestione dati, es. caricare/scaricare da internet. JSON è quindi una via di mezzo tra un testo e un linguaggio di programmazione.

Su Json tutto funziona tramite **array e dizionari**.

![[prendi file example.json della lezione 23 aprile]]

Il modo più pratico per formattare un JSON è quello di utilzzare la coppia **chiave - valore**.

```python
import json

json.dumps()  # permette di caricare in una variabile un testo json
```

- **È consigliato utilizzare sempre STRINGHE**
- Virgole per separare qualsiasi cosa
- Doppi punti per coppia chiave - valore

Per utilizzare il file json correttamente dobbiamo conoscere le chiavi,...

## Errori personalizzati
Creare degli errori personalizzati rende ancora più semplice la comprensione e l'utilizzo del nostro programma.

Per definirli dobbiamo utilizzare le classi. 
**NB**. Alla fine del nome della classe dobbiamo mettere "Error" per facilitare la comprensione
```python
class IDNumberError(ValueError):
	def __init__(self, *args: object):
		super().__init__(*args)

# Abbiamo creato una classe derivata di ValueError con tutte le proprietà di
# quest'ultima


# Lanciare l'errore
raise IDNumberError("ID non valido")

```


## Esportare in file json
```python
out.write(json.dumps(content))
```

La funzione **dumps** prende il dizionario e lo converte in stinga JSON

NB. Nel file di output "out" il contenuto però sarà in un unica stringa

*vedi esempio lezione 04 maggio 2022*

<br>

## LIbreria OS
*NB*. *Vedi lezione del 4 maggio 2022*

Mette a disposizione funzioni e variabili per interfacciarsi con il sistema operativo.

Una delle funzioni più utile è **system** che come parametro richiede un comando e lo esegue.

```python
import os

os.system("cls")
```

**NB**. Questi comandi sono dipendenti dal sistema operativo in cui stiamo operando, dobbiamo quindi **controllare in quale sistema operativo siamo**, per fare ciò utilizziamo la libreria **platform**

```python
import platform

print(platform.system())
# stampa il sistema operativo in cui siamo
```

**NB**. È possibile **importare un libreria anche all'interno di una singola funzione** e NON globalmente

#### Libreria Platform
Restituisce qualsiasi informazione tecnica del computer.

<br>

## Libreria: REQUESTS
Quando il nostro codice utilizza delle librerie esterne bisogna **specificarlo nei "requirments.txt"**.

REQUESTS è la libreria standard di python per **fare richieste web e scaricare il contenuto della pagina**. Come risultato potremmo avere:
- Codice HTML
- File JSON
- Byte code
- ...

```python
import requests

r = requests.get("https://www.google.com")
print(r.status_code)

# Ritorna 200 se il sito è on e accessibile

```

Altre funzioni di **requests**:
- **.content** --> Ritorna il codice della pagina, o nel caso (ad esempio) di una immagine, il suo bytecode.

**NB**. Con questo metodo è possibile scaricare qualsiasi immagine/documento/... presente su internet

**API KEY**: è la chiave che di identifica

Solitamente è buona cosa salvare l'API KEY in una variabile a inizio codice, e **darla come parametro**.

<br>

## Libreria: TKINTER
Questa libreria permette di creare **finestre con all'interno dei widget** (bottoni, box, checkbox, input type text, ...)

Per dare le posizioni dei widget:
- Funzione **place**, che chiede le coordinate dove posizionare il widget
- Posizionare tramite una **griglia**: si presuppone che la finestra sia divisa in righe e colonne

**NB**. Se non ci sono altri widget la grigia non viene costruita, quindi **meglio utilizzare .place**.

Per richiamare la funzione tramite un pulsante dobbiamo utilizzare il **puntatore, riferimento** di quest'ultima, quindi **non scriviamo le parentesi**.

*Esempio:*
```python
tk.Button(window, text="Close", command=exit).grid(row=2, column=5)
```

**NB**. L'angolo in alto-sx è 0,0

*Altri widget che possiamo utilizzare sono:*
- **LabelFrame** ->
- PhotoImage -> per caricare immagini
- Message -> per box con informazioni
- **Entry --> casella di testo**

I widget hanno una **discendenza** che di solito si definisce **padre - figlio**. Solitamente il padre controlla il figlio. Il figlio avrà un **posizionamento relazionare** rispetto al widget padre.

Per **espandere** i widget utilizziamo la funzione **pack()**:
*Prende il widget figlio e lo pacchetta all'interno il padre, seguendo delle specifiche*

```python
label = tk.Label(window, text="Label di prova", bg="black", fg="white")  
# conviene usare enumerazione: Color.BLACK
label.pack(expand=True)

# in questo modo occuperà tutto lo spazio della finestra, senza però riempirlo
```

- Una **LIST BOX** è una lista grafica, simile ad un array.
- Il widget **FRAME** viene utilizzato per raggruppare gli oggetti

Le **sezioni** di un **MENU** sono degli **altri menu** con il **menu principale come Padre**