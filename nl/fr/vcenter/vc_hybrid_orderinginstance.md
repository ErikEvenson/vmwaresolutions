---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-19"

---

# Commande d'instances vCenter Server with Hybridity Bundle

Afin de déployer une plateforme virtuelle VMware personnalisable et flexible totalement adaptée à vos besoins en charge de travail, commandez une instance VMware vCenter Server on {{site.data.keyword.cloud}} with Hybridity Bundle. L'instance vCenter Server with Hybridity Bundle inclut la licence VMware Hybrid Cloud Extension (HCX) qui vous autorise à utiliser le service VMware HCX on {{site.data.keyword.cloud_notm}}. Vous pouvez également ajouter des services, tels que [Zerto on {{site.data.keyword.cloud_notm}}](../services/addingzertodr.html) pour la reprise après incident.

## Conditions requises

Assurez-vous que :
*  Vous avez configuré les données d'identification de l'infrastructure {{site.data.keyword.cloud_notm}} sur la page **Paramètres**. Pour plus d'informations, voir [Gestion des paramètres et comptes utilisateur](../vmonic/useraccount.html).
*  Vous avez passé en revue les informations décrites dans la rubrique [Exigences et planification pour les instances vCenter Server with Hybridity Bundle](vc_hybrid_planning.html).
* Vous avez passé en revue le format des noms d'instance et de domaine. Le nom de domaine et le libellé de sous-domaine sont utilisés pour générer le nom d'utilisateur et les noms de serveur de l'instance.

Tableau 1. Format de la valeur des noms d'instance et de domaine

| Nom        | Format de la valeur      |
  |:------------- |:------------- |
  | Nom de domaine | `<root_domain>` |  
  | Nom d'utilisateur de connexion vCenter Server | `<user_id>@<root_domain>` (utilisateur Microsoft Active Directory) ou `administrator@vsphere.local` |
  | Nom de domaine complet vCenter Server | `vcenter.<subdomain_label>.<root_domain>`. La longueur maximale admise est de 50 caractères. |
  | Nom du site de connexion unique | `<subdomain_label>` |
  | Nom de serveur ESXi qualifié complet | `<host_prefix><n>.<subdomain_label>.<root_domain>`, où `<n>` est la séquence du serveur ESXi. La longueur maximale admise est de 50 caractères. |  
  | Nom de domaine complet PSC | `psc-<subdomain_label>.<subdomain_label>.<root_domain>`. La longueur maximale admise est de 50 caractères. |

**Important** : ne modifiez aucune des valeurs définies lors de la commande et du déploiement de l'instance. Toute modification risquerait de rendre votre instance inutilisable. Par exemple, le réseau public pourrait s'arrêter, les serveurs et les instances de serveur virtuel pourraient passer derrière un mi-parcours Vyatta ou l'instance de serveur virtuel IBM CloudBuilder pourrait s'arrêter ou être supprimée.

## Paramètres système

Vous devez spécifier les paramètres système répertoriés ci-après lorsque vous commandez une instance vCenter Server with Hybridity Bundle.

### Nom d'instance

Le nom de l'instance qui doit respecter les règles suivantes :
* Seuls les caractères alphanumériques et le tiret (-) sont autorisés.
* Le nom d'instance doit commencer et se terminer par un caractère alphanumérique.
* Le nom d'instance ne doit pas dépasser 10 caractères.
* Le nom d'instance doit être unique au sein de votre compte.

### Principale ou secondaire

Indiquez si vous souhaitez commander une nouvelle instance principale ou une instance secondaire pour une instance principale existante.

## Paramètres d'octroi de licence

Les licences suivantes sont incluses avec votre commande d'instance vCenter Server with Hybridity Bundle. Vous devez spécifier **Advanced** ou **Enterprise** pour les éditions de licence NSX.

* VMware vCenter Server 6.5
* VMware vSphere Enterprise Plus 6.5u1
* VMware NSX Service Providers Edition (Advanced ou Enterprise) 6.4
* Edition de licence VMware vSAN 6.6 (Advanced ou Enterprise).

**Attention :**
* Les instances vCenter Server with Hybridity Bundle ne prennent pas en charge le mode BYOL (Bring Your Own License).
* Les éditions de licence minimum sont indiquées sur l'interface utilisateur. Si différentes éditions de composant sont prises en charge, vous pouvez sélectionner celle qui vous convient.

## Paramètres de serveur bare metal

Les paramètres bare metal dépendent de votre {{site.data.keyword.CloudDataCent_notm}} et de votre configuration personnalisée.

Quatre serveurs ESXi sont nécessaires pour le cluster initial et pour les clusters d'après déploiement dans le cadre des configurations vSAN. Tous les serveurs ESXi se partagent la même configuration. Après le déploiement, vous pouvez ajouter quatre clusters supplémentaires.

### Emplacement de centre de données

Sélectionnez l'{{site.data.keyword.CloudDataCent_notm}} où l'instance doit être hébergée.

### Personnalisée

Indiquez le modèle d'UC et la quantité de mémoire RAM du serveur bare metal personnalisé.

Tableau 2. Options pour les serveurs {{site.data.keyword.baremetal_short}} personnalisés

| Options d'UC        | Options de RAM       |
|:------------- |:------------- |
| Dual Intel Xeon E5-2620 v4/16 coeurs au total, 2,1 GHz | 64 Go, 128 Go, 256 Go, 512 Go, 768 Go, 1,5 To |
| Dual Intel Xeon E5-2650 v4/24 coeurs au total, 2,2 GHz | 64 Go, 128 Go, 256 Go, 512 Go, 768 Go, 1,5 To |
| Dual Intel Xeon E5-2690 v4/28 coeurs au total, 2,6 GHz | 64 Go, 128 Go, 256 Go, 512 Go, 768 Go, 1,5 To |
| Processeur Dual Intel Xeon Silver 4110/16 coeurs au total, 2,1 GHz | 64 Go, 96 Go, 128 Go, 192 Go, 384 Go, 768 Go, 1,5 To |
| Processeur Dual Intel Xeon Gold 5120/28 coeurs au total, 2,2 GHz | 64 Go, 96 Go, 128 Go, 192 Go, 384 Go, 768 Go, 1,5 To |
| Processeur Dual Intel Xeon Gold 6140/36 coeurs au total, 2,3 GHz | 64 Go, 96 Go, 128 Go, 192 Go, 384 Go, 768 Go, 1,5 To |
### Nombre de serveurs bare metal

Quatre serveurs ESXi sont sélectionnés par défaut et ne sont pas modifiables.

## Paramètres de stockage

VMware vSAN 6.6 est inclus avec votre commande d'instance vCenter Server with Hybridity Bundle. Vous devez spécifier les paramètres de stockage suivants lorsque vous commandez l'instance :

* **Type et taille de disque pour disques de capacité vSAN** : sélectionnez la capacité qui répond à vos besoins de stockage partagé.
* **Nombre de disques de capacité vSAN** : sélectionnez le nombre de disques que vous voulez ajouter pour le stockage partagé vSAN. Le nombre de disques doit être de 2, 4, 6 ou 8.

## Paramètres d'interface réseau

Vous devez spécifier les paramètres d'interface réseau répertoriés ci-après lorsque vous commandez une instance vCenter Server with Hybridity Bundle.

### Préfixe de nom d'hôte

  Le préfixe du nom d'hôte qui doit respecter les règles suivantes :
  *  Seuls les caractères alphanumériques et le tiret (-) sont autorisés.
  *  Le préfixe de nom d'hôte doit commencer et se terminer par un caractère alphanumérique.
  *  Le préfixe de nom d'hôte ne doit pas dépasser 10 caractères.

### Libellé de sous-domaine

Le libellé du sous-domaine qui doit respecter les règles suivantes :
*  Seuls les caractères alphanumériques et le tiret (-) sont autorisés.
*  Le libellé de sous-domaine doit commencer et se terminer par un caractère alphanumérique.
*  Le libellé de sous-domaine ne doit pas dépasser 10 caractères.
*  Le libellé de sous-domaine doit être unique au sein de votre compte.

### Nom de domaine

Le nom du domaine racine qui doit respecter les règles suivantes :
* Le nom de domaine doit être composé d'au moins deux chaînes séparées par un point (.)
* La première chaîne doit commencer par un caractère alphabétique et se terminer par un caractère alphanumérique.
* Toutes les chaînes, à l'exception de la dernière, ne peuvent contenir que des caractères alphanumériques et des tirets (-).
* La dernière chaîne ne peut contenir que des caractères alphabétiques.
* La dernière chaîne doit comporter entre 2 et 24 caractères.

**Remarque :** la longueur maximale du nom de domaine complet des hôtes et des machines virtuelles est de 50 caractères. Les noms de domaine doivent respecter cette longueur maximale.

### Commander de nouveaux VLAN

Sélectionnez **Commander de nouveaux VLAN** pour commander un nouveau VLAN public et deux nouveaux VLAN privés.

Un VLAN public et deux VLAN privés sont nécessaires pour votre commande d'instance. Les deux VLAN privés sont liés respectivement à chaque serveur bare metal.

### Sélectionner des VLAN existants

En fonction de l'{{site.data.keyword.CloudDataCent_notm}} que vous avez sélectionné, des VLAN publics et privés existants peuvent être disponibles.

Un VLAN public et deux VLAN privés sont nécessaires pour votre commande d'instance. Les deux VLAN privés sont liés respectivement à chaque serveur bare metal.

Choisissez **Sélectionner des VLAN existants** pour réutiliser des VLAN publics et privés existants et faites votre choix parmi les VLAN et les sous-réseaux disponibles.

**Important :**
* Vérifiez que la configuration de pare-feu sur les VLAN sélectionnés ne bloque pas le trafic des données de gestion.
* Vérifiez que tous les VLAN sélectionnés se trouvent dans le même pod, car les serveurs ESXi ne peuvent pas être mis à disposition sur des VLAN multi-pods.

### DNS configuration

Sélectionnez la configuration de système de noms de domaine (DNS, Domain Name System) de votre instance :

* **Une instance de serveur virtuel Windows publique pour Active Directory/DNS** : une unique instance de serveur virtuel Windows Microsoft pour Microsoft Active Directory (AD), qui fonctionne en tant que serveur de noms de domaine pour l'instance où sont enregistrés les hôtes et les machines virtuelles, est déployée et peut être interrogée.
* **Deux machines virtuelles Windows Server dédiées à haute disponibilité sur le cluster de gestion** : deux machines virtuelles Microsoft Windows sont déployées, pour plus de sécurité et de robustesse.

**Important :** vous devez fournir deux licences Microsoft Windows Server 2012 R2 si vous configurez votre instance de manière à utiliser deux machines virtuelles Microsoft Windows. Utilisez la licence d'édition Microsoft Windows Server 2012 R2 Standard et/ou la licence d'édition Microsoft Windows Server 2012 R2 Datacenter.

Chaque licence ne peut être affectée qu'à un seul serveur physique et couvre jusqu'à deux processeurs physiques. Une licence d'édition Standard est à même d'exécuter deux machines virtuelles Microsoft Windows virtualisées par serveur à 2 processeurs. Par conséquent, deux licences sont nécessaires puisque deux machines virtuelles Microsoft Windows sont déployées sur deux hôtes différents.

Vous disposez de 30 jours pour activer les machines virtuelles.

Pour plus d'informations sur la commande de licence Windows, voir la [documentation Windows Server 2012 R2](https://www.microsoft.com/en-us/licensing/product-licensing/windows-server-2012-r2.aspx#tab=2).

## Paramètres de services

Lorsque vous commandez une instance vCenter Server with Hybridity Bundle, vous pouvez également commander des services supplémentaires. Pour plus d'informations sur les services, voir [Services disponibles pour les instances vCenter Server with Hybridity Bundle](vc_hybrid_addingremovingservices.html#available-services-for-vcenter-server-with-hybridity-bundle-instances).

## Récapitulatif de la commande

Selon la configuration que vous avez sélectionnée pour l'instance et les services complémentaires, le coût estimé est généré et affiché instantanément dans la section **Récapitulatif de la commande** sur le panneau de droite. Cliquez sur **Détails concernant la tarification** en bas à droite du panneau pour générer un document PDF contenant les détails relatifs à l'estimation.

## Procédure

1. Dans le catalogue {{site.data.keyword.cloud_notm}}, cliquez sur **VMware** dans le panneau de navigation de gauche, puis cliquez sur **vCenter Server** dans la section **Centres de données virtuels**.
2. Sur la page **VMware vCenter Server on IBM Cloud**, cliquez sur la carte **vCenter Server with Hybridity Bundle**, puis sur **Créer**.
3. Sur la page **vCenter Server**, entrez le nom de l'instance.
4. Sélectionnez le type d'instance :
   * Cliquez sur **Instance principale** pour déployer une seule instance dans l'environnement ou pour déployer la première instance dans une topologie multisite.
   * Cliquez sur **Instance secondaire** pour connecter l'instance à une instance (principale) existante dans l'environnement à des fins de haute disponibilité et procédez comme suit :
     1. Sélectionnez l'instance principale à laquelle vous voulez que l'instance secondaire soit connectée.
     2. Entrez le mot de passe de l'administrateur PSC pour l'instance principale.
5. Sélectionnez l'édition de licence NSX et l'édition de licence vSAN.
6. Spécifiez les paramètres de serveur bare metal.
  1. Sélectionnez l'{{site.data.keyword.CloudDataCent_notm}} qui doit héberger l'instance.
  2. Sélectionnez le modèle d'UC **Personnalisé** et la quantité de mémoire **RAM**.

  **Remarque :** la valeur quatre, affectée par défaut à la zone **Nombre de serveurs bare metal**, ne peut pas être modifiée.

7. Procédez à la configuration du stockage.
  1. Renseignez la zone **Type et taille de disque pour disques de capacité vSAN**.
  2. Renseignez la zone **Nombre de disques de capacité vSAN**.
8. Procédez à la configuration de l'interface réseau.
  1. Renseignez les zones Préfixe de nom d'hôte, Libelle de sous-domaine et Nom de domaine racine.
  2. Sélectionnez la configuration VLAN.
     *  Si vous voulez commander de nouveaux VLAN publics et privés, cliquez sur **Commander de nouveaux VLAN**.
     *  Si vous voulez réutiliser les VLAN publics et privés existants lorsqu'ils sont disponibles, cliquez sur **Sélectionner des VLAN existants**, puis sélectionnez le VLAN public, le sous-réseau principal, le VLAN privé, le sous-réseau principal privé et le VLAN privé secondaire.
  3. Sélectionnez la configuration DNS.
9. Sélectionnez les services complémentaires à déployer dans l'instance en cliquant sur la carte de service correspondante. Si un service nécessite de la configuration, spécifiez les paramètres qui lui sont propres et cliquez sur **Ajouter un service** sur la carte.  
Pour savoir comment indiquer les paramètres d'un service, voir la rubrique de commande de service correspondante.

8. Sur la page **Récapitulatif de la commande**, vérifiez la configuration de l'instance avant de passer la commande.
   1. Passez en revue les paramètres de l'instance.
   2. Passez en revue le coût estimé de l'instance. Cliquez sur **Détails concernant la tarification** pour générer un récapitulatif au format PDF. Pour sauvegarder ou imprimer votre récapitulatif de commande, cliquez sur l'icône d'**impression** ou de **téléchargement** dans l'angle supérieur droit de la fenêtre du PDF.
   3. Cliquez sur le ou les liens des conditions applicables à votre commande et prenez soin d'accepter ces conditions avant de commander l'instance.
   4. Cliquez sur **Mettre à disposition**.

## Résultats

Le déploiement de l'instance commence automatiquement. Vous recevez une confirmation que la commande est en cours de traitement et vous pouvez vérifier l'état du déploiement en affichant les détails de l'instance.

Une fois l'instance correctement déployée, les composants décrits dans [Spécifications techniques relatives aux instances vCenter Server with Hybridity Bundle](vc_hybrid_overview.html#technical-specifications-for-vcenter-server-with-hybridity-bundle-instances) sont installés sur votre plateforme virtuelle VMware. Les serveurs ESXi que vous avez commandés sont, par défaut, regroupés en **cluster1**. Si vous avez commandé des services supplémentaires, le déploiement des services commence une fois votre commande honorée.

Lorsque l'instance est prête pour utilisation, elle prend le statut **Prêt à l'emploi** et vous recevez une notification par courrier électronique.

Lorsque vous commandez une instance secondaire, le client Web VMware vSphere de l'instance principale (liée à l'instance secondaire) devra peut-être être redémarré une fois la commande d'instance secondaire honorée.

## Etape suivante

Affichez et gérez l'instance vCenter Server with Hybridity Bundle que vous avez commandée.

**Important** : vous devez gérer les composants {{site.data.keyword.vmwaresolutions_short}} créés dans votre compte {{site.data.keyword.cloud_notm}} uniquement depuis la console {{site.data.keyword.vmwaresolutions_short}}, et non depuis le portail	{{site.data.keyword.slportal}} ou autre élément extérieur à la console.
Si vous modifiez ces composants en dehors de la console {{site.data.keyword.vmwaresolutions_short}}, les modifications ne sont pas synchronisées avec la console.

**ATTENTION** : gérer des composants {{site.data.keyword.vmwaresolutions_short}} (installés dans votre compte {{site.data.keyword.cloud_notm}} lorsque vous avez commandé l'instance) en dehors de la console {{site.data.keyword.vmwaresolutions_short}} risque de rendre votre environnement instable. Ces activités de gestion incluent :
*  L'ajout, la modification, le retour ou la suppression de composants
*  L'extension ou la réduction de la capacité de l'instance via l'ajout ou la suppression de serveurs ESXi
*  La mise hors tension de composants
*  Le redémarrage de services

   Seules les activités de gestion des partages de fichiers du stockage partagé depuis le portail {{site.data.keyword.slportal}} font exception. Il s'agit des activités suivantes : commande, suppression (pouvant avoir un impact sur des magasins de données éventuellement montés), accord d'autorisation et montage de partages de fichiers de stockage partagé.

### Liens connexes

* [Inscription à un compte {{site.data.keyword.cloud_notm}}](../vmonic/signing_softlayer_account.html)
* [Affichage des instances vCenter Server with Hybridity Bundle](vc_hybrid_viewinginstances.html)
* [Configuration multisite pour des instances vCenter Server with Hybridity Bundle](vc_hybrid_multisite.html)
* [Ajout et affichage de clusters pour des instances vCenter Server with Hybridity Bundle](vc_hybrid_addingviewingclusters.html)
* [Extension et réduction de capacité pour des instances vCenter Server with Hybridity Bundle](vc_hybrid_addingremovingservers.html)
* [Commande, affichage et retrait de services pour des instances vCenter Server with Hybridity Bundle](vc_hybrid_addingremovingservices.html)
* [Suppression d'instances vCenter Server with Hybridity Bundle](vc_hybrid_deletinginstance.html)
