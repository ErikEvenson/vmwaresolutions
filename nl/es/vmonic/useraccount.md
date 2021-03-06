---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-27"

---

# Gestión de cuentas y valores de usuario

{{site.data.keyword.vmwaresolutions_full}} se comunica con la infraestructura de {{site.data.keyword.cloud_notm}} mediante llamadas de {{site.data.keyword.slapi_short}}. Para acceder a la {{site.data.keyword.slapi_short}} de forma segura, debe enlazar las credenciales de su cuenta de infraestructura de {{site.data.keyword.cloud_notm}} (SoftLayer) a su cuenta de {{site.data.keyword.cloud_notm}}.

**Nota**: La cuenta de infraestructura de {{site.data.keyword.cloud_notm}} (SoftLayer) se conocía anteriormente como la cuenta de IBM SoftLayer.

También puede especificar si desea recibir notificaciones por correo electrónico y por consola sobre diversos sucesos.

## Antes de empezar

* Solo puede enlazar una cuenta de infraestructura de {{site.data.keyword.cloud_notm}} (SoftLayer) a una cuenta de usuario de {{site.data.keyword.cloud_notm}}.
* La cuenta de infraestructura de {{site.data.keyword.cloud_notm}} (SoftLayer) que está utilizando debe cumplir determinados requisitos. Para obtener más información, consulte [Requisitos de cuenta de infraestructura de {{site.data.keyword.cloud_notm}}](slaccountrequirement.html).
* Si la clave de API para su cuenta de infraestructura de {{site.data.keyword.cloud_notm}} (SoftLayer) cambia, debe actualizar la clave en la página **Valores** de la consola de {{site.data.keyword.vmwaresolutions_short}}.

   **Importante**: es su responsabilidad asegurarse de que la clave de API que se guarda en la página **Configuración** es correcta y está actualizada.
   De lo contrario, las operaciones que requieren la validación de clave de API podrían fallar.

## Procedimiento

1. En la consola de {{site.data.keyword.vmwaresolutions_short}}, pulse **Valores** en el panel de navegación de la izquierda.
2. En el área **Notificaciones**, especifique los valores de notificación:
   * Si desea recibir una notificación por correo electrónico cuando se produzcan sucesos, pulse **Habilitar notificaciones por correo electrónico**.
   * Si desea recibir una notificación en la consola cuando se produzcan sucesos, pulse **Habilitar notificaciones de consola**.
3. En el área **Credenciales de infraestructura de IBM Cloud**, escriba el nombre de usuario y la clave de API de la cuenta de infraestructura de {{site.data.keyword.cloud_notm}} (SoftLayer) utilizando uno de los métodos siguientes:
   * Si la cuenta de infraestructura de {{site.data.keyword.cloud_notm}} (SoftLayer) y la cuenta de {{site.data.keyword.cloud_notm}} están enlazadas, pulse **Recuperar** para especificar las credenciales automáticamente.
   * Si la cuenta de infraestructura de {{site.data.keyword.cloud_notm}} (SoftLayer) y la cuenta de {{site.data.keyword.cloud_notm}} no están enlazadas, inicie sesión en el [portal de clientes de infraestructura de {{site.data.keyword.cloud_notm}}](https://control.softlayer.com/) y, a continuación, siga las instrucciones de la consola para obtener y especificar las credenciales.
   * Si no tiene una cuenta de infraestructura de {{site.data.keyword.cloud_notm}} (SoftLayer), [regístrese en una](../vmonic/signing_softlayer_account.html) y, a continuación, siga las instrucciones de la consola para obtener y especificar las credenciales.
4. Pulse **Guardar credenciales**.

## Resultados

Después de enlazar la cuenta de {{site.data.keyword.cloud_notm}} y la cuenta de infraestructura de {{site.data.keyword.cloud_notm}} (SoftLayer), la consola recupera automáticamente las credenciales de la cuenta de infraestructura de {{site.data.keyword.cloud_notm}} (SoftLayer) para comunicarse con el entorno de VMware en {{site.data.keyword.cloud_notm}}.

Las credenciales de la cuenta de infraestructura de {{site.data.keyword.cloud_notm}} (SoftLayer) almacenadas se utilizan en operaciones futuras que requieren interacción con la infraestructura de {{site.data.keyword.cloud_notm}}.

Si las notificaciones por correo electrónico o en la consola están habilitadas para determinados sucesos de la instancia, se le notificará por correo electrónico o mediante mensajes en la consola cuando se produzcan dichos sucesos.

### Enlaces relacionados

* [Preguntas frecuentes](faq.html)
* [Pedido de instancias de Cloud Foundation](../sddc/sd_orderinginstance.html)
* [Pedido de instancias de vCenter Server](../vcenter/vc_orderinginstance.html)
* [Notificaciones](notifications.html)
* [API de SoftLayer](../../../customer-portal/cpapi.html){:new_window}
