---

copyright:

  years:  2016, 2018

lastupdated: "2017-07-19"

---

# Supresión de las instancias de vCenter Server con el paquete híbrido (Hybridity) en una configuración de varios sitios

Existen consideraciones especiales a tener en cuenta antes de suprimir instancias de VMware vCenter Server on {{site.data.keyword.cloud}} con el paquete híbrido (Hybridity) que forman parte de una configuración de varios sitios.

Cuando suprima una instancia de vCenter Server con el paquete híbrido (Hybridity), los siguientes componentes se liberarán en esta secuencia:
1. Todos los servicios desplegados
2. Cuota de soporte y servicios
3. Licencias del producto VMware
4. Servidores ESXi
5. Subredes
6. VLAN

Debido a las dependencias entre recursos, los componentes de la instancia no se liberan inmediatamente cuando se suprime la instancia. Por ejemplo, las subredes y las VLAN no se pueden suprimir hasta que la infraestructura de {{site.data.keyword.cloud_notm}} haya reclamado por completo los servidores ESXi, lo cual sucede al final del ciclo de facturación de la infraestructura de {{site.data.keyword.cloud_notm}}. Al final del ciclo de facturación de la infraestructura de {{site.data.keyword.cloud_notm}}, que suele ser de 30 días, se suprimen las subredes y las VLAN y se completa la supresión de la instancia.

**Atención**: se le facturará por la instancia suprimida hasta el final del ciclo de facturación de la infraestructura de {{site.data.keyword.cloud_notm}}.

## Procedimiento

1. Elimine todos los servicios desde la instancia secundaria de vCenter Server con el paquete híbrido (Hybridity).
2. Asegúrese de que no tiene ningún objeto NSX ampliado en la instancia secundaria que desea suprimir.
3. Suprima el vCenter secundario y el PSC (Platform Services Controller) del dominio SSO (inicio de sesión único) primario. Para obtener más información, consulte [Eliminación del registro de vCenter Server de un inicio de sesión único](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2106736){:new_window}.
4. Disminuya el nivel de la VSI (instancia de servicio virtual) del controlador de dominio local. Para obtener más información, consulte [Disminución del nivel de controladores de dominio y de dominios](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-ds/deploy/demoting-domain-controllers-and-domains--level-200-){:new_window}.
5. Suprima la instancia secundaria de vCenter Server con el paquete híbrido (Hybridity) desde la consola de {{site.data.keyword.vmwaresolutions_short}}.
6. Repita los pasos 1 a 5 para todas las instancias secundarias de vCenter Server con el paquete híbrido (Hybridity) de la configuración de varios sitios.
7. Después de suprimir todas las instancias secundarias, también puede suprimir la instancia primaria desde la consola de {{site.data.keyword.vmwaresolutions_short}}.

### Enlaces relacionados

* [Supresión de instancias de vCenter Server con el paquete híbrido (Hybridity)](vc_hybrid_deletinginstance.html)
* [Solicitud, visualización y eliminación de servicios desde instancias de vCenter Server con el paquete híbrido (Hybridity)](vc_hybrid_addingremovingservices.html)
