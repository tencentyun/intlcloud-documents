> Os grupos de segurança podem ser associados a CVMs, ENIs, bancos de dados em nuvem e CLBs. Neste documento, usamos os CVMs como exemplo.
>

## Cenário
Um grupo de segurança pode ser associado a um ou mais CVMs para controle de acesso à rede. Eles são uma parte importante das medidas de segurança da rede do CVM. É possível associar o CVM a um ou mais grupos de segurança, se necessário. Veja a seguir as instruções detalhadas.

##  Pré-requisitos
É necessário já ter uma instância do CVM criada antes de começar.

## Instruções
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na barra lateral esquerda, selecione **[Security Group (Grupo de segurança)](https://console.cloud.tencent.com/cvm/securitygroup)**. A página Security Group (Grupo de segurança) é exibida.
3. Selecione a região desejada e procure o grupo de segurança.
4. Em **Operation (Operação)**, clique em **Manage Instances (Gerenciar instâncias)** que correspondem ao grupo de segurança desejado. A página **Bind with Instance (Vincular à instância)** é exibida.
5. Clique em **Add Instance (Adicionar instância)**. A página **Add Instance (Adicionar instância)** é exibida.
6. Selecione as instâncias desejadas e clique em **OK** para adicionar.

## Consulte também
- Você pode verificar todos os grupos de segurança em uma região específica. 
Consulte [Visualização de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/34828).
- Se você deseja desassociar uma instância do CVM a um ou mais grupos de segurança, você pode removê-la do grupo de segurança. 
Consulte [Remoção de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/34830).
- Se um grupo de segurança não for mais necessário, é possível excluí-lo. Quando um grupo de segurança é excluído, todas as regras dele também são excluídas. 
Consulte [Exclusão de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/34831).

