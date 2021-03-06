---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-31"

---

# Notas sobre a Liberação para V2.5

Esta liberação inclui novos recursos, atualizações de componentes, aprimoramentos de usabilidade e correções de bug. Para obter uma lista de problemas corrigidos em liberações diferentes, problemas conhecidos com o produto e dicas adicionais para usar o {{site.data.keyword.vmwaresolutions_full}}, veja o [{{site.data.keyword.vmwaresolutions_short}} dW Answers](https://developer.ibm.com/answers/topics/cloudvmw/){:new_window}.

## Correção para Spectre e Meltdown

O {{site.data.keyword.vmwaresolutions_short}} liberou correções do VMware em resposta às vulnerabilidades conhecidas como Spectre e Meltdown (CVE-2017-5753, CVE-2017-5715 e CVE-2017-5754).

* CVEID: [CVE-2017-5753](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5753)
* CVEID: [CVE-2017-5715](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5715)
* CVEID: [CVE-2017-5754](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5754)

Para obter mais informações, veja [Tratando as vulnerabilidades Spectre e Meltdown](../vmonic/trbl_fix_spectre.html).

## Atualização de componente NSX

Esta liberação instala o VMware NSX for vSphere 6.4.1 para novas implementações do VMware vCenter Server on {{site.data.keyword.cloud_notm}}, VMware vCenter Server on {{site.data.keyword.cloud_notm}} with Hybridity Bundle, NetApp ONTAP Select e VMware Federal on {{site.data.keyword.cloud_notm}}.

## Remoção da configuração de backup padrão

O {{site.data.keyword.vmwaresolutions_short}} oferece dois serviços de complementos integrados para backup: IBM Spectrum Protect&trade; Plus on {{site.data.keyword.cloud_notm}} e Veeam on {{site.data.keyword.cloud_notm}}. Esses serviços permitem que você planeje e forneça a recuperação de sua infraestrutura de gerenciamento e de sua carga de trabalho. Além disso, o IBM Resiliency Services oferece serviços gerenciados para backups do Veeam.

Iniciando com a liberação da V2.5, os serviços IBM Spectrum Protect Plus on {{site.data.keyword.cloud_notm}} e Veeam on {{site.data.keyword.cloud_notm}}, quando implementados, não pré-configuram mais o backup de quaisquer VMs. Essa mudança permite assegurar a configuração adequada de todos os aspectos de suas tarefas de backup, incluindo planejamento, período de retenção, uso de deduplicação, monitoramento e alertas e gerenciamento de chaves de criptografia. Além disso, a VM do IBM CloudDriver não é mais configurada como um servidor de arquivos persistente para backups do NSX.

Você é responsável pela configuração, gerenciamento e monitoramento de todos os componentes de software, incluindo o backup e a disponibilidade da infraestrutura de gerenciamento e das cargas de trabalho. Para obter mais informações, consulte [Fazendo backup de componentes](../archiref/solution/solution_backingup.html#backing-up-components).

**Nota:** essa mudança não afeta as instâncias implementadas antes da V2.5 que já instalaram o serviço IBM Spectrum Protect Plus on {{site.data.keyword.cloud_notm}} ou Veeam on {{site.data.keyword.cloud_notm}}.

## Resiliência do IBM CloudDriver

Para instâncias implementadas ou submetidas a upgrade para liberações V2.5 ou mais recentes, o componente IBM CloudDriver não está mais configurado como uma máquina virtual (VM) dentro do cluster do vSphere. Em vez disso, ele é implementado como uma Virtual Server Instance (VSI) da infraestrutura do {{site.data.keyword.cloud_notm}}, conforme necessário, com o código mais recente do {{site.data.keyword.cloud_notm}} for VMware para operações, como a implementação de nós, clusters ou serviços adicionais. Além disso, o IBM CloudDriver foi mudado para se comunicar com o plano de gerenciamento do {{site.data.keyword.cloud_notm}} usando a rede privada do {{site.data.keyword.cloud_notm}} para que as regras de firewall NSX Edge Services Gateway (ESG) de gerenciamento e de conversão de endereço de rede (NAT) que permitem a comunicação de saída do IBM CloudDriver com a rede pública sejam removidas.

Alguns serviços de complemento, como F5 on {{site.data.keyword.cloud_notm}}, FortiGate Virtual Appliance on {{site.data.keyword.cloud_notm}} e Zerto on {{site.data.keyword.cloud_notm}}, ainda requerem acesso à rede pública, portanto o NSX ESG de gerenciamento permanece implementado em todas as instâncias.

## Usuário ativado por IAM e gerenciamento de acesso

Iniciando com a liberação V2.5, o {{site.data.keyword.vmwaresolutions_short}} é integrado ao IBM Identity and Access Management (IAM) para fornecer uma abordagem unificada para gerenciar contas do usuário e acesso de usuário dentro de sua conta do {{site.data.keyword.cloud_notm}}. Por causa do qual:
* Agora é possível incluir múltiplos usuários em sua conta do {{site.data.keyword.cloud_notm}} para colaboração e gerenciar seu acesso aos serviços e recursos provisionados em sua conta designando diferentes funções de acesso de plataforma a eles.  
* As instâncias que são implementadas nas liberações V2.5 e mais recentes são vinculadas automaticamente à conta do usuário que está sendo usada quando a instância é pedida.
* Para instâncias que foram implementadas nas liberações V2.4 e anteriores, é possível migrá-las para uma conta especificada do {{site.data.keyword.cloud_notm}} e, em seguida, gerenciá-las usando o IAM também.

Para obter mais informações, veja:
* [Convidando usuários para acessar serviços e recursos](../vmonic/iamuserinvite.html)
* [ Gerenciando o acesso de usuário com o IAM ](../vmonic/iam.html)

## Mudanças nas contas do usuário e grupos para instâncias do VMware vCenter Server e do VMware Cloud Foundation

O grupo de usuários **ic4v-vCenter** foi criado no Microsoft Active Directory Server e incluído nas permissões globais no vCenter Server e nos grupos de usuários para o NSX Manager. O grupo contém a conta do usuário de **automação** para instâncias do vCenter Server e contas do usuário específicas do serviço para instâncias do vCenter Server e do Cloud Foundation.

Não edite as permissões globais do grupo **ic4v-vCenter** na página **Usuários e grupos** no VMware vSphere Web Client. Fazer isso pode afetar as operações de gerenciamento.

Para instâncias do Cloud Foundation, use o ID do usuário do host **customerroot** no lugar do ID do usuário do host **raiz**. Continue a usar o ID do usuário do host **raiz** para instâncias do vCenter Server.

Para obter mais informações sobre contas do usuário, veja:

* [Considerações sobre como alterar os artefatos do vCenter Server](../vcenter/vcenter_chg_impact.html)
* [Considerações sobre como alterar os artefatos do Cloud Foundation](../sddc/cf_chg_impact.html)

## Atualizações para serviços complementares

### IBM Spectrum Protect Plus on IBM Cloud

Iniciando com a liberação V2.5, o serviço IBM Spectrum Protect Plus on {{site.data.keyword.cloud_notm}} é implementado como duas VMs separadas com base nas melhores práticas, com uma VM executando o servidor Spectrum Protect Plus e a outra VM executando o servidor vSnap e o proxy do VADP.

Agora é possível pedir até dez armazenamentos de dados de backup, permitindo até 120 TB de armazenamento de backup. O vSnap e a VM do VADP são dimensionados dependendo de seu tamanho de armazenamento de backup selecionado e de acordo com as informações nos [Blueprints do IBM Spectrum Protect Plus](https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Tivoli%20Storage%20Manager/page/IBM%20Spectrum%20Protect%20Plus%20Blueprints).

### KMIP for VMware on IBM Cloud

Um novo terminal está agora disponível na Alemanha para o serviço KMIP for VMware on {{site.data.keyword.cloud_notm}}.

Para obter mais informações, veja [Configuração do serviço KMIP for VMware on {{site.data.keyword.cloud_notm}}](../services/kmip_ordering.html#kmip-for-vmware-on-ibm-cloud-service-configuration).

## Documentação nova e atualizada

### Documentação de armazenamento anexado

O armazenamento Anexado para o vCenter Server no documento técnico do IBM Cloud agora está disponível na seção *Referência* da documentação do usuário. Esse documento de arquitetura de referência está disponível somente em inglês. Para obter mais informações, veja [Armazenamento anexado para o vCenter Server on IBM Cloud](../archiref/attached-storage/storage-benefits.html).

### Especificações técnicas

As especificações técnicas para todos os tipos de instância e tipos de serviço estão agora disponíveis na documentação do usuário e vinculadas por meio da interface com o usuário. Para obter mais informações, veja o tópico de visão geral apropriado para sua instância e serviço.

### Serviços de documentação

As informações de serviços são melhoradas para identificar facilmente o suporte de serviço com base no número da liberação em que ele foi disponibilizado.

Para obter mais informações, veja:

* [Serviços disponíveis para instâncias do vCenter Server](../vcenter/vc_addingremovingservices.html#available-services-for-vcenter-server-instances)
* [Serviços disponíveis para instâncias do vCenter Server with Hybridity Bundle](../vcenter/vc_hybrid_addingremovingservices.html#available-services-for-vcenter-server-with-hybridity-bundle-instances)
* [Serviços disponíveis para instâncias do Cloud Foundation](../sddc/sd_addingremovingservices.html#available-services-for-cloud-foundation-instances)

## Atualizações e aprimoramentos da interface com o usuário

A interface com o usuário é atualizada e fornece os aprimoramentos a seguir:

* Se você tiver uma conta de infraestrutura do {{site.data.keyword.cloud_notm}} (SoftLayer) que esteja vinculada à sua conta do {{site.data.keyword.cloud_notm}}, agora será possível clicar no botão **Recuperar** recém-incluído na página **Configurações** para obter o nome do usuário e a chave API para sua conta de infraestrutura do {{site.data.keyword.cloud_notm}} (SoftLayer) automaticamente.
* Uma nova guia **Histórico de implementação** foi incluída na área de janela de navegação esquerda da página de detalhes da instância para você verificar o histórico de implementação de uma instância.
* Várias mensagens de erro e aprimoramentos de dica de ferramenta foram feitos para ajudá-lo na seleção da configuração apropriada na interface com o usuário.
