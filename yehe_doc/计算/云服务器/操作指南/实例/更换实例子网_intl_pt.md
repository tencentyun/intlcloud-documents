## Visão geral
Este documento descreve como alterar a sub-rede de uma instância do CVM no VPC pelo console.

## Limites

- O CVM associado reinicia automaticamente depois que sua sub-rede é alterada.
- A sub-rede do ENI secundário não pode ser alterada.

## Direções

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Em **Instances (Instâncias)**, selecione a região a qual a instância cuja sub-rede precisa ser alterada pertence.
3. Localize a instância cuja sub-rede precisa ser alterada, clique em seu ID/nome e entre na página de detalhes da instância.
4. Selecione a guia **ENI**, clique no ID do ENI principal, 
e entre na página de gerenciamento do ENI, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/feeec3ecd76a2f5710d1b775b9f7f1d9.png)
5. Clique em **Change Subnet (Alterar sub-rede)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/713d6383b128a66ae25f5342a7387631.jpg)
6. Selecione uma nova sub-rede na caixa pop-up. Insira um novo IP e clique em **OK**, conforme mostrado abaixo:
A configuração entrará em vigor depois que a instância for reiniciada.
>! 
> - Crie uma sub-rede se não for possível encontrar nenhuma sub-rede nesta zona de disponibilidade.
> - Apenas o endereço IP privado do CIDR da sub-rede atual pode ser usado como o novo IP.
>
![](https://main.qcloudimg.com/raw/58c3534b2d6c9da255c5a32bbde8a4c1.png)
