# Correzione prova Bombi multidisciplinare

##### 1. Differenza tra routing statico e routing adattivo?
Con il routing statico...
...
Con il routing dinamico i router si scambiano informazioni e sulla base di queste si determinano le tabelle di routing.

##### 2. Distance Vector Routing? Come funziona rispetto al Link State Routing?
Il DVR si basa sui vettori di distanza e cerca il percorso con il cammino minimo. (**come però anche il Link State Routing**). Con il DVR il router riceve dai vicini immediati i vettori distanza, basandosi su questa informazione e sulle distanze misurate, si determina qual è il vicino migliore per una direzione e il relativo costo.
Il vantaggio del DVR è molto più semplice rispetto al Link State Routing perchè non richiede la conoscenza totale della rete; ha però il problema del **conteggio all'infinito**.

##### 3. Applicando l'algoritmo di Dijkstra, determina il sink tree e la tabella di routing
*vedi esercizio sul blocco*

##### 4. Esercizio tabella di routing
*vedi esercizio sul blocco + foto cell*

##### 5. Esercizio piano indirizzamento + Katharà
NB. è **ifconfig...** NON ipconfig

##### 6. Spiega il significato dei campi: sequence number, ack number e window size dell'intestazione TCP
- Sequence number rappresenta il numero del primo byte contenuto nel segmento.
- ACK number è il numero del primo byte del prossimo segmento che mi aspetto di ricevere.
- Window size rappresenta il numero massimo di byte che l'entità TCp è disposta a ricevere al momento.

##### 7. Considera la figura che rappresenta lo scambio di segmenti tra 2 entità TCP
*vedi esercizio sul blocco + foto cell*

##### 8. Descrivi il controllo della congestione in TCP Tahoe
Congestion Window rappresenta il numero massimo byte che possono essere inviati senza dover ricevere un riscontro (cioè quanti byte non confermati sono ancora in giro per la rete).

La Congestion Window parte dalla dimensione di un segmento e viene raddoppiata ad ogni ACK ricevuto fino a raggiungere un valore di soglia, una volta raggiunto ciò incrementa di 1.
Se c'è il timeout su l'ACK di un segmento allora la congestion window parte dal valore iniziale e la soglia viene impostata a metà del valore del congestion window di quando si è verificato il timeout.

##### 9. Descrivi lo scopo del protocollo TLS e spiega (con uno schema) come viene determinata la chiave di sessione
Con il TLS riusciamo ad avere la certezza di star parlando proprio con quel server (tramite una serie di certificati). In più siamo sicuri che il traffico è cifrato.

Il client manda una nonce al server, il server risponde inviando la propria nonce e una catena di certificati, la catena di certificati consente al browser di accettare l'identità del server.

Il client invia al server una premaster-key cifrata usando la chiave pubblica del server.

Entrambe le parti hanno le componenti per conoscere la master-key e si calcolano una **chiave segreta di sessione** che sarà utilizzata per cifrare il traffico futuro.
