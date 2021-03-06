---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-20"

---

# Ordine di istanze Cloud Foundation

Per distribuire una piattaforma SDDC (Software-Defined Data Center) unificata con una configurazione di calcolo, archiviazione e rete standard, ordina un'istanza VMware Cloud Foundation. Durante l'ordine iniziale, puoi anche aggiungere servizi, come [Zerto on {{site.data.keyword.cloud}}](../services/addingzertodr.html) per il ripristino di emergenza.

## Requisiti

Assicurati di aver completato le seguenti attività:
*  Hai configurato le credenziali dell'infrastruttura {{site.data.keyword.cloud_notm}} nella pagina **Impostazioni**. Per ulteriori informazioni, vedi [Gestione di account utente e impostazioni](../vmonic/useraccount.html).
*  Hai esaminato i requisiti e le considerazioni in [Requisiti e pianificazione per le istanze Cloud Foundation](sd_planning.html).

**Importante:** non modificare alcun valore impostato durante l'ordine e la distribuzione dell'istanza. Ciò potrebbe comportare l'inutilizzabilità dell'istanza. Inoltre, non modificare il nome dell'istanza, il nome del dominio root, l'etichetta del dominio secondario o il prefisso del nome host, dopo che l'istanza è stata distribuita.

## Impostazioni di sistema

Quando ordini un'istanza Cloud Foundation, devi specificare le seguenti impostazioni di sistema.

### Nome istanza

Il nome dell'istanza deve rispettare i seguenti requisiti:
* Sono consentiti solo caratteri alfanumerici e trattini (-).
* Il nome dell'istanza deve iniziare e terminare con un carattere alfanumerico.
* La lunghezza massima del nome dell'istanza è di 10 caratteri.
* Il nome dell'istanza deve essere univoco all'interno del tuo account.

### Primaria o secondaria

Scegli se ordinare un nuova istanza primaria o un'istanza secondaria per un'istanza primaria esistente.

## Impostazioni di licenza

Specifica le opzioni di licenza per i seguenti componenti VMware nell'istanza:  
* Licenza vCenter Server - Standard
* Licenza vSphere - Enterprise Plus
* Licenza NSX - Enterprise
* Licenza vSAN: seleziona l'edizione Advanced o Enterprise

Per gli utenti Business Partner, la licenza vCenter Server (Standard edition), la licenza vSphere (Enterprise Plus edition), la licenza NSX e la licenza vSAN sono incluse e acquistate per tuo conto. Tuttavia, devi specificare l'edizione per la licenza vSAN.

Per gli utenti non Business Partner, puoi utilizzare le licenze VMware fornite da IBM per questi componenti selezionando **Includi con l'acquisto** o puoi utilizzare l'opzione Bring Your Own License (BYOL) selezionando **Fornita dall'utente** e immettendo le tue chiavi di licenza.

## Impostazioni di Bare Metal Server

### Ubicazione data center

Seleziona il {{site.data.keyword.CloudDataCent_notm}} in cui deve essere ospitata l'istanza.

### Preconfigurato

Se selezioni **Preconfigurato**, non puoi modificare le impostazioni di CPU o RAM.

In base ai tuoi requisiti, seleziona una configurazione di Bare Metal Server:
  * Small (Dual Intel Xeon E5-2650 v4 / 24 core totali, 2,2 GHz / 128 GB di RAM / 12 unità)
  * Large (Dual Intel Xeon E5-2690 v4 / 28 core totali, 2,6 GHz / 512 GB di RAM / 12 unità)

### Personalizzato

Se selezioni **Personalizzato**, puoi scegliere la combinazione di CPU e RAM in base alle tue esigenze.

Seleziona il modello di CPU e la RAM per il Bare Metal Server.

Tabella 1. Opzioni per i {{site.data.keyword.baremetal_short}} personalizzati

| Opzioni CPU        | Opzioni RAM       |
|:------------- |:------------- |
| Dual Intel Xeon E5-2620 v4 / 16 core totali, 2,1 GHz | 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Dual Intel Xeon E5-2650 v4 / 24 core totali, 2,2 GHz | 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Dual Intel Xeon E5-2690 v4 / 28 core totali, 2,6 GHz | 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Processore Dual Intel Xeon Silver 4110 / 16 core totali, 2,1 GHz | 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |
| Processore Dual Intel Xeon Gold 5120 / 28 core totali, 2,2 GHz | 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |
| Processore Dual Intel Xeon Gold 6140 / 36 core totali, 2,3 GHz | 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |

### Numero di server Bare Metal

Un'istanza Cloud Foundation comprende quattro server bare metal nella distribuzione iniziale. Non puoi modificare il numero di server bare metal quando effettui l'ordine.

## Impostazioni di archiviazione

Le istanze Cloud Foundation supportano solo l'archiviazione vSAN.
* Se selezioni la configurazione **Preconfigurato** di Bare Metal Server, le impostazioni di archiviazione sono standardizzate e non possono essere modificate:
  * Per la configurazione **Small** di Bare Metal Server, vengono ordinate 2 unità disco SED SSD da 1,9 TB.
  * Per la configurazione **Large** di Bare Metal Server, vengono ordinate 4 unità disco SED SSD da 3,8 TB.
* Se selezioni la configurazione **Personalizzato** di Bare Metal Server, puoi personalizzare l'archiviazione vSAN VMware per la tua istanza specificando le seguenti impostazioni in **Storage vSAN**:
  * **Tipo e dimensioni del disco per i dischi vSAN**: seleziona la capacità che soddisfa le tue esigenze di archiviazione condivisa.
  * **Numero di dischi vSAN**: specifica il numero di dischi per l'archiviazione condivisa vSAN che vuoi aggiungere. Le quantità dei dischi devono essere 2, 4, 6 o 8.

## Impostazioni dell'interfaccia di rete

Quando ordini un'istanza Cloud Foundation, devi specificare le seguenti impostazioni dell'interfaccia di rete.

### Prefisso nome host

Il prefisso del nome host deve rispettare i seguenti requisiti:
*  Sono consentiti solo caratteri alfanumerici e trattini (-).
*  Il prefisso del nome host deve iniziare e terminare con un carattere alfanumerico.
*  La lunghezza massima del prefisso del nome host è di 10 caratteri.

### Etichetta dominio secondario

L'etichetta del dominio secondario deve rispettare i seguenti requisiti:
*  Sono consentiti solo caratteri alfanumerici e trattini (-).
*  L'etichetta del dominio secondario deve iniziare e terminare con un carattere alfanumerico.
*  La lunghezza massima dell'etichetta del dominio secondario è di 10 caratteri.
*  L'etichetta del dominio secondario deve essere univoca all'interno del tuo account.

### Nome dominio

Il nome del dominio root deve rispettare i seguenti requisiti:
* Il nome del dominio deve essere composto da due o più stringhe separate da un punto (.)
* La prima stringa deve iniziare con un carattere alfabetico e terminare con un carattere alfanumerico.
* Tutte le stringhe, tranne l'ultima, possono contenere solo caratteri alfanumerici e trattini (-).
* L'ultima stringa può contenere solo caratteri alfabetici.
* La lunghezza dell'ultima stringa deve essere compresa tra 2 e 24 caratteri.

**Nota:** la lunghezza massima del nome di dominio completo (o FQDN, Fully Qualified Domain Name) per gli host e le VM (macchine virtuali) è di 50 caratteri. I nomi di dominio devono essere adattati a questa lunghezza massima.

### Formato del valore per le impostazioni di rete

Il nome del dominio e l'etichetta del dominio secondario vengono utilizzati per generare il nome utente e i nomi server dell'istanza, come mostrato nella seguente tabella.

Tabella 2. Formato del valore per i nomi utente, nomi dominio e nomi server

| Nome        | Formato del valore      |
  |:------------- |:------------- |
  | Nome dominio | `<root_domain>` |  
  | Nome completo server ESXi | `<host_prefix><n>.<subdomain_label>.<root_domain>`, dove `<n>` è la sequenza del server ESXi. La lunghezza massima è di 50 caratteri. |   
  | Nome utente di accesso vCenter Server | `<user_id>@<root_domain>` (utente di Microsoft Active Directory) o `administrator@vsphere.local` |
  | Dome di dominio completo vCenter Server | `vcenter-1.<subdomain_label>.<root_domain>`. La lunghezza massima è di 50 caratteri. |  
  | Dome di dominio completo SDDC Manager | `sddcmanager.<subdomain_label>.<root_domain>`. La lunghezza massima è di 50 caratteri. |
  | Nome del sito SSO (Single Sign-On) | `<subdomain_label>`
  | Nome di dominio completo PSC | `PSC-<subdomain_label>.<subdomain_label>.<root_domain>`. La lunghezza massima è di 50 caratteri. |  

  Il nome di dominio completo di SDDC Manager non può essere risolto pubblicamente. In caso contrario, la configurazione dell'istanza Cloud Foundation potrebbe non riuscire e non può essere ripristinata. Prima di specificare un nome di dominio, consulta [Considerazioni sulla scelta del nome del dominio root](../vmonic/trbl_limitations.html#considerations-when-choosing-a-root-domain-name-for-cloud-foundation-instances).

### VLAN

Le impostazioni di rete si basano sulla tua selezione di **Ordina nuove VLAN** o **Seleziona VLAN esistenti**.

Per l'ordine della tua istanza sono richieste una VLAN pubblica e due VLAN private. Le due VLAN private sono collegate a ogni Bare Metal Server.

**Ordina nuove VLAN**  
Seleziona questa opzione per ordinare una nuova VLAN pubblica e due nuove VLAN private.

**Seleziona VLAN esistenti**  
A seconda del {{site.data.keyword.CloudDataCent_notm}} che hai selezionato, potrebbero essere disponibili VLAN pubbliche e private esistenti.

Se scegli di riutilizzare VLAN pubbliche e private esistenti, specifica le VLAN e le sottoreti:
  * La **VLAN pubblica** serve per l'accesso alla rete pubblica.
  * La **VLAN privata** serve per la connettività tra i data center e i servizi in {{site.data.keyword.cloud_notm}}.
  * La **VLAN privata secondaria** serve per le funzioni di VMware come vSAN.
  * La **Sottorete primaria** è assegnata agli host fisici per l'accesso alla rete pubblica.
  * La **Sottorete primaria privata** è assegnata agli host fisici per il traffico di gestione.

**Importante:**
* Assicurati che la configurazione del firewall sulle VLAN selezionate non blocchi il traffico dei dati di gestione.
* Assicurati che tutte le VLAN selezionate si trovino nello stesso pod, poiché i server ESXi non possono essere forniti su VLAN con pod misti.

## Servizi

Quando ordini un'istanza Cloud Foundation, puoi anche ordinare servizi aggiuntivi. Per ulteriori informazioni sui servizi disponibili, vedi [Servizi per le istanze Cloud Foundation](sd_planning.html#services-for-cloud-foundation-instances).

## Riepilogo ordine

In base alla tua configurazione selezionata per l'istanza e i servizi aggiuntivi, il costo stimato viene generato e visualizzato immediatamente nel riquadro di destra. Fai clic su **Dettagli dei prezzi** nella parte inferiore del riquadro di destra per generare un documento PDF che fornisce i dettagli della stima.

## Procedura

1. Dal catalogo {{site.data.keyword.cloud_notm}}, fai clic su **VMware** nel riquadro di navigazione a sinistra e quindi su **Cloud Foundation** nella sezione **Data center virtuali**.
2. Nella pagina **VMware Cloud Foundation on IBM Cloud**, fai clic su **Crea**.
3. Nella pagina **Cloud Foundation**, immetti il nome dell'istanza.
4. Seleziona il tipo di istanza:
   * Fai clic su **Istanza primaria** per distribuire una singola istanza nell'ambiente o per distribuire la prima istanza in una topologia multisito.
   * Fai clic su **Istanza secondaria** per connettere l'istanza a un'istanza esistente (primaria) nell'ambiente per l'alta disponibilità e completa quindi la seguente procedura:
     1. Seleziona l'istanza primaria a cui desideri collegare l'istanza secondaria.
     2. Immetti la password di amministratore PSC per l'istanza primaria.
5. Completa le impostazioni di licenza per i componenti dell'istanza:
   *  Per utilizzare le licenze fornite da IBM, seleziona **Includi con l'acquisto**.
   *  Per utilizzare la tua propria licenza, seleziona **Fornita dall'utente** e immetti la chiave di licenza.  
6. Completa le impostazioni di Bare Metal Server:
   1. Seleziona il {{site.data.keyword.CloudDataCent_notm}} in cui ospitare l'istanza.
   2. Seleziona la configurazione di Bare Metal Server.
      * Se selezioni **Preconfigurato**, scegli una configurazione tra **Small** e **Large**.
      * Se selezioni **Personalizzato**, specifica il modello di CPU e la dimensione della RAM.
7. Completa le impostazioni di archiviazione:
   * Se hai selezionato **Preconfigurato** per la configurazione Bare Metal, nota che le impostazioni di archiviazione per le configurazioni **Small** e **Large** standardizzate di Bare Metal Server non possono essere modificate.
   * Se hai selezionato **Personalizzato** per la configurazione Bare Metal, specifica il **Tipo e dimensioni del disco per i dischi vSAN** e il **Numero di dischi vSAN**.
8. Completa le impostazioni dell'interfaccia di rete:
   1. Immetti il prefisso del nome host, l'etichetta del dominio secondario e il nome del dominio root. Per un'istanza secondaria, il nome di dominio viene compilato automaticamente.
   2. Seleziona le impostazioni della VLAN:
      * Se vuoi ordinare nuove VLAN pubbliche e private, fai clic su **Ordina nuove VLAN**.
      * Se vuoi riutilizzare le VLAN pubbliche e private esistenti quando sono disponibili, fai clic su **Seleziona VLAN esistenti** e specifica le VLAN e le sottoreti.

9. Seleziona i servizi aggiuntivi da distribuire nell'istanza facendo clic sulla scheda del servizio corrispondente. Se un servizio richiede la configurazione, completa le impostazioni specifiche del servizio e fai clic su **Aggiungi servizio** nella finestra di configurazione a comparsa. Per informazioni su come fornire le impostazioni per un servizio, vedi l'argomento relativo all'ordine del servizio corrispondente.

10. Nel riquadro **Riepilogo ordine**, verifica la configurazione dell'istanza prima di effettuare l'ordine.
    1. Esamina le impostazioni per l'istanza.
    2. Esamina il costo stimato dell'istanza. Fai clic su **Dettagli dei prezzi** per generare un riepilogo in formato PDF. Per salvare o stampare il riepilogo
   del tuo ordine, fai clic sull'icona **Stampa** o **Download** nella parte superiore destra della finestra PDF.
    3. Assicurati che l'account da addebitare sia corretto e seleziona quindi la casella di spunta **Accetto che all'account riportato di seguito venga addebitato un corrispettivo**.
    4. Fai clic sul link o sui link dei termini che si applicano al tuo ordine. Assicurati di accettare questi termini e quindi seleziona la casella di spunta **Ho letto e accetto gli accordi di servizio di terze parti elencati di seguito**.
    5. Fai clic su **Fornitura**.

## Risultati

La distribuzione dell'istanza inizia automaticamente. Riceverai la conferma che l'ordine è in fase di elaborazione e puoi controllare lo stato della distribuzione visualizzando i dettagli dell'istanza.

Una volta che l'istanza è stata distribuita correttamente, i componenti descritti in [Specifiche tecniche per le istanze Cloud Foundation](../sddc/sd_cloudfoundationoverview.html#technical-specifications-for-cloud-foundation-instances) vengono installati sulla tua piattaforma virtuale VMware. I server ESXi che hai ordinato vengono raggruppati come **SDDC-Cluster** per impostazione predefinita. Se hai ordinato servizi aggiuntivi, la distribuzione dei servizi inizia dopo che l'ordine è stato completato.

Quando l'istanza è pronta per l'uso, lo stato dell'istanza viene modificato in **Pronto per l'utilizzo** e riceverai una notifica via e-mail.

Se ordini un'istanza secondaria, il client web VMware vSphere per l'istanza primaria (collegata a quella secondaria) potrebbe essere riavviato una volta completato l'ordine della tua istanza secondaria.

## Operazioni successive

Visualizza e gestisci l'istanza Cloud Foundation che hai ordinato.

**Importante**: devi gestire i componenti {{site.data.keyword.vmwaresolutions_short}} creati nel tuo account {{site.data.keyword.cloud_notm}} solo attraverso la console {{site.data.keyword.vmwaresolutions_short}}, non il {{site.data.keyword.slportal}} o qualsiasi altro mezzo all'esterno della console. Se modifichi questi componenti al di fuori della console {{site.data.keyword.vmwaresolutions_short}}, le modifiche non saranno sincronizzate con la console.

**ATTENZIONE**: la gestione di un qualsiasi componente {{site.data.keyword.vmwaresolutions_short}} (installato nel tuo account {{site.data.keyword.cloud_notm}} nel momento in cui hai ordinato l'istanza) dall'esterno della console {{site.data.keyword.vmwaresolutions_short}} può rendere instabile il tuo ambiente. Queste attività di gestione includono:

*  Aggiunta, modifica, restituzione o rimozione dei componenti
*  Espansione o contrazione della capacità dell'istanza mediante l'aggiunta o la rimozione di server ESXi
*  Spegnimento dei componenti
*  Riavvio dei servizi

   Le eccezioni a queste attività includono la gestione delle condivisioni file di archiviazione condivisa dal {{site.data.keyword.slportal}}. Tali attività includono: l'ordine, l'eliminazione (che potrebbe influire sugli archivi di dati, se montati), l'autorizzazione e il montaggio di condivisioni file di archiviazione condivisa.

### Link correlati

* [Registrazione di un account {{site.data.keyword.cloud_notm}}](../vmonic/signing_softlayer_account.html)
* [Visualizzazione delle istanze Cloud Foundation](sd_viewinginstances.html)
* [Aggiunta, visualizzazione ed eliminazione di cluster per le istanze Cloud Foundation](sd_addingviewingclusters.html)
* [Espansione e contrazione della capacità per le istanze Cloud Foundation](sd_addingremovingservers.html)
* [Ordine, visualizzazione e rimozione dei servizi per le istanze Cloud Foundation](sd_addingremovingservices.html)
* [Eliminazione di istanze Cloud Foundation](sd_deletinginstance.html)
* [Domande frequenti su BYOL](../vmonic/faq_byol.html)
