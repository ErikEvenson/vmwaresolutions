---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-20"

---

# Pedindo instâncias do Cloud Foundation

Para implementar uma plataforma unificada de data center definido por software (SDDC) com configuração padrão de cálculo, armazenamento e rede, peça uma instância do VMware Cloud Foundation. Durante o pedido inicial, também é possível incluir serviços, como o [Zerto on {{site.data.keyword.cloud}}](../services/addingzertodr.html) para recuperação de desastre.

## Requisitos

Assegure-se de que tenha concluído as tarefas a seguir:
*  Você configurou as credenciais de infraestrutura do {{site.data.keyword.cloud_notm}} na página **Configurações**. Para obter mais informações, veja [Gerenciando contas de usuários e configurações](../vmonic/useraccount.html).
*  Você revisou os requisitos e considerações em [Requisitos e planejamento para instâncias do Cloud Foundation](sd_planning.html).

**Importante:** não modifique nenhum valor configurado durante o pedido e a implementação da instância. Isso pode fazer com que a instância se torne inutilizável. Além disso, não mude o nome da instância, o nome do domínio-raiz, o rótulo do subdomínio ou o prefixo de nome do host depois que a instância for implementada.

## Configurações do sistema

Deve-se especificar as configurações do sistema a seguir ao pedir uma instância do Cloud Foundation.

### Nome da instância

O nome da instância deve atender aos requisitos a seguir:
* Apenas caracteres alfanuméricos e o traço (-) são permitidos.
* O nome da instância deve iniciar e terminar com um caractere alfanumérico.
* O comprimento máximo do nome da instância é de 10 caracteres.
* O nome da instância deve ser exclusivo dentro de sua conta.

### Principal ou secundário

Selecione se pedirá uma nova instância primária ou uma instância secundária para uma instância primária existente.

## Configurações de licenciamento

Especifique as opções de licenciamento para os seguintes componentes do VMware na instância:  
* Licença do vCenter Server - Padrão
* Licença do vSphere - Enterprise Plus
* Licença NSX - Enterprise
* Licença do vSAN: selecione o Advanced ou Enterprise Edition

Para usuários do Parceiro de Negócios, a licença do vCenter Server (Standard Edition), a licença do vSphere (Enterprise Plus Edition), a licença do NSX e a licença do vSAN são incluídas e compradas em seu nome. No entanto, deve-se especificar a edição da licença vSAN.

Para usuários que não são do Parceiros de negócios, é possível usar as licenças do VMware fornecidas pela IBM para esses componentes selecionando **Incluir com a compra** ou é possível usar Bring Your Own License (BYOL) selecionando **Eu fornecerei** e inserindo as suas próprias chaves de licença.

## Configurações do Bare Metal Server

### Local do datacenter

Selecione o {{site.data.keyword.CloudDataCent_notm}} no qual a instância deve ser hospedada.

### Pré-configurado

Quando você seleciona **Pré-configurado**, não é possível mudar as configurações de CPU ou RAM.

Com base em seus requisitos, selecione uma configuração do Bare Metal Server:
  * Pequeno (Dual Intel Xeon E5-2650 v4/total de 24 núcleos, 2.2 GHz/128 GB de RAM/12 unidades)
  * Grande (Dual Intel Xeon E5-2690 v4/total de 28 núcleos, 2.6 GHz/512 GB de RAM/12 unidades)

### Customizado

Ao selecionar **Customizado**, será possível escolher a combinação de CPU e RAM de acordo com suas necessidades.

Selecione o modelo de CPU e RAM para o Bare Metal Server.

Tabela 1. Opções para {{site.data.keyword.baremetal_short}}customizado

| Opções de CPU        | Opções de RAM       |
|:------------- |:------------- |
| Dual Intel Xeon E5-2620 v4/total de 16 núcleos, 2.1 GHz | 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Dual Intel Xeon E5-2650 v4/total de 24 núcleos, 2.2 GHz | 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Dual Intel Xeon E5-2690 v4/total de 28 núcleos, 2.6 GHz | 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Processador Dual Intel Xeon Silver 4110/total de 16 núcleos, 2,1 GHz | 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |
| Processador Dual Intel Xeon Gold 5120/total de 28 núcleos, 2,2 GHz | 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |
| Processador Dual Intel Xeon Gold 6140/Total de 36 núcleos, 2,3 GHz | 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |

### Número de Bare Metal Servers

Uma instância do Cloud Foundation inclui quatro Bare Metal Servers na implementação inicial. Não é possível mudar o número de Bare Metal Servers quando você coloca a ordem.

## Configurações de armazenamento

As instâncias do Cloud Foundation suportam somente o armazenamento vSAN.
* Quando você seleciona a configuração **Pré-configurado** do Bare Metal Server, as configurações de armazenamento são padronizadas e não podem ser mudadas:
  * Para a configuração **Pequeno** do Bare Metal Server, 2 unidades de disco de 1,9 TB SSD SED são pedidas.
  * Para a configuração **Grande** do Bare Metal Server, 4 unidades de disco de 3,8 TB SSD SED são pedidas.
* Ao selecionar a configuração **Customizado** do Bare Metal Server, é possível customizar o armazenamento do VMware vSAN para sua instância especificando as configurações a seguir em **Armazenamento vSAN**:
  * **Tipo e tamanho do disco para discos de capacidade vSAN**: selecione a capacidade que atenda às suas necessidades de armazenamento compartilhado.
  * **Número de discos de capacidade vSAN**: especifique o número de discos para o armazenamento compartilhado vSAN que você deseja incluir. As quantidades de disco devem ser 2, 4, 6 ou 8.

## Configurações da interface de rede

Deve-se especificar as configurações da interface de rede a seguir ao pedir uma instância do Cloud Foundation.

### Prefixo de Nome do Host

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

**Nota:** o comprimento máximo do FQDN (Nome completo do domínio) para hosts e VMs (máquinas virtuais) é de 50 caracteres. Os nomes de domínio devem ajustar-se a este comprimento máximo.

### Formato de valor para as configurações de rede

O nome de domínio e o rótulo do subdomínio são usados para gerar o nome do usuário e nomes de servidor da instância, conforme mostrado na tabela a seguir.

Tabela 2. Formato de valor para nomes de usuário, nomes de domínio e nomes de servidor

| Nome        | Formato do valor      |
  |:------------- |:------------- |
  | Nome de domínio | `<root_domain>` |  
  | Nome do servidor ESXi totalmente qualificado | `<host_prefix><n>.<subdomain_label>.<root_domain>`, em que `<n>` é a sequência do servidor ESXi. O comprimento máximo é de 50 caracteres. |   
  | Nome do usuário de login do vCenter Server | `<user_id>@<root_domain>` (Usuário do Microsoft Active Directory) ou `administrator@vsphere.local` |
  | FQDN do vCenter Server | `vcenter-1.<subdomain_label>.<root_domain>`. O comprimento máximo é de 50 caracteres. |  
  | FQDN do SDDC Manager | `sddcmanager.<subdomain_label>.<root_domain>`. O comprimento máximo é de 50 caracteres. |
  | Nome do site de Conexão única (SSO) | `<subdomain_label>`
  | FQDN do PSC | `PSC-<subdomain_label>.<subdomain_label>.<root_domain>`. O comprimento máximo é de 50 caracteres. |  

  O FQDN do SDDC Manager não pode ser resolvido publicamente. Caso contrário, a configuração da instância do Cloud Foundation pode falhar e não é recuperável. Antes de especificar um nome de domínio, revise [Considerações ao escolher um nome de domínio-raiz](../vmonic/trbl_limitations.html#considerations-when-choosing-a-root-domain-name-for-cloud-foundation-instances).

### VLANs

As configurações de rede se baseiam em sua seleção de **Pedir novas VLANs** ou **Selecionar VLANs existentes**.

São necessárias uma VLAN pública e duas VLANs privadas para o seu pedido de instância. As duas VLANs privadas são truncadas em cada Bare Metal Server.

**Pedir novas VLANs**  
Selecione para pedir uma nova VLAN pública e duas novas VLANs privadas.

**Selecionar VLANs existentes**  
Dependendo do {{site.data.keyword.CloudDataCent_notm}} selecionado, VLANs públicas e privadas existentes podem estar disponíveis.

Ao selecionar para reutilizar VLANs públicas e privadas existentes, especifique as VLANs e as sub-redes:
  * **VLAN pública** é para acesso à rede pública.
  * **VLAN privada** é para conectividade entre os data centers e os serviços dentro do {{site.data.keyword.cloud_notm}}.
  * **VLAN privada secundária** é para recursos do VMware, como vSAN.
  * **Sub-rede primária** é designada a hosts físicos para o acesso à rede pública.
  * **Sub-rede primária privada** é designada a hosts físicos para tráfego de gerenciamento.

**Importante:**
* Assegure-se de que a configuração de firewall nas VLANs selecionadas não bloqueie o tráfego de dados de gerenciamento.
* Assegure-se de que todas as VLANs selecionadas estejam no mesmo pod, porque os servidores ESXi não podem ser provisionados em VLANs de pod misto.

## Serviços

Ao pedir uma instância do Cloud Foundation, é possível também pedir serviços adicionais. Para obter mais informações sobre os serviços disponíveis, veja [Serviços para instâncias do Cloud Foundation](sd_planning.html#services-for-cloud-foundation-instances).

## Resumo do Pedido

Com base em sua configuração selecionada para a instância e os serviços de complemento, o custo estimado é gerado instantaneamente e exibido na área de janela à direita. Clique em **Detalhes da precificação** na parte inferior da área de janela direita para gerar um documento PDF que forneça os detalhes da estimativa.

## Procedimento

1. No Catálogo do {{site.data.keyword.cloud_notm}}, clique em **VMware** na área de janela de navegação esquerda e, em seguida, clique em **Cloud Foundation** na seção **Datacenters virtuais**.
2. Na página **VMware Cloud Foundation on IBM Cloud**, clique em **Criar**.
3. Na página **Cloud Foundation**, insira o nome da instância.
4. Selecione o tipo de instância:
   * Clique em **Instância primária** para implementar uma única instância no ambiente ou para implementar a primeira instância em uma topologia multissite.
   * Clique em **Instância secundária** para conectar a instância a uma instância existente (primária) no ambiente para alta disponibilidade e conclua as etapas a seguir:
     1. Selecione a instância primária à qual deseja que a instância secundária seja conectada.
     2. Insira a senha do administrador do PSC para a instância primária.
5. Conclua as configurações de licença para os componentes da instância:
   *  Para usar licenças fornecidas pela IBM, selecione **Incluir com a compra**.
   *  Para usar sua própria licença, selecione **Eu fornecerei** e insira a chave de licença.  
6. Conclua as configurações do Bare Metal Server:
   1. Selecione o {{site.data.keyword.CloudDataCent_notm}} para hospedar a instância.
   2. Selecione a configuração do Bare Metal Server.
      * Quando você selecionar **Pré-configurado**, escolha uma configuração de **Pequeno** e **Grande**.
      * Ao selecionar **Customizado**, especifique o modelo de CPU e o tamanho da RAM.
7. Conclua as configurações de armazenamento:
   * Se você selecionou **Pré-configurado** para a configuração de Bare Metal, observe que as configurações de armazenamento para as configurações padronizadas **Pequeno** e **Grande** do Bare Metal Server não podem ser mudadas.
   * Se você selecionou **Customizado** para a configuração de Bare Metal, especifique o **Tipo e tamanho do disco para discos de capacidade de vSAN** e **Número de discos de capacidade de vSAN**.
8. Conclua as configurações da interface de rede:
   1. Insira o prefixo de nome do host, o rótulo do subdomínio e o nome do domínio-raiz. Para uma instância secundária, o nome do domínio é preenchido automaticamente.
   2. Selecione as configurações de VLAN:
      * Se desejar pedir novas VLANs públicas e privadas, clique em **Pedir novas VLANs**.
      * Se quiser reutilizar as VLANs públicas e privadas existentes quando estiverem disponíveis, clique em **Selecionar VLANs existentes** e especifique as VLANs e as sub-redes.

9. Selecione os serviços complementares a serem implementados na instância clicando no cartão de serviço correspondente. Se um serviço requerer configuração, conclua as configurações específicas do serviço e clique em **Incluir serviço** na janela de configuração pop-up. Para obter informações sobre como fornecer configurações para um serviço, veja o tópico de ordem de pedido correspondente.

10. Na área de janela **Resumo do pedido**, verifique a configuração da instância antes de fazer o pedido.
    1. Revise as configurações para a instância.
    2. Revise o custo estimado da instância. Clique em **Detalhes da precificação** para gerar um PDF de resumo. Para salvar ou imprimir o resumo de seu pedido, clique no ícone **Imprimir** ou **Fazer download** no canto superior direito da janela PDF.
    3. Assegure-se de que a conta a ser cobrada esteja correta e, em seguida, marque a caixa de seleção **Entendo que a conta listada abaixo será cobrada**.
    4. Clique no link ou nos links dos termos que se aplicam ao seu pedido. Assegure-se de que concorda com esses termos e, em seguida, marque a caixa de seleção **Li e concordei com os Contratos de Prestação de Serviços de Terceiros listados abaixo**.
    5. Clique em **Provisão**.

## Resultados

A implementação da instância é iniciada automaticamente. Você recebe confirmação de que o pedido está sendo processado e pode verificar o status da implementação visualizando os detalhes da instância.

Quando a instância for implementada com êxito, os componentes descritos em [Especificações técnicas para instâncias do Cloud Foundation](../sddc/sd_cloudfoundationoverview.html#technical-specifications-for-cloud-foundation-instances) serão instalados em sua plataforma virtual do VMware. Os servidores ESXi que você pediu são agrupados como **SDDC-Cluster** por padrão. Se tiver pedido serviços adicionais, a implementação dos serviços iniciará após a conclusão do pedido.

Quando a instância estiver pronta para usar, seu status mudará para **Pronta para usar** e você receberá uma notificação por e-mail.

Quando você pedir uma instância secundária, o VMware vSphere Web Client da instância primária (vinculado à secundária) poderá ser reiniciado depois que o pedido da instância secundária estiver concluído.

## O que fazer a seguir

Visualizar e gerenciar a instância do Cloud Foundation que você pediu.

**Importante**: deve-se gerenciar os componentes do {{site.data.keyword.vmwaresolutions_short}} criados em sua conta do {{site.data.keyword.cloud_notm}} apenas por meio do console do {{site.data.keyword.vmwaresolutions_short}}, não do {{site.data.keyword.slportal}} ou de qualquer outro meio fora do console. Se você mudar esses componentes fora do console do {{site.data.keyword.vmwaresolutions_short}}, as mudanças não serão sincronizadas com o console.

**CUIDADO**: gerenciar quaisquer componentes do {{site.data.keyword.vmwaresolutions_short}} (que foram instalados em sua conta do {{site.data.keyword.cloud_notm}} quando você pediu a instância) fora do console do {{site.data.keyword.vmwaresolutions_short}} pode desestabilizar seu ambiente. Estas atividades de gerenciamento incluem:

*  Incluindo, modificando, retornando ou removendo componentes
*  Expandindo ou contraindo a capacidade da instância por meio da inclusão ou remoção de servidores ESXi
*  Desativando componentes
*  Reiniciando os serviços

   As exceções a essas atividades incluem o gerenciamento de compartilhamentos de arquivos de armazenamento compartilhado por meio do {{site.data.keyword.slportal}}. Essas atividades incluem: pedido, exclusão (que poderá afetar armazenamentos de dados, se montado), autorização e montagem de compartilhamentos de arquivos de armazenamento compartilhados.

### Links relacionados

* [Inscrevendo-se para uma conta do {{site.data.keyword.cloud_notm}}](../vmonic/signing_softlayer_account.html)
* [Visualizando instâncias do Cloud Foundation](sd_viewinginstances.html)
* [Incluindo, visualizando e excluindo clusters para instâncias do Cloud Foundation](sd_addingviewingclusters.html)
* [Expandindo e contraindo capacidade para instâncias do Cloud Foundation](sd_addingremovingservers.html)
* [Pedindo, visualizando e removendo serviços para instâncias do Cloud Foundation](sd_addingremovingservices.html)
* [Excluindo instâncias do Cloud Foundation](sd_deletinginstance.html)
* [Pergunta mais frequente sobre BYOL](../vmonic/faq_byol.html)
