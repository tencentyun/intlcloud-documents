O TcaplusDB é um serviço de banco de dados NoSQL distribuído, totalmente hospedado, e consiste basicamente nas camadas de gerenciamento, acesso e armazenamento. As camadas de acesso e armazenamento consistem em vários nós de conexão e nós de armazenamento e aceitam o escalonamento de nó horizontal. Cada camada tem suas próprias funções, e a arquitetura geral é mostrada abaixo:
![](https://main.qcloudimg.com/raw/3afc344e14b9f2d2b6eacf46b0751af6.jpg)

#### Camada de gerenciamento
A camada de gerenciamento do TcaplusDB é usada para armazenar metadados e informações de gerenciamento, programar o sistema do TcaplusDB e gerenciar dados do TcaplusDB.

#### Camada de acesso
A camada de acesso do TcaplusDB é usada para processar solicitações do usuário, interagir com nós de dados na camada de armazenamento, além de obter dados e retorná-los aos usuários.

#### Camada de armazenamento
O serviço da camada de armazenamento é o serviço principal do TcaplusDB usado para armazenar dados do usuário, responder às solicitações da camada de acesso e retornar informações de dados.

### Estrutura lógica do TcaplusDB
A estrutura lógica do TcaplusDB consiste em clusters, grupos de tabelas e tabelas conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/486543524b9eb422f86682524c7aa3ad.jpg)

