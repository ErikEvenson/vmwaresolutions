---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-20"

---

# Commande, affichage et retrait de services pour des instances vCenter Server

Vous pouvez commander des services pour vos instances VMware vCenter Server, telle une solution de reprise après incident. Lorsque vous n'avez plus besoin de ces services, vous pouvez les supprimer de vos instances.

## Services disponibles pour les instances vCenter Server

Le tableau suivant présente les services disponibles sur les instances vCenter Server :

Tableau 1. Services disponibles pour les instances vCenter Server

| Nom de service | Disponibilité | Support d'instance |
|----------------------------------------------------------------------------------------|------------------|
| [F5 on {{site.data.keyword.cloud}}](../services/f5_considerations.html)                                 | Oui | A partir de V1.9 |
| [FortiGate Security Appliance on {{site.data.keyword.cloud_notm}}(../services/fortinetvm_considerations.html) | Oui | A partir de V2.0 |
| [HyTrust CloudControl on {{site.data.keyword.cloud_notm}}](../services/htcc_considerations.html)              | Oui | A partir de V2.3 |
| [HyTrust DataControl on {{site.data.keyword.cloud_notm}}](../services/htdc_considerations.html)              | Oui | A partir de V2.3 |
| [IBM Spectrum Protect&trade; Plus on {{site.data.keyword.cloud_notm}}](../services/spp_considerations.html)         | Oui | A partir de V2.2 |
| [KMIP for VMware on {{site.data.keyword.cloud_notm}}](../services/kmip_considerations.html)                  | Oui | A partir de V2.2 |
| [Veeam on {{site.data.keyword.cloud_notm}}](../services/veeam_considerations.html)                          | Oui | A partir de V1.8 |
| [VMware HCX on {{site.data.keyword.cloud_notm}}](../services/hcx_considerations.html)                         | Non | Non applicable |
| [Zerto on {{site.data.keyword.cloud_notm}}](../services/addingzertodr.html)                                 | Oui | A partir de V1.2 |


## Ajout de services à des instances vCenter Server

Pour ajouter un service à votre instance vCenter Server, cliquez sur le lien de service approprié dans le tableau précédent pour passer en revue les remarques relatives au service et vérifiez les composants qui sont déployés. Suivez ensuite les instructions décrites dans la rubrique sur la commande de service afin d'ajouter le service à votre instance.

### Résultats de l'installation d'un service

Lorsque l'installation du service est terminée, vous êtes prévenu par un courrier électronique, et le service s'affiche sur la page **Services** de l'instance avec le statut **Installé**.

## Affichage des services pour une instance vCenter Server

1. A partir de la console {{site.data.keyword.vmwaresolutions_short}}, cliquez sur **Instances déployées** dans le panneau de navigation de gauche.
2. Dans le tableau **Instances vCenter Server**, cliquez sur l'instance dont vous souhaitez afficher les services.
3. Cliquez sur **Services** dans le panneau de navigation de gauche.
4. Sur la page **Services**, cliquez sur un service pour passer en revue les informations le concernant, par exemple, le statut du service et d'autres détails.
5. Selon le service visualisé, vous pouvez accéder aux consoles de service à l'aide des données d'identification fournies sur la page des détails de service et vous pouvez gérer le service à partir de là.

## Retrait de services pour une instance vCenter Server

1. A partir de la console {{site.data.keyword.vmwaresolutions_short}}, cliquez sur **Instances déployées** dans le panneau de navigation de gauche.
2. Dans le tableau **Instances vCenter Server**, cliquez sur l'instance dont vous souhaitez retirer des services.
3. Cliquez sur **Services** dans le panneau de navigation de gauche.
4. Sur la page **Services**, localisez l'instance de service que vous souhaitez retirer et cliquez sur l'icône **Supprimer**.
5. Dans la fenêtre **Supprimer un service**, passez en revue, le cas échéant, les remarques ou avertissements. Sélectionnez **Je comprends** et cliquez sur **Supprimer**.

### Résultats du retrait d'un service

Une fois votre demande de retrait du service acceptée, le service prend le statut **Retrait en cours**.

Lorsque le retrait du service est terminé, vous êtes prévenu par un courrier électronique, et le service est retiré de la page **Services** de l'instance.

**Attention** : les services retirés vous sont facturés jusqu'à échéance du cycle de facturation de l'infrastructure {{site.data.keyword.cloud_notm}}.

### Liens connexes

* [Foire aux questions](../vmonic/faq.html)
