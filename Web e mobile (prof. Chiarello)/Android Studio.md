# Android Studio

Un' **ACTIVITY è una pagina**, cioè una schermata di un'app.

Si parte dal layout, poichè il nostro leyout della schermata è l'**input e output**.

L'activity è tutta scritta in XML
Il movimento e le azioni è fatto in JAVA

La **VIEW** è qualsiasi oggetto che mettiamo nel layout (es. text box , bottone , immagine , ...)

Il layout è come io metto gli oggetti nella schermata:
- constraint layout
- linear layout : in orizzontale o verticale
- table layout : organizza in tabella

Devo definire prima il **constraint layout** (lato to lato)

Ogni oggetto ha tante proprietà che vengono definite nel file XML

Nel nome, **@+** identifica che questo oggetto lo si va a prendere nelle risorse

### Esercizio CALCOLATRICE
File importanti:
- mainactivity.java
- activity_main.xml
- string.xml : qui vado a definire tutte le varibili di tipo stringa, Android da errore se vado a dichiarare direttamente la stringa all'interno dell'oggetto


Quando si definisce un layout bisogna definire i nomi degli oggetti e il loro **TIPO**

**AndroidManifest.xml** è come l'index, rappresenta la prima activity

Dobbiamo usare variabili:
- di **lavoro**, cioè quelle che utilizziamo
- **collegate agli oggetti**, quelle che prendolo l'oggetto del layout