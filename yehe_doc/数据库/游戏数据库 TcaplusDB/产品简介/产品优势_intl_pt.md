### Baixo custo
O serviço de armazenamento NoSQL de tabela de chaves, que emprega armazenamento na memória suplementado por armazenamento em disco, permite alternar dados em processo entre memória e discos, além de expandir dinamicamente a capacidade em vários processos para garantir que os dados ativos sejam armazenados na memória e os dados inativos nos discos. Esse serviço economiza cerca de 70% dos custos em comparação com o armazenamento somente na memória e cerca de 40% em comparação com o Redis+MySQL.

### Alto desempenho
Funcionalidades, incluindo troca de dados quentes e frios entre memória e discos com base no algoritmo menos usado recentemente (LRU), armazenamento de dados em disco SSD e distribuição de dados em vários servidores, garantem um alto desempenho de até 100 mil QPS por servidor com uma latência menor que 10 milissegundos.

### Alta disponibilidade
O mecanismo de backup dinâmico principal/secundário garante uma recuperação rápida em caso de falha do sistema.

### Suporte para necessidades específicas de jogos
As necessidades específicas do jogo, como um modelo de vários servidores/várias regiões, inicialização rápida de servidores, acesso entre regiões, consolidação de dados entre regiões, compactação de dados e muitas outras, são atendidas e otimizadas continuamente de acordo com os requisitos do jogo.

### Expansão dinâmica
O espaço de armazenamento é ilimitado e a capacidade pode ser expandida ou reduzida dinamicamente de acordo com as necessidades reais de um jogo e não afeta a sua operação. Essa funcionalidade torna mais fácil lidar com mudanças repentinas em escala industrial.

### Facilidade de aprendizado
O serviço herda as tecnologias de desenvolvimento da plataforma de computador e se beneficia da experiência de desenvolvimento da equipe de jogos para computador. A API de serviço fornece APIs de operação síncrona e assíncrona fáceis.

### Operação baseada em serviço
Com um modo de aplicação de recursos prático, não será mais necessário implantar o ambiente de serviço de armazenamento manualmente.

### Otimização da utilização de recursos para melhorar a eficiência operacional
O alarme e outros sistemas básicos são integrados para fornecer recursos de monitoramento em nível de processo. As APIs de serviço fornecem acesso fácil à expansão da capacidade do servidor, ao balanceamento de carga e à recuperação de desastres.
