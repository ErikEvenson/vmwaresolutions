---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-20"

---

# Ordine di istanze vCenter Server

Per distribuire una piattaforma virtualizzata VMware flessibile e personalizzabile che soddisfi al meglio le tue esigenze del carico di lavoro, ordina un'istanza VMware vCenter Server. Durante l'ordine iniziale, puoi anche aggiungere servizi, come [Zerto on {{site.data.keyword.cloud}}](../services/addingzertodr.html) per il ripristino di emergenza.

## Requisiti

Assicurati di aver completato le seguenti attività:
* Hai configurato le credenziali dell'infrastruttura {{site.data.keyword.cloud_notm}} nella pagina **Impostazioni**. Per ulteriori informazioni, vedi [Gestione di account utente e impostazioni](../vmonic/useraccount.html).
* Hai esaminato le informazioni in [Requisiti e pianificazione per le istanze vCenter Server](vc_planning.html).
* Hai esaminato il formato del nome di istanza e di dominio. Il nome del dominio e l'etichetta del dominio secondario vengono utilizzati per generare il nome utente e i nomi server dell'istanza.

Tabella 1. Formato del valore per i nomi di istanza e di dominio

| Nome        | Formato del valore      |
  |:------------- |:------------- |
  | Nome dominio | `<root_domain>` |  
  | Nome utente di accesso vCenter Server | `<user_id>@<root_domain>` (utente di Microsoft Active Directory) o `administrator@vsphere.local` |
  | Dome di dominio completo vCenter Server | `vcenter.<subdomain_label>.<root_domain>`. La lunghezza massima è di 50 caratteri. |
  | Nome del sito SSO (Single Sign-On) | `<subdomain_label>` |
  | Nome completo server ESXi | `<host_prefix><n>.<subdomain_label>.<root_domain>`, dove `<n>` è la sequenza del server ESXi. La lunghezza massima è di 50 caratteri. |  
  | Nome di dominio completo PSC | `psc-<subdomain_label>.<subdomain_label>.<root_domain>`. La lunghezza massima è di 50 caratteri. |

**Importante**: non modificare alcun valore che è stato impostato durante l'ordine e la distribuzione dell'istanza. Ciò potrebbe comportare l'inutilizzabilità dell'istanza. Ad esempio, la rete pubblica potrebbe arrestarsi, i server e le VSI (Virtual Server Instance) potrebbero spostarsi dietro Vyatta durante il provisioning o la VSI di IBM CloudBuilder potrebbe interrompersi o essere eliminata.

## Impostazioni di sistema

Quando ordini un'istanza vCenter Server, devi specificare le seguenti impostazioni di sistema.

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
* VMware vSphere Enterprise Plus 6.5u1
* VMware vCenter Server 6.5
* VMware NSX Service Providers Edition (Base, Advanced o Enterprise) 6.4

Per gli utenti Business Partner, la licenza vCenter Server (Standard edition), la licenza vSphere (Enterprise Plus edition) e la licenza NSX sono incluse e acquistate per tuo conto. Tuttavia, devi specificare l'edizione per la licenza NSX.

Per gli utenti non Business Partner, puoi utilizzare le licenze VMware fornite da IBM per questi componenti selezionando **Includi con l'acquisto** o puoi utilizzare l'opzione Bring Your Own License (BYOL) selezionando **Fornita dall'utente** e immettendo le tue chiavi di licenza.

**Attenzione**:
* È necessaria una licenza con un minimo di 8 CPU, ossia per 4 server con 2 CPU per ogni server. La scelta della licenza per ogni componente VMware si applica all'istanza di base e a qualsiasi server ESXi che aggiungi all'istanza in un secondo momento. Pertanto, devi assicurarti che la tua licenza supporti la futura espansione della capacità nella tua infrastruttura.
* Le edizioni minime della licenza sono indicate sull'interfaccia utente. Se sono supportate edizioni diverse per i componenti, puoi selezionare l'edizione che vuoi. Sei responsabile di garantire che la chiave di licenza fornita sia corretta per ogni componente VMware selezionato.
* Per vSphere, al momento dell'ordine verrà addebitato un costo di licenza, ma tale costo verrà successivamente accreditato sul tuo account.
* Puoi modificare le licenze fornite utilizzando il client web VMware vSphere al termine della distribuzione dell'istanza.
* Il supporto per i componenti VMware per i quali fornisci le licenze verrà offerto direttamente da VMware, non dal supporto IBM.

## Impostazioni di Bare Metal Server

Le impostazioni Bare Metal si basano sulla tua selezione del data center e sulla scelta di una configurazione preconfigurata o personalizzata.

### Ubicazione data center

Seleziona il {{site.data.keyword.CloudDataCent_notm}} in cui deve essere ospitata l'istanza.

### Preconfigurato

Se selezioni **Preconfigurato**, non puoi modificare le impostazioni di CPU o RAM.

In base ai tuoi requisiti, seleziona una configurazione di Bare Metal Server:
  * Small (Dual Intel Xeon E5-2620 v4 / 16 core totali, 2,1 GHz / 128 GB di RAM / 2 unità)
  * Medium (Dual Intel Xeon E5-2650 v4 / 24 core totali, 2,2 GHz / 256 GB di RAM / 2 unità)
  * Large (Dual Intel Xeon E5-2690 v4 / 28 core totali, 2,6 GHz / 512 GB di RAM / 2 unità)

### Personalizzato

Se selezioni **Personalizzato**, puoi scegliere la combinazione di CPU e RAM in base alle tue esigenze.

Seleziona il modello di CPU e la RAM per il Bare Metal Server.

Tabella 2. Opzioni per i {{site.data.keyword.baremetal_short}} personalizzati

| Opzioni CPU        | Opzioni RAM       |
|:------------- |:------------- |
| Dual Intel Xeon E5-2620 v4 / 16 core totali, 2,1 GHz | 64 GB, 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Dual Intel Xeon E5-2650 v4 / 24 core totali, 2,2 GHz | 64 GB, 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Dual Intel Xeon E5-2690 v4 / 28 core totali, 2,6 GHz | 64 GB, 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Processore Dual Intel Xeon Silver 4110 / 16 core totali, 2,1 GHz | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |
| Processore Dual Intel Xeon Gold 5120 / 28 core totali, 2,2 GHz | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |
| Processore Dual Intel Xeon Gold 6140 / 36 core totali, 2,3 GHz | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |

### Numero di server Bare Metal

Per il cluster iniziale nell'istanza, puoi configurare il numero di server ESXi nel seguente modo:
* Se hai selezionato **Preconfigurato**, puoi configurare il numero di server ESXi nell'intervallo 2 - 10.
* Se hai selezionato **Personalizzato**, puoi configurare il numero di server ESXi nell'intervallo 2 - 20.

Tutti i server ESXi condividono la stessa configurazione. Dopo la distribuzione iniziale, puoi aggiungere altri quattro cluster. Se hai selezionato la configurazione **Personalizzato** per vSAN, sono richiesti 4 server ESXi per i cluster iniziali e di post-distribuzione. Per ulteriori informazioni sul numero minimo di server ESXi, vedi [Un'istanza vCenter Server a due nodi è altamente disponibile?](../vmonic/faq.html#is-a-two-node-vcenter-server-instance-highly-available-).

## Impostazioni di archiviazione

Le impostazioni di archiviazione si basano sulla tua selezione della configurazione Bare Metal Server e sul tipo di archiviazione.

### Archiviazione vSAN

vSAN è disponibile solo se selezioni la configurazione Bare Metal **Personalizzato**. Specifica le seguenti opzioni vSAN:

* **Numero di dischi vSAN**: specifica il numero di dischi per l'archiviazione condivisa vSAN che vuoi aggiungere. Le quantità dei dischi devono essere 2, 4, 6 o 8.
* **Tipo e dimensioni del disco per i dischi vSAN**: seleziona la capacità che soddisfa le tue esigenze di archiviazione condivisa.
* **Licenza vSAN**: utilizza la licenza VMware fornita da IBM per il componente vSAN selezionando **Includi con l'acquisto** o utilizza l'opzione BYOL (Bring Your Own License) selezionando **Fornita dall'utente** e immettendo la tua chiave di licenza.

### Archiviazione NFS

Se selezioni **Storage NFS**, puoi aggiungere l'archiviazione condivisa a livello di file per la tua istanza in cui tutte le condivisioni utilizzano le stesse impostazioni o puoi specificare impostazioni di configurazione diverse per ogni condivisione file. Specifica le seguenti opzioni NFS:

**Nota:** il numero di condivisioni file deve essere compreso tra 1 e 32.

* **Configura le condivisioni singolarmente**: seleziona questa opzione per specificare diverse impostazioni di configurazione per ogni condivisione file.
* **Numero di condivisioni**: quando utilizzi la stessa impostazione di configurazione per ogni condivisione file, specifica il numero di condivisioni file per l'archiviazione condivisa NFS che vuoi aggiungere.
* **Dimensione**: seleziona la capacità che soddisfa le tue esigenze di archiviazione condivisa.
* **Prestazioni**: seleziona l'IOPS (Input/output Operations Per Second) per GB in base ai tuoi requisiti del carico di lavoro.
* **AGGIUNGI NFS**: seleziona questa opzione per aggiungere singole condivisioni file che utilizzano impostazioni di configurazione diverse.

Tabella 3. Opzioni del livello di prestazioni NFS

| Opzione        | Dettagli       |
  |:------------- |:------------- |
  | 2 IOPS/GB | Questa opzione è progettata per i carichi di lavoro più generici. Applicazioni di esempio includono: hosting di piccoli database, backup di applicazioni web o immagini disco di macchine virtuali per un hypervisor. |
  | 4 IOPS/GB | Questa opzione è progettata per i carichi di lavoro ad alta intensità che hanno un'alta percentuale di dati attivi alla volta. Applicazioni di esempio includono: database transazionali. |
  | 10 IOPS/GB | Questa opzione è progettata per i tipi di carichi di lavoro più impegnativi, come l'analisi. Applicazioni di esempio includono: database ad alte transazioni e altri database sensibili alle prestazioni. Questo livello di prestazioni è limitato a una capacità massima di 4 TB per condivisione file. |

## Impostazioni dell'interfaccia di rete

Quando ordini un'istanza vCenter Server, devi specificare le seguenti impostazioni dell'interfaccia di rete.

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

**Nota:** la lunghezza massima del nome di dominio completo (FQDN) per gli host e le VM (macchine virtuali) è di 50 caratteri. I nomi di dominio devono essere adattati a questa lunghezza massima.

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
* La **Sottorete privata primaria** è assegnata agli host fisici per il traffico di gestione.

**Importante:**
* Assicurati che la configurazione del firewall sulle VLAN selezionate non blocchi il traffico dei dati di gestione.
* Assicurati che tutte le VLAN selezionate si trovino nello stesso pod, poiché i server ESXi non possono essere forniti su VLAN con pod misti.

### Configurazione DNS

Seleziona la configurazione DNS (Domain Name System) per la tua istanza:

* **Singola VSI Windows pubblica per Active Directory/DNS**: viene distribuita una singola VSI di Microsoft Windows Server per Microsoft Active Directory (AD) consultabile, che funziona come DNS per l'istanza in cui sono registrati gli host e le VM. Questa opzione è stata distribuita per impostazione predefinita per le istanze della V1.9 e successive.
* **Due VM di Windows Server dedicate e altamente disponibili sul cluster di gestione**: vengono distribuite due VM di Microsoft Windows, che aiutano a migliorare la sicurezza e la solidità.

**Importante:** se configuri la tua istanza per utilizzare le due VM di Microsoft Windows, devi fornire due licenze Microsoft Windows Server 2012 R2. Utilizza la licenza Microsoft Windows Server 2012 R2 Standard Edition o la licenza Microsoft Windows Server 2012 R2 Datacenter Edition o entrambe.

Ogni licenza può essere assegnata solo a un singolo server fisico e copre fino a due processori fisici. Una licenza Standard Edition è in grado di eseguire due VM di Microsoft Windows virtualizzate per ogni server con 2 processori. Pertanto, sono necessarie due licenze poiché due VM di Microsoft Windows vengono distribuite in due host diversi.

Hai 30 giorni per attivare le VM.

Per ulteriori informazioni sulle licenze di Windows, vedi la [Documentazione di Windows Server 2012 R2](https://www.microsoft.com/en-us/licensing/product-licensing/windows-server-2012-r2.aspx#tab=2).

## Impostazioni dei servizi

Quando ordini un'istanza vCenter Server, puoi anche ordinare servizi aggiuntivi. Per ulteriori informazioni sui servizi, vedi [Servizi disponibili per le istanze vCenter Server](vc_addingremovingservices.html#available-services-for-vcenter-server-instances).

## Riepilogo ordine

In base alla configurazione che hai selezionato per l'istanza e i servizi aggiuntivi, il costo stimato viene generato e visualizzato immediatamente nella sezione **Riepilogo ordine** nel riquadro di destra. Fai clic su **Dettagli dei prezzi** nella parte inferiore del riquadro di destra per generare un documento PDF che fornisce i dettagli della stima.

## Procedura

1. Dal catalogo {{site.data.keyword.cloud_notm}}, fai clic su **VMware** nel riquadro di navigazione a sinistra e quindi su **vCenter Server** nella sezione **Data center virtuali**.
2. Nella pagina **VMware vCenter Server on IBM Cloud**, fai clic sulla scheda **vCenter Server** e quindi su **Crea**.
3. Nella pagina **vCenter Server**, immetti il nome dell'istanza.
4. Seleziona il tipo di istanza:
   * Fai clic su **Istanza primaria** per distribuire una singola istanza nell'ambiente o per distribuire la prima istanza in una topologia multisito.
   * Fai clic su **Istanza secondaria** per connettere l'istanza a un'istanza esistente (primaria) nell'ambiente per l'alta disponibilità e completa quindi la seguente procedura:
     1. Seleziona l'istanza primaria a cui desideri collegare l'istanza secondaria.
     2. Immetti la password di amministratore PSC per l'istanza primaria.
5. Completa le impostazioni di licenza per i componenti dell'istanza.  
   *  Per utilizzare le licenze fornite da IBM, seleziona **Includi con l'acquisto** e, se necessario, seleziona l'edizione della licenza.
   *  Per utilizzare la tua propria licenza, seleziona **Fornita dall'utente** e immetti la chiave di licenza.
6. Completa le impostazioni di Bare Metal Server.
    1. Seleziona il {{site.data.keyword.CloudDataCent_notm}} in cui ospitare l'istanza.
    2. Seleziona la configurazione di Bare Metal Server.
       * Se selezioni **Preconfigurato**, scegli **Small**, **Medium** o **Large** per la configurazione.
       * Se selezioni **Personalizzato**, specifica il modello di CPU e la dimensione della RAM.
    3. Specifica il numero di {{site.data.keyword.baremetal_short}}. Se intendi utilizzare vSAN come soluzione di archiviazione, ricorda che sono richiesti un minimo di 4 {{site.data.keyword.baremetal_short}}.  

7. Completa le impostazioni di archiviazione:
  * Se selezioni **Storage vSAN**, specifica il **Tipo e dimensioni del disco per i dischi vSAN**, il **Numero di dischi vSAN** e come la **Licenza vSAN** deve essere fornita.
  * Se selezioni **Storage NFS** e vuoi aggiungere e configurare le stesse impostazioni per tutte le condivisioni file, specifica il **Numero di condivisioni**, la **Dimensione** e le **Prestazioni**.
  * Se selezioni **Storage NFS** e vuoi aggiungere e configurare le condivisioni file singolarmente, seleziona **Configura condivisioni singolarmente**, fai clic sull'icona **+** accanto all'etichetta **Aggiungi NFS** e seleziona la **Dimensione** e le **Prestazioni** per ogni singola condivisione file. Devi selezionare almeno una condivisione file.

8. Completa le impostazioni dell'interfaccia di rete.
   1. Immetti il prefisso del nome host, l'etichetta del dominio secondario e il nome del dominio root. Per un'istanza secondaria, il nome di dominio viene compilato automaticamente.
   2. Seleziona le impostazioni della VLAN:
      * Se vuoi ordinare nuove VLAN pubbliche e private, fai clic su **Ordina nuove VLAN**.
      * Se vuoi riutilizzare le VLAN pubbliche e private esistenti quando sono disponibili, fai clic su **Seleziona VLAN esistenti** e specifica le VLAN e le sottoreti.
   3. Specifica la configurazione DNS.

9. Seleziona i servizi aggiuntivi da distribuire nell'istanza facendo clic sulla scheda del servizio corrispondente. Se un servizio richiede la configurazione, completa le impostazioni specifiche del servizio e fai clic su **Aggiungi servizio** sulla scheda.
Per informazioni su come fornire le impostazioni per un servizio, vedi l'argomento relativo all'ordine del servizio corrispondente.

10. Nel riquadro **Riepilogo ordine**, verifica la configurazione dell'istanza prima di effettuare l'ordine.
   1. Esamina le impostazioni per l'istanza.
   2. Esamina il costo stimato dell'istanza. Fai clic su **Dettagli dei prezzi** per generare un riepilogo in formato PDF. Per salvare o stampare il riepilogo del tuo ordine, fai clic sull'icona **Stampa** o **Download** nella parte superiore destra della finestra PDF.
   3. Fai clic sul link o sui link dei termini che si applicano al tuo ordine e conferma di accettare questi termini prima di ordinare l'istanza.
   4. Fai clic su **Fornitura**.

## Risultati

La distribuzione dell'istanza inizia automaticamente. Riceverai la conferma che l'ordine è in fase di elaborazione e puoi controllare lo stato della distribuzione visualizzando i dettagli dell'istanza.

Una volta che l'istanza è stata distribuita correttamente, i componenti descritti in [Specifiche tecniche per le istanze vCenter Server](vc_vcenterserveroverview.html#technical-specifications-for-vcenter-server-instances) vengono installati sulla tua piattaforma virtuale VMware. I server ESXi che hai ordinato vengono raggruppati come **cluster1** per impostazione predefinita. Se hai ordinato servizi aggiuntivi, la distribuzione dei servizi inizia dopo che l'ordine è stato completato.

Quando l'istanza è pronta per l'uso, lo stato dell'istanza viene modificato in **Pronto per l'utilizzo** e riceverai una notifica via e-mail.

Se ordini un'istanza secondaria, il client web VMware vSphere per l'istanza primaria (collegata a quella secondaria) potrebbe essere riavviato una volta completato l'ordine della tua istanza secondaria.

## Operazioni successive

Visualizza e gestisci l'istanza vCenter Server che hai ordinato.

**Importante**: devi gestire i componenti {{site.data.keyword.vmwaresolutions_short}} creati nel tuo account {{site.data.keyword.cloud_notm}} solo attraverso la console {{site.data.keyword.vmwaresolutions_short}}, non il {{site.data.keyword.slportal}} o qualsiasi altro mezzo all'esterno della console.
Se modifichi questi componenti al di fuori della console {{site.data.keyword.vmwaresolutions_short}}, le modifiche non saranno sincronizzate con la console.

**ATTENZIONE**: la gestione di un qualsiasi componente {{site.data.keyword.vmwaresolutions_short}} (installato nel tuo account {{site.data.keyword.cloud_notm}} nel momento in cui hai ordinato l'istanza) dall'esterno della console {{site.data.keyword.vmwaresolutions_short}} può rendere instabile il tuo ambiente. Queste attività di gestione includono:
*  Aggiunta, modifica, restituzione o rimozione dei componenti
*  Espansione o contrazione della capacità dell'istanza mediante l'aggiunta o la rimozione di server ESXi
*  Spegnimento dei componenti
*  Riavvio dei servizi

   Le eccezioni a queste attività includono la gestione delle condivisioni file di archiviazione condivisa dal {{site.data.keyword.slportal}}. Tali attività includono: l'ordine, l'eliminazione (che potrebbe influire sugli archivi di dati, se montati), l'autorizzazione e il montaggio di condivisioni file di archiviazione condivisa.

### Link correlati

* [Registrazione di un account {{site.data.keyword.cloud_notm}}](../vmonic/signing_softlayer_account.html)
* [Visualizzazione delle istanze vCenter Server](vc_viewinginstances.html)
* [Configurazione multisito per le istanze vCenter Server](vc_multisite.html)
* [Aggiunta, visualizzazione ed eliminazione di cluster per le istanze vCenter Server](vc_addingviewingclusters.html)
* [Espansione e contrazione della capacità per le istanze vCenter Server](vc_addingremovingservers.html)
* [Ordine, visualizzazione e rimozione dei servizi per le istanze vCenter Server](vc_addingremovingservices.html)
* [Eliminazione di istanze vCenter Server](vc_deletinginstance.html)
