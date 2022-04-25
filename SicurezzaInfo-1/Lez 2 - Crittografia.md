## Crittografia Simmetrica
La **crittografia simmetica** è la cifratura più utilizzata poichè più semplice, più veloce e richiede meno potenza computazionale.

Questo tipo di critttografia richiede 5 elementi:
- **plaintext**: il testo in chiaro
- **encrypt algorithm**: algoritmo di cifratura
- **secret key**: chiave per la cifratura (password)
- **cipher key**: testo in outpit dopo aver applicato l'algoritmo di cifratura
- **decrypt algorithm**: algoritmo di decifratura

Per un utilizzo sicuro:
- *Utilizzare un algoritmo forte*
- *Una secret key **condivisa***

Esistono **2 tipologie di attacco** per la crittografia simmetrica:
1. **Crittoanalisi**: consiste nello studio dell'algoritmo di cifratura, capire come il testo viene trasformato
2. **Brute-Force**: provare una serie di combinazioni finchè non trovo quella che mi ritorna il risultato corretto (dispendioso per tempo e risorse)

La cifratura simmetrica si divide in:
- **A BLOCCHI**: gli algoritmi di cifratura a blocchi sono i più diffusi, il **plain text viene diviso in blocchi di lunghezza fissa**, un esempio sono **AES** e DES.
	- Più lenti rispetto quelli a flusso
	- La velocità di cifratura cambia a seconda della lunghezza della chiave
	- **NB.** L'algoritmo **DES Singolo** è insicuro poichè la chiave è di soli **56bit**
- **A FLUSSO**: l'algoritmo cifra gli elementi in input continuamente, vengono utilizzati per lo **streaming audio / video**
	- L'input viene cifrato continuamente al momento, tipicamente **1 byte per volta**

## Cifratura Asimmetrica
La **crittografia asimmetrica** consiste nell'utilizzo di **due chiavi**, una **pubblica** e una **privata**.

##### Funzionamento
1. Ogni utente genera una **coppia di chiavi**
2. **Una delle chiavi viene caricata in un repository pubblico**, questa è la chiave pubblica. La chiave complementare viene tenuta dal mittente, questa sarà la chiave privata
3. Se Bob vuole mandare un messaggio ad Alice, **Bob cifra il messaggio con la chiave pubblica di Alice**
4. Quanto **Alice riceve il messaggio lo decripta con la sua chiave privata**. Nessun altro può leggere il messaggio

**NB**. Questo meccanismo **solitamente** viene utilizzato **per verificare l'identità del destinatario**.
**NB2**. **Posso anche inviare un messaggio criptato con la mia chive privata**, in questo caso però i possessori della mia chiave pubblica potranno leggere il messaggio, in questo caso non si spediscono informazioni troppo private.

# Message Authentication
L'autenticazione dei messaggi ci aiuta contro la falsificazione dei dati, **garantisce quindi l'autenticità di un messaggio** e che la sorgente sia autentica.

La **sola crittografia simmetrica NON può garantire l'autenticità dei dati**.
(mentre la sola autenticazione senza cifratura NON garantisce la confidenzialità)

Solitamente vengono utilizzate 2 tecniche:

#### 1. Message Authentication Code (MAC)
Questa tecnica per la *Message Authentication* consiste nell'**utilizzare una secret key per generare un blocco di dati**.
- Fornisce **autenticazione e integrità**.
- **NON sono funzioni reversibili**

*A deve inviare un messaggio a B, calcola il MAC come funzione le cui variabili sono il messaggio e la secret key: MAC = F(K + M), il MAC viene accodato al messaggio e trasmesso. B ricalcola il MAC con la stessa secret key e lo compara con quello ricevuto.*

Il processo è simile a quello visto per la cifratura, qui però l'algoritmo di autenticazione NON può essere reversibile. 

**HMAC sono implementazioni del MAC con funzioni di hashing** (SHA, MD5,...)

#### 2. Funzioni di hashing one-way
**Ricevono in input messaggi di lunghezza variabile** e **restituiscono una stringa**, chiamata **DIGEST**, di **lunghezza fissa**.

A differenza del MAC, con le funzioni di hashing non abbiamo bisogno di una secret key.

*Ecco alcuni esempi di implementazione del digest:*
- Autenticazione di messaggi tramite digest cifrati con **cifratura simmetrica**
	1. Messaggio dato input a funzione di hashing
	2. Digest risultante combinato con secret key
	3. L'insieme viene dato all'algoritmo di cifratura
- Autenticazione di messaggi tramite digesti cifrati con **cifratura asimmetrica**
- Autenticazione di messaggi tramite digest del messaggio **concatenato ad una secret key** 
	- Qui è impossibile all'hacker risalire alla secret key, se non alterando il messaggio

Alcune considerazioni:
- Le funzioni di cifratura sono LENTE, percui si prediligono funzioni di hashing
- L'hardware per la cifratura è ottimizzato per grandi quantità di dati
- Gli algoritmi di cifratura potrebbero essere coperti da un brevetto

**NB**. **SALTING**: se il sistema alla mia password accoda qualche *salt* diventa più complicato risalire alla password tramite hash. 

# Funzioni di hashing
Sono **funzioni matematiche che NON permettono di tornare al messaggio originale** una volta calcolato il digest.

*Una funzione di hash produce una **fingerprint** di un file, messaggio, ...*

##### Proprietà necessarie ad una funzione di hash (H):
1. H può essere applicata a **blocchi di dati di qualsiasi lunghezza**
2. H **produce una stringa di dimensioni fisse**
3. H(x) deve essere **di semplice computazione** per qualsiasi x
4. Deve essere impossibile, dato l'input, ritornare al risultato
5. **Resistenza alle Collisioni (Deboli e Forti**

**NB**. Queste funzioni però hanno una **combinazione FINITA**, c'è quindi il **RISCHIO di COLLISIONE**, cioè 2 input diversi ritornano lo stesso hash.

NB1. Le prime 3 proprietà servono per garantire la Message Authentication
NB2. La quarta proprietà è necessaria nel caso si utilizzi una secret key
NB3. La quinta proprietà garantisce che sia impossibile trovare un altro messaggio con lo stesso digest originale

##### Altre applicazioni degli hash:
- **Password**: calcolato l'hash, questo viene salvato nel DB. Al login si calcola l'hash della password immessa dall'utente e si confronta l'hash ritornato con quello salvato nel DB
- **Intrusion Detection**: confrontiamo il digest di un file sospetto con quelli di malware conosciuti. In questo modo possiamo anche monitorare e bloccare il traffico appena troviamo un hash sospetto

# Algoritmi di Cifratura Asimmetrica
### RSA
- Funziona con **cifratura a BLOCCHI**
- È l'algoritmo più conosciuto
- Oggigiorno vengono usate **chiavi di almento 1024bit**

### Diffie-Hellman
- Utilizzato SOLO **per lo scambio di chiavi**
- *In realtà fa parte degli algoritmi di cifratura simmetrica*

# Firma digitale
La crittografia asimmetrica può essere utilizzata per fornire autenticazione con una tecnica chiamata **Digital Signature**, cioè: *il risultato di una trasformazione crittografica di dati che fornisce un meccanismo per verificare **autenticazione**, **integrità** e **non-repudiation***.

NB. Questo metodo garantisce che il blocco dati è stato firmato dal firmatario indicato e che non è stato alterato dal momento della firma.

##### Alcuni algoritmi di Digital SIgnature:
- **Digital Signature Algorithm** (**DSA**)
- **RSA Digital Signature Algorithm**, basato sull'RSA
- **Elliptic Curve Digital Signature Algorithm**

#### Funzionamento:
*Mittente:*
Bob invia un messaggio ad Alice. Bob usa una funzione di hash per **generare il digest** del messaggio, questo **digest insieme alla chiave privata di Bob sono dati in input all'algoritmo di firma**. Il risultato, che è la **firma**, viene **concatenato alla fine del messaggio**.

*Destinatario:*
Alice riceve il messaggio e la firma. **Calcola l'hash (digest) del messaggio** e lo da in input, insieme alla chiave pubblica di Bob, all'**algoritmo di firma digitale**.
L'algoritmo restituisce se la firma è valida o meno, Alice in questo modo **riesce a capire se il messaggio è autentico**.

**NB**. In questo caso il messaggio NON è cifrato.

# Key Management
## Certificati a chiave pubblica
La **chiave pubblica deve essere trasmessa o condivisa**, chiunque però potrebbe fare una annuncio di questo tipo, rubando l'identità di Bob.

I **certificati a chiave pubblica** accoppiano una chiave pubblica ad un **UserID**. Questo blocco di dati viene **firmato da una terza parte di fiducia**.
Questo certificato contiene anche il **periodo di validità** dello stesso.

La terza parte che emette il certificato si chiama **Certificate Authority** (**CA**).

#### Funzionamento:
1. L'utente crea una coppia di chiavi
2. L'utente prepara un certificato NOn firmato che include UserID e chiave pubblica
3. L'utente invia il certificato alla CA, questa:
4. La CA firma il certificato:
	1. Calcola l'hash del certificato (non firmato)
	2. **Firma il certificato con la propria chiave privata**
5. La CA concatena la firma al certificato non firmato per **produrre il certificato privato**.
6. La CA invia il certificato firmato all'utente
7. L'utente può adesso inviare il proprio certificato agli altri
8. Gli altri utenti possono verificare la validità del certificato:
	1.  Calcolando l'hash del certificato (senza firma)
	2.  Verificando la firma con la chiave pubblica della CA


