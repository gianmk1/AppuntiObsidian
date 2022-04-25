# Lesson 13: Debugging
Il debugging è nato come un tool per ispezionare qualsiasi processo.

*Ad un certo punto i programmi iniziano a fare cose diverse di quelle che pensavano, bisogna analizzare quindi i vari stati di un programma.*

Utile anche per **trovare vulnerabilità e sfruttarle**.

Conseguenza: sviluppare delle tecniche per capire se un determinato programma sta venendo debuggato o meno (anti-debugger), in questo caso, nella fase in cui monitorato, potrebbe simulare di fare qualcos'altro.

*http://www.alexonlinux.com/how-debugger-works*

### Come funziona un debugger?
![[schema riassuntivo]]


**Un programma può essere debuggato soltanto da un altro processo.**

GDB (debugger) è un processo che può controllare più programmi allo stesso tempo, spawnare nuovi processi o attaccarsi a processi già esistenti.

### ptrace()
È una chiamata di sistema che ci permette di ispezionare qualsiasi tipo di programma.

signature:
che cosa vogliamo fare esattamente con ptrace()

ptrace ritorna un valore che ci dice se il debugging ha funzionato o meno (-1 se qualcosa è andato storto)

### Come funziona GDB?
![[schema gdb]]
![[schema gdb 2]]
![[schema gdb 3]]

**NB**. Nel kernel c'è un registro in cui vengono salvati dei segnali inviati da e verso il kernel.


**BREAKPOINT** è un'istruzione CC messa all'interno del codice assembly. Richiama il debugger.

Una delle tattiche di anti-debug di un malware potrebbe essere quella di inserire dei CC all'interno del codice per evitare che il debugging funzioni correttamente.

### Recap
- Un debugger può fare debugging di più processi
- Un debuggato può essere controllato da un solo debug per volta
- i Breakpoint sono dei **0xCC** inseriti all'interno del debuggato

**NB**. Il CC ferma temporaneamete l'esecuzione di un programma.
<br>

## Anti-debugging
Sono delle tecniche per cercare di capire se il programma sta venendo debuggato.

### Chiamata ptrace()
Un processo debuggato può essere debuggato da qualsiasi processo (non solo GDB).

Quindi possiamo invocare ptrace su noi stessi, se c'è qualcuno che sta cercando di debuggare, si troverà il programma già in fase di debugging (e il suo debugger ritornerà -1)

**NB**. Per disabilitare ciò dobbiamo fare **analisi-statica**, trovare il ptrace() e rimuoverlo.

### GDB env variable
Alcune versioni di GDB quando vengono avviate, settano delle variabili d'ambiente. Queste permettono al nostro programma di capire se c'è qualcuno che sta cercando di debuggare.

### GDB heap relocated
...
...

### GDB no-ASLR
Si può andare a controllare se alcune librerie sono state inseriti in indirizzi noti che utilizza GDB

### Who is my parent?
Controllando il nome del processo padre possiamo capire se siamo in una situazione di debugging

### VSDO
...
...
<br>

## Come possiamo rimuovere queste tecniche di debug?
- BIsogna cercare queste tecniche di debug (**ptrace**, **0xCC**, **getenv()**): NON solo sul main ma su **.init**, **.fini**, **_start**.
- Una volta trovate usiamo hex editor o radare per patchare
<br>

## DEMO
- **gdb [nome-programma]**
- **run** per far partire il programma
- **disas [nome-funzione]**, per andare a vedere la funzione e i vari indirizzi (che sono diversi dal binary), per mettere un breakpoint possiamo utilizzare questi indirizzi
- **b*[indirizzo-breakpoint]** per inserire un breakpoint
- **c** per continuare l'esecuzione del programma
- **jump [nome-funzione]**, per saltare alla funzione scelta
- **b [nome-funzione]**, per mettere un breakpoint in una specifica funzione
- **x $[registro]**, per mostrare a che indirizzo punta
- **x/s $[registro]** per mostrare **in modalità stringa** quello che punta l'indirizzo

NB. Mettendo un breakpoint riusciamo a capire cosa sta succedendo nei registri / stack in quel momento
NB. Installare **GDB Peda**, che da degli strumenti in più
NB. Anche con IDA possiamo inserire breakpoint e debuggare

#### Le fasi ordinate
1. Mettere breakpoint al main
2. Runnare il programma
3. Guardare gli indirizzi
4. Mettere i breakpoint dove vogliamo


### Alcuni comandi:
**print (char*) [nome-variabile]**, per fare il cast su una variabile e stamparla