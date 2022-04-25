# Cisco Packe Tracer
### Esempio di subnetting
*Prendiamo come esempio la rete **192.168.0.0 / 24**:*

- Il **/24** sta dicendo che i primi 24 bit della maschera sono **fissi**, si possono utilizzare solo i restanti 8bit per gli indirizzi
- Con /24 avrò a disposizione **2^8 = 256 indirizzi**, di questi:
	- Il primo, 192.168.0.0 è l'**indirizzo di rete**
	- L'ultimo, 192.168.0.255 è l'**indirizzo di broadcast**
	- I restanti indirizzi saranno gli **host** a disposizione, cioè **256 - 2 = 254 host**.
	Il primo host disponibile è 192.168.0.1
	L'ultimo host disponibile è 192.168.0.255
	
### I cavi e porte
- Il cavo **CROSS** si utilizza per dispositivi dello **stesso livello** ISO/OSI
- Il cavo **DIRITTO** si utilizza per dispositivi di **livelli diversi** ISO/OSI

##### Cavi ethernet
- Cat5
- Cat 5e
- Cat 6
- Cat 7
- Cat 7a
- Cat 8 (Lunghezza-Max di 150m)

Ogni categoria ha un'efficienza, una schermatura e una limitazione sulla lunghezza del cavo diversa. Più si sale di livello: più il cavo può essere lungo, più veloce e meglio schermato.

*Ogni porta è una scheda di rete, avrà quindi un indirizzo e un MAC address.*

##### Porte
- **CFE** , col cavo RJ-45
- **FFE e FGE** , col cavo in **fibra** (F=FastEthernet , G=GigaEthernet)

### I dispositivi 
*Dispositivi e il loro corrispettivo livello ISO/OSI:*

- **Router**: livello 3
- **PC**: livello 3
- **Switch**: livello 2
- **Access-Point**: livello 2
- **HUB**: livello 1

### Identificare i router
All'interno di una rete dobbiamo identificare correttamente i router in quanto possono risiedere in un particolare punto della rete.

- **R** : per router **interno** ad un'area
- **BR** : per un router di confine
- **ABR** : per router di **confine tra due aree**
- **ASBR** : per router di **confine tra sistemi autonomi**

**Cos'è un Sistema Autonomo?**
Un Sistema Autonomo (o **AS**) è un **insieme di router** che hanno lo **stesso protocollo di routing**.

### Pacchetti





<br>
<br>

---
## Distribuire il DHCP
**DHCP**, Dynamic Host Configuration Protocol

Per distribuire il DHCP in una rete possiamo utilizzare 2 metodi:
1. Impostare un **server DHCP** esterno
2. Configurare un **DHCP pool** all'interno del **router**

#### Nel Server
Dopo aver configurato il server, questo avrà bisogno anche di:
- un **indirizzo dns** 
- un **default gateway**.

#### Nel router
*Ecco i comandi da utilizzare nella CLI:*
1. `enable`
2.  `conf t`
3. `ip dhcp pool [NOME_POOL]` (es. Area Clienti)
4. `network [INDIRIZZO_RETE] [SUBNET_MASK]`
5. `default router [INDIRIZZO_GATEWAY_RETE]`

All'interno del pool dhcp possiamo **configurare il DNS**:
`router(dhcp-config)# dns-server [INDIRIZZO_SERVER_DNS]`

Per **escludere un intervallo di indirizzi** dal DHCP:
`router(config)# ip dhcp excluded-address [PRIMO_HOST] [ULT_HOST]`

**NB**. Altri comandi utili:
- `no network [NOME_RETE]` , per eliminare la rete dalla configurazione
- `do show ip dhcp pool` , per visualizzare i pool DHCP
- `no ip dhcp pool [NOME POOL]` , per eliminare un pool

<br>
<br>

---
## Routing statico
INTERNETWORKING: per collegare più reti assieme staticamente configurando manualmente ciscun router.

Per funzionare correttamente bisogna configurare le rotte **di andata** ma anche quelle per il **ritorno**.

Possiamo configurare i **percorsi statici** con 2 metodi:
1. Da interfaccia grafica
2. Da terminale

**NB.** Per vedere le tabelle di routing da terminale: `show ip route`

#### Da terminale
*Il comando per inserire per inserire una rotta è il seguente:*

`ip route [RETE_DA_RAGGIUNGERE] [SUBNETMASK_RETE] [INDIRIZZO_NEXT_HOP]`

L'**indirizzo del next hop** corrisponde all'indirizzo della porta da cui possiamo raggiungere il router cui collegata la rete che vogliamo rendere disponibile.

![[routing-statico-CiscoPT]]

**NB**. Dando la sequente rotta, `ip route 0.0.0.0 0.0.0.0 [NEXT_HOP]`, **tutto il traffico** sarà rediretto in quella rotta.

<br>
<br>

---
### Routing dinamico (in generale)
Alcuni protocolli di routing dinamici:
- **RIP**, *Routing Information Protocol*	
- **OSPF**, *Open Short Path First*
- **BGP**, *Border Gateway Protocol*

##### RIP (Routing Information Protocol)
Utilizzato per reti di **piccole dimensioni**.

##### OSPF (Open Short Path First)
Utilizzato per reti di **medie dimensioni** come una piccola / media azienda, specialmente se quest'ultima è divisa in aree. Può essere diviso in:
- **SingleArea**
- **MultiArea**

L'**OSPF ragiona per aree**, è di tipo **link-state-routing**, finchè non ha l'intera conoscenza della rete non si attiva. Per fare ciò manda dei **pacchetti LSA** per conoscere la rete, così da ricostruire l'**intera topologia**.

*L'intero sistema compreso di tutte le sue aree potrebbe essere un Sistema Autonomo.*

##### BGP (Border Gateway Protocol)
Viene utilizzato per sistemi di **grandi dimensioni**. Questo protocollo viene utilizzato **soprattutto per gestire un Sistema Autonomo esternamente** (eBGP). Il protocollo BGP è di 2 tipi:
- **eBGP** (**external**): eseguito su 2 o più router di **diverso Sistema Autonomo**
- **iBGP** (**internal**): eseguito su router dello **stesso Sistema Autonomo**

*Più Sistemi Autonomi possiamo conneterli via BGP, mentre l'interno del sistema possiamo gestirlo con l'OSPF.*

#### REDISTRIBUZIONE
I protocolli di routing non si parlano tra di loro, di conseguenza per farli comunicare bisogna utilizzare la tecnica della **reditribuzione delle rotte** tra protocolli diversi. 

<br>
<br>

---
## Interfaccia di loopback
Sono delle **interfacce virtuali**, configurate in un router, che permettono di **simulare una rete**.

Possono servire per:
- Verificare il **testing**
- **Verificare possibili errori** della rete

**NB.** Se, interrogando l'interfaccia, questa mi risponde, probabilmente c'è un problema col cavo.
**NB2.** Quando nella tabella di routing c'è una voce come **8.8.8.8 / 32**, identifica un **unico indirizzo**, cioè l'indirizzo della macchina.

##### Configurazione
1. `enable`
2. `conf t`
3. `int loopback [NUM_INTERF_LOOPBACK]` , può essere 0,1,...
4. `ip add [INDIRIZZO_LOOPBACK] [MASK_LOOPBACK]` , *es. ip add 3.3.3.3 255.0.0.0*
5. `no shutdown` , per attivare la porta

<br>
<br>

---
## RIP
Devo dare al router **tutte le rotte adiacenti** (cioè quelle **direttamente connesse**), da soli i router ricostruiranno, con un algoritmo, la topologia della rete.

*Ecco la sequenza dei comandi:*
1. `enable`
2. `conf t`
3. `router rip` , per entrare nella configurazione del routing RIP
4. `version 2` , per abilitare la versione 2
5. `network [INDIRIZZO_RETE_ADIACENTE]`

**NB**. La metrice massima nel RIP è di **16 hop**, quindi le rotte possono avere massimo 16 salti, dopo non si vedrà più nulla.
**NB1**. Utilizziamo il comando `show ip route` per vedere la configurazione del RIP nel router

![[esempio file rip]]

<br>
<br>

---
## OSPF
Per configurare l'OSPF ho bisogno di:
- un **numero di processo**,
Posso avere **più processi OSPF contemporaneamente attivi**, devo quindi dare un identificativo al processo. *Es. L'OSPF può essere utilizzato sia internamente che esternamente ad un Sistema Autonomo, e avere quindi più processi attivi.*
- un **numero di area**,
L'OSPF ragiona per aree, **per prima** bisogna sempre definire l'**area 0** (o **backbone**), ogni processo ha sempre l'area 0.
- un **router-id**
È un numero di quattro cifre decimali che serve per identificare univocamente un router

*Ecco la sequenza di comandi:*
1. `enable`
2. `conf t`
3. `router ospf [NUMERO_PROCESSO]`
4. `route-id [x.x.x.x]` , *es. 1.1.1.1*
5. `network [RETE_ADIACENTE] [WILDE_MASK_RETE_ADI] area [NUMERO_AREA]`

**NB**. Col comando network dobbiamo mettere la **wilde-mask** (cioè la **negazione**), non la maschera normale.
**NB1**. Alcuni ulteriori comandi:
- `show ip ospf` , per vedere la configurazione generale dell'OSPF
- `show ip ospf neighbor` , per vedere i vicini

#### Propagazione della default-static-route in OSPF
Per propagare una default route, il **router di confine** deve essere configurato con:
- Una default **static route** con: `ip route 0.0.0.0 0.0.0.0 [NEXT_HOP]`
- Il comando `default-information originate` nella modalità di configurazione OSPF del router. 
Ciò indica al router di confine di essere: la **fonte delle informazioni** sulla default-route e di **diffondere la default-route** negli updates OSPF (cioè **a tutti gli altri router**).

![[esempio ospf]]

<br>
<br>

---
# BGP
Dobbiamo dare al router **tutte le rotte adiacenti** e i **vicini immediati** con il corrispettivo numero di Sistema Autonomo.

*Ecco la sequenza di comandi:*
1. `enable`
2. `conf t`
3. `router bgp [NUM_SISTEMA_AUTONOMO]`
4. `neighbor [PORTA_VICINO_IMM] remote-as [NUM_AS_VICINO_IMM]` , 
5. `network [INDIRIZZO_RETE_ADIACENTE] mask [MASHERA_RETE_ADICENTE]`

*Ecco un esempio:*
neighbor 9.1.1.2 remote-as 200
network 9.1.1.0 mask 255.255.255.252

**NB**. Alcuni ulteriori comandi:
- `show ip bgp` , per vedere tutte le possibili rotte per raggiungere un vicino qualsiasi. I percorsi con `*>` sono i **migliori** e quindi quelli che verranno utilizzati.
- `show ip bgp summary` , per vedere il sommario del bgp nel router

![[esempio bgp]]

<br>
<br>

---
# Redistribuzione tra RIP e OSPF
#### OSPF -> RIP
Per ridistribuire i percorsi RIP in OSPF, nel router di confine:
1. `enable`
2. `conf t`
3. `router ospf [NUM_PROCESSO]`
4. `redistribute rip subnets`

#### RIP -> OSPF
Per ridistribuire i percorsi OSPF in RIP, nel router di confine:
1. `enable`
2. `conf t`
3. `router rip`
4. `redistribute ospf [NUM_PROCESSO_OSPF_DA_RIDISTR] metric [CONTEGGIO_HOP]`

**NB**. Quando ridistribuiamo qualsiasi rotta esterna instradata conTIP, dobbiamo specificare il **conteggio degli hop** per raggiungere quella rete esterna: il conteggio degli hop non deve corrispondere esattamente alle condizioni reali, possiamo eccedere nell'allocazione.

![[esempio]]

<br>
<br>

---
# Redistribuzione tra OSPF e BGP
#### BGP -> OSPF
Per ridistribuire i percorsi BGP in OSPF, nel router di confine:
1. `enable`
2. `conf t`
3. `router ospf [NUM_PROCESSO]`
4. `redistribute bgp [NUM_SIS_AUTONOMO_DA_RIDISTR] subnets`

#### OSPF -> BGP
Per ridistribuire i percorsi OSPF in BGP, nel router di confine:
1. `enable`
2. `conf t`
3. `router bgp [NUM_SISTEMA_AUTONOMO]`
4. `redistribute ospf [NUM_PROCESSO_OSPF_DA_RIDISTR]`

![[esempio]]

<br>
<br>

---