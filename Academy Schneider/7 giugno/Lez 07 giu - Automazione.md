# Automazione
AUTOMAZIONE è una parola che nasce in grecia, indica qualcosa che si muove/fa qualcosa senza il supporto dell'uomo. (**agisce secondo la propria volontà**)

*Es. Mulino da Seta Bolognese*, circa 1700, fu un segreto industriale di grande valore.

### Automazione Industriale
Per automazione industriale si intende *la tecnologia attraverso la quale un processo o una procedura può essere realizzata senza l'intervento umano.*

In una fabbrica del 1932 c'erano molte persone che giravano nell'impianto, la sicurezza era praticamente a 0, sostenibilità bassissima,...
In più non c'erano connessioni tra una macchina e l'altra.

**Il controllo di qualità era molto SOGGETTIVO**, poichè eseguito da una persona e non da un macchina.

### Produzione DISCRETA vs CONTINUA
Quella degli smartphone, automobili, monitor è una produzione **discreta**, dove il prodotto finale **può ritornare al suo stato iniziale (= prima della fase di produzione)**.

La salsa di pomodoro è invece una produzione **CONTINUA** poichè non può ritornare al suo stato originario.

### Tipologie di Controllo
Esistono principalmente 2 tipologie di controllo: aperto o chiuso.

##### Controllo ad ANELLO APERTO
Definito un **RIFERIMENTO**, improvvisamente c'è una richiesta esterna, quindi il valore impostato non è più raggiunto. Se nessuno avesse perturbato il sistema, non ci sarebbe stato un calo del valore.

--> Definisco un valore e porto il mio sistema a quest'ultimo. Questo quindi funzionerà fino a quando non ci sarà una perturbazione del sistema

##### Controllo ad ANELLO CHIUSO
Il mio sistema controlla che, ad esempio, la termperatura ideale sia uguale a quella impostata, di conseguenza il sistema agisce raggiungere la temperatura impostata (+ acqua fredda - acqua calda , o viceversa)

--> Misuro il valore in uscita, controllo, prendo delle decisioni e agisco. Tutto questo per tenere costante questo valore.

### Control loop (CHIUSO)
- **SET point**: punto che vogliamo raggiungere
- **Controller**: in base a ciò che gli è stato chiesto e ai dati che riceve, **prende una decisione**
- **Esecuzione della decisione**

In un anello di controllo chiuso ho bisogno di qualcuno che pensi, di qualcuno che faccia e di qualcuno che misuri. Questi 3 elementi si traducono in **dispositivi industriali**:
- **DISCRETE CONTROLLER**, dispositivo che agisce in maniera molto specifica
- **CONTROLLER DISTRIBUITI**, tanti piccoli controller locali che producono un'azione GLOBALE, come l'apertura/chiusura di una valvola
- **CONTROLLER A LOGICA PROGRAMMABILE o PLC**, in grado di mettere in pratica della azioni di controllo programmate da una persona, i **comportamenti** vengono eseguiti tramite degli **attuatori**

- **SENSORE INDUSTRIALE**, esistono moltissimi tipi di sensori: di posizione, di presenza, di temperatura, di umidità,... in definitiva sono **oggetti in gradi di misurare**
- **ATTUATORI**, sono i componenti in grado di **eseguire i comportamenti** che gli sono state inviate dai controller. Esistono vari tipologie di attuatori:
	- **Elettrici**
	- **Pneumatici**
	- **Meccanici**, in grado di **trasformare il moto da rotatorio a LINEARE**

