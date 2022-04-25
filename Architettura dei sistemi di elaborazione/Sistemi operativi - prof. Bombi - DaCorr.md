# Sistemi operativi (prof. Bombi)

Un sistema operativo (o **OS** o **S.O.**) è un insieme di programmi che vengono caricati in memoria centrale all'avvio del sistema. Ha 2 scopi principali:
1. Ottimizzare l'uso delle risorse del sistema, prendendone il controllo e assegnandole ai processi
2. Funge da interfaccia tra l'utente e la macchina fisica

![[inserire foto schema: utente-applicazione-os-hardware]]

L'utente in realtà gestisce anche direttamente con l'OS, es. ambiente grafico

### Programmi e processi
Il **programma** è un'*entità passiva*: un insieme di byte contenente la codifica binaria delle istruzioni da eseguire. Quando viene eseguito diventa un processo.

Il **processo** è un'*entità attiva*, l'instanza di un programma in esecuzione.

**Un processo è un programma in esecuzione**

### Cos'è una risorsa?
I processi per avanzare hanno biogno di Cpu, memoria RAM, dispositivi di I/O
Possono anche avere bisogno di dati generatti de altri processi.

**Una risorsa è un'unità hardware e software necessaria all'avanzamento di un processo.
**

CPU, ram e dispositivi i/o sono le risorsa hardware
dati condivisi tra più processi (es. dati processo a ha bisogno di dati processo b per continuazione) sono le risorse software
### Servizi forniti dall' S.O.
- sviluppo di software
- esecuzione di programma
- accesso ai dispositivi
- accesso protetto alle risorse
- gestione degli errori
- ecc.

### Rappresentazione schematica di un pc - i Bus
![[inserire schema base di un calcolatore - è di colore azzurro/blu]]

Questo schema rappresenta il minimo indispensabile. 
La cpu, la memoria e I/O sono dei *sottosistemi*, i 3 principali del computer che svolgono compiti specifici. Questi 3 sono messi in comunicazione da dai **bus di sistema**. 
La sua composizione è:
- Control Bus: determina il massimo di dati che si possono mandare, insieme di segnali (es. diretti da CPU alla memoria (cioè la *scrittura*), ecc.), ognuno dei quali ha un significato specifico.
- Address Bus: servono a identificare a quale allocazione di memoria o dispositivo di i/o è interessato ai dati. Normalmente solo la cpu è abilitata a scrivere nell'address bus.
- Data Bus: contenuto del dato da trasferire

Ogni linea del control bus ha un significato indipendente da tutte le altre del bus control e ogni linea ha la sua direzione.

Trasferimento DMA: --- completare ---

NB: con n bit ho a disposizione 2 all n combinazioni

### Struttura interna della CPU
![[schema struttura interna processore]]

Il processore funziona sul ciclo **fetch - decode - execute**

Il processore deve eseguire istruzioni che sono nella ram, il ciclo base è:
- **istruction fetcher** prelievo: lettura dalla memoria
- **istruction decoder** (control unit del processore) decodifica dell'istruzione, mandando  in giro molti segnali di controllo (esterni e interni) apre e chiude porte che fanno in modo che l'istruzione venga eseguita
- i **registri** sono una memoria interna della cpu, serve per contentere dati in transito da cpu a memoria (e vicecersa)
- **ALU** componente logica del processore che è in grado di eseguire le operazioni logiche: *and, or, not* e le *operazioni aritmetiche base*. Gli operandi di queste operazioni devono essere nei registri per essere utilizzati

NB: **Registro dei flag di stato** è fatto di tanti bit, ognuno con un proprio significato; è presente tra questi il **bit di modo** se vale 0 la CPU è in modalità kernel, se 1 è in modalità utente.

Program counter: contiene...
instruction register:
registro dei flag di stato:

### Sistema multiprogrammato (o multitasking)
Sono presenti e attivi nel sistema molti processi contemporaneamente. I processi si contendono l'uso del processore e della memoria (risorse). Quando un OS è multitasking c'è il problema della protezione dell risorse

Es. Processo A non deve poter modificare la memoria del processo B

In un sistema multitasking c'è una condivisione dell risorse tra i processi.
La memoria è **ripartita** tra i vari processi
Il processore ''è 1 invece", c'è quindi una **ripartizione nel tempo**

Risorsa memoria: bisogna impedire ad un processo di accedere alle aree di memoria asssegnate ad altri processi, l'hardware deve supportare questa caratteristica

## Protezione dell risorse 
Quando sistema è multitasking servono dei meccanismi di protezione hardware per esercitare la protezione sulle risorse. *Le risorse allocate a programmi/utenti devono essere protette nei confronti di accessi illeciti di altri programmi/utenti.*

L'architettura hardware prevede un bit di modo (kernel - 0 ; user - 1).
Al verificarsi di un errore, l'hardware commuta in modalità kernel.

Meccanismo di interruzione: --- completare ---

I programmi utente vengono eseguiti in user mode, il sistema operativo è eseguito in kernel mode (**supervisor**)

Ogni architettura hardware ha il suo set di istruzioni macchina, prevede alcune istruzioni che possono essere eseguite solo in modalità kernel

**Interruzioni**:
1. Hardware: generate dai dispositivi quando completano l'esecuzione di un compito dato. Es. tastiera manda segnale di interruzione, OS interrompe programma precedente, viene eseguito del codice di risposta
2. Software: programma che sta funzionando in modalità utente, ad un certo punto viene interrotto, processore va in modalità kernel e os esegue delle istruzioni (**system call**)
3. Trap: generate in situzioni di errori

Meccanismo di interruzioni hardware: segnali che arrivano da dispositivi periferici per segnalare il termine di un'operazione 

Errore **Trap**: se utente chiede es. divisione per 0, viene generata una trap
Errore **Segmentation fault**: saturazione della memoria disponibile per il processo

--- vedere slide protezione #2 ---
<br>

*Esempio:*
Il processore è istante per istante in uno **stato**, se si sta eseguendo un programma (A) e il disco finisce un trasferimento (B), il sistema riceve un **segnale di interruzione**, l'OS esegue l'operazione richiesta (kernel mode). Il controllo ora ritorna al programma iniziale (user mode).
C'è bisogno di un **salvataggio di stato** che salva lo stato della cpu, lo cambia e alla fine lo rispristina come da inizio. 

Quando c'è un'interruzione si memorizza stao pc nello stack (o stak)

## Organizzazione a strati dell'OS
![[inserire immagine pag 14 del pdf]]

- NUCLEO: 
	1. gestisce il processore
	2. gestisce i/o di basso livello: insieme dell routine di risposta dei diversi dispositivi hardware
	3. gestisce la comunicazione tra processi

- GESTIONE DELLA MEMORIA: decide a quale processo allocare una parte di memoria
- GESTIONE DELLE PERIFERICHE: 
- FILE SYSTEM: componente dell os che mappa la struttura fisica del disco (diviso in blocchi). L'utente ha una visione logica del disco, permessa dal file system
- INTERAZIONE UTENTE:

**NB**. i/o di basso livello VS i/o di alto livello:

## Come viene gestita la risorsa cpu
![[sschema pag 16 pdf]]

**Vari tipi di stati:**
- PRONTO: ha un processo con tutte le risorse che gli servono tranne la cpu, è quindi in coda
- Passaggio da ESECUZIONE a BLOCCATO (o Attesa): non ha senso tenere occupata la cpu per un processo che al momento non la sta utilizzando e magari sta aspettando che termini il processo di lettura di un disco. Il processo viene quindi messo in stato BLOCCATO (o ATTESA). 
- PRONTO: Viene riportato allo stato di PRONTO quando ha finito, in questo caso, la lettura del disco
- NUOVO: momento in cui il processo viene creato, accumula le risorse che gli servono

Si può passare da ESECUZIONE a PRONTO o BLOCCATO

- IN MEMORIA SECONDARIA:

	La memoria è virtualizzata, quella di un singolo processo potrebbe essere più grande di quella fisica (reale) => una piccola parte della memoria virtuale è realmente mappata in quella fisica, il resto viene mappato nel disco (SWAP)
	Se il sistema è in crisi, ha poca memoria disponibile rispetto ai processi in esecuzioni:
	sceglie un processo, gli toglie tutta la memoria e la sposta nella swap (nel disco), fino a quando non si libererà abbastanza la memoria del dispositivo

	- Swap IN: 
	- Swap OUT:

NB. le istruzioni per essere eseguite **comunque devono essere nella RAM**

NB. La CACHE:
	- è gestita dall'hardware non dal sistema operativo
	- hardware deve tenere aggiornata la cache rispetto alla ram
	- cache della cpu ≠ registri della cpu

## Scheduler e Dispatcher -???-
Quando l'os è multitasking il sistema può agire solo quando ci sono delle interruzioni (che comunque un timer ne genera ciclicamente).
Con timer => passaggio da esecuzione a pronto
Con interruzione => passaggio da esecuzione a bloccato 

??? vedi slide

## Process Control Block (o PCB)-???-

Ogni processo è descritto da un PCB in cui viene descritto:
- nome e/o id del processo
- stato del processo (attesa, pronto, ...)
- contesto hardware del processo (registri del processore)
- altre informazioni per la gestione del processo
- link a altri PCB (serve per gestire le code di processi)

NB. Quando parliamo di indirizzi di memoria ci riferiamo sempre alla memoria RAM (memoria centrale del sistema, che ha sempre un piccolo pezzo di memoria ROM).
I processi lavorano in uno spazio di memoria virtuale
Anche il sistema operativo ha un suo spazio di memoria virtuale

Ogni spazio di memoria virtuale è mappato nella RAM, a sua volta anche la ram è mappata in una memoria più piccola detta CACHE, che però è molto piccola, quindi ci sono dei meccaniscmi hardware che portano informazioni dalla ram alla cache

## Scheduling dei processi 
Processi possono essere catalogati come:
- CPU-bound: molta elaborazione, usano molto il processore
- i/o - bound: poca elaborazione, necessitano di molte interazioni (es. con l'utente)

Lo scheduling normalmente è di tipo **preemptive**: allo scadare del time-slice il processo viene messo in coda nei processi pronti.

I processi cpu bound sono favoriti perchè usano molto il processore, gli altri stanno molto tempo nello stato di bloccato.
Il sistema operativo quindi lavora con le **priorità**: i processi hanno priorità diversi, il dispatcher prende il primo processo in attesa nella coda con la priorità più bassa

La priorità viene assegnata ai processi dinamicamente:

NB. potrebbe succedere che un processo a priorità bassa non riesce mai ad andare in esecuzione, questa situazione di chiama **stardation**, viene quindi data priorità alta ad un processo di priorità alta

- Processi BATCH (a priorità minore): avanzano quando il processore non serve a nessun altro
- ...

#### Overhead del sistema operativo
La percentuale di tempo di CPU (o di RAM) usato del sistema operativo per svolgere le sue funzioni. Overhead troppo alto compromette l'efficenza dell'uso del cpu.

#### Cosa vuol dire sfruttare una risorsa?
 Contrasti tra le risorsa
 
 ## Politiche di scheduling
FCFS:
RR: una sola coda di processi pronti e si va a turno
PS:
MF (Multilevel Feedback Scheduling): prevede l'aggiustamento dinamico delle priorità

## Gestione della memoria pt2
![[inserire schema della memoria RAM]]

Ad oggi si usano tecniche di virtualizzazione della memoria.
Per poter gestire correttamente la memoria il OS deve garantire:
- Protezione (vedi sopra)
- Trasparenza: il processo non deve essere consapevole di quello che succede 
- Allocazione logica: le **le pagine di memorira** assegnate ad un processo non sono per forza contigue (una dopo l'altra). Il programma deve vederle però come fisicamente contigue


NB. Tecnica di Overlay: utilizzata nei vecchi computer dai sviluppatore per dividere il programma (troppo grande per caricarlo completamente in memoria) in una parte che rimaneva nella memoria RAM, e il resto veniva diviso in blocchi e quando c'era bisogno di uno di quest'ultimi lo si caricava in memoria.
Ora non bisogna più preoccuparsi di questo => **Trasparenza** (vedi sopra)

- Condivisione: condivisione dei dati è necessaria nel caso di processi cooperanti che fanno parte del medesimo programma. In windows si chiamano **DLL**. Tutto questo serve per evitare che lo stesso codice venga duplicato nella RAM.

## Memoria virtuale impaginata
Già spiegato sopra.
Sia la memoria virtuale che quella fisica (RAM) è divisa in pagine.
Memoria fisica è divisa in blocchi uguali detti frame o pagine fisiche
Memoria virtuale è divisa in blocchi uguali detti pagine o pagine logiche

Esempio: A caso l'os, quando un processo ha bisogno di una pagina virtuale, la carica nella ram

Sia gli indirizzi fisici che quelli virtuali sono divisi in numero della pagine + offset. 
L'offset non cambia, bisogna solo capire in quale pagina fisica risiede una virtuale:
Il **MMU** determina la corrispondenza tra pagina virtuale e fisica

#### MMU
Questo processo della mmu è oneroso in termine di risorse, quindi questo utilizza una memoria che velocemente da la traduzione da pagina virtuale a fisica chiamata **TLB**

### Politica di fetching
Per decidere quali pagine virtuale caricare
1. **demand paging**: all'inizio non si carica nulla, la pagina viene portata in memoria solo quando il rocessore chiede di accedere ad un suo indirizzo
2. **prepaging**:

### Politica di sostituzione
Quando un processo ha raggiunto il massimo della pagine fisiche a lui dedicate disponibili e richiede l'accesso ad un atra, serve una sostituzione:
- Algoritmo ottimo:
- Algoritmo LRU: si toglie la pagine che non viene utilizzata da più tempo
- algoritmo FIFO: si toglie la pagina che è caricata da più tempo (non è una buona politica)
- Altoritmo di tipo clock: si toglie la pagina che non è usata da molto tempo (non per forze la prima caricata)

La Cache per fare posto utilizza una politica di LRU: si toglie la pagine che non viene utilizzata da più tempo 

---
Fonti: 
- [[Sistemi Operativi - prof. Bombi.pdf]]