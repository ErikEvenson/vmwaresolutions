---

copyright:

  years:  2016, 2018

lastupdated: "2018-08-17"

---

# Release notes for V2.5

This release includes new features, component updates, usability enhancements, and bug fixes. For a list of fixed issues in different releases, known issues with the product, and additional tips to use {{site.data.keyword.vmwaresolutions_full}}, see [{{site.data.keyword.vmwaresolutions_short}} dW Answers](https://developer.ibm.com/answers/topics/cloudvmw/){:new_window}.

## Spectre and Meltdown remediation

{{site.data.keyword.vmwaresolutions_short}} has released patches from VMware in response to the vulnerabilities known as Spectre and Meltdown (CVE-2017-5753, CVE-2017-5715, and CVE-2017-5754).

* CVEID: [CVE-2017-5753](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5753)
* CVEID: [CVE-2017-5715](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5715)
* CVEID: [CVE-2017-5754](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5754)

For more information, see [Addressing Spectre and Meltdown vulnerabilities](../vmonic/trbl_fix_spectre.html).

## NSX component update

This release installs VMware NSX for vSphere 6.4.1 for new deployments of VMware vCenter Server on {{site.data.keyword.cloud_notm}}, VMware vCenter Server on {{site.data.keyword.cloud_notm}} with Hybridity Bundle, NetApp ONTAP Select, and VMware Federal on {{site.data.keyword.cloud_notm}}.

## Removal of default backup configuration

{{site.data.keyword.vmwaresolutions_short}} offers two integrated add–on services for backup: IBM Spectrum Protect&trade; Plus on {{site.data.keyword.cloud_notm}} and Veeam on {{site.data.keyword.cloud_notm}}. These services allow you to plan and provide for the recovery of both your management infrastructure and your workload. Additionally, IBM Resiliency Services offers managed services for Veeam backups.

Starting with the V2.5 release, the IBM Spectrum Protect Plus on {{site.data.keyword.cloud_notm}} and Veeam on {{site.data.keyword.cloud_notm}} services, when deployed, no longer preconfigure the backup of any VMs. This change allows you to ensure proper configuration of all aspects of your backup jobs, including schedule, retention period, use of deduplication, monitoring and alerts, and management of encryption keys. Additionally, the IBM CloudDriver VM is no longer configured as a persistent file server for NSX backups.

You are responsible for the configuration, management, and monitoring of all software components, including the backup and availability of the management infrastructure and workloads. For more information, see [Backing up components](../archiref/solution/solution_backingup.html#backing-up-components).

**Note:** This change does not affect instances deployed prior to V2.5 that have already installed the IBM Spectrum Protect Plus on {{site.data.keyword.cloud_notm}} or Veeam on {{site.data.keyword.cloud_notm}} service.

## IBM CloudDriver resiliency

For instances deployed in or upgraded to V2.5 or later releases, the IBM CloudDriver component is no longer configured as a virtual machine (VM) within the vSphere cluster. Instead, it is deployed as an {{site.data.keyword.cloud_notm}} infrastructure virtual server instance (VSI) as needed with the latest {{site.data.keyword.cloud_notm}} for VMware code for operations such as deploying additional nodes, clusters, or services. Additionally, the IBM CloudDriver is changed to communicate with the {{site.data.keyword.cloud_notm}} management plane using the {{site.data.keyword.cloud_notm}} private network so that the management NSX Edge Services Gateway (ESG) firewall and network address translation (NAT) rules permitting the IBM CloudDriver to communicate outbound to the public network are removed.

Some add-on services such as F5 on {{site.data.keyword.cloud_notm}}, FortiGate Virtual Appliance on {{site.data.keyword.cloud_notm}}, and Zerto on {{site.data.keyword.cloud_notm}} still require public network access, so the management NSX ESG remains deployed in all instances.

## IAM-enabled user and access management

Starting with the V2.5 release, {{site.data.keyword.vmwaresolutions_short}} is integrated with IBM Identity and Access Management (IAM) to provide a unified approach for managing user accounts and user access within your {{site.data.keyword.cloud_notm}} account. Because of which:
* You can now add multiple users to your {{site.data.keyword.cloud_notm}} account for collaboration, and you can manage their access to the services and resources provisioned in your account by assigning different platform access roles to them.  
* Instances that are deployed in V2.5 and later releases are automatically linked to the user account that is being used when the instance is ordered.
* For instances that were deployed in V2.4 and previous releases, you can migrate them to a specified {{site.data.keyword.cloud_notm}} account and then manage them by using IAM as well.

For more information, see the following topics:
* [Inviting users to access services and resources](../vmonic/iamuserinvite.html)
* [Managing user access with IAM](../vmonic/iam.html)

## Changes to user accounts and groups for VMware vCenter Server and VMware Cloud Foundation instances

The **ic4v-vCenter** user group has been created on the Microsoft Active Directory server and added to global permissions on vCenter Server and user groups for the NSX Manager. The group contains the **automation** user account for vCenter Server instances and service-specific user accounts for vCenter Server and Cloud Foundation instances.

Do not edit global permissions of the **ic4v-vCenter** group in the **Users and Groups** page on the VMware vSphere Web Client. Doing so can impact management operations.

For Cloud Foundation instances, use the **customerroot** host user ID in place of the **root** host user ID. Continue to use the **root** host user ID for vCenter Server instances.

For more information about user accounts, see the following topics:

* [Considerations about changing vCenter Server artifacts](../vcenter/vcenter_chg_impact.html)
* [Considerations about changing Cloud Foundation artifacts](../sddc/cf_chg_impact.html)

## Updates for add-on services

### IBM Spectrum Protect Plus on IBM Cloud

Starting with the V2.5 release, the IBM Spectrum Protect Plus on {{site.data.keyword.cloud_notm}} service is deployed as two separate VMs based on best practices, with one VM running the Spectrum Protect Plus server and the other VM running the vSnap server and VADP proxy.

You can now order up to ten backup data stores, allowing up to 120 TB of backup storage. The vSnap and VADP VM are sized depending on your selected backup storage size and according to the information in the [IBM Spectrum Protect Plus Blueprints](https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Tivoli%20Storage%20Manager/page/IBM%20Spectrum%20Protect%20Plus%20Blueprints).

### KMIP for VMware on IBM Cloud

A new endpoint is now available in Germany for the KMIP for VMware on {{site.data.keyword.cloud_notm}} service.

For more information, see [KMIP for VMware on {{site.data.keyword.cloud_notm}} service configuration](../services/kmip_ordering.html#kmip-for-vmware-on-ibm-cloud-service-configuration).

## New and updated documentation

### Attached storage documentation

The Attached storage for vCenter Server on IBM Cloud technical document is now available in the *Reference* section of the user documentation. This reference architecture document is available in English only. For more information, see [Attached storage for vCenter Server on IBM Cloud](../archiref/attached-storage/storage-benefits.html).

### Technical specifications

The technical specifications for all instance types and service types are now available in the user documentation and linked from the user interface. For more information, see the appropriate overview topic for your instance and service.

### Services documentation

The services information is improved to easily identify the service support based on the release number it was made available in.

For more information, see the following topics:

* [Available services for vCenter Server instances](../vcenter/vc_addingremovingservices.html#available-services-for-vcenter-server-instances)
* [Available services for vCenter Server with Hybridity Bundle instances](../vcenter/vc_hybrid_addingremovingservices.html#available-services-for-vcenter-server-with-hybridity-bundle-instances)
* [Available services for Cloud Foundation instances](../sddc/sd_addingremovingservices.html#available-services-for-cloud-foundation-instances)

## User interface updates and enhancements

The user interface is updated and provides the following enhancements:

* If you have an {{site.data.keyword.cloud_notm}} infrastructure (SoftLayer) account that is linked to your {{site.data.keyword.cloud_notm}} account, you can now click the newly added **Retrieve** button on the **Settings** page to get the user name and API key for your  {{site.data.keyword.cloud_notm}} infrastructure (SoftLayer) account automatically.
* A new **Deployment History** tab is added on the left navigation pane of the instance details page for you to check deployment history of an instance.
* Various error messages and tooltip enhancements have been made to assist you in selecting the appropriate setting on the user interface.
