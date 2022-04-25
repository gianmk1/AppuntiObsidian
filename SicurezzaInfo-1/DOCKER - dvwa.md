### DOCKER
`docker run -d -p 8080:80 --rm [nome_container]`
-d : per lanciare il container come demone
-p per configurare porte
--rm : per rimuovere conteiner una volta stoppato

NB sagikazarmark/dvwa

`docker ps` ci fa vedere i processi (in questo caso i container)

# DVWA
## XSS (Reflected)
L'obiettivo è iniettare del codice e vedere se la pagina lo ritorna.

Per ovviare al fatto che http è un protocollo state-less si utilizzano i cookie (es PHP_SESSIONID) per ricordare la connessione

I cookie hanno dei flag di metterli in sicurezza, se il cookie ha httpOnly non possiamo modificarlo e non può essere utilizzato da JavaScript

## XSS (Stored)
A differenza della prima qui il messaggio che scriviamo viene memorizzato all'interno del database

## Session Hijacking

## File Inclusion
Inclusione di una pagina


## SQL Injection
Dvwa SQL injection:

La query che farà sarà circa: SELECT * FROM users WHERE id = '$id';
Noi dobbiamo provare a rompere questa query

SELECT * FROM users WHERE id = ' 'OR 1=1;# ';
- Il valore che inseriremo noi è 'OR 1=1;#
- Ci mostrerà gli utenti se id = nulla o 1=1
- Il commento (#) ci servirà per non far valutare gli ultimi 2 caratteri

Un tool utile è SqlMAP

sqlmap -u "[http://localhost:8081/vulnerabilities/sqli/index.php?id=1&Submit=Submit](http://localhost:8080/vulnerabilities/sqli/index.php?id=1&Submit=Submit)" --cookie="PHPSESSID=l72h1ra5kk5bnigrs1rlah0n80; security=low" --dump

## BruteForce
Tool utile : BURP