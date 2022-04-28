
>?As vantagens descritas neste documento são exclusivas para as instâncias do TencentDB for MySQL de dois nós e três nós.

## Custo-benefício e facilidade de uso
- **É permitida a separação de leitura/gravação**
As réplicas somente leitura podem ser montadas no TencentDB for MySQL. A arquitetura de uma source e várias réplicas permite que você responda a solicitações em massa. É fornecido o grupo do RO com a funcionalidade de balanceamento de carga para otimizar bastante a distribuição de pressão entre as réplicas somente leitura.

- **Hardware poderoso que garante alto desempenho**
O SSD NVMe apresenta alto desempenho de E/S, garantindo leituras e gravações contínuas.
São permitidos um máximo de 240 mil consultas por segundo (QPS, na sigla em inglês) e um espaço de armazenamento máximo de 6 TB para uma instância.

## Alta segurança
- **Proteção anti-DDoS**
Quando você sofre um ataque DDoS, essa funcionalidade pode ajudar a resistir a diversos tráfegos de ataque, garantindo o funcionamento normal dos negócios.

- **Proteção contra ataques a banco de dados**
Defesa eficaz contra ataques a banco de dados como ataques de injeção de SQL e de força bruta.

## Alta confiabilidade
Os dados são armazenados online em uma arquitetura de source/réplica, garantindo a alta segurança dos dados. Além disso, os dados de backup podem ser armazenados por um longo período, permitindo a recuperação de dados em caso de desastre em um banco de dados.

- **Criptografia de dados**
A funcionalidade Transparent Data Encryption (TDE) garante a segurança dos dados em tempo real e dos dados de backup.

- **Database Audit**
A funcionalidade de auditoria de dados de nível financeiro ajuda a evitar o roubo de dados importantes, rastrear operações que não estão em conformidade e localizar pulls mal-intencionados.

## Alta disponibilidade
- **Backup dinâmico em tempo real**
O mecanismo de backup dinâmico de servidor duplo permite a restauração sem perdas de dados dos últimos 7 a 1830 dias com base no backup de dados e no backup de logs (binlog). Esses backups podem ser retidos por 7 a 1830 dias.

- **Recuperação automática de desastres**
São fornecidos a detecção automática de falhas e o failover automático. Os procedimentos de alternância de source/réplica e failover são imperceptíveis para os usuários.

## Vantagens com relação aos bancos de dados físicos
- **Fácil gerenciamento de bancos de dados em massa**
Os bancos de dados podem ser gerenciados por linha de comando ou pelo console. São aceitos o gerenciamento de banco de dados em lote, a configuração de permissões e a importação de SQL. 

- **Importação de dados e reversão de backup**
São fornecidos vários métodos de importação de dados para a inicialização. O backup dos dados é feito de forma automática diariamente. O TencentDB permite que os dados sejam revertidos para qualquer momento dentro do período de retenção com base nos arquivos de backup.

- **Monitoramento profissional e alarme**
São fornecidos o monitoramento multidimensional e alarmes baseados em limites de recursos personalizados. Também é possível baixar relatórios de análise de consultas lentas e relatórios completos de execução do SQL.

- **Vários métodos de acesso**
É permitido o acesso à rede pública e à VPC. Você pode conectar instâncias do TencentDB ao seu IDC, uma nuvem privada ou outros recursos de computação para implantação em uma nuvem híbrida de forma conveniente.
