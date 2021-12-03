O mapa de topologia da rede exibe todos os recursos do VPC, para que você possa obter implantações e conexões do VPC em tempo real.

## Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Clique em **Network Topology Map (Mapa de topologia da rede)** na barra lateral esquerda.
    ![](https://main.qcloudimg.com/raw/c7e8ecf743767784df696cf149413d75.png)
3. Selecione uma região e VPC para exibir os recursos de nuvem do VPC, como CVM, CLB, TencentDB e NoSQL, e sua relação de topologia de rede.
  Nas duas sub-redes do VPC de exemplo, conforme mostrado abaixo, a sub-rede `test6` contém duas instâncias do CLB. Esse VPC se comunica com a internet por meio do NAT Gateway e da rede pública do CLB. Ele se comunica com o VPC oposto por meio do Peering Connection.
    ![](https://main.qcloudimg.com/raw/1cc6ff3a212bc7ef26b261ba8610cba5.png)
