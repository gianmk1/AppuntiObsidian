# Ripasso per verifica
- *Studiare anche pacchetto IP nelle slide "Livello di Rete in Internet"*
- *Forse no "Introduzione alle reti"*
- *Esercizi su: backward learning, spanning tree, distance vector routing, alg. Dijkstra*
- *Internet protocol*

*Vedi appunti su foglio scritto*

---

## Sliding Windows
Il protocollo sliding non costringe il mittende ad aspettare la risposta per ogni frame trasmesso. 

I protocolli sliding windows vengono utilizzati con full- duplex : entrambe le parti contemporaneamente trasmettono dei frame dati, e ogni frame dati contiene delle informazioni di controllo che fanno capire all'altra entità che le informazioni sono stare ricevute correttamente.

Protocollo HDLC : orientato alla connessione e affidabile in cui le trame sono di vario tipo, quelle di informazioni hanno 2 numeri:
1. Uno di sequenza
2. Uno di ACK = numero di sequenza della propria trama che mi aspetto di ricevere

![[schema sul foglio]]

*Apertura connessione: con due **connection request**.*

Posso aver trasmesso alcune trame senza bisogno di conferma, ma NON si può andare avanti all'infinito, in qualsiasi momento infatti: potrebbe arrivare una **conferma negativa**.


La finestra di trasmissione è il numero di trame che possono essere spedite senza avere alcun tipo di riscontro, 

NB. In HLCD la finestra di trasmissione è 7 : posso ricevere 7 frame senza avere riscontro, devo però tenerle in memoria


Nel go-back-n non si accettano trame fuori sequenza, finestra di ricezione = a 1 (ricevo uno per volta)

Con rifiuto selettivo (o selective repeat) invece costringe ad avere la finestra di ricezione ampia quanto quella di trasmissione


Con Sliding Windows : l'idea è come se la finestra che scorre nel flusso di dati da trasmettere rappresenta una certa quantità di dati trasmetti ma non ancora con riscontro

---

## ESERCIZIO backward learning 

*vedi appunti*

---

## ESERCIZIO spanning tree

Usiamo lettere al posto degli indirizzi MAC

*vedi appunti*

---

## ESERCIZIO algoritmo dijkstra

*vedi appunti*

---

## ESERCIZIO distance vector routing

*vedi appunti*

---

## ESERCIZIO link state