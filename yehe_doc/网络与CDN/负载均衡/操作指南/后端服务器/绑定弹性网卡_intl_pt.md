## Visão geral do ENI
O [Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/document/product/576/18525) se refere ao tipo de interfaces de rede virtuais que podem ser vinculadas a instâncias do CVM em VPCs. Um ENI pode ser migrado livremente entre instâncias do CVM dentro do mesmo VPC e da mesma zona de disponibilidade, ajudando você a criar com facilidade clusters de alta disponibilidade, implementar failover de baixo custo e gerenciar redes de maneira mais refinada.
Os servidores de back-end do CLB podem ser vinculados ao CVM e ao ENI. Especificamente, uma instância do CLB se comunica com o servidor de back-end pela rede privada e, se várias instâncias do CVM e ENIs estiverem vinculados à instância do CLB, o tráfego de acesso será encaminhado para os IPs privados das instâncias do CVM e dos ENIs.
> Atualmente, a funcionalidade de vinculação do ENI do CLB está em teste beta. Se desejar usá-la, [envie um tíquete](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=163&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB) para solicitar.

## Pré-requisitos
Um ENI deve ser vinculado a uma instância do CVM antes de poder ser vinculado a uma instância do CLB. Como uma instância do CLB apenas encaminha o tráfego como um balanceador de carga, mas não processa a lógica de negócios, a instância do CVM, como um recurso de computação, é necessária para processar as solicitações do usuário. Primeiro, faça login no [Console do ENI](https://console.cloud.tencent.com/vpc/eni) para vincular o ENI necessário à instância do CVM.
![](https://main.qcloudimg.com/raw/3d7c79999350a4b80e0a2b2f546b559f.png)

## Instruções
1. Primeiro, é necessário configurar um listener do CLB. Para obter mais informações, consulte a [Visão geral de listeners do CLB](https://intl.cloud.tencent.com/document/product/214/6151).
2. Clique em **+** à esquerda do listener criado para expandir os nomes de domínio e caminhos de URL, selecione o caminho de URL desejado e exiba o servidor de back-end existente vinculado à direita do listener.
![](https://main.qcloudimg.com/raw/0c0ed8c9e456cfb52126f34537f0f779.png)
3. Clique em **Bind (Vincular)** e selecione o servidor de back-end a ser vinculado e configure a porta e o peso do servidor na janela pop-up. Você pode selecionar "CVM" ou "ENI" como o servidor de back-end.
 - CVM: você pode vincular os IPs privados principais dos ENIs principais de todas as instâncias do CVM no mesmo VPC que a instância do CLB.
 - ENI: você pode vincular os IPs de todos os ENIs no mesmo VPC que a instância do CLB, exceto os IPs privados principais dos ENIs principais de instâncias do CVM, como IPs privados secundários de ENIs principais e IPs privados de ENIs secundários. Para obter mais informações sobre os tipos de IPs de ENIs, consulte [ENI - Principais conceitos](https://intl.cloud.tencent.com/document/product/576/18526). 
![](https://main.qcloudimg.com/raw/89fdb725e535b81361d9a80ab0984e7a.png)
4. A configuração específica após a vinculação é mostrada conforme abaixo:
![](https://main.qcloudimg.com/raw/46defc2ad3e445e4acd6808c22aeb937.png)
