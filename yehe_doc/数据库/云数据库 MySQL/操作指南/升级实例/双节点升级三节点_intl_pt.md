
## Visão geral
Este documento descreve como atualizar uma instância do TencentDB for MySQL de [dois nós](https://intl.cloud.tencent.com/document/product/236/38329) para [três nós](https://intl.cloud.tencent.com/document/product/236/39783) no console.
>?
>- Somente instâncias de dois nós do TencentDB for MySQL podem ser atualizadas para três nós.
>- A atualização não interromperá o serviço da instância.
>- Você também pode comprar instâncias de três nós na [página de compra](https://buy.cloud.tencent.com/cdb).

## Instruções
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique em um ID de instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a página de detalhes da instância.
2. Na seção **Configuration Info (Informações de configuração)**, clique em **Upgrade to Three-node (Atualizar para três nós)** ao lado de **Architecture (Arquitetura)**.
![](https://main.qcloudimg.com/raw/cbc0ef63b4b4824a8eedf92898a039f6.png)
3. Na caixa de diálogo pop-up, especifique o modo de replicação de dados e as zonas de disponibilidade e clique em **OK**.
 - **Modo de replicação de dados**: para obter mais informações, consulte [Replicação de instância de banco de dados](https://intl.cloud.tencent.com/document/product/236/7913).
 - **Implantação multi-AZ**: a implantação multi-AZ protege o serviço de banco de dados de ser interrompido em caso de falhas de banco de dados ou falhas de zona de disponibilidade.
    - Para uma instância de três nós, suas réplicas podem ser implantadas na zona de disponibilidade de origem ou em diferentes zonas de disponibilidade. Recomendamos que você implante uma réplica na zona de disponibilidade de origem e outra réplica em uma zona de disponibilidade diferente.
    - Atualmente, apenas algumas zonas de disponibilidade de origem oferecem suporte à seleção de diferentes zonas de disponibilidade como zonas de disponibilidade de réplica. Você pode visualizar essas zonas de disponibilidade de origem e as zonas de disponibilidade de réplica compatíveis na [página de compra](https://buy.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/6b1a4c2b43587cc99c7b01d544f53cd2.png)
4. Após a conclusão do pagamento, você será redirecionado para a lista de instâncias. Depois que o status da instância mudar de **Changing configuration (Alterando configuração)** para **Running (Em execução)**, ela poderá ser usada normalmente.

## Perguntas frequentes
#### Como visualizo as informações de arquitetura de uma instância?
Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, visualize as informações de arquitetura na coluna **Configuration (Configuração)**; ou clique em um ID de instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para entrar na página de detalhes da instância, na qual você pode visualizar as informações de arquitetura na seção **Configuration Info (Informações de configuração)** > **Architecture (Arquitetura)**.
![](https://main.qcloudimg.com/raw/e783ce5c7070b8084cf03b053d7e5077.png)

#### Como visualizo as zonas de disponibilidade de origem e réplica de uma instância?
Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique em um ID de instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para entrar na página de detalhes da instância, na qual você pode visualizar as zonas de disponibilidade de origem e réplica na seção **Availability Info (Informações de disponibilidade)**.
![](https://main.qcloudimg.com/raw/f022ef04a1db5bf566cc626990e534f5.png)

