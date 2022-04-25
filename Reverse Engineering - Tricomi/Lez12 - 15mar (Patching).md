# Lesson 12: Patching
**Patching**: modificare i byte di un programma

*Perchè ci serve?*
- Per fixare qualche bug
- Per cambiare il flow del programma

**NB**. Molto spesso non abbiamo il codice sorgente e quindi dobbiamo modificare l'eseguibile

##### Fase 1
È importante **capire cosa il programma sta facendo**.

NB. **Patching** è diverso da **Instrumentation** (prendere un programma e quando lo si esegue aggiungere nostre istruzioni)

### Come funziona?
Col patching, in questo caso, vogliamo modificare quell'IF, in modo che se a è diverso da ok: andiamo alla funzione A

### Cosa usiamo?
Vari tools:
- IDA Pro
- Binja
- **Ghidra** (gratis ma non funziona)
- **Hex editor**
- **Radare 2** 

### Strategia per patchare
1. Creare una copia del binary (prima di ogni patch)
2. Usare un **disassembly** per trovare le istruzioni da patchare
3. **Trovare l'istruzione, si trovano i corrispettivi byte all'interno del programma**
4. Si cambiano i byte e si salva
5. Si runna il programma

**NB**. *Link delle istruzioni binary*

### Per fare il punto 3 sopra?
1. Utilizzare l'hex di IDA (cliccando l'istruzione) per trovare i byte corrispettivi e poi trovarli in un hex editor

2. Quando carichiamo il programma in memoria, **calcoliamo il Relative Virtual Address** (*vedi link*)

NB. I byte all'interno del bunary solitamente sono codificati in Little Endian

### Strategia su Radare 2
1. Fare una copia del binary
2. Aprirlo in write mode
3. Lanciare le analisi
4. Cercare la funzione da patchare
5. Stampare la funzione disassemblata
6. Andare all'indirizzo da patchare
7. Patchare usando l'istruzione "wa"
8. Ricaricare il binary e verificare


### Cosa possiamo fare?
- **Utilizzare i NOP** per eliminare alcune istruzioni / set di registri / ... , mettendo più NOP di quanti l'istruzione ne prenda. Quando si "noppa un istruzione" bisogna riempire tutti i byte (es. nella call 5 byte)

**NB**. Per eliminare qualcosa utilizziamo sempre i NOP

- Invertire i branches (JE <-> JNE)
- Rimuovere i branches (NOP / JMP)
- Cambiare alcune costanti
- **Inserire nuove funzioni all'interno del binary** (prima bisogna scriverla in assembly poi convertirla in binario, trovare un punto vuoto nel binary, aggiungere la funzione, chiamarla, sostituendo alcune istruzioni... in pratica si cerca di **modificare il flow** del programma)

### DEMO 1_hello_world

NB. Importante impostare l'hex editor con visualizzazione "singolo byte"

JNZ fa un jump **short** all'indirizzo **994** (cioè **0C**)

JNZ è la stessa cosa di  "jump not equal"


**NB**. Importante fare attenzione a **SOSTITUIRE i byte** e **NON aggiungere byte**.