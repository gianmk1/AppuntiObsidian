# Lezione 7-8 aprile
**Analisi statica**: cercare di capire se nel codice del software ci sono vulnerabilità o difetti, **senza eseguire il codice**.

NB. Ci sono strumenti che controllano **pattern nel codice**.

## Executive communication
**SICUREZZA DEL SOFTWARE** = sicurezza di un bene / asset

ISO25010, Qualità dei prodotto software: la sicurezza serve per proteggere dati e informazioni.

Le proprietà da conservare quanto si parla di sicurezza del software sono:
1. Confidenzialità
2. Disponibilità
3. Integrità
4. Non-repudation
5. Accountability

*L'obiettivo sarebbe quello di costruire un software (inteso anche l'infrastruttura cui è posto) sicuro al 100%. Questo è IMPOSSIBILE. Però dobbiamo preservare il più possibile che:*
- **Operazioni e funzionalità continuano normalmente** -> chi lo sta usando non se ne accorge 
-  **anche quando è soggetto ad attacchi** -> MITIGAZIONE del rischio

Compromettere un software potrebbe compromettere l'intero sistema.

### Alcuni attacchi:
##### EquiFax
Rubati dati personali di 145milioni di persone, tra cui data di nascita / codice fiscale / ...

- 2012: nella libreria Apache Struts (**libreria opensource**) è stato introdotto un bug
- 2015-16: altre versioni
- 2017: trovato il bug e sfruttato nell'attacco

##### TalkTalk
Attacco realizzato tramite una **SQL injection**, con un metodo vecchio di 20 anni.

##### eBay
Manomessa la pagina di pagamento, tramite **cross-site scripting** (simil sql injection), portava ad una pagina di un dominio fraudolento.

##### Ariane 5
Razzo durante il lancio, improvvisamente cambia direzione verso il suolo.

L'errore che ha causato questo incidente è stato un **overflow**, un dato veniva passato da un 64bit float a un 16bit float.

Questo errore è stato subito scoperto da un **analizzatore statico** chiamato **Polyspace**.

## Il Software è un ASSET
**ASSET** = risorsa, **bene**, qualcosa cosa io stabilisco avere valore
Un software è qualcosa che ha valore, è un bene:

Un asset può avere valore:
- Perchè **possiede** valore
- Perchè **produce** valore
- Perchè **da accesso** a qualcosa di valore

## Vulnerabilità
> Una **VULNERABILITÀ** è una **debolezza in un asset che** in qualche modo **rende suscettibile il mio asset/software** ad attacchi/fallimenti. 

>Una vulnerabilità è l'**operazione di sfruttamento di una debolezza**.

Un **ATTACCO** è un'**azione intenzionale** che vuole ridurre il valore di un asset.
Un **FALLIMENTO** sono **azioni non intenzionali** che possono ridurre il valore di un asset.

**Attacchi/fallimenti/errori** sono azioni che definite come **MINACCE** o **threats**, questa parola **non distingue se la minaccia è intenzionale o meno**

## CVE, Common Vulnerability and Exposures
**CVE** = definisce la vulnerabilità come una debolezza è può essere sia software che hardware. Se sfruttata può portare un impatto negativo a CIA (Confidentiality,...).

La **mitigazione** di queste vulnerabilità può comportare l'**intero software**, *non la singola linea di codice*. Devo valutare tutto il percorso a cui può portare quella vulnerabilità. Posso dover agire **anche a livello di progettazione/architettura**.

> **CVE è una raccolta di vulnerabilità REALI** (**storicità**), trovate in codice applicativo reale, cui vengono esposte assieme a: **codice identificativo**, data di "rilascio", descrizione della vulnerabilità (e come funziona)

https://nvd.nist.gov/ , viene gestito il db dell'NVD

*Es. id di una cve: CVE-2022-22946*

CVE è diventato uno standard per cercare di veicolare l'importanza di gestire degli attacchi. Permette di capire in che modo una determinata debolezza è stata sfruttata.

L'elenco CVE raccoglie vulnerabilità trovate sia che queste derivino da **codice opensource sia da codice proprietario**

**CVE-ID**: specifica la **vulnerabilità reale**
**CWE-ID**: specifica la **debolezza** che è stata sfruttata

## CWE, Common Weakness Enumeration , pt1
È un altro standard col quale si vuole cercare di costruire una base di conoscenza che **raccogliesse tutte le tipologie di DEBOLEZZE** (**NON vulnerabilità**) che un sistema/software può avere. NON sono legate solamente al codice ma anche per strutturali. Può essere intesa come un'**enciclopedia/dizionario di debolezze**.

*Es. la SQL injection è stata raccolta nel CWE*
*Es. NullDereference = CWE 476*

*Questo indice è stato realizzato poichè ogni software di analisi statica chiamava queste debolezze ognuno con un nome diverso. Con la CWE si evitano fraintendimenti, questo costituisce quindi un **linguaggio comune**.*

**MITRE-CORPORATION** è l'agenzia no-profit che si è occupata di realizzare questo dizionario.

Ogni debolezza è identificata da un **numero univoco** e da una **descrizione**.

CWE ha una **rappresentazione GERARCHICA** delle debolezze. **Una debolezza può farne a capo ad un'altra**, cioè essere di tipo più specifico di un'altra

**NB**. Nella descrizione di una CWE può esserci anche un richiamo alla CVE in cui è stata sfruttata.

**CAPEC**: spiegano quali sono le **tecniche principali di attacco per sfruttare la debolezza** in questione.

Struttura di una CWE:
1. **Descrizione debolezza**
2. Struttura gerarchica
3. Esempi
4. Elenco di CVE che sfruttano la debolezza (CWE) in questione
5. Riferimenti su come mitigare tale debolezza
6. CAPEC, altro standard che elenca delle tecniche di attacco

## CWE, pt2
Un altro modo per debolezza è **flaws**.

#### SDLC, Software Development Life Cycle
1. **Analisi requisiti** (= cosa deve fare il software)
2. **Progettazione/Disegno** (mi serve una componente che...)
3. **Sviluppo** (= scrittura del codice)
4. **Test**: posso trovare degli errori, quindi ritorno alla fase di analisi requisiti/progettazione ecc.
5. **Release**

In **qualsiasi momento** durante il ciclo di sviluppo del software è **possibile che venga inserita una vulnerabilità**:

- non ho analizzato correttamente i requisiti
- non ho progettato bene
- non ho scritto correttamente il codice
- non ho testato a sufficienza
- non ho deployato/mantenuto il software correttamente

#### Come possiamo cercare di prevenire una vulnerabilità?
*Devo garantire queste 3 proprietà*:
- **Confidenzialità**, l'informazione deve essere disponibile solo a chi ne ha effetto accesso. 
- **Integrità**, bisogna garantire che tutte le operazioni che un dato subisce siano sempre in grado di garantire la correttezza del dato che tratto
- **Disponibilità**, l'informazione è disponibile all'uso 

**NB**. Il grado di confidenzialità **non è un valore numerico**, ma un insieme di specifiche/caratteristiche

##### Le PATH injection - CWE 22
Spesso nei sistemi viene chiesto di inserire una stringa che rappresenta un path (= percorso).

In questo attacco **manipoliamo il percorso** da scrivere.

Es. path = C:/Users/nome_utente/Docs/../../../x.txt --> In questo modo io scrivo in C
<br>

# Compliance & Risk management

## Approaching Risk Management
Devo riusciare a portare l'idea del valore che una debolezza può compromettere -> il **rischio**. Che a sua volta si traduce in termini economici (e non solo)

***Come faccio a gestire il rischio?** Non posso gestire una tantum ma deve essere un processo continuo.*
**CICLO**:
1. **Identificare potenziali rischi**, devo già pensare quali sono i possibili rischi che corro disegnando il software in un determinato modo. 
2. **Analizzare il rischio**
3. **Valutare il rischio**
4. **Gestisco il rischio**, es. sanitizzazione, riscrittura codice, ...
5. **Monitor del rischio nel tempo**, devo continuare a monitorare il rischio nel tempo

Diverse tipologie di rischio:
- Strategico
- Di Compliance, quanto riesco ad aderire alle linee guida
- Di Mercato, es. reputazione del mercato
- Regolamentativo, leggi a cui devo sottostare
- Operazione, sistemistico

Ci sono **3 standard** che ci **aiutano a capire quali possono essere i rischi e a cosa devo quindi porre attenzione**.
Inoltre bisogna anche **dare una valutazione di un rischio**, per fare ciò mi aiuta il **CVSS**.

## CISQ
È un'**organizzazione internazionale con l'obiettivo di realizzare degli standard per la misura della QUALITÀ del software** e per lo sviluppo di software **sicuro**/affidabile/...

Si cerca di **definire quanto effort** (=fatica) **devo impiegare** per riuscire a portare il mio software da un certo grado di qualità/sicurezza ad uno che desidero.

**DEBITO TECNICO** è la **misura in giornate** (**FTE**) di tempo necessario per raggiungere un certo grado di qualità/sicurezza desiderata di un software. **Si traduce poi in termini economici.**

FTE = Full Time Employer

### CISQ - Standard
Alcuni progetti realizzati dalla CISQ:
- **Software sizing**: es. **LoC** = Lines of Code
- **Code quality**: questo progetto è diventato un ISO, poichè non esisteva uno prima. Le caratteristiche principale per la qualià del codice sono **sicurezza**, **performance**, **manutenzione**, **disponibilità**
- **Technical Debt**: es. DWE 19 - 10 giorni di technical debt

##### CISQ code quality
Per ogni caratteristica principale sono specificate delle **"good coding pratices"** e **"good architectural practies"**.

CISQ è l'unico standard che garantisce QUALITÀ + SICUREZZA

Per ogni controllo elencato (NON PRIORITIZZATO) da CISQ c'è un riferimento alla CWE corrispondente.
<br>

## OWASP, Open Web Application Security Project
*Alcuni progetti owasp:*
**CycloneDX** --> analizza il mio progetto e cerca tutte le libreria di terze parti utilizzate (**direttamente** o **indirettamente** (= **TRANSITIVE**)). In più **informa nel caso ci siano delle vulnerabilità sulla specifica libreria**, se ci sono **versioni aggiornate delle librerie**, ... --> **Lista che elenca i potenziali rischi** a cui devo portare attenzione

**Dependency-Track** --> va a prendere le liste delle dipendenze e cerca se ci sono vulnerabilià sulla libreria, questo è un **Software Compositioning Analysis**, cioè un **analizzatore statico**.

**SAMM**: progetto di linee guida per stabilire la ...

**OWASP Cheat Sheet**: linee guida di controlli da verificare per rispettare determinati standard

### Owasp vs CISQ
**Rispetto a CISQ, Owasp implenta un RANK** (= grado). In più rispetto al CVE vengono considerati anche i tentativi di attacco NON riusciti.

### Owasp Top10
> È una lista contenente le **debolezze più rischiose delle applicazioni web**, secondo Owasp. Questa classifica permette di capire dove si concentra maggiormente un hacker.

> Le debolezze vengono riportante in base al corrispondente rischio riportato in uno score

### Owasp Top10: Security Risk
*Come fa OWASP a valutare quanto un attacco è rischioso, e inserirlo di conseguenza nella graduatoria?*

Il **vettore di attacco** = **insieme di operazioni** che possono potenzialmente **compromettere l'applicazione**, colpiranno una debolezza piuttosto di un'altra. Un vettore d'attacco, ad esempio, può colpire 3 debolezze però sfruttarne solo 1. Per quest'ultima verifico se ci sono dei meccanismi di controllo e gli **impatti della vulnerabilità**

Ci possono essere diversi tipi di**Impatti**:
- **Tecnici**: tutto ciò che rappresenta qualcosa di valore
- **Business**: es. la banca è molto critiche, altre aree possono esserlo di meno

Più l'asset si avvicina al cliente finale e più avrà valore.
**Più la vulnerabilità si avvicina a qualcosa che ha valore (es. cliente) è più alto sarà il rischio.**

#### Owasp Top10: Risk assignment
![[inserire immagine slide]]

*Rosso è la parte piu grave*
**NB**. La parte di business in Owasp la da l'insieme dei partecipanti (aziende) che sono raccolti nella costruzione della top10.

Influiscono:
- facilità nel trovare la vulnerabilità...
- 
<br>

## A1: Broken Access Control
Al primo posto della Top10 2021. 
*Ogni categoria di vulnerabilità nell top10 owasp viene descritta con:*

- Descrizione
- Come prevenire questo rischio
- Esempio di scenario
- Lista delle CWE correlate
- Riferimenti  a strumenti che owasp o altri che propongono per risolvere/identificare/ecc. la vulnerabilità

NB. Le categorie di Owasp sono tradotte in un elenco di debolezze CWE.

## A3: Injection
Per injection si intende **qualsiasi modo in cui un informazione non fidata riesce a entrare nel mio sistema** e a corrompere un punto critico. **A seconda del punto critico colpito, avrò una determinata injection**.

Nella categoria injection Owasp infatti ci sono molti CWE, specifici per il punto critico che va a colpire l'injection.

## A6: Vulnerable and Outdated Components
*Tempo fa molto sottovalutato nelle aziende. Anche trovando delle vulnerabilità in una libreria: è da escludere il fatto che un team cerchi di risolvere "in casa" i problemi di una libreria. Eventuali aggiornamenti di questa comporterebbero, nuovamente, di dover modificare la libreria.*

*Alcune soluzioni:*
- Si può cercare di gestire in maniera diversa l'applicativo quando si integra con la libreria vulnerabile.
- Si può cercare di riscrivere alcuni pezzi del vecchio codice
- **Controllare tutte le interazioni tra le parti vecchie e quelle nuove**, in questo modo posso mitigare / **sanificare** il codice e ridurre il rischio di avere una qualsiasi delle vulnerabilità correlate.

Quando si parla di componenti vulnerabili e vecchie non è solo per la parte open ma anche per quella proprietaria interna.

<br>

## SANS25 Top 25 Software Errors
Il terzo standard per l'identificazione del rischio:

> Classifica degli errori/debolezzi più comuni o che hanno avuto più impatto

Queste 25 debolezze, secondo SANS25, sono le più rischiose poichè:
1. **facili da individuare e da sfruttare**, 
2. Possono permettere a chi riesce a violare il mio sistema di avere un forte controllo

Hanno anche dei **programmi formativi**, sia per consapevolezza che per pratica.

Ha origine dagli stessi organizzatori della CWE, qui c'è quindi un elenco preciso e definio di debolezze. **NON categorizza come fa OWASP**.

La mission di SANS non è solo fare una classifica ma anche rendere disponibili dei programmi di formazione.

Il rank della classificare viene assegnato tramite uno score.

**NB**. Il NULL Pointer NON gestito può comportare l'interruzione dell'esecuzione del software. Ci sono aziende molto sensibili a questo errore, es. automotive, medico

Si prende una debolezza e si guarda **quanti CVE hanno sfruttato la CWE**, si calcola la CVSS e la media di questi rappresenta lo score della top25.

## CVSS, Common Vulnerability Scoring System
Non serve per la identificazione del rischio ma per **analisi del rischio**. Di fatto è un **algoritmo**.

Utilizzato da SANS25 per costruire il proprio score. Viene **usato anche nei CVE**.
Fino a 4/5 anni fa questo standard era quasi sconosciuto.

> Questo standard si occupa di **misurare il grado di rischio** di una certa vulnerabilità

Curato da **FIRST**, si occupa di costruire algoritmi che calcolano la pericolosità di una vulnerabilità, e di convertirlo in un valore **numerico**. Questo standard è diventato uno **strument universale**.

*È comunque difficile stabilire a priori il grado di pericolosità di una vulnerabilità, poichè se sfruttata correttamente, potrebbe prendere dei dati più sensibili di altri, a seconda del sistema.*

### Metriche del CVSS
- Componente di BASE: stabilisce la **pericolosità TEORICA** di una debolezza
- Di **contesto**:
	- Temporale
	- Ambientale (dove è inserita l'applicazione)

Questi ultimi 2 fattori incrementano o diminuiscono il rischio teorico.

##### CVSS, Base Metric Group
Alcune metriche:
- Vettore di attacco
- Privilegi richiesti
- ...

In più quanto impatta sulla CIA, col base score si vuole rappresentare la difficoltà di sfruttare una debolezza.

##### CVSS, Fattore temporale
Stabilito che quella debolezza può essere sfruttata e attaccata, rappresenta **quanto quella vulnerabilità può mutare nel tempo**.

Se stabilisco che il mio codice è maturo, e sono sicuro la vulnerabilità rimarrà nel tempo, il **temporal metric aumenterà il base score**


##### CVS, Ambiente/Contesto
Stabilisce determinate misure che descrivono la presenza di controlli:
**quanto riesco a limitare il rischio di quella debolezza**.

Rappresenta le caratteristiche di una vulnerabilità che sono **rilevanti secondo un particolare ambiente/contesto**

Es. applicazione x avrà grado di rischio minore, poichè quando si interagisce con la potenziale vulnerabiltà in realtà sono già protetto
<br>

### Esempio di CVSS nell'NVD
Ci sono più versioni di CVSS.

**Il CVE riporta solo il BASE SCORE**, guardando poi alle altre metriche della CVSS andrò ad aumentare o diminuire quello score.

La stringa del CVSS nel NVD riporta anche le sigle  di tutte le metriche della **base metric group**.

https://www.first.org/cvss/calculator/3.1

### Considerazioni
Tutti gli standard visti hanno come obiettivo quello di fornire elementi specifici, **sta a noi poi riportare considerazioni e risultati appropriati all'ambiente** in cui stiamo lavorando (area di business, tipo applicazioni,...)

#### NIST National Vulnerability Dashboard
Fa capire nel mercato quanto sono gravi le vulnerabilità che sono state trovate.

#### CVE Statistic
Mostra le tipologie più frequenti/numerose dell vulnerabilità registrate nel CVE, posso capire come e chi sta sfruttando cosa.

<br>

## Collegamenti tra gli standard
1. Abbiamo debolezza nel nostro software, viene sfruttata e produce un CVE.
2. Il CVE lo registra nel database NVD, l'**NVD analizzando la vulnerabilità**, **assegna un CWE** corrispondente alla debolezza sfruttata
3. **NVD usa CVSS per dare uno score alla vulnerabilità** (e non alla specifica debolezza)

*Come fa l'NVD a capire la debolezza che è stata sfruttata?*
- Analizza
- Testing
- ...

Il proprietario del software come fa a capire che ha una debolezza del software, oltre a seguire le best practies dell OWASP, **posso usare strumenti degli AST**:

**AST (Application Security Testing)** -> tool statici o dinamici per verificare la debolezza del software, questi producono una **serie di errori con riferimento alla specifica CWE**.

*NB. Alcuni tipi di AST: SAST, DAST, MAST (Mobile), RAST, IAST.*
http://sonarcloud.io/


**NB**. Ovviamente questi test devono essere realizzati prima di rilasciare il software.

In base alle segnalazioni dei tool riportate (e ai CWE): **devo stabilire da dove voglio iniziare per sistemare il codice**, questo lo bisogna fare **PRIORITIZZANDO**.

Stabilito cosa voglio assicurarmi di controllare, comincio a stabilire che in ogni ciclo di sviluppo, andrò andare ad inserire degli specifici check.

**Non basta avere uno strumento che mi permette di trovare le POTENZIALI debolezze del software**, devo fare io successivamente un'analisi soggettiva.

![[inserire immagine ultima slide]]