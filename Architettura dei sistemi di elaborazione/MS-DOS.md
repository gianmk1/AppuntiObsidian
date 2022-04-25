# DOS

### Bootstrap di DOS
1. Lettura di eventuali paramentri di configuazione file CONFIG.SYS
2. AUTOEXEC.BAT:
3. COMMAND.COM:

### Schema di funzionamento dei processore comandi di MS-DOS

![[inserire schema pag 7 di msdos.pdf]] (molto importante)

1. Vado a cercare dove sta l'os nel mio file system. Se c'è lo avvio se no do errore
2. Sto in ascolto, in attesa di comandi
3. Quando trovo il comando: se è interno (cd, mkdir, ecc.) lo suo, altrimenti lo cerco nella cartella dei comandi degli utenti esterni (file batch)

#### Comando MS-DOS
È composto da 3 parti:
1. **Nome** (identifica il comando)
2. **Parametri** (definiscono gli oggetti su cui il programma deve agire)
3. **Opzioni** (composte da / seguita da 1 o più caratteri, hanno scopo di alterare la modalità di esecuzione del programma)

### Drive, prompt
In windows il disco principale è il **C:**

### Estensioni notevoli
- **COM**: il contenuto del file verrà caricato in memoria esattamente com'è (file immagine)
- **EXE**: il contenuto del file deve subire un processo di finitura in funzione dell'indirizzo di memoria scelto
- **BAT**: 

### I caratteri "jolly"
`*` rappresenta una **qualsiasi sequenza** (eventualmente nulla) di caratteri permessi
`?` rappresenta un **qualsiasi carattere singolo**

Es. `dir *.bat` : mostra tutti i file nella directory con estensione .bat

`|` per fare una concatenazione di comandi
`\` per le opzioni
`{}` per definire un insieme

**NB**. *Percorso relativo:* il punto nel quale ci troviamo diventa la radice del mio percorso. Nel DOS utilizziamo il **./** per indicare la directory corrente 

### Alcuni comandi:
- **copy** : per copiare file (es. copy f1 c:\ => copia il file f1 nella radice del disco C)
- **move**: per spostare o cambiare nome alla directory
- **ren**: per rinominare un file (es. ren *.txt *.scr => cambia l'estensione di tutti i file txt in scr)
- **del**: cancella un file o un gruppo di file
- **print**: per la stampa a video
- **attrib**: modifica o imposta la modalità di accesso al file
- **diskcopy**: per copiare da disco a disco
- **format**: per formattare un disco
- **echo**: per dare in output a video qualcosa
- **cls**: per pulire la console
- **set**: per variabili d'ambiente
- **rem**: per commentare

**NB**. Per creare un file vuoto: *type nul > nome_file*
**NB2**. *@echo off* : per disattivare la stampa a video dei comandi


##### Dispositivi come file
Alcuni dispositivi sono associati nomi particolari, per esempio CON alla console, PRN alla stampante

--- CONTINUARE---

##### Formattazione dei dischi
La formattazione può essere logica o fisica:
- logica: toglie solamente la radice del file system, i file rimangono
- fisica: viene modificato ogni bit del fily system

##### PATH

---completare---

### Comandi di rete (---completare---)
- **ping**: 
- **tracert**:
- **netstat**: mostra tutti i processi attivi nel mio dispositivo

### Variabili
Istanziazione variabile: **set peppe=amicone**
Richiamare una variabile:	**%peppe%**

### Comando type e parametri
Vedi file di prova su cartella es1

%1

![[script type2_1.bat ]]

### File Struttura - le etichette

Queste etichette si possono usare per fare dei salti

:begin è un'etichetta, inizio

:main è la parte principale

:end è la parte finale dello script

### Il costrutto IF

### Operatori di comparazione

- **EQU**	= uguale
- **NEQ** = diverso
- **LSS** = minore di
- **LEQ** = minore uguale a 
- **GTR** = maggiore di
- **GEQ** = maggiore uguale a

### Comando goto

### Operatori di redirezione
- `>`: ogni volta sovrascrive quello che trova
- `>>`: invece di sovrascrivere **accoda**
- `<`: legge il file su STDIN
- `<<`:

### Operatore Pipe
`|`: collega comandi diversi

### Comando Find

### Cartella AppData

### Variabili d'ambiente
Per accedere facilemente a dei percorsi senza doverli indicare ogni volta
![[vedi slide]]

- %alluserprofile% : 
- %appdata% : è importante pulire questa cartella dai vecchi programmati disinstallati
- %programdata%
- %systemdrive%
- %systemroot% e %winroot%
- %temp%
- %userprofile%



### Comandi DOS di rete
![[vedi file pdf]]

- netstat : fa vedere tutti le informazioni relative alle connessioni in entrata e uscita
- arp : mostra la tabella degli indirizzi ip associato al mac address
- nbtstat : mostra nomi NetBIOS....
- hostname
- tracert : per esaminare il percorso di un host rmeoto
- ipconfig
- nslookup : 
- route: per vedere tabella routing della mia macchina
- netdiag : fa diagnosi della rete

Netstat:
In **netstat** 0.0.0.0 indirizzi di rete del mio computer

`*.*` non sono utilizzate

ARP:
Con `arp -a` vediamo la tabella che associa il mac address all'indirizzo fisico

nbtstat:
Con `netstat -a sito_web`

nslookup:
`nslookup` otteniamo il nome e l'indirizzo IP del server DNS predefinito del dspositivo ...
#### Protoccolli 

UDP: uniform data protocot
TCP: transmission control protocol
**Socket**:

TCP e UDP sono al livello 3, quando noi colleghiamo la presa alla scheda di rete, in quella presa c'è il socket che comincia a comunicare

