
TencentDB for MySQL menyediakan templat parameter sistem untuk pengaturan parameter batch. Parameter dalam templat parameter sistem dapat dioptimalkan dan diperbarui dengan iterasi MySQL. Dokumen ini menjelaskan riwayat pembaruan parameter di templat parameter sistem.
>?
>- Perubahan parameter dalam templat parameter sistem tidak memengaruhi instans database yang sudah menerapkan templat. Jika Anda perlu menerapkan parameter baru ke sekumpulan instans, Anda dapat mengimpor templat yang diperbarui saat mengatur parameter dalam batch.
>- Untuk petunjuk tentang cara menggunakan templat parameter sistem, lihat [Mengelola Templat Parameter](https://intl.cloud.tencent.com/document/product/236/31906).

## MySQL 8.0
### November 2020

| Nama Parameter | Kategori Pembaruan | Deskripsi Parameter |
| ------------------------------ | ---------- | ------------------------------------------------------------ |
| innodb_flush_log_at_trx_commit | Parameter baru didukung | Menentukan ketahanan transaksi InnoDB |
| sync_binlog | Parameter baru didukung | Mengontrol seberapa sering server MySQL menyinkronkan log biner ke disk |
| local_infile | Parameter baru didukung | Mengontrol apakah LOCAL didukung untuk LOAD DATA INFILE |
| innodb_log_file_size | Parameter baru didukung | Ukuran dalam byte dari setiap file log dalam grup log |
| cdb_recycle_bin_enabled | Parameter baru didukung | Mengontrol apakah tabel yang dihapus ditempatkan di keranjang sampah |
| binlog_format | Rentang nilai diperbarui | Rentang nilai baru: [baris]                                      |
| innodb_autoinc_lock_mode       | Nilai default diperbarui | Nilai default baru: 2                                          |
| table_open_cache               | Nilai default diperbarui | Nilai default baru: 2000                                          |
| slave_pending_jobs_size_max    | Nilai default diperbarui | Nilai default baru: 1073741824                                          |
| time_zone                      | Rentang nilai diperbarui | Rentang nilai baru: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00] |
| max_connections                | Rentang nilai diperbarui | Rentang nilai baru: [1-100000]                                 |
| slave_rows_search_algorithms   | Nilai default diperbarui | Nilai default baru: TABLE_SCAN,INDEX_SCAN,HASH_SCAN            |
| innodb_open_files              | Rentang nilai diperbarui | Nilai default baru: 10240                                      |
| slave_parallel_type            | Rentang nilai diperbarui | Rentang nilai baru: [LOGICAL_CLOCK\|TABLE\|DATABASE]           |


## MySQL 5.7
### Agustus 2020

| Nama Parameter | Kategori Pembaruan | Deskripsi Parameter |
| ------------------------------- | ------------ | --------------------------------------------------------- |
| log_warnings | Parameter baru didukung | Mengontrol apakah akan menghasilkan pesan peringatan tambahan |
| innodb_flush_log_at_trx_commit | Parameter baru didukung | Menentukan ketahanan transaksi InnoDB |
| sync_binlog | Parameter baru didukung | Mengontrol seberapa sering server MySQL menyinkronkan log biner ke disk |
| local_infile | Parameter baru didukung | Mengontrol apakah LOCAL didukung untuk LOAD DATA INFILE |
| innodb_log_file_size | Parameter baru didukung | Ukuran dalam byte dari setiap file log dalam grup log |
| binlog_format | Rentang nilai diperbarui | Rentang nilai baru: [baris]                                      |
| innodb_autoinc_lock_mode       | Nilai default diperbarui | Nilai default baru: 2                                          |
| innodb_open_files | Rentang nilai diperbarui | Rentang nilai baru: [1 - 102400] |
| table_open_cache               | Nilai default diperbarui | Nilai default baru: 2000                                          |
| slave_pending_jobs_size_max | Nilai default diperbarui | Nilai default baru: 1 GB |
| zona_waktu | Rentang nilai diperbarui | Rentang nilai baru: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>- 05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\| \+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00 \|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00] |
| max_connections                | Rentang nilai diperbarui | Rentang nilai baru: [1-100000]                                 |
| cdb_more_gtid_feature_supported | Semua fitur kernel didukung (termasuk parameter) | -          |
| slave_parallel_works                    | Semua fitur kernel didukung (termasuk parameter) |    -                                                       |
| tls_version                     | Parameter tidak digunakan lagi     |     -                                                      |
| slave_rows_search_algorithms   | Nilai default diperbarui | Nilai default baru: TABLE_SCAN,INDEX_SCAN,HASH_SCAN            |
| innodb_open_files | Nilai default diperbarui | Nilai default baru: 10240                                      |

## MySQL 5.6
### Agustus 2020

| Nama Parameter | Kategori Pembaruan | Deskripsi Parameter |
| ------------------------------- | ---------- | --------------------------------------------------------- |
| log_warnings | Parameter baru didukung | Mengontrol apakah akan menghasilkan pesan peringatan tambahan |
| innodb_flush_log_at_trx_commit | Parameter baru didukung | Menentukan ketahanan transaksi InnoDB |
| sync_binlog | Parameter baru didukung | Mengontrol seberapa sering server MySQL menyinkronkan log biner ke disk |
| local_infile | Parameter baru didukung | Mengontrol apakah LOCAL didukung untuk LOAD DATA INFILE |
| innodb_log_file_size | Parameter baru didukung | Ukuran dalam byte dari setiap file log dalam grup log |
| binlog_format | Rentang nilai diperbarui | Rentang nilai baru: [baris]                                      |
| innodb_autoinc_lock_mode       | Nilai default diperbarui | Nilai default baru: 2                                          |
| innodb_open_files | Rentang nilai diperbarui | Rentang nilai baru: [1 - 102400] |
| table_open_cache               | Nilai default diperbarui | Nilai default baru: 2000                                          |
| slave_pending_jobs_size_max     | Nilai default diperbarui | Nilai default baru: 1GB     |
| time_zone                       | Rentang nilai diperbarui | Rentang nilai baru: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00]      |
| max_connections                | Rentang nilai diperbarui | Rentang nilai baru: [1-100000]                                 |
| cdb_more_gtid_feature_supported | Nilai default diperbarui | Nilai default baru: MATI |
| slave_rows_search_algorithms   | Nilai default diperbarui | Nilai default baru: TABLE_SCAN,INDEX_SCAN,HASH_SCAN            |
| innodb_open_files | Nilai default diperbarui | Nilai default baru: 10240                                      |


## MySQL 5.5
### Agustus 2020

| Nama Parameter | Kategori Pembaruan | Deskripsi Parameter |
| ------------------------ | ---------- | -------- |
| innodb_autoinc_lock_mode | Nilai default diperbarui | Nilai default baru: TABLE_SCAN,INDEX_SCAN,HASH_SCAN            |
| innodb_open_files | Nilai default diperbarui | Nilai default baru: 10240 |
