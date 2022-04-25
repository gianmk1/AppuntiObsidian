# Indirizzi IP (rivedere)
Sono 32 bit, l'**indirizzamento IP** è gerarchico, l'indirizzo è diviso in 2 campi: una porzione identifica in modo univoco la rete, e un'altra porzione identifica un nodo all'interno di quella rete.
Questa suddivisione è variabile.

**Metodo Classfull**
![[inserire schema pag2 pdf inirizzi IP]]

#### 3 classi: A, B, C

Esempio: 120.7.4.2
Rappresentazione decimale a punti, ognuno di questi numeri è un byte dell'indirizzo, è quindi una sequenza di 32bit (**0**111 1000 0000 0111 0000 0100 0000 0010).
- Il bit più significativo (il primo) è 0, identifica una rete di classe A sono solo 126, ciascuna di essa può ospitare più di 16milioni di nodi (vedi sotto)
- I primi 8 bit 
- I seguenti 24 bit quindi permettono 2^24 combinazioni


120.0.0.0 => rappresenta la rete


**NB**. Tutto ciò che comincia con 127 è riservato per la *localhost*

Quando si fa la configurazione manuale di un nodo bisogna specificare:
- indirizzo ip 

##### Cos'è una maschera di sottorete?
Ha degli 1 nella parte di indizzo che determina il numero di rete e ha degli 0 nella parte dell'indizzo che determina l'host all'interno della rete

ES. maschera di sottorete della classe B è 255.255.0.0

<br>

(riferito a schema slide 3 del pdf)

In internet tutti i nodi che appartengono ad una stessa rete fisica devono appartenere tutti alla stessa rete IP
Corrispondenza rete fisica - rete ip: 

vengono quindi sprecati degli indirizzi ip (es. multicast)
Questo ha portato nel tempo ad un altro modo di indirizzare che si chiama **classless**

NB. nel router ogni interfaccia di rete deve avere il suo indirizzo ip

### Notazione Classless
![[schema slide 4 del pdf]]

![[vedi slide 5 del pdf]]

Un prefisso lungo L: i primi L bit dell indirizzo rappresentano la rete, i rimanenti bit 

Prefisso predefinito per classe A:
Prefisso predefinito per classe B:
Prefisso predefinito per classe C: /24

Esempio CIDR (Classless Inter Domain Router), rete 184.13.12.0/22

Quali sono gli indirizzi che posso effettivamente usare in questo range?
![[vedi slide pag 6]]

*Svolgimento:*
Passo in binario, converto 152 in binario => 1001 1000

184 13 1001 10|**00 0000 0000**			-> questa è la parte variabile

Quando ho tutti 0 è l'indirizzo di rete, quando ho tutti 1 è l'indirizzo di broadcast

### Indirizzi IP speciali

