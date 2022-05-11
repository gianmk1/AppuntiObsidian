# Lezione 11 maggio
## Virtual Box
Alcune macchine utilizzate saranno **Metasploitable 2** e **Windows 7**.

**NB**. La versione Free di VMware (a differenza di VMware) **non concede la possibilità di fare snapshot** della macchina.

**NB**. L'extension pack di VirtualBox consente di utilizzare USB di tipo 3.0

#### Istantanee
Una delle funzioni più importanti di VirtualBox è quella di poter fare uno **snapshot della macchina**, cioè uno stato della macchina corrente.

Se dovesse succedere qualcosa alla macchina durante il suo utilizzo, invece di reinstallarla posso tornare al punto in cui ho fatto l'istantanea tramite gli snapshot

**NB**. È consigliabile effettuare un'istantanea **appena configurata la macchina per la prima volta**

## Nikto
È un software opensource che **effettua vulnerability assessment sui web server**. Esso include un database di file e configurazioni notorialmente vulnerabili.

Prima di cominciare bisogna aggiornare il DB con:  **sudo nikto -update** (deprecated)

`nikto -h [INDIRIZZO IP VITTIMA]`  

## Nmap
È possibile utilizzare nmap anche per **trovare le vulnerabilità**. Infatti permette di:

NB. **Alcuni stati possibili delle porte:** 
- Una porta può essere **APERTA**
- **CHIUSA** (accessibile ma non vi è alcun servizio in esecuzione su di essa)
- **FILTRATA** (un filtro di pacchetti impedisce ai probe di raggiungere la porta), 
- **UNFILTERED** (la porta è accessibile ma nmap non sa se è aperta o chiusa), 

Quante porte ci sono su un server? **65536**.

Scansionare tutte le porte, con versione,... :
`sudo nmap -sS -sV -O -p1-65536 [INDIRIZZO IP VITTIMA]`

**NB**. La versione delle porte spesso ci permette di **scoprire delle vulnerabilità**.

Possiamo usare nmap **come tool di vulnerability assessment** con:
`sudo nmap -sV -O -p1-1024 --script vulners  192.168.1.245`

Lo script **vulners** ci permette di trovare le vulnerabilità

## OpenVas
È un framework che include servizi e strumenti per la scansione e la gestione completa delle vulnerabilità.

A fine installazione diamo il comando seguende per installare il plugin per riconoscere le vulnerabilità:
`sudo gvm-feed-update`

Per avviare openvas:
`sudo gvm-start`
E andare alla pagina di login:
`https://127.0.0.1:9392/login`

**NB**. Quando si avvia OpenVas è necessario che vengano avviati anche i 3 servizi collegati

Credenziali OpenVas: **admin** - **"psw salvata da installazione"**

#### Lanciare una scansione di un Server
1. Impostare un **target** (Configuration > Target)
2. Impostare una **scansione** (Scans > Tasks)
	- Posso impostare degli **alert** per essere avvisati in particolari condizioni
	- Impostare delle **schedules** per le scansioni
3. Esportare un **repot**


**NB1**. Più l'analisi è invasiva e più "rumore" generiamo
**NB2**. Può volerci un po' di tempo per **sincronizzare le configurazioni delle scansioni**

Il **QoD** mi dice la **percentuale che la corrispondente vulnerabilità sia sfruttabile** nella macchina vittima

In OpenVas è presente uno strumento che permette di **confrontare più repot tra di loro**, in questo modo possiamo valutare **se sono state applicate delle patch** o **se sono state scoperte nuove vulnerabilità** sulla macchina.

<br>

## OWASP Zap
È uno strumento utilizzato per la scansione di sole **applicazioni web**.

Il vantaggio è che è molto semplice da utilizzare.

Tramite le **"bandierine colorate"** mi segnala se ci sono più o meno alert gravi