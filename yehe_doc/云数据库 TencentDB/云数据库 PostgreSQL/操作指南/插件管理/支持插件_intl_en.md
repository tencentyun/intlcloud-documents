TencentDB for PostgreSQL supports creating custom extensions (`CREATE EXTENSION extension_name`). The following extensions are supported.

>?To use the timescaledb, pipelinedb, wal2json, decoder_raw, and decoderbufs extensions, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

| Extension Name                 | 9.3.5  | 9.5.4  | 10.4   | 11.8   | 12.4   |
| ---------------------- | ------ | ------ | ------ | ------ | ------ |
| btree_gin              | 1.0    | 1.0    | 1.2    | 1.3    | 1.3    |
| btree_gist             | 1.0    | 1.0    | 1.5    | 1.5    | 1.5    |
| chkpass                | 1.0    | 1.0    | 1.0    | 1.0    | 1.0    |
| citext                 | 1.0    | 1.0    | 1.4    | 1.5    | 1.6    |
| cube                   | 1.0    | 1.0    | 1.2    | 1.4    | 1.4    |
| dict_int               | 1.0    | 1.0    | 1.0    | 1.0    | 1.0    |
| earthdistance          | 1.0    | 1.0    | 1.1    | 1.1    | 1.1    |
| fuzzystrmatch          | 1.0    | 1.0    | 1.1    | 1.1    | 1.1    |
| hstore                 | 1.2    | 1.2    | 1.4    | 1.5    | 1.6    |
| intagg                 | 1.0    | 1.0    | 1.1    | 1.1    | 1.1    |
| intarray               | 1.0    | 1.0    | 1.2    | 1.2    | 1.2    |
| isn                    | 1.0    | 1.0    | 1.1    | 1.2    | 1.2    |
| jsonbx                 | Unsupported | 1.0    | Unsupported | Unsupported | Unsupported |
| ltree                  | 1.0    | 1.0    | 1.1    | 1.1    | 1.1    |
| pg_hint_plan           | 1.1.4  | 1.1.5  | 1.3.6  | 1.3.6  | 1.3.6  |
| pg_prewarm             | Unsupported | 1.0    | 1.1    | 1.2    | 1.2    |
| pg_stat_statements     | 1.1    | 1.3    | 1.5    | 1.6    | 1.7    |
| pg_trgm                | 1.1    | 1.1    | 1.3    | 1.4    | 1.4    |
| pgcrypto               | 1.0    | 1.2    | 1.3    | 1.3    | 1.3    |
| pgrouting              | 2.4.1  | 2.4.1  | 2.6.0  | 2.6.0  | 3.1.0  |
| pgrowlocks             | 1.1    | 1.1    | 1.2    | 1.2    | 1.2    |
| pl/perl                | 1.0    | 1.0    | 1.0    | 1.0    | 1.0    |
| pl/pgsql               | 1.0    | 1.0    | 1.0    | 1.0    | 1.0    |
| pl/tcl                 | 1.0    | 1.0    | 1.0    | 1.0    | 1.0    |
| plcoffee               | 2.0.0  | 2.0.0  | 2.3.4  | 2.3.15  | 2.3.15 |
| plls                   | 2.0.0  | 2.0.0  | 2.3.4  | 2.3.15  | 2.3.15 |
| plv8                   | 2.0.0  | 2.0.0  | 2.3.4  | 2.3.15  | 2.3.15 |
| postgis                | 2.3.0  | 2.3.0  | 2.3.7  | 3.0.1  | 3.0.2  |
| postgis_tiger_geocoder | 2.3.0  | 2.3.0  | 2.4.1  | 3.0.1  | 3.0.2  |
| sslinfo                | 1.0    | 1.0    | 1.2    | 1.2    | 1.2    |
| tablefunc              | 1.0    | 1.0    | 1.0    | 1.0    | 1.0    |
| tsearch2               | 1.0    | 1.0    | Unsupported | Unsupported | Unsupported |
| unaccent               | 1.0    | 1.0    | 1.1    | 1.1    | 1.1    |
| uuid-ossp              | 1.0    | 1.0    | 1.1    | 1.1    | 1.1    |
| timescaledb            | Unsupported | Unsupported | 1.7.5  | 1.7.4  | 1.7.5  |
| pipelineDB             | Unsupported | Unsupported | 1.0.0  | 1.0.0  | Unsupported |
| pg_hashids             | Unsupported | Unsupported | 1.2.1  | 1.2.1  | 1.2.1  |
| wal2json               | Unsupported | Unsupported | 2.3    | 2.3    | 2.3    |
| decoder_raw            | Unsupported | Unsupported | 1.0    | 1.0    | 1.0    |
| postgres-decoderbufs   | Unsupported | Unsupported | 1.2.2  | 1.2.2  | 1.2.2  |
| hll                    | Unsupported | 2.14   | 2.14   | 2.14   | 2.14   |
| pg_bigm                | Unsupported | 1.2    | 1.2    | 1.2    | 1.2    |
| imgsmlr                | 1.0    | 1.0    | 1.0    | 1.0    | 1.0    |
| rum                    | Unsupported | Unsupported | 1.3    | 1.3    | 1.3    |
| zhparser               | 1.0    | 1.0    | 1.0    | 1.0    | 1.0    |
| postgis_topology       | 2.3.0  | 2.3.0  | 2.4.1  | 3.0.1  | 3.0.2  |
| address_standardizer   | 2.3.0  | 2.3.0  | 2.4.1  | 3.0.1  | 3.0.2  |
| postgis_sfcgal         | 2.3.0  | 2.3.0  | 2.4.1  | 2.4.1  | 3.0.2  |
| pgagent         | 4.0.0  | 4.0.0  | 4.0.0  | 4.0.0  | 4.0.0  |
