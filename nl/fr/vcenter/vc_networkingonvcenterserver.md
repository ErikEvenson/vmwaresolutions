---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-24"

---

# Remarques relatives à la mise en réseau des instances vCenter Server

Passez en revue les informations suivantes pour obtenir des détails relatifs aux remarques et exigences concernant la mise en réseau de vos instances vCenter Server on {{site.data.keyword.cloud}}. Prenez soin de respecter les exigences de sorte que vos instances puissent fonctionner correctement.

## Composants de mise en réseau pour les instances vCenter Server

Pour passer en revue les composants de mise en réseau inclus dans votre instance vCenter Server, voir [Spécifications techniques relatives aux instances vCenter Server](vc_vcenterserveroverview.html#technical-specifications-for-vcenter-server-instances). 

## Remarques relatives au pare-feu NSX

Si vous utilisez des pare-feu DFW NSX, vous devez configurer des règles pour toutes les communications établies à partir de l'instance de serveur virtuel IBM CloudDriver de manière à autoriser tous les protocoles à communiquer sur les adresses IP `10.0.0.0/8` et `161.26.0.0/16`.

## Utilisation de NSX avec vos machines virtuelles

Lors du déploiement d'une instance vCenter Server, VMware NSX est commandé, installé, mis sous licence et configuré dans votre instance. De même, NSX Manager, des contrôleurs NSX et la zone de transport NSX sont configurés et chaque serveur ESXi est configuré avec les composants NSX.

Une passerelle NSX Edge Services Gateway est également déployée pour être utilisée par vos machines virtuelles de charge de travail. Pour plus d'informations, voir [Configuration du réseau en vue d'utiliser la passerelle NSX ESG gérée par le client avec vos machines virtuelles](vc_esg_config.html#configuring-your-network-to-use-the-customer-managed-nsx-esg-with-your-vms).

## Remarques relatives à la modification de mots de passe pour des composants NSX

Passez en revue les remarques suivantes avant de modifier les mots de passe de NSX Manager, des contrôleurs NSX et de la passerelle NSX Edge :
* Ne modifiez pas le mot de passe de NSX Manager figurant sur la page **Récapitulatif** de l'instance dans la console {{site.data.keyword.vmwaresolutions_short}}.
* Ne modifiez pas les mots de passe des contrôleurs NSX. Pour savoir comment modifier les mots de passe des contrôleurs NSX, voir [Modification du mot de passe d'un contrôleur](https://docs.vmware.com/en/VMware-NSX-for-vSphere/6.2/com.vmware.nsx.admin.doc/GUID-2667DD9E-E2F5-4403-BAC2-C7D1BBC23228.html).
* Ne modifiez pas le mot de passe et les paramètres SSH de la passerelle VMware NSX ESG (Edge Services Gateway) gérée par le client. Ne modifiez pas le mot de passe de la passerelle VMware NSX ESG (Edge Services Gateway) de gestion et du routeur logique distribué associé.

### Liens connexes

* [Présentation de NSX](https://docs.vmware.com/en/VMware-NSX-for-vSphere/6.2/com.vmware.nsx-cross-vcenter-install.doc/GUID-10944155-28FF-46AA-AF56-7357E2F20AF4.html){:new_window}
* [Passerelle NSX Edge Services Gateway](https://www.ibm.com/cloud/garage/architectures/implementation/virtualization_nsx){:new_window}
* [Gestion des règles de conversion d'adresses réseau](https://docs.vmware.com/en/VMware-NSX-for-vSphere/6.2/com.vmware.nsx.admin.doc/GUID-5896D8CF-20E0-4691-A9EB-83AFD9D36AFD.html){:new_window}
