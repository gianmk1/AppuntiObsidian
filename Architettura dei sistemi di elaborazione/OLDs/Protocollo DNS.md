# Protocollo DNS (Domain Name System)
![[presentazione non ancora disponibile]]

... *system* -> è quindi composta da più parti

È un sistema articolato il cui compito è quello di **mappare i nomi dei nod nei loro indirizzi IP.**

La struttura DNS consente una gestione semplice dei nomi:
1. **evitando conflitti**
2. **ottenendo buone prestazioni**

**NON c'è un repository centrale**, nel quale sono elencati tutti i nomi dns. Come invece c'era quando è nato internet.

C'è invece una **directory distribuita**, basata su uno spazio dei nomi gerarchico e un protocollo automatizzato.

##### Cos'è una directory?
Una directory è un elenco in cui si trovano dell informazioni, dove la ricerca la si fa per nome. La caratteristiche della directory è che si fanno **molti accessi in lettura** ma pochi in scrittura.

Una directory distribuita implica che **pezzi di questa directory sono in gestione a diversi name server autorevoli**.**

**NB.** Il processo di "traduzione" di un nome nel corrispondente indirizzo si chiama **RISOLUZIONE**.

![[immagine dello spazio dei nomi]]

Lo spazio dei nomi è **gerarchico**. In cima c'è la **RADICE**, che noi non vediamo mai.

*Nei nomi DNS prima vediamo la "foglia" e a salire la gerarchia dei nomi (alberi)*

#### DNS: lo spazio dei nomi
I **TOP LEVEL DOMAIN** sono i nomi di dominio di primo livello, questi sono gestiti da ICANN.

- I **TLD generici** descrivono intere categorie, ma sno utilizzati prevalentemente negli USA. es. .com / .net 
- I **country code TLD** derivano da una lista standard di nazioni e sono pensati per un utilizzo nazionale. es. .it / .uk
	- Alcuni di essi (es. .tv delle Isole Tuvalu) sono commercializzati all'esterno

Poi ci vorrà un **name server AUTOREVOLE** che gestisca i nomi all'interno di un dominio.

NB. **DNS Spoofing**: consiste nel reindirizzare qualcuno in un serve sbagliato.

<br>
<br>

![[immagine gerarchia dns laboratorio kathara]]

*Le foglie della gerarchia corrispondono a dei nodi veri (computer), un nodo intermedio potrebbe corrispondere ad un computer come no. 
I domini sono degli sottoalberi, i domini si sovrappongono gli uni gli altri.*

Ogni **ZONA** è servita da un name server autorevole (**dnsroot**), e questo può delegare ad altri nameserver autorevoli a gestire il sottodominio in questione (es. *org*). Conseguentemente sotto *.org* ci sono altri migliaia di sottodomini. Il nameserver del dominio *.org* delegerà a sua volta ad altri nameserver autorevoli.

**ZONA**: è una porzione dello spazio dei nomi gestita da un nameserver autorevole, e di fatto è un dominio a cui sono stati tolti i sottodomini delegati ad altri.

##### root nameserver
**I root nameserver sono 13 e DUPLICATI con un meccanismo di IP ANYCAST**

*NB. Ogni volta che qualcuno al mondo cerca un indirizzo dns, il primo passo è quello di collegarsi al **dnsroot** per questo c'è bisogno che i server vengano duplicati.* 

**IP ANYCAST** consente di avere lo stesso indirizzo IP per nodi diversi. In quale modo il calcolo delle tabelle di routing farà si che quando si cerca una route per x.x.x.x si verrà portati al nodo più geograficamente vicino che ha quell'indirizzo.

## Ripasso...

**NB.** Lo spazio dei nomi ha una struttura gerarchica e su questa gerarchia sono appoggiati i nameserver autorevoli. I rootname server sono molti, e alcuni di essi sono duplicati utilizzando la tecnica dell'**IP anycast**.

Il **root nameserver** delega ad altri nameserver **autorevoli** i **SOTTODOMINI**. Questi sono detti **autorevoli** perchè hanno ricevuto la nomina dal root nameserver. A loro volta i nameserver del dominio di 1o livello **delegano**.

Una **ZONA** è un albero privato dei sottoalberi, che sono stati affidati ad altri nameserve autorevoli.

<br>
<br>

### Resource Record
- Host (A) record : I resource record definiscono una corrispondenza tra un nome di dominio e un indirizzo IPV4.

Alias (CNAME) record
Definiscono degli alias

Mail Exchanger (MX) record

##### completare ...



#### DNS iterator
Noi normalmente, per risolvere i nomi, non ci affidiamo a un nameserver autorevole. 

Normalmente nelle configurazioni casalinghe i router fanno anche da nameserver locali, quando avviamo il procedimento di risoluzione dei nomi il device chiede al router. Questo è un **nameserver locale**.

Un **nameserver locale** non memorizza nessun record. Ma va al root nameserver che risponde restituendo il nome e l'indirizzo di un altro nameserver (es. quello delegato alla zona .it) , a questo punto si ripete la domanda e probabilmente verrà restituito nome e indirizzo di un altro nameserver che saprà dirci l'indirizzo del nome cercato.

![[inserisci slide]]

**NB**. Perchè si usa avere un nameserver locale a inizio della rete?
Tutti i nomi risolti (anche quelli parziali) vengono memorizzati in una cache, quindi la seconda/terza/... volta che si cerca un sito il router ci ritorna l'indirizzo senza passare per nameserver esterni.

### Tipologia del protocollo
Il protocollo DNS è un protocollo **domanda-risposta**. Viene utilizzato il protocollo UDP, che è NON affidabile, per ottenere la affidabilità nel protocollo dns si utilizza un meccanismo chiamato ARQ il cui fondamentalmente: *mando una domanda -> non ottengo risposta -> rimando la domanda*. La query dns contiene un identificatore, e la risposta la lo stesso identificatore.

<br>

**CLUSTER**
Un cluster sono due o più nodi della rete fisicamente vicini, che lavorano come fossero uno. I cluster possono essere utilizzati per:
- Spartire il carico di lavoro tra i diversi nodi del cluster
- Per ridondanza

Un esempio è quando abbiamo 4 webserver uguali e il carico (le richieste) viene ridistribuito su tutti e 4.

### DNS spoofing
Consiste nel cercare di inserire nella cache di un nameserver non autorevole (es. locale) una risoluzione fasulla, che faccia si che questo risponda con una traduzione sbagliata.
L'attacco si fa solitamente su un nameserver locale cosicchè tutti i client che si collegheranno a un server fasullo.


NB. L'https risolve questo attacco.

***Come funziona?***
*L'attaccante chiede al server DNS chi è? xxxx.it . E lo stesso attaccante comincia a mandare la risposta con lo stesso identificativo della query iniziale. Il nameserver locale verrà così ingannato.*

Per questo attacco è nato il **DNSSEC**, cioè la versione **sicura** del protocollo dns.


## DNSSEC
Questo protocollo **prevede che le risposte siano FIRMATE**. I client e i dnslocali devono possedere il certificato del root nameserver, quindi la richiesta viene mandata al root nameserver che risponde firmando la risposta, inoltrando anche un certificato (e non solo la risoluzione del nome).

Ogni nameserver risponde:
- chi è l'altro nameserver a cui chiedere
- qual è il suo indirizzo ip
- qual è il suo certificato

*L'ultimo nameserver risponderà con la risoluzione dell'indirizzo.*


