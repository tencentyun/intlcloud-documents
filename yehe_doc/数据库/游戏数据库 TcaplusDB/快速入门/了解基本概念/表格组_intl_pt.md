## Visão geral do grupo de tabelas
Como um método de isolamento lógico no TcaplusDB, um grupo de tabelas representa uma partição de dados que pode separar tabelas diferentes umas das outras. Um cluster pode conter vários grupos de tabelas e um grupo de tabelas pode conter várias tabelas. Os grupos de tabelas diferentes não podem acessar os dados uns dos outros.

Do ponto de vista de negócios de jogos, se um negócio de jogos aceita servidores unificados em todas as zonas e pode ler/gravar o mesmo grupo de tabelas no cluster, então ela não precisa ser dividida em zonas diferentes. Ela também pode ser específica do servidor/específica da zona, ou seja, o cluster pode conter vários grupos de tabelas.

## Criação de grupo de tabelas
Para obter instruções detalhadas, consulte [Criação de grupo de tabelas](https://intl.cloud.tencent.com/document/product/1016/32716).

## Detalhes de grupo de tabelas
Você pode consultar a configuração e os atributos do grupo de tabelas na página de lista de clusters para entender o uso geral do cluster.
Você pode fazer login no [console do TcaplusDB](https://console.cloud.tencent.com/tcaplusdb/app) e inserir a lista de clusters para consultar as informações do grupo de tabelas do cluster em questão.

As informações do grupo de tabelas contêm os quatro campos a seguir:
- ID: é o ID do grupo de tabelas no cluster atual, que é necessário durante a conexão com o banco de dados. Observe que os IDs de grupo de tabelas podem ser repetidos em clusters diferentes.
- Nome do grupo de tabelas: você pode personalizar o nome do grupo de tabelas para refletir exatamente a sua finalidade.
- Contagem de tabelas: indica a quantidade de tabelas do grupo de tabelas atual.
- Capacidade total: indica a capacidade do disco utilizado pelas tabelas do grupo de tabelas atual.
