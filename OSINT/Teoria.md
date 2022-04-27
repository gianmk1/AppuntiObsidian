# Open Source Intelligence - OSINT
Diventare esperti OSINT è molto difficile poichè ci sono molti strumenti che vengono utilizzati in questo ambito, e le conoscenze devono essere ampie.

OSINT viene utilizzato anche nella fase di **information gathering** per ricavare informazioni più o meno tecniche.

*L'informazione è li fuori, nella rete, chi sa come e dove cercarla detiene il potere.*
<br>

## Introduzione al concetto di OSINT
L'OSINT è una ricerca di informazioni da fonti pubbliche, disponibili a tutti. Non è detto però che essendo disponibili a tutti, tutti riescano ad utilizzarle. È quindi una **ricerca da fonti aperte**, possono essere però nascoste.

La parola **intelligence** è sempre stata utilizzata solo in ambito militare.

OSINT è ricerca da fonti aperte, ma esistono anche altre discipline:
- **IMINT**: elaborazioni immagini derivanti da satelliti, aerei spia, droni
- **CLOSINT**: analizi di informazioni da **fonti CHIUSE, non accessibili a tutti**

Le informazioni nel web rimangono nel web per sempre.

#### Campi e settori in cui OSINT è maggiormente richiesto
Governo, finanza, telecomunicazioni, infrastrutture critiche,...

#### Tipi di osint
Dal punto di vista della sicurezza possiamo separare OSINT in:
- **Offensiva**: raccogliere informazioni prima di un attacco
- **Difensiva**: conoscere gli attacchi contro l'azienda

L'OSINT può essere utilizzato sia **per difendersi** (cercare se ci sono informazioni delicate della propria azienda), o **per attaccare** (trovare informazioni accessibili che dovrebbero essere riservate, es. bilancio aziendale, password utenti,...)

#### Processi dell'OSINT
1. **Identificare la fonte**, dove possiamo trovare le informazioni
2. **Raccolta**, ottenere dati rilevanti dalla fonte identificata
3. **Data processing**, elabora i dati acquisiti e ottiene le informazioni significative
4. **Analisi**, unire i dati acquisiti da più fonti
5. **Report**, create un report finale

NB. Google non è l'unico motore di ricerca utile.

#### Quali informazioni cercare?
- Infrastruttura tecnologica, IP, nome host, servizi, reti, ...
- **Banca dati**
- Documenti, presentazioni, fogli di calcolo
- **Metadati**
- **Email e ricerca dei dipendenti**, es. cercare se una mail è stata compromessa

I **metadati** sono dati che **arricchiscono le informazioni** di un file, possono essere: autore, data di creazione, data di modifica,.. un metadato di una foto può dirci anche il modello di dispositivo con cui è stata scattata, o anche **dove è stata scattata la foto**.

#### Obiettivi finali dell'OSINT offensivo
- Ingengeria sociale
- Negazione del servizio
- Attacchi brute-force
- Furto di dati

#### Alcuni strumenti nel web
- Google
- [Shodan](https://www.shodan.io/) , è un motore open dove è possibile trovare qualsiasi cosa che abbia un indirizzo IP, i risultati posssono essere protetti o meno
- [Censys](https://censys.io/)
- Fofa
- [Archive](http://archive.org/) , per vedere com'era nel tempo un determinato sito
- [Have I been pwned?](https://haveibeenpwned.com/)

**NB**. Se una risorsa è protetta è provo ad accedervi sto compiendo un'effrazione.
**NB2**. Vedi repo condivisa

In un potenziale repo di una mail compromessa:
- In quali data breach è stata ritrovata la mail e relativa psw
- Consigli utilii: cambiare password, ...

[TheHarvester](https://github.com/laramies/theHarvester)

#### Google DORKS
Tramite delle ricerche mirate su google possiamo trovare qualsiasi cosa.

#### Enumerazione DNS/Sottodominio
Esistono anche strumenti che ci permettono da un IP a risalire al nome del sito, o viceversa. In più, l'enumerazione dei sottodomini è il **processo di ricerca di sottodomini validi (risolvibili)** per uno o più indirizzo IP.

[Whois Lookup](https://whois.domaintools.com/), permette di ritornare l'IP di un sito, e altre informazioni

#### Mappa di rete
A noi potrebbe interessare create una mappa della rete di una certa azienda. Che programmi girano? Che programmi hanno? Possiamo **ricostruire gli asset dell'azienda**.

In questo modo posso trovare delle possibili vulnerabilità.

**NB**. Spesso alcune informazioni utili si possono ricercare anche tramite le **offerte di lavoro troppo specifiche**, dove vengono specificate: versioni dei software utilizzati, macchine utilizzate,...

#### Cosa fare con i dati raccolti?
Devo **capire la pericolosità delle informazioni raccolte**, devo quindi fare una **Valutazione del Rischio**.

La pericolosità di un informazione trovata si calcola tramite:
- **Facilità** di trovare un informazione
- **Possibile utilizzo di quell'informazione**

![[inserisci immagine slide quadrati verdi-gialli-rossi]]

#### Qual è il vantaggio dell'OSINT?
- **Meno rischioso**, l'utilizzo di informazioni pubblicamente disponibili per raccogliere informazioni non comporta alcun rischio rispetto ad altre forme di intelligence
- **Conveniente**, la raccolta di strumenti OSINT è generalmente meno costosa rispetto ad altri fonti intelligence.
- **Facilità di accessibilità**, gli strumenti sono accessibili a tutti, e le fonti OSINT sono sempre disponibili
- **Mancanza di problemi legali**, le informazioni sono pubbliche
- **Aiutare gli investigatori finanziari**, gli evasori fiscali spesso vengono scoperti proprio tramite indagini di OSINT
- **Lotta alla contraffazione online**, le tecniche OSINT possono essere utilizzate per trovare prodotti/servizi falsi e ridurre le forze dell'ordine a chiudere tali siti o inviare avisi agli utentei affinchè smettano di trattarli.
- **Mantenere la sicurezza nazionale e la stabilità politica**, aiuta i governi a comprendere gli attaggiamenti dei loro cittadini

La parte OSINT è importante e viene ancora molto trascurata da attaccanti e **soprattutto da difensori**.

#### Tipi di raccolta intelligence
- **Passivo**: utilizzo dei tool senza mai interagire direttamente con la struttura/persona coinvolta, quindi **questi non possono essere allertati tramite alcuni dispositivi di sicurezza** --> OSINT

- **Attivo**, agisco in maniera *aggressiva* all'interno di un sito (ad esempio). **Possiamo essere identificati** da strumenti come **IDS** (sistema rilevamento intrusioni) e **IPS**. In questo caso **si cerca di sorpassare le difese della risorsa** e quindi **NON si accede più solo a informazioni pubbliche**. Comportano **conseguenze legali**.
**NB**. Genera un traffico di rete **anomalo e rilevabile** 


- **Semipassivo**, è una via di mezzo, modalità attiva che si svolte sotto la soglia di rilevamento, più costosa, **genera un traffico molto limitato**. --> STEALTH INTELLIGENCE

#### Informazioni (SPI)
Le informazioni possono essere di diverse tipologie:
1. Informazioni generiche
2. Informazioni personali
3. **Informazioni personali sensibili**
4. **Informazioni anonime**, che possono essere utilizzate per report statistici

**NB**. L'**indirizzo IP è sempre un dato PERSONALE** perchè comunque è riconducibile ad una persona. Come anche il **MAC address** poichè associato ad una scheda di rete.

**NB2**. È possibile mascherare il MAC address, al riavvio però ritornerà quello iniziale.

<br>
<br>

## Strumenti e Tecniche per effettuare OSINT
Gli strumenti e tecniche rappresentano una parte in continua evoluzione, con cambiamenti difficili da seguire.

#### Covert Accounts
Alcuni li identificano come **Sock Puppets**, cioè un **account finto ma curato nei minimi dettagli**. Gli account nascosti sono profili online che non sono associati alla nostra vera identità.

L'utilizzo del proprio account personale potrebbe rilebrare la nostra vera identità.

#### La mail da utilizzare
È fondamentale utilizzare una **mail generica** per i propri dati nascosti, per scaricare alcuni tool,... . È meglio **non utilizzare provider mail popolari** (Google, ProtonMail, Outlook), si consiglia [Fastmail](https://www.fastmail.com/)

#### TOR
Tor utilizzato da solo **non ci rende completamente anonimi**, dobbiamo usarlo in concomitanza con una **VPN** (importante che supporti OpenVPN). 

**NB**. Non esiste la privacy **assoluta**.
**NB2**. Possiamo anche acquistare una SIM anonima prepagata.

#### I diversi target
I possibili target possono essere principalmente:
1. Aziende
2. Individui

**Target: AZIENDE**, le informazioni richieste possono essere:
- Mail dei dipendenti
- Indirizzi IP associati a quell'azienda
- Estrazione di informazioni da dispositivi esposti sulla rete come telecamere, router,...
- Documenti sensibili dell'azienda

#### Alcune fonti:
- Internet
- Social
- Giornali
- Satelliti
- Alcuni servizi a pagamento

<br>
<br>

## Sicurezza dell'operatore
Quando si opera, a seconda dell'operatore e del contesto, bisogna cercare di restare il più possibili anonimi. Il problema di quando si crea un account fittizzio è la **coerenza delle informazioni**.

*Esempio: creare un codice fiscale fittizzio*

Nonostante TOR e la VPN lasciano inanomimato una parte fondamentale, il **Sistema Operativo**. Per questo possiamo utilizzare delle **Virtual Machine**.

In genere i tools sono:
- Virtual machine
- TOR
- VPN
- Tails (distro linux)
- Fake profiles
- Sock puppets
- SMS
- VoIP
- Fake mail
- Moskow rules
- Programmi per mappe mentali, [xMind](https://www.xmind.net/)

#### Tor 
*vedi sopra*

#### VPN
*vedi sopra e slide*

#### Tails
È un sistema operativo basato su Debian, è dotato di molte applicazioni perconfigurate per mantenere la sicurezza.

- Tails **cripta tutto prima di inviare tramite TOR**, questo comporta una cifratura ancora più presente.
- Bisogna configurarlo in modo che cancelli di default i metadati dei file

#### Sock Puppets
Sono più complessi di semplici profili fake. Vengono curati in ogni loro dettaglio in modo da risultare il più verosimili possibile.
Gli investigatori possono utilizzare questi account per ricavare informazioni, gli hacker possono utilizzarli invece per sferrare attacchi di Social Engineering.

NB. Signal è uno dei client messaggistica più sicuri.

#### Creare un Sock Puppets
- [Fake Name Generator](https://www.fakenamegenerator.com/)
Questo sito ci permette di creare la base per la nostra identità fittizia. Le informazioni che vengono proposte hanno una coerenza tra di loro.

- Un altro possibile sito è: (solo per identità femminili)
[Elf Qrin's Lab](https://www.elfqrin.com/fakeid.php)

- È importante anche avere un indirizzo mail *da combattimento*, è consigliabile utilizzare un indirizzo [Mail.com](https://www.mail.com/)

- Per immagini fake possiamo utilizzare [ThisPersonDoesNotExist](https://this-person-does-not-exist.com/en), che ritorna immagini create da un **intelligenze artificiali**, in questo modo non si ruba l'identità di nessuno.

- **Burner Phone e SIM card**, i burner phone sono telefoni che non sono connessi in alcun modo alla nostra identità. Il phone burner e la SIM card saranno collegate al solo account fittizio.

- Alcune app di messaggistica sicure sono **Tor Messanger**, **Signal**
 
Creato il nostro account sock per essere credibile deve **avere una vita social** con un minimo di contenuti, follower... la cosa importante dovrebbe essere quindi **far crescere nel tempo il nostro profilo social**.

#### Regole di Mosca
*vedi slide*

<br>
<br>

## Descrizione dei motori di ricerca
*Non è detto che se una risorsa non la trovi Google, altri motori non la possano trovare.*

Tramite degli **Spider** che navigano all'interno della rete, riportano tutto quello che trovano, se in un determinato indirizzo IP trovano del contenuto web, riportano l'indirizzo in un database. Tramite le parole più presenti all'interno della risorsa, si indicizza il sito.

Questo procedimento viene ripetuto all'infinito su tutte le fonti trovate.

Google, come altri motori di ricerca, mostra o meno i siti che decide lui e le ricerche sono personalizzate per ogni utente (in base a ricerche precedenti, geolocalizzazione,...) grazie alla **profilazione**.

**DuckDuckGo** è un altro motore di ricerca estremamente ampio che riporta per tutti gli utenti gli stessi risultati.

**NB.** Quando ricerchiamo informazioni è importante **utilizzare più motori di ricerca**, anche **stranieri**.

Dobbiamo **ottimizzare la ricerca**, in modo da raggiungere il prima possibile la nostra risorsa, Google offre una [Ricerca avanzata](https://www.google.com/advanced_search), è bene pero partire **dalla cosa più ovvia**.

#### Analisi tramite motore di ricerca
Possiamo **ottimizzare la ricerca**, in modo da raggiungere il prima possibile la nostra risorsa, Google offre una [Ricerca avanzata](https://www.google.com/advanced_search), è bene pero partire **dalla cosa più ovvia**.

**NB.** Quando ricerchiamo informazioni è importante **utilizzare più motori di ricerca**, anche **stranieri**.

#### Alcuni operatori Google
- Per ricercare all'interno dei siti social media, utilizzare la seguente dicitura:
**@facebook:nome cognome**

- Per cercare la parola che viene dirattamente dopo e per i suoi sinonimi:
**excel ~guide**
*Se non troverà nulla con "guide", cercherà "tutorial"*

- L'operatore **OR** viene molto utilizzato anche nelle ricerche (uno o l'altro), non verrà mai ritornato un link con entrambe le parole
- L'operatore **AND** per correlare chiavi di ricerca
- Con **-**, **ferrari -spumante**, per mostrare le ricerche "ferrari" non correlate allo spumante
- I **..** per cercare all'interno di un intervallo di tempo, *es. apple bilanci 2010..2015*
- Per cercare pagine web all'interno di un sito: **related:amazon.com**
- La parola **info:** per restituire tutte le informazioni che Google conosce sul sito web dato, *es. info:amazon.com*
- **define:information** mi da la definizione della parola
- **"free sms service"**, ritorna tutti i siti dove **trova esattamente la stringa**

#### Google Dorks (o Google Hacking)
Sono molto utilizzate anche in attività di hacking.
Utilizziamo questi Dorks riusciamo a ricavare molte informazioni in fase di OSINT.

Sono delle **query particolari che ci permettono di semplificare le nostre ricerche** ottentendo informazioni che altrimenti sarebbero poco accessibili.

*Alcuni esempi:*
- **computer forencis site:gov**, permette di cercare "computer forencis" nei siti **.gov**
- **computer forencis site:clusit.it**, permette di cercare "computer forencis" all'interno del sito **clusit.it**
- **allintitle:Nidah hassan**, permette di ritornare ricerche con "Nidah hassan" presente all'**interno del titolo**
- **allintitle:Nidah hassan**, permette di ritornare ricerche con "Nidah hassan" presente all'**interno del testo del sito**
- **allinurl:OWASP**, permette di ritornare ricerche con "OWASP" nell'url del sito
- **owasp filetype:pdf**, permette di ritornare **tutti i documenti specifici** con **estensione** specificata (qui PDF) dove all'interno è presente "OWASP"

Esistono database con tutti i Google Dorks chiamato [**Google Hacking Database**](https://www.exploit-db.com/google-hacking-database)

*Altri Google dorks*:
- **index of /backup** restituirà un elenco di server non protetti che contengono dati di backup
- **robots.txt "Disallow:" filetype:txt**, il file robots.txt indica ai crawler dei motori di ricerca i sottodomini del sito che non devono essere indicizzati, in altre parole **ignorare il processo di indicizzazione**. Con questo Dork troviamo i file robots.txt dove sono presenti voci "Disallow"
- **password filetype:txt**, per trovare file txt con la parola "password" all'interno
- **filetype:txt password farmacia**, per trovare file txt con la parola "password" e "farmacia"
- **site:italia.it & filetype:pdf** 
- **budget site:gov filetype:xls**, restituisce tutti i fogli di calcolo dei siti .gov che contengono la parola budget
- **cache:sito.it**, per visualizzare la versione più recente del sito memorizzato da Google
- **site:youtube.com**, mostra tutte le pagine indicizzate del sito "youtube.com"
- **site:youtube.com recensione**, mostra tutte le pagine che contengono "recensione" all'interno del sito "youtube.com"
- **inanchor:amazon.com**, ricerca la parola all'interno degli anchor text
- **allintext:username filetype:log**, ricerca tutti i file **.log** dove all'interno è presente la parola username
- **filetype:xls inurl:"email.xls"**, ricerca tutti i file xls con email.xls nell'url


**NB**. Un **backlinks** è un link che rimanda ad un altro sito. 
**NB2**. I file di log sono tra i più riservati all'interno di una risorsa

Questo dimostra come i Google Dorks possono essere **combinati tra di loro**

*Altri tipi di Google dorks:*
- **movie:inception**, per trovare informazioni relative al film
- **maps:vicenza**, per mostrare la mappa della località 
- **in:..**, converte in unità di misura
- **OR**, permette di cercare l'uno o l'altro dei termini inseriti
- **AND**
- **AROUND(#)**, *es. cult AROUND(3) adv*, restituirà i risultati in cui "cult" e "adv" sono distanziate di 3 parole

- **Trovare pagine NON sicure**, in alcuni siti ci sono solo alcune pagine HTTPS:
*site:www.italia.it -inurl:https*


#### Altri motori di ricerca
Alcune nazioni hanno il proprio motore di ricerca:
- [Baidu - Cina](www.baidu.com)
- [Yandex - Russia](www.yandex.com)

*Vedi slide per altri siti*

Quindi quando facciamo OSINT è importante ricercare anche su altri motori di ricerca al di la di Google. *Es. se sto cercando informazioni su una persona cinese andrò a ricercare anche su Baidu*

**Indicizzazione**, si intende quanto un motore di ricerca inserisce il sito e tutte le sue pagine all'interno del database del motore di ricerca per facilitare la ricerca dell'utente

<br>
<br>

## Fonti standard e non
Esistono diverse fonti di informazioni standard e non

- **Dati open source (OSD)** sono dati generici provenienti da una fonte primaria
- **Informazioni open source (OSINF)** si tratta di dati generici che sono stati **sottoposti ad un filtraggio** per soddisfare un criterio o un'esigenza specifica. *Es. libri su un argomento specifico, intervista,...*
- **Intelligence open source (OSINT)** si tratta di informazioni che sono state **scoperte, filtrate e designate** per soddisfare un'esigenza o uno scopo specifico.

Quando le informazioni non sono facilmente capibili dobbiamo trasformarle in un report capibile.

<br>
<br>

## Data carving
#### Proprietà di un file
- Nome
- Tipo (=estensione)
- Contenuto
- Dimensione
- Posizione sul disco
- Ultimo accesso
- Ultima modifica
- Data creazione

In un file però può mancare l'estensione, in questo modo non riusciamo subito a capire la tipologia di file.

I **MAGIC NUMBER** sono dei numeri all'interno del file, ogni file è caratterizzato da avere un **hex all'inizio del file**.
*Es. i file JPEG iniziamo sempre con "FF D8"*

La tipologia di un file NON è data dall'estensione ma dal primo byte dell'esadecimale

#### Metadati
All'interno di un file sono presenti anche dei **metadati**.

#### Steganografia
È l'arte di **nascondere informazioni all'interno di altri file**.
La stegonografia venne utilizzata per la prima volta da Giulio Cesare.

<br>
<br>

## Analisi delle Fonti Aperte - OSINT
Esistono molte forme di Intelligence (al di la dell'OSINT):
- Financial Intelligence
- Geospatial Intelligence
- Photo Intelligence
- Communications Intelligence
- ...

OSINT = Open Source INTelligence, dove:
- **Open Source si riferisce alla ricerca di informazioni tratte da fonti liberamente disponibili** (non all'open source)
- Si differenzia dalla attività di Intelligence in quanto le **informazioni NON sono ottenute "illegalmente"**

*Non si parla solo di raccolta ma anche di verifica e analisi delle informazioni.*

**Open Source Data (OSD)** -> dati grezzi da una fonte primaria
**Open Source Information (OSI)** -> dati grezzi che possono essere messi insieme che fornisce filtri e validazioni
**Open Source Intelligence (OSINT)** -> informazione che è stata deliberatamente scoperta al fine di rispondere ad una domanda
**Validated OSINT (OSINT-V)** -> l'informazione non è solo stata trovata ma anche VERIFICATA

**NB**. Spesso l'OSINT viene utilizzato per una valutazione di sicurezza.

*Se prima era sufficiente analizzare qualche giornale o libro, oggi è molto più complesso.*

Ogni servizio internet raccoglie informazioni sui suoi utenti (log, statistiche)

#### Sintesi direttive NATO
*Vedi slide*

#### Sistema conferma informazioni
Le **informazioni** che troviamo **devo essere verificate**:

*Es. Trovare la data di nascita di una persona: se trovo una pluralità di fonti concordi posso considerarle valide.*

**NB**. Una ricerca accurata RICHIEDE TEMPO!

#### Problemi operatori OSINT
- Linguaggio/barriere culturali (le informazioni non sono solo in Italiano e Inglese)
- Troppa fiducia nei tools automatici
- Disinformazione:
	1. Le informazioni possono essere **false**
	2. Le informazioni possono essere **manipolate**
	3. **Impossibilità di accesso legale all'informazione**

#### Caso Koobface
Colpisce gli utenti di Facebook:
Dopo l'infezione rimanda la connessione internet su pagine di Rogueware, inoltre tenta di ottenere informazioni sensibili delle vittime come numeri di carta di credito o dati di accesso

*Un ricercatore è riuscito a scoprire numero di telefono, nome e indirizzo del botnet master, cercando tutti i domini riconducibili allo stesso IP, uno di questi era registrato con una mail diversa dalle altre.*

#### Modalità di fase OSINT
- **MANUALE**, la ricerca viene effettuata direttamente dall'operatore
- **AUTOMATICA**, la ricerca viene effettuata tramite strumenti parametrizzabili
	- Serve una scrematura
	- Potenzialmente molto efficace
	- **Rischio di falsi positivi dovuti a AI non evoluta come analista**

La **soluzione è un MIX** tra le due. Tools e API possono automatizzare le attività ma una gran parte dei risultati sono **basati sull'intuito**. Inoltre l'**esperienza** aiuta molto.

#### Strutturare le informazioni
- **Link analysis**, l'analisi dei collegamenti è una tecnica di analisi dei dati utilizzata per **valutare le relazioni tra i nodi**.
- 
- **Mind mapper** (o **Mappa mentale**)

<br>
<br>

## COSA e DOVE cercare
**Come pianifico l'investigazione OSINT?**, bisogna definire:
- Target
- Obiettivi
- Regole di ingaggio

*Lo scopo non è un report da 200 pagine superflue, devo concentrarmi sulle informazioni utili*

#### Pianificazione delle fasi - OSINT
1. **Definire obiettivo e fonti**: elenco le mie fonti
2. **Raccolgo i dati** dalle fonti identificate nella fase precedente
3. **Analizzo e confronto** i dati raccolti
4. **Diffusione dei report** contenenti i dati precedentemente raccolti e rielaborati
5. **Misuro il gradimento del cliente**

**NB**. Nei report c'è bisogno di una **approvazione** e **revisione**

#### Classificazioni delle fonti
- Informazioni generali
- Informazioni a pagamento
- Esperti
- **Documenti "grigi"** (brevetti, report, pubblicazioni ad uso interno)
- ODS, dati grezzi, generici
- OSIF, informazione pubblica che ha subito un processo di filtraggio
- OSINT, mix tra ods e osif

#### Come vengono trattate le fonti?
- **Strumenti di hacking**
- **Avanzato uso dei motori di ricerca** (google dorks)
- **Utilizzo di portali di investigazioni online**

#### Possibili fonti
- Motori di ricerca
- Social network
- Chat
- Blog
- Siti di vendita
- Siti di immagini o video sharing
- Siti di incontri
- Giornali, pubblica amministrazione, camere di commercio
- Archivi pubblici, organizzazioni governative
- Siti istituzionali, Deep WEB
- Servizi specializzati nella ricerca, valutazione e vendita info
- Informazioni tecniche dalla rete internet (es. **Maltego**)

#### Alcune metodologie
- Ricerca per parole chiave
- Analisi delle immagini
- Correlazione informazioni
- Analisi dell'ambiente
- Analisi dei contatti (tramite un'altra persona correlata al mio target)
- Analisi informazioni tecniche internet

#### Devo cercare tutto?
NO, la ricerca:
- Dipende dal soggetto della ricerca
- Dipende dalla domanda a cui bisogna rispondere
- Le **keyword e gli argomenti cambiano** nel corso dell'analisi
- Bisogna correlare le risposte per individuare **nuove direzioni di ricerca**

**NB**. È importante lavorare ordinate altrimenti si rischia di perdere il filo della ricerca

#### Alcune problematiche
- Troppe informazioni
- Capire se una informazione è vera, falsa o manipolata
- Difficoltà linguistiche

#### Cognitive BIAS
È un pattern sistematico di deviazione dalla norma o dalla razionalità nel giudizio.

In psicologia indica la tendenza a creare la propria realtà soggettiva, sviluppata sulla base dell'interpretazione delle informazioni in possesso, anche se non logicamente connesse tra loro. Questo **porta dunque a un errore di valutazione o a mancanza di oggettività di giudizio**.

**NB**. **NON dobbiamo dare interpretazioni/giudizi personali** (secondo me, probabilemente,...)

Quanto abbiamo un intuizione, ciò che vediamo lo elaboriamo per confermare la nostra intuizione --> *L'apparenza inganna*

Nel caso di giudizi/opinioni/intuizioni bisogna confermarli **in modo oggettivo**.

**NB**. Nella Cyber Security, tutto **deve essere dimostrato oggettivamente**

#### Creazione di un profilo del soggetto
- Lavoro, famiglia, amici, hobby
- Prodotti, mercato, clienti, fornitori
- Localizzazione geografica
- Studi, interessi

*Si può anche partire dal contrario*

#### Altri motori di ricerca
- **Pipl**, motore di ricerca specializzato su persone

**NB**. I motori di ricerca NON sono infallibili. Come funzionano?
- Spider o Crawler
- Un database che indicizza i risultati del lavoro dello spider
- Un motore di backend che analizza le richieste ed i contenuti del database, **assegnango il "rank" e fornendo i risultati in base ad algoritmi** proprietari che cambiano continuamente

**NB**. Il rank di una pagina aumenta nel caso altri siti puntino a quella pagina

**Non tutti i motori di ricerca sono uguali**, durante l'analisi OSINT quindi devo affidarmi a più motori di ricerca (anche di diverse lingue)

#### Google VS Bing VS DuckDuckGo
![[inserisci immagine della slide]]

*In molti casi i motori di ricerca si comportano in modo diverso...*

Spesso alcuni motori di ricerca vengono utilizzati solo per la specifica nazione

**NB**. La maggior parte degli strumenti di ricerca al di fuori degli USA raccolgono e memorizzano dati principalmente o esclusivamente dalla loro regione o paese

**Google.com** lavora in modo diverso da google.it e **fornisce più informazioni**


