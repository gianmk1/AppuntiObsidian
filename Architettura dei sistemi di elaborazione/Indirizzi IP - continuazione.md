# 24gen Indirizzi IP - continuazione
## Indirizzi IP privati (not routable)
Un indirizzo IP privato sta all'interno dei seguenti intervalli:
- ...
- ...
- ...

## Primo livello di routing
Ogni interfaccia di rete deve conoscere il proprio indirizzo ip e prefisso (= maschera di sottorete) e gli end node devono conoscere l'indirizzo IP del loro default gateway (che deve appartenere alla stessa rete fisica)

Si confronta la parte dell'indirizzo IP di destinazione con la propria rete, se sono uguali la destinazione è direttamente raggiungibile a livello 2, altrimenti il pacchetto viene inoltrato sul default gateway.

Il pacchetto deve sempre uscire dalla stessa scheda di rete che l'end node ha, quindi si deve determinare qual è l'indirizzo di livello 2 del destinatario, questo viene fatto con il **protocollo ARP**

## Invio di un pacchetto IP su rete Ethernet
Se l'indirizzo di destinazione appartiene ad un altra rete manderò i dati al gateway, dovrò quindi trovare il suo indirizzo MAC

## Aggregazione di prefissi IP
I router dei provider/dorsali ecc. non possono lavorare con il default-gateway, dobbiamo sapere esattamente verso dove instradare, dobbiamo avere un elenco di reti e per ciascuna il gateway a cui instrdare i pacchetti, di conseguenza ci vuole una regola per ogni rete.

Anche una regola per ogni rete però è impensabile, per questo gli indirizzi ip vengono **aggregati e disgregati**:

![[scheda slide]]

*Si maggina un'organizzazione che ha a disposizione un gruppo di indirizzi IP 128.208.0.0/16, questo viene suddivisono in altre sottoreti. Da fuori (internet) vede tutto l'insieme di rete con indirizzo 128.208.0.0/16, ci sarà quindi un unica regola. Il router più interno avrà delle regole specifiche per ogni sottorete.*

*ESEMPIO:*
128.208.0.0/18		->		hmin 128.208.0.1		hmax 128.208.63.254
128.208.96.0/19    ->	   hmin 128.208.96.1  	 hmax 128.208.127.254
128.208.128.0/17   ->	   hmin 128.208.128.1 	 hmax 128.208.255.254

Con questo indirizzamento gli indirizzi liberi NON sono tutti alla fine, e ci sono dei *buchi* nel piano di indirizzamento.
Per questo quando bisogna allocare un gruppo di indirizzi, è consigliabile partire con definire il blocco più grande.

![[slide schema]]

Un router da newyork manda tutti gli indirizzi verso un router di londra, che a sua volta lo smista verso altre 3 direzioni. Nella tabella di routing di newyok si vede 192.24.0.0/19, quello di londra invece ha dei percorsi DIVISI, ci possono poi essere ulteriori **disagreggazioni (divisioni)** degli indirizzi già suddivisi.

Questo serve per avere delle tabelle di routing il meno complesse possibili.

## Longest matching prefix
Può succedere che in router ci siano più regole applicabili ad un pacchetto, in questo caso si sceglie la **regola con prefisso più lungo** poichè è la più specifica.

![[schema slide]]

*ESEMPIO:*
*Nel router di newyork si potrebbero applicare più regole (una che lo porta verso dx e una che lo porta verso sx). La regola che verrà applicata ad un indirizzo in arrivo al router di new york sarà quella di sx poichè più precisa.*

