# GOT hijacking
<br>

## PLT & GOT
L'idea è quella di abusare del dynamic linking: se con alcune vulnerabilità siamo in grado di scrivere in aree di memoria, qui possiamo andare a sfruttare il funzionamento del dynamic linking

## Ciclo di un programma
1. Codice sorgente
2. Compilazione
3. 1o link delle librerie STATICHE
4. Il dynamic linker si occupa di importare le funzioni già installate nelle nostre macchine, il dynamic linker prendere queste librerie e le carica in memoria

## Linking dinamico
C'è una tabella all'interno del binary chiamata **GOT**, dove sono salvate delle funzioni.

All'inizio NON sappiamo dove si trovano queste funzioni in memoria, si tiene traccia di dove sono le varie libreria tramite la **GOT**.
In questo modo ogni volta che andiamo a chiamare un libreria avverrà un jump all'indirizzo della libreria

## GOT in Ida Freeware e PLT
Sulla sinistra c'è l'offset (in blu) della got e a destra c'è la funzione effettivamente chiamata (in rosa).

Prima di arrivare alla tabella got abbiamo un'altra indirezione: la **PLT**.

## GOT Hijacking
**Sovrascrivere una entry GOT:**
Se riusciamo a modificare l'indirizzo di una funzione con quella di un'altra che vogliamo chiamare, il programma richiamerà quest'ultima invece di quella "originaria".

*Esempio:*
![[slide numero 12]]

Possiamo **sostituire "puts" con "system"** e leggere nel nostro buffer, così da fare eseguire al programma ciò che abbiamo scritto nelllo scanf.

## Lazy linking
L'idea è che quando abbiamo un programma abbastanza grande, ci sono migliaia di funzioni, molte delle quali non vengono utilizzate.

Per non fare perdere tempo al caricamento, solitamente viene caricato solo un 20% delle funzioni disponibilii (le altre rimangono nell'hard disk).

**Lazy linking** = carico solo quello che so utilizzerai per la maggior parte delle volte, per il resto aspetti quale secondo in più.

...
...

Possiamo mettere direttamente il nostro nuovo indirizzo al posto del **?**

*Per vedere come funziona questa cosa, bisogna utilizzare il debugger di IDA mettendo un breakpoint poco prima di una funzione linkata dinamicamente. Guardando la GOT.*

## Mitigation per la GOT
- **Full RELRO**: Possiamo mettere la GOT in modalità **non scrivibile**, a questo punto però anche il dynamic linking non si può scrivere e quindi non possiamo sfruttare il **lazy linking**
- **Partial RELRO**: risolve però solo alcune vulnerabilità

NB. RELRO = RELocation Read-Only