## Agosto de 2021
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="40%">Descrição</th>
<th width="15%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody>
 <tr>
<td>Abre a funcionalidade de bloco CIDR secundário para todos os usuários</td> 
<td>A funcionalidade de CIDR secundário é aberta a todos os usuários. Você pode editar diretamente os blocos CIDR secundários no console da VPC sem a necessidade de solicitar permissões adicionais.</td> 
<td>08-2021</td> 
<td><a href="https://intl.cloud.tencent.com/document/product/215/40070">Edição de blocos CIDR IPv4</a></td> 
</tbody>
</table>



## Novembro de 2020
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Aumento de cotas</td>
<td>As cotas dos seguintes recursos foram aumentadas:<ul><li>A quantidade de VPCs por conta por região foi ajustada para 20</li><li>A quantidade de sub-redes por VPC foi ajustada para 100</li><li>A quantidade de ENIs secundários foi ajustada para 1.000</li></ul>
</td>
<td>11-2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/38959">Limite de cota</a></td>
</tr>
</tbody></table>

## Dezembro de 2019
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Exibe a hora da última modificação nas regras do grupo de segurança</td>
<td>É fornecido o atributo “Last Modification Time (Hora da última modificação)”, que registrará a última hora de criação ou modificação e facilitará a solução de problemas.</td>
<td>12-2019</td>
<td>-</td>
</tr>
</tbody></table>

## Novembro de 2019
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Abre o HAVIP para todos os usuários</td>
<td>Um IP virtual de alta disponibilidade (HAVIP) é um endereço IP privado flutuante que permite a vinculação a um servidor usando o anúncio ARP, para atualizar o mapeamento entre o endereço IP e o endereço MAC. Em um cenário de implantação de alta disponibilidade (como o keepalived), esse endereço IP pode ser alternado do servidor principal para o servidor secundário para recuperação de desastres do serviço.</td>
<td>11-2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31817" target="_blank">Casos de uso</a></td>
</tr>
<tr>
<td>Grupos de segurança que permitem a adição de regras IPv6</td>
<td>Ao adicionar regras IPv6 do grupo de segurança, você pode ativar ou desativar o acesso à rede pública ou privada para as CVMs IPv6 em um grupo de segurança.</td>
<td>11-2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35513" target="_blank">Adição de regras de grupo de segurança</a></td>
</tr>
</tbody></table>

## Julho de 2019
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Aceita tags para VPCs</td>
<td>Os VPCs, as sub-redes e as tabelas de rotas aceitam tags de nível de recurso, que podem ajudar você a gerenciar melhor as permissões de recursos para subusuários e colaboradores.</td>
<td>07-2019</td>
<td>-</td>
</tr>
</tbody></table>

## Dezembro de 2018
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Lança a ferramenta de verificação de portas de instâncias</td>
<td>A funcionalidade de verificação de portas de instâncias pode ajudar você a verificar a acessibilidade das portas do grupo de segurança de instâncias da CVM e a localizar rapidamente falhas, melhorando a experiência do usuário.</td>
<td>12-2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31875" target="_blank">Verificação de portas de instâncias </a></td>
</tr>
</tbody></table>

## Outubro de 2018
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Permite abrir todas as portas comuns em um grupo de segurança com uma operação de um clique</td>
<td>A ativação de portas com uma operação de um clique é aplicável a cenários em que as regras do protocolo ICMP não precisam ser definidas e as operações podem ser concluídas pelas portas 22, 3389, ICMP, 80, 443, 20 e 21.</td>
<td>10-2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35513" target="_blank">Adição de regras de grupo de segurança </a></td>
</tr>
</tbody></table>

## Junho de 2018
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Aceita o conjunto de opções do DHCP</td>
<td>O DHCP é um protocolo de rede LAN que define o padrão para entrega de configurações para servidores de rede TCP/IP. As CVMs nas VPCs da Tencent Cloud aceitam o DHCP. Você pode configurar os dois parâmetros na página de detalhes da VPC. Essas configurações entrarão em vigor para todos as CVMs nessa VPC.</td>
<td>06-2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31808" target="_blank">Modificação de endereços DNS e nomes de domínio</a></td>
</tr>
<tr>
<td>Lança a funcionalidade de sondagem de rede</td>
<td>O serviço de sondagem de rede da Tencent Cloud é usado para monitorar a qualidade das conexões de rede da VPC, incluindo a latência, a taxa de perda de pacotes e outras métricas importantes. Você pode localizar problemas com rapidez definindo alertas e monitoramento multidimensional por meio da sonda de rede. Também pode criar um objeto de sonda de rede em uma sub-rede para monitorar a qualidade da conexão em tempo real, de modo a melhorar a estabilidade dos negócios.</td>
<td>06-2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35522" target="_blank">Sonda de rede</a></td>
</tr>
</tbody></table>

## Fevereiro de 2018
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Permite a vinculação de um TencentDB baseado na VPC a um grupo de segurança</td>
<td>Os grupos de segurança podem ser vinculados ao TencentDB e outros produtos relevantes. Você pode vincular um grupo de segurança a instâncias do TencentDB. Um grupo de segurança é um firewall virtual com estado que realiza a filtragem de pacotes de dados. Ele pode ser usado para definir o controle de acesso à rede para instâncias como CVMs e ENIs, e também permite o controle de acesso à rede para as instâncias do TencentDB em VPCs. Portanto, um grupo de segurança pode melhorar efetivamente a segurança do TencentDB.</td>
<td>02-2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/34832" target="_blank">Vinculação de instâncias a grupos de segurança</a></td>
</tr>
<tr>
<td>As VPCs e os grupos de segurança aceitam a auditoria de operações</td>
<td>As VPCs e os grupos de segurança aceitam o CloudAudit, que pode obter os registros históricos de chamadas de API em sua conta da Tencent Cloud, incluindo chamadas de API por meio do console da Tencent Cloud, do SDK da Tencent Cloud, ferramenta de linha de comando e outros serviços da Tencent Cloud. Isso significa que qualquer comportamento de implantação na Tencent Cloud é monitorado, e você pode descobrir os subusuários e colaboradores que usam as APIs da Tencent Cloud, os endereços IP de origem dos quais as APIs são chamadas e quando são chamadas.</td>
<td>02-2018</td>
<td>-</td>
</tr>
</tbody></table>

## Junho de 2017
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Grupos de segurança que permitem o controle de acesso</td>
<td>Fornecemos a funcionalidade de gerenciamento de permissões de usuários em grupos de segurança para tornar o seu serviço mais seguro.</td>
<td>06-2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35498" target="_blank">Visão geral do controle de acesso</a></td>
</tr>
<tr>
<td>Grupos de segurança que permitem modelos de parâmetros</td>
<td>Um modelo de parâmetros é um conjunto de parâmetros. Você pode salvar endereços IP e portas de protocolo como um modelo para que possa importar diretamente o modelo ao adicionar regras de grupo de segurança. Se usados corretamente, os modelos de parâmetros podem aumentar a eficiência no uso de grupos de segurança.</td>
<td>06-2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31867" target="_blank">Gerenciamento de modelos de parâmetros</a></td>
</tr>
<tr>
<td>Atualiza a funcionalidade de monitoramento</td>
<td>O sistema permite a exibição de dados de alarme e monitoramento de várias métricas importantes e pode obter os dados por meio de APIs para garantir uma operação estável e tranquila dos seus serviços.</td>
<td>06-2017</td>
<td>-</td>
</tr>
</tbody></table>

## Maio de 2017
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Grupos de segurança que permitem o controle de acesso</td>
<td>Fornecemos a funcionalidade de gerenciamento de permissões de usuários em grupos de segurança para tornar o seu serviço mais seguro.</td>
<td>05-2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35498" target="_blank">Visão geral do controle de acesso</a></td>
</tr>
</tbody></table>

## Janeiro de 2017
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Aceita o broadcast e o multicast</td>
<td>O broadcast e o multicast são comunicações um para muitos, o que pode ajudar as empresas a economizar largura de banda da rede e reduzir a carga da rede por meio de transmissão eficiente de dados ponto a multiponto.<li>Broadcast: a Tencent Cloud aceita o broadcast na dimensão de sub-redes.</li><li>Multicast: a Tencent Cloud aceita o multicast na dimensão da VPC.</li></td>
<td>01-2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/31809" target="_blank">Ativação ou desativação do broadcast e do multicast</a></td>
</tr>
</tbody></table>

## Outubro de 2016
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Compatível com ENIs</td>
<td>O serviço de permutação automática de várias ENIs para CVMs ajuda você a obter o isolamento entre três redes e a implantação de serviços de alta disponibilidade.</td>
<td>10-2016</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215/35502" target="_blank">Gerenciamento de ENIs</a></td>
</tr>
</tbody></table>

## Dezembro de 2015
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Permite mapas de topologia de rede</td>
<td>Um mapa de topologia de rede pode exibir claramente sua arquitetura de rede para ajudar você a resolver facilmente os problemas no gerenciamento de rede.</td>
<td>12-2015</td>
<td>-</td>
</tr>
</tbody></table>

## Maio de 2015
<table>
<thead>
<tr>
<th width="25%">Atualização</th>
<th width="50%">Descrição</th>
<th width="5%">Data de lançamento</th>
<th width="20%">Documentação</th>
</tr>
</thead>
<tbody><tr>
<td>Lança a VPC</td>
<td>Uma Virtual Private Cloud (VPC) é um espaço de rede isolado independente que permite redes definidas por software, conexão com seus IDCs pela VPN Connection ou Direct Connect e implantação flexível de nuvem híbrida.</td>
<td>05-2015</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215" target="_blank">VPC</a></td>
</tr>
</tbody></table>
