O Tencent Cloud fornece vários métodos para acessar a internet, como por meio de um endereço IP público comum, EIP, NAT Gateway e Cloud Load Balancer (CLB). 

## Endereços IP públicos comuns
Ao criar uma instância do CVM, é possível atribuir um endereço IP público comum à instância. O sistema atribuirá um endereço IP ao seu CVM para permitir que ele acesse a internet e seja acessível pela internet. 
Os endereços IP públicos comuns não podem ser vinculados ou desvinculados dinamicamente a recursos como CVMs, mas é possível convertê-los em EIPs. Para obter detalhes, consulte [Conversão de endereços IP públicos em EIPs](https://intl.cloud.tencent.com/document/product/213/16586).

## Endereços IP elásticos
Diferente dos endereços IP públicos que precisam ser solicitados e liberados com os CVMs, os endereços IP elásticos (EIPs) são recursos de nuvem independentes que são desacoplados do ciclo de vida do CVM e podem ser operados separadamente. 
Para obter informações sobre como solicitar, vincular e liberar EIPs, consulte [EIPs – Etapas](https://intl.cloud.tencent.com/document/product/213/16586). 
Os EIPs oferecem as seguintes vantagens: 
- Recursos de nuvem independentes 
É possível operar EIPs de forma independente, sem a necessidade de adquiri-los com os CVMs. 
- Vinculação e desvinculação elástica de recursos 
Os EIPs podem ser vinculados e desvinculados dos CVMs e de outros recursos a qualquer momento. 

## NAT Gateways
Um NAT Gateway fornece as funcionalidades SNAT e DNAT, o que permite estabelecer facilmente uma saída de internet e fornecer serviços para os CVMs em um VPC, a fim de acessar a internet com o mesmo endereço IP público. 
Para obter informações sobre como configurar o NAT Gateway, consulte [NAT Gateways – Visão geral da operação](https://intl.cloud.tencent.com/document/product/1015/30235).
Os NAT Gateways oferecem as seguintes vantagens: 
- Acesso seguro à internet 
Os NAT Gateways fornecem os recursos SNAT e DNAT para ocultar os endereços IP dos CVMs em um VPC durante a comunicação pela internet, garantindo a segurança. 
- Alta disponibilidade 
Os NAT Gateways oferecem backup dinâmico mestre/escravo, permutação a quente automática e encaminhamento rápido com uma taxa de até 5 Gbps. Além disso, eles são compatíveis com aplicativos de internet em grande escala. 
- Configuração flexível 
É possível modificar as especificações do NAT Gateway conforme necessário e a qualquer momento. 

## Cloud Load Balancers
Um Cloud Load Balancer (CLB) distribui o tráfego para vários CVMs, a fim de aprimorar os recursos de serviço externo dos sistemas de aplicativos. Ele elimina pontos únicos de falha para garantir sistemas de aplicativos altamente disponíveis.
Para obter informações sobre como adquirir e configurar um CLB, consulte [CLBs – Introdução](https://intl.cloud.tencent.com/document/product/214/8975).
Os CLBs oferecem as seguintes vantagens: 
- Cluster único de alto desempenho 
Um cluster do CLB consiste em vários servidores físicos, com uma disponibilidade de até 99,95%. O sistema de clusters pode remover instâncias com falha e selecionar instâncias em bom funcionamento para garantir a execução adequada dos serviços no servidor real.
- Alta segurança e estabilidade
Com o sistema anti-DDoS do BGP, o CLB pode se defender contra a maioria dos ataques de rede (como ataques DDoS) e limpar ataques de tráfego em segundos, evitando endereços IP bloqueados ou consumo total da largura de banda.

## Gateways públicos
Um gateway público é um CVM com a funcionalidade de encaminhamento habilitada. Em um VPC, os CVMs sem um endereço IP público conseguem acessar a internet por meio de gateways públicos em sub-redes diferentes. Os gateways públicos podem converter os endereços de origem do tráfego da internet de outros CVMs para seus próprios endereços IP.
Para obter informações sobre como configurar um gateway público, consulte [Configuração de gateways públicos](https://intl.cloud.tencent.com/document/product/215/33404).
