# User Authentication
**Access Control**:
1. Identità (username)
2. Verifica (password)

NB. Quanto trattato qui è completamente diverso dalla **message authentication**

Con i sistemi di autenticazione andiamo a verificare se l'utente può accedere a servizi specifici. Tramite user authentication l'OS gestisce cosa l'utente può vedere o meno.

4 proprietà per il metodo di verifica dell'user authentication:
- che si conosce (es. password)
- che si possiede (es. token)
- che si ha, static biometrics (es. fingerprint)
- sistemi dinamici biometrici (es. voce)

Questi tipi di accessi possono essere utilizzati **da soli** o **combinati**.

##### Password Authentication
Il sistema va a vedere i privilegi di un utente, dopo aver verificato la password.

**Discretionary access control**: per ogni utente si va a vedere quale operazione può fare

##### Password Vulnerability
All'interno di un PC le password non vengono salvate in chiaro, ma vengono **hashate**. Quando un utente fa a fare il login si compara l'hash della passowrd immessa con quella salvata.

**1. Offline Dictionary Attack:**
Se ho l'hash della password posso:
- conoscendo la funzione, provando molte password comuni e vedere se c'è corrispondenza tra gli hash
- informazioni relative all'utente, molte persone salvano le password con parole vicine a loro

**Contromisure:**
- Avere una buona password
- Proteggere queste informazioni il più possibile

**2. Specific account Attack**
- È importante non far scegliere agli utenti password semplici.
- Bisogna bloccare l'account dopo un tot di tentativi

**3. Popular Password guessing**
*Prendo 1 milione di account facebook, e cerco di accedere con delle password popolari. Prima o poi si riuscirà a bucare qualche account*

È importante quindi utilizzare una password NON COMUNE

**4. Workstation Hijacking**
È importante NON lasciare un pc loggato quando si lascia la postazione. 

Si possono utilizzare quindi software che bloccano il pc se un utente si alza dalla postazione e non si risiede entro un tot di secondi.

**5. Exploit user mistakes**
Gli utenti tendono a scrivere le password, soprattutto se devono essere complicate, in un post-it , foglio di carta.

Con questi utenti bisogna fare **user training** (= informare). E combianare password con altri sistemi di autenticazione.

**6. Exploiting multiple password uses**
Spesso si utilizza la stessa password per più siti diversi.

**7. Electronic monitoring**
Quando facciamo l'accesso con le credenziali, in quale modo, questa deve passare attraverso il cavo ethernet o il wifi. Si può quindi **sniffare** la rete.

### Hashed password
Le password, quando vengono salvate in un sistema, vengono **hashate** tramite una funzione di hash in cui diamo come parametri la password immessa e il **sale**.

**Salt**: solitamente è un numero intero che va da 1 a 1.000.000 .
Nel nostro PC quindi troveremo il **file con le password** hashate e il **file con i sali**.

**NB**. Anche se abbiamo questi valori, è quasi impossibile ritornare la password originaria.

### Password Craking
Gli **attacchi dizionario** sono computazionalmente complessi. Si creano quindi delle tabelle **rainbow table** con le passsword già hashate con i vari salt.

### Password Choices
Bisogna sempre cercare di istruire gli utenti il più possibile e **dare delle regole**.
