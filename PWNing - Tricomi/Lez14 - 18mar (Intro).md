# Intro to PWNING
**PWN?** 
Si intende prendere il controllo di una macchina/programma.

**Cos'è la memory corruption?**
Si cerca di modificare la memoria di un programma/processo, l'idea è quella che, se riusciamo a prendere controllo della memoria, riusciamo a prendere il controllo dell'interno processo.

**Alcuni esempi:**
- **Morris (1988)**, primo worm virus, questo programma prendeva una lista di nodi da ciscun computer, si trasformò in un DOS che blocco tutta la rete internet
- **Root dei dispositivi (Unlocking device)**, le custom ROM permettono di avere privilegi di root nel telefono, si cercano delle vulnerabilità per sovrascrivere quei byte che esplicitano se siamo o meno root
- **Per attaccare servizi remoti**

### Memory corruption vulnerability

NB. Buffer è un'area di memoria che noi designiamo per un input dell'utente, che però non andiamo a controllare, di conseguenza possiamo ad andare a scrivere più byte di quanti "richiesti", sovrascrivendo così il codice

- **BUFFER OVERFLOW**
- **OUT-Of-BOUNDS ACCESSES**
- ...
- ...

### Memory corruption: TIPOLOGIE
1. Viene modificato lo stato della memoria, ma **NON SI CAMBIA IL FLOW DEL PROGRAMMA**
2. Si va effettivamente a **MODIFICARE IL FLOW DEL PROGRAMMA**, si possono chiamare funzioni che normalmente non verrebbero chiamate

### 1 step: EXPLOITATION
Trovare dei punti del programma per cui, se facciamo qualcosa di strano, questo crasha (**segmentation fault**). Da semplice vulnerabilità diventa un exploit

### MEMORIA
**La memoria è una sequenza PIATTA di byte**. All'interno della memoria non c'è scritto nulla per quanto riguarda la lunghezza degli array, tipi,...

Alcuni meccanismi per proteggere la memoria come definire l'area di memoria in sola lettura

**Ogni byte di memoria è identificato con un INDIRIZZO**.

### Little Endian Byte Order
Il byte meno significativo è posto nel byte col numero minore di indirizzo.

*78 56 34 12 <---> 0x12345678*


### a (linux) process memory
- **Eseguibile**, definito in varie sezioni (**.text**, **.pit**, **.data**, **.bss** )
- **Librerie** esterne
- **Heap**, area di memoria in **allocazione dinamica**
- **Stack**, area di memoria **molto più rigida**

**NB**. Lo **stack cresce al CONTRARIO**.


### Buffer overflow
Alcuni linguaggi come C e C++ NON vengono controllati automaticamente i bound di un buffer. (python non ha queste vulnerabilità, tranne per alcune librerie che sono scritte in C)

Se il programmatore non controlla queste vulnerabilità, un hacker potrebbe sfruttarla.

![[immagine esempio buffer flow]]

Area rosa: il nostro buffer

*Se inseriamo 20 byte non ci sono problemi, se ne inseriamo 40 invece andiamo a sovrascrivere un'area di memoria.*


NB. **"A" in esadecimale è 41**

Nel buffer overflow dobbiamo:
1. Cercare di capire quanto grande è il buffer
2. Provare a riempirlo tutto con spazzatura
3. Andare a inserire le informazioni che vogliamo

### Exercise 1
Andiamo a commentare la parte di codice che dovrebbe controllare la password inserita.

Quando vengono definite le aree in memoria (stack cresce al contrario, come una pila di libri): quando definiamo auth_flag le designiamo un po' di posto

Se andiamo a fare un overflow dell password possiamo andare a modificare anche l'auth_flag

![[immagine slide_2 dell'ex 1]]

NB. **Allineamento del programma**: il compilatore funziona meglio quando le istruzioni sono posizionate in particolari indirizzi (in base all'architettura) sono multipli di 4 / 8 byte

*L'area rosa è la spaziatura aggiunta dal compilatore per fare l'allinemento*


NB. **In C tutto ciò che NON è zero viene considerato VERO**, questa è una grande vulnerabilità

## Tools
- IDA (per disassembler)
- Radare 2 (per disassembler)
- GDB + Peda (peda da delle informazioni della memoria)
- **pwn tools (python)**, ci da accesso ad un set di istruzioni che ci permettono di interagire con il nostro binary: possiamo dare input, leggere ciò che ci torna, possiamo automatizzare, ...

*vedi link utilii sulle slide*

## DEMO


**NB**. 
- **ALLOCAZIONE**: come una pila di libri (dal basso verso l'alto)
- **SCRITTURA**: la scrittura nello stack però è verso il basso (all'interno dello spazio allocato)

**NB**. Il buffer overflow 

NB. [rbp - 4] : la prima variabile (si parte dal base point e si tolgono 4byte).

RBP è L'indrizzo del base pointer della funzione. Ogni variabile viene definita dal base point in poi (in poi = tornare indietro)

Il computer per ricorsarsi dove sono salvate le variabili parte dal base pointer e torna indietro

## Esercizio 3
se scegliamo "java" la chiamata NON viene sovrascritta, mentre con gli altri linguaggi si.

Facciamo jumpare il flow alla funzione con indirizzo 0x04007A2

Ora dobbiamo capire quant'è la dimensione del buffer (32), dobbiamo mettere i primi 4 byte a "java" , poi diamo un tot di garbage (28 caratteri) fino ad arrivare a call e qui mettiamo l'indirizzo (**tradotto in Little Endian**)

La funzione p64 converte la in Little Endian a 64bit

NB. Utilizziamo le stringhe in byte