# Realtà aumentata
REALTÀ VIRTUALE --> 100% realtà virtuale
REALTÀ AUMENTATA --> 30% di aggiunta + 70% realtà

I 3 livelli nella pratica:
1. Raccolta dati in campo
2. Edge Box che analizza i dati e li spedisce ad un server (della AR)
3. Tramite cellulare/tablet/... andiamo a collegarci al server

Ci sono 2 modi per andare a sfruttare la realtà aumentata:
1. Caricando lo scenario in sola **modalità locale**
2. Lo scenario viene caricato in un server e i device si collegano a quest'ultimo

<br>

Il riconoscimento dello scenario avviene tramite:
- **Riconoscimento d'immagine**, quando c'è un match tra la fotocamera e la foto caricata sul sever
- **Tramite dei TAG**, sono univoci e limitati, somigliano a dei QR code. Il riconoscimento avviene sul solo tag, non sull'immagine in cui è posto.

Quest'ultimo metodo aiuta anche nel caso ci siano più immagini salvate molto simili.

<br>

Per sfruttare questo servizio dobbiamo avere:
1. Applicazione smartphone
2. Software runtime che gira sul server
3. Builder, cioè il software dove andiamo a creare il progetto di realtà aumentata

<br>

## Builder
Abbiamo a disposizione:
- Variabili
- Punto di interesse
- Documento
- Immagini
- **Note**
- Sottoscene
- **Trigger**, per legare dei punti di interesse a delle varibili
- Link ad applicazioni esterne (ad esempio alla dashboard della macchina)

*Alcune considerazioni:*
- Spesso i documenti possono riportare il manuale dello specifico componente inquadrato
- Una **sottoscena** può mostrare, per esempio, l'interno di una cabina chiusa senza doverla aprire
- Un trigger permette, ad esempio, di far lampeggiare un punto dell'immagine basandoci sul valore di una variabile (es. sensore temperatura)
- Lasciare una **nota** nello scenario può servire in caso di un lavoro in sospeso sul macchinario

<br>

### Procedure
Lo scopo delle procedure è quello di **portare l'utilizzatore del macchinario alla risoluzione del problema**

È possibile accedere alle **procedure** tramite:
1. Riconoscimento dell'immagine (=**vicino alla macchina**)
2. Slegata dal resto

### Livelli di accesso
Questi servono per limitare le possibilità di accesso ai non addetti ai lavori o ai dipendenti non formati per un task.

La mia esperienza con la realtà aumentata sarà quindi limitata a solo ciò mi è concesso accedere/vedere/modificare/...

Con **security level = 0**, il valore è accessibile e leggibile da tutti.

**NB**. Spesso sommergere un operatore di dati poco influenti al suo scopo può provocare confusione, meglio quindi limitare l'esperienza dell'utente.

<br>

Il nome che daremo all'interno di una variabile qui dovrà essere poi lo stesso del nodo di Node Red

<br>

### Esercitazione Modbus
I nodi che hanno 2 uscite o più portano in output sempre lo stesso messaggio ma in formati differenti.