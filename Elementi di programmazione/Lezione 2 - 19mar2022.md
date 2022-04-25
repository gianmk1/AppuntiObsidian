# Come funziona python?
Possiamo distinguere 2 tipologie di linguaggi:
- **COMPILATO**
- **ESEGUITO**

Python è un linguaggio interpretato, noi scriviamo un codice ad alto livello e questo viene subito interpretato. 

*Quali sono gli step che esegue l'interprete di python?*
1. La prima cosa che viene fatta è il **controllo della sintassi**, che ha come input il codice che noi scriviamo. Se questo procedimento non va a buon fine, avremo come output un errore. Se invece è tutto corretto, viene dato come output il codice in byte (linguaggio binario)
2. Il codice risultato viene **interpretato dalla PVM (Python Virtual Machine)**. Python crea un ambiente virtuale: su questo viene eseguito il codice python che noi abbiamo scritto. Questa ritorna gli output

	**NB**. Anche nella PVM abbiamo degli input che sono quelli dati dall'utente (funzione input)
	**NB**. Anche se sintatticamente è tutto corretto ci possono comunque essere degli errori in esecuzione, anche questi vengono ritornati come output.

## Schema a blocchi
Schema utile per descrivere/capire il funzionamento di un programma.
Ogni blocco ha una funzione generica, es. *attuatore*, *inizio-fine programma*, ...

*Alcuni blocchi:*
- Il **primo blocco** (ad elisse) è il blocco di INIZIO o FINE.
- **Attuatore** (rettangolo) è il blocco che fa qualcosa
- **Blocco Input/Output** (romboide) è il blocco per un print o un input
- **Decisionale** (quadrato girato a 45gradi), è un if: ci sono 2 possibili vie

