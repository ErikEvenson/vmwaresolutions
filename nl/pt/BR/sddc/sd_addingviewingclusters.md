---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-19"

---

# Incluindo, visualizando e excluindo clusters para instâncias do Cloud Foundation

Os servidores ESXi que você configurou quando pediu uma instância são agrupados em um cluster padrão. O nome do cluster padrão é:
* Para instâncias que foram implementadas na V2.1 ou liberações mais recentes: **MGMT-Cluster-`<subdomain_label>`**
* Para instâncias que foram implementadas na V2.0 ou liberações anteriores: **SDDC-Cluster**

É possível incluir seus próprios clusters em instâncias do VMware Cloud Foundation para expandir a capacidade de cálculo e armazenamento. Em um cluster, é possível gerenciar servidores ESXi para melhor alocação de recurso e alta disponibilidade. Quando não for mais necessário, será possível excluir os clusters incluídos de suas instâncias.

**Disponibilidade**:
* O recurso incluir cluster está disponível somente para instâncias que foram implementadas na (ou submetidas a upgrade para a) V2.0 e liberações mais recentes.
* O recurso excluir cluster está disponível somente para instâncias que são implementadas na (ou submetidas a upgrade para a) V2.3 e liberações mais recentes.  

## Incluindo clusters para instâncias do Cloud Foundation

É possível incluir até cinco clusters em uma instância do Cloud Foundation.

### Configurações do sistema

Quando você inclui um cluster em uma instância do Cloud Foundation, deve-se especificar as configurações a seguir.

#### Nome do cluster

O nome do cluster deve atender aos requisitos a seguir:
* Apenas caracteres alfanuméricos e o traço (-) são permitidos.
* O nome do cluster deve iniciar e terminar com um caractere alfanumérico.
* O comprimento máximo do nome do cluster é de 30 caracteres.
* O nome do cluster deve ser exclusivo dentro da instância do Cloud Foundation.

#### Local do datacenter

O local do {{site.data.keyword.CloudDataCent}} do cluster é configurado como o {{site.data.keyword.CloudDataCent_notm}} da instância do Cloud Foundation por padrão. É possível implementar o cluster em um {{site.data.keyword.CloudDataCent_notm}} diferente da instância implementada, mas deve-se assegurar que a latência de rede entre os dois {{site.data.keyword.CloudDataCents_notm}} seja menor que 150 ms. Para verificar a latência de rede, é possível usar uma ferramenta, como o [SoftLayer IP Backbone Looking Glass](http://lg.softlayer.com/){:new_window}.

Os data centers disponíveis para você dependem da configuração do Bare Metal Server selecionada para implementação. Se você selecionar a configuração **Customizada**, poderá também implementar o cluster em um pod da infraestrutura do {{site.data.keyword.cloud}} diferente, se o data center selecionado contiver pods adicionais. Isso é útil quando o pod da infraestrutura do {{site.data.keyword.cloud_notm}} padrão em que a instância inicial é implementada tiver atingido sua capacidade máxima.

**Nota:** as configurações padronizadas **Pequeno** e **Grande** do Bare Metal Server usam um pod padrão que não pode ser mudado.

Se você implementar o cluster em um data center ou pod diferente, três VLANs adicionais serão pedidas para uso com o {{site.data.keyword.baremetal_short}} pedido.

### Configurações do Bare Metal Server

É possível escolher **Customizado** ou **Pré-configurado**.

#### Customizado

Para a configuração **Customizada**, você tem um número de opção para o **Modelo de CPU** e **RAM**. As opções disponíveis podem diferir dependendo da versão na qual a sua instância foi inicialmente implementada.

Tabela 1. Opções para {{site.data.keyword.baremetal_short}}customizado

| Opções de CPU   | Opções de RAM   |
|:------------- |:------------- |
| Dual Intel Xeon E5-2620 v4/total de 16 núcleos, 2.1 GHz | 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Dual Intel Xeon E5-2650 v4/total de 24 núcleos, 2.2 GHz | 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Dual Intel Xeon E5-2690 v4/total de 28 núcleos, 2.6 GHz | 128 GB, 256 GB, 512 GB, 768 GB, 1,5 TB |
| Processador Dual Intel Xeon Silver 4110/total de 16 núcleos, 2,1 GHz | 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |
| Processador Dual Intel Xeon Gold 5120/total de 28 núcleos, 2,2 GHz | 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |
| Processador Dual Intel Xeon Gold 6140/Total de 36 núcleos, 2,3 GHz | 128 GB, 192 GB, 384 GB, 768 GB, 1,5 TB |

#### Pré-configurado

Para a configuração **Pré-configurado**, é possível escolher uma **Configuração do Bare Metal Server**, dependendo de seus requisitos:
* Pequeno (Dual Intel Xeon E5-2650 v4/total de 24 núcleos, 2.2 GHz/128 GB de RAM/12 discos)
* Grande (Dual Intel Xeon E5-2690 v4/total de 28 núcleos, 2.6 GHz/512 GB de RAM/12 discos)

### Configurações do armazenamento vSAN

Para as configurações **Pré-configuradas** do Bare Metal Server, não é possível mudar as configurações de armazenamento do vSAN:
* Para a configuração **Pequeno**, duas unidades de disco de 1,9 TB SSD SED são pedidas.
* Para a configuração **Grande**, quatro unidades de disco de 3,8 TB SSD SED são pedidas.

Para a configuração **Customizada** do Bare Metal Server, é possível customizar o armazenamento vSAN especificando o número de discos de capacidade de vSAN e o tipo e o tamanho de disco que atendem às suas necessidades de armazenamento.

### Configurações de licenciamento

É possível especificar as opções de licenciamento para os componentes do VMware no cluster, incluindo VMware vSphere e VMware vSAN:
* Para usuários do Parceiro de Negócios, a licença do vSphere (Enterprise Plus edition) e a licença vSAN são incluídas e compradas em seu nome. No entanto, deve-se especificar a edição da licença vSAN.
* Para usuários que não são do Parceiro de Negócios, é possível usar as licenças do VMware fornecidas pela IBM para os componentes selecionando **Incluir com compra** ou usar o Bring Your Own License (BYOL) para os componentes selecionando **Eu fornecerei** e inserindo suas próprias chaves de licença.

## Procedimento para incluir clusters em instâncias do Cloud Foundation

1. No console do {{site.data.keyword.vmwaresolutions_short}}, clique em **Instâncias implementadas** na área de janela de navegação esquerda.
2. Na tabela **Instâncias do Cloud Foundation**, clique na instância na qual você deseja incluir clusters.

   **Nota:** assegure-se de que a instância esteja no status **Pronto para uso**. Caso contrário, não será possível incluir clusters na instância.

3. Clique em **Infraestrutura** na área de janela de navegação esquerda e clique em **Incluir** no canto superior direito da tabela **CLUSTERS**.
4. Na página **Incluir cluster**, insira o nome do cluster.
5. Se você desejar hospedar o cluster em um {{site.data.keyword.CloudDataCent_notm}} diferente daquele no qual a instância está hospedada, sob **Bare Metal Server**, marque a caixa de seleção **Selecionar um local diferente** e escolha o {{site.data.keyword.CloudDataCent_notm}} para hospedar a instância.
6. Conclua a configuração do Bare Metal:
   * Se tiver selecionado **Customizado**, selecione o **Modelo de CPU** e o tamanho da **RAM**.
   * Se tiver selecionado **Pré-configurado**, selecione a **Configuração do Bare Metal Server**.
7. Conclua a configuração de armazenamento:
   * Se tiver selecionado **Customizado** para a configuração de Bare Metal, especifique o **Número de discos de capacidade vSAN** e **Tipo e tamanho do disco para discos de capacidade vSAN**.
   * Se tiver selecionado **Pré-configurado** para a configuração de Bare Metal, observe que as configurações de armazenamento para as configurações **Pequeno** e **Grande** do Bare Metal Server não poderão ser mudadas.
8. Especifique como suas chaves de licença são fornecidas:
   * Para usuários do Parceiro de Negócios, a licença do vSphere (Enterprise Plus edition) e a licença vSAN são incluídas e compradas em seu nome. No entanto, deve-se especificar a edição da licença vSAN.
   * Para usuários que não são Parceiros de Negócios, é possível selecionar uma das opções a seguir:
       * Se desejar comprar novas licenças em seu nome, selecione **Incluir com a compra** para os componentes. Para VMware vSAN, selecione também a edição de licença.
       * Se desejar usar sua própria licença do VMware para um componente, selecione **Eu fornecerei** e insira a chave de licença para o componente.
9. Na área de janela **Resumo do pedido**, verifique a configuração de cluster antes de incluir o cluster.
   1. Revise as configurações para o cluster.
   2. Revise o custo estimado do cluster. Clique em **Detalhes da precificação** para gerar um PDF de resumo. Para salvar ou imprimir o resumo de seu pedido, clique no ícone **Imprimir** ou **Fazer download** no canto superior direito da janela PDF.
   3. Clique no link ou nos links dos termos que se aplicam ao seu pedido e confirme que concorda com esses termos antes de incluir o cluster.
   4. Clique em **Provisão**.

### Resultados após incluir clusters para instâncias do Cloud Foundation

1. A implementação do cluster é iniciada automaticamente e o status do cluster muda para **Inicializando**. É possível verificar o status da implementação visualizando o histórico de implementação na página de resumo da instância.
2. Quando o cluster estiver pronto para usar, seu status mudará para **Pronto para usar**. O cluster recém-incluído é ativado com a Alta disponibilidade (HA) do vSphere e o Distributed Resource Scheduler (DRS) do vSphere.

**Importante**: não é possível mudar o nome do cluster. Mudar o nome do cluster pode causar falha das operações de inclusão ou remoção de servidores ESXi no cluster.

## Visualizando clusters em instâncias do Cloud Foundation

1. No console do {{site.data.keyword.vmwaresolutions_short}}, clique em **Instâncias implementadas** na área de janela de navegação esquerda.
2. Na tabela **Instâncias do Cloud Foundation**, clique em uma instância para visualizar os clusters contidos.
3. Clique em **Infraestrutura** na área de janela de navegação esquerda. Na tabela **CLUSTERS**, visualize o resumo sobre os clusters:
   * **Nome**: o nome do cluster.
   * **Servidores ESXi**: o número de servidores ESXi no cluster.
   * **CPU**: a especificação de CPU dos servidores ESXi no cluster.
   * **Discos vSAN customizados**: o número de discos vSAN no cluster, incluindo o tipo de disco e a capacidade.
   * **Memória**: o tamanho total da memória dos servidores ESXi no cluster.
   * **Local do data center**: o data center no qual o cluster está hospedado.
   * **Pod**: o pod no qual o cluster é implementado.
   * **Status**: o status do cluster. O status pode ter um dos valores a seguir:
   <dl class="dl">
       <dt class="dt dlterm">Inicializando</dt>
       <dd class="dd">O cluster está sendo criado e configurado.</dd>
       <dt class="dt dlterm">Modificando</dt>
       <dd class="dd">O cluster está sendo modificado.</dd>
       <dt class="dt dlterm">Pronto para usar</dt>
       <dd class="dd">O cluster está pronto para uso.</dd>
       <dt class="dt dlterm">Excluindo</dt>
       <dd class="dd">O cluster está sendo excluído.</dd>
       <dt class="dt dlterm">Excluído</dt>
       <dd class="dd">O cluster é excluído.</dd>
   </dl>
   * **Ações**: clique no ícone **Excluir** para excluir o cluster.
4. Clique em um nome do cluster para visualizar a lista de servidores ESXi e suas informações:

   * **Nome**: o nome do servidor ESXi está no formato `<host_prefix><n>.<subdomain_label>.<root_domain>`, em que:

      `host_prefix` é o prefixo do nome do host,
      `n` é a sequência do servidor ESXi,
      `subdomain_label` é o rótulo do subdomínio e
      `root_domain` é o nome do domínio-raiz.

   * **Versão**: a versão do servidor ESXi.
   * **Credenciais**: o nome de usuário e a senha para acessar o servidor ESXi.
   * **IP privado**: o endereço IP privado do servidor ESXi.
   * **Status**: o status do servidor ESXi, que pode ser um dos valores a seguir:
        <dl class="dl">
        <dt class="dt dlterm">Incluído</dt>
        <dd class="dd">O servidor ESXi foi incluído e está pronto para uso. </dd>
        <dt class="dt dlterm">Incluindo</dt>
        <dd class="dd">O servidor ESXi está sendo incluído. </dd>
        <dt class="dt dlterm">Excluindo</dt>
        <dd class="dd">O servidor ESXi está sendo excluído.</dd>
        </dl>
   * Os detalhes da licença do vSAN e a licença do vSphere. Os detalhes da licença do vSphere estão disponíveis somente quando você selecionou para usar sua própria licença do VMware (BYOL) para isso durante o pedido de cluster:
       * **Tipo de licença**: a licença do vSAN ou a licença do vSphere.
       * **Tipo de pedido**: a licença é fornecida pelo usuário (BYOL) ou é comprada no nome do usuário.
       * **Edição de licença**: a edição da licença.
       * **chave de licença**: A chave de licença.
       * **Capacidade total (CPU)**: a capacidade total ou o número de CPU fornecido pela licença.
       * **Capacidade livre (CPU)**: a capacidade que está atualmente disponível na licença.

## Excluindo clusters de instâncias do Cloud Foundation

Talvez você queira excluir um cluster de uma instância quando ela não for mais necessária.

### Antes de excluir

* Use este procedimento para excluir clusters de instâncias implementadas na V2.3 ou liberações mais recentes.
* Para clusters implementados em instâncias da V2.2 ou anteriores, deve-se fazer upgrade da instância para a V2.3 para ser possível excluir os clusters incluídos na instância.
* É possível excluir um único cluster de cada vez. Para excluir múltiplos clusters, deve-se fazer isso em sequência, aguardando que o cluster anterior seja excluído antes de tentar excluir o próximo cluster.
* Assegure-se de que todos os nós em um cluster estejam ativados e operacionais antes de excluir o cluster.
* Ao excluir um cluster, todas as VMs (máquinas virtuais) do cluster também serão excluídas e não poderão ser recuperadas. Se quiser manter as VMs, migre-as para outros clusters.
* O cluster padrão não pode ser excluído.

## Procedimento para excluir clusters de instâncias do Cloud Foundation

1. No console do {{site.data.keyword.vmwaresolutions_short}}, clique em **Instâncias implementadas** na área de janela de navegação esquerda.
2. Na tabela **Instâncias do Cloud Foundation**, clique na instância da qual você deseja excluir clusters.

   **Nota**: assegure-se de que a instância esteja no status **Pronto para usar**. Caso contrário, não será possível excluir clusters da instância.

3. Clique em **Infraestrutura** na área de janela de navegação esquerda. Na tabela **CLUSTERS**, localize o cluster que você deseja excluir e clique no ícone **Excluir**.
4. Confirme que você concluiu a migração de VMs para outros clusters, se apropriado, e que deseja excluir o cluster.

### Links relacionados

* [Visualizando instâncias do Cloud Foundation](sd_viewinginstances.html)
* [Expandindo e contraindo capacidade para instâncias do Cloud Foundation](sd_addingremovingservers.html)
