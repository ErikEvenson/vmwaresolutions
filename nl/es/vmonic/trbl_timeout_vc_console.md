---

copyright:

  years:  2016, 2018

lastupdated: "2018-05-29"

---

# Se supera el tiempo de espera al conectar con el cliente web de VMware vSphere

## Problema
Cuando intenta conectar con el cliente web de vSphere, recibe el siguiente error de tiempo de espera excedido:

`The server at <IP_address> is taking too long to respond. (El servidor de <IP_address> está tardando demasiado en responder).`

## Solución
Siga los pasos siguientes para resolver el problema.

1. Asegúrese de haber seguido los pasos de la ayuda contextual que se muestra cuando mueve el puntero del ratón sobre el botón de la **consola de vCenter**. Por su comodidad, estos pasos también se muestran de la siguiente manera:   
   1. Instale el plug-in Adobe Flash Player para su navegador.   
   2. Cree una contraseña de VPN desde el {{site.data.keyword.slportal_full}}.    
   3. Inicie una sesión en el portal de VPN del centro de datos utilizando las credenciales de VPN de la infraestructura {{site.data.keyword.cloud_notm}}.    
   4. Añada la correlación entre dirección IP y nombre de host de PSC (Platform Services Controller) al archivo hosts con el siguiente formato:

      ```javascript
      IPAddress              HostName
      ```

2. Anote la dirección IP que se muestra, ya que la necesitará en uno de los siguientes pasos.
3. Asegúrese de que tiene acceso a la VPN de la infraestructura {{site.data.keyword.cloud_notm}}. Siga estos pasos en el {{site.data.keyword.slportal}}:
   1. Pulse **Cuenta > Acceso a VPN**.
   2. Pulse **Enlace SSL** en la columna **Acceso a VPN**.
   3. En la página **Acceso a VPN para nombre de usuario**, establezca la opción **Acceso a subred** en **Manual**.
   4. En la misma página, localice la subred correspondiente al par dirección IP/nombre de host. Consulte el **Paso 2** para obtener más información.    

      Por ejemplo, si la dirección IP de la instancia es `xx.yyy.zz.15` y la dirección IP de vCenter es `xx.yyy.zz.10`, debe otorgar acceso para la subred `xx.yyy.zz.0/26`.

   5. Marque el recuadro de selección **Otorgar acceso** para dicha subred y pulse **Guardar**.
