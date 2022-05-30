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

Per gestire i dati di una rubrica non è conveniente utilizzare una lista di liste poichè tramite **dizionario possiamo richiamare la chiave** quindi è una questione di **comodità**, (quindi una **LISTA DI DIZIONARI**)

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

L'**analytics** è uno dei campi fondamentali in python

# Lez 24 maggio
#### Canali Youtube validi
- **corey schafer** -> Python, Pandas, Matplotlib, Django
- **socratica** -> Python, SQL
- **ThreeBlueOneBrown** -> Statistica, Matematica, Algebra lineare
- **StatQuest** -> Machine Learning

## Intelligenza artificiale
Nell'**intelligenza artificiale** noi cerchiamo di fare imparare alle macchine **tramite la statistica**. Tipicamente ci sono 3 ambiti nel machine learning:
- **Classificazione**, da degli esempi viene data un etichetta
- **Regressione**, prevedere dei valori continui
- **Clustering**, anche detto apprendimento NON supervisionato, questo si utilizza quando non abbiamo a disposizione degli esempi con soluzione

**NB**. Una macchina può memorizzare o può apprendere.

## continuazione di Pandas
I 2 oggetti principali di Pandas sono:
- **DATAFRAME**,  è una rappresentazione del database. I dataframe hanno una serie di metodi per semplificare le operazioni sui dati.
- **SERIE**

Il problema di quando si utilizzano delle librerie è che bisogna **impararle**, per fare questo è consigliato **leggere la documentazione**.

[Pandas - guida](https://pandas.pydata.org/docs/user_guide/index.html#user-guide)

##### Variabile categorica VS continua
La variabile **CATEGORIA** sono delle categorie, nel machine learning qualcosa appartiene ad una categoria ma tra di loro non sono ordinate.

Le variabili **CONTINUE** invece possono essere ad esempio 2021, 2022, 2023 cioè **ordinabili**. Le variabili continue possono essere o meno numeriche (come quelle categoriche).

**NB**. Le variabili booleane sono categoriche.

<br>

*vedi esericizi del 24 maggio 2022*

Gli **attributi principali di un oggetto dataframe** sono l'**INDICE** e le **COLONNE**.

**Pandas** è ottimizzato per le **operazioni vettorializzate** quindi non c'è bisogno di utilizzare i **FOR** poichè lenti e dispendiosi di risorse.

**setindex()** serve a sovrascrivere l'indice predefinito della tabella con uno da noi assegnato

**NB**. **Nan** = **valore mancante**

### Grafici
Molto spesso abbiamo la necessità di rappresentare dei dati, per fare ciò dobbiamo presentare i dati nel modo più semplice / diretto possibile, utilizzando quindi **grafici**.

È fondamentale **scegliere il tipo di grafico** più adatto allo scopo.

**NB**. La **gaussiana** è una distribuzione teorica caratteristica di un evento casuale.

Per prima cosa dobbiamo importare il modulo **pyplot** dalla libreria **matplotlib**.
Noi useremo l'usage pattern **Object-oriented API** (cioè quello orientato agli oggetti).

L'oggetto base di matplotlib è la **FIGURE** che è un oggetto contenitore, all'interno di questo sono presenti altri oggetti come **axis**,...

##### pyploy.subplots
**pyplot.subplots** è la funzione base che permette di creare la figura, questa permette di creare più **plot** nella stessa figura.
Nella stessa figura possiamo **metterci più grafici**, creando quindi una **matrice di grafici**.

Le **axs sono le aree di disegno** dove andiamo a fare i grafici veri e propri.

**Squeeze = False** ???

Per fare un **grafico a barre** dobbiamo utilizzare il metodo **.bar()** di **ax**.

[Metodi di Axes](https://matplotlib.org/stable/api/axes_api.html#id5)

Per selezionare tramite indice:
frazione_sopravvissuti_classe.loc[indice]

<br>
<br>

## Backend con Python
