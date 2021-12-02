Depois que a tabela de rotas for criada, ela precisará ser associada à sub-rede para controlar o tráfego de saída da sub-rede. Este documento descreve como associar a tabela de rotas ou desassociá-la da sub-rede.

## Associação à sub-rede
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Route Tables (Tabelas de rotas)** na barra lateral esquerda para acessar a página de gerenciamento.
3. Existem dois métodos para associar à sub-rede:
 + Na lista, selecione a tabela de rotas que precisa ser associada à sub-rede e clique em **More (Mais)** > **Associated Subnets (Sub-redes associadas)** na coluna **Operation (Operação)**.
![](https://main.qcloudimg.com/raw/0e8f63501b1a2c8c8c99d4f9d838b4e3.png)
 + Clique no ID da tabela de rotas para acessar a página de detalhes, selecione a guia **Associated Subnets (Sub-redes associadas)** e clique em **+Associate Subnet (+Associar sub-rede)**.
![](https://main.qcloudimg.com/raw/6e814d4f11035afba7f35100ef4bcde6.png)
4. Na janela pop-up, selecione a sub-rede a ser associada (uma tabela de rotas pode ser associada a várias sub-redes ao mesmo tempo e é possível filtrar rapidamente por ID/nome da sub-rede). Avalie o impacto comercial da associação na sub-rede. Confirme o impacto e clique em **OK**.
>!Depois que a tabela de rotas for associada à sub-rede, a tabela de rotas original associada à sub-rede será substituída pela nova, e o tráfego de saída da sub-rede será executado de acordo com as políticas na nova tabela de rotas. Avalie cuidadosamente o impacto na empresa.
  >


## Desassociação da sub-rede
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Route Tables (Tabelas de rotas)** na barra lateral esquerda para acessar a página de gerenciamento.
3. Clique no ID da tabela de rotas para acessar a página de detalhes, alterne para a guia **Associated Subnets (Sub-redes associadas)** e clique em **Disassociate (Desassociar)**.
![](https://main.qcloudimg.com/raw/077e50e31696c2f9733d3e7030a8e709.png)
4. Na janela pop-up, selecione uma nova tabela de rotas para a sub-rede a ser desassociada e clique em **OK** para completar a dissociação da tabela de rotas atual da sub-rede. A política de tráfego de saída da sub-rede será executada com base na nova tabela de rotas selecionada para ela.

