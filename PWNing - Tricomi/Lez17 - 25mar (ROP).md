#  Return Oriented Programming
<br>

## A PWN mitigation
La memoria può essere settata con dei permessi, es. WRITE+EXECUTE, per cui il buffer non può essere scrivibile ed eseguibile allo stesso momento.

Se c'è questa mitigation non possiamo fare molto.

NB. In questo caso NON possiamo andare a richiamare una shellcode come abbiamo visto nelle lezioni precedenti

## Bypassing
Possiamo utilizzare del codice già scritto nel programma. 
*Ritagliamo pezzi di codice e li concateniamo insieme.*

## Code reuse
L'idea è quella di isolare dei pezzi di codice che andremo a chiamare **GADGETS**, che devono essere **piccoli** e **concatenati tra di loro** (= l'uno richiama l'altro).

L'idea è quella di prendere dei gadgets che **finiscono sempre con una funzione RET**.

*Noi finora abbiamo solamente sovrascritto un tot del buffer fino ad arrivare al return point.*

Possiamo invece: inserire del padding, inserire i gadget.

## ROP Chain Example
*Obiettivo: spawnare una shell*

IDEA: andiamo giù nello stack sovrascrivendo con ciò che vogliamo.

1. Il primo gadget è il primo indirizzo di ritorno. Pop rax prendere quello che c'è nello stack e lo mette su rax (es. indirizzo scrivibile)
2. Inseriamo rax e la stringa per la shell
3. Secondo gadget: andare a scrivere all'indirizzo la stringa /bin/sh
4. Terzo gadget: **pop rdi**.
5. Ora andiamo a chiamare system.

**Il return ci permette di scendere al gadget successivo**.

NB. **RDI** è il primo registro che viene utilizzato per passare i parametri delle funzioni
**NB**. **Return è un puntatore da 8byte**

*Leggi i paper linkati sulle slide*

## Esercizi
NB. Quando la funzione MOVAPS viene chiamata lo stack pointer deve terminare con 0, se quindi il programma crasha ma pensiamo che la chain sia giusta dobbiamo **allineare manualmente lo stack**:
Possiamo quindi un gadget che semplicemente faccia il return (cioè scenda a quello dopo), facendo così stiamo aggiungendo 8byte alla nostra catena.

## Come trovare i gadgets?
**ropgadget** --binary [nome_programma] | grep "rax"

Altri tool possono essere **ropper** o **pwntools rop**,...