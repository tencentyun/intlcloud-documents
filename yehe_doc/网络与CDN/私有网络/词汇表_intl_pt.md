## C

### CIDR

Consulte [CIDR](https://intl.cloud.tencent.com/document/product/215/4925).

## E

### EIP

Consulte [IP elástico](https://intl.cloud.tencent.com/document/product/215/4925).

## G

### IP público

Um IP público pode ser acessado pela Internet, e é usado para a comunicação entre a instância e a Internet ou outros recursos da Tencent Cloud (como recursos de banco de dados) com pontos de extremidade públicos.

### Gateway público

Um gateway público é uma CVM que pode encaminhar o tráfego entre a Internet e as VPCs. Um CVM sem um IP público pode acessar a Internet por meio de um gateway público.

## J

### Rede clássica

A rede clássica é o pool de recursos de rede pública para todos os usuários da Tencent Cloud. A Tencent Cloud atribui IPs privados às CVMs na rede clássica. Ela possui uma configuração simples e é de fácil uso, tornando-a adequada para os usuários que precisam de alta usabilidade e início rápido com as CVMs. Por outro lado, a VPC é adequada para os usuários com recursos e necessidades de gerenciamento de rede.
Para mais informações, consulte [Comunicação com a rede clássica](https://intl.cloud.tencent.com/document/product/215/35505).

## K

## Zona de disponibilidade

Uma zona de disponibilidade é um IDC físico da Tencent Cloud com fonte de alimentação e rede independentes em uma única região. Ela pode garantir a estabilidade dos negócios, pois as falhas em uma zona de disponibilidade são isoladas sem afetar outras zonas de disponibilidade na mesma região.

## N

### IP privado

Um IP privado é um endereço IP atribuído a uma instância em uma VPC da Tencent Cloud ou rede clássica, e não pode ser acessado pela Internet. Ele pode ser usado para comunicação entre instâncias em uma VPC ou redes clássicas.

## S

### VPC

A VPC cria um espaço de rede isolado na Tencent Cloud, que é semelhante a uma rede tradicional executada em seus IDCs. A VPC hospeda os seus recursos da Tencent Cloud, incluindo a [Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213), o [Cloud Load Balancers](https://intl.cloud.tencent.com/document/product/214), o [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236) etc. Em vez de se preocupar com a aquisição e operação de dispositivos de rede, você pode se concentrar em personalizar intervalos de IP, endereços IP, políticas de roteamento etc. Você pode acessar a Internet facilmente por meio de [EIP](https://intl.cloud.tencent.com/document/product/213/16586), [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015) e [Gateway público](https://intl.cloud.tencent.com/document/product/213/34835), e conectar a VPC aos seus IDCs pelo [VPN](https://intl.cloud.tencent.com/document/product/1037)/[Direct Connect](https://intl.cloud.tencent.com/document/product/216). O [Peering Connection](https://intl.cloud.tencent.com/document/product/553) da VPC da Tencent Cloud permite implementar um servidor unificado para acesso global e recuperação de desastres 2-regiões-3-DC. Além disso, o grupo de segurança e a [ACL de rede](https://intl.cloud.tencent.com/document/product/215/31850) da VPC da Tencent Cloud podem atender totalmente às suas necessidades de segurança de rede.

## T

### EIP

Um IP elástico é um endereço IP público que pode ser solicitado independentemente. Ele permite a vinculação e desvinculação dinâmicas. Você pode vinculá-lo ou desvinculá-lo da CVM (ou instâncias do NAT Gateway) em sua conta. Os seus principais usos são:

1. Reter um IP. A declaração ICP do nome de domínio é necessária para IP e DNS da China Continental.
2. Mascarar uma falha de instância. Por exemplo, um nome DNS é mapeado para um endereço IP por meio do mapeamento dinâmico de DNS. Pode levar até 24 horas para propagar esse mapeamento para toda a Internet, enquanto um IP elástico permite o remapeamento rápido de um IP de uma CVM para outro. Quando uma CVM falha, você pode simplesmente iniciar e remapear outra instância para responder rapidamente a falhas de instância.

## V

### VPC

Consulte [VPC](https://intl.cloud.tencent.com/document/product/215/4925).

## W

### CIDR

O roteamento entre domínios sem classe (CIDR, na sigla em inglês) é um bloco de endereço de espaço de rede independente especificado pelo usuário. Ele combina IP e mascaramento para alcançar a divisão de rede. No exemplo de `10.1.0.0/16`, `10.1.0.0` é o endereço IP do bloco de rede e `16` é a máscara do bloco de rede. Você pode redimensionar o bloco de rede ajustando o tamanho da máscara. A quantidade de IPs em um bloco de rede é igual a 2 ^ (32 máscaras), e o bloco de rede `10.1.0.0/16` tem no máximo 65.536 endereços IP.