---

copyright:

  years:  2016, 2018

lastupdated: "2018-08-13"

---

# Attached storage infrastructure management

Infrastructure management refers to the VMware components that are managing the vSphere ESXi infrastructure.

For more information about the components, see Figure 2. NSX Manager network overview in [Virtual infrastructure design](../solution/design_virtualinfrastructure.html).

## Virtual networking design

The network virtualization that is used in this design uses the existing vSphere Distributed Switch (vDS) associated with the private network and specified in the [{{site.data.keyword.vmwaresolutions_full}} architecture](../solution/solution_overview.html).

## vSphere Distributed Switch

As stated previously, another VLAN is created within the vCenter Server solution and used to attach the NFS mount point to the ESXi hosts in the existing cluster. Since the vCenter Server solution already has a vSphere Distributed Switch (vDS) associated with the private network, another port group is created and tagged with the additional VLAN number since this additional VLAN is not native.

The following table describes the default settings of the new port group.

**Important:** Do not change these default settings.

Table 1. NFS port group summary

| Port Group Name | SDDC-DPG-NFS |
|:--------------- |:------------ |
| Port binding | Static |
| VLAN type | Private VLAN B |
| Load balancing | Route base on originating virtual port |
| Active Uplinks | Uplink1 and uplink2 |

In addition to the creation of the vDS port group for NFS storage traffic, a VMkernel port is created on each vSphere ESXi host in the deployment and assigned to the SDDC-DPG-NFS port group. The VMkernel port is also assigned an IP address from the private portable subnet that is associated with the attached storage VLAN, that is, Private VLAN B and its MTU is set to 9000 to support jumbo frames.

Figure 1. Private vDS Port groups and Uplinks

![Private vDS Port groups and Uplinks](private_vds_portgroups_and_uplinks.svg "Private vDS port groups and uplinks")

### vSphere host static routing

Although the vDS is configured with a new port group and a VMkernel port is assigned to the port group, the solution creates a static route on each vSphere ESXi host in the deployment so that all NFS traffic traverses the VLAN and subnet for NFS. The static route is created in `/etc/rc.local.d/local.sh` so that it persists across host restarts.

### Related links

* [Solution overview](../solution/solution_overview.html)
