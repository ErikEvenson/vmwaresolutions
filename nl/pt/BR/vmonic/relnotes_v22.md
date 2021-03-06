---

copyright:

  years:  2016, 2018

lastupdated: "2018-05-18"

---

# Notas sobre a liberação para V2.2

Esta liberação inclui novos recursos, atualizações de componentes, aprimoramentos de usabilidade e correções de bug. Para obter uma lista de problemas corrigidos em liberações diferentes, problemas conhecidos com o produto e dicas adicionais para usar o {{site.data.keyword.vmwaresolutions_full}}, veja o [{{site.data.keyword.vmwaresolutions_short}} dW Answers](https://developer.ibm.com/answers/topics/cloudvmw/){:new_window}.

## Correção para Spectre e Meltdown

O {{site.data.keyword.vmwaresolutions_short}} liberou correções do VMware em resposta às vulnerabilidades conhecidas como Spectre e Meltdown (CVE-2017-5753, CVE-2017-5715 e CVE-2017-5754).

* CVEID: [CVE-2017-5753](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5753)
* CVEID: [CVE-2017-5715](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5715)
* CVEID: [CVE-2017-5754](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5754)

Para obter mais informações, veja [Tratando as vulnerabilidades Spectre e Meltdown](../vmonic/trbl_fix_spectre.html).

## Upgrade da máquina virtual do IBM CloudDriver

Durante o processo de upgrade da V2.2, a máquina virtual do IBM CloudDriver é reimplementada com o CentOS Linux liberação 7.4.1708. Além disso, todas as novas instâncias fornecidas incluem o CentOS Linux liberação 7.4.1708 no IBM CloudDriver.

**Importante:**

* Se você estiver usando uma solução de backup que faça referência à máquina virtual do IBM CloudDriver, depois de fazer upgrade para a V2.2, assegure-se de que a solução de backup esteja fazendo referência à nova máquina virtual do IBM CloudDriver.
* Antes de fazer upgrade para a V2.2, assegure-se de substituir o VSI do Legacy Veeam pelo serviço Veeam on {{site.data.keyword.cloud_notm}}. O Legacy Veeam não é mais suportado na V2.2 e liberações futuras, portanto, os backups dos componentes de gerenciamento associados ao Legacy Veeam não estão disponíveis para uma restauração.

Para obter mais informações sobre como usar o serviço Veeam on {{site.data.keyword.cloud_notm}}, veja:
* [Componentes e considerações para o Veeam on {{site.data.keyword.cloud_notm}}](../services/veeam_considerations.html)
* [Gerenciando o Veeam on {{site.data.keyword.cloud_notm}}](../services/managingveeam.html)

## Suporte para o VMware Federal on IBM Cloud

O VMware Federal on {{site.data.keyword.cloud_notm}} fornece suporte para pedir uma instância base do vCenter Server no WDC03 Federal on {{site.data.keyword.CloudDataCent_notm}}. Além de suportar um subconjunto de ofertas da instância vCenter Server, o VMware Federal on {{site.data.keyword.cloud_notm}} fornece às agências do Governo Federal dos EUA a opção de proteger instâncias implementadas do VMware vCenter Server. A seleção da opção para proteger as instâncias implementadas remove as informações confidenciais armazenadas sobre a instância e remove a conexão de gerenciamento aberta para acesso contínuo à instância para funções de gerenciamento, como a inclusão e a remoção de hosts e clusters. Depois de selecionar a opção segura, todas as funções de gerenciamento serão desativadas, exceto uma exclusão total da instância.

Para obter considerações importantes antes de proteger uma instância do VMware Federal, veja [Protegendo instâncias do VMware Federal](../vcenter/vc_fed_securinginstance.html).

(Atualizado em 2 de abril de 2018) Agora, é possível expandir ou contrair a capacidade de sua instância do VMware Federal incluindo ou removendo servidores ESXi. Essa opção está disponível apenas para instâncias do VMware Federal que não foram protegidas.

Para obter mais informações, veja:

* [Visão geral do VMware Federal on {{site.data.keyword.cloud_notm}}](../vcenter/vc_fed_overview.html)
* [Incluindo, visualizando e excluindo clusters para instâncias do VMware Federal](../vcenter/fed_addviewdeleteclusters.html)
* [Expandindo e contraindo a capacidade para instâncias do VMware Federal](../vcenter/vc_fed_addingremovingservers.html)

## Definições de configuração avançadas em servidores ESXi

Para a V2.2 ou liberações mais recentes, novas instâncias são pedidas com um novo conjunto de definições de configuração avançadas para servidores ESXi.
Para instâncias que tiveram upgrade feito de uma liberação anterior para a V2.2 ou liberações mais recentes, algumas configurações requerem a reinicialização dos servidores ESXi, portanto, apenas um subconjunto de definições de configuração é aplicado automaticamente.

Recomenda-se que você mude as definições de configuração restantes para os novos valores para consistência em todas as instâncias e para permitir o suporte adequado para a expansão de armazenamento. A IBM planeja testar apenas com essas novas configurações para todas as liberações futuras do {{site.data.keyword.cloud_notm}} for VMware Solutions.

Para obter mais informações, veja _Definições de configuração avançadas para servidores ESXi_ em:
* [Lista de materiais do vCenter Server](../vcenter/vc_bom.html#advanced-configuration-settings-for-esxi-servers)
* [Lista de materiais do Cloud Foundation](../sddc/sd_bom.html#advanced-configuration-settings-for-esxi-servers)

## Suporte para até 51 servidores ESXi para um cluster inicial e até 59 servidores ESXi para clusters adicionais

Para a V2.2 e liberações mais recentes, é possível aumentar o número de servidores ESXi para um máximo de 51 para um cluster inicial e até 59 para clusters adicionais.

**Importante:** para instâncias implementadas na V2.1 ou liberações anteriores, deve-se ativar o suporte vSAN necessário para aumentar o tamanho do cluster para além de 32. Para obter mais informações e etapas para aumentar o número de servidores ESXi, veja _Quantos servidores ESXi posso incluir em um cluster?_ em [Perguntas mais frequentes sobre servidores ESXi](../vmonic/faq_esxi.html#how-many-esxi-servers-can-i-add-to-a-cluster-).

## Opções adicionais de configuração de rede para instâncias do vCenter Server e do Cloud Foundation

Para pedidos de instâncias do vCenter Server e do Cloud Foundation, você tem a opção de reutilizar VLANs públicas e privadas existentes para sua configuração de rede. Quando as VLANs existentes não estiverem disponíveis, você continua tendo a opção de pedir uma VLAN nova pública e duas VLANs novas privadas.

Para obter considerações importantes antes de selecionar as VLANs existentes, veja a seção *Configurações da interface de rede* em:
* [Pedindo instâncias do vCenter Server](../vcenter/vc_orderinginstance.html)
* [Pedindo instâncias do Cloud Foundation](../sddc/sd_orderinginstance.html)

## Atualizações para instâncias do VMware vCenter Server

### Atualizações da definição de configuração do componente NSX e do grupo da porta

A liberação atual se aplica à atualização do componente VMware NSX for vSphere 6.3.5. Para obter mais informações sobre componentes, veja [Lista de materiais do vCenter Server](../vcenter/vc_bom.html).

Para instâncias do VMware vCenter Server que são implementadas na V2.2 ou liberações mais recentes, as definições de configuração do NSX e do grupo da porta mudaram. Para obter mais informações, veja a seção *Definições de configuração do NSX e do grupo da porta* em [Lista de materiais do vCenter Server Software](../vcenter/vc_bom.html#nsx-and-port-group-configuration-settings).

### Nova opção para configuração do DNS

Agora, você tem a opção de selecionar a implementação de um único VSI (Virtual Server Instance) do Microsoft Windows Server para o Microsoft Active Directory (AD) ou duas máquinas virtuais do Microsoft Windows de alta disponibilidade no cluster de gerenciamento. Para liberações anteriores à V2.2, o único VSI do Microsoft Windows para Microsoft AD foi automaticamente implementado por padrão. A nova opção para selecionar duas máquinas virtuais do Microsoft Windows fornece mais privacidade a e opção para fazer backup e restauração das máquinas virtuais usando o serviço Veeam.

**Nota:** deverão ser fornecidas duas licenças do Microsoft Windows Server 2012 R2 se você configurar sua instância para usar as duas máquinas virtuais do Microsoft Windows. Use a licença da edição Microsoft Windows Server 2012 R2 Standard e/ou a licença da edição Microsoft Windows Server 2012 R2 Datacenter. Você tem 30 dias para ativar as máquinas virtuais.

Para obter mais informações, veja a seção *Configurações do sistema* em [Pedindo instâncias do vCenter Server](../vcenter/vc_orderinginstance.html#system-settings)​.

### Maior número de clusters por instância

É possível incluir até 10 clusters nas instâncias do VMware vCenter Server que são implementadas em ou têm upgrade feito para a V2.2. e liberações mais recentes. Para obter mais informações, veja [Incluindo e visualizando clusters para instâncias do vCenter Server](../vcenter/vc_addingviewingclusters.html)​.

## Atualizações para clusters do VMware vSphere

### Pacotes configuráveis de licença do componente disponíveis para clientes do Parceiro de Negócios

Os usuários do Parceiro de Negócios agora podem selecionar entre quatro pacotes configuráveis de licença do componente ao pedir um novo cluster do vSphere. Escolha entre Padrão com Gerenciamento, Avançado, Avançado com Rede ou Avançado com Rede e Gerenciamento. É possível também incluir componentes adicionais do VMware em seu pedido. No entanto, a opção de Bring Your Own License não está disponível.

Para obter mais informações, veja a seção *Configurações de licenciamento* em [Pedindo novos clusters do vSphere](../vsphere/vs_orderinginstances.html).

## Atualizações para instâncias do NetApp ONTAP Select

A liberação atual se aplica à atualização do NetApp ONTAP Select 9.3.

### Maior número de unidades SATA para Bare Metal Servers do IBM Cloud de alta capacidade

Trinta e quatro unidades SATA estão, agora, disponíveis para o {{site.data.keyword.baremetal_short}} de alta capacidade do NetApp ONTAP Select. Para obter mais informações, veja [Especificações técnicas para instâncias do NetApp ONTAP Select](../netapp/np_netappoverview.html#technical-specifications-for-netapp-ontap-select-instances).

## Atualizações para serviços complementares

### Opção de largura de banda aumentada para o F5 on IBM Cloud

Você tem a opção de selecionar uma largura de banda máxima de 10 Gbps ao instalar o serviço F5 on {{site.data.keyword.cloud_notm}} para instâncias do Cloud Foundation e do vCenter Server. Para obter mais informações, veja [Considerações para o F5 on {{site.data.keyword.cloud_notm}}](../services/f5_considerations.html).

### KMIP for VMware on IBM Cloud

É possível pedir uma instância do Cloud Foundation ou do vCenter Server com o serviço KMIP para VMware on {{site.data.keyword.cloud_notm}} incluído ou incluir o serviço em uma instância existente do Cloud Foundation ou do vCenter Server após a implementação inicial.

Esse serviço fornece um serviço altamente disponível 24x7 para gerenciar chaves de criptografia que são usadas pelo VMware no {{site.data.keyword.cloud_notm}}. Este serviço oferece a capacidade de tempo de execução para permitir que os clientes criem, recuperem, ativem, revoguem e destruam as chaves de criptografia e também fornece a capacidade de gerenciamento para manter as associações entre as credenciais do cliente e essas chaves de criptografia.

Para obter mais informações, veja [Considerações para KMIP para VMware on {{site.data.keyword.cloud_notm}}](../services/kmip_considerations.html).

### IBM Spectrum Protect Plus on IBM Cloud

O serviço IBM Spectrum Protect&trade; Plus on {{site.data.keyword.cloud_notm}} está disponível para instâncias que são implementadas em (ou têm upgrade feito para a) V2.2 ou liberações mais recentes.

Este serviço fornece uma solução eficiente e escalável para proteção de dados, reutilização de dados e recuperação de dados para ambientes virtuais. É possível implementá-lo como uma solução independente ou integrá-lo ao ambiente do IBM Spectrum Protect&trade; Plus para transferir cópias para armazenamento de longo prazo e controle de dados.

O serviço IBM Spectrum Protect Plus on {{site.data.keyword.cloud_notm}} fornece proteção de dados somente para as VMs de carga de trabalho.

Para obter mais informações, veja [Gerenciando o IBM Spectrum Protect Plus on {{site.data.keyword.cloud_notm}}](../services/managingspp.html).

### Serviços gerenciados

Serviços gerenciados para o Veeam on {{site.data.keyword.cloud_notm}} e para o Zerto on {{site.data.keyword.cloud_notm}} estão disponíveis para instâncias do VMware vCenter Server e do VMware Cloud Foundation. Talvez você queira solicitar serviços gerenciados se não desejar gerenciar a complexidade de sua própria solução e ambiente.

O serviço Veeam on {{site.data.keyword.cloud_notm}} se integra continuamente com os hypervisors do VMware para ajudar sua empresa a alcançar alta disponibilidade (HA). Um ambiente de backup totalmente gerenciado pode ser implementado usando o software de backup Veeam e o IBM Resiliency Backup as a Service.

O serviço Zerto on {{site.data.keyword.cloud_notm}} fornece recursos de replicação e de recuperação de desastre, que podem ser integrados às ofertas de implementação para proteger e recuperar dados no ambiente virtual do VMware no {{site.data.keyword.cloud_notm}}. Um ambiente de recuperação de desastre (DR) totalmente gerenciado pode ser implementado usando o software Zerto DR e o IBM Resiliency Services.

É possível solicitar serviços gerenciados para suas instâncias da página **Introdução**, seja colocando um novo pedido da instância ou incluindo o serviço em uma instância existente.

Para obter mais informações, veja:
* [Solicitando serviços para o Veeam on {{site.data.keyword.cloud_notm}}](../services/managing_veeam_services.html)
* [Solicitando serviços para o Zerto on {{site.data.keyword.cloud_notm}}](../services/managing_zerto_services.html)

## Documentação nova e atualizada

* A tabela de comparação com as funções suportadas para instâncias do Cloud Foundation e do vCenter Server, bem como clusters do VMware vSphere, está disponível na documentação. É possível ver, em uma visão rápida, as diferenças entre as funções que cada tipo de instância fornece. Para obter mais informações, veja [Gráfico de comparação de oferta](../vmonic/inst_comp_chart.html).

* As VLANs e a Lista de Materiais (BOM) de software são fornecidas na documentação para instâncias do Cloud Foundation e do vCenter Server, bem como clusters do VMware vSphere.

  Para obter mais informações, veja:

  * [Lista de materiais do vCenter Server](../vcenter/vc_bom.html)
  * [Lista de materiais do Cloud Foundation](../sddc/sd_bom.html)
  * [Lista de materiais do VMware vSphere](../vsphere/vs_bom.html)

## Atualizações e aprimoramentos da interface com o usuário

São feitas melhorias em toda a interface com o usuário:

* Quando você pede uma instância, todas as opções de hardware são filtradas por local e as opções indisponíveis são exibidas no estado desativado.
* A configuração do **{{site.data.keyword.baremetal_short}}** é preenchida automaticamente quando você pede um cluster do vSphere com base nas configurações existentes. É possível atualizar a configuração de acordo com seus requisitos.
* Várias mensagens de erro e aprimoramentos de dica de ferramenta foram feitos para ajudá-lo na seleção da configuração apropriada na interface com o usuário.
