## Ikhtisar
Perintah ini digunakan untuk mengkueri informasi dasar dari server atau tabel. `show tables` dapat mengkueri jenis tabel dan jenis protokol, dan `show status` dapat mengkueri status koneksi saat ini, informasi server direktori, dan informasi lapisan akses.

## Sintaksis
```
tampilkan [status/tables];
```

## Parameter

| Parameter | Deskripsi |
| ------ | ---- |
| tabel  | Nama tabel |

## Sampel
Mengkueri informasi tabel dalam grup tabel saat ini:
```
tcaplus> tampilkan tabel;
 
----------------------------------------------------------
| Nama Tabel                         Jenis      Protokol  |
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
