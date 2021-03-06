---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-27"

---

# Gestion des paramètres et comptes utilisateur

{{site.data.keyword.vmwaresolutions_full}} communique avec l'infrastructure {{site.data.keyword.cloud_notm}} via des appels {{site.data.keyword.slapi_short}}. Pour accéder en toute sécurité à {{site.data.keyword.slapi_short}}, vous devez associer les données d'identification de votre compte d'infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer) à votre compte {{site.data.keyword.cloud_notm}}.

**Remarque** : auparavant, le compte d'infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer) s'appelait compte IBM SoftLayer.

Vous pouvez également indiquer si vous voulez recevoir des notifications par courrier électronique et par console concernant divers événements.

## Avant de commencer

* Vous ne pouvez lier qu'un seul compte d'infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer) à un compte utilisateur {{site.data.keyword.cloud_notm}}. 
* Le compte d'infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer) que vous utilisez doit répondre à certaines exigences. Pour plus d'informations, voir [Exigences liées au compte d'infrastructure {{site.data.keyword.cloud_notm}}](slaccountrequirement.html).
* Si la clé d'API de votre compte d'infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer) change, vous devez mettre à jour la clé sur la page **Paramètres** de la console {{site.data.keyword.vmwaresolutions_short}}.

   **Important** : il vous incombe de vérifier que la clé d'API enregistrée sur la page **Paramètres** est correcte et à jour.
   Sinon, les opérations qui nécessitent la clé d'API risquent d'échouer.

## Procédure

1. Dans la console {{site.data.keyword.vmwaresolutions_short}}, cliquez sur **Paramètres** dans le panneau de navigation de gauche.
2. Dans la zone **Notifications**, spécifiez vos paramètres de notification. 
   * Si vous voulez être prévenu par courrier électronique de la survenue d'événements, cliquez sur **Activer les notifications par courrier électronique**.
   * Si vous voulez être prévenu sur la console de la survenue d'événements, cliquez sur **Activer les notifications par console**.
3. Dans la zone **Données d'identification d'infrastructure IBM Cloud**, entrez le nom d'utilisateur et la clé d'API de votre compte d'infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer) en utilisant l'une des méthodes décrites ci-dessous : 
   * Si votre compte d'infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer) et votre compte {{site.data.keyword.cloud_notm}} sont liés, cliquez sur **Extraire** pour activer la saisie automatique des données d'identification. 
   * Si votre compte d'infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer) et votre compte {{site.data.keyword.cloud_notm}} ne sont pas liés, connectez-vous au [portail client d'infrastructure {{site.data.keyword.cloud_notm}}](https://control.softlayer.com/) et suivez les instructions de la console pour obtenir et saisir les données d'identification. 
   * Si vous ne disposez d'aucun compte d'infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer), [inscrivez-vous pour en recevoir un](../vmonic/signing_softlayer_account.html) et suivez les instructions de la console pour obtenir et saisir les données d'identification. 
4. Cliquez sur **Sauvegarder les données d'identification**.

## Résultats

Une fois que le compte {{site.data.keyword.cloud_notm}} et le compte d'infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer) sont liés, la console extrait automatiquement les données d'identification du compte d'infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer) pour communiquer avec votre environnement VMware sur {{site.data.keyword.cloud_notm}}.

Les données d'identification stockées pour le compte d'infrastructure {{site.data.keyword.cloud_notm}} (SoftLayer) sont utilisées dans les opérations ultérieures qui nécessitent une interaction avec l'infrastructure {{site.data.keyword.cloud_notm}}. 

Si les notifications par courrier électronique ou sur la console pour certains événements d'instance, vous recevez des messages par courrier électronique ou sur la console lorsque ces événements se produisent.

### Liens connexes

* [Foire aux questions](faq.html)
* [Commande d'instances Cloud Foundation](../sddc/sd_orderinginstance.html)
* [Commande d'instances vCenter Server](../vcenter/vc_orderinginstance.html)
* [Notifications](notifications.html)
* [API SoftLayer](../../../customer-portal/cpapi.html){:new_window}
