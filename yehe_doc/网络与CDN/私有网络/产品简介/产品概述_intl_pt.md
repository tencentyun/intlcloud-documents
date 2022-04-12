Um Virtual Private Cloud (VPC) é um espaço de rede logicamente isolado. Com o VPC, você pode configurar um espaço de rede logicamente isolado para os seus recursos, como os [CVMs](https://intl.cloud.tencent.com/document/product/213/495) e os [bancos de dados em nuvem](https://intl.cloud.tencent.com/document/product/236). Esse produto oferece melhor segurança de recursos de nuvem e pode atender às suas necessidades em vários cenários.

Este documento apresenta os componentes principais, os modos de conexão e a segurança dos VPCs.
## Componentes principais
Uma instância do VPC tem três componentes principais: intervalos de IP do VPC, sub-redes e tabelas de rotas.
### Intervalos de IP do VPC
Ao criar um VPC, você precisa especificar um [bloco CIDR (roteamento entre domínios sem classe)](http://intl.cloud.tencent.com/document/product/215/4925) como o grupo de endereços IP do VPC.

O VPC da Tencent Cloud é compatível com blocos CIDR em qualquer um dos seguintes intervalos de IP privados:
- **10.0**.0.0 - **10.255**.255.255 (**o intervalo das máscaras deve ser de 16 a 28**)
- **172.16**.0.0 - **172.31**.255.255 (**o intervalo das máscaras deve ser de 16 a 28**)
- **192.168**.0.0 - **192.168**.255.255 (**o intervalo das máscaras deve ser de 16 a 28**)

### Sub-redes
Um VPC é composto por pelo menos uma sub-rede. Todos os recursos de nuvem em um VPC (como CVMs e bancos de dados em nuvem) devem ser implantados em uma sub-rede, e o bloco CIDR da sub-rede deve estar dentro do bloco CIDR do VPC.

Um VPC é configurado no nível da [região](https://intl.cloud.tencent.com/document/product/215/31786) (como Guangzhou), já uma sub-rede é configurada no nível da [zona de disponibilidade](https://intl.cloud.tencent.com/document/product/215/31786) (como Zona 1 de Guangzhou). É possível dividir um VPC em uma ou mais sub-redes. As sub-redes no mesmo VPC podem se interconectar por padrão, já as sub-redes em VPCs diferentes são isoladas por padrão.
![](https://main.qcloudimg.com/raw/9fe1af6b2ee439449a6fefa64663215c.png)

### Tabelas de rotas
Quando você cria um VPC, o sistema gera automaticamente uma tabela de rotas padrão para garantir que todas as sub-redes do VPC estejam interconectadas. Se as políticas de roteamento na tabela de rotas padrão não puderem atender às suas necessidades de negócios, você poderá criar uma tabela de rotas personalizada.

Para mais informações sobre tabelas de rotas, consulte [Visão geral de tabelas de rotas](https://intl.cloud.tencent.com/document/product/215/31810).

## Conexões do VPC
A Tencent Cloud fornece uma ampla variedade de soluções de conexão do VPC para diferentes cenários.
- Os CVMs e os bancos de dados em nuvem em um VPC podem se conectar à Internet por IP elástico e NAT Gateway.
- O Peering Connection e o Cloud Connect Network são usados para habilitar a comunicação entre os VPCs.
- Os VPCs e os IDCs locais são interconectados por meio do VPN Connection, do Direct Connect e do Cloud Connect Network. 


## Segurança do VPC
Um VPC é um espaço de rede logicamente isolado na nuvem. Os VPCs diferentes são isolados uns dos outros para proteger a segurança dos negócios.
- Grupo de segurança: um grupo de segurança é um firewall virtual com estado capaz de filtrar pacotes. Ele controla o tráfego de entrada e de saída no nível da instância, e é um meio importante de isolamento de segurança de rede.
- Lista de controle de acesso (ACL) de rede: uma ACL de rede é um firewall virtual sem estado para filtrar pacotes no nível de sub-rede. Ela pode ser usada para controlar os fluxos de dados de entrada e de saída de sub-redes na granularidade de protocolo e de porta.
- Cloud Access Management (CAM): o CAM ajuda você a gerenciar com segurança o acesso aos seus recursos da Tencent Cloud. Por exemplo, o CAM fornece gerenciamento de identidade e de políticas para que você possa controlar quem tem acesso aos VPCs.

Para mais informações sobre a segurança do VPC, consulte [Gerenciamento de segurança](https://intl.cloud.tencent.com/document/product/215/31848).
