# IPv6
## Link local
Un indirizzo link local è l'**indirizzo di una interfaccia all'interno di una rete broadcast** (in pratica una **rete lan**), non è quindi "routato" dai router IPv6

**NB1**. Gli indirizzi IPv6 sono di lunghezza di **128bit**
**NB2**.  Gli indirizzi **IPv6 identificano sempre una interfaccia** e NON i nodi (router/host)

Per calcolarlo c'è bisogno di del **MAC address** che è diviso in:
1. **24 bit** per il numero del **produttore**
2. **24 bit** per il numero della **scheda**

*Esempio:*
MAC: 000C.CF69.EAD7 (48bit)

1. Costruisco **estensione indirizzo MAC a 64bit**:
	a. **Primi** 24bit MAC + **FFFE** + **Ultimi** 24bit MAC
	--> 000C.CF + FFFE + 69.EAD7
	--> 000C:CFFF:FE69:EAD7
	
	b. **Negazione del SETTIMO bit**  
	--> **000C** = 0000 0000 0000 1010
	--> 0000 00**1**0 0000 1010 = **020C**
	
	Il risultato finale è: 020C:CFFF:FE69:EAD7
	
2. **Aggiunta del prefisso FE80**, per raggiungere indirizzo a **128bit**
--> **FE80** + 020C:CFFF:FE69:EAD7
--> FE80::020C:CFFF:FE69:EAD7 o **FE80::20C:CFFF:FE69:EAD7**

<br>
<br>

## Global Unicast
Sono gli indirizzi univoci al mondo instradabili a livello globale, equivalgono agli **indirizzi IPv4 pubblici**.

Il link global unicast è un indirizzo a **128bit** con **64bit di prefisso** e i restanti 64bit costituiti da gli **ultimi 64bit dell'indirizzo link local**, ovvero l'**Interface ID**.

Lo **standard che sancisce la struttura** degli indirizzi IPv6 è lo **RFC 3587**.

Struttura:
**001** + prefisso **routing globale** (45bit) + **subnetting** (16bit) + **host** (64bit)

a. Costruzione del **prefisso**:
1. **Anno corrente** -> 2022
2. Riferimento alla **formazione** -> 0DB8
3. Riferimento alla **istituzione** -> ACAD
4. Riferimento al **numero di rete** -> 000B
5. Riferimento alla **inferfaccia** --> 0001 o **Interface ID**

	Prefisso finale: 2022:DB8:ACAD:B::1

**NB1**. I primi 3 bit del prefisso devono sempre essere **001**
**NB2**. Gli **"0" iniziali** in ogni campo possono essere **omessi**
**NB3**. La notazione **::** è permessa **una sola volta** all'interno di un indirizzo

b. Aggiungendo ora l'Interface ID abbiamo un **indirizzo IPv6**:

--> 2022:DB8:ACAD:B + CFFF:FE69:EAD7
--> Indirizzo IPv6: 2022:DB8:ACAD:B:CFFF:FE69:EAD7

**NB**. È stato tolto il riferimento all'interfaccia precedente.

<br>

## VPN
Fasi per la definizione di una VPN:
1. **Costruzione del tunnel**, con la definizione di una **mappa**
2. Definisco **criptazione dei dati**
3. **Associazione mappa-porta**

<br>
<br>

## ACL
Le ACL sono delle **regole per filtrare il traffico** in entrata e uscita da/a un host/rete.

Esistono **2 tipi di Access List Control**:
1. **ACL standard**: servono per filtrare l'accesso controllando il **traffico in ENTRATA** alla destinazione
2. **ACL estese**: servono per filtrare l'accesso controllando il **traffico in USCITA** dalla sorgente (mittente)

#### ACL Standard
- Le ACL standard hanno un **numero identificativo** compreso tra **1 e 99**.
- La regola deve essere applicata sull'**interfaccia più vicina alla destinazione del traffico** per filtrarne il traffico in entrata (= rete cui non si potrà accedere)

#### ACL Estese
- Le ACL estese hanno un **numero identificativo** compreso tra **100-199**.
- La regole deve essere applicata sull'**interfaccia più vicina alla sorgente del traffico** per filtrare il traffico in uscita (= rete con traffico in uscita limitato)

#### Configurazione ACL:
1. **Definire la regola**
2. Mi sposto sull'interfaccia corretta
3. Associare la regola all'**interfaccia**

**NB**. L'ordine con le quali sono definite le regole all'interno di una ACL è **importante** poichè altrimenti alcune regole potrebbero essere ignorate.

<br>
<br>

## NAT
#### NAT Statico
1. **Definizione "regola"**
2. **Mappatura** delle varie porte
	1. **ip nat inside** --> porta all'interno della rete **privata**
	2. **ip nat outside** --> porta all'esterno della rete, quella **pubblica**

*Esempio:*
ip nat inside source static 10.255.255.253 (server_rete_interna) 50.40.30.1 (indirizzo_col_quale_deve_uscire, cioè quello PUBBLICO)

#### NAT Dinamico (o Overload)
1. Definire una **access list** (utilizziamo **ACL standard**)
2. Definire le **porte interne ed esterne**
3. Fare la **mappatura**

*Esempio*:
- access-list 1 permit 10.0.0.0 0.0.255.255
- ip nat inside source list 1 interface fa1/0 overload

**NB1**. La regola **si applica sulla porta ESTERNA**
**NB2**. È possibile anche definire un **POOL di indirizzi** con i quali il traffico uscirà dalla rete NAT

#### Port Forwarding
Le fasi sono simili a quanto visto per il NAT Statico. Per ogni porta bisogna definire il **numero** e se la connessione è di tipo **TCP o UDP**

*Esempio*:
- ip nat inside source static udp 50.25.0.10 53 12.12.0.9 53

*Tutto il traffico in arrivo all'indirizzo 12.12.0.9 alla porta 53 viene inoltrato all'indirizzo 50.25.0.10 alla porta 53*

<br>

## Altro:
#### Alcune PORTE:
- HTTP --> **80**
- HTTPS --> **443**
- DNS --> **53**, UDP
- FTP --> **21**,  TCP
- SMTP --> **25**, è il protocollo utilizzato per l'**invio** delle mail
- POP --> **110**, è il protocollo utilizzato per la **ricezione** delle mail
- IMAP --> **143**, è il protocollo utilizzato per la **ricezione** delle mail


---
- [Fonte 1 - IPv6](https://www.windowserver.it/2015/02/ipv6-overview-generale/)