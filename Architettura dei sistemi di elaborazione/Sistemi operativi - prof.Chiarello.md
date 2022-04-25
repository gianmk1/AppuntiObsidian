# Sistemi operativi

Il **sistema operativo** (o **SO**) è un **insieme di programmi e di moduli software**, scritti allo scopo di rendere disponibili all'uso le risorse di calcolo e i dispositivi collegati al pc. Esso ascolta ciò che gli sta intorno e rimane in attesa che gli succeda qualcosa.

Un OS può essere:
1. **Aperto**: costruito in modo da poter operare con molteplici dispositivi senza far riferimento a produttori specifici
2. **Proprietario** (o **Chiuso**): scritto per essere eseguito su un insieme ristretto di macchine
3. **Centralizzato**: i dati e le applicazioni risiedono in un unico **mainframe** molto potente, ad esso sono collegati vari *terminali dumb* (senza capacità di elaborazione autonoma). *Alta sicurezza* ma *lentezza di esecuzione*.
4. **Distribuito**: insieme di **computer interconnessi** con capacità di elaborazione offline. La comunicazione tra di essi avviene tramite messaggi. 

I sistemi informatici aziendali sono passati da essere dei sistemi *centralizzati* a dei sistemi *distribuiti*, questo processo si chiama **downsizing**. 
<br>

## L'organizzazione modulare
Le richieste dell'utilizzatore vengono acquisite e gestite dall'OS rispettando delle **politiche di gestione**, cioè delle regole. La struttura di un OS è *gerarchica*, all'interno di ogni livello si usa raggruppare una classe di problemi in **moduli**.

![[schema_moduli.png]]

Questi moduli permettono di richiedere risorse ai dispositivi utilizzando comandi più comprensibili. Si dice che **virtualizzano** i dispositivi, li trasformano in *macchine virtuali* in grado di eseguire operazioni complesse come se fossero elementari (in modo logico piuttosto che fisico).

I moduli devono essere **indipendenti**, se un OS è costruito con criteri di modularità può essere usato su macchine diverse sostituendo i soli moduli che operano sull'hardware, mantenendo le stesse primitive.

##### Alcune definizioni:
- **Procedura**: *sequenza di istruzioni raggruppate* in un unico blocco
- **Primitiva**: ogni procedura standard per mezzo della quale si possono utilizzare i servizi di un modulo. *Programmi elementari che servono per interrogare una risorsa hardware*.
- **Modulo**: *collezione di routine facilmente riusabile* che attiva i meccanismi necessari per la risoluzione di un problema logico (es. gestione memoria, operazione di I/O)
- **Portabilità** (di un OS): si intende la sua attitudine ad essere eseguito in macchine diverse. Quando i diversi OS possono interagine tra di loro si parla di **interoperabilità**.
<br>

## Sistemi monoprogrammati e multiprogrammati
Le risorse hardware di un pc sono:
- Unità centrala di elaborazione (**CPU**)
- Memorie centrali (**MC**) (es. Ram, Rom, Cache)
- Unità di memoria di massa (**MM**)
- Dispositivi di **I/O**

#### Sistema monoprogrammato
Un sistema viene detto **monoprogrammato** quando la sua memoria centrale contiene, in un dato istante, codice utente proveniente da un unico programma. La CPU ha quindi in esecuzione un **unico programma** e ci sono pertanto dei **tempi di inattività**.

L'esecuzione di un'istruzione di un programma comporta una **system call**, cioè una **richiesta di qualche routine** dell'OS (es. quando viene richiesto l'accesso a una periferica)

![[tempi_sistema_monotasking.png]]

Si può dividere il tempo che intercorre tra inizio e fine del programma in intervalli, cioè le diverse attività della CPU:
- esecuzione di istruzioni del programma utente
- esecuzione di istruzioni del sistema operativo
- **stato di inattività**

In questo modo l'utilizzo della CPU è poco efficiente, la si potrebbe sfruttare meglio facendo in modo che, nel tempo di inattività, vengano eseguiti altri programmi.

#### Sistema multiprogrammato (o multitasking)
L'obiettivo è quello di sfruttare al massimo la macchina **utilizzando i tempi morti** della CPU, nei quali normalmente non sarebbe impegnata, per svolgere altri programmi.
Così facendo una frazione di tempo disponibile viene utilizzata per lo **scheduler** (gestore dei processi).

Una risorsa viene gestita in modo **TIME SHARING** quando il suo uso viene concesso per un **tempo massimo**, questo intervallo è chiamato **TIME SLICE**.
La CPU rimane assegnata ad un programma utente finchè:
- Il programma utente termina
- Il programma utente richiede che vengano effettuate operazioni che coinvolgono altri dispositivi
- **scade il time slice**

Dopo uno di questi eventi l'OS decide a quale tra gli altri programmi spetti il prossimo *time slice*. Le modalità con le quali l'OS si decide prende queste decisioni costituiscono un esempio di **politiche di gestione**.

**NB1**. La realizzazione più semplice di quest'ultima consiste nell'assegnamento **round robin** (a rotazione), il programma a cui è tolta la risorsa viene messa in fondo ad una coda di programmi in attesa.
**NB2**. L'OS usa dei meccanismi di **priorità** che consentono ad alcuni programmi di essere eseguiti più rapidamente.
<br>

## Classificazione dei sistemi operativi
1. **Sistemi dedicati**: prevedono l'utilizzo da parte di un solo utente per volta. I più moderni supportano il multitasking
2. **Sistema batch**: funziona a prescindere dall'operabilità dell'utente. Si possono scrivere file **script** (o **batch**) conteneti sequenze di comandi.
3. **Sistemi interattivi multiutente**: utilizzato da più utenti contemporaneamente. La risorsa CPU viene decicata a ciascun utente a turno per un tempo definito (**time sharing**). Serve quindi una CPU potente e una MC capiente. *Es: Server scolastico*
<br>

## Stati dei processi
Un **programma** è un **insieme di istruzioni**, raggruppate in uno o più file, scritte con un procedimento algoritmico che serve per la risoluzione di un problema.
Un **processo** è un **programma in esecuzione**. *Definisce un insieme di azioni da eseguire in sequenza e di dati che vengono elaborati dalle stesse azioni.*

![[schema_processi_1.png]]

**NB**. Nella memoria di massa è presente anche la partizione **swap**

L'OS interviene appena termina l'assegnazione della CPU al processo attuale.
Questo può avvenire per 3 motivi:
1. Il **processo termina**: l'OS libera l'area della RAM occupata dal processo e la riempie con uno di quelli *parcheggiati*
2. Il **time slice finisce**: l'OS sospende il processo dandogli lo stato di **pronto** e assegna la CPU a un altro processo (sempre nello stato di pronto)
3. Il processo **richiede operazione di I/O**: il processo ha eseguito una *system call*. L'OS attribuisce al processo lo stato di **attesa**, al termine dell'operazione di I/O torna allo stato di **pronto**

![[scheduling_processi.png]]

Gli **stati** possibili in cui si può trovare un processo sono:
- **Parcheggiato**: quando attende di essere caricato nella RAM
- **Pronto**: quanto attende di venire assegnato alla CPU
- In **Esecuzione**: quando il processo è in evoluzione poichè assegnato alla CPU
- In **Attesa**: richiede un'operazione di I/O o attende un evento
- **Terminazione**: quando il processo è stato completato e può essere tolto dalla RAM
<br>

## Le interruzioni
Quando un evento avviene in tempi che **dipendono da fattori esterni al sistema** viene detto **asincrono**, alcuni esempi sono: gli errori, la fine di una stampa, invio di comandi tramite dispositivi di input.

Il verificarsi di questi eventi viene comunicato alla CPU usando il meccanismo di **interrupt** (segnali di interruzione), si può così segnalare alla CPU che è successo qualcosa e deve interrompere momentaneamente la sua attività (salva lo stato del processo in esecuzione).
A seconda del tipo di interrupt vengono avviate delle *routine di sistema* che provvedono all'attuazione delle misure necessarie.
Il processo che si occupa della gestione delle interruzioni si chiama **interrupt handler**.

Un'interruzione causata dal *time sharing* (interrupt dopo un certo periodo di tempo definito) NON dipende da fattori esterni alla macchina, si parta quindi di **interruzioni sincrone**.

3 tipi fondamentali di **interrupt**:
- **Asincroni**: generati dall'hardware, segnalano eventi non correlati all'orologio interno della CPU
- **Sincroni generati dall'hardware**: segnalano eventi accaduti in relazione all'orologio interno
- **Sincroni provocati via software**: usati per accedere a *routine* particolari
<br>

## Il nucleo
Chiamato anche **kernel**, è la parte dell'OS più vicina alla macchina, è strettamente dipendente dall'hardware. Le funzioni fondamentali sono:
1. Avvio e terminazione dei processi
2. Assegnazione della CPU ai processi
3. Sincronizzazione tra i processi
4. Sincronizzazione dei processi con l'ambiente esterno

Il nulceo comprende tutte le routine di risposta alle interruzioni e le procedure che assegnano la CPU ai diversi processi. Le **norme che regolano queste assegnazioni** si chiamano **politiche di scheduling**:

La più semplice è quella **round robin** che prevede una coda di processi *pronti* e un insieme di processi *in attesa*. Quando si toglie la CPU ad un processo (*es. time slice scade*) questo viene messo in fondo alla coda (se rimane allo stato di pronto) o passa allo stato di attesa.
In entrambi casi la CPU viene **assegnata al primo processo della coda**.

Si possono organizzare i processi in più *code* corrispondenti alle diverse **priorità**. Al momento di scegliere quale processo mandare in esecuzione **si favoriscono quelli a prorità elevata**.

*Quando un processo a bassa priorità è in esecuzione e un processo con priorità maggiore ritorna da un'operazione di I/O, il primo viene interrotto e il secondo va subito in esecuzione.* Questo meccanismo si chiama **preemption** (prelazione).

Con questa gestione si garantisce che i processi privilegiati vengano eseguiti più frequentemente, comunque si deve **garantire l'esecuzione di tutti i processi**.

**NB**. Il gestore dei processi (**scheduler**) e il gestore delle interruzioni (**interrupt handler**) sono anch'essi dei processi e hanno proprità **massima**.
<br>

## Esecuzione parallela ed esecuzione concorrente dei processi

Nella situazione più semplice l'avanzamento di diversi processi avviene in modo **sequenziale**, cioè l'OS assegna a ogni processo le risorse necessare e **nel momento in cui servono**, per portare a termine il lavoro.

L'esecuzione dei processi è più efficiente e veloce se si introducono alcuni meccanismi:

#### Elaborazione parallela
Nell'elaborazione parallela un singolo programma o meglio, un processo, **viene suddiviso** in più set di istruzioni che vengono **eseguite in parellelo**.

Uh **thread** è una **sequenza di istruzioni in corso di esecuzione**, è un sottoinsieme di un processo.

- In un ambiente **multithread** possiamo creare più thread contemporaneamente attivi, cioè più sequenze di istruzioni eseguite parallelamente.

- In un ambiente **singlethread** l'utente può eseguire solo un programma per volta, o solo una sequenza di istruzioni, e deve attendere la conclusione di un lavoro per passare al successivo.

L'**elaborazione parallela** permette di far lavorare più processi in modo **asincrono**: ogni thread procede, utilizzando la CPU e effettuando operazioni di I/O, senza distrurbare gli altri.

**NB.** Sia i processi che i thread sono sequenze di istruzioni, la differenza sta nel fatto che i processi vengono eseguiti in **spazi di memoria separati** mentre i thread vengono eseguiti in uno **spazio di memoria condiviso**.

#### Elaborazione concorrente
Si parla di elaborazione concorrente dei processi quando:
1. I processi entrano in concorrenza per l'uso di una risosa condivisa
2. Un processo ha bisogno dei risultati prodotti da altri processi per avanzare

In questi casi l'OS deve svolgere la gestione della **sincronizzazione** tra i processi:
bisogna garantire un accesso ordinato alle risorse e **impedire condizioni di conflitto** che rallentino l'avanzamento dell'elaborazione. Deve anche impedire **interferenze** che potrebbero portare a perdite di dati.

*Meccanismo del **semaforo** *:
Il processo che usa i semafori ne verifica il valore e, se prende in uso una risorsa, ne cambia il valore in modo che i successivi processi possano sapere che devono aspettare.

Bisogna perciò garantire l'equità, un sistema è **equo**:
Quando permette a tutti i processi di accedere alle risorsa e portare a compimento il lavoro. Un sistema equo permette di evitare le situazioni di:
- **Starvation**: quando 1 o più processi non riescono ad accedere ad una risorsa
- **Deadlock**: quando 2 processi sono in attesa di una condizione che non potrà mai accadere
<br>

## Gestione della memoria
Il gestore della memoria *simula l'esistenza di una pluralità di unità di memoria centrale*, ciasuna associata a un processo, mascherando la limitazione fisica della MC reale.
Nel caso di programmi molto grandi la loro completa allocazione nella MC sarebbe problematica e monopolizerebbe la risorsa.

Si utilizzano perciò tecniche di funzionamento in **overlay**, per le quali è sufficiente avere in memoria centrale una porzione del programma , lasciano il resto nella memoria di massa (area di **swap**), caricando altre porzioni di quest'ultimo solo quando necessarie e liberando memoria quando non servono più.

La zona del disco riservata per questa gestione si chiama *area di **swap** *.

I processi hanno così a disposizione la memoria centrale di cui hanno bisogno, anche se in realtà essa è solo **virtuale**, poichè non corrisponde alla memoria fisica.
Ciò si realizza tramite 2 tecniche, la **paginazione** e la **segmentazione**.

#### Paginazione
Ogni programma viene considerato come **diviso in blocchi** di **eguali** dimensioni detti **pagine logiche.** La memoria centrale viene a sua volta divisa in **pagine fisiche** (*frame*) di dimensioni uguali a quelle delle logiche.

![[paginazione_2.png]]

Una tabella riassume la situazione delle pagine di un programma descrivendo:
- se occupa una pagina fisica
- la pagina occupata
- la posizione sul disco della pagina logica
- altre info: *es*. **flag** che indica se la pagina è stata modificata
<br>
![[swap_in_memoria.png]]

A ogni accesso alla MC si verifica se la pagina richiesta è presente o meno in memoria: se NON lo è, l'OS provvede a caricarla in una pagina fisica (**swap-in**). Se tutte le pagine fisiche sono occupate, si scarica una pagina presente in MC (**swap-out**).

Le pagine contenenti il nucleo dell'OS **restano fisse in memoria** e non vengono mai paginate sul disco, il meccanismo che si occupa di ciò si chiama **pinning**.

#### Segmentazione
Con questa tecnica la suddivisione del programma in memoria viene effettuata in base a **criteri logici** è può essere controllata dallo sviluppatore. Ciascun blocco ha quindi **lunghezza arbitraria** e viene detto **segmento**.

La ripartizione deve seguire il criterio del *minimo recupero di chiamate* tra segmenti diversi. Cioè al crescere della complessità del programma, bisogna raggruppare in segmenti le procedure più frequentemente usate.

Per ogni segmento occorre sapere:
- se è presente in memoria
- qual è l'indirizzo dove inizia
- dove si trova su disco
- la sua dimensione
<br>

## Le periferiche virtuali
Il **device manegement** è la parte dell'OS che consente di definire i dispositivi virtuali:
- nascondendo i reali meccanismi con i quali le periferiche comunicano, attraverso delle primitive
- gestendo i contrattempi che possono verificarsi (es. errori di trasmissione)

In questo modo l'utente può utilizzare le periferiche senze preoccuparsi delle loro caratteristiche e delle operazioni fisiche che vengono svolte.

L'OS può anche aumentare in modo virtuale il numero di periferiche tramite lo **spooling**.
<br>

## Il File System
Il file system è un meccanismo che gestisce l'**organizzazione fisica** delle informazioni memorizzate sul disco presentandole all'utente in modo **logico**.
Il **file system** provvede alla **virtualizzazione** delle memorie di massa. Bisogna rappresentare i byte fisici nel disco in modo **logico** tramite **file** (programmi, testi, foto,...).

Le principali funzioni del file system sono:
1. **Gestire lo spazio** in modo ottimale
2. **Garantire l'accesso ai file** in modo veloce, anche in presenza di più richieste di accesso allo stesso file
3. Fornire agli utenti **meccanismi di protezione dei file**, come protezione dalla lettura del file, dalla scrittura, dalla cancellazione
4. Rendere disponibili facilmente le operazioni di uso comune sui file, es. copia, cancellazione, rinominazione,...

**NB**. Il file system deve essere anche in grado di comunicare con le **periferiche** (es, pendrive usb, disco esterno,...)

Il file system consente di riferirsi in **modo logico** alle informazioni registrate, in termini di **identificatori** (al posto degli indirizzi fisici), adoperando le **directory**, che contengono per ciascun file:
- L'**identificatore** (nome del file)
- Informazioni sulla posizione
- Data di creazione
- Numero di record contenuti
- Dimensione dei record
- Modalità di accesso consentite

La directory di livello più alto è detta **root (o radice /)**, non è contenuta in altre directory ed è allocata in posizione fissa e nota al sistema.
La struttura ad albero è composta da *nodi non terminali (directory)* e da *nodi terminali (i file)*.

Per individuare file descritti in altre directory, al di fuori quindi di quella *corrente*, bisogna utilizzare il **pathname**, che può essere:
1. **Assoluto**: quando il nome del file viene descritto indicando tutti i nodi che occorre attraversare a partire dalla root
2. **Relativo**: quando l'attraversamento inizia dalla directory *corrente*

**NB**. Anche la tastiera e il video vengono considerati file di ingresso e uscita (**standart input** e **standard output**). 
<br>

## L'interprete di comandi
Anche detto **shell** è un programma dell'OS che riceve in ingresso le richieste di esecuzione di operationi espresse in linguaggio di comandi.

Il linguaggio dei comandi permette la scrittura di veri e propri algoritmi strutturali, in Linux si chiamano **script** in DOS sono detti **file BAT**.
<br>

## I processi attivati dal sistema operativo
Quando il computer viene acceso, occore caricare l'OS in memoria centrale, copiandolo dal disco sul quale permanentemente risiede. A ciò provvvede un programma registrato su ROM chiamato **IPL (Initial Program Loader)** che assume il controllo della CPU all'avvio.
Il caricamento viene chiamato **BOOTSTRAP**. Molto spesso il caricamento dell'OS non è completo ma riguarda solo una parte.

In fase di **bootstrap** viene caricato in memoria il **kernel** oltre ad altro software. Prima di tutto di manda in esecuzione lo **scheduler** (gestore dei processi), esso attiva a sua volta altri processi.

![[bootstrap.png]]
<br>

## Programmazione del software
I linguaggi di programmazione possono essere di vari tipi:

1. **Compilato**: in questi tipi di linguaggio il codice viene convertito in **Assembly** attraverso il compilatore e successivamente tradotto in **binario**. Per fare modifiche bisogna accedere al codice sorgente e successivamente ricompilarlo. *Es: C, C++*
2. **Interpretato**: il programma è rappresentato dal codice sorgente stesso, ogni volta che è eseguito viene prima *tradotto e poi compilato* (riga per riga). C'è quindi una maggiore semplicità di sintassi ma una **minore velocità di esecuzione**. *Es: Python, PhP*

**NB**. Java è un linguaggio **pseudocompilato**, il codice viene compilato in un linguaggio intermedio, il **Bytecode** (.class) che viene dato ad una **VM (Virtual Machine)** con la quale viene interpretato. Ciò permette di avere file leggeri ma che possono girare su qualsiasi macchina.
<br>

## Protezione e sicurezza
- **Backup & Restore**
- **Crittografia**

---
Fonti:
- [[PremesseTeoricheSO-prof. Chiarello.pdf]]
- [[Gestione dei processi.pdf]]
