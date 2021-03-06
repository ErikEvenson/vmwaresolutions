---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-27"

---

# HyTrust DataControl on IBM Cloud 概述

HyTrust DataControl on {{site.data.keyword.cloud}} 服务通过集成密钥管理提供高强度加密功能，以确保工作负载在整个生命周期中的安全。此服务可以提供操作系统级别和数据级别的加密，这意味着可以对工作负载中的任何目录、文件夹或文件进行加密和解密。

**可用性**：此服务仅可用于运行 vSphere 6.5 以及部署在（或升级到）V2.3 或更高发行版的实例。

## HyTrust DataControl on IBM Cloud 的技术规范

HyTrust DataControl on {{site.data.keyword.cloud_notm}} 服务中订购并包含了以下组件：

### HyTrust DataControl 设备
* CPU：2 个 vCPU
* RAM：8 GB
* 磁盘：在融合集群中的 vSAN 上常驻 20 GB VMDK
* 网络：位于为管理指定的支持 VLAN 的专用可移植网络上

### 高可用性
两个 DataControl 设备以主动/主动配置方式进行部署。

### 许可证和费用

按主机订购许可证：为环境中的每个主机订购了一个 HyTrust DataControl 许可证。

## 除去 HyTrust DataControl on IBM Cloud 时的注意事项

除去 HyTrust DataControl on {{site.data.keyword.cloud_notm}} 服务之前，请确保已对 DataControl 中的所有磁盘进行加密或备份。除去该服务后，可能会删除密钥，并且可能会锁定 VM。

### 相关链接

* [订购 HyTrust DataControl on {{site.data.keyword.cloud_notm}}](htdc_ordering.html)
* [管理 HyTrust DataControl on {{site.data.keyword.cloud_notm}}](managinghtcc.html)
* [联系 IBM 支持](../vmonic/trbl_support.html)
* [常见问题](../vmonic/faq.html)
* [HyTrust Web 站点](https://www.hytrust.com/)
