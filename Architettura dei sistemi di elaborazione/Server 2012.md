# Server 2012
Nel server posso avere molteplici dischi.

Utilizza (al posto di raid x) il: mirroring (raid 1), striping (raid 0), spanning (raid 3-5)

MIRRORING -> Tutti i dati di un disco vengono copiati su un altro e viceversa
STRIPING -> velocità maggiore, lo stesso dato è memorizzato su più dischi
SPANNING -> Utilizza un disco di parità, più veloce del mirroring ma un pò meno sicuro
(Vedi su wikipedia il raid 3 e raid5)


Quando installiamo server 2012 è a **livello di dominio**, quando invece deve gestire i domini bisogna far salire il server da livello di dominio a **livello FORESTA**.

Tutti i domini insieme sono una **FORESTA**

ACTIVE DIRECTORY è la gestione di tutti i permessi degli utenti/dischi/ecc. in tutto il server

## ACTIVE DIRECTORY
1. Alzare il server a **livello di dominio**
2. Creare un utente
3. Collegarsi da Win7 a Server2012 tramite Active Directory

*utentecyber@itsmeccatronico.it*

ACTIVE DIRECTORY server oer gestire **gruppi di utenti**, **domini**