Uma tabela de rotas consiste em várias políticas de roteamento que controlam a direção do tráfego de saída das sub-redes na VPC. Cada sub-rede só pode ser associada a uma tabela de rotas, já cada tabela de rotas pode ser associada a várias sub-redes. Você pode criar várias tabelas de rotas para sub-redes com rotas de tráfego diferentes.

## Tipos
Existem dois tipos de tabelas de rotas: padrão e personalizada. 
- **Tabela de rotas padrão**: ao criar uma VPC, o sistema gera automaticamente uma tabela de rotas padrão, que será associada às sub-redes criadas posteriormente se nenhuma tabela de rotas personalizada for selecionada. Você não pode excluir a tabela de rotas padrão, mas pode adicionar, excluir e modificar as políticas de roteamento nela.
- **Tabela de rotas personalizada**: você pode criar ou excluir uma tabela de rotas personalizada na VPC. Essa tabela de rotas personalizada pode ser associada a todas as sub-redes para aplicar a mesma política de roteamento.
![](https://main.qcloudimg.com/raw/a86260ffb40bec52c9f64a307d956691.png)  
>?Você pode associar uma tabela de rotas ao [criar uma sub-rede](https://intl.cloud.tencent.com/document/product/215/31806) ou [alterar a tabela de rotas](https://intl.cloud.tencent.com/document/product/215/40090) após a criação de uma sub-rede.
>

## Política de roteamento
Uma tabela de rotas controla as rotas de tráfego usando políticas de roteamento. Uma política de roteamento consiste no destino, tipo do próximo salto e próximo salto.
- **Destination (Destino)**: especifica o intervalo de IP de destino para o qual você deseja encaminhar o tráfego. Deve ser um intervalo de IP. Se você quiser inserir um único endereço IP, defina a máscara para `32` (por exemplo, `172.16.1.1/32`). O destino não pode ser um intervalo de IP da VPC onde reside a tabela de rotas, pois a rota local já permite a interconexão de rede privada neste VPC.
>?Se você implantou um [serviço TKE](https://intl.cloud.tencent.com/document/product/457/6759) na VPC, o destino configurado na política de roteamento da sub-rede da VPC não pode estar dentro do bloco CIDR da VPC nem conter o intervalo de IP do TKE.
>Por exemplo, se o bloco CIDR da VPC for `172.168.0.0/16` e o bloco CIDR do TKE for `192.168.0.0/16`, o intervalo de IP de destino não pode estar dentro de `172.168.0.0/16`, ou conter `192.168.0.0/16`, quando você configurar a política de roteamento para uma sub-rede da VPC.
>
- **Next-hop type (Tipo do próximo salto)**: indica a saída de pacotes de dados para a VPC. O tipo do próximo salto da VPC aceita **NAT Gateway**, **Peering Connection**, **VPN Gateway (Gateway do VPN)**, **Direct Connect Gateway (Gateway do Direct Connect)**, **CVM** e outros.
- **Next hop (Próximo salto)**: especifica a instância do próximo salto (identificada pelo ID do próximo salto) para a qual o tráfego é encaminhado, como um NAT Gateway em uma VPC.


### Prioridade das políticas de roteamento
Quando há várias políticas de roteamento em uma tabela de rotas, a seguinte prioridade de roteamento se aplica, de alta para baixa:
- Tráfego dentro da VPC: o tráfego dentro da VPC é correspondido primeiro.
- Rota de correspondência exata (a correspondência de prefixo mais longa): quando há várias rotas na tabela de rotas que podem corresponder ao IP de destino, a rota com a máscara mais longa (exata) é correspondida para determinar o próximo salto.
- IP público: se nenhuma política de roteamento for correspondida, uma instância da CVM pode acessar a Internet por meio de seu endereço IP público.
**Caso de uso:**
Quando uma sub-rede está associada a um NAT Gateway, e a CVM na sub-rede possui um IP público (ou EIP), a CVM acessa a Internet por meio do NAT Gateway por padrão (porque a prioridade da rota de correspondência exata é maior que a do IP público). No entanto, você pode definir uma política de roteamento para permitir que a CVM acesse a Internet usando seu endereço IP público. Para mais detalhes, consulte [Ajuste das prioridades dos NAT Gateways e EIPs](https://intl.cloud.tencent.com/document/product/1015/32734).

## ECMP 
O Roteamento de vários caminhos de custo igual (ECMP, na sigla em inglês) significa que existem várias rotas de igual custo para um único destino. A tecnologia de roteamento tradicional usa apenas um caminho para transferir pacotes para o mesmo destino, enquanto os demais caminhos estão no estado de espera ou inválido. Quando o caminho falha, leva tempo para usar outro caminho. Por outro lado, o ECMP usa várias rotas de custos iguais no ambiente de rede para aumentar a largura de banda de transmissão, equilibrar o tráfego em várias rotas e obter backup com links redundantes.

O VPC aceita o ECMP para o mesmo tipo de rota, conforme detalhado abaixo.

| Tipo do próximo salto     | Aceita o ECMP (mesmo tipo de rota)  | Quantidade máxima de ECMPs |
| -------------- | ----------------------- | --------------------------- |
| NAT Gateway        | Não                       | N/A                 |
| IP público da CVM | Não                     | N/A                 |
| CVM       | Sim                    | 8       |
| Peering Connection       | Não                     | N/A                 |
| Gateway do Direct Connect       | Sim                     | 8       |
| CCN         | Não                    | N/A                 |
| HAVIP   | Sim                    | 8       |
| Gateway do VPN        | Sim                      | 8       |

<dx-alert infotype="explain" title="">
O CCN aceita um ECMP com gateway do Direct Connect ou Peering Connection.
</dx-alert>


### Casos de uso
O ECMP é frequentemente usado para equilibrar a carga de tráfego em gateways com largura de banda limitada. Suponha que você precise de 2.000 Mbps para interconectar seus negócios baseados na VPC e IDC, mas a largura de banda máxima atual do VPN é de 1.000 Mbps. Para atingir o objetivo, você pode criar dois gateways do VPN de 1.000 Mbps e dois túneis VPN.

## Rotas principal/secundária
As rotas principal/secundária referem-se a dois ou mais caminhos para o mesmo destino, com um caminho ativo e caminhos em espera ou inválidos. Suponha que haja duas rotas da VPC para o IDC, ou seja, caminho A e caminho B. Todos os pacotes são enviados ao destino pelo caminho A, enquanto o caminho B fica inválido ou em espera. Quando o caminho A sofre falhas de ligação, você pode ativar o caminho B para assumir o tráfego do caminho A, garantindo assim a disponibilidade da aplicação. Nesse caso, os caminhos A e B são chamados de rotas principal e secundária.

O tipo do próximo salto determina a prioridade das rotas. Ao adicionar uma política de roteamento à tabela de rotas da VPC, você pode configurar diferentes tipos de gateways para atuar como rotas principal e secundária para um único destino. Depois, a investigação de rede da VPC pode ser usada para verificar a qualidade e a acessibilidade da ligação. Após configurar uma política de alarme, você pode detectar prontamente qualquer exceção de ligação e alternar com rapidez entre as rotas principal e secundária para atender aos requisitos de alta disponibilidade.
>?
>+ Atualmente, a funcionalidade de prioridade de rotas está na versão beta. Para usá-la, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).
>+ O tipo do próximo salto determina a prioridade da rota na tabela de rotas da VPC. Por padrão, a prioridade de rota de alta para baixa é CCN, gateway do Direct Connect, gateway do VPN e outros.
>+ Atualmente, você não pode ajustar a prioridade das rotas no console. Se necessário, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).

A tabela a seguir descreve se as rotas principal/secundária são aceitas em diferentes tipos de rotas da VPC.

| Tipo do próximo salto         | Aceita rotas principal/secundária                                            |
| ------------------ | ------------------------------------------------------- |
| NAT Gateway            | Não                                                      |
| IP público da CVM     | Não                                                      |
| CVM          | Sim, com CCN, gateway do VPN, gateway do Direct Connect ou HAVIP  |
| Peering Connection (intrarregião) | Não                                                      |
| Peering Connection (entre regiões) | Não                                                      |
| Gateway do Direct Connect          | Sim, com CCN, gateway do VPN, HAVIP ou CVM  |
| CCN          | Sim, com gateway do VPN, gateway do Direct Connect, HAVIP ou CVM  |
| HAVIP          | Sim, com CCN, gateway do VPN, gateway do Direct Connect ou CVM  |
| Gateway do VPN         | Sim, com CCN, gateway do Direct Connect, HAVIP ou CVM  |


### Casos de uso
As rotas principal/secundária são frequentemente usadas para encaminhar o tráfego continuamente quando uma ligação de gateway falha.
+ Gateway do Direct Connect baseado na VPC (principal) e gateway do VPN para a VPC (secundária)
  **Cenário**: interconecte uma VPC da Tencent Cloud e um IDC local por meio de um gateway do Direct Connect baseado na VPC. Enquanto isso, crie túneis VPN por meio de um gateway do VPN para atuar como o vínculo de comunicação secundário entre o IDC e a VPC.
   ![](https://main.qcloudimg.com/raw/683779ec1aef376985b027df945fe54c.png)
+ Gateway do Direct Connect baseado no CCN (principal) e gateway do VPN para a VPC (secundária)
  **Cenário**: interconecte uma VPC da Tencent Cloud e um IDC local por meio de uma instância do CCN. Enquanto isso, crie túneis VPN por meio de um gateway do VPN para atuar como o vínculo de comunicação secundário entre o IDC e a VPC.
	![](https://main.qcloudimg.com/raw/7e21527a285edb29c7e57df566723acb.png)
