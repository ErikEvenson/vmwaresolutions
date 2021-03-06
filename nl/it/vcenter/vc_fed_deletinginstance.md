---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-19"

---

# Eliminazione di istanze VMware Federal

Per rilasciare i componenti che hai ordinato in un'istanza VMware Federal, elimina l'istanza.

Quando elimini un'istanza VMware Federal, i seguenti componenti vengono rilasciati in modo sequenziale:

1. Tariffe per supporto e servizio
2. Licenze del prodotto VMware
3. Server ESXi
4. Sottoreti

A causa delle dipendenze delle risorse, i componenti della tua istanza non vengono rilasciati immediatamente quando elimini l'istanza. Ad esempio, le sottoreti non possono essere eliminate finché i server ESXi non vengono completamente recuperati dall'infrastruttura {{site.data.keyword.cloud}}, cosa che avviene alla fine del ciclo di fatturazione dell'infrastruttura {{site.data.keyword.cloud_notm}}. Alla fine del ciclo di fatturazione dell'infrastruttura {{site.data.keyword.cloud_notm}}, che in genere è di 30 giorni, le sottoreti vengono eliminate e l'eliminazione dell'istanza viene completata.

**Attenzione:** per l'istanza eliminata ti vengono addebitati costi fino alla fine del ciclo di fatturazione dell'infrastruttura {{site.data.keyword.cloud_notm}}.

## Eliminazione di istanze dalla pagina delle istanze distribuite

1. Dalla console {{site.data.keyword.vmwaresolutions_short}}, fai clic su **Istanze distribuite** nel riquadro di navigazione a sinistra.
2. Nella tabella **Istanze vCenter Server**, trova l'istanza da eliminare.
3. Nella colonna **Azioni**, fai clic sull'icona Elimina.
   Lo stato dell'istanza viene modificato in **In fase di eliminazione**. Una volta che l'istanza è stata eliminata, i suoi componenti vengono rilasciati e il suo stato viene modificato in **Eliminato**.
4. Se vuoi rimuovere il record dell'istanza dalla console {{site.data.keyword.vmwaresolutions_short}}, completa la seguente procedura:
   1. Nella colonna **Azioni**, fai di nuovo clic sull'icona Elimina.
   2. Nella finestra **Elimina istanza**, fai clic su **OK**.

## Eliminazione di istanze dalla pagina dei dettagli dell'istanza

1. Dalla console {{site.data.keyword.vmwaresolutions_short}}, fai clic su **Istanze distribuite** nel riquadro di navigazione a sinistra.
2. Nella tabella **Istanze vCenter Server**, fai clic sull'istanza da eliminare.
3. Fai clic sull'icona del menu di overflow a destra di **Console vCenter** e quindi su **Elimina istanza**.
   Lo stato dell'istanza viene modificato in **In fase di eliminazione**. Una volta che l'istanza è stata eliminata, i suoi componenti vengono rilasciati e il suo stato viene modificato in **Eliminato**.
4. Se vuoi rimuovere il record dell'istanza dalla console {{site.data.keyword.vmwaresolutions_short}}, completa la seguente procedura:
   1. Fai di nuovo clic sull'icona del menu di overflow a destra di **Console vCenter** e quindi su **Elimina istanza**.
   2. Nella finestra **Elimina istanza**, fai clic su **OK**.

### Link correlati

* [Panoramica di VMware Federal on {{site.data.keyword.cloud_notm}}](vc_fed_overview.html)
* [Ordine di istanze VMware Federal](vc_fed_orderinginstance.html)
* [Protezione di istanze VMware Federal](vc_fed_securinginstance.html)
* [Visualizzazione delle istanze VMware Federal](vc_fed_viewinginstance.html)
* [Come contattare il supporto IBM](../vmonic/trbl_support.html)
