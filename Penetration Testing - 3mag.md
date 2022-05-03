# Pentesting
## Introduzione e basi di hacking
Una vulnerabilità spesso è presente a causa di un errore di progettazione o programmazione. Spesso si punta più a far funzionare un programma che a farlo funzionare in sicurezza.

È importante avere una **metodologia di lavoro precisa**, invece di "andare a tentoni"

Cybersecurity si occupa di proteggere **reti**, **dispositivi**, **programmi**, **dati**. NB. È possibile fare penetration test su **qualsiasi cosa connessa alla rete**.

**Information Security** è legata alla sicurezza delle informazioni e non del dato in se.
*Es. 20031971 è un dato qualsiasi, se invece lo interpreto come 20/03/1971 ho una informazione*.

### Triade CIA
**Triade CIA**, dobbiamo riuscire a garantire:
- **Confidenzialità**, informazione accessibile a chi ne ha l'autorizzazione
- **Integrità**, informazione modificabile solo da chi ha l'autorizzazione
- **Disponibilità**, capacità di un sistema/applicazione web di fornire un informazione in seguito ad una richiesta (un attacco Ddos mira alla disponibilità di un servizio)

### Cosa vogliamo proteggere?
- IoT
- Rete
- Software
- Persone
- Hardware
- Privacy
- **Informazioni**

Le informazioni possono essere **DIGITALI** o **CARTACEI** e possono essere **comuni, personali o particolari**

### Standard di qualità
ISO 9126 e ISO 25010 definiscono **come si scrive codice di QUALITÀ e SICURO** poichè vengono rispettati dei paradigmi ferrei.

**NB**. *Zero Day* è una vulnerabilità non ancora nota per cui non esiste una patch.

### Ethical Hacking
Gli **hacker etici** (o *white hat*) sono delle figure esperte in sicurezza informatica reclutati con lo scopo di *testare* la capacità di un sistema informatico ad attacchi provenienti dal mondo reale.

NB. **ETICO** --> È presente un accordo scritto tra hacker e obiettivo

**Obiettivi hacking etico:**
- Trovare tutte le debolezze
- Valutare dei rischi che nascono dai punti deboli trovati e **prioritizzare i rischi**
- Risoluzione delle problematiche
- Rafforzamento delle misure di sicurezza (eventualmente valutando l'adozione di framework orientati alla sicurezza)
- Sensibilizzazione

L'hacker etico si concentra su falle e carenze presenti nell'**ideazione**, **progettazione** e **implementazione** dell'infrastruttura digitale dell'azienda.

**Codici maligni funzionanti** (sequenze di comando o interi programmi di piccole dimensioni) prendono il nome di **exploit**.

**NB**. Il linguaggio più utilizzato nel mondo del penetration test è Python.

Alcune considerazione sugli ethical hacking:
- Massima trasparenza e integrità
- Attenzione in caso di contesti sensibili, quando facciamo penetration test **NON ci è tutto permesso**
- Sempre necessario un accordo scritto
- Pianificare e dettagliare tutte le operazioni oggetto dell'accordo
- Garantire la trasparenza, ogni passaggio fatto deve essere documentato (software, versione software,...)
- I report prodotti possono contenere anche dei consigli operativi (es. implementazione di un **honeypot**)
- Estrema attenzione a non trascurare alcuna debolezza che potrebbero essere sfruttate

**NB**. **Honeypot** un dispositivo/area/... protetta dove sono presenti delle informazioni inventate che fanno da **esca per l'attaccante**.

### Grey Hat
Questi hacker si trovano sulla linea di confine tra *buono* e *cattivo*, tra *legale* e *illegale*. Sono identificabili in quelle figure che **in modo non autorizzato**, cercano vulnerabilità all'interno di sistemi per aiutare il legittimo proprietario.

**NB**. È difficile identificare un hacker etico da uno malevolo

### 2 tipologie di Pentesting
1. di **infrastrutture IT** (reti, server, computer, wifi)
2. di **servizi di rete** (applicazioni web, portali gestione clienti, sistemi per monitoraggio di server)

Solitamente gli EH devono anche:
- Fare scanning delle porte (nmap)
- ...

Esistono degli **standard internazionali per l'esecuzione dei penetration testing** come **OWASP** (solo per applicazioni WEB), **PTES, OSSTMM** (soprattutto per infrastruttura di rete).

### Penetration Test
**Attacco informatico controllato ad un sistema** che non viene fatto con l'intenzione di delinquere ed è commissionato dall'azienda proprietaria del sistema.

Normalmente un attacco pentest viene richiesto con una clausola **red-team** per cui nessuno all'interno dell'azienda sa come e quando avverrà l'attacco (nemmeno il reparto di Cybersecurity)

Settori della cybersecurity:
- **Red-team** si occupa di attacchi informatici (OFFENSIVA)
- **Yellow-team** si occupa della sicurezza dell'azienda (firewall, computer,...)
- **Blue-team** si occupa di **rispondere agli attacchi informatici** (DIFESA)

**NB**. Penetration Test NON vuol dire Vulnerabilty Assessment

#### Alcuni tipologie di penetration testing:
1. **Web application penetration testing**, si concentra su applicazioni web, framework, API, moduli
2. **Mobile application penetration testing**
3. **External application penetration testing**
4. **Internal application penetration testing**, tentativo di ottenere i privilegi di amministratore di sistema completi all'interno della rete interna
5. **Wireless application penetration testing**, violare la crittografia WEP o WPA
6. **IoT penetration testing**, qualsiasi cosa ha un IP può essere soggetta ad attacchi

- **Whitebox penetration test**: l'attaccante ha tutte le informazioni che gli servono (indirizzi IP, architettura di rete)
- **Blackbox penetration test**: l'attaccante non sa nulla riguardo l'infrastruttura di rete, dispositivi,...
- **Greybox penetration test**: una via di mezzo tra le 2. Quelli più comuni

**NB**. È consigliato utilizzare **firewall di marchi e modelli diversi**

#### Vulnerability Assessment VS Penetration Test
Fase in cui si **identificano le vulnerabilità presenti all'interno di un sistema**, applicazione web,... . Segue poi la fase di **penetration test** che invece **mostra se la vulnerabilità può essere sfruttata o meno**.

Il **Vulnerability Assessment da un punteggio ad ogni vulnerabilità trovata**.

Spesso i penetration test sono necessari nel caso l'azienda voglia o sia certificata, es. ISO 27001 o GDPR

#### Alcuni strumenti di penetration testing:
- Port Scan
- Scanner vulnerabilità
- Scanner per applicazioni
- Proxy di valutazione delle applicazioni WEB

Nei vari ambiti:
- Penetration Test **WEB**: OWASP ZAP, Nmap, Dirbuster
- Penetration Test **Cloud**: Astra, Pacu, Prowler
- Penetration Test **Rete**: wireshark, nmap
- Penetration Test **Mobile**: MobeSF, Astra Security Scan, Cydia
- Penetration Test **Blockchain**: BitcoinJ, Truffle

### Fasi del Penetration Test
1. Pianificare il penetration test (mi è concesso tutto?, quali IP?)
2. **Information gathering**, con tool come **Maltego** o **Recon-ng**
3. **Analisi delle vulnerabilità**, con tool come OpenVAS, nmap (con delle specifiche opzioni)
4. **Exploitation**
5. **Post-Exploitation**, una volta entrato nel sistema raccolto alcune informazioni per dimostrare di essere entrato
	1. **Privilege escalation**, con tool come **meterpreter**
	2. **Disabilitazione firewall** (come dimostrazione NON esecuzione)
	3. **Mantenimento dell'accesso**
6. **Reporting e Analyze**, dove vengono specificati tutti i passaggi eseguiti per entrare nel sistema
7. **Pulizia**, lasciare il sistema come lo si è trovato all'entrata, quindi rimozioni di script, riportare i privilegi come in origine

--> NON bisogna mai eseguire comandi che **danneggino la macchina host**

**NB**. Se un blackhat cancella completamente i file di log **risulterebbe troppo sospetto**. In più è possibile risalire all'identità dell'attaccante tramite **analisi dei REGISTRI DI SISTEMA**.

<br>
<br>

## VA e Tools
Una vulnerabilità è un qualsiasi punto che può essere sfruttato per entrare nel sistema, ed è importante la **valutazione di una vulnerabilità**

Gli **strumenti di scansione delle vulnerabilità** possono:
- Analizzare il codice
- Trovare rootkit, backdoor e trojan
- ...

*Alcuni tool di esempio:*
- **Nikto**, È uno degli strumenti più utilizzati ed è molto **legato ai server**.
- **Netsparker**, simile a Nikto ma impiega molto tempo poichè fa un'analisi molto approfondita
- **OpenVAS**, è uno dei migliori strumenti di scansione, è possibile utilizzarlo non solo in applicazioni web ma anche nei database, nell'OS, nelle reti e nelle maccine virtuali