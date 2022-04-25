# Kathará
Laboratori base:
- https://github.com/KatharaFramework/Kathara-Labs/wiki/Basic-Topics

---

Per creare un nuovo laboratorio, creare una nuova cartella con file lab.conf con la configurazione scritta in formato kathará

pc1[0]=A			scheda di rete 0 del PC1
pc2[0]=B

r1[0]=A
r1[1]=C

r2[0]=B
r2[1]=C

Creo una cartella per ogni nodo della rete: PC1, PC2, R1, R2
Poi servirebbero i file di configurazione dei nodi

Faccio partire il laboratorio con comando kathara lstart

Comando **route** mostra la tabella di routing

Per configurare una scheda: *es.* ifconfig eth0 150.7.2.1/25

Gateway 0.0.0.0 = senza bisogno di routing

Netmask 255.255.255.252 = maschera di rete di connessioni point to point


ESERCIZIO PACKET TRACER:
![[file xournal vecchio]]

**NB** Su docker nel caso di errore 500 dare il comando `docker system prune -f`


il file **lab.conf** istruisce kathara su quali sono le schede di rete del computer e come esse si parlano

I file di startup, uno per ogni dispositivo, contengono: la configurazione delle schede di rete e le tabelle di route

## Firewall
- Un firewall permette agli utente di una rete interna di iniziale connessione solo con alcuni servizi esterni (versione BASE)
- Limitare la possibilità di accessi dall'esterno solo ad alcuni server appositamente dedicati. In questo caso è opportuno separare i server in una rete a parte (DMZ)

NB. Active Directory: per gestire le utente, alla fine è un server di autenticazione. Un server del genere non starà in una DMZ ma in nella rete interna. Un server WEB invece verrà posto in una DMZ

NB. Quindi posso avere dei server anche nella rete interna, se saranno utilizzati solo da utenti interni.

#### Operatività dei firewall
I firewall sono **middle-box** perchè operano su diversi livelli.
In particolare gli stateful firewall operano filtraggi in base a:
- porta TCP o UDP sorgente/destinazione
- indirizzi ip sorgente/destinazione
- interfaccia sorgente/destinazione
- stato di eventuali connessioni aperte o in fase di attivazione

I firewall possono essere personali (desktop firewall) o network firewall che sono posti all'estremità della rete. Un network firewall può essere un dispositivo ad hoc o regole impostate nel router.

NB. Anche quando la rete è protetta da network firewall è meglio configurare dei desktop firewall, anche per aumentare il livello di protezione e per proteggersi da attacchi provenienti dall'INTERNO.

#### Linux firewall: iptables
Iptables è un software che ragione con il concetto di catena:

- Prerouting: contiene le regole di NAT

Iptables consente sulle catene input/output/forward di decidere se far passare i pacchetti o meno in base a delle regole

Di default iptables LASCIA PASSARE tutto

Leghiamo la regola ad un'interfaccia 
