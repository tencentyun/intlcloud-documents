Untuk memudahkan Anda melihat dan tetap mengetahui cara kerja instans, TencentDB for MySQL menyediakan berbagai metrik pemantauan performa dan fitur pemantauan yang nyaman (tampilan khusus, perbandingan waktu, metrik pemantauan gabungan, dll). Anda dapat login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), dan melihatnya di **Instance Monitoring** (Pemantauan Instans) pada halaman manajemen instans.
>?
>- Anda bisa mendapatkan metrik pemantauan instans dengan memanggil [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881) API atau menggunakan TencentDB for MySQL [metrik pemantauan](https://intl.cloud.tencent.com/document/product/248/11006) di Cloud Monitor.
>- Anda dapat [membuat dasbor](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=10) untuk metrik pemantauan guna menganalisis data yang dipantau secara dinamis.
>- Jika jumlah tabel dalam satu instans melebihi satu juta, pemantauan database mungkin terpengaruh. Pastikan jumlah tabel dalam satu instans di bawah satu juta.

## Jenis Instans untuk Pemantauan
Sumber TencentDB for MySQL, baca saja, dan instans pemulihan bencana serta node proksi database dapat dipantau, dan setiap instans dilengkapi dengan tampilan pemantauan terpisah untuk kueri yang mudah.

## Jenis Pemantauan
Empat jenis pemantauan tersedia untuk TencentDB for MySQL: pemantauan sumber daya, pemantauan mesin (umum), pemantauan mesin (diperpanjang), dan pemantauan deployment. Anda dapat melihat metrik dari berbagai jenis pemantauan untuk mendapatkan pemahaman yang cepat dan akurat tentang bagaimana performa dan pengoperasian instans.
- **Resource monitoring** (Pemantauan sumber daya) menyediakan data pemantauan CPU, memori, disk, dan jaringan.
- **Engine monitoring (general)** (Pemantauan mesin (umum)) menyediakan data pemantauan jumlah koneksi, kunci, tabel hotspot, dan kueri lambat, membantu Anda memecahkan masalah dan mengoptimalkan performa.
- **Engine monitoring (extended)** (Pemantauan mesin (diperpanjang)) menyediakan lebih banyak variasi metrik pemantauan terkait mesin untuk membantu Anda mengidentifikasi masalah database yang ada atau potensial sebanyak mungkin.
- **Deployment monitoring** (Pemantauan deployment) menyediakan metrik pemantauan terkait dengan penundaan replika sumber. Ini dibagi menjadi pemantauan sumber dan pemantauan replika:
 - Deploy pemantauan pada sumber: ketika instans yang dipantau adalah instans sumber yang bukan merupakan replika instans apa pun, data pemantauan terkait replikasi tidak valid untuk sumbernya, dan utas IO dan SQL dinonaktifkan. Data pemantauan terkait replikasi valid dan IO serta utas SQL dapat diaktifkan hanya jika instans yang dipantau adalah pemulihan bencana atau instans baca-saja.

 - Deploy pemantauan pada replika: instans sumber dua atau tiga node dan instans pemulihan bencana datang dalam arsitektur sumber/replika secara default. Akibatnya, data pemantauan terkait replikasi valid untuk replika hanya jika instans yang dipantau adalah sumber atau instans pemulihan bencana. Data pemantauan tersebut dapat mencerminkan jarak dan waktu penundaan replikasi antara sumber atau instans pemulihan bencana dan node replika tersembunyinya. Kami sarankan Anda mengawasi data pemantauan replika tersebut. Jika sumber atau instans pemulihan bencana gagal, node replika tersembunyi yang dipantaunya dapat dipromosikan ke instans sumber dengan cepat.

![](https://main.qcloudimg.com/raw/183cebeb93cdeaca2dedeb228ab8f0be.png)

## Memantau Granularitas
TencentDB for MySQL telah mengadopsi kebijakan adaptif untuk memantau granularitas sejak 11 Agustus 2018, yang berarti Anda tidak dapat memilih granularitas pemantauan seperti yang diinginkan untuk saat ini. Sintaks kebijakannya sebagai berikut:

| Rentang Waktu | Pemantauan Granularitas | Deskripsi Adaptasi | Periode Retensi |
|:-------|:--------|:----|:-----|
| (0j, 4j] | 5 detik | Rentang waktu di bawah 4 jam, dan granularitas pemantauan adalah 5 detik | 1 hari |
| (4j, 2h] | 1 menit | Rentang waktu di atas 4 jam tetapi di bawah 2 hari, dan granularitas pemantauan adalah 1 menit | 15 hari |
| (2h, 10h] | 5 menit | Rentang waktu di atas 2 hari tetapi di bawah 10 hari, dan granularitas pemantauan adalah 5 menit | 31 hari |
| (10h, 30h] | 1 jam | Rentang waktu di atas 10 hari tetapi di bawah 30 hari, dan granularitas pemantauan adalah 1 jam | 62 hari |

>?Saat ini, Anda dapat melihat data pemantauan TencentDB for MySQL dalam 30 hari terakhir.

## Metrik Pemantauan
Cloud Monitor menyediakan metrik pemantauan berikut untuk instans TencentDB for MySQL dalam dimensi instans:

>?Untuk informasi selengkapnya tentang cara menggunakan metrik pemantauan TencentDB, lihat [Metrik Pemantauan TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/248/11006).

| Nama Metrik | Parameter | Satuan | Deskripsi |
|---------|---------|---------|---------|
| Kueri per Detik | qps | Hitungan/detik | Jumlah pernyataan SQL (INSERT, SELECT, UPDATE, DELETE, dan REPLACE) yang dieksekusi oleh database per detik. Metrik ini terutama mewakili kemampuan pemrosesan aktual dari instans TencentDB |
| Transaksi per Detik | tps | Hitungan/detik | Jumlah transaksi yang dieksekusi per detik dalam database |
| Kueri Lambat | slow_queries | - | Jumlah kueri yang memerlukan waktu lebih dari `long_query_time` detik untuk dieksekusi |
| Pemindaian Tabel Lengkap | pilih_pindai | Hitungan/dtk | Jumlah pemindaian tabel lengkap yang dilakukan per detik |
| Kueri SELECT | select_count | Hitungan/dtk | Jumlah kueri yang dieksekusi per detik |
| Kueri UPDATE | com_update | Hitungan/dtk | Jumlah pembaruan yang dijalankan per detik |
| Kueri DELETE | com_delete | Hitungan/dtk | Jumlah penghapusan yang dilakukan per detik |
| Kueri INSERT | com_insert | Hitungan/dtk | Jumlah penyisipan yang dieksekusi per detik |
| Kueri REPLACE | com_replace | Hitungan/dtk | Jumlah penggantian yang dieksekusi per detik |
| Jumlah Kueri | kueri | Hitungan/dtk | Semua pernyataan SQL yang dieksekusi seperti SET dan SHOW |
| Buka Koneksi | threads_connected | - | Jumlah koneksi yang saat ini terbuka |
| Pemanfaatan Koneksi | connection_use_rate | % | Jumlah koneksi terbuka/jumlah maksimum koneksi |
| Pemanfaatan Kueri | query_rate | % | QPS aktual/QPS yang direkomendasikan |
| Penggunaan Disk Total | kapasitas | MB | Ini termasuk direktori data MySQL dan log seperti binlog, relaylog, undolog, errorlog, dan slowlog |
| Ruang Disk yang Digunakan oleh Data | real_capacity | MB | Ini hanya mencakup direktori data MySQL |
| Ruang Disk yang Digunakan oleh File Log | log_capacity | MB | Ini hanya mencakup binlog log MySQL, relaylog, undolog, errorlog, dan slowlog |
| Ruang Disk yang Digunakan oleh File Log | disk_log_used | MB | Ini hanya mencakup binlog, relaylog, dan undolog MySQL |
| Ruang Disk yang Digunakan oleh File Sementara | disk_tmp_used | MB | Ini hanya mencakup file sementara MySQL |
| Pemanfaatan Disk |volume_rate | % | Total penggunaan disk/ruang instans yang dibeli |
| Lalu Lintas Keluar Pribadi | byte_sent | Byte/dtk | Jumlah byte yang dikirim per detik |
| Lalu Lintas Masuk Pribadi | byte_diterima | Byte/dtk | Jumlah byte yang diterima per detik |
| Tingkat Hit Cache Kueri | qcache_hit_rate | % | Tingkat hit cache kueri |
| Pemanfaatan Cache Kueri | qcache_use_rate | % | Pemanfaatan cache kueri |
| Kunci Meja Ditunggu |table_locks_waited| Hitungan/detik | Berapa kali permintaan untuk kunci meja tidak dapat segera diberikan dan menunggu diperlukan |
| Tabel Sementara | create_tmp_tables | Hitungan/detik | Jumlah tabel sementara internal yang dibuat oleh server saat menjalankan pernyataan |
| Tingkat Hit Cache InnoDB | innodb_cache_hit_rate | % | Tingkat hit cache mesin InnoDB |
| Pemanfaatan Cache InnoDB | innodb_cache_use_rate | % | Pemanfaatan cache mesin InnoDB |
| Disk InnoDB Membaca |innodb_os_file_reads| Hitungan/dtk | Jumlah total pembacaan file yang dilakukan oleh utas baca dalam InnoDB |
| Disk Menulis InnoDB | innodb_os_file_writes | Hitungan/detik | Jumlah total penulisan file yang dilakukan oleh utas penulisan dalam InnoDB |
| InnoDB fsync() Panggilan | innodb_os_fsyncs | Hitungan/detik | Jumlah panggilan fungsi fsync oleh InnoDB per detik |
| Tabel Dibuka oleh InnoDB | innodb_num_open_files | - | Jumlah file yang saat ini dipegang InnoDB |
| Tingkat Hit Cache MyISAM | key_cache_hit_rate | % | Tingkat hit cache mesin MyISAM |
| Pemanfaatan Cache MyISAM | key_cache_use_rate | % | Pemanfaatan cache mesin MyISAM |
| Pemanfaatan CPU | cpu_use_rate | % | Jika penggunaan berlebihan sumber daya jeda diizinkan, pemanfaatan CPU dapat melebihi 100% |
| Pemanfaatan Memori               | tingkat penggunaan memori     | %   | Jika penggunaan berlebihan sumber daya jeda diizinkan, pemanfaatan memori dapat melebihi 100% |
| Penggunaan Memori | memory_use | MB | Jika penggunaan berlebihan dari sumber daya jeda diizinkan, memori yang digunakan dapat melebihi spesifikasi yang dibeli |
| File Sementara | create_tmp_files | Hitungan/dtk | Jumlah file sementara yang dibuat per detik |
| Tabel Terbuka | opened_tables | - | Jumlah tabel terbuka |
| Pernyataan COMMIT | com_commit | Hitungan/dtk | Jumlah pernyataan COMMIT per detik |
| Pernyataan ROLLBACK | com_rollback | Hitungan/dtk | Jumlah pernyataan ROLLBACK per detik |
| Utas yang Dibuat | threads_created | - | Jumlah utas yang dibuat untuk menangani koneksi |
| Menjalankan Utas | threads_running | - | Jumlah utas yang tidak tidur |
| Koneksi Maks | max_connections | - | Jumlah maksimum koneksi |
| Tabel Disk Sementara | create_tmp_disk_tables | Hitungan/dtk | Jumlah tabel sementara internal pada disk yang dibuat oleh server saat menjalankan pernyataan |
| Permintaan untuk Membaca Baris Berikutnya | handler_read_rnd_next | Hitungan/dtk | Jumlah permintaan untuk membaca baris berikutnya dalam file data |
| Pengembalian Dilakukan di Mesin Penyimpanan | handler_rollback | Hitungan/dtk | Jumlah permintaan mesin penyimpanan untuk melakukan operasi pengembalian |
| Pernyataan COMMIT Internal | handler_commit | Hitungan/dtk | Jumlah pernyataan COMMIT internal per detik |
| Halaman Gratis InnoDB | innodb_buffer_pool_pages_free | - | Jumlah halaman gratis di kumpulan buffer InnoDB |
| Total Halaman InnoDB | innodb_buffer_pool_pages_total | - | Ukuran total kumpulan buffer InnoDB di halaman |
| Pembacaan Logis InnoDB | innodb_buffer_pool_read_requests | Hitungan/dtk | Jumlah permintaan baca logis |
| Pembacaan Fisik InnoDB | innodb_buffer_pool_reads | Hitungan/dtk | Jumlah pembacaan logis yang tidak dapat dipenuhi oleh InnoDB dari kumpulan buffer, dan harus dibaca langsung dari disk |
| Data Dibaca di InnoDB | innodb_data_read | Byte/dtk | Jumlah data yang dibaca per detik |
| Total Pembacaan InnoDB | innodb_data_reads | Hitungan/dtk | Jumlah total data yang dibaca per detik |
| Total Penulisan InnoDB | innodb_data_writes | Hitungan/dtk | Jumlah total penulisan data per detik |
| Data Ditulis dalam InnoDB | innodb_data_write | Byte/dtk | Jumlah data yang ditulis per detik |
| Baris InnoDB Dihapus | innodb_rows_deleted | Hitungan/dtk | Jumlah baris yang dihapus dari tabel InnoDB |
| Baris InnoDB Disisipkan | innodb_rows_inserted | Hitungan/dtk | Jumlah baris yang dimasukkan ke dalam tabel InnoDB |
| Baris InnoDB Diperbarui | innodb_rows_updated | Hitungan/dtk | Jumlah baris yang diperbarui dalam tabel InnoDB |
| Baris InnoDB Baca | innodb_rows_read | Hitungan/dtk | Jumlah baris yang dibaca dari tabel InnoDB |
| Rata-rata. Saatnya Mendapatkan Kunci Baris InnoDB | innodb_row_lock_time_avg | ms | Waktu rata-rata untuk mendapatkan kunci baris untuk tabel InnoDB |
| Kunci Baris InnoDB Menunggu | innodb_row_lock_wais | Hitungan/dtk | Berapa kali operasi pada tabel InnoDB harus menunggu kunci baris |
| Blok yang Tidak Digunakan di Cache Kunci | key_blocks_unused | - | Jumlah blok kunci yang tidak digunakan oleh cache kunci MyISAM |
| Blok yang Digunakan di Cache Kunci | key_blocks_used | - | Jumlah blok kunci yang digunakan oleh cache kunci MyISAM |
| Blok Baca dari Key Cache | key_read_requests | Hitungan/dtk | Jumlah permintaan untuk membaca blok kunci dari cache kunci MyISAM |
| Blok Baca dari Disk | key_reads | Hitungan/dtk | Jumlah permintaan untuk membaca blok data disk dari cache kunci MyISAM |
| Blok Ditulis ke dalam Cache Kunci | key_write_requests | Hitungan/dtk | Jumlah permintaan untuk menulis blok kunci ke cache kunci MyISAM |
| Blok Ditulis ke dalam Disk | key_writes | Hitungan/dtk | Jumlah permintaan untuk menulis blok data disk ke cache kunci MyISAM |
| Penundaan Replika Sumber (dalam MB) | master_slave_sync_distance | MB | Jumlah data yang tertinggal dari replika di belakang sumber |
| Penundaan Replika Sumber (dalam Detik)     | seconds_behind_master        |	Detik   | Penundaan replika sumber (dalam detik) |
| Status Utas IO       |	slave_io_running   |	Nilai status: 0: Ya; 1: Tidak; 2: Menghubungkan | Status menjalankan utas IO     |
| Status Utas SQL    |	slave_sql_running  |	Nilai status: 0: Ya; 1: Tidak                      | Status menjalankan utas SQL |

