Um VPC é uma rede virtual isolada logicamente que você pode usar exclusivamente e planejar de forma independente no Tencent Cloud. Para usar qualquer recurso do Tencent Cloud, é necessário criar um VPC e uma sub-rede. Uma sub-rede é um espaço de rede no VPC. Você pode dividir um VPC em pelo menos uma sub-rede. O VPC é regional, já a sub-rede é específica da zona de disponibilidade. As sub-redes no mesmo VPC podem se comunicar entre si por meio de uma rede privada, por padrão.

Todos os recursos de nuvem, como os CVMs e os CLBs em um VPC, devem ser implantados em uma sub-rede.


## Ciclo de vida do VPC
O ciclo de vida do VPC varia com as necessidades, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/68556cee99a7ececc3936b45cdaa3ca5.svg)
1. [Criação de um VPC](https://intl.cloud.tencent.com/document/product/215/31805): é necessário [planejar sua rede](https://intl.cloud.tencent.com/document/product/215/31795) cuidadosamente antes de criar um VPC. Os blocos CIDR de VPCs e sub-redes não podem ser modificados após a criação.
2. [Exibição de um VPC](https://intl.cloud.tencent.com/document/product/215/40069): é possível exibir as informações básicas de um VPC, sua associação ao CCN e os recursos que ele contém.
3. (Opcional) Escolha as operações que se aplicam aos seus casos de uso:
 - Quando o bloco CIDR principal for insuficiente, consulte [Edição de blocos CIDR IPv4](https://intl.cloud.tencent.com/document/product/215/40070):
    - [Criação de blocos CIDR secundários](https://intl.cloud.tencent.com/document/product/215/40070#21): é possível criar blocos CIDR secundários para atender às demandas reais da rede.
    - [Exclusão de blocos CIDR secundários](https://intl.cloud.tencent.com/document/product/215/40070#32): é possível excluir os blocos CIDR secundários se não precisar mais deles.
4. [Exclusão de um VPC](https://intl.cloud.tencent.com/document/product/215/40073): após um VPC for excluído, suas sub-redes e tabelas de rota também serão excluídas.

