# VPN , Virtual Private Network

Si intende una rete privata, che però e virtuale, poichè come collegamento si utilizza l'infrastruttura della rete internet.

NB. *Come si realizza una rete privata (non virtuale)?*
Una rete LAN solitamente è sempre una rete PRIVATA. Switch, cavi, AP, sono apparati della rete... 

NB. Ci potrebbe essere una rete privata che utilizza indirizzi pubblici

Qui però vogliamo una rete privata, però su SCALA MONDIALE.

*Esempio (rete privata FISICA). Sono una banca e voglio collegare le filiali alla sede centrale, usando una rete privata. Questa cosa si può fare, ovviamente non come si fa con le LAN poichè non possiamo tirare un cavo da 200km, devo comunque utilizzare l'infrastruttura internet ma lo faccio con una LINEA PRIVATA. A questo punto per accedere alla rete ci possono essere solo intrusioni di tipo fisico.Si paga la compania telefonica per avere una linea che collega le 2 sedi.*

Queste sedi potrebbero essere collegate anche via Internet senza VPN, ma a quel punto, chiunque può interporsi tra i 2 collegamenti.

Obiettivo VPN: utilizzare l'infrastruttura internet MA in un modo che emuli le infrastrutture private

La VPN può essere utilizzata anche per collegare tra loro sedi della stessa organizzazione, oppure poter collegare da remoto il singolo computer ad una sede centrale, oppure una situazione mista.

NB. Una VPN può avere più collegamenti.

La rete privata VIRTUALE vuole emulare la rete privata fisica.

### Come funziona una VPN?

![[inserisci schema blu]]

Si lavora con un **Tunnel IP sopra IP**(Ricorda un po' il tunneling ipv4).
Tutti i pacchetti che devono andare dalla rete A alla rete B, devono passare per questo tunnel. Il **tunnel end-point** incapsula tutti i pacchetti in uscita nei payload di pacchetti che hanno come destinazione l'altro end-point.

Nella rete A o B quindi possiamo avere un indirizzamento diverso.

Questo tunnel NON sta ancora garantendo sicurezza, non posso impedire a qualcuno di generare pacchetti e inviarmeli per questa strada, o di leggere il contenuto dei miei pacchetti. Ho solo costretto A a parlare solo con B e viceversa.

![[schema tunnel endpoint]]

![[schema esempio incapsulamento]]


## Protocollo IPSEC in modalità TUNNELING ????
IPsec si basa a **crittografia a chiave segreta**.  

![[esempio pacchetto con ipsec]]

*Encrypted è il pacchetto che deve andare da A a B, qui si ipotizza che il pacchetto contenga un payload e intestazione TCP*

- Questo pacchetto viene cifrato con crittografia con chiave segreta condivisa tra i 2 end-point.
- Viene inserita un ESP header
- Nuova intestazione IP, con indirizzo di destinazione l'altro end-point del tunnel (questa è in **chiaro**)
- Alla fine c'è una sezione **Authentication HMAC** (anche questa in chiaro): si applica una funzione hash alla parte da ... e poi si cifra con la chiave segreta condivisa

A questo punto il pacchetto originale è stato cifrato.

*Posso manometterlo / leggerlo / ... ?*
Un hacker può anche manometterlo, ma se fa ciò non tornerà il codice di autenticazione.

Quindi, usanto il tunnel, usando la cifratura e l'autenticazione (con la chiave condivisa tra i 2 end-point) 

