# Cavi

Il cavo UTP sono 4 coppie di cavi, per trasmettere in realtà basta una coppia, in cui il segnale viaggia come differenza di potenziale tra uno e l'altro

Per ottenere velocità elevate però si usano 2 coppie che trasmettono in una direzione e 2 che trasmettono nell'altra

Mettendo delle coppie di cavi vicine, si creerebbe interferenza elettromagnetica, per ovviare a ciò i cavi sono attorcigliati NON SCHERMATI


Cavo FTP: i 4 doppini sono raccolti in una schermatura metallica

Cavo STP: le singole 4 coppie sono schermate

Le schermature servono a proteggere il cavo dal rumore elettromagnetico.

l'immunità al rumore è maggiore maggiore è l'attorcigliamento dei cavetti interni al cavo

Un cavo può essere **DIRETTO** o **CROSS**


I **BRIDGE** sono di 2 tipi:
1. Per inteconnettere reti di tipo diverso
2. Per inteconnettere reti dello stesso tipo per:
	- Aumentare il diametro massimo della rete
	- ...

L'**ACCESS POINT** è un caso particolare di bridge e viene usato per collegare reti di tipo diverso (802.3 - 802.11).
Se riceve un frame 802.11 indirizzato ad una stazione della rete 802.3 deve:
- cambiare il formato del frame
- trasmettere nella rete 802.3 applicando il protocollo e le regole di questa rete 

Con un frame indirizzato a rete 802.11 viceversa

## vedi appunti Sottolivello MAC