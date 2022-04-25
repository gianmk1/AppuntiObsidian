### Perchè la cybersedcurity è importante?
1. **Digitalizzazione dei processi**
2. **Spionaggio industriale**, più diffuse
3. **Contrasto al terrorismo**
4. **Infrastrutture pubbliche**, sono i nuovi bersagli
5. **Identità digitale**


## Digitalizzazione dei processi
1. Revisione del modo di lavorare
2. Digitalizzazione dei processi industriali
3. Digitalizzazione dei documenti
4. Puntare alla **semplificazione**

## Spionaggio industriale
Queste sono i principali fattori:
1. Geopolitica (es. Russia-Ucraina)
2. Governi
3. Ricerca e sviluppo
4. Nuove tecnologie

#### OT security
L'**operational technology** è l'uso di hardware e software per monitorare e controllare processi fisici, dispositivi, ecc. (es. Spostare i binari in un bivio)

**SCADA** è uno dei sistemi utilizzato nei processi industriali

## Contrasto al terrorismo
Le principali piattaforme di comunicazione sono:
- Twitter
- Chat di videogame
- PSN
- Forum privati e non
- Deep Web

#### SOCMINT
Detta anche Social Media Intelligence, viene usata per spiare le realtà terroristiche, monitoraggio degli account,...

Uno dei punti deboli della SOCMINT è la verifica di tali informazioni, ci sono 3 problemi:
- Falsi positivi
- Falsi negativi
- ...


## Infrastrutture pubbliche
#### Alta disponibilità
Le infrastrutture pubbliche devono garantire sempre la disponibilità dei propri sistemi. es. più server collegati che forniscono lo stesso servizio

#### Protezione dei dati personali
Le infrastrutture della Pubblca Amministrazione trattano una notevole quantità di dati personali anche molto riservati.

#### Conseguenza degli attacchi
- ...
- ...
- ...
- ...

## Identità digitale
È l'insieme di tutte le nostre informazioni online, account sui social, dispositivi, ...

#### Possibili minacce
- Furto d'identità
- Ripercussioni sulla vita reale: screditamento della persona,...
- Problemi di carattere pratico: nel caso di furto di credenziali
- Comunicazione: es.compromissione di un account fb in cui si fanno partire messaggi fasulli

#### Come ci si protegge
- utilizzare password sicure
- utlizzo di multi-factor authentication

**NB.** Il rischio zero NON esiste.

#### Gestione degli account
Nel momento in cui l'azienda è molto grande c'è bisogno di un sistema di **Identity and Access Management**. 

In base ai ruoli di un account è possibile essere autorizzati o meno.

**LEAST PRIVILEGE**: se il mio lavoro è un unico compito, devo avere il minimo di autorizzazioni possibili per eseguire il mio compito

**SEPARATION OF DUTIES**: separazione dei compiti, avrò accesso solemente ai dispositivi/sistemi che mi competono

#### Modello RBAC
È un modello logici che serve per definire i **ruoli**. Spesso all'interno dei sistemi di identity ci sono delle implementazione al modello RBAC

<br>
<br>

# Office security
- Lock dei dispositivi sia fisico che applicativo
- Cancella gli appunti
- Usare il distruggidocumenti
- Proteggi la stampa con un PIN

### PC & Smartphone Security
- Lock dei dispositivi sia fisico che applicativo
- Antivirus (meglio se collegato ad un sistema aziendale)
- Full disk encryption
- Sistemi mobile con MDM, es. nel sistema mdm stabilisco una policy per cui il pin debba essere almeno di 6 cifre

### Aggiornamento software
È fondamentale per la prevenzione degli attacchi e per migliorare le funzionalità/performance.

NB. OpenVPN

# Alcuni termini:
- **Hack Value**: nozione che indica quando ne vale la pena ad acquisire un target
- **Vulnerability**:
- **Exploit**: ... sfruttare una vulnerabilità
- **Payload**: è la parte di codice exploit che esegue attività malevole come creare una backdoor, cifrare il file,...
- **Zero-Day**: una vulnerabilità NON nota, un attacco sfrutta questo tipo di vulnerabilità prima del rilascio della relativa patch
- **Daisy Chaining**: saltare da un computer all'altro per arrivare al mio target
- **Doxing**: ... 
- **Bot**: è un software che esegue o automatizza determinati task

# Tipologie di attacchi ai sistemi
- SISTEMA OPERATIVO: l'attaccante trova una vulnerabilità nel OS e la sfrutta per accedere al sistema. Queste vulnerabilità sono difficili da trovare 
- LIVELLO APPLICATIVO: l'attaccante trova una vulnerabilità nell'applicazione che vengono eseguite. Alcuni attacchi sono: buffer overflow, xss, SQL injection, man-in-the-middle, sessione hijacking, Dos,...
- ...
- ...




NB. **XSS** : in genere viene iniettata una parte di codice html all'interno di qualsiasi input (es. campo di ricerca) e se c'è una vulnerabilità possiamo sfruttarla. 

## Chi è l'hacker
- Competenze info
- Per alcuni solo un hobby
- Intezioni, curiosità o illegali

##### I vari tipi di hacker
- blackhat
- greyhat
- whitehat
- hacktivist
- state sponsored hacker : ingaggiati da governi, spesso per penetrare altri governi
- cyber terrorist
- suicide hacker
- script kiddies

### Fasi dell'hacking
1. Information gathering o reconnaissance
- Scanning
- Gaining Access
- Maintaining Access
- Clearing Tracks

1. Information gathering
	- Fase PASSIVA: Andiamo ad estrarre informazioni senza interazioni col target
	- Fase ATTIVA: c'è interazione diretta col target

2. Scanning
	Ci interessa capire le porte aperte e se ci sono vulnerabilità (es. utilizzando nmap)
	
3. Gaining Access
	Sfruttando una vulnerabilità trovata entriamo nel sistema e abbiamo un certo livello di accesso. Dobbiamo guadagnare il maggior numero di privilegi
	
4. Maintaining Access
	Manteniamo l'accesso tramite virus o backdoor

5. Clearing Tracks
	(es. script CoverMyAss)
	

# Controlli per l'information security
### Segregazione delle reti
Lo **zoning** o segregazione è fondamentale per dividere l'organizzazione in varie reti separati. ES. VLAN, dmz, ...
Segregazione logica della rete (o fisica)

### Policy di sicurezza
1. Indentificare i rischi tramite risk assessment
2. Imparare dagli altri o dalle linee guida
3. Includere il management
4. Ammende/Multe
5. Fornire la versione finale della policy a tutti
6. Assicurarsi che tutti abbiamo compreso la policy
7. Sviluppare strumenti per rinforzare la policy
8. Formare i dipendenti
9. Rivedere e aggiornare regolarmente le policy

### Rischio e Risk Management
Il rischio si riferisce al livello di incertezza o di aspettativa che un evento negativo possa causare danni al sistema

**Risk Management** porta alla riduzione e al mantenimento del rischio ad un livello accettabile

**NB** Tabelle di rischio

### Incident management
*vedi slide*



# Information gathering
### Google Dork

NB (exploit-db.com)

### WHOIS
Per trovare informazioni su domini di primo livello o di sottodomini
Possiamo utilizzare servizi come netcraft.com , **sublist3r**

### Sistemi operativi, web server e metadati
- La determinazione di un sistema operativo è essenziale per indirizzare gli attacchi
- Footprinting per siti web è inteso come il monitoraggio e analisi dei siti web
- Estrazione dei metadati può essere utile pe ricavare informazioni (es. geolocalizzazione da una foto)

### OSINT (o Open Source Intelligence)
Alcuni libri: Open Source Intelligence (sfondo blu)

### Banner Grabbing
Attivo o passivo, è il metodo utilizzato per determinare il sistema operativo del target tramite una porta

### Alcuni Tool:
- Maltego: per OSINT
- recon-ng
- FOCA
- recondog
- OSRFramework
- sn1per
- LHF

# Tipologie di attacco:
## Attacco DoS e DDoS
Attacco una struttura per fare in modo che questa non offra più il suo servizio

**NB**. Se si tratta di un servizio essenziale è tra gli attacchi più temuti e efficaci

DOS

DdOS

Tipologie:
...

Dettagli:
- UDP Flood
- SYN Flood
- ...

Detection e mitigazione:
...


## Session Hijacking
Si può tradurre come compromettere la sessione.
Una sessione è una stringa di dati che ci permette di essere riconosciuti e autenticati ???
### Concetti e tipologie

Con il session hijacking possiamo inserirci all'interno di una comunicazione http per rubare una sessione e quindi autenticarsi come un altro utente
2 tipi:
1. A livello network: sniffiamo la connessione
2. A livello applicativo: in altri modi

### Session management
Per ovviare a questo attacco ci sono delle linee guida:
- quando si effettua un login la sessione va cambiata

## Man-in-the-middle
Anche detto MITM, quando qualcuno si interpone nella comunicazione tra due parti

*vedi video su youtube*

NB importante è criffografare la rete anche all'interno dell'azienda (es, tra backend e frontend)
NB non riguarda solo http e https
NB hatercap tool

## Buffer overfolow
In C/C++ ogni tipo di variabile ha la sua lunghezza predefinita. Questo attacco tenta di scrivere in tutte le "celle" di una variabile e finire in **overflow** così da arrivare  a scrivere del codice nella RAM che successivamente verrà eseguito.

<br>
<br>
<br>
<br>

*Quando abbiamo un buffer di x byte, riusciamo a uscire dal buffer e scriverci l'attacco*

# Malware
*Malicious software*

È un software malevolo in grado di arrecare danni ad un sistema, disabilitare funzionalità e/o fornire il controllo remoto di un dispositivo.

### Composizione di un malware
- **CRYPTER**: protegge il malware dalla reverse engineering (= risalire dall' "exe" al codice sorgente), altrimenti sappiamo come difendersi
- **DOWNLOADER**: trojan che **scarica** altri malware dalla rete (es. ransomware,...)
- **DROPPER**: trojan che **installa** altri malware (quelli scaricati dal downloader)
- **EXPLOIT**: codice malevolo che sfrutta una vulnerabilità per entrare nel sistema (per poi inserire un payload, vedi sotto)
- **INJECTOR**: inietta la parte di codice malware (o **payload**) nel sistema
- **OBFUSCATOR**: programma che permette l'offuscamento del codice e degli intenti di un malware, così da rendere difficile la rilevazione
- **PACKER**: programma che prende tutte le componenti del malware e le mette in un unico eseguibile
- **PAYLOAD**: codice malevolo che permette di prendere controllo di un sistema (dopo l'exploit)
- **MALICIOUS CODE**: comandi che definiscono le funzionalità dl malware, come furto credenziali, creazione backdoor,...

### Malware analysis
È un processo di difesa (*blue team*) di **reverse engineering**.
2 tiplogie principali di difesa:
1. STATIC ANALYSIS: si *disassembla* il codice e lo si studia per capirne il funzionamento
2. DYNAMIC ANALYSIS: fatto solitamente in ambienti protetti, viene fatto "detornare" il malware all'interno di questo sistema e lo si studia

NB CODE REVIEW : parte dell'application security

### Metodi di detection:
- **SCANNING**: calcolare l'hash di un malware, inserirlo in un database, in caso di corrispondenza viene lanciato un alert e bloccato il malware.
- **INTEGRITY CHECKING**: sempre utilizzando funzioni di hashing andiamo a calcolare l'integrità dei dati all'interno del nostro hard-disk, nel momento in cui un file ha una signature difersa e non l'ho modificato sono stato infettato
- **INTERCEPTION**: qualsiasi cosa fatta all'interno del PC viene interrotta e intercettata e se questa è legittima questa continua, altrimenti termina
- **CODE EMULATION**:...
- **HEURISTIC ANALYSIS**: andiamo analizzare dinamicamente come si comporta il malware...

### Indicatori di compromissione
1. I processi richiedono più tempo e risorse
2. Beep del computer senza nessun video (spesso si inseriscono nel bios)
3. I drive cambiano etichetta
4. Il S.O. viene caricato con errori o non viene caricato affatto
5. Avvisi constanti dall'antivirus
6. Il computer di blocca di frequente o resistuisce errori come BSOD
7. Mancano file e cartelle
8. L'attività dell'hard-disk è sospetta
9. La finestra del browser si blocca
10. Mancanza di spazio sul disco
11. Popup di pubblicità inattesi

<br>
<br>
<br>
<br>

# Injection
Sono principalemente di 3 tipi: sql-injection, LDAP injection, command injection

### SQL Injection
![[inserire immagine]]

Quando andiamo a fare il login di una persona sul nostro sistema in genere la query che il sistema fa sul db è (vedi sopra)

Se ritorna true ci autentica al sistema

Per fare una SQL injection dobbiamo ritornare quello che c'è dopo il where come vero

Il concetto è quello di far diventare la proposizione vera

Con la SQL injection si possono incatenare vari attacchi fino ad ottenere la shell di sistema.

Cosa possiamo fare:
1. Estrazione di dati
2. Creazione degli accessi (backdoor)
	1. sul livello applicativo: io accedo alla web app con una credenzial creata
	2. sul sistema operativo: creo una backdoor sul sistema
3. Danneggiamento (eliminazione dei dati)

Tool utile è **SQL map**

### Command injection
Iniezione di comandi sull'applicativo / sul sistema operativo

NB system è una funzione di php che ci permette di utilizzare comandi dell'OS

L'obiettivo è quello di esecuzione di comandi sul sistema operativo host attraverso un'applicazione web

![[vedi schema slide]]

### LDAP injection
LDAP è un protocollo per accedere a database di informazioni strutturate ad albero. (es. **active directory**, db ad informazioni gerarchiche. Si stabilisce un dominio all'interno del quale si inseriscono le informazioni.)

LDAP injection sono simili, come concetto, a quello si sql injection.

Come in sql injection è possibile bypassare il controllo del login e autenticarsi come un altro utente.

<br>
<br>
<br>

##### Report annuali cybersecurity

![[diagrammi a torta su tecniche - esiti - finalità]]

