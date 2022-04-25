# Social Engineering
### Tipologie di Social Engineer
- Ladri di identità
- Broker di informazioni
- Governi
- Commerciali
- ...

### Perchè utilizzare la SE?
- Ottenere informazioni
- Sfruttare il sistema più vulnerabile, cioè l'**essere umano**

L'essere umano ha bisogno di relazioni. Questo bisogno può esser sfruttato.

### Alcuni possibili attacchi
- Servizio clienti
- Consegna pacco
- Supporto tecnico
- USB abbandonata
- Commerciale
- Pausa sigaretta

### 1 passo - Reconnaissance
Stessa fase dell'ethical hacking.
Più informazioni ho su una persona, meglio riesco a fare un'attacco!

1) **OSINT**:
Raccogliere tutte le informazioni aperte, utilizzando i social network (alcuni tool sono **TheHarvester , recon-ng , Sherlock**)

2) **Osservazione ed appostamenti:**
	- Mappatura edificio, stanze ed entrate
	- Orari di lavoro
	- Convenzioni (vestiario , idCard)
	- Fraternizzare con le persone
	- Terminologia specifica del settore

3) **Dumpster Diving**
Cercare nella spazzatura

### 2 passo - Pretext
**Si costruisce un personaggio**. Il concetto è quello di personificarsi in un'altra persona, costruendo anche un'identità digitale parallela.

### 3 passo - Accesso alla struttura

### 4 passo - Azione
- Mantenere la calma
- Ricostruire la mappa della struttura
- Pensare a come uscire in seguito (**gates**)
- Ricordare il proprio obiettivo e pianificare le prossime mosse
- Non parlare in modo negativo...

## Principi di Persuasione
### Reciprocity
**Principio di reciprocità**: meccanismo di far sentire in debito l'altra persona. È nirmale che una persona voglia ricambiare un favore, dopo aver ricevuto qualcosa.

**Alcuni esempi:**
- Offrire un caffè
- Scambiarsi i regali di natale
- Quid Pro Quo ("qualcosa per qualcosa")
- **Advance Fee Scam**

### Commitment and Consistency
L'essere umano **vuole essere coerente con se stesso**.
Non è bravo ad ammettere di aver cambiato idea o di aver sbagliato.

**Commitmet**: utilizzato per guadagnare un certo livello di fiducia.

**Alcuni esempi:**
- Giustificare le proprie scelte passate, anche se errate
- *Costo Sommerso*, continuare a pagare non per un guadagno, ma perchè ormai si è speso troppo

### Social Proof (o Riprova Sociale)
L'attitudine a conformarsi con il comportamente degli altri, quando non si sa cosa fare, oppure di trovare conferma delle proprie azioni nel giudizio altrui.

**Alcuni esempi:**
- Social Media, Influencer
- Identificarsi con un brand
- Situazioni di emergenza

### Authority
**POTERE**: possesso della capacità di controllare gli altri
**AUTORITÀ**: diritto di esercitare il proprio controllo sugli altri

*Diversi tipi di autorità:*
- Legale (superiore al lavoro, insegnante)
- Organizzativa
- Sociale

**Alcuni esempi:**
- Impersonare un superiore per richiedere informazioni, o direttamente denaro (es. **truffa del CEO**)
- Forze di polizia
- Esperti di un settore

### Liking
La tendenza a seguire e venire persuasi da chi e cosa ci piace.

*Un like su Facebook / Instagram fa piacere.
Il concetto di piacere è alla base dei rapporti interpersonali.*

**Alcuni esempi:**
- Moda, Design, Arte

### Scarcity
La **paura di perdere un'occasione perchè limitata**, oppure l'aumento del valore di qualcosa perchè limitato.

### Unity
La **condivisione di un'identità, dei nostri ideali, con altre persone**. Si distingue dalla Social Proof per il suo significato più profondo e la necessità di essere genuina.

NB. La famiglia è l'esempio di Unity più potente.


## Altre tecniche psicologiche:
### Framing
Porre una domanda, contestualizzandola in modo da predeterminare la risposta nel soggetto.

**Alcuni esempi:**
- 75% Magro VS 25% Grasso
- Emissioni ridotte del 10% VS Emissioni di 95 g/km

### Elicitation
L'atto di ottenere ed estrapolare informazioni in maniera indiretta.

Una corretta formulazione delle domande è fondamentale per l'Elicitation:
- Hai fame?
- Cosa vorresti mangiare?

**Preloading**: influenzare prima ancora della domanda.

<br>
<br>

### Il valore delle informazioni
Poche persone si rendono conto di quanto valgano veramente le informazioni. Alcune possono sembrare inutili, ma sono in realtà di grande importanza di Social Engineer

NB. L'attacante deve stare attento a non *farsi prendere troppo* e a non cadere nel suo stesso attacco (es. divulgando informazioni personali)

<br>
<br>
<br>

# Phishing
Il Phishing (addescaggio) serve a far abboccare gli utenti online con varie tecniche. Generalmente il vettore con cui si utilizza il phishing è la mail.

### Cosa vuole l'attacante?
- Azione fisica: l'attaccante invita tramite mail a fare un bonifico
- Furto di dati: l'attaccante riesce a ricostruire la nostra identità online
- Trasmissione di un payload ai privati: se voglio costruire una botnet, mando un virus a un privato che poi utilizzerò, ad esempio, per un attacco Ddos

#### Caso studio: Sony Data Breach
Nel 2015 Sony è stata attaccata tramite una mail di phishing sottoforma di verifica dell'Apple ID. 

#### Caso studio: Ukraine Power Plant
Gli hacker sono riusciti ad entrare (sono stati pagati, erano un gruppo APT). Hanno rubato le credenziali di un operatore tramite phishing

NB. APT = Advanced Persistent Treat, APT come gruppo (es. APT24). Oppure l'APT è anche un attacco che infetta l'azienda, prende qualcosa e poi esce. L'obiettivo è quello di NON farsi scoprire

### Call To Action
In genere nelle mail viene inserito un bottone, cioè la **call to action**.
Gli attaccanti devono creare una call to action forte che possa attirare il click dell'utente.
Solitamente la call to action NON è all'inizio della mail

Alcune tecniche:
- Motivazioni di urgenza
- Ricatto

## Tassonomia
Quello che abbiamo all'interno di una mail di phishing sono una serie di elementi, es il nostro nome utente, data di nascita,.. Tutti i dati presenti nella mail si uniscono a un serie di elementi che contribuiscono a rendere una mail di phishing ottimale:
- Dispositivo da compromettere
- Vittima: A chi lo sto mandando? Voglio una persona specifica (quindi una mail studiata per lui) o una qualunque? 
- Obiettivo: Dobbiamo fare una Botnet? O altro?
- Tematica e Contenuto
- Motivatore: Frasi che ci permettono di accedere alla mente di chi sta leggendo
- Metodo di "Exploitation": In quale modo inseriamo il virus all'interno del dispositivo della vittima?

#### Dispositivi da compromettere
- Computer personale: solitamente il più facile a cui accedere
- Computer aziendale: solitamente il più difficile, poichè più controllato
- Tablet / Smartphone
- Macchinario di una azienda
- Dispositivi IoT: es. smartwatch, lampadine iot
- Aereo / Treno / ...
- ...

#### Vittima
- "Una persona qualunque"
- "Una persona specifica"
- Un gruppo di persone accomunati da uno o più aspetti: *Voglio attaccare un comune, cerco la mail di tutti quelli che stanno in quel comune, o entro un certo raggio.* Es2: *Voglio attaccare i cittadini che hanno dei certi ideali*
- Executives, chi all'interno dell'azienda è più privilegiato

#### Obiettivo
- Guadagno economico
- Reputazione: l'attaccante vuole costruirsi una reputazione
- Senso di sfida
- Conoscenza
- Vendetta: conosco la vittima, quindi creo una mail di phishing molto costruita

#### Tematica e Contenuto
- Titolo: Deve essere accattivante
- Mittente
- Testo (inteso come contenuto)
- Link: Il link che vediamo può non essere quello reale a cui verremmo rendirizzati
- Software (malware): Si possono scrivere degli script se scriviamo una mail in HTML
- **Firma**: "certifica" chi sta scrivendo (non sempre)
- **TONO**: questo va più sul piano emotivo / sentimentale. Questo agisce sul "primo strato del subconscio", magari subito non ci colpisce ma abbassa la soglia di attenzione. 

#### Metodo di "Exploitation"
- Testo: se l'attaccante vuole far compiere qualche azione alla vittima (es. mettendo nel testo un indirizzo di un portafoglio BTC) in seguito ad un ricatto
- Link
- Malware:
	- come allegato
	- scaricabile tramite una pagina html

#### Motivatore
- Intrattenimento
- Social
- Ricompensa / Riconoscimento: *"Sei il 1000esimo visitatore, hai vinto un xyz !"*
- Curiosità
- Lavoro
- Urgenza: *Scarcicity o Urgenza*
- Paura: *ho la tua mail e la tua password e un tuo video privato. Si abbassa la razionalità della vittima.*
- Opportunità

<br>
<br>
## Contromisure
#### Come identificare e/o difendersi dal phishing?
- **Educazione alla cybersecurity**, educare i colleghi, soprattutto i meno tecnici, a riconoscere queste minacce
- Segnalazione rapida : che sarà inviata poi a Microsoft / Google / Amministrazione di sistema
- Blacklist , Whitelist , Greylist : sono liste pubbliche in cui sono presenti tutti i server che inviano mail spam. Un server che finisce in blacklist è difficile da toglierlo.
- Gestore delle password
- Autenticazione a 2 fattori
- Machine Learning: in base a tutte le mail che dai alla rete neurale da elaborare, questa impara quali sono di phishing
- *Computer Vision : algoritmi che guardano la mail come gli occhi di una persona*
- Ontologia

#### Educazione alla cybersecurity
- Scetticismo e non cedere agli impulsi
- Training alla cybersecurity continuo e costante
- Indicatori buoni ed indicatori inaffidabili

Possibili modalità di training:
- Lezioni frontali
- E-Learning
- Simulazioni di phishing, il più efficace. 
- Pratica con strumenti anti-phishing

#### Segnalazione rapida
Il **tempismo è vitale** per affrontare il phishing. Segnalare una mail permette di:
- Avvisare i tecnici informatici, che potranno mettere quella mail (e il server da cui è stata inviata) in una blacklist, salvando così gli atrli utenti.
- Correre ai ripari dopo la compromissione dell'account

#### Blacklist e Whitelist

#### Gestore delle password

#### Autenticazione a 2 fattori

#### Machine Learning
Machine Learning e Data Mining hanno algoritmi che studiano le mail, e quando una arriva riescono in pochi secondi a capire se questa è una mail di phishing o meno.

#### Computer Vision
Il computer vede la mail con gli *occhi di una persona*

## Esempi
- *Principe Nigeriano*
- **Romance**, messaggi volti a creare una relazione sentimentale con il destinatario
- **Corriere Amazon / FedEX**
- **Lotteria**
- **Rinnovo Password**
- **Spearphishing**= PHISHING MIRATO: phishing perfezionato per essere il più efficace possibile contro un determinato gruppo di individui, che condividono una o più caratteristiche.

### XSS (Cross Site Scripting) nelle mail
Possiamo prendere un url, copiarlo in una mail, e quando una vittima apre la mail viene rendirizzato alla pagina con il payload xss. È possibile quindi utilizzare come vettore di attacco la mail con i link XSS

### Malware
Qualsiasi tipologia di software malevolo, che può essere incorporato in una gande varietà di formati file anche apparentemente innocui

NB. Windows nasconde le estensione, questo rende più facile NON accorgersi del virus

### Ransomware
Uno dei suoi principali vettori è la mail

### Office Macro
Sono delle funzionalità di Office tramite le quali è possibile scrivere della macro. 
Le **macro possono eseguire codice**, sono quindi molto pericolose.

### URL Contraffatti

### URL Shortners
Su internet ci sono servizi per abbreviare gli URL e renderli più comodi da utilizzare.
Tuttavia, questo maschera il loro vero contenuto, senza possibilità di verifica preventiva.

### URL Padding
Su dispositivi con schermi ridotti è molto più facile far "sforare" il nome dell'indirizzo web oltra la barra degli indirizzi del browser.

<br>
<br>
<br>

##### Punti chiave per difendersi?
1. Non cedere all'istinto ("call to action")
2. Controllare la legittimità del dominio del mittente
3. Controllare la legittimità dei link esterni
4. Nel dubbio, contattare il personale IT



##### Alcuni tool utili:
- Gophish
- USecure