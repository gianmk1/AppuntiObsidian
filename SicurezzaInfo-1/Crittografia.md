# Crittografia

## Crittografia Simmetrica
La **crittografia simmetrica** è la cifratura più utilizzata poichè più semplice e veloce. Richiede meno potenza computazionale.
Questo tipo di crittografia richiede 5 elementi:
- plaintext : testo "in chiaro"
- encrypt algorithm : algoritmo di cifratura (es. DSA, AES)
- secret key : password
- ciphretext : output dopo aver applicato la cifratura
- decrypt algorithm : algoritmo di decifratura (quello ci cifratura applicato in maniera inversa)

![[inseriesci schema slide]]

Utilizzo:
- Secret key condivisa
- Algoritmo di cifratura forte

Attaccare crittografia simmetrica:
1. **Crittoanalisi**: studio dell'algoritmo di cifratura, capire come da A il testo viene trasformato in B. Facendo delle prove con mie testi e con password scelte da me studio l'algoritmo.
2. **Brute-Force**: provo una serie di combinazioni finchè non trovo quella che mi da il risultato corretto. Dispendioso in termini di tempo e risorse (meglio utilizzarlo con la GPU).

**NB.** Analisi delle **frequenze**, es. cifrario di Cesare

La cifratura simmetrica si divide in 2 modalità:
- Algoritmo di cifratura a **BLOCCHI**: divido il "plaintext" in blocchi di lunghezza fissa (es. AES e DES). Più lenti rispetto quelli a flusso.

NB. L'insicurezza del 'singolo' DES è data dalla lunghezza della chiave che è solamente di 56bit. La velocità di cifratura cambia a seconda della lunghezza della chiave.

![[inserisci slide tempo chiave]]

NB. 10^9 corrisponde ad un PC moderno. 10^13 corrisponde ad un PC con una GPU dedicata abbastanza potente.

<br>

- Algoritmo di cifratura a **FLUSSO**: viene cifrato tutto il flusso, vengono utilizzati es. per lo streaming audio/video.

L'input viene continuamente cifrato al momento, tipicamente 1 byte (8 bit) alla volta.

![[inserisci schema ]]

Qui sopra la chiave è in input aad un generatore di byte pseudocasuali, il prodotto, cioè la **keystream**, viene combinato in **XOR** con il plaintext per produrrre il **ciphertext**.

## Crittografia Asimettrica
La **crittografia asimettrica** non ha una sola chiave ma ne ha **2**. Una **pubblica** e **privata**, quella pubblica viene inviata ad un destinatario.

NB. È stata introdotta da Diffie e Hellman nel 1976

##### Panoramica e struttura:
1. Ogni utente genera una **coppia** di chiavi
2. La chiave che rimane a noi è quella privata, quella pubblica viene inviata al destinatario o caricata in un repository
3. Se il destinatario vuole 

![[schema cifratura asimettrica]]

Nel momento in cui vado a cifrare con una chiave privata non inserisco informazioni troppo personali, qualcunaltro potrebbe avere la stessa chiave.
Questo meccanismo viene solitamente utilizzato per verificare l'identità del destinatario.

# Messagge authentication
Per garantire l'autenticità e l'integrità del messaggio. Questo avviene in 2 modalità:
Crittografia simmetrica può essere integrata, ma da sola garantisce solo la confidenzialità
Autenticazione senza cifratura: non garantisce la confidenzialità
La cifratura viene usata il meno possibile poichè molto costosa

2 modalità:
1. Message authentication code (MAC): fornisce autenticità e integrità, consiste nell'utilizzare una secret key epr generare un blocco dati.
	*leggi spiegazione sulla slide + inserisci diagramma*
	Le funzioni di MAC sono simili a quelle di cifratura, ormai si utilizzano solamente HMAC, cioè con implementazioni di hash
	
	Una volta effettuata la funzione, avendo il risultato, non possiamo tornare al messaggio originario: non sono quindi funzioni reversibili
2. Funzioni di hashing onw-way: ricevono in input messaggi di lunghezza variabile e restituiscono una stringa chiamata **digest**. A differenza del MAC con le funzioni di hashing non abbiamo bisogno di una secretkey.
	**digest = hash**
	
	Autenticazione di messaggi tramite digest con cifratura asimetrica
	![[inserisci schema]]
	
	a. Messaggio dato in input a funzione di hashing
	b. Digest risultante combinato con secret key
	c. L'insieme viene dato all'algoritmo di cifratura
	d. ...
	
	
	Autenticazione di messaggi tramite digest cifrati con cifratura asimettrica
	![[inserisci schema]]
	
	Stesso funzionamento ma chi manda ha la chiave privata, chi riceve ha quella pubblica
	
	
	Autenticazione tramite digest del messaggoi concatenato ad una secret key
	![[inserisci schema]]
	
	Alcune note:
	- Le funzioni di cifratura classiche sono LENTE, percui si prediligono funzioni di hashing
	- L'hardware per la cifratura è ottimizzato per grandi quantità di dati, con piccolo blocchi c'è molto overhead
	- Gli algoritmi da cifratura potrebbero essere protetti da brevetto

NB. Nell'implementazione con concatenazione è impossibile per un attaccante risalitre alla secret key. Non si può alterare il messaggio se non alterandolo

NB. **Salting**: se il sistema alla mia password accoda qualche salt diventa più complicato risalire alla password tramite hash. Per pwd cracking si possono trovare vari dizionari con parole in chiaro o corrispettivi hash


## Funzioni di hashing
Funzioni matematiche non reversibili, una funzione di hash produce un "impronta" di un file/messaggio/... . 

NB. Gli antivirus fino qualche anno fa calcolavano l hash del malware e i pc calcolavano l hash di ogni file per controllare se avevano quel virus.
Era molto dispendioso per la CPU

6 proprietà necessarie di una funzione di hash:
1. H (funzione di hash) può essere applicato a blocchi di file di qualsiasi grandezza
2. H produce una stringa di dimensioni fisse (es. SHA1 - 32caratteri)
3. H(x), cioè l'input deve essere semplice computazionalmente
4. Non possiamo trovare l'input avendo il risultato
5. Resistenza alle COLLISIONI

NB. Queste funzioni hanno però una combinazione finita. C'è il rischio di **COLLISIONE** (2 input diversi mi ritornano lo stesso hash)

- Le prime 3 proprietà vanno a garantire la message authentication
- La 4a proprietà è ovviamente fondamentale 
- La 5a garantisce che sia impossibile trovare...

Altre applicazioni degli hash:
- **password**: calcolato l'hash questo viene salvano nel db. Al login si calcola l hash della password immessa e la si confronta con l hash salvato
-**Intrusion detection**: per verificare modifiche, confrontarli con i digest del malware. Possiamo anche controllare il traffico in entrata, appena trovo un hash di un malware blocco il traffico


## Algoritmi di cifratura asimmetrica
**RSA**: funziona con cifratura a blocchi
Oggigiorno vengono usate chiavi di almeno 1024bit, meglio usare però chiavi a 4096bit

**Diffie-Hellman**: utilizzato per lo scambio di chiavi, questo tipo di algoritmo in realtà si trova per la cifratura simmetrica
*L'algoritmo è limitato allo scambio di chiavi*

**Curve elittiche**: abbastanza nuovo


## Firma digitale
Il risultato di una trasformazioni crittografata di dati che fornisce un meccanismo per veificare autenticazione, integrità e non-repudiation (cioè sistema che riceve o manda non può dire di non averlo ricevuto o spedito)

Garantisce che sia firmato da X e non è stato alterato dal momento che è stato firmato.

Algoritmi di digital signature:
- Digital signature algoritm (DSA)
- ...
- Elliptic Curve

*Struttura di un algoritmo di Digital Signature:*
![[inserisci schema slide]]

*Note:*
Anche in questo caso il messaggio non è cifrato
Quando abbiamo l'algoritmo di digital signature possiamo utilizzare uno dei 3 metodi

## Key management
### Certificati a chiave pubblica
La chiave pubblica deve essere trasmessa  a tutti, purtroppo chiunque potrebbe fare un annuncio di questo tipo, rubando l'identità di es. Bob

I certificati a chiave pubblica risolvono questo problema, accoppiano una chiave pubblica ad un **user ID**. Questo blocco viene firmato da una terza parte: la **CA, Certificate Authority**

Il periodio di validità di questi certificato è in genere di 1/2 anni

Procedure di come dall'utente arriviamo a un certificato firmato:
1. utente crea una coppia di chiavi
2. utente prepara un certificato non firmato che include userid e chiave pubblica
3. utente invia certificato a CA
4. la ca firma il certificato:
	1. .
	2. ...
5. ...
6. La CA invia il certificato all'utente
7. L'utente può adesso inviare il proprio certificato agli altri utenti
8. ...
	1. ...
	2. ...

Fidandomi della CA mi fido a mia volta del mittente.

![[inserire schema slide]]

# Numeri casuali e pseudorandomici
Inseriti, ad esempio, negli algoritmi di hashing e di cifratura per aumentarne l'entropia.

In linux il file /dev/random viene richiamato quando c'è bisogno di creare entropia negli algoritmi o per restituire "bit a caso"

C'è anche /dev/urandom