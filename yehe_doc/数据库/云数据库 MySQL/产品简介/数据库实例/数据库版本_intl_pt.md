## Versões compatíveis
Atualmente, o TencentDB for MySQL é compatível com o MySQL v8.0, v5.7, v5.6 e v5.5. Para mais informações sobre as funcionalidades de cada versão, consulte a [documentação oficial](https://dev.mysql.com/doc/refman/5.7/en/). As políticas oficiais de suporte ao ciclo de vida do MySQL são mostradas abaixo:

| Versão            | Data de disponibilidade geral | Fim do suporte premium | Fim do suporte estendido | Fim do suporte de manutenção |
| :------------------ | :------- | :------------ | :------------- | :-----------|
| MySQL Database 5.0 | 5 de outubro  | 11 de dezembro              | Não disponível        | Indeterminado             |
| MySQL Database 5.1 | 8 de dezembro  | 13 de dezembro              | Não disponível        | Indeterminado             |
| MySQL Database 5.5 | 10 de dezembro  | 15 de dezembro              | 18 de dezembro               | Indeterminado             |
| MySQL Database 5.6 | 13 de fevereiro  | 18 de fevereiro              | 21 de fevereiro               | Indeterminado             |
| MySQL Database 5.7 | 15 de outubro  | 20 de outubro              | 23 de outubro               | Indeterminado             |
| MySQL Database 8.0 | 18 de abril  | 23 de abril              | 26 de abril               | Indeterminado             |

>?
> - O suporte oficial estendido para o MySQL v5.5 terminou em dezembro de 2018. Não houve nenhuma declaração explícita sobre extensão de suporte adicional, possivelmente porque a correção de problemas leva mais tempo. É altamente recomendável usar uma versão posterior do MySQL.
> - O MySQL v5.6 e as versões posteriores não são mais compatíveis com mecanismo de armazenamento MyISAM, portanto recomendamos que você use o mecanismo InnoDB, que apresenta desempenho melhor e mais estável.
> - Atualmente, o MySQL v5.6 e as versões posteriores aceitam três modos de replicação: assíncrona, semissincronizada e sincronização forte. Apenas o modo de replicação assíncrona está disponível no MySQL v5.5.


## Vantagens do TencentDB for MySQL v8.0
- Combinado com um conjunto completo de serviços de gerenciamento e o kernel TXSQL, o TencentDB for MySQL fornece um serviço de banco de dados de nível empresarial que é mais estável e rápido de implantar. Ele se aplica a vários casos de uso e ajuda você a atualizar seus negócios.
- O TXSQL é totalmente compatível com o MySQL e os forks MySQL amplamente utilizados.
- O TencentDB for MySQL tem três sistemas de recuperação de desastres: espera ativa, espera manual e alternância entre AZs. Ele pode atingir até 99,95% de disponibilidade de serviço e até 99,9996% de confiabilidade de dados.
- O TencentDB for MySQL apresenta um conjunto completo de serviços de gerenciamento de banco de dados fáceis de usar, incluindo monitoramento, backup, reversão, criptografia, dimensionamento automático, auditoria, e diagnóstico e otimização inteligentes, permitindo que você se concentre mais no desenvolvimento dos negócios.
- Uma instância do TencentDB for MySQL pode lidar com mais de 500 mil consultas por segundo (QPS, na sigla em inglês). O TencentDB for MySQL simplifica muito o desenvolvimento dos negócios, as operações de banco de dados e a arquitetura de negócios, facilitando o gerenciamento dos bancos de dados.
- Arquiteturas avançadas: nó único, dois nós e três nós.
- Compatível com o CStore, um mecanismo de armazenamento colunar de alto desempenho, aceitando milhões de gravações em tempo real por segundo e consultas em tempo real em qualquer dimensão de dezenas de bilhões de dados em milissegundos. Para solicitar o CStore, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).

## Comparação entre as funcionalidades do TencentDB for MySQL v8.0 e do Oracle MySQL v8.0

| Funcionalidade | TencentDB for MySQL v8.0                                 | Oracle MySQL v8.0                                         |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Desempenho de custos | 1. Recursos elásticos. <br>2. Kernel TXSQL da Tencent. <br>3. Funcionalidades integradas de backup e restauração. <br>4. Um conjunto completo de ferramentas e serviços SaaS. | 1. Enorme custo de investimento único. <br>2. A versão de software livre não tem otimização de desempenho. <br>3. Recursos e custos adicionais de backup. <br>4. Taxas de rede pública e altas taxas de nome de domínio. |
| Disponibilidade | 1. É fornecido um sistema completo de alternância de alta disponibilidade. <br>2. As réplicas somente leitura equilibram automaticamente a carga e o tráfego. <br>3. São fornecidas instâncias de recuperação de desastres para a recuperação de desastres remota, garantindo alta disponibilidade. | 1. É necessário comprar servidores e aguardar a entrega. <br>2. É necessário implantar os sistemas de alta disponibilidade e balanceamento de carga por conta própria. <br>3. Alto custo para criar data centers em várias regiões. |
| Confiabilidade | 1. Confiabilidade dos dados de até 99,9996%. <br>2. RPO/RTO baixo. <br>3. Replicação de dados de réplica de source estável. | 1. Confiabilidade de dados de 99%, que depende da probabilidade de danos a um único disco. <br>2. É necessário investimento extra em P&D para alcançar um RPO baixo. <br>3. Podem ocorrer atrasos ou interrupções na replicação de dados. |
| Facilidade de uso | 1. É fornecido um conjunto completo de serviços de gerenciamento de banco de dados, e é possível operar os bancos de dados com facilidade no console. <br>2. Monitoramento com precisão de segundos e alarmes inteligentes. <br>3. Um sistema automático de alta disponibilidade em várias AZs. <br>4. Atualização de versão com um clique. | 1. É necessário implantar sistemas de alta disponibilidade e backup e restauração por conta própria, o que demanda tempo e dinheiro. <br>2. É necessário investimento extra para adquirir um sistema de monitoramento. <br>3. Alto custo para configurar data centers em regiões diferentes com custos de funcionários para as operações. <br>4. O custo de atualização de versão é alto e a manutenção requer um longo tempo de inatividade. |
| Desempenho   | 1. Os discos SSD locais têm excelente desempenho e o hardware personalizado permite iterações rápidas. <br>2. O TXSQL otimizado garante alto desempenho. <br>3. O DBbrain permite o diagnóstico e a otimização inteligentes do MySQL. | 1. O Oracle MySQL tem uma velocidade de iteração de hardware mais lenta do que a computação em nuvem, geralmente resultando em desempenho inferior. <br>2. Pode ser caro, pois os bancos de dados dependem de DBAs sênior. <br>3. O Oracle MySQL não possui ferramentas de desempenho nativas, portanto, você precisa comprá-las ou implantá-las por conta própria. |
| Segurança   | 1. Prevenção antecipada: lista de permissões, grupo de segurança, isolamento baseado em VPC. <br>2. Proteção durante as operações de bancos de dados: criptografia de dados TDE + KMS. <br>3. Auditoria após as operações de bancos de dados: auditoria do SQL. <br>4. O TencentDB for MySQL é atualizado logo após o Oracle MySQL ter atualizações de segurança. | 1. O custo da configuração da lista de permissões é alto e você precisa implementar a rede privada por conta própria. <br>2. Você precisa implementar a criptografia por conta própria durante as operações de bancos de dados. <br>3. É difícil auditar SQLs após as operações de bancos de dados, pois o MySQL de software livre não aceita a auditoria do SQL. <br>4. Depois que o MySQL for atualizado, a equipe de operações precisará instalar as atualizações ou os bancos de dados terão que ser desligados para manutenção. |

## Comparação entre os desempenhos do TencentDB for MySQL v8.0 e do Oracle MySQL v8.0
#### Desempenho de leitura
![](https://main.qcloudimg.com/raw/1bf9f7294ca6b4631f203333819ab2a1.png)

#### Desempenho de gravação
![](https://main.qcloudimg.com/raw/f77b34eb5c769539325b2f04a539ad4f.png)

