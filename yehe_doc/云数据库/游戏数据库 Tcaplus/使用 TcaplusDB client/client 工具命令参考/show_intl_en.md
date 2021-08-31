## Overview
This command is used to query the basic information of the server or table. `show tables` can query table type and protocol type, and `show status` can query the current connection status, directory server information, and access layer information.

## Syntax
```
show [status/tables];
```

## Parameter

| Parameter | Description |
| ------ | ---- |
| table  | Table name |

## Sample
Query the information of tables in the current table group:
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
