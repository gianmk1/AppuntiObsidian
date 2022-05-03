# Introduzione a Reverse Engineering
Nella **reverse engineering** abbiamo un programma, sappiamo che fa alcune cose ma non nello specifico e non chi e come è stato creato, dobbiamo "tornare indietro" per capire come funziona effettivamente il programma.

Alcune motivazioni per fare ciò:
- analizzare un software proprietario
- studiare le vulnerabilità di un software
- c'è una scarsa documentazione del software

### Reversing in CTFs
Capire come funziona il codice sorgente da un programma che ci verrà dato.

NB. può esserci dell'**offuscamento del codice** che rende più difficile capire il funzionamento del programma.

### Reversing in Real Life
- **Analizzare malware**, rimuovere Ransomware
- Ottenere licenze gratuite da software proprietari
- ...

## Compilatore
Da un sorce code, attraverso un compiler otteniamo un codice binario

## Reversing software
Tornare indietro dalle istruzioni 0/1 al source code

Solitamente però da 0-1 si passa ad **assembly** e da questo ritornare al source code.

## Il ciclo di vita di un programma
1. Si parte dal **source code**
2. Un **compilatore** dal source code produce un **object code**
3. Un **linker prende le librerie "statiche"e le va unire al codice sorgente** (importa negli eseguibili)
4. Viene prodotto l'**eseguibile**
5. Vengono **importate**, eventualmente, **dinamicamente delle altre librerie**
6. Inizia il **processo**

La parte di compiler e linker ci fanno perdere il source code.

## Analisi
**1. STATICA**: **senza** eseguire il programma
**2. DINAMICA**: quando si esegue il programma attraverso il **debugger**

## Eseguibili
Gli eseguibili hanno formati specifici per i vari sistemi operativi.
PE -> Windows
ELF -> Linux
Mach-O -> MacOS

GLi eseguibili sono formati da diverse sezioni:
- **text**
- dove salvati i dati NON inizializzati
- ...

Gli eseguibili possono essere caricati in memoria tramite vari metodi: con indirizzi definiti, con indirizzi randomici,...

## Executable and Linkable Format (ELF)
**È il formato principale degli eseguibili di Linux.**

- Program header: descrive i vari segmenti del programma
- Section header: ci dice dove sono i segmenti del programma e come devono essere caricati in memoria

## Disassembler
Il compito di un disassembler è quello di partire da un codice binario per tornare a **assembly**.

NB. Alcuni tool consigliati sono **IDA**, **Radare2** e **Ghidra**.

## HEX editor
È un programma che apre qualsiasi tipo di file e lo mostra il codice esadecimale.

NB. Alcuni tool sono **bless**, **hexedit**, **biew**.

## Alcuni comandi linux
- **file** fa capire che tipo di file è e come è stato compilato, ecc.
- **strings** da una lista di tutte le stringhe che vengono trovate all'interno di un programma
- **gbd** (è un debugger)

## Decompilers
Portano direttamente dal codice binario a quello sorgente, molto spesso però potrebbe dare degli errori. Molte poi è consigliabile lavorare direttamente a livello di assembly, e il decompiler ci porta a un *livello molto alto*.