# Sistemi operativi (prof. Chiarello)

**Sistema operativo** è un insieme di programmi e di moduli software. Ascolta ciò che gli sta intorno ed è in attesa gli succeda qualcosa
Può essere:
1. Aperto: costruito in modo da poter operare con molteplici dispositivi reperibilli sul mercato
2. Chiuso: scritto per essere eseguito su un insieme ristretto e definito di macchine
3. Sistemi centralizzati: es. mainframe (molto potente) e terminali *dumb*, alta sicurezza ma lentezza di esecuzione
4. Sistemi distribuiti: computer interconnessi con capacità di elaborazione offline e capaci di scambiarsi messaggi tra di loro

Passare da sistemi centralizzati a distribuiti si chiama **downsizing**
Le richieste dell'utilizzatore sono gestite dal sistema operativo rispettando le **politiche di gestione**

PROCEDURA: insieme di istruzioni

SERVIZI: 

PRIMITIVA: Piccoli programmi che servono per interrogare una risorsa hardware.
Ogni procedura standard per mezzo della quale si possono utilizzare i servizi di un *modulo*. 

MODULO: 

PORTABILITÁ (di un sistema operativo): si intende la sua attitudine a essere eseguito su macchina diverse

Quando i sistemi possono interagire tra di loro si parla di **interoperabilitá**

### Sistemi monoprogrammati e multiprogrammati
Nei sistemi monoprogrammati la cpu ha in esecuzione codice proveniente da un **unico** programma, quindi ci sono dei tempi di inattività
Nei sistemi multiprogrammati la cpu ha in esecuzione codice proveniente da **vari** programmi

Le risore hardware del pc sono:
- CPU
- Memorie centrali (MC)
- Unitá di memoria di massa (MM)
- dispositivi di I/O

-- INSERIRE SCHEMA PAG 12 --

**Round robin**: 

Nei sistemi multiprogrammati si utilizzano tempi inattivo (presenti nei sistemi monoprogrammati) della cpu (dove non fa nulla)

Risorsa gestita nei seguenti modi:

**Time sharing**: quando il suo uso viene concesso per un tempo che non può superare un massimo: questo intervallo viene chiamato **Time slice**.
Cpu (di sistema multiprogrammato) rimane assegnata ad un programma fino a quando:
-	Il programma utente termina
-	Il programma utente richiede che vengano effettuate operazioni che coinvolgono altri dispositivi

Accaduto uno di questi due eventi il sistema operativo decide a quale tra gli altri programmi spetti il prossimo time slice. Le modalità con cui il sistema operativo prende queste decisioni costituiscono un esempio di **politiche di gestione** 

### Classificazione sistemi operativi
1. Sistemi dedicati
	- un solo utente per volta

2. Sistemi batch
	- in funzione a prescindere dall'operabilità dell'utente
	
3. Sistemi interattivi multiutente
	- Obiettivo consiste nel mettere a disposizione a ciascun utente una periferica interattiva come il video, sistema centralizzato, ogni utente ha il suo spazio
	(es. server scolastico)
	- serve una CPU potente 

### Processi
Il processo è il programma che ha in esecuzione la cpu. É un insieme finito di azioni da eseguire in sequenza e dai dati che vengono elaborati dalle stesse azioni. Chiamiamo *processore* l'oggetto che causa l'evoluzione del processo.

-- INSERISCI FOTO --

I processi fermi (parcheggiati) possono essere memorizzati nella memoria di massa (es. swap)
Nella memoria centrale abbiamo invece i processi:
- pronti
- in esecuzione
- in attesa di I/O

-- INSERISCI FOTO -- 

Gli stedi possibili nel quale un processo si può trovare:
1. ...
2. ...

### Le interruzioni

Quando un evento avviene in tempi che dipendono da fattori esterni al sistema viene detto asincrono.

-- INSERISCI SCHEMA --

3 tipi fondamentali di interrupt:

1. Asincroni: generati solo dall'hardware, 
2. Sincroni generati dall'hardware: segnalano eventi accaduti in relazione all'orologio interno
3. Sincroni generati dal software: usati per accedere a routine particolari

### Il Nucleo

Chiamato anche **kernel**, è la parte del sistema operatico più vicina alla macchina, è strettamente dipendente dall'hardware. Le funzioni fondamentali sono:
1. Avvi e terminazione dei processi
2. Assegnazione della CPU ai diversi processi
3. Sincronizzazione tra i processi
4. Sincronizzazione dei processi con l'ambiente esterno

### Esecuzione parallela ed esecuzione concorrente dei processi

L'avanzamento dei processi può avvenire in modo *sequenziale* o ???

**THREAD**: sequenza di istruzioni in corso di esecuzione

L'elaborazione parallela permette di far lavorare più processi in modo del tutto
asincrono: ogni thread procede per la propria strada, utilizzando la CPU ed effettuan-
do operazioni di I/O senza disturbare gli altri.

**Elaborazione concorrente** di processi: il sistema operatico deve gestire la sincronizzazione tra i processi

NB. Metafora del semaforo

### Gestione della memoria

Se RAM viene occupata bisogna spostare i processi. Viene utilizzata quindi una memoria **swap**, dove vengono messi i processi che sono in attesa (quelli parcheggiati).

--(lasciare perdere la paginazione e segmentazione della memoria) -- 

### Periferica virtuale

Quando non abbiamo a disposizione una stampante e "stampiamo" in pdf: questa è una periferica virtuale

-- non serve altro?? --

## File system

1. Parlare con le periferiche
2. Gestire traffico CPU
3. Gestione della memoria di massa

Il file system provvede alla **virtualizzazione** delle memorie di massa: dobbiamo rappresentare i byte in una maniera logica, tramite i **file** (testo, programma, immagine, comando...)

Dobbiamo quindi:
1. Gestire in modo ottimale lo spazio
2. Garantire accesso dei dati all'utente, anche se presenti più utenti
3. Fornire agli utenti meccanismi di protezione dei file
4. Rendere disponibili operazioni di uso comune sui file: 
		- copia
		- cancellazione
		- modifica


Un FIle per essere definito tale deve avere:

1. Nome
2. Informazione sulla posizione dove è allocato nel disco
3. Data di creazione
4. Numero di record contenuti
5. Dimensione del record
6. Modalità consentite di accesso (esecuzione, lettura, scrittura)

La directory di livello più elevato è detta **root** (radice /)

**Pathname**: nome del file espresso attraverso il percorso di directory. Può essere **assoluto** o **relativo**

### L'interprete di comandi

Anche detta **Shell**, è un programma dell'OS che riceve in ingresso le richieste di esecuzione di operazioni, espresse usando il linguaggio di comandi.

Il linguaggio dei comandi permette la scrittura di veri e prorpi algoritmi strutturati, in linux **script** in DOS sono i **file BAT**

### I processi attivati dal sistema operativo

**BOOTSTRAP**: parte di accensione di ROM e BIOS

Dopo il bootstrap arriva il sistema operativo (Win, Linux,...):

-- INSERIRE SCHEMA DEL CARICAMENTO DELL'OS --

### Programmazione del software 
I linguaggi di programmazione possono essere **compilati** o **interpretati**

-- INSERIRE SCHEMA DEL LINGUAGGIO C --

Programma compilato ha 2 passaggi: prima il compilatore poi il linker (traduce tutto il programma in linguaggio macchina), così può essere eseguito senza dover interpretare le istruzioni: velocità maggiore

-- INSERIRE SCHEDA DEL LINGUAGGIO JAVA

in Java il file compilato .class viene dato alla VM (Virtual Machine) e può essere eseguito in ogni macchina. VM traduce ogni istruzione per il specifico OS, è quindi più lento. Qui il linguaggio è **interpretato** (traduco ogni riga di codice in linguaggio macchina e la eseguo)

NB. PhP è un linguaggio *interpretato*

### Protezione e la sicurezza
- **Backup & Restore** 
- **Crittografia**