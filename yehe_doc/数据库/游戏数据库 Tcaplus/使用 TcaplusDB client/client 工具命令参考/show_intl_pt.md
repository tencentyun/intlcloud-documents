## Visão geral
Este comando é usado para consultar as informações básicas do servidor ou da tabela. `show tables` pode consultar o tipo de tabela e o tipo de protocolo, e `show status` pode consultar o status atual da conexão, as informações do servidor de diretório e as informações da camada de acesso.

## Sintaxe
```
show [status/tables];
```

## Parâmetro

| Parâmetro | Descrição |
| ------ | ---- |
| table  | Nome da tabela |

## Exemplo
Consulte as informações das tabelas no grupo de tabelas atual:
```
tcaplus> show tables;
 
----------------------------------------------------------
| Table Name                         Type      Protocol  |
----------------------------------------------------------
| test_table                         GENERIC   TDR       |
| tbMailTest                         LIST      PROTOBUF  |
| pb_generic_index_shardingkey       GENERIC   PROTOBUF  |
| pb_generic_index_noshardkey        GENERIC   PROTOBUF  |
| pb_generic_noindex_noshardkey      GENERIC   PROTOBUF  |
| pb_list                            LIST      PROTOBUF  |
| pb_list2                           LIST      PROTOBUF  |
| pb_sortedlist                      LIST      PROTOBUF  |
| aes_info                           GENERIC   TDR       |
| auth_info                          GENERIC   TDR       |
| depend_me_services                 GENERIC   TDR       |
| host_info                          GENERIC   TDR       |
| instance_info                      GENERIC   TDR       |
| node_info                          GENERIC   TDR       |
| service_depends                    GENERIC   TDR       |
| service_info                       GENERIC   TDR       |
| token_info                         GENERIC   TDR       |
| cl_list                            LIST      PROTOBUF  |
| cl_generic                         GENERIC   PROTOBUF  |
| table_generic                      GENERIC   TDR       |
----------------------------------------------------------
```
