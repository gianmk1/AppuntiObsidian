# Shellcode
**STACK OVERFLOW**

Sullo stack c'è tutto ciò che server al nostro programma per essere runnato correttamente: funzioni, flow del programma

## x86 stack
Quando andiamo a chiamare **foo**:
- push
- salvare base pointer (BP)
- salvare le variabili (locals)

BP punta all'inizio dei local, molto spesso il BP viene utilizzato per accedere alle variabili. *es. BP - 4*

SP (stack pointer) punta all'inizio dello stack

Se andiamo a chiamare un'altra funzione **bar**:
- *...stesso procedimento visto sopra...*

Queste funzioni (insieme al BP e locals) definiscono sullo stack 2: **STACK FRAME**.

> *A noi interessa sovrascrivere il **return address**. Il base pointer non da molti problemi (anche se messo a caso), il return address invece se gli mettiamo qualcosa a caso fa crashare il programma.*

## Stack overflow: example
![[immagine esempio slide]]
Se mettiamo 46 A maiuscole: **andiamo a sovrascrivere il return address.**

Questo è il **metodo più utilizzato per CAMBIARE IL FLOW DEL PROGRAMMA**.

## Shellcode
SHELLCODE è un termine per dire **codice che spawna una shell**.

Noi vogliamo iniettare il nostro codice e richiamarlo attraverso l'indirizzo di ritorno.

#### Esempio
![[immagine di esempio]]

Possiamo scrivere dentro al buffer del codice assembly e nel return address mettere l'indirizzo del buffer (sopra), così da, ad esempio, spawnare una shell.

**La sezione in rosso è il PADDING.**

*Una volta aperta la shell NON ci interessa più del programma, questo può anche crashare.*

## Mitigation
- **Inserire delle STACK CANARIES**, inserite dal programmatore: se determinati codici in determinate posizioni non vengono ritrovati il programma si chiude
- Write Execute, si va a flaggare la memoria come scrivibile o leggibile ma non entrambi, la shell in questo caso diventa inutile. Per questo bisogna andare a prendere funzioni già presenti all'interno del programma

## Come trovare lo spazio dall'inizio del buffer e l'indirizzo di ritorno?
- **pattern_create [size] [nome_file]**
- **pattern_search**, con gdb peda ci dice dov'è andato il nostro pattern all'interno del programma

In questo modo sappiamo esattamente dove siamo arrivati dal messaggio di partenza.

***Sequenza dei comandi:***
1. gdb [nome_programma]
2. pattern_create 200 [file_output]
3. run < [file_output]
4. pattern_search

Qui possiamo vedere dove crasha il programma la dimensione del basepoint, del buffer ec.

## Alcune reverse shell 32bit x86
- http://shell-storm.org/shellcode/files/shellcode-585.php (25byte)
- http://shell-storm.org/shellcode/files/shellcode-851.php (30byte)