## Descrizione Progetto
Questo progetto implementa un'architettura Zero Trust (ZTA) in ambiente industriale 4.0, integrando Digital Twin, Next-Generation Firewall (NGFW) e Multi-access Edge Computing (MEC). L'architettura è progettata per garantire un accesso sicuro e controllato ai sistemi industriali, utilizzando un approccio "never trust, always verify".

## Struttura del Progetto
- **nodo-edge**: Contiene le applicazioni dei digital twin
  - Interfacce per i macchinari DMG e SISMA
  - Controller per l'acquisizione dati in tempo reale
  - Moduli di elaborazione dei dati locali
  
- **nodo-private/Aggregated_DT**: Webapp principale per l'industria 4.0
  - Dashboard per la visualizzazione e il monitoraggio dei dati
  - Sistema di sicurezza basato su ZTA
  - Gestione dinamica del firewall OPNsense

## Aggregated_DT: Componente Nodo-Private

### Descrizione
Aggregated_DT è un'applicazione di visualizzazione che raccoglie dati dai macchinari industriali, calcola i tempi di accesso ai server e configura dinamicamente il firewall utilizzando l'API OPNsense. L'applicazione implementa principi di Zero Trust Architecture per garantire che l'accesso ai dati e alle configurazioni avvenga in modo sicuro e temporaneo.

### Funzionalità Principali
- **Raccolta Dati**: Acquisizione dati da endpoint DMG e SISMA
- **Calcolo Tempi di Accesso**: Calcolo e registrazione dei tempi di accesso ai server
- **Configurazione Dinamica del Firewall**: Interazione con l'API OPNsense per configurare regole firewall
- **Visualizzazione Dati**: Interfaccia web per la visualizzazione dei dati raccolti
- **Sicurezza ZTA**: Implementazione di accesso temporaneo e just-in-time alle risorse

### Componenti ZTA Implementati
- **Accesso Temporaneo**: Le porte di rete vengono aperte solo per il tempo necessario alle operazioni
- **Gestione Automatica del Firewall**: Apertura e chiusura sincronizzata delle regole firewall
- **Monitoraggio in Tempo Reale**: Dashboard per verificare lo stato degli accessi
- **Context Manager**: Utilizzo di `with` statement in Python per garantire la chiusura delle porte

### Struttura File
- **app.py**: File principale dell'applicazione che avvia il server web e i script di raccolta dati
- **secure_access_manager.py**: Modulo per la gestione degli accessi sicuri secondo il paradigma ZTA
- **dt_data_manager.py**: Interfaccia per l'accesso sicuro ai dati dei Digital Twin
- **ADT_sisma.py**: Script per la raccolta e l'elaborazione dei dati dai macchinari SISMA
- **ADT_DMG.py**: Script per la raccolta e l'elaborazione dei dati dai macchinari DMG
- **filter_rule_OPN.py**: Modulo per interagire con l'API OPNsense per configurare le regole firewall
- **traffic_manager.py**: Gestione e analisi del traffico di rete
- **static**: Directory contenente file statici (CSS, JavaScript)
- **templates**: Directory contenente template HTML
  - **access_status.html**: Visualizzazione dello stato degli accessi ZTA
  - **firewall_dashboard.html**: Pannello per la gestione del firewall
  - **traffic.html**: Monitoraggio del traffico di rete
  - **index.html**: Dashboard principale
- **test_sisma**: Directory contenente dati di test per SISMA
- **test_dmg**: Directory contenente dati di test per DMG

## Principi di ZTA Implementati

### 1. Verifica ed Autorizzazione Esplicita
Ogni richiesta viene autenticata e autorizzata indipendentemente dalla rete di origine. L'implementazione utilizza:
- Autenticazione multi-fattore attraverso il sistema di login
- Verifica dell'identità per ogni operazione di accesso ai dati o configurazione

### 2. Accesso con Privilegio Minimo
Gli utenti hanno accesso solo alle risorse necessarie per svolgere il loro lavoro, per il tempo minimo necessario:
- Apertura temporanea delle porte firewall solo durante le operazioni necessarie
- Chiusura automatica dopo il completamento delle operazioni
- Gestione granulare dei permessi basata sui ruoli utente

### 3. Monitoraggio Continuo
Tutte le attività vengono monitorate e registrate per rilevare comportamenti anomali:
- Dashboard in tempo reale dello stato degli accessi
- Logging completo di tutte le operazioni con timestamp
- Sistema di notifica per accessi non autorizzati o sospetti

## Installazione e Configurazione

### Requisiti
- Python 3.8+
- Flask
- Connessione di rete ai Digital Twin industriali
- Accesso all'API OPNsense per la configurazione del firewall

### Installazione
1. **Clonare il repository**:
   ```sh
   git clone https://github.com/gianmarcodirenzo-99/Implementazione-ZTA-Industria_4.0.git
   cd Implementazione-ZTA-Industria4.0/nodo-private/Aggregated_DT
