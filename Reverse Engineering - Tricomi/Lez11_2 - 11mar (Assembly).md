# Assembly
## Introduzione a x86(64) ASM
L'archittettura dei nostri computer è x86_64 (32 o 64bit)

## Memoria di un processo in linux
In memoria viene prima di tutto caricato l'eseguibile, cui ha diverse sezioni:
- TEXT : il codice
- PIT
- RODATA : dati in sola lettura
- GOT
- DATA: dati in lettura/scrittura

![[memory.png]]

**RIP** è un'area di memoria in cui si ha accesso in mamiera più o meno regolare

R --> 8 byte
E --> 4 byte

**STACK** è invece controllato direttamente dal processore è ha un **struttura molto rigida**, l'**ultima cosa ad essere inserità sarà l'ultima cosa ad essere tolta**. Si parte dal basso e si continua verso l'alto.

NB. **Lo STACK cresce AL CONTRARIO di come crescono gli indirizzi di memoria.**

La CPU lavora con **REGISTRI** che sono le **variabili del processore**.

## Registri
![[registers.png]]

Ci sono diversi tipi di registri:
- **general porpuse** : utilizzati per qualsiasi cosa, in un'architettura 64bit i registri sono grandi 64bit 
- **stack pointer**: RSP ha al suo interno l'indirizzo dell'ultimo stack utilizzato
- **base pointer**: ci dice dove è collocata la funzione
- **instruction ptr**

## Alcune istruzioni
**NB**. Il **primo operando è la destinazione** della nostra operazione e il **secondo è la sorgente**.

**MOV**
es. MOV EAX = EBX ---> EAX = EBX

es. MOV EAX, [ESP + 4] ----> EAX = *(ESP + 4) stiamo dando a EAX il valore salvato all'indirizzo 1004 (se ESP è uguale a 1000)

**LEA**, carica effettivamente l'indirizzo della sorgente. Viene utilizzato soprattutto per accedere agli array

**PUSH**, operazione che mette qualcosa in cima allo stack.

**POP**, prende un valore dello stack e lo va a mettere in un registro di destinazione che vogliamo noi. Esegue l'operazione inversa del PUSH

*esempio* 
PUSH EAX , 
POP EBX  =

MOV EBX, EAX

**ADD**, fa un'addizione
esempio
ADD ESP, 0x10 --> stiamo rimuovendo 16 byte dallo stack di memoria

**SUB**, da una sottrazione

### Le FLAGS
ZF = viene settata quando il risultato di un'operazione è UGUALE a 0
SF = viene settata quando il risultato di un'operazione è MINORE di 0


<br>
<br>

**CMP**, sta per *compare*, viene fatta una sottrazione il cui viene tolto il risultato. Il compare setta la ZF se i due valori, destination e source sono uguali.
Viene settata una variabile temporanea per il risultato.

**JUMP** va a saltare all'indirizzo cui li diamo.

#### JUMP condizionali
Prima di fare un JUMP devono essere soddisfatte alcune condizioni.
es. controllare se un valore è > di 0

- **JZ/JE** il jump funziona solo se ZF = 1
- **JNZ/JNE** il jump funziona solo se ZF = 0
- **JB, JA** ...

#### Esempio
*Vogliamo controllare se la lunghezza di una password è uguale a 16.*

MOV RAX, password_lenght
CMP RAX, 0x10
JZ ok
JMP exit
ok:
...print 'la lunghezza è corretta'...

**XOR**, esegue lo XOR bit a bit tra la source e la destination

**CALL**, ha un unico parametro che indentifica la destinazione cui noi vogliamo andare a chiamare.
per richiamare una funzione in ASM quindi facciamo un CALL all'indirizzo della funzione
Quando voglio chiamare un funzione con dei parametri la situazione si complica

**RET**, sta per **return** ed è l'opposto di call. La funzione dovrebbe sempre terminare con un RET. 

#### Come si passano i parametri di funzione?
Nel caso di 32bit i parametri vengono passati sullo STACK
Nel caso di 64bit alcuni parametri vengono caricati nei registri e alcuni nello STACK

## Calling Convention - SystemV AMD64
Nel 64bit ci sono **6 registri che in ordine vengono utilizzati per portare gli argomenti all'interno di una funzione**. (rdi, rsi, rdx, rcx, r8, r9)

Quando stiamo chiamando una funzione in ASM bisogna subito andare a vedere se qualcuno di questi indirizzi sta venendo inizializzato.

NB. Ogni funzione ha il suo base point che dice dov'è lo "spazio vitale" della funzione nello stack point.

**RAX** è il registro che **contiene i valori di ritorno di una funzione**.

**NOP**, quando un processore vede l'istruzione NOP questo non fa nulla e va avanti.
È un'istruzione molto utile per patchare un programma. Con il NOP possiamo cancellare qualsiasi CALL, CMP, ... all'interno del programma.