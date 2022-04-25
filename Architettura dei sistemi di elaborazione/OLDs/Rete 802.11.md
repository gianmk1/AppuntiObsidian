# 802.11, la rete wi-fi

Gestire il protocollo MAC nella rete wifi è molto più complicato che nella rete cablata, anche trasurando il fatto che le reti wifi sono utilizzate da dispositivi mobili che tandono a cambiare spesso nel tempo: 

1. Le stazioni possono avere diverse aree di copertura in relazione alla loro posizione
2. Non è possibile rilevare collisione mentre si sta trasmettendo.
	NB. Ascoltando il canale mentre trasmette, la stazione, sentirebbe solo la sua trasmissione.

#### Stazione nascosta
![[schema sulle slide (l'hub rappresentato è in realtà un access-point)]]

La portata di una antenna è una sfera. I cerchi in figura rappresentano le varie portate delle stazioni. 
A può sentire quello che l'hub trasmette e vicecersa
B può sentire quello che l'hub trasmette e viceversa
A però non raggiunge B e viceversa

B anche ascoltando il canale potrebbe sentirlo libero non sentendo la comunicazione che avviene tra A e l'access-point/hub. E si verifica quindi la collisione nell'area che interseca A e B

B è quindi **nascosto** rispetto ad A

#### Stazione esposta
![[inserisci schema sulla slide]]

*Spiegazione:*
Se S1 sta trasmettendo qualcosa verso R1 e S2 si mette in ascolto lo sente occupato. Ma se S2 iniziasse a trasmettere verso R2 non impedirebbe a R1 di ricevere correttamente il segnale.

S2 (nella portata di S1 ...) è la stazione **esposta**

<br>

## 802.11, Livello Fisico
Si utilizzano bande di frequenza diverse e si usano anche delle tecniche di modulazione per variare l'ampiezza

## 802.11
- Il protocollo utilizzato è CSMA/CA, cercando quindi di evitare le collisioni
- La trasmissione è **affidabile** (cioè con un acknowledge di risposta) con **ARQ** per evitare la perdita di frame. 

NB. Perchè nell'802.3 non è previsto il riscontro e invece qui si? Nell'802.3 si "intercetta" la collisione e le stazioni sanno che c'è stata. Con l'802.11 quando si trasmette un frame non c'è modo di sapere se c'è o meno stata la collisione. Serve quindi un acknowledge

- I frame hanno 3 indirizzi: sorgente, destinazione, access-point
- I frame indicano la propria durata con cui occuperanno il canale, anche per ricevere l'acknowledge
- altro, es. crittografia (WPA / WPA-2)

#### 802.11 : CSMA/CD
![[inserire schema]]

Prima di trasmettere si ascolta il canale e se è libero.
Quando il canale è libero non si comincia subito a trasmettere ma ogni stazione sceglie un intervallo di tempo (**backoff**) per cui ogni stazione deve attendere prima di cominciare a trasmettere.

Questo serve per cercare di evitare le collisioni intervallando il tempo in cui le stazioni possono trasmettere appena il canale è libero.
*vedi spiegazione sulla slide*

Oltre all'ascolto del canale fisico esiste anceh un ascolto virtuale per cui ogni stazione mantiene una struttura della **NAV** per 
