## Cenário

É possível modificar o IP privado de uma instância do CVM no VPC diretamente no console ou alterando a sub-rede da instância do CVM. Este documento descreve como modificar o IP privado de uma instância do CVM no console do VPC.
Para obter detalhes sobre como alterar a sub-rede, consulte [Alterar sub-rede da instância](http://intl.cloud.tencent.com/document/product/213/16565).

## Limites

- A modificação do IP principal de um ENI principal pode fazer com que o CVM reinicie.
- O IP principal de um ENI secundário não pode ser modificado.

## Direções

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Selecione a região da instância cujo IP privado você deseja modificar e clique no ID/nome da instância para entrar em sua página de detalhes.
3. Na página de detalhes da instância, selecione a guia [ENI] e clique em <img src = "https://main.qcloudimg.com/raw/57a0c76b72cd97bd80bf857cd30c867a.png" style = "margin: 0;"> para expandir o ENI principal.
4. Na lista de operações do ENI principal, clique em **Modify Primary IP (Modificar o IP principal)**.
5. Na janela “Modify Primary IP (Modificar o IP principal)” que é exibida, insira o novo IP e clique em **OK**. A alteração entra em vigor depois que a instância é reiniciada.
>! Só é possível inserir o IP privado no CIDR da sub-rede atual.
>

