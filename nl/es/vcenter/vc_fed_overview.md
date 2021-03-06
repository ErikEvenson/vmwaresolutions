---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-19"

---

# Visión general de VMware Federal on IBM Cloud

VMware Federal on {{site.data.keyword.cloud}} ofrece soporte para solicitar una instancia básica de vCenter Server además de proporcionar a las agencias del gobierno federal de EE.UU. la opción de proteger las instancias desplegadas de vCenter Server. Al seleccionar la opción de proteger las instancias desplegadas, se elimina la información confidencial almacenada sobre la instancia y se elimina la conexión de gestión abierta para el acceso continuo a la instancia para funciones de gestión, como la adición y eliminación de hosts y clústeres. Después de seleccionar la opción segura, todas las funciones de gestión se inhabilitan, excepto para una supresión de instancia completa.

Para obtener más información sobre vCenter Server on {{site.data.keyword.cloud_notm}} y la arquitectura de vCenter Server, consulte [Visión general de vCenter Server](vc_vcenterserveroverview.html).

**Atención:** VMware Federal on {{site.data.keyword.cloud_notm}} solo ofrece un subconjunto de las ofertas de vCenter Server. No se da soporte a la configuración de varios sitios, a los servidores nativos de {{site.data.keyword.cloud_notm}} preconfigurados, a traer su propia licencia ni a la opción de solicitar servicios adicionales.

## Especificaciones técnicas para las instancias de VMware Federal en IBM Cloud

Se incluyen los siguientes componentes:

### Servidor nativo

Puede solicitar dos o más {{site.data.keyword.baremetal_short}} personalizados con una de las siguientes configuraciones:

* 2-CPU Intel Broadwell generation (Intel Xeon E5-2600 v4 series)
* 2-CPU Intel Skylake generation (Intel Xeon 4100/5100/6100 series)

Para la configuración de almacenamiento NFS, el número recomendado de {{site.data.keyword.baremetal_short}} se establece en tres como valor predeterminado.

**Nota:** si selecciona almacenamiento vSAN, la configuración necesita cuatro {{site.data.keyword.baremetal_short}}.

### Redes

Se solicitan los siguientes componentes del sistema de redes:
*  Tres VLAN (LAN virtuales): una VLAN pública y dos VLAN privadas
*  Se despliega una VXLAN (LAN extensible virtual) con DLR (direccionador lógico distribuido) para una potencial comunicación este-oeste entre cargas de trabajo locales conectadas a redes de la capa 2 (L2). La VXLAN se despliega como una topología de direccionamiento de ejemplo, que puede modificar o eliminar o a la que puede añadir componentes. También puede añadir zonas de seguridad por conectar VXLAN adicionales a las nuevas interfaces lógicas del DLR.
*  Dos VMware NSX Edge Services Gateways:
  * Una Edge Services Gateway (ESG) de NSX de VMware de servicios de gestión segura para el tráfico de gestión de HTTPS saliente, desplegado por IBM como parte de la topología del sistema de redes de gestión. Las máquinas virtuales de gestión de IBM utilizan esta ESG para comunicarse con componentes externos específicos de gestión de IBM que están relacionados con la automatización. Para obtener más información, consulte [Configuración de la red para que utilice la ESG gestionada por el cliente](../vcenter/vc_esg_config.html#configuring-your-network-to-use-the-customer-managed-nsx-esg-with-your-vms).

    **Importante**: el usuario no puede acceder ni utilizar esta ESG. Si lo modifica, es posible que no pueda gestionar la instancia de vCenter Server desde la consola de {{site.data.keyword.vmwaresolutions_short}}. Además, tenga en cuenta que el uso de un cortafuegos o la inhabilitación de las comunicaciones ESG con componentes externos de gestión de IBM harán que {{site.data.keyword.vmwaresolutions_short}} quede inutilizable.
  * Una Edge Services Gateway de NSX de VMware gestionada por el cliente para el tráfico de salida y de entrada de carga de trabajo HTTPS, que IBM despliega como plantilla que puede modificar para proporcionar acceso VPN o acceso público. Para obtener más información, consulte [¿Representa NSX Edge gestionado por el cliente un riesgo para la seguridad?](../vmonic/faq.html#does-the-customer-managed-nsx-edge-pose-a-security-risk-)

  **Nota**: Los VMware NSX Edge Services (ESG) para el tráfico de gestión de HTTPS saliente se elimina como parte de la acción para proteger la instancia de VMware Federal desplegada. Para obtener más información, consulte [Protección de instancias de VMware Federal](vc_fed_securinginstance.html).

### Instancias de servidor virtual

Se solicitan las siguientes VSI (instancias de servidor virtual):
* Una VSI para IBM CloudBuilder, que se cierra una vez completado el despliegue de la instancia.
* (Para instancias de V2.3 y posteriores) Puede elegir desplegar un único Microsoft Windows Server VSI for Microsoft Active Directory (AD) o dos VM Microsoft Windows de alta disponibilidad en el clúster de gestión para ayudar a mejorar la seguridad y la solidez.
* (Para instancias de V2.2) Se despliega y se puede consultar una VSI de Microsoft Windows Server para Microsoft Active Directory (AD), que funciona como DNS para la instancia en la que se han registrado los hosts y máquinas virtuales.

### Almacenamiento

Durante el despliegue inicial, puede elegir entre las opciones de almacenamiento vSAN y NFS.

La opción vSAN ofrece configuraciones personalizadas, con diversas opciones para el tipo y la cantidad de discos:
* Cantidad de disco: 2, 4, 6 u 8.
* Disco de almacenamiento: SSD SED de 960 GB, SSD SED de 1,9 TB o SSD SED de 3,8 TB.

  Además se solicitan 2 discos de caché de 960 GB por host.

La opción NFS ofrece almacenamiento a nivel de archivo compartido personalizado para cargas de trabajo con distintas opciones de tamaño y de rendimiento:
* Tamaño: 1, 2, 4, 8 o 12 TB.
* Rendimiento: 2, 4 o 10 IOPS/GB.
* Configuración individual de comparticiones de archivos.

Si elige la opción NFS, se solicita una compartición de archivos de 2 TB, 4 IOPS/GB para los componentes de gestión.

### Licencias proporcionadas por IBM y tarifas

* VMware vSphere Enterprise Plus 6.5u1
* VMware vCenter Server 6.5
* VMware NSX Service Providers Edition (Base, Advanced o Enterprise) 6.4
* (Para clústeres vSAN) VMware vSAN Advanced o Enterprise 6.6

## Especificaciones técnicas para los nodos de expansión de VMware Federal en IBM Cloud

Cada nodo de expansión de vCenter Server desplegará e incurrirá en cargos por los siguientes componentes en su cuenta de {{site.data.keyword.cloud_notm}}.

### Hardware para nodos de expansión

Un servidor nativo con la configuración que se muestra en [Especificaciones técnicas para las instancias de VMware Federal en {{site.data.keyword.cloud_notm}}](vcenter/vc_fed_overview.html#technical-specifications-for-vmware-federal-on-ibm-cloud-instances).

### Licencias y tarifas correspondientes a nodos de expansión

* Un VMware vSphere Enterprise Plus 6.5u1
* Un VMware NSX Service Providers Edition (Base, Advanced o Enterprise) 6.4
* (Para clústeres vSAN) VMware vSAN Advanced o Enterprise 6.6

**Importante**: solo debe gestionar los componentes de {{site.data.keyword.vmwaresolutions_short}} que se crean en la cuenta de {{site.data.keyword.cloud_notm}} desde la consola de {{site.data.keyword.vmwaresolutions_short}}, no desde el {{site.data.keyword.slportal}} ni mediante ningún otro método fuera de la consola. Si cambia estos componentes fuera de la consola de {{site.data.keyword.vmwaresolutions_short}}, los cambios no se sincronizan con la consola.

**ATENCIÓN:**: el hecho de gestionar los componentes de {{site.data.keyword.vmwaresolutions_short}}, que se instalaron en la cuenta de {{site.data.keyword.cloud_notm}} al solicitar la instancia, desde fuera de la consola de {{site.data.keyword.vmwaresolutions_short}} podría hacer que el entorno quedara inestable. Estas actividades de gestión incluyen:
*  Añadir, modificar, devolver o eliminar componentes
*  Ampliar o reducir la capacidad de la instancia mediante la adición o eliminación de servidores ESXi
*  Apagar componentes

   Las excepciones a estas actividades incluyen la gestión de comparticiones del archivo de almacenamiento compartido desde el {{site.data.keyword.slportal}}. Estas actividades incluyen: solicitar, suprimir (lo que puede afectar los almacenes de datos si están montados), autorizar y montar comparticiones del archivo de almacenamiento compartido.

### Enlaces relacionados

* [Lista de materiales de software de vCenter Server](vc_bom.html)
* [Requisitos y planificación de instancias de VMware Federal](vc_fed_planning.html)
* [Solicitud de instancias de VMware Federal](vc_fed_orderinginstance.html)
* [Protección de instancias de VMware Federal](vc_fed_securinginstance.html)
* [Cómo ponerse en contacto con el equipo de soporte de IBM](../vmonic/trbl_support.html)
* [Almacenamiento en bloque y de archivos de {{site.data.keyword.cloud_notm}}](https://www.ibm.com/cloud/garage/content/architecture/virtualizationArchitecture/shared-storage){:new_window}
