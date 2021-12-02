Uma tabela de rotas consiste em várias políticas de roteamento e é usada para controlar as rotas de tráfego de saída de sub-redes no VPC. Cada sub-rede pode ser associada a uma tabela de rotas, já cada tabela de rotas pode ser associada a várias sub-redes. É possível criar várias tabelas de rotas para sub-redes com rotas de tráfego diferentes.

## Tipo
Existem dois tipos de tabelas de rotas: tabelas de rotas padrão e personalizadas:
- Quando um usuário cria um VPC, o sistema gera automaticamente uma tabela de rotas padrão para ele. Uma sub-rede criada posteriormente será associada de forma automática à tabela de rotas padrão, se nenhuma tabela de rotas personalizada for selecionada. Não é possível excluir a tabela de rotas padrão, mas é possível adicionar, excluir e modificar as políticas de roteamento nela.
- Você pode criar uma tabela de rotas personalizada no VPC, e as tabelas de rotas personalizadas podem ser excluídas. É possível estabelecer uma tabela de rotas personalizada para as sub-redes com a mesma política de roteamento, e associá-la a todas as sub-redes que precisam seguir esta política de roteamento.
  

Você pode associar uma tabela de rotas ao [criar uma sub-rede](https://intl.cloud.tencent.com/document/product/215/31806) ou [alterar a tabela de rotas associada a uma sub-rede](https://intl.cloud.tencent.com/document/product/215/31806) após a criação de uma sub-rede.

## Política de roteamento
Uma tabela de rotas controla as rotas de tráfego usando políticas de roteamento. Uma política de roteamento consiste no destino, tipo de próximo salto e próximo salto.
- **Destino**: refere-se ao intervalo de IP de destino para o qual você deseja encaminhar o tráfego. A descrição do intervalo de IP de destino aceita apenas o formato de intervalo de IP. Se quiser que o destino seja um único endereço IP, você pode definir a máscara para `32` (como `172.16.1.1/32`). O destino não pode ser o intervalo de IP no VPC da tabela de rotas, porque o roteamento local já indica a intercomunicação de rede privada padrão neste VPC.
- **Tipo de próximo salto**: indica a saída para pacotes de dados do VPC. O tipo de próximo salto de VPC aceita **NAT Gateway**, **Peering Connection**, **VPN Gateway**, **Direct Connect Gateway (Gateway do Direct Connect)**, **CVM** e outros.
- **Próximo salto**: especifica a instância do próximo salto (representada pelo uso do ID do próximo salto), como um NAT Gateway em um VPC.

### Prioridade das políticas de roteamento
Quando há várias políticas de roteamento em uma tabela de rotas, a seguinte prioridade de roteamento se aplica, de alta para baixa:
- Tráfego dentro do VPC: o tráfego dentro do VPC é correspondido primeiro.
- Roteamento mais preciso (correspondência de prefixo mais longa): quando há várias entradas na tabela de rotas que podem corresponder ao IP de destino, a rota com a máscara mais longa (mais precisa) é usada como correspondência para confirmar o próximo salto.
- IP público: se a correspondência falhar para todas as políticas de roteamento, a internet pode ser acessada por meio do IP público.

### Explicação das prioridades do NAT Gateway/EIP
Quando uma sub-rede estiver associada a um NAT Gateway, e o CVM na sub-rede tiver um IP público (ou EIP), ele acessará a internet por meio do NAT Gateway por padrão (porque a prioridade da rota mais precisa é maior do que a do IP público). No entanto, é possível definir uma política de roteamento para permitir o acesso à internet usando o IP público do CVM. Para obter informações detalhadas, consulte [Ajuste das prioridades dos NAT Gateways e EIPs](https://intl.cloud.tencent.com/document/product/1015/32734).
