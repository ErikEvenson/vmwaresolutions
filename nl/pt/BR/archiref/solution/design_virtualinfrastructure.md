---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-17"

---

# Design de infraestrutura virtual

A camada de infraestrutura virtual inclui os componentes de software do VMware que virtualizam os recursos de cálculo, armazenamento e rede fornecidos na camada de infraestrutura física: VMware vSphere ESXi, VMware NSX e, opcionalmente, VMware vSAN.

## Design do VMware vSphere

A configuração do vSphere ESXi consiste nos aspectos a seguir:
* Configuração de inicialização
* Sincronização de
* Acesso ao host
* Acesso de usuário
* Configuração de DNS

A Tabela 1 descreve as especificações para cada aspecto. Após a configuração e instalação do ESXi, o host é incluído em um VMware vCenter Server e é gerenciado de lá.

O design permite acessar os hosts virtuais por meio do Direct Console User Interface (DCUI), do Shell ESXi e do Shell Seguro (SSH).

Por padrão, os únicos usuários que podem efetuar login diretamente são os usuários _raiz_ e _ibmvmadmin_ para a máquina física do host. O administrador pode incluir usuários finais por meio do domínio do Microsoft Active Directory (MSAD) para permitir acesso de usuário ao host. Todos os hosts no design de solução do vCenter Server são configurados para sincronizar com um servidor NTP central.

Tabela 1. Configuração do vSphere ESXi

| Atributo              | Parâmetro de configuração |
|:---------------------- |:----------------------- |
| Local de inicialização ESXi     | Usa discos locais configurados no RAID-1 |
| Sincronização de   | Usa  {{site.data.keyword.cloud}}  Servidor NTP |
| Acesso ao host            | Suporta DCUI, Shell ESXi ou SSH |
| Acesso de usuário            | Autenticação Local e MSAD |
| Resolução do nome de domínio | Usa o DNS conforme descrito em [Design de serviços comuns](design_commonservice.html) |

O cluster do vSphere hospeda as máquinas virtuais (VMs) que gerenciam a nuvem central, bem como recursos de cálculo para cargas de trabalho do usuário.

Para instâncias do Cloud Foundation:
* Uma instância contém 4 hosts ESXi na implementação inicial.
* Após a implementação, é possível escalar a instância até um máximo de 32 hosts ESXi.

Para instâncias do vCenter Server:
* Quando uma instância usa somente NFS, o número mínimo de hosts ESXi na implementação inicial é 2, mas 3 é recomendado para HA. É possível escalar até um máximo de 59 hosts ESXi durante ou após a implementação inicial.
* Quando uma instância usa vSAN, o número mínimo de hosts ESXi na implementação inicial é 4. É possível escalar até um máximo de 59 hosts ESXi durante ou após a implementação inicial.

Para suportar mais cargas de trabalho do usuário, é possível escalar o ambiente da seguinte forma:  
* Implementando hosts de cálculo adicionais de clusters existentes
* Implementando clusters adicionais gerenciados pelo mesmo vCenter Server Appliance
* Implementando novas instâncias do vCenter Server ou do Cloud Foundation com seu próprio vCenter Server Appliance.

Para obter mais informações sobre clusters, veja [o documento	{{site.data.keyword.cloud_notm}} executando a arquitetura de solução
VMware Clusters](https://www.ibm.com/cloud/garage/files/IBM-Cloud-for-VMware-Solutions-Multicluster-Architecture.pdf).

## Design do VMware vSAN

Nesse design, o armazenamento do VMware vSAN é empregado em instâncias do Cloud Foundation e, opcionalmente, em instâncias do vCenter Server para fornecer armazenamento compartilhado para os hosts do vSphere.

Conforme mostrado na Figura 1, o vSAN agrega o armazenamento local em múltiplos hosts ESXi dentro de um cluster do vSphere e gerencia o armazenamento agregado como um único armazenamento de dados da VM. Dentro desse design, os nós de cálculo contêm unidades de disco locais para o S.O. ESXi e o armazenamento de dados vSAN. Independentemente de a qual cluster um nó pertence,
duas unidades SATA de 1 TB estão incluídas em cada nó para hospedar a instalação do ESXi.

Figura 1. Conceito vSAN

![Conceito do vSAN](virtual_vSAN.svg "O vSAN agrega o armazenamento local em múltiplos hosts ESXi dentro de um cluster do vSphere e gerencia o armazenamento agregado como um único armazenamento de dados da VM")

O vSAN emprega os componentes a seguir:
* O design do vSAN de grupo de dois discos, com cada grupo de disco consistindo em dois ou mais discos. Um SSD do menor tamanho no grupo serve como a camada de cache e os SSDs restantes servem como a camada de capacidade.
* O controlador RAID integrado é configurado para cada unidade, exceto para as duas unidades de S.O., no nível do RAID-0.
* Um único armazenamento de dados do vSAN é criado a partir de todo o armazenamento.

Os recursos disponíveis do vSAN dependem da edição de licença que você seleciona ao pedir a instância. Para obter mais informações, veja [Comparação de edição do VMware vSAN](appendix.html#vmware-vsan-edition-comparison).

### Configuração de rede virtual para vSAN

Para esse design, o tráfego do vSAN atravessa entre hosts ESXi em uma VLAN privada dedicada. Os dois adaptadores de rede conectados ao comutador de rede privada são configurados no vSphere como um vSphere Distributed Switch (VDS) com ambos os adaptadores de rede como uplinks. Um grupo de portas do kernel do vSAN dedicado configurado para a VLAN vSAN reside dentro do VDS. Os quadros gigantes (MTU 9000) são ativados para o VDS privado.

O vSAN não carrega o tráfego de balanceamento entre uplinks. Como resultado, um adaptador está ativo enquanto o outro está em espera para suportar a alta disponibilidade (HA). A política de failover de rede para vSAN é configurada como **Failover explícito** entre portas de rede física.

Para obter mais informações sobre conexões NIC físicas, veja a Figura 2. Conexões NIC físicas do host em [Design de infraestrutura física](design_physicalinfrastructure.html).

### Design de política de armazenamento

Quando o vSAN está ativado e configurado, as políticas de armazenamento são configuradas para definir as características de armazenamento da VM. As características de armazenamento especificam níveis diferentes de serviço para VMs diferentes.

A política de armazenamento padrão nesse design tolera uma única falha. A política padrão é configurada com a codificação de apagamento do RAID 5, com o **Método de tolerância a falhas** configurado como **RAID-5/6 (codificação de apagamento) - Capacidade** e **Nível primário de falhas** configurado como 1.

A configuração do RAID 5 requer um mínimo de quatro hosts. Como alternativa, é possível escolher a configuração do RAID 6 com o **Método de tolerância a falhas** configurado como **RAID-5/6 (codificação de apagamento) - Capacidade** e **Nível primário de falhas** configurado como 2.

A configuração do RAID 6 requer um mínimo de 6 hosts. A **Duplicação** e a **Compactação** também são ativadas na política de armazenamento padrão.

Uma instância usa a política padrão, a menos que especificado de outra forma por meio do console do vSphere. Quando uma política customizada for configurada, o vSAN garantirá isso quando possível. No entanto, se a política não puder ser garantida, não será possível provisionar uma VM que usa a política, a menos que ela esteja ativada para forçar o fornecimento.

As políticas de armazenamento devem ser reaplicadas após a inclusão de novos hosts ESXi ou correção dos hosts ESXi.

### Configurações do vSAN

As configurações do vSAN são definidas com base nas melhores práticas para implementar soluções do VMware no {{site.data.keyword.cloud_notm}}. Isso inclui configurações de SIOC, grupo de portas de configurações de failover explícito e configurações de cache de disco.
* Configurações de política de cache de SSD: No **Read Ahead**, **Write Through**, **Direct** (NRWTD)
* Configurações de controle de E/S de rede
   * Gerenciamento: 20 compartilhamentos
   * Máquina Virtual: 30 compartilhamentos
   * vMotion: 50 compartilhamentos
   * vSAN: 100 compartilhamentos
* Portas do kernel vSAN:  ** Failover Explícito **

## Design do VMware NSX

A virtualização de rede fornece uma sobreposição de rede que existe dentro da camada virtual. Isso fornece a arquitetura com recursos, como fornecimento rápido, implementação, reconfiguração e destruição de redes virtuais sob demanda. Esse design usa o vSphere Distributed Switch (vDS) e o VMware NSX for vSphere para implementar a rede virtual.

Nesse design, o NSX Manager é implementado no cluster inicial. O NSX Manager é designado a um endereço IP suportado pela VLAN do bloco de endereço móvel privado, que é designado para componentes de gerenciamento e configurado com os servidores DNS e NTP discutidos em [Design de serviços comuns](design_commonservice.html). O NSX Manager é instalado com as especificações listadas na Tabela 2.

Tabela 2. Atributos do NSX Manager

| Atributo       | Especificação |
|:--------------- |:------------- |
| Gerenciador NSX     | Dispositivo Virtual |
| Número de vCPUs | 4 |
| Memória          | 16 GB |
| Disco            | 60 GB no compartilhamento do NFS de gerenciamento |
| Tipo de Disco       | Thin-provisioned |
| Rede         | Móvel Privada A designada para componentes de gerenciamento |

A figura a seguir mostra o posicionamento do NSX Manager em relação a outros componentes na arquitetura.

Figura 2. Visão geral da rede do NSX Manager

![Visão geral de rede do NSX Manager](virtual_NSX.svg "NSX Manager em relação aos outros componentes na arquitetura")

Após a implementação inicial, a automação do {{site.data.keyword.cloud_notm}} implementa três NSX Controllers dentro do cluster inicial. Cada um dos controladores é designado a um endereço IP suportado pela VLAN da sub-rede móvel Privada A que é designada para componentes de gerenciamento. Além disso, o design cria regras de antiafinidade VM-VM para separar os controladores entre os hosts no cluster. O cluster inicial deve conter um mínimo de três nós para assegurar alta disponibilidade para os controladores.

Além dos controladores, a automação do {{site.data.keyword.cloud_notm}} prepara os hosts vSphere implementados com o NSX VIBS para permitir o uso de uma rede virtualizada por meio de VXLAN Tunnel Endpoints (VTEPs). Os VTEPs são designados a um endereço IP suportado pela VLAN do intervalo de endereço IP móvel Privado A que é especificado para VTEPs conforme listado em [Resumo de VLAN e sub-rede](design_physicalinfrastructure.html#table_vlan_subnet_summary). O tráfego VXLAN reside na VLAN não identificada e é designado ao vSphere Distributed Switch (VDS) privado.

Subsequentemente, um conjunto de IDs de segmento é designado e os hosts no cluster são incluídos na zona de transporte. Somente unicast é usado na zona de transporte porque o rastreamento do Internet Group Management Protocol (IGMP) não está configurado dentro do {{site.data.keyword.cloud_notm}}.

Depois disso, os pares do NSX Edge Services Gateway são implementados. Em todos os casos, um par de gateways é usado para o tráfego de saída dos componentes de automação que residem na rede privada. Para o vCenter Server, um segundo gateway, conhecido como borda gerenciada pelo cliente, é implementado e configurado com um uplink para a rede pública e uma interface designada à rede privada. Para obter mais informações sobre os NSX Edge Services Gateways que são implementados como parte da solução, veja [Arquitetura da solução NSX Edge no {{site.data.keyword.cloud_notm}}](https://www.ibm.com/cloud/garage/files/IBM_Cloud_for_VMware_Solutions_NSX_Edge_Services_Gateway.pdf).

Os administradores em nuvem podem configurar quaisquer componentes NSX necessários, como o Distributed Logical Router (DLR), os comutadores lógicos e os firewalls. Os recursos do NSX disponíveis dependem da edição de licença do NSX que você escolher ao pedir a instância. Para obter mais informações, veja [Comparação de edição do VMware NSX Edition](appendix.html#vmware-nsx-edition-comparison). Para instâncias do vCenter Server, a automação do {{site.data.keyword.cloud_notm}} inclui o vCenter Server Appliance e o Platform Services Controller (PSC) na lista de exclusão de firewall distribuído do NSX Manager.

### Design do comutador distribuído

O design usa um número mínimo de vSphere Distributed Switches (VDS). Os hosts no cluster são conectados às redes pública e privada. Os hosts são configurados com dois comutadores virtuais distribuídos. O uso de dois comutadores segue a prática de rede do {{site.data.keyword.cloud_notm}} que separa as redes pública e privada. O diagrama a seguir mostra o design do VDS.

Figura 3. Design do comutador distribuído

![Distributed Switch Design](virtual_network_distributedswitch.svg "VDS design")

Conforme mostrado na figura, um VDS é configurado para conectividade de rede pública (SDDC-Dswitch-Public) e o outro VDS é configurado para conectividade de rede privada (SDDC-Dswitch-Private).

A separação de diferentes tipos de tráfego é necessária para reduzir a contenção e a latência e aumentar a segurança. As VLANs são usadas para segmentar funções de rede física.

Esse design usa três VLANs: duas para tráfego de rede privada e uma para tráfego de rede pública. A tabela a seguir mostra a separação de tráfego.

Tabela 3. Mapeamento de VLAN para tipos de tráfego

| VLAN  | Designação | Tipo de Tráfego |
|:----- |:----------- |:------------ |
| VLAN1 | Público      | Disponível para acesso à Internet |
| VLAN2 | Privado A   | Gerenciamento do ESXi, Gerenciamento, VXLAN (VTEP) |
| VLAN3 | Privado B   | vSAN, NFS, vMotion |

O tráfego de cargas de trabalho circulará em comutadores lógicos suportados pelo VXLAN.

O cluster do vSphere usa dois comutadores distribuídos vSphere configurados como nas tabelas a seguir. 

Tabela 4. Comutadores distribuídos de cluster convergido

| vSphere Distributed<br>Nome do comutador | Função | Rede<br>Controle de E/S | Balanceamento de Car<br>Modo | NIC Físico<br>Portas | MTU |
|:------------- |:------------- |:------------- |:------------- |:------------- |:------------- |
| SDDC-Dswitch-Privado | Gerenciamento do ESXi, SAN Virtual, vSphere vMotion, VXLAN Tunnel Endpoint, NFS (VTEP) | Ativado | Rota baseada na porta virtual de origem de failover explícito (vSAN, vMotion) (todos os outros) | 2 | 9.000<br>(Quadros gigantes) |
| SDDC-Dswitch-Public | Tráfego de gerenciamento externo (North-Sul) | Ativado | Rota Baseada na Porta Virtual de Origem | 2 | 1.500<br>(padrão) |

**Nota:** os nomes, o número e a ordenação dos NICs do host podem variar dependendo do {{site.data.keyword.CloudDataCent_notm}} e da seleção de hardware do host.

Tabela 5. Definições de configuração de grupo de portas do comutador distribuído de cluster convergido

| Parâmetro          | Configuração       |
|:------------------ |:------------- |
| Balanceamento de     | Rota baseada na porta virtual de origem \* |
| Detecção de Failover | Somente status do link |
| Notificar comutadores        | Ativado |
| Failback           | Não |
| Ordem de Failover     | Uplinks ativos: Uplink1, Uplink2 \* |

\* **Nota**: o grupo de portas do vSAN usa o failover explícito com ativo/espera, uma vez que ele não suporta balanceamento de carga de tráfego de armazenamento vSAN.

Tabela 6. Grupos de portas do comutador virtual de cluster convergido e VLANs

| Comutador Distribuído do vSphere | Nome do Grupo da Porta | Equipe | Uplinks | ID de VLAN |
|:------------- |:------------- |:------------- |:------------- |:---------- |
| SDDC-Dswitch-Privado | SDDC-DPortGroup-Mgmt | Porta virtual de origem | Ativo: 0, 1 | VLAN1 |
| SDDC-Dswitch-Privado | SDDC-DPortGroup-vMotion | Porta virtual de origem | Ativo: 0, 1 | VLAN2 |
| SDDC-Dswitch-Privado | SDDC-DPortGroup-VSAN | Failover explícito | Ativo: 0<br>Standby: 1 | VLAN2 |
| SDDC-Dswitch-Privado | SDDC-DPortGroup-NFS | Porta virtual de origem | Ativo: 0, 1 | VLAN2 |
| SDDC-Dswitch-Privado | Gerado Automaticamente pelo NSX | Porta virtual de origem | Ativo: 0, 1 | VLAN1 |
| SDDC-Dswitch-Public | SDDC-DPortGroup-External | Porta virtual de origem | Ativo: 0, 1 | VLAN3 |

Tabela 7. Adaptadores de kernel da VM de cluster convergido

| Comutador Distribuído do vSphere | Purpose | Grupo de Portas Conectado | Serviços Ativados | MTU |
|:-------------------------- |:------- |:-------------------- |:---------------- |:--- |
| SDDC-Dswitch-Privado | Gerenciamento | SDDC-DPortGroup-Mgmt | Tráfego de Gerenciamento | 1.500<br>(padrão) |
| SDDC-Dswitch-Privado | vMotion | SDDC-DPortGroup-vMotion | Tráfego de vMotion | 9.000 |
| SDDC-Dswitch-Privado | VTEP | *Gerado automaticamente pelo NSX* | \- | 9.000 |
| SDDC-Dswitch-Privado | VSAN | SDDC-DPortGroup-VSAN | VSAN | 9.000 |
| SDDC-Dswitch-Privado | NAS | SDDC-DPortGroup-NFS | \-  | 9.000 |

### Configuração do NSX

Esse design especifica a configuração de componentes NSX, mas não aplica nenhuma configuração de componente de sobreposição de rede. É possível projetar a sobreposição de rede com base em suas necessidades. Os aspectos a seguir são pré-configurados:

* Os servidores de gerenciamento e controladores são instalados e integrados à IU da web do vCenter
* Os agentes ESXi são instalados e os endereços IP do VTEP são configurados por host ESXi
* Configuração do VTEP, configuração do controlador e configuração de VXLAN (zona de transporte)
* Dispositivos NSX Edge Services Gateway para uso por componentes de gerenciamento
* Somente para instâncias do vCenter Server: dispositivos NSX Edge Services Gateway para uso do cliente

Os aspectos a seguir não estão configurados:
* Roteadores distribuídos virtuais
* Micro segmentação
* VXLANs
* Gerenciamento do NSX vinculado para outras instâncias do VMware

### Links relacionados

* [ {{site.data.keyword.cloud_notm}}  executando a arquitetura de solução de Clusters do VMware ](https://www.ibm.com/cloud/garage/files/IBM-Cloud-for-VMware-Solutions-Multicluster-Architecture.pdf)
* [ NSX Edge na  {{site.data.keyword.cloud_notm}}  arquitetura da solução ](https://www.ibm.com/cloud/garage/files/IBM_Cloud_for_VMware_Solutions_NSX_Edge_Services_Gateway.pdf)
