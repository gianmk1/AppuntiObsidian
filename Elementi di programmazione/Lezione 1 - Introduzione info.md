# Introduzione - 12mar
NB. Libro consigliato: *Programmazione in Python* di Kenneth A. Lambert

I computer hanno:
- **logica cablata**, NON c'è un controllo, tutte le operazioni vengono fatte tramite segnali / porte logiche e segnali analogici. Il
- **logia programmata**, qui c'è un **PROCESSORE** c' 

La logica cablata ha un **grande contro**: una volta fatta NON è modificabile.
Nella logica programmata invece devo studiare un **linguaggio di programmazione**.

## NB. Algebra di bool
0 - falso - 0V
1 - vero - 5V

*Come faccio a dire quando è 0V il segnale è 0 e quando è 5V il segnale è 1?*
Questa logica porta dei problemi, quindi NON si utilizza più.

### Porte logiche
**AND**
1 x 1 = 1
0 x 1 = 0

**OR**
1 + 1 = 1
0 + 1 = 1
0 + 0 = 0

**Coniugato o Opposto:**
...
...

L'algebra di bool si utilizza in programmazione anche quando utilizziamo l'**IF**.

**NB**. **ELEMENTO NEUTRO**: neutro, vuol dire che non cambia risultato. 
0 + 1 = 1			-> x + 0 = x
0 + 0 = 0 			

1 x 0 = 0			-> y x 1 = y
1 x 1 = 1 

### Continuazione logica programmata / cablata
- Logica PROGRAMMATA : tutto dipende dal programma scritto (che deve essere scritto correttamente). Molto più dispendiosa (CPU, programmatore da pagare, manutenzione). La CPU poi ha **SCALDA MOLTO**.

- Logica CABLATA: è **affidabile**, è molto **sicura**, ha un costo minore in termini di soldi e energia. 


## Programmi e Algoritmi
*Perchè ho bisogno di scrivere un programma?*

Concetto del **PROBLEMA COMPUTAZIONALE**:

Un problema computazionale è una situazione da risolvere di un elaboratore, è quindi un problema che un Computer/CPU è in grado di risolvere.
*Abbiamo 2 insimi: I e S, I = esemplari S = soluzioni. In teoria NON si potrebbe avere un esemplare che punta a 2 soluzioni*
*Un esemplare è una situazione/il modo con cui un problema si sottopone nella realtà.*

Un problema computazionale deve essere risolvibile da un computer, per farlo risolvere da questo devo **creare un ALGORITMO**.

L'**ALGORITMO** è una **serie di istruzioni**: 
1. **ORDINATA**, se l'istruzione 1 è di un tipo e la 2 di un'altro, farò prima la 1 e poi la 2. NON è mai possibile avere 2 istruzioni allo stesso istante.
2. **FINITA**, NON posso avere un algoritmo infinito, si avrebbe un **loop infinito**.
3. **NON AMBIGUA**, l'algoritmo deve sempre dire al computer cosa fare precisamente

NB. In python c'è un errore che riguarda proprio l'ambiguità.

L'algoritmo quando ha queste 3 proprietà compila, ma non è detto che riesca a risolvere il problema che volevamo implementare, sta a noi che operazioni fare per risolvere quel problema.

**NON esiste una soluzione unica**, ci sono infiniti modi, uno o l'altro avranno **EFFICENZE DIVERSE.**

### Complessità
La complessità di un algoritmo è il punto centrale dell'informatica.
Si cerca sempre di rendere più efficiente un algoritmo.

*Es. Google troverà 10milioni di risultati in 1 secondo. Come fa a fare ciò? Google qualche hanno fa ha speso 20miliardi di dollari per portare l'algoritmo da 0.9secondi per ricerca media a 0.8secondi.*

Per la complessità si utilizza la **Funzione O(n)**
O non è propriamente una funzione, poichè NON ha bisogno di essere definita, è più un *insieme di funzioni*. (f(x) sta dentro O)

![[vedi schema sulle slide]]

*Relazione tra quante operazioni devo fare e il tempo che ci si mette per ritornare i risultati.*

Più la complessità è maggiore più tempo ci vuole per risolvere un "problema".

## Tipi di memorie e Strutture Dati
Una **struttura dati** è un'architettura con la quale i dati vengono memorizzati e ispezionati nella memoria.

Nel computer ci sono vari tipi di memorie:
- **RAM** Random Access Memory, *random* perchè che io scelga di leggere x o y, il tempo per la lettura di quasiasi dei 2 NON cambia. 
La memoria ram memorizza i dati "temporanei", in python possono essere le librerie / funzioni
- **ROM** Read Only Memory, **memoria di sola lettura**, in questa memoria viene memorizzato il firmware, il kernel,.. tutti i file di sistemi che non devono essere modificati dall'utente
- **epROM**, può essere solo letta ma può essere anche CANCELLATA, quindi la si può modificare cancellandola. Es Arduino ha una memoria eprom. Questo tipo di memoria è solo dell'OS e **non è volatile**
- **di MASSA**, memorzza tutti i file di sistema e dell'utente, deve persistere nel tempo. C'è un **tempo di risposta**.

**NB**. La memoria cache è tutta la memoria di buffer dei programmi.

### Strutture Gerarchiche

Ci sono modi di salvare dati che possono essere più o meno efficienti.

##### Struttura ad ALBERO
Una logica per memorizzare i dati può essere quella **ad albero**, dove ogni oggetto (file) deriva da un suo superiore.
La **radice ( / )** è da dove parte tutto (**padre**).
Quelli sotto si chiamano **figli**.
Gli ultimi si chiameranno **foglie**.

Un *singolo quadrato* viene detto **NODO**.
C'è un **ORDINE** e delle **REGOLE** tra i nodi.
Questa struttura è **GERARCHICA** mentre ce sono anche **lineari**.

![[esempio di una struttura ad albero]]

NB. Lineare fa pensare che c'è un *prima* e un *dopo*.

##### Struttura GRAFO
Il **GRAFO** è una struttura simile a quella ad albero, **senza avere però le regole** di quest'ultimo (come padri, figli, foglie).

**NB**. C'è comunque un ordinamento, il grafo è comunque una **struttura gerarchica**.
Nel grafo, a differenza dell'albero, possiamo inserire il **PESO**, cioè il costo per passare da un punto all'altro.

![[esempio di una struttura grafo]]

I *pallini* si chiamano **vertici** e le *connessioni* si chiamano **lati**.

### Strutture Lineari

##### Lista o Lista Concatenata
*Es. quando utilizziamo il browser possiamo andare avanti o indietro nella naviagazione in base alle pagine viste precedentemente/successivamente.*

Può essere definita come una **CATENA**, quindi una serie di maglie concatenate.

NB. Se la RAM utilizzasse questo sistema non sarebbe più random, bisognerebbe passare ogni elemento per raggiungere quello desiderato.

![[esempio di una struttura lista]]

È una combinazione di *elementi* (o **anelli**) e *collegamenti* (o **connessioni**).

##### Coda (o Queue)
La CODA è una **struttura orizzontale** in cui gli elementi vengono inseriti nell'ordine con cui arrivano. *Logica della coda della mensa*

La coda ha **logica FIFO (First In First Out)**, il primo che entra è il primo che esce.

![[esempio di una struttura coda]]

##### Coda PRIORITARIA
L'ordine non è più *il primo che arriva è il primo che esce*, ma **il primo che arriva CON LA PRIORITÀ PIÙ ALTA è il primo che esce.** 

Qui ora dobbiamo salvare non solo l'ordine con cui gli elementi arrivamo ma anche **la priorità di ciascuno**.

![[esempio di una struttura coda prioritaria]]

*Esempio: stiamo giocando a scacchi con un computer, il computer non può capire quale è la mossa che lo fa arrivare il più vicino possibile alla vittoria, quindi ordina tutte le mosse possibili in una coda prioritaria, ciascuna mossa avrà priorità diversa e verrà eseguita quella con priorità più ALTA*

##### STACK (o pila)
Lo STACK è una **struttura verticale**. L'ingresso è uscita è **sempre da sopra** (a differenza della coda).

*Esempio: una pila di maglietta, per prendere la prima maglietta che ho inserito dovrò togliere IN ORDINE tutte quelle sopra. Se voglio mantenere l'ordine devo **creare una nuova pila**. NON possono tenere ferme le magliette e sfilare quella sotto.*

Lo stack è la struttura più utilizzata nei linguaggi di programmazione.

NB. La **ricorsione** è quando una funzione chiama un'altra funzione. *Es. da un sito principale vengo renderizzato ad un altro sito e così via. I siti sono quindi impilati in uno stack. Se sono sul sito C e voglio tornare in A devo: chiudere il sito C, chiudere il sito B e ora sono su A.*

![[esempio di una struttura stack]]

NB. **NON posso avere una pila prioritaria**

## Dimostrare la correttezza dell'algoritmo
Ci sono vari modi per dimostrarlo:

1. **Tramite ESEMPIO**: questo metodo è molto veloce, facile da eseguire ma la dimostrazione che io faccio vale solo e soltanto per l'esempio che porto. *Google non può dimostrare il suo algoritmo di ricerca tramite esempio, altrimenti dovrebbe fare un esempio per i miliardi di siti memorizzati da Google.*

2. **Tramite CONTROESEMPIO**: faccio un esempio che mi serve per dimostrare che l'algoritmo NON funziona. *Basta avere un esempio sbagliato per dimostrare che l'algoritmo non funziona per tutto.* 
NB. È difficile dimostrare la correttezza tramite controesempio.

3. **Tramite INDUZIONE**: è molto più "teorica" rispetto al primo metodo. 
**CASO BASE** => Con l'induzione io prendo un **esempio generico**, e dimostro che per questo esempio l'alg funziona.
**INDUZIONE** => prendo il **caso successivo e dimostro che l'algoritmo funziona** anche per questo
In questo modo **TUTTI I CASI sono DIMOSTRATI**.
*Essendo che l'esempio generico è uno qualsiasi, prendendo quello dopo che è anch'esso uno qualunque e dimostrando questi 2 li dimostro tutti.*
NB. [n(n + 1) / 2] = 1 + 2 + 3 +4 +5 , questa formula si dimostra tramite *induzione*.

4. **INVARIANTE DI CICLO**, quando abbiamo un algoritmo che funziona su un ciclo viene utilizzata una dimostrazione chiamata *invariante di ciclo*. Per tutte le interazione del ciclo bisogna dimostrare che per ogni ciclo viene fatta la stessa cosa, per fare ciò basta **dimostrare il primo caso**.

