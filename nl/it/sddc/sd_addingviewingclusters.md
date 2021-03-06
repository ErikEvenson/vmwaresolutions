---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-19"

---

# Aggiunta, visualizzazione ed eliminazione di cluster per le istanze Cloud Foundation

I server ESXi che hai configurato quando hai ordinato un'istanza sono raggruppati in un cluster predefinito. Il nome del cluster predefinito è:
* Per le istanze distribuite nelle release della V2.1 o successive: **MGMT-Cluster-`<subdomain_label>`**
* Per le istanze distribuite nelle release della V2.0 o precedenti: **SDDC-Cluster**

Puoi aggiungere i tuoi propri cluster alle istanze VMware Cloud Foundation per espandere la capacità di calcolo e archiviazione. All'interno di un cluster, puoi gestire i server ESXi per una migliore allocazione delle risorse e alta disponibilità. Quando non sono più necessari, puoi eliminare i cluster aggiunti dalle tue istanze.

**Disponibilità**:
* La funzione di aggiunta cluster è disponibile solo per le istanze che sono state distribuite o aggiornate alle release della V2.0 e successive.
* La funzione di eliminazione cluster è disponibile solo per le istanze che sono state distribuite o aggiornate alle release della V2.3 e successive.  

## Aggiunta di cluster alle istanze Cloud Foundation

A un'istanza Cloud Foundation puoi aggiungere fino a cinque cluster.

### Impostazioni di sistema

Quando aggiungi un cluster a un'istanza Cloud Foundation, devi specificare le seguenti impostazioni.

#### Nome cluster

Il nome del cluster deve rispettare i seguenti requisiti:
* Sono consentiti solo caratteri alfanumerici e trattini (-).
* Il nome del cluster deve iniziare e terminare con un carattere alfanumerico.
* La lunghezza massima del nome del cluster è di 30 caratteri.
* Il nome del cluster deve essere univoco all'interno dell'istanza Cloud Foundation.

#### Ubicazione data center

L'ubicazione del {{site.data.keyword.CloudDataCent}} del cluster è impostata sul {{site.data.keyword.CloudDataCent_notm}} dell'istanza Cloud Foundation per impostazione predefinita. Puoi distribuire il cluster in un {{site.data.keyword.CloudDataCent_notm}} diverso rispetto a quello dell'istanza distribuita, ma devi assicurarti che la latenza di rete tra i due {{site.data.keyword.CloudDataCents_notm}} sia inferiore a 150 ms. Per controllare la latenza di rete, puoi utilizzare uno strumento come [SoftLayer IP Backbone Looking Glass](http://lg.softlayer.com/){:new_window}.

I data center disponibili dipendono dalla configurazione Bare Metal Server selezionata per la distribuzione. Se selezioni la configurazione **Personalizzato**, puoi anche distribuire il cluster a un pod dell'infrastruttura {{site.data.keyword.cloud}} diverso, nel caso in cui il data center selezionato contenga ulteriori pod. Ciò è utile quando il pod dell'infrastruttura {{site.data.keyword.cloud_notm}} predefinito in cui è distribuita l'istanza iniziale ha raggiunto la sua capacità massima.

**Nota:** le configurazioni standardizzate **Small** e **Large** di Bare Metal Server utilizzano un pod predefinito che non può essere modificato.

Se distribuisci il cluster in un diverso data center o pod, vengono ordinate tre VLAN aggiuntive da utilizzare con i {{site.data.keyword.baremetal_short}} ordinati.

### Impostazioni di Bare Metal Server

Puoi scegliere **Personalizzato** o **Preconfigurato**.

#### Personalizzato

Per l'impostazione **Personalizzato**, hai una serie di opzioni per il **Modello CPU** e la **RAM**. Le opzioni disponibili potrebbero variare in base alla versione in cui è stata inizialmente distribuita la tua istanza.

Tabella 1. Opzioni per i {{site.data.keyword.baremetal_short}} personalizzati

| Opzioni CPU   | Opzioni RAM   |
|:------------- |:------------- |
| Dual Intel Xeon E5-2620 v4 / 16 core totali, 2,1 GHz | 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Dual Intel Xeon E5-2650 v4 / 24 core totali, 2,2 GHz | 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Dual Intel Xeon E5-2690 v4 / 28 core totali, 2,6 GHz | 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Processore Dual Intel Xeon Silver 4110 / 16 core totali, 2,1 GHz | 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |
| Processore Dual Intel Xeon Gold 5120 / 28 core totali, 2,2 GHz | 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |
| Processore Dual Intel Xeon Gold 6140 / 36 core totali, 2,3 GHz | 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |

#### Preconfigurato

Per l'impostazione **Preconfigurato**, puoi scegliere una **Configurazione Bare Metal Server** in base ai tuoi requisiti:
* Small (Dual Intel Xeon E5-2650 v4 / 24 core totali, 2,2 GHz / 128 GB di RAM / 12 dischi)
* Large (Dual Intel Xeon E5-2690 v4 / 28 core totali, 2,6 GHz / 512 GB di RAM / 12 dischi)

### Impostazioni di archiviazione vSAN

Per le configurazioni **Preconfigurato** di Bare Metal Server, non puoi modificare le impostazioni dell'archiviazione vSAN:
* Per la configurazione **Small**, vengono ordinate due unità disco SED SSD da 1,9 TB.
* Per la configurazione **Large**, vengono ordinate quattro unità disco SED SSD da 3,8 TB.

Per la configurazione **Personalizzato** di Bare Metal Server, puoi personalizzare l'archiviazione vSAN specificando il numero di dischi vSAN il tipo e la dimensione del disco che soddisfano le tue esigenze di archiviazione.

### Impostazioni di licenza

Puoi specificare le opzioni di licenza per i componenti VMware nel cluster, inclusi VMware vSphere e VMware vSAN:
* Per gli utenti Business Partner, la licenza vSphere (Enterprise Plus edition) e la licenza vSAN sono incluse e acquistate per tuo conto. Tuttavia, devi specificare l'edizione per la licenza vSAN.
* Per gli utenti non Business Partner, per i componenti puoi utilizzare le licenze VMware fornite da IBM selezionando **Includi con l'acquisto** o puoi utilizzare l'opzione Bring Your Own License (BYOL) selezionando **Fornita dall'utente** e immettendo le tue chiavi di licenza.

## Procedura per aggiungere i cluster alle istanze Cloud Foundation

1. Dalla console {{site.data.keyword.vmwaresolutions_short}}, fai clic su **Istanze distribuite** nel riquadro di navigazione a sinistra.
2. Nella tabella **Istanze Cloud Foundation**, fai clic sull'istanza a cui vuoi aggiungere i cluster.

   **Nota:** assicurati che l'istanza sia nello stato **Pronto per l'utilizzo**. In caso contrario, non potrai aggiungere i cluster all'istanza.

3. Fai clic su **Infrastruttura** nel riquadro di navigazione a sinistra e quindi su **Aggiungi** nell'angolo superiore destro della tabella **CLUSTER**.
4. Nella pagina **Aggiungi cluster**, immetti il nome del cluster.
5. Se vuoi ospitare il cluster in un {{site.data.keyword.CloudDataCent_notm}} diverso da quello in cui è ospitata l'istanza, in **Bare Metal Server**, seleziona la casella di spunta **Seleziona un'ubicazione differente** e scegli il {{site.data.keyword.CloudDataCent_notm}} per ospitare l'istanza.
6. Completa la configurazione Bare Metal:
   * Se hai selezionato **Personalizzato**, seleziona il **Modello CPU** e la dimensione della **RAM**.
   * Se hai selezionato **Preconfigurato**, seleziona la **Configurazione Bare Metal Server**.
7. Completa la configurazione di archiviazione:
   * Se hai selezionato **Personalizzato** per la configurazione Bare Metal, specifica il **Numero di dischi vSAN** e **Tipo e dimensioni del disco per i dischi vSAN**.
   * Se hai selezionato **Preconfigurato** per la configurazione Bare Metal, nota che le impostazioni di archiviazione per le configurazioni **Small** e **Large** di Bare Metal Server non possono essere modificate.
8. Specifica come vengono fornite le tue chiavi di licenza:
   * Per gli utenti Business Partner, la licenza vSphere (Enterprise Plus edition) e la licenza vSAN sono incluse e acquistate per tuo conto. Tuttavia, devi specificare l'edizione per la licenza vSAN.
   * Per gli utenti non Business Partner, puoi selezionare una delle seguenti opzioni:
       * Se vuoi acquistare nuove licenze per tuo conto, seleziona **Includi con l'acquisto** per i componenti. Per VMware vSAN, seleziona anche l'edizione della licenza.
       * Se vuoi utilizzare la tua propria licenza VMware per un componente, seleziona **Fornita dall'utente** e immetti la chiave di licenza per il componente.
9. Nel riquadro **Riepilogo ordine**, verifica la configurazione del cluster prima di aggiungerlo.
   1. Esamina le impostazioni per il cluster.
   2. Esamina il costo stimato del cluster. Fai clic su **Dettagli dei prezzi** per generare un riepilogo in formato PDF. Per salvare o stampare il riepilogo del tuo ordine, fai clic sull'icona **Stampa** o **Download** nella parte superiore destra della finestra PDF.
   3. Fai clic sul link o sui link dei termini che si applicano al tuo ordine e conferma di accettare questi termini prima di aggiungere il cluster.
   4. Fai clic su **Fornitura**.

### Risultati dopo l'aggiunta dei cluster alle istanze Cloud Foundation

1. La distribuzione del cluster viene avviata automaticamente e lo stato del cluster viene modificato in **Inizializzazione**. Puoi controllare lo stato della distribuzione visualizzando la cronologia di distribuzione nella pagina di riepilogo dell'istanza.
2. Quando il cluster è pronto per l'uso, il suo stato viene modificato in **Pronto per l'utilizzo**. Il cluster appena aggiunto viene abilitato con vSphere High Availability (HA) e vSphere Distributed Resource Scheduler (DRS).

**Importante**: non puoi modificare il nome del cluster. La modifica del nome del cluster potrebbe comportare errori nelle operazioni di aggiunta o rimozione dei server ESXi nel cluster.

## Visualizzazione dei cluster nelle istanze Cloud Foundation

1. Dalla console {{site.data.keyword.vmwaresolutions_short}}, fai clic su **Istanze distribuite** nel riquadro di navigazione a sinistra.
2. Nella tabella **Istanze Cloud Foundation**, fai clic su un'istanza per visualizzare i cluster al suo interno.
3. Fai clic su **Infrastruttura** nel riquadro di navigazione a sinistra. Nella tabella **CLUSTER**, visualizza il riepilogo dei cluster:
   * **Nome**: il nome del cluster.
   * **Server ESXi**: il numero di server ESXi nel cluster.
   * **CPU**: la specifica CPU dei server ESXi nel cluster.
   * **Dischi vSAN personalizzati**: il numero di dischi vSAN nel cluster, incluso il tipo di disco e la capacità.
   * **Memoria**: la dimensione totale della memoria dei server ESXi nel cluster.
   * **Ubicazione Data Center**: il data center in cui è ospitato il cluster.
   * **Pod**: il pod in cui è distribuito il cluster.
   * **Stato**: lo stato del cluster. Lo stato può assumere uno dei seguenti valori:
   <dl class="dl">
       <dt class="dt dlterm">Inizializzazione</dt>
       <dd class="dd">Il cluster è in fase di creazione e configurazione.</dd>
       <dt class="dt dlterm">In fase di modifica</dt>
       <dd class="dd">Il cluster è in fase di modifica.</dd>
       <dt class="dt dlterm">Pronto per l'utilizzo</dt>
       <dd class="dd">Il cluster è pronto per l'uso.</dd>
       <dt class="dt dlterm">In fase di eliminazione</dt>
       <dd class="dd">Il cluster è in fase di eliminazione.</dd>
       <dt class="dt dlterm">Eliminato</dt>
       <dd class="dd">Il cluster è stato eliminato.</dd>
   </dl>
   * **Azioni**: fai clic sull'icona **Elimina** per eliminare il cluster.
4. Fai clic sul nome di un cluster per visualizzare l'elenco di server ESXi e le relative informazioni:

   * **Nome**: il nome del server ESXi è nel formato `<host_prefix><n>.<subdomain_label>.<root_domain>`, dove:

      `host_prefix` è il prefisso del nome host,
      `n` è la sequenza del server ESXi,
      `subdomain_label` è l'etichetta del dominio secondario e
      `root_domain` è il nome del dominio root.

   * **Versione**: la versione del server ESXi.
   * **Credenziali**: il nome utente e la password per accedere al server ESXi.
   * **IP privato**: l'indirizzo IP privato del server ESXi.
   * **Stato**: lo stato del server ESXi, che può assumere uno dei seguenti valori:
        <dl class="dl">
        <dt class="dt dlterm">Aggiunto</dt>
        <dd class="dd">Il server ESXi è stato aggiunto ed è pronto per l'uso. </dd>
        <dt class="dt dlterm">In fase di aggiunta</dt>
        <dd class="dd">Il server ESXi è in fase di aggiunta. </dd>
        <dt class="dt dlterm">In fase di eliminazione</dt>
        <dd class="dd">Il server ESXi è in fase di eliminazione.</dd>
        </dl>
   * I dettagli della licenza vSAN e della licenza vSphere. I dettagli della licenza vSphere sono disponibili solo se hai scelto di utilizzare la tua propria licenza VMware (BYOL) durante l'ordine del cluster:
       * **Tipo di licenza**: la licenza vSAN o la licenza vSphere.
       * **Tipo di ordine**: la licenza è fornita dall'utente (BYOL) o acquistata per conto dell'utente.
       * **Edizione licenza**: l'edizione della licenza.
       * **Chiave di licenza**: la chiave di licenza.
       * **Capacità totale (CPU)**: la capacità totale o il numero di CPU fornite dalla licenza.
       * **Capacità libera (CPU)**: la capacità attualmente disponibile nella licenza.

## Eliminazione di cluster dalle istanze Cloud Foundation

Potresti voler eliminare un cluster da un'istanza quando non è più necessario.

### Prima di eliminare

* Utilizza questa procedura per eliminare i cluster dalle istanze distribuite nelle release della V2.3 o successive.
* Per i cluster distribuiti nelle istanze della V2.2 o precedenti, devi aggiornare l'istanza alla V2.3 per poter eliminare i cluster che hai aggiunto all'istanza.
* Puoi eliminare un singolo cluster alla volta. Per eliminare più cluster, devi farlo in sequenza: attendere che il cluster precedente venga eliminato prima di tentare di eliminare quello successivo.
* Assicurati che tutti i nodi in un cluster siano accesi e operativi prima di eliminare il cluster.
* Quando elimini un cluster, verranno eliminate anche tutte le VM (macchine virtuali) dal cluster e non potranno essere ripristinate. Se vuoi mantenere le VM, migrale in altri cluster.
* Non è possibile eliminare il cluster predefinito.

## Procedura per eliminare i cluster dalle istanze Cloud Foundation

1. Dalla console {{site.data.keyword.vmwaresolutions_short}}, fai clic su **Istanze distribuite** nel riquadro di navigazione a sinistra.
2. Nella tabella **Istanze Cloud Foundation**, fai clic sull'istanza da cui vuoi eliminare i cluster.

   **Nota**: assicurati che l'istanza sia nello stato **Pronto per l'utilizzo**. Altrimenti, non potrai eliminare i cluster dall'istanza.

3. Fai clic su **Infrastruttura** nel riquadro di navigazione a sinistra. Nella tabella **CLUSTER**, individua il cluster che vuoi eliminare e fai clic sull'icona **Elimina**.
4. Conferma di aver completato la migrazione delle VM in altri cluster, se appropriato, e di voler eliminare il cluster.

### Link correlati

* [Visualizzazione delle istanze Cloud Foundation](sd_viewinginstances.html)
* [Espansione e contrazione della capacità per le istanze Cloud Foundation](sd_addingremovingservers.html)
