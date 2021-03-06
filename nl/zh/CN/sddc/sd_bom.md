---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-19"

---

# Cloud Foundation 材料清单

查看 VMware Cloud Foundation 实例的材料清单 (BOM) 信息。

## Cloud Foundation 实例的 VLAN BOM

下表详细描述了 Cloud Foundation VLAN 的 BOM 信息。

表 1. Cloud Foundation 实例中 VLAN 的 BOM

|VLAN|类型|详细信息|
|:----------|:----------|:-------------|
|VLAN1|公用，主|分配给物理 ESXi 服务器以用于公用网络访问。在初始部署后未使用。可用于因特网访问。|
|VLAN2|专用 A，主|由 {{site.data.keyword.cloud}} 分配给物理 ESXi 服务器。通过管理界面用于 VMware vSphere 管理流量。<br><br>分配给充当管理组件的 VM（虚拟机）。<br><br>分配给 VMware NSX VTEP（VXLAN 隧道端点）|
|VLAN3|专用 B，可移植|分配给 VMware vSAN（如果使用）。<br><br>分配给 VMware NFS（如果使用）。<br><br>分配给 VMware vSphere vMotion。|

## Cloud Foundation 实例的软件 BOM

下表详细描述了 Cloud Foundation 软件组件的 BOM 信息。

表 2. Cloud Foundation 实例中软件组件的 BOM

|制造商|组件|版本|
|:-------------|:-----------------------------------------|:-------------|
|VMware|vSphere ESXi|6.5 U1g（应用了补丁级别 ESXi650-201803001 的 ESXi 6.5u1）|
|VMware|vCenter Server Appliance|6.5 Update 1g|
|VMware|Platform Services Controller|6.5 Update 1g|
|VMware|vSAN|6.6.1|
|VMware|NSX for vSphere|6.3.5|
|VMware|SDDC Manager|2.4|
|IBM|CloudDriver|2.4|
|Microsoft|Windows Server Standard Edition（64 位）|2012R2|

## ESXi 服务器的高级配置设置

查看下表以了解在 ESXi 服务器上应用的高级配置设置的概述，具体取决于 Cloud Foundation 实例是部署在 V2.2 或更高版本中，还是从先前 V2.1 或更低发行版升级到 V2.2 或更高版本。

表 3. Cloud Foundation 实例和集群的 ESXi 服务器高级配置设置

|配置设置|如果是新部署在 V2.2 或更高版本中|如果是从 V2.1 或更低版本升级|   
|:------------- |:------------- |:------------- |
|TCP/IP 堆大小|**TcpipHeapSize** = 32|未设置|
|最大 TCP/IP 堆大小|**TcpipHeapMax** = 1536|未设置|  
|最大卷数|**MaxVolumes** = 256|**/NFS/MaxVolumes** 和 **/NFS41/MaxVolumes** = 256|  
|脉动信号最大故障数|**HeartbeatMaxFailures** = 10|未设置|  
|脉动信号频率|**HeartbeatFrequency** = 12|未设置|  
|脉动信号超时|**HeartbeatTimeout** = 5|未设置|
|最大队列深度|**MaxQueueDepth** = 64|未设置|
|队列已满样本大小|**QFullSampleSize** = 32|**/Disk/QFullSampleSize** = 32|
|队列已满阈值|**QFullThreshold** = 8|**/Disk/QFullThreshold** = 8|

**注**：
* IBM Spectrum Protect&trade; Plus on {{site.data.keyword.cloud_notm}} 服务需要 **MaxVolumes** 设置，因为该服务可能会在 ESXi 服务器上使用超过缺省数量的 NFS 安装。
* 配置设置的**未设置**值指示不会自动应用新设置，因为这需要重新引导 ESXi 服务器，这样可能有破坏性。

  建议将**未设置**配置设置更改为新值，以实现在所有实例上的一致性，并为存储扩展提供充分支持。对于所有 {{site.data.keyword.vmwaresolutions_short}} V2.2 和更高发行版，IBM 计划仅测试这些新设置。

  有关更多信息，请参阅[增大定义 ESXi/ESX 主机上 NFS 最大挂载量的默认值](https://kb.vmware.com/s/article/2239)。

### 相关链接

* [VMware ESXi/ESX 的构建号和版本 (2143832)](https://kb.vmware.com/s/article/2143832)
* [VMware vCenter Server 的构建号和版本 (2143838)](https://kb.vmware.com/s/article/2143838)
* [VMware Cloud Foundation on {{site.data.keyword.cloud_notm}} 保护数据表](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=C87A0EC07E7311E6BA51E79BE9476040)
* [Cloud Foundation 概述](sd_cloudfoundationoverview.html)
* [规划 Cloud Foundation 实例](sd_planning.html)
