## Visão geral
Uma função do Cloud Access Management (CAM) é uma identidade virtual com um conjunto de permissões. É usada para conceder à entidade de função as permissões para acessar serviços e recursos e realizar operações no Tencent Cloud. É possível associar a função do CAM a uma instância do CVM para chamar outras APIs do Tencent Cloud da instância usando a chave temporária do serviço de token de segurança (STS) atualizada periodicamente. Isso garante a segurança da sua chave secreta e ajuda a implementar um controle de permissão refinado, evitando os riscos de segurança do uso de chaves persistentes.

Este documento descreve como vincular, modificar e excluir uma função.

## Vantagens
Vincular uma função do CAM a instâncias traz as seguintes funcionalidades e vantagens.
- Você pode acessar outros serviços do Tencent Cloud usando chaves temporárias do STS. Para obter mais informações, consulte [APIs do STS](https://intl.cloud.tencent.com/document/product/598/35840).
- É possível conceder funções associadas a diferentes políticas de acesso a instâncias para que as instâncias recebam diferentes permissões de acesso aos recursos do Tencent Cloud, o que ajuda a implementar um controle de permissão refinado.
- Você não precisa salvar a chave secreta em uma instância. Em vez disso, você pode controlar facilmente as permissões de acesso da instância alterando a autorização da função.




## Instruções de uso
- A instância permite apenas que a entidade de função que contém `cvm.qcloud.com` assuma a função. Para obter mais informações, consulte [Conceitos](https://intl.cloud.tencent.com/document/product/598/19421).
- A instância deve estar localizada em um VPC.
- Uma instância pode vincular apenas uma função do CAM por vez.
- Você pode vincular, modificar ou excluir uma função sem pagar taxas extras.


## Direções

### Vinculação/modificação de funções
#### Vinculação/modificação da função de um CVM
1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm) e clique em **Instances (Instâncias)** na barra lateral esquerda.
2. Na página **Instances (Instâncias)**, selecione a instância do CVM para a qual deseja vincular ou modificar a função e, em seguida, clique em **More (Mais)** > **Instance Settings (Configurações da instância)** > **Bind/Modify a Role (Vincular/Modificar uma função)** na coluna **Operation (Operação)**, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/34d5a9866aa28fdb8a3363884918e3bb.png)
3. Na janela pop-up, selecione a função que deseja vincular e clique em **OK**.
#### Vinculação/modificação de funções em lote
1. Na página **Instances (Instâncias)**, selecione as instâncias do CVM para as quais deseja vincular ou modificar as funções, clique em **More Actions (Mais ações)** > **Instance Settings (Configurações da instância)** > **Bind/Modify a Role (Vincular/Modificar uma função)** no topo da lista, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/4093443ee4f5b484860f8c8eae3b3b3e.png)
2. Na janela pop-up, selecione a função que deseja vincular e clique em **OK**.
>?Os CVMs modificados usando este método terão o mesmo nome de função.



### Exclusão de funções
#### Exclusão da função de um CVM
1. Na página **Instances (Instâncias)**, localize a instância do CVM da qual deseja excluir a função, clique em **More (Mais)** > **Instance Settings (Configurações da instância)** > **Delete a Role (Excluir uma função)** na coluna **Operation (Operação)**, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/8b44772763ab60fa69c404360db1ebbf.png)
2. Clique em **OK** na janela pop-up.
#### Exclusão de funções em lote
1. Na página **Instances (Instâncias)**, selecione as instâncias do CVM das quais deseja excluir as funções, clique em **More Actions (Mais Ações)** > **Instance Settings (Configurações da instância)** > **Delete a Role (Excluir uma função)** acima da lista, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/72669a0d3bbdde1491c24b5acc0eadbf.png)
2. Clique em **OK** na janela pop-up.



