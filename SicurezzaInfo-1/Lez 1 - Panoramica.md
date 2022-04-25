# Concetti di Security
### Computer security
È l'insieme di misure e controli che garantiscono **confidenzialità**, **integrità** e **disponibilità** delle risorse dei sistemi informativi, che siano essi Hardware, Software o le informazioni stesse.

*Nello specifico:*
- **Confidenzialità**: informazioni (o sistemi) confidenziali rimangono tali, quindi NON accessibili a soggetti non autorizzati
- **Integrity**: le informazioni e i programmi sono modificati solo con metodi autorizzati. L'integrità dei sistemi invece si riferisce allo scopo di un determinato sistema, garantendo che esso possa eseguire solo le azioni per cui è stato programmato.
- **Availability**: garantisce che i sistemi siano disponibili, che funzionino e che il servizio che offrono non sia negato agli utenti autorizzati

### Alcune terminologie
**ASSET**: risorse in generale, che possono essere:
- Hardware: computer, server, modem, firewall
- Software: sistemi operativi, applicazioni, tool
- Dati: file, database (**dove vado a salvare le informazioni**)
- Rete: reti LAN e WAN

**Altri termini:**
- **Attacco**: **qualsiasi azione rivolta a collezionare, distruggere o degradare** i sistemi informativi o l'informazione stessa
- **Security Policy**: **criteri di sicurezza** che hanno lo scopo di mantenere un determinato livello di sicurezza
- **Minacce**: qualsiasi **circostanza o evento che può impattare negativamente** su un sistema informativo o un'informazione
- **Vulnerabilità**: **vulnerabilità** in un sistema, processo, policy o implementazione che **può essere sfruttata per un attacco**

**Attacchi e provenienza:**
- **Attacco attivo**: tentativo di **alterare le risorse di sistema o l'operatività del sistema** stesso
- **Attacco passivo**: tentativo di **utilizzare le informazioni** di un sistema **senza alterarne le risorse**
- **Attacco interno**: è un **attacco iniziato all'interno del perimetro**, l'attaccante (insider) ha accesso autorizzato alle risorse e/o alle informazioni
- **Attacco esterno**: proviene dall'esterno, l'attaccante non ha accesso autorizzato ai sistemi e lo ottiene illegalmente

**NB**. Le minacce incrementano il rischio che si pone sull'asset.

# Minacce, Attacchi e Asset
#### Definizioni:
- **Minaccia**: la minaccia si concretizza nel momento in cui un sistema elabora informazioni che hanno un valore per un soggetto (attaccante)
- **Attacco**: quando si ha una minaccia ed un attaccante riesce a sfruttare una vulnerabilità, si arriva all'attacco che è quella fase necessaria per ottenere accesso o informazioni dagli asset
- **Asset**: risorse importanti per il proprietario

# Requisiti funzionali
Sono i **requisiti necessari per permettere ai sistemi di eseguire le operazioni** per i quali sono stati programmati.

### Requisiti di sistema
-   **Access Control**: permette l'accesso solo agli autorizzati
-   **Awareness and Training**: spiegare al personale i rischi associati alla sicurezza
-   **Audit and Accountability**: tracciare e monitorare le azioni degli utenti per permettere analisi in caso di attacco (i cosidetti LOG), il tracciamento è necessario anche per rispondere alle leggi
-   **Certificaitions, Accreditations and Security Assessments**: Es. ISO 27-2001, effettuare deli assessment periodici sui sistemi e sulle reti per garantire i **criteri minimi di sicurezza**
-   **Configuration Management**: riguarda la gestione delle configurazioni, avere una **baseline** minima di sicurezza, mantenere un inventario delle configurazioni dei vari applicativi
-   **Contingency Planning**: stabilire dei piani in caso di emergenza, se mi attaccano e non ho un piano, non si agisce correttamente
-   **Identification and Authentication**: serve per identificare gli utenti che hanno accesso ad un sistema, in molti sistemi è essenziale che l'utenza sia nominale
-   **Incident Response**: stabilire un quadro operativo per le azioni in risposta all'emergenza: preparazione personale, detection del problema, piani di recovery post-incidente
-   **Maintence**: manutenzione ordinaria e straordinaria sui sistemi
-   **Media protection**: proteggere i media (documenti, foto,...) sia digitali che cartacei. Limitare l'accesso ai solo utenti autorizzati.










