---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-20"

---

# Pedindo instâncias do VMware Federal

Para implementar uma plataforma virtualizada VMware flexível e customizável que melhor se ajuste às suas necessidades de carga de trabalho, peça uma instância do VMware Federal que permite desconectar a conexão de gerenciamento aberta e proteger a instância implementada.

**Nota:** apenas as instâncias do vCenter Server suportam o VMware Federal on {{site.data.keyword.cloud}} neste momento.

## Requisitos

Assegure-se de que tenha concluído as tarefas a seguir:
* Você configurou as credenciais de infraestrutura do {{site.data.keyword.cloud_notm}} na página **Configurações**. Para obter mais informações, veja [Gerenciando contas de usuários e configurações](../vmonic/useraccount.html).
* Você revisou as informações em [Requisitos e planejamento para instâncias do VMware
Federal](vc_fed_planning.html).
* Você revisou o formato de nome da instância e do domínio. O nome do domínio e o rótulo do subdomínio são usados para gerar o nome do usuário e os nomes do servidor da instância.

Tabela 1. Formato de valor para nomes de instância e de domínio

| Nome        | Formato do valor      |
  |:------------- |:------------- |
  | Nome de domínio | `<root_domain>` |  
  | Nome do usuário de login do vCenter Server | `<user_id>@<root_domain>` (Usuário do Microsoft Active Directory) ou `administrator@vsphere.local` |
  | FQDN do vCenter Server | `vcenter.<subdomain_label>.<root_domain>`. O comprimento máximo é de 50 caracteres. |
  | Nome do site de Conexão única (SSO) | `<subdomain_label>` |
  | Nome do servidor ESXi totalmente qualificado | `<host_prefix><n>.<subdomain_label>.<root_domain>`, em que `<n>` é a sequência do servidor ESXi. O comprimento máximo é de 50 caracteres. |  
  | FQDN do PSC | `psc-<subdomain_label>.<subdomain_label>.<root_domain>`. O comprimento máximo é de 50 caracteres. |

**Importante**: não modifique quaisquer valores que são configurados durante o pedido e a implementação da instância. Isso pode fazer com que a instância se torne inutilizável. Por exemplo, a rede pública pode ser encerrada, os servidores e Virtual Server Instances (VSIs) podem mover-se atrás de um Vyatta quando a provisão está em andamento, ou o IBM CloudBuilder VSI pode ser parado ou ser excluído.

## Configurações do sistema

Deve-se especificar as configurações do sistema a seguir ao pedir uma instância do VMware Federal.

### Nome da instância

O nome da instância deve atender aos requisitos a seguir:
* Apenas caracteres alfanuméricos e o traço (-) são permitidos.
* O nome da instância deve iniciar e terminar com um caractere alfanumérico.
* O comprimento máximo do nome da instância é de 10 caracteres.
* O nome da instância deve ser exclusivo dentro de sua conta.

### Principal ou secundário

Solicite uma nova instância primária. A implementação de uma instância secundária para alta disponibilidade não é suportada neste momento.

## Configurações de licenciamento

Licenças do VMware fornecidas pela IBM para o seguinte:

* VMware vCenter Server 6.5
* VMware vSphere Enterprise Plus 6.5u1
* VMware NSX Service Providers Edition (Base, Advanced ou Enterprise) 6.4
* (Para clusters do vSAN) VMware vSAN Advanced ou Enterprise 6.6

**Atenção:**

* As edições de licença mínimas são indicadas na interface com o usuário. Se diferentes edições de componentes forem suportadas, será possível selecionar a edição desejada. Você é responsável por assegurar que a chave de licença fornecida está correta para cada componente de VMware selecionado.
* Para o vSphere, um encargo de licença incorrerá no momento do pedido, mas esse encargo será creditado subsequentemente em sua conta.

## Configurações do Bare Metal Server

As configurações de Bare Metal são baseadas em sua configuração customizada. A opção para selecionar uma configuração pré-configurada não é suportada neste momento.

### Local do datacenter

Selecione o {{site.data.keyword.CloudDataCent_notm}} no qual a instância deve ser hospedada.

### Customizado

Especifique o modelo de CPU e RAM para o Bare Metal Server.

Tabela 2. Opções para {{site.data.keyword.baremetal_short}} customizados

| Opções de CPU        | Opções de RAM       |
|:------------- |:------------- |
| Dual Intel Xeon E5-2620 v4/total de 16 núcleos, 2.1 GHz | 64 GB, 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Dual Intel Xeon E5-2650 v4/total de 24 núcleos, 2.2 GHz | 64 GB, 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Dual Intel Xeon E5-2690 v4/total de 28 núcleos, 2.6 GHz | 64 GB, 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Processador Dual Intel Xeon Silver 4110/total de 16 núcleos, 2,1 GHz | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |
| Processador Dual Intel Xeon Gold 5120/total de 28 núcleos, 2,2 GHz | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |
| Processador Dual Intel Xeon Gold 6140/Total de 36 núcleos, 2,3 GHz | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |

### Número de Bare Metal Servers

É possível configurar o número de servidores ESXi no intervalo de 2 a 20.

Todos os servidores ESXi compartilham a mesma configuração. Na pós-implementação, é possível incluir mais quatro clusters. Para configurações de armazenamento vSAN, 4 servidores ESXi são necessários para os clusters iniciais e pós-implementação. Para obter mais informações sobre o mínimo de servidores ESXi, veja [Uma instância do vCenter Server com dois nós é altamente disponível?](../vmonic/faq.html#is-a-two-node-vcenter-server-instance-highly-available-)

## Configurações de armazenamento

As configurações de armazenamento são baseadas em sua seleção de configuração do Bare Metal Server e o tipo de armazenamento.

### Armazenamento vSAN

Para vSAN, especifique as opções de armazenamento a seguir:

* **Tipo e tamanho do disco para discos de capacidade vSAN**: selecione a capacidade que atenda às suas necessidades de armazenamento compartilhado.
* **Número de discos de capacidade vSAN**: selecione o número de discos para o armazenamento compartilhado vSAN que você deseja incluir. As quantidades de disco devem ser 2, 4, 6 ou 8.
* Selecione a edição de licença VMware vSAN 6.6 (Avançada ou Corporativa).

### Armazenamento NFS

Quando você selecionar **Armazenamento do NFS**, será possível incluir armazenamento compartilhado no nível de arquivo para a sua instância na qual todas as ações usam as mesmas configurações ou será possível especificar definições de configuração diferentes para cada compartilhamento de arquivo. Especifique as seguintes opções NFS:

**Nota:** o número de compartilhamentos de arquivos deve estar no intervalo de 1 a 32.

* **Configurar compartilhamentos individualmente**: selecione para especificar
diferentes definições de configuração para cada compartilhamento de arquivo.
* **Número de compartilhamentos**: ao usar a mesma definição de configuração para cada compartilhamento de arquivo, especifique o número de compartilhamentos de arquivos para o armazenamento compartilhado do NFS que você deseja incluir.
* **Tamanho**: selecione a capacidade que atenda às suas necessidades de armazenamento compartilhado.
* **Desempenho**: selecione o IOPS (Input/output Operations Per Second) por GB com base em seus requisitos de carga de trabalho.
* **ADD NFS**: selecione para incluir compartilhamentos de arquivos individuais que usam definições de configuração diferentes.

Tabela 3. Opções de nível de desempenho do NFS

| Opção        | Detalhes       |
  |:------------- |:------------- |
  | 2 IOPS/GB | Esta opção foi projetada para a maioria de cargas de trabalho de propósito geral. Os aplicativos de exemplo incluem: hospedagem de bancos de dados pequenos, backup de aplicativos da web ou imagens de disco da máquina virtual para um hypervisor. |
  | 4 IOPS/GB | Esta opção foi projetada para cargas de trabalho de maior intensidade que possuem uma alta porcentagem de dados ativos de cada vez. Os aplicativos de exemplo incluem: bancos de dados transacionais. |
  | 10 IOPS/GB | Esta opção foi projetada para os tipos de carga de trabalho mais exigentes, como analítica. Os aplicativos de exemplo incluem: bancos de dados de alta transação e outros bancos de dados sensíveis ao desempenho. Esse nível de desempenho é limitado a uma capacidade máxima de 4 TB por compartilhamento de arquivo. |

## Configurações da interface de rede

### Prefixo de nome do host

O prefixo de nome do host deve atender aos requisitos a seguir:
*  Apenas caracteres alfanuméricos e o traço (-) são permitidos.
*  O prefixo de nome do host deve iniciar e terminar com um caractere alfanumérico.
*  O comprimento máximo do prefixo do nome do host é de 10 caracteres.

### Rótulo do subdomínio

O rótulo do subdomínio deve atender aos requisitos a seguir:
*  Apenas caracteres alfanuméricos e o traço (-) são permitidos.
*  O rótulo do subdomínio deve iniciar e terminar com um caractere alfanumérico.
*  O comprimento máximo do rótulo do subdomínio é de 10 caracteres.
*  O rótulo do subdomínio deve ser exclusivo em sua conta.

### Nome de domínio

O nome do domínio-raiz deve atender aos requisitos a seguir:
* O nome de domínio deve consistir em duas ou mais sequências separadas por ponto (.)
* A primeira sequência deve começar com um caractere alfabético e terminar com um caractere alfanumérico.
* Todas as sequências, exceto a última, podem conter apenas caracteres alfanuméricos e de traço (-).
* A última sequência pode conter apenas caracteres alfabéticos.
* O comprimento da última sequência deve estar no intervalo de 2 a 24 caracteres.

**Nota:** o comprimento máximo do Nome completo do domínio (FQDN) para hosts e VMs é de 50 caracteres. Os nomes de domínio devem ajustar-se a este comprimento máximo.

### Configuração de DNS

Selecione a configuração do Sistema de Nomes de Domínio (DNS) para sua instância:

* **Único VSI público do Windows para o Active Directory/DNS**: um único VSI do Microsoft Windows Server para o Microsoft Active Directory (AD), que funciona como o DNS para a instância na qual os hosts e as máquinas virtuais são registrados, é implementado e pode ser consultado.
* **Duas VMs do Windows Server dedicadas e altamente disponíveis no cluster de gerenciamento**: para a V2.3 e liberações futuras, duas máquinas virtuais do Microsoft Windows são implementadas, ajudando a aprimorar a segurança e robustez.

**Importante:** deve-se fornecer duas licenças do Microsoft Windows Server 2012 R2 se você configurar sua instância para usar as duas máquinas virtuais do Microsoft Windows. Use a licença da edição Microsoft Windows Server 2012 R2 Standard e/ou a licença da edição Microsoft Windows Server 2012 R2 Datacenter.

Atualmente, cada licença pode ser designada a apenas um único servidor físico e abrange até dois processadores físicos. Uma licença Standard Edition é capaz de executar duas máquinas virtuais virtualizadas do Microsoft Windows por servidor com 2 processadores. Portanto, duas licenças são necessárias, pois duas máquinas virtuais do Microsoft Windows são implementadas em dois hosts diferentes.

Você tem 30 dias para ativar as máquinas virtuais.

Para obter mais informações sobre como pedir o licenciamento do Windows, veja [Documentação do Windows Server 2012 R2](https://www.microsoft.com/en-us/licensing/product-licensing/windows-server-2012-r2.aspx#tab=2).

## Resumo do Pedido

Com base em sua configuração selecionada para a instância, o custo estimado é gerado instantaneamente e exibido na seção **Resumo do pedido** na área de janela direita. Clique em **Detalhes da precificação** na parte inferior da área de janela direita para gerar um documento PDF que forneça os detalhes da estimativa.

## Procedimento

1. No Catálogo do {{site.data.keyword.cloud_notm}}, clique em **VMware** na área de janela de navegação esquerda e, em seguida, clique em **vCenter Server** na seção **Datacenters virtuais **.
2. Na página **VMware vCenter Server on IBM Cloud**, clique no cartão **vCenter Server** e clique em **Criar**.
3. Na página **vCenter Server**, insira o nome da instância.
4. Clique em **Instância primária** para implementar uma única instância no ambiente.
5. Especifique a edição de licença do VMware NSX.
6. Conclua a configuração do Bare Metal Server:
  1. Selecione o {{site.data.keyword.CloudDataCent_notm}} para hospedar a instância.
  2. Selecione o modelo de CPU **Customizado** e a quantia de **RAM**.
7. Conclua a configuração de armazenamento.
  * Quando você selecionar **Armazenamento vSAN**, especifique o **Tipo
e tamanho do disco para discos de capacidade vSAN**, o **Número de discos de
capacidade vSAN** e como a **Licença vSAN** deve ser fornecida.
  * Quando você selecionar **Armazenamento NFS** e desejar incluir e definir as mesmas configurações para todos os compartilhamentos de arquivos, especifique o **Número de compartilhamentos**, o **Tamanho** e o **Desempenho**.
  * Quando você selecionar **Armazenamento NFS** e desejar incluir e configurar compartilhamentos de arquivos individualmente, selecione **Configurar compartilhamentos
individualmente**, em seguida, clique no ícone **+** ao lado do rótulo **Incluir NFS** e selecione o **Tamanho** e o **Desempenho**
para cada compartilhamento de arquivo individual. Deve-se selecionar pelo menos um compartilhamento de arquivo.
8. Conclua a configuração da interface de rede.
   1. Insira o prefixo de nome do host, o rótulo do subdomínio e o nome do domínio-raiz.
   2. Selecione a configuração do DNS.
9. Na área de janela **Resumo do pedido**, verifique a configuração da instância antes de fazer o pedido.
   1. Revise as configurações para a instância.
   2. Clique no link ou nos links dos termos que se aplicam ao seu pedido e confirme que concorda com esses termos antes de pedir a instância.
   3. Revise o custo estimado da instância clicando no link de custo em **Calcular custo**. Para salvar ou imprimir o resumo de seu pedido, clique no ícone **Imprimir** ou **Fazer download** no canto superior direito da janela PDF.
   4. Clique em **Provisão**.

## Resultados

A implementação da instância é iniciada automaticamente. Você recebe confirmação de que o pedido está sendo processado e pode verificar o status da implementação visualizando os detalhes da instância.

Quando a instância for implementada com êxito, os componentes descritos em [Especificações técnicas para instâncias do VMware Federal on {{site.data.keyword.cloud_notm}}](vc_fed_overview.html#technical-specifications-for-vmware-federal-on-ibm-cloud-instances) ser instalados em sua plataforma virtual VMware. Os servidores ESXi pedidos são agrupados como **cluster1** por padrão.

Quando a instância estiver pronta para usar, seu status mudará para **Pronta para usar** e você receberá uma notificação por e-mail.

## O que fazer a seguir

Visualize, gerencie ou proteja a instância do VMware Federal que você pediu.

**Importante:** deve-se gerenciar os componentes do {{site.data.keyword.vmwaresolutions_short}} criados em sua conta do {{site.data.keyword.cloud_notm}} somente por meio do console do {{site.data.keyword.vmwaresolutions_short}}, não do	{{site.data.keyword.slportal}} ou de qualquer outro meio fora do console.
Se você mudar esses componentes fora do console do {{site.data.keyword.vmwaresolutions_short}}, as mudanças não serão sincronizadas com o console.

**CUIDADO:** Gerenciar quaisquer componentes do {{site.data.keyword.vmwaresolutions_short}} (que foram instalados em sua conta do {{site.data.keyword.cloud_notm}} quando você pediu a instância) de fora do console do {{site.data.keyword.vmwaresolutions_short}} pode desestabilizar seu ambiente. Estas atividades de gerenciamento incluem:
*  Incluindo, modificando, retornando ou removendo componentes
*  Expandindo ou contraindo a capacidade da instância por meio da remoção de servidores ESXi
*  Desativando componentes

   As exceções a essas atividades incluem o gerenciamento de compartilhamentos de arquivos de armazenamento compartilhado por meio do {{site.data.keyword.slportal}}. Essas atividades incluem: pedido, exclusão (que poderá afetar armazenamentos de dados, se montado), autorização e montagem de compartilhamentos de arquivos de armazenamento compartilhados.

### Links relacionados

* [Inscrevendo-se para uma conta do {{site.data.keyword.cloud_notm}}](../vmonic/signing_softlayer_account.html)
* [Visualizando instâncias do VMware Federal](vc_fed_viewinginstance.html)
* [Expandindo e contraindo a capacidade para instâncias do VMware Federal](vc_fed_addingremovingservers.html)
* [Incluindo, visualizando e excluindo clusters para instâncias do VMware Federal](fed_addviewdeleteclusters.html)
* [Protegendo instâncias do VMware Federal](vc_fed_securinginstance.html)
* [Excluindo instâncias do VMware Federal](vc_fed_deletinginstance.html)
* [Entrando em contato com o Suporte IBM](../vmonic/trbl_support.html)
