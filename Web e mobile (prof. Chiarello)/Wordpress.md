# Wordpress
Wordpress è un CMS, è un gestore di contenuti.
Un CMS da la possibilità di creare facilmente siti web, ha bisogno di un server web apache e di un **database**, per inserirci tutti i collegamenti tra le pagine.

Credenziali database: root - root

Su xampp shell mysql:
	*mysql -u root -p*  

NB. La password è vuota

**Comandi shell mysql:**
- show databases;
- use nome_database;
- show tables;

- quit (per uscire)

Credenziali wordpress local:
User:	admin
PSW:	

#### Consigli su Wordpress:
- **pagine** sono dei contenuti statici
- **articoli**: contenuti dinamici

Wordpress è il CMS più attaccato al mondo. Servono dei plugin per fare il **backup** del sito e per la **privacy** per percorsi brevi, o per la mappa del sito

Come faccio ad indicizzare il mio sito?
- Google analytics
- Inserire delle parole chiare nel sito

Le pagine su wordpress vengono nominate con dei numeri, meglio sostituirli con dei **permanent-link**

NB. https://material.io/design per indicazioni su dimensioni, formati, colori

www.agid.gov.it riporta le dichiarazioni di accessibilità. Basata su legge Stanga del 2004

Legge dei 3 colori per i siti, stessa cosa per i font, i contenuti devono essere raggiungibili in 3 click

![[vedi slide su come progettare sito web]]


---- 
**COMPITO:** Traspondere su altervista ciò fatto in locale
1. Attivare database (con nome database, nome utente e password)
2. Caricare con ftp il contenuto dello zip di wordpress
3. Nome utente e password di wordpress complicate quando il sito è online e mettere la cartella di wordpress in una con un nome diverso che non centra nulla


##### Template requisiti
È importante compilare il documento che specifica i requisiti e eventuali servizi del sito web, ecc.


#### Utilizzare strumenti di verifica
![[vedi sezione su classroom]]

- **Accessibility** : 

- **CookieBOT** : controlla se il sito sta utilizzando i cookie in modo conforme al GDPR.
NB. Ci possono volere anche 24h per questa verifica

- **Test Mobile Friendly** : per verificare se il sito viene visualizzato correttamente anche su dispositivi mobile

- **Plugin per gestione dei Cookie**

- **Velocità caricamento del sito web**

##### diagrams.net
Permette di utilizzare dei mockup, dei framework che permettono di descrivere graficamente la struttura del nostro sito web.

#### Strumenti di backup, rispristino e trasferimento
**Akeeba backup**

NB. quando si trasferisce un CMS bisogna trasferire il database e tutta la parte hosting. Akeeba backup fa il trasferimento/backup di entrambe le due cose.

##### Il sito web deve avere assolutamente una MAPPA