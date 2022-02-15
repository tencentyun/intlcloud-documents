## Visão geral de cluster
Um cluster é a unidade de gerenciamento básica do TcaplusDB, que fornece serviço do TcaplusDB independente para negócios.
Do ponto de vista de negócios de jogos, um cluster pode fornecer serviços para os submódulos independentes de um jogo ou para o jogo inteiro.

## Criação de cluster
Para obter instruções detalhadas, consulte [Criação de cluster](https://intl.cloud.tencent.com/document/product/1016/32714).


## Detalhes do cluster
Você pode consultar a configuração do cluster e os detalhes dos atributos fazendo login no [console do TcaplusDB](https://console.cloud.tencent.com/tcaplusdb/app) e clicando no ID do cluster em questão.
Os detalhes do cluster consistem em três partes:

##### Informações básicas
- Cluster ID (ID do cluster): o ID exclusivo do cluster, que pode ser usado para localizar o cluster e controlar o acesso ao cluster, mas não pode ser usado para conexão com o banco de dados.
- Access ID (ID de acesso): o ID de conexão do cluster, que identifica o cluster quando você acessa o banco de dados por meio do SDK ou da ferramenta de cliente.
- Connection protocol (Protocolo de conexão): os protocolos de definição de tabelas aceitos por cluster. Atualmente, apenas o Protocol Buffers é aceito.
- Cluster name (Nome do cluster): o nome do cluster, que pode ser personalizado conforme necessário.
- Region (Região): a região do cluster.
- RESTful API (API RESTful): o endereço usado para acesso ao banco de dados por meio de uma API RESTful na mesma sub-rede do VPC.

##### Informações da rede
- Network (Rede): informações do VPC no qual o cluster atual está localizado.
- Subnet (Sub-rede): informações da sub-rede na qual o cluster atual está localizado.
- Private address (Endereço privado): o endereço IP privado atribuído ao cluster atual. As instâncias do CVM na mesma sub-rede do VPC do cluster podem acessar esse endereço IP.
- Private port (Porta privada): o número da porta de acesso atribuído ao cluster atual.

##### Outras informações
- Creation time (Hora de criação): a hora de criação do cluster atual.
- Connection password (Senha de conexão): caso tenha esquecido a senha, consulte a senha de acesso ao cluster no [console](https://console.cloud.tencent.com/tcaplusdb/app).
