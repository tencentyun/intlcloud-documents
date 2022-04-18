Para facilitar a visualização e manter-se atualizado sobre como as instâncias funcionam, o TencentDB for MySQL fornece uma ampla variedade de métricas de monitoramento de desempenho e recursos de monitoramento convenientes (exibição personalizada, comparação de tempo, métricas de monitoramento mescladas etc.). Você pode fazer login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e visualizá-los em **Instance Monitoring (Monitoramento de instância)** na página de gerenciamento de instâncias.
>?
>- >- É possível obter métricas de monitoramento de instância chamando a API [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881) ou usando as [métricas de monitoramento](https://intl.cloud.tencent.com/document/product/248/11006) do TencentDB for MySQL no Cloud Monitor.
 >- Também é possível [criar painéis](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=10) para métricas de monitoramento para analisar, dinamicamente, os dados monitorados.
>- Se o número de tabelas em uma única instância exceder um milhão, o monitoramento do banco de dados pode ser afetado. Certifique-se de que o número de tabelas em uma única instância seja inferior a um milhão.

## Tipos de instâncias para monitoramento
Instâncias de origem, somente leitura e recuperação de desastres do TencentDB for MySQL, bem como nós de proxy de banco de dados, podem ser monitorados e cada instância é fornecida com uma visualização de monitoramento separada para facilitar a consulta.

## Tipos de Monitoramento
Quatro tipos de monitoramento estão disponíveis para o TencentDB for MySQL: monitoramento de recursos, monitoramento de mecanismo (geral), monitoramento de mecanismo (estendido) e monitoramento de implantação. Você pode visualizar as métricas de diferentes tipos de monitoramento para obter uma compreensão rápida e precisa de como as instâncias são executadas e operam.
- **Monitoramento de recursos** fornece dados de monitoramento de CPU, memória, disco e rede.
- **Monitoramento do mecanismo (geral)** fornece dados de monitoramento do número de conexões, bloqueios, tabelas de pontos de acesso e consultas lentas, ajudando a solucionar problemas e otimizar o desempenho.
- **Monitoramento de mecanismo (estendido)** fornece uma variedade mais ampla de métricas de monitoramento relacionadas ao mecanismo para ajudá-lo a identificar, o máximo possível, problemas de banco de dados existentes ou potenciais.
- **Deployment monitoring (Monitoramento de implantação)** fornece métricas de monitoramento em relação ao atraso da réplica de origem. Ele se divide em monitoramento de origem e monitoramento de réplica:
 - Implantação de monitoramento na origem: quando a instância monitorada é uma instância de origem que não é uma réplica de nenhuma instância, os dados de monitoramento relacionados à replicação são inválidos para a origem e os threads de E/S e SQL são desabilitados. Os dados de monitoramento relacionados à replicação são válidos e os threads de E/S e SQL podem ser habilitados somente quando a instância monitorada é uma recuperação de desastre ou uma instância somente leitura.

 - Implantação de monitoramento na réplica: a instância de origem de dois ou três nós e a instância de recuperação de desastres vêm em uma arquitetura de origem/réplica por padrão. Como resultado, os dados de monitoramento relacionados à replicação são válidos para a réplica somente quando a instância monitorada é uma instância de origem ou de recuperação de desastres. Esses dados de monitoramento podem refletir a distância e o tempo de atraso da replicação entre a origem ou a instância de recuperação de desastres e seus nós de réplica ocultos. Recomendamos que você fique atento a esses dados de monitoramento da réplica. Se a instância de recuperação de desastres ou de origem falhar, seus nós de réplica ocultos monitorados podem ser promovidos para a instância de origem rapidamente.

![](https://main.qcloudimg.com/raw/183cebeb93cdeaca2dedeb228ab8f0be.png)

## Monitoramento de granularidade
O TencentDB for MySQL adotou uma política adaptável para monitorar a granularidade desde 11 de agosto de 2018, o que significa que, por enquanto, você não pode selecionar uma granularidade de monitoramento conforme desejado. A política adaptativa é a seguinte:

| Período de tempo | Granularidade de monitoramento | Descrição da adaptação | Período de retenção |
|:-------|:--------|:----|:-----|
| (0h, 4h] | 5 segundos | O intervalo de tempo está abaixo de 4 horas e a granularidade do monitoramento é de 5 segundos | 1 dia |
| (4h, 2d] | 1 minuto | O intervalo de tempo está acima de 4 horas, mas abaixo de 2 dias, e a granularidade do monitoramento é de 1 minuto | 15 dias |
| (2d, 10d] | 5 minutos | O intervalo de tempo está acima de 2 dias, mas abaixo de 10 dias, e a granularidade do monitoramento é de 5 minutos | 31 dias |
| (10d, 30d] | 1 hora | O período de tempo está acima de 10 dias, mas abaixo de 30 dias, e a granularidade do monitoramento é de 1 hora | 62 dias |

>?Atualmente, você pode visualizar os dados de monitoramento do TencentDB for MySQL nos últimos 30 dias.

## Monitoramento de métricas
O Cloud Monitor fornece as seguintes métricas de monitoramento para instâncias do TencentDB for MySQL na dimensão da instância:

>?Para obter mais informações sobre como usar as métricas de monitoramento do TencentDB, consulte [Métricas de monitoramento do TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/248/11006).

| Nome da métrica | Parâmetro | Unidade | Descrição |
|---------|---------|---------|---------|
| Consultas por segundo | qps | Contagens/segundo | O número de instruções SQL (INSERT, SELECT, UPDATE, DELETE, e REPLACE) executadas pelo banco de dados por segundo. Essa métrica representa principalmente a capacidade real de processamento da instância do TencentDB |
| Transações por Segundo | tps | Contagens/segundo | O número de transações executadas por segundo no banco de dados |
| Consultas lentas | slow_queries | - | O número de consultas que levam mais de `long_query_time` segundo(s) para serem executadas |
| Verificações de tabela completa | select_scan | Contagens/segundo | O número de varreduras de tabela completa executadas por segundo |
| Consultas SELECT | select_count | Contagens/segundo | O número de consultas executadas por segundo |
| Consultas UPDATE | com_update | Contagens/segundo | O número de atualizações executadas por segundo |
| Consultas DELETE | com_delete | Contagens/segundo | O número de exclusões executadas por segundo |
| Consultas INSERT | com_inserir | Contagens/segundo | O número de inserções executadas por segundo |
| Consultas REPLACE | com_replace | Contagens/segundo | O número de substituições executadas por segundo |
| Consultas totais | queries | Contagens/segundo | Todas as instruções SQL executadas, como SET e SHOW |
| Conexões Abertas | threads_conectados | - | O número de conexões atualmente abertas |
| Utilização da conexão | connection_use_rate | % | O número de conexões abertas/o número máximo de conexões |
| Utilização de consultas | query_rate | % | QPS real/QPS recomendado |
| Uso total do disco | capacidade | MB | Isso inclui os diretórios e logs de dados do MySQL, como binlog, relaylog, undolog, errorlog e slowlog |
| Espaço em disco usado por dados | real_capacity | MB | Isso inclui apenas os diretórios de dados do MySQL |
| Espaço em disco usado por arquivos de log | log_capacity | MB | Isso inclui apenas logs binlog, relaylog, undolog, errorlog e slowlog do MySQL |
| Espaço em disco usado por arquivos de log | disk_log_used | MB | Isso inclui apenas logs binlog, relaylog e undolog do MySQL |
| Espaço em disco usado por arquivos temporários | disk_tmp_used | MB | Isso inclui apenas os arquivos temporários do MySQL |
| Utilização do Disco |volume_rate | % | Uso total do disco/espaço de instância comprado |
| Tráfego de saída privado | bytes_sent       | Byte/segundo | O número de bytes enviados por segundo |
| Tráfego de entrada privado | bytes_received | Byte/segundo | O número de bytes recebidos por segundo |
| Taxa de acertos do cache de consulta | qcache_hit_rate | % | A taxa de acertos do cache de consulta |
| Utilização do cache de consulta | qcache_use_rate | % | A utilização do cache de consulta |
| Bloqueios de tabela esperados |table_locks_waited| Contagens/segundo | O número de vezes que um pedido de bloqueio de tabela não pôde ser concedido imediatamente e foi necessária uma espera |
| Tabelas temporárias | created_tmp_tables | Contagens/segundo | O número de tabelas temporárias internas criadas pelo servidor durante a execução de instruções |
| Taxa de acertos do cache InnoDB | innodb_cache_hit_rate | % | A taxa de acertos do cache do mecanismo InnoDB |
| Utilização do Cache InnoDB | innodb_cache_use_rate | % | A utilização do cache do mecanismo InnoDB |
| Leituras de disco do InnoDB |innodb_os_file_reads| Contagens/segundo | O número total de leituras de arquivo realizadas por threads de leitura dentro do InnoDB |
| Gravações de disco InnoDB | innodb_os_file_writes | Contagens/segundo | O número total de gravações de arquivo executadas por threads de gravação no InnoDB |
| Chamadas InnoDB fsync() | innodb_os_fsyncs | Contagens/segundo | O número de chamadas da função fsync pelo InnoDB por segundo |
| Tabelas abertas pelo InnoDB | innodb_num_open_files | - | O número de arquivos que o InnoDB mantém abertos no momento |
| Taxa de acerto do cache MyISAM | key_cache_hit_rate | % | A taxa de acertos do cache do mecanismo MyISAM |
| Utilização do cache MyISAM | key_cache_use_rate | % | A utilização do cache do mecanismo MyISAM |
| Utilização da CPU | cpu_use_rate | % | Se o uso excessivo de recursos ociosos for permitido, a utilização da CPU pode exceder 100% |
| Utilização de Memória               | memory use rate     | %   | Se o uso excessivo de recursos ociosos for permitido, a utilização da memória poderá exceder 100% |
| Uso de memória | memory_use | MB | Se o uso excessivo de recursos ociosos for permitido, a memória usada pode exceder a especificação adquirida |
| Arquivos Temp | created_tmp_files | Contagens/segundo | O número de arquivos temporários criados por segundo |
| Tabelas abertas | opened_tables | -      | O número de tabelas abertas |
| Instruções COMMIT | com_commit | Contagens/segundo | O número de instruções COMMIT por segundo |
| Declarações ROLLBACK | com_rollback | Contagens/s | O número de instruções ROLLBACK por segundo |
| Threads criados | threads_criados | - | O número de threads criados para lidar com conexões |
| Threads em execução | threads_running | - | O número de threads que não estão inativos |
| Máximo de conexões | max_connections | - | O número máximo de conexões |
| Tabelas de disco temporário | created_tmp_disk_tables | Contagens/segundo | O número de tabelas temporárias internas criadas em disco pelo servidor durante a execução de instruções |
| Solicitações para ler a próxima linha | handler_read_rnd_next | Contagens/segundo | O número de solicitações para ler a próxima linha no arquivo de dados |
| Reversões executadas no mecanismo de armazenamento | handler_rollback | Contagem/segundo | O número de solicitações de operação de reversão a um mecanismo de armazenamento |
| Instruções COMMIT internas | handler_commit | Contagens/segundo | O número de instruções COMMIT internas por segundo |
| Páginas gratuitas do InnoDB | innodb_buffer_pool_pages_free | - | O número de páginas gratuitas no pool de buffers do InnoDB |
| Total de páginas InnoDB | innodb_buffer_pool_pages_total | - | O tamanho total do pool de buffers do InnoDB em páginas |
| Leituras Lógicas do InnoDB | innodb_buffer_pool_read_requests | Contagens/segundo | O número de solicitações de leitura lógica |
| Leituras físicas do InnoDB | innodb_buffer_pool_reads | Contagens/segundo | O número de leituras lógicas que o InnoDB não pôde satisfazer no pool de buffers e teve que ler diretamente do disco |
| Dados lidos no InnoDB | innodb_data_read | Byte/segundo | A quantidade de dados lidos por segundo |
| Total de leituras do InnoDB | innodb_data_reads | Contagens/segundo | O número total de leituras de dados por segundo |
| Total de gravações do InnoDB | innodb_data_writes | Contagens/segundo | O número total de gravações de dados por segundo |
| Dados gravados no InnoDB | innodb_data_written | Byte/segundo | A quantidade de dados gravados por segundo |
| Linhas do InnoDB excluídas | innodb_rows_deleted | Contagens/segundo | O número de linhas excluídas das tabelas do InnoDB |
| Linhas do InnoDB inseridas | innodb_rows_inserted | Contagens/s | O número de linhas inseridas nas tabelas do InnoDB |
| Linhas do InnoDB atualizadas | innodb_rows_updated | Contagens/segundo | O número de linhas atualizadas nas tabelas do InnoDB |
| Linhas do InnoDB lidas | innodb_rows_read | Contagens/segundo | O número de linhas lidas das tabelas do InnoDB |
| Tempo médio para adquirir um bloqueio de linha do InnoDB | innodb_row_lock_time_avg | ms | O tempo médio para adquirir um bloqueio de linha para tabelas do InnoDB |
| Esperas de bloqueio de linha do InnoDB | innodb_row_lock_waits | Contagens/segundo | O número de vezes que as operações nas tabelas do InnoDB tiveram que esperar por um bloqueio de linha |
| Blocos não utilizados no cache de chave   | key_blocks_unused              | -     | O número de blocos de chave não utilizados pelo cache de chave MyISAM |
| Blocos usados ​​no cache de chave      | key_blocks_used                  | -     | O número de blocos de chave usados ​​pelo cache de chave MyISAM |
| Blocos lidos do cache de chave | key_read_requests | Contagens/segundo | O número de solicitações para ler um bloco de chave do cache de chave MyISAM |
| Blocos lidos do disco         | key_reads                | Contagens/segundo | O número de solicitações para ler um bloco de dados de disco do cache de chave MyISAM |
| Blocos gravados no cache de chave | key_write_requests | Contagens/segundo | O número de solicitações para gravar um bloco de chave no cache de chaves MyISAM |
| Blocos gravados em disco         | key_writes                | Contagens/segundo | O número de solicitações para gravar um bloco de dados de disco no cache de chave MyISAM |
| Atraso da réplica de origem (em MB)     | master_slave_sync_distance  | MB | A quantidade de dados que retardou a réplica em relação à origem |
| Atraso da réplica de origem (em segundos)     | seconds_behind_master        |	Segundo   | O atraso da réplica de origem (em segundos) |
| Status do thread de E/S       |	slave_io_running   |	Valores de status: 0: Sim; 1: Não; 2: Conectando | O status de execução do thread de E/S     |
| Status do thread SQL    |	slave_sql_running  |	Valor de status: 0: Sim; 1: Não                      | O status de execução do thread SQL |

