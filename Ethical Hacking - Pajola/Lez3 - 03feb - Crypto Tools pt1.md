# Tool di crittografia pt.1

Cifrari: ogni lettera veniva mappata con un'altra lettera.
La crittografia è uno dei rami più importanti della cybersecurity.
Andremo a vedere algoritmi simmetrici, asimmetrici e hash function.

Bisogna utilizzare dei metodi sicuri di comunicazione

plain text = testo in chiaro
alg di encryption = funzioni che ci permettono di rendere sicuro il messaggio
key = password

### Symmetric Encryption 
![[vedi schema slide]]

L'unico modo per vedere il contenuto originale è quello di utilizzare lo **stesso algoritmo usato dal mittente e la stessa chiave**

Per utilizzare un algoritmo simmetrico la chiave deve essere **comune**

Si può cercare di decifrare il messaggio (non conoscendo la chiave) tramite:
- **bruteforce**, soluzione "stupida".
- **criptoanalisi**, identificare delle possibili vulnerabilità dell'algoritmo di crittografia

NB. Botnet: master + zombie, il master infetta delle macchine che poi contribuiranno per fare bruteforce

Solamente aggiungendo un bit alla chiave, la complessità del brute-force cresce a dismisura.

Ci sono 3 tipi di cifrari simmetrici molto famosi: **DES**, **AES**, **Triple DES**.
**DES era uno dei primi cifrari, si utilizzavano 64bit di plaintext block e 56bit di chiave**, questo algoritmo non era molto sicuro, quindi si decise di applicarlo 3 volte: **Triple DES**

Esistono cifrari:
- A blocco, converte in plain text prendendo un blocco per volta
- Stream ciphers: può essere o a caratteri o a blocchi, **solitamente si cifra un singolo bit per volta**, **ogni digit è criptato con il corrispondente della chiave**

## Cifrario di Cesare
Ogni lettera del testo in chiaro è sostituita, nel testo cifrato, dalla lettere che si trova un certo numero di posizioni dopo nell'alfabeto

### Tool cryptographic: XOR
Operazione booleana:

0 xor 0 = 0
0 xor 0 = 1
1 xor 0 = 1
1 xor 1 = 0

Ha alcune proprietà:
- è una **operazione reversibile**
- gode delle proprietà **associativa e suriettiva**

Lo XOR di 2 interi è il risultato dello **xor tra le loro rappresentazioni binarie**

#### XOR - Kasiski Elimination
È un modo per rompere tutti i cifrari con lo xor. Si basa sul fatto che con un messaggio abbastanza grande

Quando si ragiona a blocchi e con lo xor, possono esserci delle ripetizioni di caratteri sul plain text che hanno la stessa identica chiave. (più è corta la chiave più è probabile che ciò accada)

Individuando le sequenze ripetute si può dedurre la lunghezza della chiave
