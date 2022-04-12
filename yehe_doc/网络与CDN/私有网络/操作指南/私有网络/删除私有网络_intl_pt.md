Quando uma VPC não está mais em uso e não tem outros recursos (Peering Connections, ClassicLink, NAT Gateway, gateway do VPN, gateway do Direct Connect, CCN e conexão privada), exceto sub-redes vazias, tabelas de roteamento e ACLs de rede, ela pode ser excluída.
>?Uma sub-rede vazia se refere a uma sub-rede que não usa nenhum IP; ou seja, quando há apenas sub-redes vazias, tabelas de roteamento e ACLs de rede em uma VPC, a VPC pode ser excluída; quando há uso de IP em uma sub-rede, a VPC não pode ser excluída.
>

## Instruções
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região da VPC na parte superior da página **VPC**.
3. Na lista de VPCs, localize a VPC a ser excluída, clique em **Delete (Excluir)** na coluna **Operation (Operação)** e confirme a exclusão.
![](https://qcloudimg.tencent-cloud.cn/raw/ac7203b074651d3a7bab148496094054.png)
