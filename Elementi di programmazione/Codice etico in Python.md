# Codice Etico in Python
Sono regole non scritte per scrivere un codice in Python. Mettiamo delle regole perchè il codice deve sempre essere facilmente comprensibile.

1. Il codice si scrive sempre in **lingua inglese** (comprese variabili, ecc.)
2. I nomi delle variabili devono essere coerenti alla funzione
3. Le variabili si scrivono **sempre in minuscolo**
4. Le costanti in python non esistono, per cui si dichiarano come variabili ma **tutto in maiuscolo**, es. *PI = 3.1415 o PI_GRECO=3.14.15*
5. Se il nome di una variabile contiene nomi:
	- *esempioVariabile = " "* (**Camel Cased**)
	- *esempio_variabile = " "*
6. Una variabile NON si scrive mai *Valore = ""*
7. Le **classi** si scrivono così *Valore = ""*
8. Le **funzioni** riprendono le regole della varibili
9. Solitamente si scrive **1 riga di commenti ogni 3 di codice**
10. Le linee di codice devono essere abbastanza corte
11. Bisognerebbe mettere sempre lo stesso tipo di dati all'interno dell'array. Nel caso lo si faccia bisogna specificare tramite commento che tipi contiene l'array
12. **NON scrivere mai lettere accentate, ANCHE NEI COMMENTI**

<br>
<br>
<br>

# Alcuni suggerimenti
## Come generare numeri casuali?
```python
import random

# random.randint , genera un numero intero
# random.shuffle , genera dei numeri random e li mescola
# random.uniform , genera dei numeri (entro intervallo) ma vicini tra di loro

random.randomint(0, 100)
# genera numero interno da 0 a 100
```