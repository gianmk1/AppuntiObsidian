# Lez 17 maggio - Python in azienda

## Intro
Applicazioni aziendali dove python è utile:
- Data Analytics & Machine Learning
- Dashboard
- Data Engineering
- Alert
- Automazione
- IOT con MicroPython
- Applicazioni Web / Locali

I for in python **sono abbastanza inefficienti**: se abbiamo un for con più di 1000 interazioni stiamo sbagliando qualcosa. 

## List Comprehension

## LAMBDA
Cioè una funzione definita senza nome
```python
somma_2 = lambda x: x + 2

# O in versione standard
def somma_2(x):
	return x + 2
```

## Sorgenti DATI
I dati possono provenire da:
- **Database**
- **Rest API**
- **File**:
	- **JSON**, tipi delle REST Api
	- **PICKLE**, file binari che rappresentano qualsiasi oggetto in Python. In questo possiamo salvare anche un'oggetto di una classe.
	- **CSV**, file per salvare dati tabulari

[Kaggle](https://www.kaggle.com/) - mette a disposizioni una serie di **dataset** per l'apprendimento

Un file **CSV** è un file di testo in cui le **colonne sono separate dalla virgole** e le **righe sono separate dagli a capo**.

## Libreria PANDAS
È una delle librerie principali per la manipolazione di dati.

*Vedi lezione del 17 maggio 2022*

```python
# Per importare un file CSV
passeggeri = pandas.read_csv("train.csv")
```

Pandas è così diffuso poichè è stata scritta una documentazione molto ricca e semplice da leggere.

**DataFrame** è una rappresentazione del database. I dataframe hanno una serie di metodi per semplificare le operazioni sui dati.

##### Quali sono le azioni base che si fanno su un DB?
SELECT -> da sola seleziona le colonne, le **condizioni stringono le righe**, il **group by** invece ...

**NB1**. Il **group by** per categoria crea una struttura temporanea a cui poi esegue una specifica funzione. 

![[vedi screenshoot 1 group by]]

**NB2**. Il **windowing**, che può essere **rolling** che effettua un group by scorrendo le linee del dataset, o **expanding** dove una si utilizza una **expanding window**.

![[vedi screenshoot 2]]

#### Alcune JOIN
Quando mettiamo insieme 2 tabella, dobbiamo specificare delle condizioni. In una delle 2 tabella potrebbe non esserci il **campo che fa da ponte** tra le 2. 

**LEFT** JOIN -> prendo tutte le righe della tabella sx (anche quelle che non hanno il ponte con la dx), quindi ci saranno dei campi nulli
**RIGHT** JOIN -> viceversa
**INNER** JOIN -> prendo solo gli elementi (righe) che hanno il **campo ponte** in comune tra le 2 tabelle
**OUTER** JOIN -> prende TUTTE le righe, che abbiano o meno valorizzato il campo che fa da ponte

Le colonne della tabella in cui non ci sono riferimenti saranno **NaN**

<br>

Una **MASCHERA** è una condizione di True o False