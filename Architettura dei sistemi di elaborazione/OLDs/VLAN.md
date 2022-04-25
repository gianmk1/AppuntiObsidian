# Virtual LAN (VLAN)
Il protocollo VLAN consente di separere la topologia fisica della rete dalla sua topologia logica.

Questo rende possibile realizzare due o più reti virtuali separate, sulla stessa infrastruttura fisica, senza necessità di duplicazione degli apparati.

**NB**. Dividere le reti a renderle disponibili ad una specifica utenza limita il rischio di attacchi/fughe di dati/... . 
**NB2** In un'azienda posso avere 2/3 reparti con dispositivi e server diversi, non è detto che io possa sempre fare tanti rete separati (anche per evitare la continua duplicazione degli apparecchi).

La LAN virtuale permette di separare la rete fisica in due o più reti virtuali in modo che le stazioni collegate ad una rete virtuali non possano interagire con quelle dell'altra rete virtuale.

![[inserire schema di esempio nella slide (CISCO)]]

### VLAN funzionamento
È richiesta una configurazione a livello sistemistico per cui nello switch si deve dire a ogni porta a quale VLAN appartiene. Le porte che sono utilizzate per connettere due switch in cui passa il traffico sia della vlan-1 che della vlan-2, devono avere una *doppia mappatura*.

**VLAN-tagging**: quando un frame va inoltrato verso una porta con doppia mappatura al frame viene aggiunto un tag in cui si specifica la vlan di appartenenza. Ora il frame diventa 802.1/Q

![[inserisci schema 802.1/Q]]