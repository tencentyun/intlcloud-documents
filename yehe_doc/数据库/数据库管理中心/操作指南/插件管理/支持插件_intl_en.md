This document lists the kernel versions of TencentDB for PostgreSQL.

TencentDB for PostgreSQL supports creating custom extensions (`CREATE EXTENSION extension_name`). The following extensions are supported.
>?
>
>- The `timescaledb`, `pipelinedb`, `wal2json`, `decoder_raw`, and `decoderbufs` extensions cannot be directly created and used. To use them, [contact us](https://intl.cloud.tencent.com/contact-us) for assistance.
- If you have any requirements for or suggestions on extensions, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

| Extension                           | v13.3_r1.0 | v12.7_r1.1 | v11.12_r1.1 | v10.17_r1.1 | v9.5.25_r1.1 | v9.3.25_r1.1 | v9.3.5_r1.0 | v9.5.4_r1.0   | v10.4_r1.1 | v11.8_1.0 | v12.4_r1.0  |
|-------------------------------|------------|------------|-------------|-------------|--------------|--------------|-------------|---------------|------------|-----------|-------------|
|  pg_hint_plan                 | 1.3.7      | 1.3.6      |  1.3.6      | 1.3.6       | 1.1.5        |  1.1.4       | 1.1.4       | 1.1.5         | 1.3.6      | 1.3.6     | 1.3.6       |
|  pg_prewarm                   | 1.2        | 1.2        |  1.2        | 1.1         | 1.0          | Unsupported          | Unsupported         | Unsupported           | 1.1        | 1.2       | 1.2         |
|  pg_stat_error                | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       | 1.0         |
|  pg_stat_log                  | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       | 1.0         |
|  pg_stat_statements           | 1.8        | 1.7        |  1.6        | 1.6         | 1.3          |  1.1         | 1.1         | 1.3           | 1.5        | 1.6       | 1.7         |
|  pgrowlocks                   | 1.2        | 1.2        |  1.2        | 1.2         | 1.1          |  1.1         | 1.1         | 1.1           | 1.2        | 1.2       | 1.2         |
|  sslinfo                      | 1.2        | 1.2        |  1.2        | 1.2         | 1.0          |  1.0         | 1.0         | 1.0           | 1.2        | 1.2       | 1.2         |
|  tablefunc                    | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       | 1.0         |
|  tcn                          | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       | 1.0         |
|  unaccent                     | 1.1        | 1.1        |  1.1        | 1.1         | 1.0          |  1.0         | 1.0         | 1.0           | 1.1        | 1.1       | 1.1         |
|  uuid-ossp                    | 1.1        | 1.1        |  1.1        | 1.1         | 1.0          |  1.0         | 1.0         | 1.0           | 1.1        | 1.1       | 1.1         |
|  pg_cron                      | Unsupported        | Unsupported        | Unsupported         | 1.1         | 1.1          | Unsupported          | Unsupported         | 1.1           | 1.1        | Unsupported       | Unsupported         |
|  pgagent                      | 4.0        | 4.0        |  4.0        | 4.0         | 1.2          |  4.0         | 4.0         | 4.0           | 4.0        | 4.0       | 4.0         |
|  pg_partman                   | Unsupported        | Unsupported        | Unsupported         | Unsupported         | 2.6.4, 1.4    | Unsupported          | Unsupported         | 2.6.4, 1.4, 1.0 | Unsupported        | Unsupported       | Unsupported         |
|  tsearch2                     | Unsupported        | Unsupported        | Unsupported         | Unsupported         | 1.0          |  1.0         | 1.0         | 1.0           | Unsupported        | Unsupported       | Unsupported         |
|  postgis                      | 3.0.2      | 3.0.2      |  3.0.1      | 3.0.1       | 2.3.0        |  2.3.0       | 2.3.0       | 2.3.0         | 2.3.7      | 3.0.1     | 3.0.2       |
|  postgis_raster               | 3.0.2      | 3.0.2      |  3.0.1      | 3.0.1       | Unsupported          | Unsupported          | Unsupported         | Unsupported           | Unsupported        | 3.0.1     | 3.0.2       |
|  postgis_sfcgal               | 3.0.2      | 3.0.2      |  3.0.1      | 3.0.1       | 2.3.0        |  2.3.0       | Unsupported         | Unsupported           | Unsupported        | Unsupported       | 3.0.2       |
|  postgis_tiger_geocoder       | 3.0.2      | 3.0.2      |  3.0.1      | 3.0.1       | 2.3.0        |  2.3.0       | 2.3.0       | 2.3.0         | 2.4.1      | 3.0.1     | 3.0.2       |
|  postgis_topology             | 3.0.2      | 3.0.2      |  3.0.1      | 3.0.1       | 2.3.0        |  2.3.0       | 2.3.0       | 2.3.0         | 2.4.1      | 3.0.1     | 3.0.2       |
|  pgrouting                    | 3.1.0      | 3.1.0      |  2.6.0      | 2.6.0       | 2.4.1        |  2.4.1       | 2.4.1       | 2.4.1         | 2.6.0      | 2.6.0     | 3.1.0       |
|  address_standardizer         | 3.0.2      | 3.0.2      | 3.0.1       | 3.0.1       | 2.3.0        | 2.3.0        | 2.3.0       | 2.3.0         | 2.4.1      | 3.0.1     | 3.0.2       |
|  address_standardizer_data_us | 3.0.2      | 3.0.2      |  3.0.1      | 3.0.1       | 2.3.0        |  2.3.0       | 2.3.0       | 2.3.0         | 2.4.1      | 3.0.1     | 3.0.2       |
|  earthdistance                | 1.1        | 1.1        |  1.1        | 1.1         | 1.0          |  1.0         | 1.0         | 1.0           | 1.1        | 1.1       | 1.1         |
|  plperl                       | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       | 1.0         |
|  plpgsql                      | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       | 1.0         |
|  pltcl                        | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       | 1.0         |
|  plv8                         | 2.3.15     | 2.3.15     |  2.3.15     | 2.3.4       | 2.0.0        |  2.0.0       | 2.0.0       | 2.0.0         | 2.3.4      | 2.3.15    | 2.3.15      |
|  bool_plperl                  | 1.0        | Unsupported        | Unsupported         | Unsupported         | Unsupported          | Unsupported          | Unsupported         | Unsupported           | Unsupported        | Unsupported       | Unsupported         |
|  jsonb_plperl                 | 1.0        | 1.0        |  1.0        | Unsupported         | Unsupported          | Unsupported          | Unsupported         | Unsupported           | Unsupported        | 1.0       | 1.0         |
|  hstore                       | 1.7        | 1.6        |  1.5        | 1.4         | 1.3          |  1.2         | 1.2         | 1.3           | 1.4        | 1.5       | 1.6         |
|  hstore_plperl                | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          | Unsupported          | Unsupported         | 1.0           | 1.0        | 1.0       | 1.0         |
|  plcoffee                     | 2.3.15     | 2.3.15     |  2.3.15     | 2.3.4       | 2.0.0        |  2.0.0       | 2.0.0       | 2.0.0         | 2.3.4      | 2.3.15    | 2.3.15      |
|  plls                         | 2.3.15     | 2.3.15     |  2.3.15     | 2.3.4       | 2.0.0        |  2.0.0       | 2.0.0       | 2.0.0         | 2.3.4      | 2.3.15    | 2.3.15      |
|  timescaledb                  | 2.1.1      | 1.7.4      |  1.7.5      | 1.7.5       | Unsupported          | Unsupported          | Unsupported         | Unsupported           | 1.7.5      | 1.7.5     | 1.7.4       |
|  pipelinedb                   | Unsupported        | Unsupported        |  1.0.0      | 1.0.0       | Unsupported          | Unsupported          | Unsupported         | Unsupported           | 1.0.0      | 1.0.0     | Unsupported         |
|  rdkit                        | 3.8        | 3.8        |  3.8        | 3.8         | Unsupported          | Unsupported          | Unsupported         | Unsupported           | Unsupported        | Unsupported       | 3.8         |
|  imgsmlr                      | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       | 1.0         |
|  zhparser                     | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       | 1.0         |
|  intagg                       | 1.1        | 1.1        |  1.1        | 1.1         | 1.0          |  1.0         | 1.0         | 1.0           | 1.1        | 1.1       | 1.1         |
|  intarray                     | 1.3        | 1.2        |  1.2        | 1.2         | 1.0          |  1.0         | 1.0         | 1.0           | 1.2        | 1.2       | 1.2         |
|  isn                          | 1.2        | 1.2        |  1.2        | 1.1         | 1.0          |  1.0         | 1.0         | 1.0           | 1.1        | 1.2       | 1.2         |
|  xml2                         | 1.1        | 1.1        |  1.1        | 1.1         | 1.0          |  1.0         | 1.0         | 1.0           | 1.1        | 1.1       | 1.1         |
|  jsonbx                       | Unsupported        | Unsupported        | Unsupported         | Unsupported         | 1.0          | Unsupported          | Unsupported         | 1.0           | Unsupported        | Unsupported       | Unsupported         |
|  dict_int                     | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       | 1.0         |
|  dict_xsyn                    | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       | 1.0         |
|  citext                       | 1.6        | 1.6        |  1.5        | 1.4         | 1.1          |  1.0         | 1.0         | 1.1           | 1.4        | 1.5       | 1.6         |
|  ltree                        | 1.2        | 1.1        |  1.1        | 1.1         | 1.0          |  1.0         | 1.0         | 1.0           | 1.1        | 1.1       | 1.1         |
|  postgres_fdw                 | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       | 1.0         |
|  orafce                       | Unsupported        | Unsupported        | Unsupported         | Unsupported         | 3.3          |  3.3         | 3.3         | 3.3           | Unsupported        | Unsupported       | Unsupported         |
|  chkpass                      | 1.0        | 1.0        |  1.0        | 1.0         | 1.0          |  1.0         | 1.0         | 1.0           | 1.0        | 1.0       |     -        |
|  bloom                        | 1.0        | 1.0        |  1.0        | 1.0         | Unsupported          | Unsupported          | Unsupported         | Unsupported           | 1.0        | 1.0       | 1.0         |
|  btree_gin                    | 1.3        | 1.3        |  1.3        | 1.2         | 1.0          |  1.0         | 1.0         | 1.0           | 1.2        | 1.3       | 1.3         |
|  btree_gist                   | 1.5        | 1.5        |  1.5        | 1.5         | 1.1          |  1.0         | 1.0         | 1.1           | 1.5        | 1.5       | 1.5         |
|  roaringbitmap                | 0.5        | 0.5        |  0.5        | 0.5         | Unsupported          | Unsupported          | Unsupported         | Unsupported           | Unsupported        | Unsupported       | Unsupported         |
|  rum                          | 1.3        | 1.3        |  1.3        | 1.3         | Unsupported          | Unsupported          | Unsupported         | Unsupported           | 1.3        | 1.3       | 1.3         |
|  cube                         | 1.4        | 1.4        |  1.4        | 1.2         | 1.0          |  1.0         | 1.0         | 1.0           | 1.2        | 1.4       | 1.4         |
|  decoderbufs                  | 0.1.0      | 0.1.0      |  0.1.0      | 0.1.0       | Unsupported          | Unsupported          | Unsupported         | Unsupported           | 0.1.0      | 0.1.0     | 0.1.0       |
|  pg_bigm                      | 1.2        | 1.2        |  1.2        | 1.2         | 1.2          | Unsupported          | Unsupported         | 1.2           | 1.2        | 1.2       | 1.2         |
|  fuzzystrmatch                | 1.1        | 1.1        |  1.1        | 1.1         | 1.0          |  1.0         | 1.0         | 1.0           | 1.1        | 1.1       | 1.1         |
|  hll                          | 2.15       | 2.14       |  2.14       | 2.14        | 2.14         | Unsupported          | Unsupported         | 2.14          | 2.14       | 2.14      | 2.14        |
|  pg_trgm                      | 1.5        | 1.4        |  1.4        | 1.3         | 1.1          |  1.1         | 1.1         | 1.1           | 1.3        | 1.4       | 1.4         |
|  pg_hashids                   | 1.2.1      | 1.2.1      |  1.2.1      | 1.2.1       | 1.2.1        |  1.2.1       | 1.2.1       | 1.2.1         | 1.2.1      | 1.2.1     | 1.2.1       |
|  pgcrypto                     | 1.3        | 1.3        |  1.3        | 1.3         | 1.2          |  1.0         | 1.0         | 1.2           | 1.3        | 1.3       | 1.3         |

