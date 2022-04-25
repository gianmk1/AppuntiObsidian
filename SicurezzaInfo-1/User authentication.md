# User authentication
Fase di autenticazione (username e password)

Principi di autenticazione:
- Qualcosa che conosciamo: password, pin
- Qualcosa di cui siamo in possesso FISICAMENTE: chiavi elettroniche, chiavi fisiche si chiamano TOKEN
- Qualcosa che fa parte di noi: impronta digitale, retina,...
- Qualcosa che facciamo: riconoscimeno vocale, ritmo della scrittura, in generale i **comportamenti** dell'utente davanti ad un sistema

## Autenticazione con password
Abbiamo un userid e una password. 

USER ID:
- determina se l'utente è autorizzato ad accedere ad un sistema
- determina i privilegi accordati all'utente
- ...

Vulnerabilità delle password, vari attacchi:
- **Offline dictionary attack**: l'attaccante compara gli hash delle password con gli hash della password più comunemente utilizzate. (molto dispendioso per CPU, SecList ha molti tool per questo). Se utilizziamo un salting (in linux è la parte tra i due $ dell hash)è più complicato arrivare alla pwd
- **Specific account attack**: l'attaccante prende di mira un target specifico e prova ad indovinare la pwd. Un meccanismo di difesa contro questo attacco è il lock dell'utente dopo vari tentativi di login sbagliati. 
- **Popular password attack**: è una variante dell'attacco precedente ma qui il target non è più singolo ma multiplo.
- **Password guessing**: l'attaccante cerca di conoscere il target e le password policy del sistema così da poter indovinare la password con più facilità. ES. creare un dizionario di pwd con informazioni relative all'utente
- **Workstation hijacking**: l'attaccante aspetta fino a quando la workstation è lasciata incustodita
- **Exploiting user mistakes**: se la pws viene generata automaticamente dal sistema l'utente l'appunterà da qualche parte e non la cambia più. Al primo login bisogna cambiare la pwd
- **Exploiting multiple password use**: utilizzare un unica password su più sistemi è molto pericoloso. Bisogna utilizzare password diversa tra di loro, con almeno 20 caratteri e possibilmente cambiarle ogni tot tempo. Utilizzare SSO (es. Accedi con Google, accedi con Facebook)
- **Eletronic monitoring**: quando la pwd passa attraverso la rete può essere sniffata da un attaccante, es. con un keylogger hardware o software. Anche se c'è la cifratura è possibile bypassarla dall'attaccante

### Password salting
![[vedi schema sulla slide]]

Quando andiamo a fare il login viene effettuata una select sul db, viene preso l hash salvato sul sistema e confrontato con quello della password con cui si sta cercando di accedere

Benefici del salting:
- Previene che password uguali siano visibili "ad occhio" nel database. Con il salting (diverso per ogni password), vediamo ogni riga diversa anche se si utilizza la stessa password
- Aumenta la difficoltà in caso di Dictionary attack: aumento numero di bit
- ...

##### Password File Access Control
Su linux password di sistema in /etc/shadow

Le hashed password sono contenute in un file accessibile **solo da un utente privilegiato**. Le hashed password sono scritte in un file **shadow file**, per separarle dal file che contiene gli USER ID

#### Strategie di password selection
Come scegliere una password, come spiegare l'importanza delle password:
- Secutiry awareness agli utenti: corsi di informazione
- Password **randomiche** generate dal computer, con cambio obbligatorio ogni tot
- **Check password reattivi**: il sistema esegue un proprio password cracker per cercare di identificare le passoword deboli e avvisare l'admin di sistema
- **Check password proattivi**: nel momento in cui un utente sceglie un pwd non è possibile sceglierne una semplice

## Autenticazione token-based

##### MEMORY CARD:
Memorizzano dati ma non elaborano, es. le vecchie carte bancarie con la solla banda magnetica:
- Richiedono un reader particolare
- La perdita di un token toglie all'utente la possibilità di accedere
- L'utente accetta un tale sistema per prelevare in banca, ma non per accedere un computer

##### SMART CARD:
A differenza delle precedenti:
- Includono un processore (es. carte di credito moderne)
- Richiedono un'interfaccia utente (tastiera, display)
- Interfaccia elettronica:
	- **Contact**: ...
	- **Contatless**: ...
- 3 protocolli di autenticazione:
	- Statico: quando l'autorizzazione viene fatta sul token stesso (es. chiavette usb con tastierino numerico)
	- Dynamic password generator: es. nei token bancari
	- Challenge - response: il server propone una "sfida" e il token genera una risposta a quest'utlima
	
La categoria di smart token più importante è la smartcard, simile alle carte di credito, hanno una CPU

Una smart card ha 3 tipi di memorie:

- ROM: memoria di sola lettura
- EEPRON: simile alla prima ma programmabile, è possibile modificare i dati all'iterno
- RAM: per i dati temporanei

##### ELETRONIC IDENTITY CARD:
Le eID sono simili alle smart card, riescono a fornire una garanzia più forte sull'identità di una persona

Contiene i seguenti dati:
- Dati personali
- numero di documenti
- CAN: 6 cifre, usate come password
- MRZ: 3 linee di testo, leggibili da macchine e umani, può essere utilizzata come password

Contine un chip NFC e della memoria

Le funzioni principali:
- **ePass**: è una funzione usata dai governi per salvare informazioni sulla persona, simile a quella dei passaporti
- **eID**: funzione generica per scopi governativi e applicativi, viene salvata l'identità
- **eSign**: serve per firmare dei documenti, all'interno della card c'è una chiave privata e un certificato

## Autenticazione biometrica
Possiamo utilizzare delle caratteristiche fisiche "nostre" :
- caratteri facciali
- imponte digitali
- retina
- iride
- geometria della mano
- firma
- voce

Caratteri facciali: fotografata la faccia e calcolate varie distanze tra occhi, bocca, naso,... Può essere integrata anche il sistema vascolare tramite una particolare fotocamera. 
*Es*. iPhone fa una mappatura in 3D

Impronte digitali: vengono utilizzate spesso nei telefoni ed è il primo sistema di identificazione per le forze dell'ordine. 

Geometria della mano: viene calcolata la dimensione, distanza tra le dita, lunghezza delle dita,...

Retina: fotocamera con fascio infrarosso a bassa intensità, la fotografia del reticolato della retina diventa la nostra pwd

Iride: riconoscimento della geometria dell'iride

Firma: salvando molti sample di firma in un algoritmo

Voce: la voce è un altro elemento univoco, viene registrata da un microfono per calcolare l'intensità, velocità di dizione e altre particolarità

![[inserire grafico cos-accuracy]]

NB. L'iride è quello più accurato ma anche il più costoso

... inserire gli altri schemi

#### Sovrapposizione impostore/utente
![[inserisci schema slide]]

C'è possibilità che in base alla luce, alla polvere, ecc. non riusciamo ad accedere seppur autorizzati. Stessa cosa può accadere al contrario, un attaccante cammufandosi può essere verificato come utente genuino.

NB. CyberChef è un tool sviluppato dai servizi inglesi 

# 21  gennaio 2022

## Autenticazione remota
### password protocol
L'autenticazione con password per sistemi remoti avviene tramite protocolli **challenge-response ???**.

I protocolli sono cambiati nel tempo, ma il funzionamento logico è lo stesso:
1. Utente invia la propria identità all'host
2. L'host genera un numero casuare **r** chiamato **nonce (= number once)**, e lo invia al utente, l host definisce anche due funzioni h e f e le comunica all'utente
3. L'utente fa una funzione (una stringa)
	*Vedi slide*
	Viene fatto il prodotto del numero casuale, l'hash della password e inviato il server
4. Inviato il risultato il server rifà le stesse operazioni (con r l'hash della psw e la funzione utilizzata), se il prodotto è uguale, l'utente è autenticato

*Vedi schema slide*
	

## Problemi di sicurezza nell'autenticazione

# 01 febbraio
