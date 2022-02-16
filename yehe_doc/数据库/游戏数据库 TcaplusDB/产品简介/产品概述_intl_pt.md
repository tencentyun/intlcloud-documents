## Visão geral
Com o crescimento explosivo dos dados de jogos, tornou-se cada vez mais difícil para os bancos de dados relacionais tradicionais atender às necessidades, como funções de leitura e gravação simultâneas, armazenamento eficiente e acesso a dados em massa, alta escalabilidade e alta disponibilidade. Por outro lado, os bancos de dados NoSQL se desenvolveram rapidamente devido às suas vantagens, como expansão simples e funções rápidas de leitura e gravação.
O TencentDB for TcaplusDB foi desenvolvido especialmente para armazenamento de dados de jogos com base no conceito de design e tecnologia de bancos de dados não relacionais. Ele pode equilibrar desempenho e custo de acordo com as características dos jogos. Até agora, ele forneceu serviços de armazenamento de dados estáveis para vários jogos online com dezenas de milhões de usuários ativos diários, como Arena of Valor, CrossFire e NARUTO.

## Introdução
O TencentDB for TcaplusDB é um serviço de armazenamento de dados distribuído NoSQL projetado para jogos e permite o acesso à API [Protobuf](https://intl.cloud.tencent.com/document/product/1016/30295#P). Ao combinar cache com discos, o TcaplusDB pode oferecer alto desempenho enquanto economiza custos para prover suporte a estruturas de todos os servidores/todas as regiões e vários servidores/várias regiões. Além disso, ele fornece soluções seguras, confiáveis e completas que abrangem a expansão/redução da capacidade com serviço ininterrupto, backup para recuperação de desastres e reversão rápida em resposta ao crescimento explosivo de dados e operações de cauda longa dos jogos. Ele já é amplamente utilizado em centenas de jogos populares como Arena of Valor, CrossFire e NARUTO.

## Funcionalidades
#### Cache combinado com armazenamento persistente
Descrição: o armazenamento em cache e em disco são combinados, e os dados quentes e frios são automaticamente trocados dentro/fora.
Valor do usuário: não há necessidade de usar dois tipos de bancos de dados e, portanto, a arquitetura do aplicativo é simplificada.
#### Suporte para todos os servidores/todas as regiões
Descrição: o espaço de armazenamento é ilimitado, com uma única tabela limitada a 50 TB. Há suporte para expansão/redução de capacidade com serviço ininterrupto, assim como todos os servidores/todas as regiões e vários servidores/várias regiões.
Valor do usuário: não há necessidade de se preocupar com a expansão do espaço de armazenamento.
#### Suporte de acesso ao PB
Descrição: o acesso flexível aos dados é habilitado pelo uso do Protobuf, e o acesso e a extração de campos especificados são aceitos.
Valor do usuário: a largura de banda é bastante economizada e com menor custo.
#### Reversão rápida
Descrição: é efetuado o pull do backup manual rapidamente e, em seguida, descompactado em paralelo. O processo de reversão é totalmente automatizado e há suporte para reversão para um ponto preciso no tempo. Com 300 GB de backup de dados frios em cada nó, todos os nós podem ser recuperados em 2 horas.
Valor do usuário: a reversão rápida pode reduzir as perdas por falha.
#### Backup para recuperação de desastres
Descrição: proteção contra sobrecarga; backup dinâmico principal/secundário; backup manual diário para recuperação de desastres com dados retidos por até 30 dias e registros binlog por 15 dias.
Valor do usuário: a segurança dos dados é garantida e a falha de operação é tratada facilmente.
