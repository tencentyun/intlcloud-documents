Cloud Block Storage (CBS) menyediakan perangkat blok jaringan yang sangat tersedia, sangat andal, berbiaya rendah, dan dapat disesuaikan yang dapat digunakan sebagai disk terpisah dan dapat diperluas untuk CVM.CBS menyimpan data pada tingkat blok data dalam mekanisme terdistribusi tiga salinan untuk memastikan keandalan data.CBS diklasifikasikan menjadi empat jenis:**Premium Cloud Storage**, **SSD**, **Enhanced SSD**, dan **Tremendous SSD**.Setiap jenis memiliki kinerja dan karakteristik yang unik, serta harganya berbeda-beda.

## Catatan
- Saat ini, Enhanced SSD dan Tremendous SSD hanya tersedia di zona ketersediaan tertentu.Dua jenis disk tersebut akan didukung di lebih banyak zona ketersediaan.
- Kinerja Enhanced SSD hanya dijamin jika terpasang ke model S5, M5, dan SA2 yang dibuat setelah 1 Agustus 2020, dan semua model generasi selanjutnya.
- **Tremendous SSD** hanya dapat dibeli dan digunakan dengan instance CVM Standard Storage Optimized S5se.**
- Enhanced SSD dan Tremendous SSD tidak dapat digunakan sebagai disk sistem.
- Enhanced SSD dan Tremendous SSD tidak dapat dienkripsi.
- Enhanced SSD dan Tremendous SSD tidak dapat ditingkatkan dari jenis disk lain.


## Ikhtisar
- **Premium Cloud Storage**
Premium Cloud Storage Tencent Cloud adalah jenis penyimpanan hybrid.Penyimpanan ini mengadopsi mekanisme Cache untuk menyediakan penyimpanan seperti SSD berperforma tinggi, dan menggunakan mekanisme terdistribusi tiga salinan untuk memastikan keandalan data.Premium Cloud Storage cocok untuk penggunaan tingkat kecil dan sedang dengan persyaratan tinggi untuk keandalan data dan persyaratan standar untuk kinerja, seperti server Web/Aplikasi, pemrosesan logis bisnis, serta situs kecil dan sedang.
- **SSD**
SSD adalah disk cloud all-flash yang menggunakan SSD NVMe sebagai media penyimpanan, dan menggunakan mekanisme terdistribusi tiga salinan.Jenis disk ini menyediakan layanan penyimpanan dengan latensi rendah, IOPS acak tinggi, I/O throughput tinggi, dan keamanan data hingga 99,9999999% sehingga cocok untuk penggunaan dengan persyaratan tinggi untuk kinerja I/O.
- **Enhanced SSD**
Enhanced SSD didasarkan pada mesin penyimpanan terbaru Tencent Cloud, media penyimpanan SSD NVMe, dan infrastruktur jaringan terbaru.Jenis disk ini menggunakan mekanisme terdistribusi tiga salinan untuk menyediakan penyimpanan berkinerja tinggi dengan latensi rendah, IOPS acak tinggi, I/O throughput tinggi, dan keamanan data hingga 99,9999999% sehingga cocok untuk penggunaan intensif I/O dengan persyaratan tinggi untuk latensi, seperti basis data besar dan NoSQL.Uniknya, kinerja dan kapasitas disk cloud Enhanced SSD dapat disesuaikan secara terpisah untuk memenuhi kebutuhan Anda.
- **Tremendous SSD**
Tremendous SSD didukung oleh mesin penyimpanan terdistribusi berkinerja tinggi terbaru dari Tencent Cloud, infrastruktur jaringan berkecepatan tinggi, dan perangkat keras penyimpanan terbaru.Jenis disk ini menawarkan kinerja jangka panjang dan stabil dengan latensi sangat rendah.Jenis disk ini cocok untuk beban kerja intensif I/O dan throughput yang membutuhkan latensi sangat rendah, seperti basis data besar (MySQL, HBase, Cassandra, dll.), model penyimpanan nilai-kunci (etcd, rocksdb, dll.), layanan pencarian log (Elasticsearch, dll.), dan bisnis bandwidth tinggi real-time (pemrosesan video, siaran langsung, dll.).Jenis disk ini berkinerja baik dalam beban kerja transaksi utama, layanan basis data inti, layanan OLTP skala besar, pemrosesan video, dan skenario lainnya.Kinerja dan kapasitas disk cloud Tremendous SSD dapat disesuaikan secara terpisah untuk memenuhi kebutuhan Anda.


## Metrik Kinerja
Tabel di bawah ini membandingkan kinerja keempat layanan CBS.

| Metrik | Tremendous SSD | Enhanced SSD | SSD | Premium Cloud Storage|
| ----| -----|---- | ----- | --|
| Ukuran maksimum (GB)     | 32.000 | 32.000 | 32.000 | 32.000 |
| IOPS maksimum    | 1.100.000 | 100.000 | 26.000 | 6.000 |
| Kinerja IOPS acak | Kinerja dasar: IOPS acak = min{4000+100 × kapasitas (GiB), 50000}<br>Kinerja ekstra: IOPS maksimum = min{128 × kinerja ekstra, 1050000} <br> | Kinerja dasar: IOPS acak = min{1800 + 50 × kapasitas (GiB), 50000}<br>Kinerja ekstra: IOPS maksimum = min{128 × kinerja ekstra, 50000} <br>Untuk informasi selengkapnya, lihat [Kinerja Enhanced SSD](https://intl.cloud.tencent.com/document/product/362/39611) | IOPS acak = min{1800 + 30 × kapasitas (GiB), 26000} | IOPS acak = min{1800 + 8 × kapasitas (GiB), 6000} |
| Throughput maksimum (MB/dtk) | 4.000 MB/dtk | 1.000 MB/dtk | 260 MB/dtk | 150 MB/dtk |
| Kinerja throughput (MB/dtk) | Kinerja dasar: throughput = min{120 + 0,5 × kapasitas (GiB), 350}<br>Kinerja ekstra: throughput = min{1 × kinerja ekstra, 3650} <br> | Kinerja dasar: throughput = min{120 + 0,5 × kapasitas (GiB), 350}<br>Kinerja ekstra: throughput = min{1 × kinerja ekstra, 650} <br>Untuk informasi selengkapnya, lihat [Kinerja Enhanced SSD](https://intl.cloud.tencent.com/document/product/362/39611) | Throughput = min{120 + 0,2 × kapasitas (GiB), 260} | Throughput = min{100 + 0,15 × kapasitas (GiB), 150} |
| Latensi baca/tulis acak utas tunggal | 0,1-0,5 mdtk | 0,3-1 mdtk| 0,5-3 mdtk | 0,8-5 mdtk|
|Catatan| Tremendous SSD hanya dapat dibeli dengan instance [Standard Storage Optimized S5se](https://intl.cloud.tencent.com/document/product/213/11518).Jenis disk ini dapat dibeli secara terpisah, atau digunakan pada jenis instance CVM lainnya.| Kinerja Enhanced SSD hanya dijamin jika terpasang ke S5, M5, dan SA2 dan model generasi yang lebih baru.| Tidak ada | Tidak ada |


>?Perbedaan utama antara disk cloud terletak pada kinerja I/O.

## Kasus Penggunaan
**Enhanced SSD lebih cocok untuk skenario yang sensitif terhadap latensi atau intensif I/O**, termasuk:
- Kinerja tinggi dan keandalan data tinggi: cocok untuk sistem bisnis misi-penting dengan beban tinggi.SSD menyediakan redundansi data tiga salinan dan dilengkapi dengan kemampuan komprehensif untuk pencadangan data, snapshot, dan pemulihan data dalam hitungan detik.
- Basis data sedang dan besar: mendukung penggunaan basis data relasional sedang dan besar yang berisi tabel dengan jutaan baris, seperti MySQL, Oracle, SQL Server, dan MongoDB.
- NoSQL Besar: mendukung bisnis NoSQL seperti HBase dan Cassandra.
- Elasticsearch: mendukung penyimpanan ES latensi rendah.
- Layanan video: cocok untuk penggunaan dengan kebutuhan bandwidth penyimpanan yang tinggi, seperti encoding dan decoding audio/video, siaran langsung, dan pemutaran rekaman.
- Analisis data besar: cocok untuk analisis data, penambangan data, kecerdasan bisnis, dan bidang lainnya.Menyediakan kemampuan pemrosesan terdistribusi untuk data di tingkat TB dan PB.

**Tremendous SSD lebih cocok untuk skenario sensitif latensi yang membutuhkan latensi sangat rendah**, termasuk:
- Penyimpanan nilai-kunci/key-value (KV): mendukung rocksdb, etcd, dll. Layanan penyimpanan KV umumnya menulis data ke disk dalam mode I/O seri, yang memerlukan latensi sangat rendah.Latensi utas tunggal menentukan kinerja sistem secara keseluruhan.Tremendous SSD menjamin latensi serendah puluhan mikrodetik sehingga cocok untuk sistem bisnis inti dengan persyaratan tinggi untuk keandalan dan ketersediaan data.
- Basis data besar: mendukung penggunaan basis data relasional sedang dan besar yang berisi tabel dengan jutaan baris, seperti MySQL, Oracle, SQL Server, dan MongoDB.
- NoSQL Besar: mendukung bisnis NoSQL seperti HBase dan Cassandra.
- Elasticsearch: mendukung penyimpanan ES latensi rendah.
- Layanan video: cocok untuk penggunaan dengan kebutuhan bandwidth penyimpanan yang tinggi, seperti encoding dan decoding audio/video, siaran langsung, dan pemutaran rekaman.
- Sistem bisnis inti: cocok untuk penggunaan intensif I/O dan sistem bisnis inti lainnya dengan persyaratan keandalan data yang tinggi.
- Analisis data besar: cocok untuk analisis data, penambangan data, kecerdasan bisnis, dan bidang lainnya.Menyediakan kemampuan pemrosesan terdistribusi untuk data di tingkat TB dan PB.
- Kinerja tinggi dan keandalan data tinggi: cocok untuk sistem bisnis misi-penting dengan beban tinggi.SSD menyediakan redundansi data tiga salinan dan dilengkapi dengan kemampuan komprehensif untuk pencadangan data, snapshot, dan pemulihan data dalam hitungan detik.

**SSD berlaku untuk penggunaan dengan beban tinggi dan sedang**, termasuk:
- Basis data sedang: penggunaan basis data relasional sedang dan besar, seperti MySQL.
- Pemrosesan image: mendukung analisis data dan bisnis penyimpanan, seperti pemrosesan image.

**Premium Cloud Storage terutama cocok untuk skenario data berikut**:
- Basis data kecil dan menengah dan server Web/Aplikasi.Memberikan kinerja I/O jangka panjang dan stabil.
- Skenario yang membutuhkan kapasitas dan kinerja penyimpanan yang seimbang, seperti layanan kantor perusahaan.
- Pengujian bisnis inti dan debugging front dan back end.

## Deskripsi Penagihan
Untuk detail harga disk cloud, lihat [Ikhtisar Harga](https://intl.cloud.tencent.com/document/product/362/2413).
