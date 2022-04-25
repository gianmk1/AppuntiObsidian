 # Cisco Packer Tracer

[Calcolatrice IP](https://httplab.it/ipcalc.php)

È un simulatore di reti

NET ID: 192.168.0.0/24 => il /24 sta dicendo che i primi 24 bit della maschera sono fissi, i restanti 8 si

Con un /24 avrò a disosizione 2^8 = 256 indirizzi ip (da 0 a 255)
il primo è l'indirizzo di rete è 192.168.0.0
l'ultimo è l'indirizzo di broadcast è 192.168.0.255

Ho quindi a disposizione 256 - 2 indrizzi = 254 indirizzi ip (host)
Min è 192.168.0.1
Max è 192.168.0.254

Cavo CROSS per dispositivi dello stesso livello dello stack ISO/OSI
Cavo DRITTO per dispositivi di livelli diversi dello stack ISO/OSI

Router: livello 3
PC: livello 3
switch: livello 2
access point: livello 2
HUB: livello 1 (trasmette a tutti)

Per cambiare hardware del dispositivo prima bisogna spegnerlo

Porta:
- CFE: col cavo rj45
- FFE e FGE: col cavo in fibra (più veloci, F=FastEthernet G=GigaEthernet)  

I cavi rj45 hanno diverse categorie:
- Cat5
- Cat 5e
- Cat 6
- Cat 7
- Cat 7a
- Cat 8

Ogni categoria ha un'efficenza e una schermatura diversa e una limitazione sulla lunghezza del cavo. Più si sale di livello: più il cavo può essere lungo, più schermato e veloce

Nel Cat 8 la lunghezza massima del cavo è 150m, oltre il segnale può arrivare comunque ma sarà più lento e **alterato**

Ogni porta è una scheda di rete, un indirizzo e un MAC address

Router è quello che ci permette di comunicare in internet
*Es: router in classe ha:*
- router
- server dhcp
- switch
- access point

Cos'è un CLUSTER?

Usiamo questa come convenzione:
Gateway (router) è sempre l'ultima disponibile nei miei indrizzi

Server/ Servizi sempre nella penultima porta

Tutti i dispositivi hanno un servizio DNS che risolve l'indirizzo finale (localhost)

DHCP: Dynamic Host Configuration Protocol (per distribuire)

### --- 18/11

In un indirizzo IP ogni numero rappresenta un byte, per ogni numero decimale quindi il minimo è 0, il massimo è 255

es. il /24 indica i bit **riservati all'indirizzo di rete**

192.168.0.0/24 => 192.168.0.xxxxxxxx
I primi 3 decimali sono bloccati
192.168.0.00000000		- n0		MIN
192.168.0.00000001		 - n1
192.168.0.00000010		 -n2		
...
192.168.0.11111111			MAX (255)

Di questi 192.168.0.11111111 - 255 è il Broadcast
In un /24 quindi ho disponibili 254 indirizzi  [ (2^n) - 2  ]

Servono 2 operandi: l'indirizzo IP e la Subnet-mask, tra di loro c'è una operazione AND

### Tabelle di verità 

**AND**
0	0	=	FALSO
0	1	=	FALSO
1	0	=	FALSO
1	1	=	VERO


### Pacchetti su packet tracer
Il pacchetto ARP parte sempre per primo per abbinare gli indirizzi ip al mac address e alle porte corrispondenti

Pacchetto ARP come messaggio di broadcast

NB Prima che possa partire un pacchetto ICMP deve partire uno ARP, ricevute le informazioni nella tabella ARP possono partire i pacchetti ICMP


L'hub manda anche l iCMP coma pacchetto broadcast (a tutti), con lo SWITCH il pacchetto ICMP va diretto al destinatario

Per fare collegare 2 reti diverse ho sempre bisogno di un router, che fa da "corridoio" grazie alle tabelle di routing

Indirizzo ip dei gateway: l'ultimo possibile

nell es 2 reti: ho dato alle 2 porte connesse ai 2 switch l indirizzo di gateway (l ultimo disponibile per ciscuna rete)

Poi all interno dei laptop e dei pc abbiamo configurato i gateway



NB. Solitamente il primo pacchetto inviato su packet tracer dopo un cambio di configurazione va perso, le seconda volta torna tutto alla normalità

LA configurazione DHCP si fa all'interno del router:

Il cavo azzurro è quello per la CONSOLE, poi dal pc/laptop andiamo su terminal


Il router su packet tracer ha 3 livelli:
1. Per entrarci con comando ENABLE (entra in root)

? per il manuale

`show ip route`

`configure termianl` : entro nella parte di config

`ip dhcp pool nome_zona_dhcp` : abilitare dhcp

es. `network 192.168.1.0 255.255.255.0` : abilito dhcp alla rete 192.168.1.0 con subnet mask...

`dafault-router indirizzo_gateway` : 

NB. default router = gateway


## ES2XCASA:
1. Realizza una sala server con 2 server: 1 HTTP e 1 DNS, con indirizzamento statico NETID 192.168.3.0/24
2. Realizza una area clienti per solo dispositivi wifi, tipo smartphone o tablet (non altro).
	NETID 192.168.4.0/?? (deve essere servita per un max di 62 clienti), serviti da DHCP pool denominato "Clienti". 
	(Fare subnetting, non c'è bisogno di escludere)


Correzione es 2 per casa:
Dare un SSID agli access point per fare in modo che i device si colleghino alla rete wifi corretta

Attivo server DNS dando un nome al sito e l'indirizzo che corrisponde al serve http
Poi ai device diamo l'indirizzo di DNS
Ora possiamo conneterci al server http con url (senza ricorrere all'indirizzo IP)

Distribuiamo quanto visto sopra con il DHCP, ci sono 2 metodi:
1. Mettere un SERVER DHCP, che non ha bisogno di dns e defult gatewway in realtà, perchè interno a una sottorete. Sul servizio DHCP specifichiamo dns e default gateway

2. Oppure possiamo metterlo dentro il ROUTER, ecco i comandi da dare:
	`configure terminal`
	`ip dhcp pool nome_rete`
	`network indirizzo_di_rete mask`
	`default router indirizzo_gateway`
	
	Poi abilitiamo DNS server con:
	`dns-server nome_server_dns` (dentro dhcp-config)
	
	NB: 
		- `no network nome_rete` per eliminare rete
		- `do show ip dhcp pool` per vedere le reti dhcp

In entrambi i metodi ora abbiamo a  disposizione il server DNS e possiamo es. accedere al sito web tramie www.nome_sito.com


NB: 11000000.10101000.00000100.00 **000000** quelli evidenziati sono i bit liberi, se sono tutti uguali a 0 abbiamo un **indirizzo di rete**, se sono tutti uguali a 1 abbiamo un **indirizzo di broadcast**. Le restanti combinazioni rappresentano i possibili host

## Routing statico
Collegare più router assieme

Riferirsi ad esercizio routing.pkt

Cavo che collega direttamente router e pc è quello INCROCIATO.
Router e switch invece sono dello stesso livello dello stack ISO/OSI

Qui abbiamo 3 reti, la terza è quella tra i 2 router.

Dobbiamo specificare i percorsi. Nella tab routing del router diamo la network a cui deve connetersi, la mask e il "prossimo passo", cioè l indirizzo della porta del secondo router a cui si vuole collegare il primo

#### ES3XCASA:
Consiglio: all'inizio fare solo un solo collegamento per rete

Bisogna fare anche dei subnetting

# Routing dinamico
Alcuni protocolli che vedremo:

**RIP** = Routing Information Protocol
C'è anche RIP v2 per le subnet

**OSPF single area**
**OSPF multiple area**
(Open Short Path First)

**BGP** = border gateway protocol, usato per GRANDI SISTEMI
**AS** = sistema autonomo (vedi sotto)

**NB** anche redistribuzione

#### RIP
Lo useremo per una rete privata, sistemi piccoli (con comunque vari router)

#### OSPF
Rete media per piccola/media azienda, specialmente se quest'ultima è divisa in aree

#### AS
Un insieme di router che ha un unico protocollo di routing si chiama **sistema autonomo**, il protocollo usato è BGP.

***Un sistema autonomo è una rete di router che ha lo stesso protocollo di Routing***

Che può essere: 
**External**: (es. eBGP o iBGP) 
**Internal**:

Un protocollo può essere interno o esterno ad un sistema autonomo.
BGP è nato per gestire un sistema autonomo esternamente (soprattutto)

Più sistemi autonomi possiamo conneterli via BGP, l'interno del sistema può essere gestito con OSPF (anche diviso in più aree)

----

I protocolli non si parlano, per farli parlare devo usare la redistrubuzione delle rotte tra protocolli diversi

#### Es per casa
Su rete biblioteca togliere routing statico e mattere quello dinamico

## RIP
Devo dare nel router tutte le rotte adiacenti (quelle direttamente connesse), le vedo sulla routing table di cisco PT

Il RIP non vuole il CIDR, cioè la /

Da solo i router ricostruiranno con un algoritmo la rete


NB. utilizzare **tracert** per vedere dove passa un pacchetto

Quando ci sono tante subnetting dobbiamo dire al RIP di funzionare in versione 2, e **dobbiamo farlo dal terminale del router**

*Ecco la sequenza di comandi:*
- `enable`
	
	Qui dentro si usa soprattutto il comando **show**,
	i comandi che qui ci interessano sono **ping**, ssh, telnet, **configure** e traceroute
	
	es. `show ip route` visualizza la tabella di routing, la tabella di routing vista da terminale mostra più informazioni
	
- `configure terminal` o `conf t`
	
	Ora siamo nel livello di configurazione del terminale
	
- `router rip` : per configurare il rip devo fare:

- `version 2` : per abilitare la versione 2

- `network nome_rete` : per aggiungere una rete


NB. La metrica massima nel RIP è di 16 hop, quindi rotte con massimo 16 salti, dopo non vede più nulla


## OSPF
Su packet tracer si fa tutto da riga di comando

Possiamo avere più processi OSPF contemporaneamente in esecuzione, devo quindi dare un identificativo al processo

- `enable`
- `configure terminal`
- `router ospf num_processo`


	Alcuni comandi importanti:
	- routed-id, network, no, redistribuite, neighbor
	- **no**, per cancellare rotta sbagliata

L'ospf può essere utilizzato sia internamente che esternamente ad un sistema autonomo, serve quindi un numero_di_processo, magari è un router sia di confine che interno.

**NB**. L'OSPF ragiona per aree, la prima area che bisogna sempre definire è l'**area 0** o **backborne**. (ogni processo ha sempre l'area 0)
Quando dei router sono nel bordo vuol dire che sono *di confine*, **border router** e devono far comunicare 2 aree.

Scalabilità : l'ospf ragiona per **aree**
Si dice che 'osp è di tipo link-sta... : finchè non ha la conoscenza completa della rete, lui non si attiva. Manda dei pacchetti (LSA) per conoscenza della rete, deve conoscere **tutta la mappa** per funzionare.

L'intero sistema compreso di tutte le sue aree potrebbe essere un sistema autonomo.

Sigle per i router:
**R** : per router interno ad un area
**BR** : per un router di confine 
**ABR** : router di confine tra due aree
**ASBR** : per router di confine **tra sistemi autonomi**

- `router-id 0.0.0.1` : id definito dal progettista (sempre lo stesso per comunicare)
- `network RETE_ADIACENTE WILDE_MASK area NUMERO_AREA`

**NB** il router-id è un numero di 4 cifre decimali

**NB** l'ospf non vuole la maschera ma la **negazione della maschera**

**NB** deve arrivare un messaggio in cui il router ci dice che sta comunicando con l'altro router e le specifiche di questa comunicazione

Per vedere le tabelle di routing dalla CLI :
`show ip route` (nella parte generale)

Per vedere la configurazione dell'OSPF all'interno del router:
`show ip ospf`

#### Redistribuzione due reti, una RIP e una OSPF
*vedi PDF:*
[[sistemi-e-reti-3.1.1-RIP-OSPF-Redistribuzione.pdf]]

*vedi Esercizio:*
![[RedistribuzioneRotte_RIP-OSPF]]

I protocolli di routing NON si parlano bisogna utilizzare la tecnica di **redistribuzione**

`redistribute ?`

Per redistribuire RIP in OSPF:
`redistribute rip subnet`

La metrica per il RIP al massimo è 16, poi è infinito

#### Intefacce di loopback
Sono delle interfacce **virtuali**, metto in un router una interfaccia di loopback che mi **simula una rete**.

Servono a:
1. verificare il testing
2. verificare possibili errori della rete

Se interrogo la mia interfaccia virtuale sul router e mi risponde probabilmente c'è un problema col cavo

**NB** **no shutdown** per fare in modo che l'interfaccia non si spenga


Quando c'è, per esempio, 3.3.3.3/**32** la tabella di routing ci dice che quest'ultimo è un **unico indirizzo**, identificato come l'**indirizzo della macchina**.



**ROTTA DI DEFAULT**, NETWORK E MASCHERA A 0.0.0.0 e hop, redirige tutto il traffico in quella rotta

Sto dicendo che qualsiasi indirizzo ip arriva e fa richiesta per uscire lo puoi spedire


### BGP

`enable`
`configure terminal`
`router bgp numero_sistema_autonomo`
`neighbor hop_della_rete_vicina numero_sistema_autonomo_rete_adiacente`
`network rete_vicina maschera_della_rete`


**show ip bgp summary** : fa vedere il sommaio del bgp configurato in un router
**show ip bgp** : fa vedere tutte le possibili rotte per raggiungere i vicini, dove vediamo *> è il **percorso migliore**

**show ip protocols**


#### Redistributire BGP - OSPF

`enable`
`configure terminal`
`router ospf num_processo_ospf`
`redistribute bgp num_bgp_rete_corrente subnets`


#### Redistributire OSPF - BGP

`enable`
`configure terminal`
`router bgp num_bgp_rete_corrente`
`redistribute ospf num_processo_ospf`

### 13 gennaio 2022
*vedi cartella "EsercizioOSPF-BGP"*

*Chiedere di come è stata configurata*

**NB**. Posso vedere la routing table anche da CLI tramite comando **show ip route**

Per vedere come è configurato il BGP:
**show ip bgp**
*Il percorso indicato col **>** è quello consigliato e più veloce.*


Per vedere come è configurato l'OSPF:
**show ip ospf** : ci fa vedere tutti i protocollo ospf che abbiamo nel nostro router

Configurare bgp:
`router bgp 300`

`router-id x.x.x.x`
Indico i vicini (e la porta per cui si arriva):
`neighbor 4.0.0.1 remote-as 100`
Indico le reti adiacenti:
`network 4.0.0.0 mask 255.0.0.0`
`...`
NB. **Inserisco anche rete INTERNA**

<br>
<br>
<br>
<br>

# NAT 

**Posso rendere dei set di indirizzi privati in modo che escano con un solo indirizzo pubblico**

## NAT STATICO

*Vedi esercizio NAT_Statico*

Indirizzo es. 10.255.255.253 deve uscire, essere tradotto e uscire come indirizzo pubblico 

FASE 1: **MAPPATURA**
 
**ip nat inside source static 10.255.255.253 (server_rete_interna) 50.40.30.1 (indirizzo_col_quale_deve_uscire, cioè quello PUBBLICO)**

FASE 2: **ASSEGNAZIONE**
- definire la porta all'interno della rete privata (interface > **ip nat inside**)
- definire la porta esterna alla rete privata (interface > **ip nat outside**)

Il router si occupa della traduzione degli indirizzi e lo istrada poi correttamente

**NB**. Questa è una configurazione statica:
Devo **aggiungere la mappatura** anche per PC0 e Laptop
es.  ip nat inside source static 10.0.0.2 50.40.30.1 (per PC0)


INSIDE : rete privata
OUTSIDE : parte pubblica

**NB**. Per vedere le **traduzioni NAT** : **show ip nat translations**


## NAT DINAMICO (o overload)

*Vedi esercizio NAT-Dinamico.pkt*

1) **Definire un ACCESS LIST**
2) **Definire le porte esterne ed interne**
3) fare la **MAPPATURA**

**ACL**: regole di instradamento delle rotte di un router, dove posso permettere o negare l'utilizzo di una rotta.
Sono di 2 tipi:
- **Standard**, numero che va da 0 a 99
- **Estese**, numero che va da 100 a 199

Per il NAT dinamico overload utilizziamo quelle **standard** 

 **access-list 1 permit 10.0.0.0 0.255.255.255** --> Permetti alla rete 10.0.0.0 di attraversare "qualcosa"

NB. ACL come l'ospf vogliono le wilde-mask

*Come nel NAT statico, definisco le porte interne ed esterne*

##### Ora posso fare la MAPPATURA
Col comando:
**ip nat inside source list 10 interface FastEthernet4/0 overload**

<br>
<br>
<br>

## Port Forwarding

R2 : ip nat inside source static tcp 70.60.50.1 80 50.40.30.2 8888

Qui si parla di **destination NAT**

-> Tutto ciò che ricevi tramite richiesta TCP lo invii alla porta 80 del server web, quello che deve arrivare voglio che abbia richiesta specificata con porta 8888
(un ping non funziona quindi)

Il browser invece è una richiesta TCP

# 27 gennaio
## DMZ
È la parte di rete pubblica di una LAN. Il pubblico acceder alla DMZ, la parte privata può accedere alla DMZ ma dalla DMZ non si può accedere alla parte privata.

**FIREWALL**
Si possono classificare per flusso:
- ingress firewall : controllano il flusso esterno alla LAN
- egress firewall : controllano il flusso interno verso l'esterno

Per numero di host:
- personal firewall: se proteggono solo un dispositivo
- network firewall: se protegge una rete intera

## ACL
Abbiamo 2 tipi di acl, **standard**, per filtrare l'accesso controllando il traffico in entrata alla destinazione (bisogna pensare al router e all'interfaccia di questo dove verrà applicata la regola), **estese**, che servono a filtrare l'accesso controllando il traffico in uscita dal mittente

ACL va da 101 a 199 per le estese e da 1 a 99 per le standard

### ACL standard

per le standard il comando è:
`access-list access-list-number {permit/deny} source address [wildmask mask]`

per le ESTESE il comando è:
`access-list access-list-number {permit/deny} protocol source-wildecard [operator port] destination destination-wildcard [operatore port [estabilished] [log]`

`show access-lists` per vedere le regole definite


*vedi file ACL-1-standard-bloccoDiUnIP-*.pht

# 28 gennaio

## ACL estese
Di default hanno una politica di **negazione**.
  
Qui, possono mettere la regola il più vicino possibile alla rete/pc che voglio bloccare (a differenza delle ACL standard dove era il contrario)

```access-list 101-199 [permit/deny] [protocollo] [IP_origine] [wildcard_origine] [IP_destinazione] [wildcard_destinazione]```

*vedi comandi su file acl-estense.pkt*

# 01 febbraio

NB. Il port-forwarding è il NAT attraverso una porta

## IPV6
Se c'è **link local** è riferito ad una rete privata
In internet invece si parla di **global unicast**

L'indirizzo fisico e il link local hanno qualcosa in comune

## Link local
Possiamo comunicare con gateway, ma non tra le due reti

#### Costruire il link local
1. Recuperare l'indirizzo fisico della macchina
2. Il MAC address è diviso in 2 parti:
	- 24 bit per il numero del produttore
	- 24 bit per il numero della scheda
3. Bisogna passare alla **notazione estesa a 64 bit**, cioè **EUI-64**
	- primi 24 bit del mac +
	- 'FFFE' +
	- ultimi 24 bit
4. Aggiungo poi il prefisso FE80:: , :: indicano che lì ci sono tutti 0

NB. Bisogna invertire però il 7o bit

Esempio NON CORRETTO:

00E0.F95C.94CD

00E0F9 5C94CD

00E0F9 FFFE 5C94CD

00E0:F9FF:FE5C:94CD

00E0 => 0000 0000 11100 000

0000 0010 1110 0000 => 02E0

 02E0:F9FF:FE5C:94CD
 
 Finale: FE80::02E0:F9FF:FE5C:94CD

#### Configurare nel router il gateway:
R4(config)#ipv6 unicast-routing
R4r(config)#int gig0/0
R4(config-if)#ipv6 enable
R4(config-if)#ipv6 address fe80::1 link-local
R4(config-ip)#no shutdown

**NB. FE80::1 significa il primo indirizzo, cioè FE80::0000:0000:0000:0001**

NB1. **show ipv6 interface brief** per vedere la configurazione delle porte in ipv6

NB2. Possibile domanda d'esame è come configurare l'indirizzo IPv6

<br>
<br>

# Global unicast
Per far comunicare 2 reti devo avere indirizzi **link global unicast**, che sono a 128bit (64 di prefisso)

### Primi 64bit dell'indirizzo (definiti da ISP)
- **i primi 3 bit più a sinistra devono essere fissati come 001**
- i 45 bit rimanenti sono riservati per il prefisso di routing globale
- i 16 bit per il subnetting
- 64 bit per l'host

### Costruzione del prefisso
- scelgo l'anno corrente
- 0DB8 sono riferiti, di solito, a corsi di formazione
- ACAD riferito all'istruzione ITS
- B000 è riferito al numero di rete
- 0001 è riferito al numero di interfaccia

**NB.** I primi 3 bit sono 001, (2022 -> **001**0 0000 0010 0010)

Costituito l'intero prefisso, aggiungiamo l'indirizzo link local


#### Configurare IPV6 global unicast su router 	

...
...
...
...

<br>
<br>
<br>

# VPN

NB. Su packet tracer bisogna utilizzare router dalla serie 29xx in su.

All'interno del tunnel ci saranno i messaggi che devono viaggiare in sicurezza

1a fase: COSTRUZIONE DEL TUNNEL
2a fase: FAR VIAGGIARE IN SICUREZZA I PACCHETTI
3a fase: ASSOCIAZIONE DI UNA MAPPA ALLA PORTA


Esempio su *vpn-semplice.pkt:*

1. definisco la policy di sicurezza
2. dico con chi devo parlare
3. creo una access-list di tipo extended che mi permette la comunicazione tra le 2 reti
4. costruisco la mia mappa (devo unire tutte queste cose)
5. crypto map CMAP 10 ipsec-isakmp
6. Assegno la mapa all'interfaccia 

NB. Ho due password, una per il tunnel e una per i messaggi criptati all'interno del tunnel


#### Spiegazione VPN con NAT

VPN 12 sorpassa il NAT.

Poi uniamo il messaggio criptato dentro il tunnel (set transform-set ...)
Associamo la mappa all'interfaccia di uscita del ruoter

NAT-LAN è una lista estesa


## Il canale WIFI

I canali possono interferire tra di loro. 
Il segnale migliore si ha con i **canali 1 , 6 , 11**, a patto che NON TUTTI i router siano impostati su uno di questi canali.

Le modalità di trasmissione wireless sono:
- **WLAN** : livello **locale**
- **WPAN** : livello **domestico** (Personal)
- **WAN** : livello area

I protocolli:
- **802.11** 
- **bluetooth**

Protocollo di collisione della rete wifi?
**CSMA / CA** , Carrier Sense Multiple Access / Collisione Avoidance

<br>
<br>
<br>

# 24 marzo 2022

## Ripasso port forwarding
int fa0/0
ip nat inside
int fa4/0
ip nat outside
int fa5/0
ip nat outside
int se2/0
ip nat outside
ip nat inside source static tcp 50.25.0.10 80 12.12.0.18 80
ip nat inside source static tcp 50.25.0.10 80 12.12.0.22 80
ip nat inside source static tcp 50.25.0.10 80 12.12.0.14 80


##### guardare gli esericizi del 23 marzo + es-multidisciplinare





---

Materiale aggiuntivo:
- [Fondamentali informatica PoliMI](http://www.antlab.polimi.it/teaching-capone/lab-fond-di-internet-e-reti)


*Apri cartella:*
[Cartella esercizi Cisco PT](file:///C:/Users/Utente/Desktop/ITS-Synched/CiscoPTprojects)

https://luciano.defalcoalfano.it/nf-appunti/P2_03_dynamic_routing.html