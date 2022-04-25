# Introduzione alle vulnerabilità web
Al giorno d'oggi la maggior parte delle applicazioni sono via web.

#### Che cosa significa "hacking"?
- Prendere accesso a delle risorse
- Prendere dei file sensibili
- Rompere un'applicazione

Le motivazioni possono essere variabili...

#### Chi può essere un "hacker"?
*Un hacker è una persona molto skillata (informaticamente parlando) che usa la propria conoscenza per raggiungere un obiettivo o uno scopo.*

Un hacker però NON deve per forza essere *super skilled*:
Se il sistema che si vuole hackerare è estremamente sicuro (es. NASA) un hacker deve essere estremamente skillato, se il sistema è però normale non c'è bisogno di essere così skillati.

Quando si parla di hacking bisogna sempre definire la vittima e le possibili difese di quest'ultima.

#### Scenario
- **Chi è l'hacker che dobbiamo combattere?**
- **Chi è il difensore?**, solitamente quando si parla di cybersecurity la difesa è fatta da persone abbastanza comuni, con sistemi non super sicuri. Spesso la security non è la priorità dello sviluppo di un sistema applicativo industriale.

Molto spesso (purtroppo) la cybersecurity è un **aspetto secondario**.

### CTF
Quando noi siamo un attaccante e abbiamo un target system dobbiamo capire come bisogno exploitarlo.

La metodologia delle CTF è quella che si va ad applicare anche nella realtà.

#### Come si procede?
1. **Information gathering**, raccogliere le informazioni sul target, es. tipo di linguaggio utilizzato, i protocolli che vengono utilizzati nell'applicazione,... . 
2. **Cercare le vulnerabilità**, una volta scoperto, ad esempio, il linguaggio, possiamo cercare le vulnerabilità su questo. Anche tramite dei **tool**

### Esempio 1
**Toward Data Science** è una rivista online dove molti professionisti postano il loro tutorial. 

*Pur essendo gratuito richiede dopo un po'di tempo di fare il login.*

Utilizziamo l'**INSPECT del browser**.

La CONSOLE serve per utilizzare il javascript della pagina.

SOURCES significa le risorse che arrivano con la pagina.

NETWORK serve per monitorare lo scambio di pacchetti tra la pagina e la web app.

APPLICATION ci sono le WebSQL inviate e i Cookies