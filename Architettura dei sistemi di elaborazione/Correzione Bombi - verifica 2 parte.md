# Correzione verifica (2a parte)
<br>

##### Descrivi quale problema potrebbe verificarsi se ogni connessione TCP iniziasse a numerare i segmenti da 0
Si rischierebbe di confondere una richiesta di connessione ritardataria con una sua "reincarnazione duplicata".
<br>

##### Perchè motivo in genere quando si determina una chiave segreta di sessione si utilizzano 2 nonce?
Le 2 nonce vengono utilizzate per garantire la "freschezza" della chiave e per impedire un attacco di replica, poichè i messaggi scambiati tra le 2 parti sono inservibili allo scadere della chiave di sessione.
<br>

##### Descrivi il funzionmento di una VPN basata su IPSEC tunnel mode
Se stiamo costruendo una vpn basata sull'IPSEC tunnel mode:
Il tunnel è un ipv4 su ipv4, cioè il pacchetto ipv4 originario viene incapsulato in un pacchetto ipv4 e il pacchetto che deve essere effettivamente trasmesso è cifrato mentre la "parte ESP" è autenticat. *Si calcola un hash di ciò che deve essere autenticato e lo si cifra mediante una chiave segreta.*

Tutto il traffico in uscita/entrata passa attraverso un tunnel
<br>

##### Esericizio DNS
![[es-verifica.png]]
@ IN NS ns.abcd.it
ns IN A 100.100.1.1
www IN A 100.100.1.2
ftp IN A 100.100.1.3
private IN NS ns.private.abcd.it
ns private IN A 100.100.1.4
<br>

##### Esercizio Active Directory
![[es2-verifica.png]]
- 2 unità organizzative e all'interno di ognuna un gruppo, uno per tecnici e uno per progettazione.
- Permessi di share neutri: tutti possono fare tutto
- Permessi NTFS: lettura + scrittura per progettisti e sola lettura per tecnici
- GPO applicata all'UO tecnici per rimuovere il task-manager

