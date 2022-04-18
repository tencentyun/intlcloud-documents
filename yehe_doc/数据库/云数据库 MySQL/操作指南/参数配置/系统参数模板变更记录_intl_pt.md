
O TencentDB for MySQL fornece modelos de parâmetros do sistema para configurações de parâmetros em lote. Os parâmetros nos modelos de parâmetros do sistema podem ser otimizados e atualizados com a iteração do MySQL. Este documento descreve o histórico de atualização dos parâmetros nos modelos de parâmetros do sistema.
>?
>- As alterações dos parâmetros em um modelo de parâmetro do sistema não afetam as instâncias de banco de dados que já aplicaram o modelo. Se você precisar aplicar novos parâmetros a um lote de instâncias, poderá importar o modelo atualizado ao definir parâmetros em lotes.
>- Para obter instruções sobre como usar modelos de parâmetros do sistema, consulte [Gerenciar modelos de parâmetros](https://intl.cloud.tencent.com/document/product/236/31906).

## MySQL 8.0
### Novembro de 2020

| Nome do parâmetro                       | Categoria de atualização   | Descrição do parâmetro                                                     |
| ------------------------------ | ---------- | ------------------------------------------------------------ |
| innodb_flush_log_at_trx_commit | Novo parâmetro compatível         | Determina a durabilidade da transação do InnoDB                  |
| sync_binlog                     | Novo parâmetro compatível         | Controla com que frequência o servidor MySQL sincroniza o log binário com o disco           |
| local_infile                    | Novo parâmetro compatível         | Controla se LOCAL é compatível com LOAD DATA INFILE |
| innodb_log_file_size            | Novo parâmetro compatível         | O tamanho em bytes de cada arquivo de log em um grupo de logs         |
| cdb_recycle_bin_enabled        | Novo parâmetro compatível       | Controla se a tabela excluída é colocada na lixeira |
| binlog_format                  | Intervalo de valores atualizado | Novo intervalo de valores: [row]                                      |
| innodb_autoinc_lock_mode       | Valor padrão atualizado | Novo valor padrão: 2                                          |
| table_open_cache               | Valor padrão atualizado | Novo valor padrão: 2000                                          |
| slave_pending_jobs_size_max    | Valor padrão atualizado | Novo valor padrão: 1073741824                                          |
| time_zone                      | Intervalo de valores atualizado | Novo intervalo de valores: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00] |
| max_connections                | Intervalo de valores atualizado | Novo intervalo de valores: [1-100000]                                 |
| slave_rows_search_algorithms   | Valor padrão atualizado | Novo valor padrão: TABLE_SCAN,INDEX_SCAN,HASH_SCAN            |
| innodb_open_files              | Intervalo de valores atualizado | Novo valor padrão: 10240                                      |
| slave_parallel_type            | Intervalo de valores atualizado | Novo intervalo de valores: [LOGICAL_CLOCK\|TABLE\|DATABASE] |


## MySQL 5.7
### Agosto de 2020

| Nome do parâmetro                       | Categoria de atualização | Descrição do parâmetro                                                     |
| ------------------------------- | ------------ | --------------------------------------------------------- |
| log_warnings                    | Novo parâmetro compatível         | Controla se deve produzir mensagens de aviso adicionais   |
| innodb_flush_log_at_trx_commit  | Novo parâmetro compatível         | Determina a durabilidade da transação do InnoDB                  |
| sync_binlog                     | Novo parâmetro compatível         | Controla com que frequência o servidor MySQL sincroniza o log binário com o disco           |
| local_infile                    | Novo parâmetro compatível         | Controla se LOCAL é compatível com LOAD DATA INFILE |
| innodb_log_file_size            | Novo parâmetro compatível         | O tamanho em bytes de cada arquivo de log em um grupo de logs         |
| binlog_format                  | Intervalo de valores atualizado | Novo intervalo de valores: [row]                                      |
| innodb_autoinc_lock_mode       | Valor padrão atualizado | Novo valor padrão: 2                                          |
| innodb_open_files               | Intervalo de valores atualizado   |   Novo intervalo de valores: [1 - 102400]                |
| table_open_cache               | Valor padrão atualizado | Novo valor padrão: 2000                                          |
| slave_pending_jobs_size_max     | Valor padrão atualizado   |   Novo valor padrão: 1GB     |
| time_zone                       | Intervalo de valores atualizado   |  Novo intervalo de valores: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00]       |
| max_connections                | Intervalo de valores atualizado | Novo intervalo de valores: [1-100000]                                 |
| cdb_more_gtid_feature_supported | Todos os recursos do kernel são compatíveis (incluindo o parâmetro) | -          |
| slave_parallel_works                    | Todos os recursos do kernel são compatíveis (incluindo o parâmetro) | -                                                       |
| tls_version                     | Parâmetro descontinuado     |     -                                                      |
| slave_rows_search_algorithms   | Valor padrão atualizado | Novo valor padrão: TABLE_SCAN,INDEX_SCAN,HASH_SCAN            |
| innodb_open_files              | Valor padrão atualizado | Novo valor padrão: 10240                                      |

## MySQL 5.6
### Agosto de 2020

| Nome do parâmetro                       | Atualizar categoria   | Descrição do parâmetro                                                     |
| ------------------------------- | ---------- | --------------------------------------------------------- |
| log_warnings                    | Novo parâmetro compatível         | Controla se deve produzir mensagens de aviso adicionais   |
| innodb_flush_log_at_trx_commit | Novo parâmetro compatível         | Determina a durabilidade da transação do InnoDB |
| sync_binlog                     | Novo parâmetro compatível         | Controla com que frequência o servidor MySQL sincroniza o log binário com o disco           |
| local_infile                    | Novo parâmetro compatível         | Controla se LOCAL é compatível com LOAD DATA INFILE |
| innodb_log_file_size            | Novo parâmetro compatível         | O tamanho em bytes de cada arquivo de log em um grupo de logs         |
| binlog_format                  | Intervalo de valores atualizado | Novo intervalo de valores: [row]                                      |
| innodb_autoinc_lock_mode       | Valor padrão atualizado | Novo valor padrão: 2                                          |
| innodb_open_files               | Intervalo de valores atualizado |   Novo intervalo de valores: [1 - 102400]                |
| table_open_cache               | Valor padrão atualizado | Novo valor padrão: 2000                                          |
| slave_pending_jobs_size_max     | Valor padrão atualizado |  Novo valor padrão: 1GB     |
| time_zone                       | Intervalo de valores atualizado |   Novo intervalo de valores: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00]      |
| max_connections                | Intervalo de valores atualizado | Novo intervalo de valores: [1-100000]                                 |
| cdb_more_gtid_feature_supported | Valor padrão atualizado |  Novo valor padrão: OFF    |
| slave_rows_search_algorithms   | Valor padrão atualizado | Novo valor padrão: TABLE_SCAN,INDEX_SCAN,HASH_SCAN            |
| innodb_open_files              | Valor padrão atualizado | Novo valor padrão: 10240                                      |


## MySQL 5.5
### Agosto de 2020

| Nome do parâmetro                       | Categoria de atualização   | Descrição do parâmetro                                                     |                                                     |
| ------------------------ | ---------- | -------- |
| innodb_autoinc_lock_mode   | Valor padrão atualizado | Novo valor padrão: TABLE_SCAN,INDEX_SCAN,HASH_SCAN            |
| innodb_open_files        | Valor padrão atualizado |  Novo valor padrão: 10240        |
