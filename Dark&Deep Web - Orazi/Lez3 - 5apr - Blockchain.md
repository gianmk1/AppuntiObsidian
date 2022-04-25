# Blockchain
Ci sono 3 etimologie che vengono date alla parola **blockchain**:
1. Associata alle cryptocurrency
2. Architettura/codice che sta sotto una specifica valuta
3. Idea di blockchain in generale

*Qual è lo scopo principale della blockchain?*
Quello di **rimuovere intermediari**: far fare al codice quello che solitamente viene fatto da terzi. -> Delegare quindi ad **una macchina** per creare una **catena della fiducia**.

*Es. notaio*

### Terminologie
- **Blockchain** è l'esempio perfetto di **sistema distribuito**.
- **DLT**, **Distributed Ledger Technology**
- **Ledger** è un **registro che contiene tutte le transizioni che vengono fatte**, ed è **distribuito**, ognuno ha una copia di questo. Chiunque abbia questo database può aggiungere dati a questo ma **NON può modificare o rimuovere dati**.
- La blockchain è basata su una **rete p2p** con aggiunta di **crittografia e API**

La blockchain può essere applicata in moltissimi contesti:
- l'utilizzo più comune è quello delle **cryptocurrency**
- c'è una **copia del registro in ogni nodo di chi si aggiunge in questo network**, abbiamo quindi un **sistema REPLICATO**
- database aggiornato in "real-time"
- sono presenti **sistemi di crittografia**
- **Chiunque può scrivere nella blockchain**, a condizione che faccia parte del network. NB. Ci sono anche delle architetture private dove c'è bisogno di un login
- **Tutti possono leggere il LEDGER (registro)**
- Ci sono molti meccanismi che **rendono molto difficile modificare il ledger**

### Ledger distribuito
![[inserire immagine]]

*A sinistra un sistema centralizzato, a destra uno distribuito.*

**NB1**. Nel sistema centralizzato, tutti fanno a capo ad un unico database (si possono fare backup) ed è quindi un **single point of failure**.

**NB2**. Nel sistema distribuito, NON c'è un entità centrale che controlla il ledger. È possibile **aggiungere un record al ledger SOLTANTO mediante consenso di tutti gli utenti della rete**.

### Blocchi di funzionamento
1. Un utente inizializza una transazione: fa presente che vuole fare una transazione e ci mette la propria **firma digitale**
2. Invio della richiesta in **broadcast**, a tutti gli altri utenti della rete.
3. Uno o più nodi della rete **validano** la richiesta fatta.
4. Aggregazioni di varie richiestein blocchi
5. Invio del blocco al registro
6. Tutti gli utenti "accettano il blocco"
7. Il blocco è a questo punto parte della blockchain

NB. Non viene mai processata una singola transazione, ma si **lavora per BLOCCHI**, gli utenti cercano di validare più transizioni insieme **creano un BLOCCO** che verrà aggiungo al registro.

### Blocchi
Un **BLOCCO** è un **insieme di transizioni**, dove è presente un **puntatore al blocco precedente**, le richieste e **proof of work**.

### Mining
Il **MINING** è il **processo di validazione**, consiste nel risolvere problemi crittografici, utilizzando il proprio hardware, per validare una serie di transizioni velocemente, cosí da **inviare velocemente** il blocco alla blockchain.

Un miner va a prendere da un **pool di transizioni non confermate** una serie di transizioni, le verificare, le aggrega in blocci e lo manda all'interno della rete.

**NB**. L'**ORDINE è importante**. Le transizioni prese dal pool però vengono prese in maniera casuale.

C'è una **corsa a chi computa prima il blocco**, chi finisce per primo "vince".

Nel momento in cui un miner verifica e valida le transizioni, nel momento in cui il blocco viene validato dalla rete, il **miner viene rincompensato**.

**NB**. Solitamente un miner si sottoscrive a community di miner (**POOL**) e tutti insieme, mettendo a disposizione la loro potenza computazionale, **cercano di risolvere il prossimo blocco (il prima possibile)**.

### Utenti
- Utente normale, chi sta nella blockchain e ha semplicemente una copia del registro
- Miner, che cerca di validare le transizioni. Ovviamente anche il miner fa parte della rete e ha una copia del ledger

### Transazioni
**NON tutte le transazioni hanno lo stesso peso**, alcune danno più remunerazione di altre.

## FORK
**NB**, GIT è un sistema che server per manuntenere il codice.

Un **FORK è una diramazione**. 

Può succedere che a un certo punto ci sia un fork: qualcuno addiunge al proprio ledger una transazione che non viene riconosciuta da altri ledger, si crea quindi una **SCISSIONE**.

*Es. dogecoin deriva dal lightcoin, successivamente dal luckycoin, ...*

*Quando succede?*
- Questo può succedere anche quando un **blocco viene trovato nello stesso momento**.
- **Software incompatiblity**, viene rilasciata una nuova versione di bitcoin e io decido di rimanere con la vecchia
- Decido di creare la mia criptovaluta: mi stacco, prendo ciò che c'era prima, e da questo creo la mia nuova criptovaluta

### **Duple Spending Problem**
È un **attacco che sfrutta la vulnerabilità per cui i blocchi possono venire creati nello stesso momento**.

Tutti devono convenire nel **prossimo blocco** che deve essere integrato nella blockchain.
Se ci sono **2 blocchi paralleli validi**, in entrambe le parti la serie continuerà, e uno dei 2 sarà più veloce nel procedere (e quindi validare i blocchi) rispetto all'altro.

Per questo si aspetta la **validazione di 6 blocchi consecutivi** per **definire la transazione valida**, si reputa quindi **"infallibile" la caduta di questo fork** che è arrivato a 6 blocchi consecutivi.

*vedi video presente nelle slide*

**NB.** Ci possono essere più pool da cui vengono prese le transizioni non ancora valide.

## Bitcoin
- La prima cryptovaluta ad utilizzare la blockchain
- Create nel 2008
- Utilizzata per compra-vendita di materiale illegale
- Viene fatta anche **speculazione**

**Considerazione**. C'è una speculazione così tanto alte che è molto pericoloso investire in bitcoin ora.

Nakamoto voleva, col bitcoin, dare un sistema di pagamento elettronico, rimuovendo tutti gli intermediari terzi, sostitutendole con un'architettura su cui tutti quanti si fidano.

Nel 2009 è stato minato il primo blocco, che valeva 50bitcoin.
- Ogni **210.000 blocchi** la **reward** del miner **viene dimezzata**.
- Ci possono essere al massimo **21 milioni di bitcoin**, arrivati a questo massimo **NON si immetterà più moneta**. Questo per ovviare al meccanismo di inflazione.
- Si stima che nel 2040 si arriverà al punto accennato sopra

## Composizione di un blocco bitcoin
1. Puntatore al blocco precedente
2. Richieste validate
3. Proof of work

Ma all'interno del blocco c'è anche:
1. **HEADER**
2. **CONTEGGIO DELLE TRANSIZIONI**
3. **CONTENUTO DEL BLOCCO**
	1. **Coin base transaction**, prima transazione del blocco che il miner fa, poichè la sua reward: **somma tra la mia reward è il valore totale di tutta la chain**.
	2. **Transazioni bitcoin**

NB. La generazione di moneta avviene solo quando viene inserito nella blockchain un nuovo blocco.

### Header
- Lunghezza
- Dimensione
- Time stamp di quando è stato immesso il blocco
- Somma delle varie transazioni nel blocco
- Hash, per identificare il blocco
- Versione dello standard bitcoin
- **Puntatore al blocco precedente**
- **Merkle root**

##### Merkle Root
È un **modo per verificare l'integrità del blocco**. Un miner può fare un checksum per verificare che il blocco che io scarico nel ledger locale sia integro, corretto.

Il **merkle root** è un meccanismo col quale si riesce a fare il checksum su tutte la transazioni del blocco.

###### Funzionamento
**NON si può tenere un hash per ogni singola transazione**, quindi si crea una struttura ad albero accoppiano 2 hash per volta. Nel caso ci sia una disparità, viene **replicato l'hash**, e si fa l'hash seguente su i 2 replicati.

### Contenuto del blocco
1. Prima transazione, in favore del miner
2. Transazione normale

**Se perdo l'identificativo di una transizione**, perdo quei bitcoin associati a quella transizione.

**Io conosco solo DOVE sono le MIE TRANSAZIONI**, il **mio wallet**.

![[immagine blocco]]

## How money transfer work in BTC?
![[immagine sequenza trasferimento denaro]]

**NB**. Il ricevente è sicuro di aver ricevuto i soldi quando sono state verificate altri 6 blocchi.

<br>
<br>

## Etherium
- Non soltanto una cryptovaluta
- Creata da Vitalik Buterin
- Prima vera moneta che ha raggiunto, in breve tempo, la linea d'onda del bitcoin
- **Decentralised app platform (dapps)**
- Basato su **EVM**, cioè Etherium Virtual Machine
- La crypto si chiama ETH

Può essere usato anche per **SMART CONTRACT**: 
Tradizionalmente un contratto viene definito, controllato e certificato, ed eseguito.

*Ci sono tante entità, tanti punti di failure*.

Utilizzando un sistema di smart contracting su base etherium:
1. Definizione, il contratto non viene più scritto, ma è codice che deve essere eseguito
2. Controllo, fatto automaticamente dalla rete (o miner)
3. Esecuzione, sostituita banale esecuzione di codice

Un contratto a questo punto **NON è REVERSIBILE**, **è IMMUTABILE**.

### Databases VS blockchain
![[immagine differenze database-blockchain]]

**NB**. Ownership nella blockchain è di tutti.

## Crittografia nella blockchain
Ci sono 2 forme di crittografia utilizzate nella blockchain:
- Hashing
- Digital signature

3 sono le fomre di encryption che vengono ampliamente utilizzate:
- Crittografia simmetrica, 2 ways function
- Crittografia Asimmetrica
- Hashing

<br>

## Meccanismi di consenso
**Byzantine Fault Tolerance**: quando abbiamo un sistema in cui c'è possibilità in cui dei componenti possano fallire, la byzantine fault tolerance ci dice **quanto possiamo resistere** nel caso avvengano errori i attacchi.

Solitamente si utilizza il meccanismo **proof of work** per **cercare di dare una direzione globale univoca di quanto scritto nel ledger**.

### Blockchain consensus algorithms
- Ogni cryptovaluta può utilizzare un algoritmo di consenso diverso. Non è obbligatorio includerlo, ma non facendolo la fault tolerance diminuisce drasticamente.

Diverte tecnologie:
- **Proof of Work**, usato quotidianamente
- Proof of State

### Proof of Work
È il **meccanismo che si utilizza oggi per fare in modo che i miner non siano in grado di compromettere a tal punto la rete**, tale da controllare il flusso.

Questo si traduce in dei calcoli supplementari dati al miner, in modo che questo non riesca a controllare più del 49% della rete.

Controllando più del 51%, un'entità (miner) potrebbe **cercare di compromettere un blocco e immetterlo nel ledger principale**, facendo così in modo che tutti gli altri lo inglobino nella proprio ledger.

**NB.** Questo dovrebbe essere impedito dalle **funzioni di hash**, ma oggigiorno siamo arrivati al punto per cui un hacker potrebbe essere in grado di compromettere un blocco ricalcolando tutte le hash di tutti i blocchi precedenti. Il **proof of work**, cioè richieste computazionali addizionali, permettono di evitare ciò.

Anche la **proof of work** è un'hash function, il miner cerca di fare reverse e fornisce in seguito la risposta: se questa è giusta viene dimostrato che il miner ha lavorato effettivamente nel blocco.

Questo **OVERHEAD generato appositamente** rende quasi impossibile per il miner fare reverse di molti blocchi e, allo stesso tempo, calcolare la proof of work.


### Proof of Stake
Devo dimostrare di avere a disposizione un tot di cryptovalute (in questo caso) per poter minare. Questo fa in modo che sia molto più dispendioso controllare più del 51% della rete, poichè per fare ciò devo avere molte monete.

Questo meccanismo rende molto più difficile generare community che cooperano.

<br>

### Strutture della blockchain
Diversi client (che sono allo stesso tempo anche admin) identificati tramite uno pseudonimo. 

### Tipi di blockchain
- **Pubblica**, il controllo è decentralizzato e tutti possono partecipare.
- **Private**, c'è un sistema proprietario, un'organizzazione amministra la rete e che fornisce i permessi per leggere/scrivere dentro la blockchain.
- **Consorzio o blockchain federale**, come la private ma ci sono più entità che controllano (cioè che fanno admin), quindi una **federazione**.
<br>
<br>

### Smart Contract
Uno **smart contract** è un **smaterializzazione dei contratti classici**. Il classico contratto viene traslato in codice, generato in modo tale che sia semplice verificare il contratto, senza l'utilizzo di intermediari.

Lo smart contract è **tracciabile** e **irreversibile**.

Contratto scritto -> CODICE

##### Architettura DAO
![[immagine traduzione contratto]]
*Abbiamo una lista di controlli da fare (**clausole**), con eventuali condizioni e conseguenze.*

**DAO**, Decentralized Autonomous Organization: il primo esempio in larga scala dell'utilizzo di smart contract, era un sistema per avere un fondo comune.

*Come funziona?*
Nella fase iniziale l'investitore versa denaro nel fondo comune, il fatto che io immetta questa moneta nel DAO, fa in modo che in futuro (quanto il fondo sarà abbastanza espanso) avrò potere di voto. Quando siamo pronti ad investire, si applica un principio per cui, chi più ha investito, più la sua idea su dove investire ha peso.
Nella DAO furono raccolti più di 150milioni di dollari, da 11k membri. Tutto questo fu architettato e mantenuto da un programma, nessuna entità fisica è riuscita a cambiare il funzionamento del contratto.

**NB**. Nel 2016 c'è stato un attacco per cui un hacker è riuscito a tirare fuori più di 3 milioni di dollari e a metterli in un fondo parallelo. Il problema fu nel design dell'architettura.

Anche se l'architettura può essere sicura e decentralizzata, in realtà, qualsiasi blockchain che utilizziamo è CODICE che ha problemi / bug / ...

##### Possibili applicazioni degli smart contract
- **Lotteria**
- **Gestione condivisa di un portafoglio**, es. una transazione prima di essere emessa deve essere approvata da almeno 2/3 componenti di un wallet.
- **Gestione dell'eredità**
- **Transazioni firmate da almeno 3 device**
<br>

### Alcuni esempi smartcontract nella blockchain
- **ERC-20**, basata su ethereum, in grado di definire una lista comune di regole da seguire nel caso si volesse generare un nuovo token etherium. Permetteva agli sviluppatori di delegare la generazione del token.
- **ERC-721**, basata su ethereum, risolveva i problemi di ERC-20
- **ERC-725**, un altro standard che serviva per identificare un'entità all'interno della blockchain. Poteva descrivere persone, gruppi, oggetti e macchine.