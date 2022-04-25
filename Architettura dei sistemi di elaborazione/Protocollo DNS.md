# DNS, Domain Main System
Il compito del DNS è quello di **mappare i nomi dei nodi nei loro indirizzi IP**.

La struttura del DNS consente una gestione semplice dei nomi:
1. **Evitando conflitti**
2. **Ottenendo buone prestazioni**

NON c'è un repository centrale, ma una **DIRECTORY DITRIBUITA** basata su uno **spazio dei nomi gerarchico** e un protocollo automatizzato.

![[albero-dns.png]]

#### Cos'è una directory?
Una directory è un elenco in cui si trovano delle informazioni e la ricerca avviene per nome. Nelle directory si fanno **molti accessi in lettura** ma pochi in scrittura.

Una directory ditribuita implica che **pezzi di questa directory sono in gestione a diversi namer server autorevoli**.

**NB**. Il processo di **"traduzione"** di un nome corrispondente viene chiamato **RISOLUZIONE**.
<br>

## DNS: lo spazio dei nomi
Lo spazio dei nomi è **GERARCHICO**. 
- In cima c'è la **RADICE**, che noi non vediamo mai.
- Ogni **sottoalbero è un dominio**

*I nomi si compongono dalla foglia alla radice (che noi non vediamo mai).*

*Esempio:*
**robot.cs.washington.edu** è la risorsa robot nel dominio cs.washington.edu, sottodominio di washington.edu, sottodominio di edu, sottodominio della radice "." che normalmente viene omessa.

I **TOP LEVEL DOMAIN (o TLD)** sono i nomi di dominio di **primo livello**, gestiti da ICANN:
- i **TLD Generici** (es. .edu, **.com**, .net) **descrivono intere categorie**, ma sono utilizzati prevalentemente negli USA
- I **Country code TLD** derivano **da una lista standard di nazioni** e sono pensati per un **utilizzo nazionale**, es. .it (alcuni di essi, es. .tv vengono commercializzati)

**NB**. All'interno di ciascun dominio ci vorrà un **name server AUTOREVOLE** che gestisca i nomi.

![[nodi-dns-2.png]]

*Le foglie della gerarchia corrispondono a dei nodi veri (server-computer), un nodo intermedio potrebbe corrispondere o meno ad un computer.*

Una **ZONA** è una **porzione dello spazio dei nomi servita da un server DNS autorevole**, di fatto **è un dominio a cui sono stati tolti i sottodomini** (delegati ad altri name server).

![[zone-dns.png]]

**Un name server può DELEGARE ad altri name server autorevoli la gestione di un sottodominio**. Questi **delegati sono a loro volta autorevoli** poichè hanno ricevuto la nomina dal root name server.

**NB**. Mentre i domini si sovrappongono, **le zone NON si sovrappongono**.
<br>

### ROOT name server
**I root name server sono 13 e sono DUPLICATI tramite meccanismo di IP ANYCAST**.

Ogni volta che qualcuno nel mondo cerca un indirizzo DNS, **il primo passo è quello di collegarsi al dnsroot**, per questo c'è bisogno che i server vengano duplicati.

##### IP ANYCAST
**Consente di avere lo stesso indirizzo IP per nodi diversi.**

Il calcolo delle tabelle di routing farà si che quando si cerca una route per X.X.X.X **si verrà portati al nodo più geograficamente vicino che ha quell'indirizzo**.
<br>

### Resource records
- **Host (A) record**: definisce la **corrispondenza tra un nome di dominio e un indirizzo IPv4**
- **A6 record**: definisce la corrispondenza tra un nome di dominio e un indirizzo IPv6
- **Pointer (PTR) record**: è utilizzato nella **risoluzione inversa**, associa a un indirizzo IP un nome di dominio
- **Alias (CNAME) record**: associa un nome di dominio ad un altro nome di dominio (es. dati.mydomain.com -> punta a -> server1.mydomain.com)
- **Mail Exchanger (MX) record**: **specifica il server SMTP di posta elettronica di un dominio**
- **Nameserver (NS) record**: è utilizzato **per definire il nameserver autorevole di una zona**
- **Start of Authority (SOA) record**: contiene tutte le informazioni sulla zona gestita dal name server autorevole
- **Service (SRV) record**: specifica un servizio attivo in un determinato dominio
- **Text (TXT) record**: utilizzato per descrivere un dominio
<br>

## Risoluzione dei nomi: procedimento RICORSIVO
![[dns-iterator.png]]

**La risoluzione dei nomi avviene con un procedimento iterativo che parte con una richiesta al root name server**.

Il root name server risponde con le indicazioni necessarie a contattare il name server autorevole del TLD, e così via a scendere nella gerarchia fino a raggiungere il name server autorevole che gestisce il record relativo al nome richiesto, e a fornire quindi l'IP corrispondente.

### DNS Locale
**Normalmente i client DNS si rivolgono a un name server locale (che nelle configurazioni casalinghe è il router)**.

*Perchè si usa avere un name server locale a inizio rete?*
**Tutti i nomi risolti (anche parzialmente) vengono memorizzati in una cache**, quindi la seconda/terza/n-volta che si cerca un sito, il router ci ritorna l'indirizzo senza passare per name server esterni.
<br>

### DNS: tipologia di protocollo
Il protocollo DNS è un semplice protocollo **domanda-risposta** che lavora su UDP.
I server sono in ascolto sulla porta 53.

**Il client invia una query, ogni query ha un proprio identificativo a 16bit. La risposta del server riporta lo stesso identificativo.**

**Il protocollo DNS utilizza l'UDP, che NON È AFFIDABILE, per ottenere l'affidabilità** si utilizza un meccanismo chiamato **ARQ (Automatic Repeat Request)**, che reinvia automaticamente la risposta.

##### CLUSTER
Un **CLUSTER sono 2 o più nodi della rete fisicamente vicini che lavorano come fossero uno**. Questi cluster possono essere utilizzati per:
- **Spartire il carico** di lavoro tra i diverso nodi del cluster
- Per creare una **ridondanza**
<br>

### DNS Spoofing
Questo attacco ha lo **scopo di inserire nella cache di un name serve locale la risoluzione fasulla di un nome di dominio**, cosìcche questo risponda con una risoluzione sbagliata.

**NB1**. L'HTTPS risolve questo attacco.
**NB2**. Per ovviare a questo attacco è nato il **DNSSEC** (la versione sicura del DNS)

##### Come funziona?
*L'attaccante chiede al server DNS chi è xxxx.it ? Lo stesso attaccante comincia a mandare la risposta con lo stesso identificativo della query iniziale. Il nameserver locale verrà così ingannato.*

### DNSsec
**Questo protocollo prevede che le risposte DNS siano firmate.**

**I client e i server dns locali devono possedere il certificato del root name server**, quindi la richiesta viene mandata al **root name serve che risponde firmando la risposta** e **inoltrando anche un certificato** (oltre alla risoluzione del nome).

Ogni nameserver risponde:
- chi è l'altro nameserver a cui chiedere
- qual è il suo indirizzo ip
- qual è il suo certificato

In questo modo **i name server locali devono conoscere solo il certificato del root name server**.