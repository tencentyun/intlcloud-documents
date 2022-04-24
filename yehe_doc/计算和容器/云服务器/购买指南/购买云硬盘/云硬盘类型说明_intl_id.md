Cloud Block Storage (CBS) menyediakan perangkat blok jaringan yang sangat tersedia, sangat andal, berbiaya rendah, dan dapat disesuaikan yang dapat digunakan sebagai disk mandiri dan dapat diperluas untuk CVM. CBS menyimpan data pada tingkat blok data dalam mekanisme terdistribusi tiga salinan untuk memastikan keandalan data. CBS dibagi ke dalam empat jenis: **Premium Cloud Storage** (Penyimpanan Cloud Premium), **SSD**, **Enhanced SSD** (SSD yang Ditingkatkan), dan **Tremendous SSD** (SSD Tremendous). Setiap jenis memiliki performa dan karakteristik yang unik, dan harganya yang berbeda-beda, membuat CBS cocok untuk berbagai kasus penggunaan.

## Catatan
- Saat ini, SSD yang Ditingkatkan dan SSD Tremendous hanya tersedia di zona ketersediaan tertentu. Keduanya akan didukung di lebih banyak zona ketersediaan.
- Performa SSD yang Ditingkatkan hanya dijamin saat dipasang ke model S5, M5, dan SA2 yang dibuat setelah 1 Agustus 2020, dan semua model generasi selanjutnya.
- **Tremendous SSD** (SSD Tremendous) hanya dapat dibeli dan digunakan dengan instans Standard Storage Optimized S5se CVM.**
- SSD yang Ditingkatkan dan SSD Tremendous tidak dapat digunakan sebagai disk sistem.
- SSD yang Ditingkatkan dan SSD Tremendous tidak dapat dienkripsi.
- SSD yang Ditingkatkan dan SSD Tremendous tidak dapat diupgrade dari jenis disk lain.


## Ikhtisar
- **Premium Cloud Storage** (Penyimpanan Cloud Premium)
Penyimpanan Cloud Premium Tencent Cloud adalah jenis penyimpanan hibrida. Penyimpanan ini mengadopsi mekanisme Cache untuk menyediakan penyimpanan seperti SSD berperforma tinggi, dan menggunakan mekanisme terdistribusi tiga salinan untuk memastikan keandalan data. Penyimpanan Cloud Premium cocok untuk aplikasi kecil dan menengah dengan persyaratan keandalan data tinggi dan persyaratan performa standar, seperti server Web/Aplikasi, pemrosesan logis bisnis, serta situs kecil dan menengah.
- **SSD**
SSD adalah all-flash cloud disk yang menggunakan NVMe SSD sebagai media penyimpanan dan menggunakan mekanisme terdistribusi tiga salinan. Disk ini menyediakan layanan penyimpanan dengan latensi rendah, IOPS acak tinggi, I/O throughput tinggi, dan keamanan data hingga 99,9999999%,membuatnya cocok untuk aplikasi dengan persyaratan I/O performa tinggi.
- **Enhanced SSD** (SSD yang Ditingkatkan)
Enhanced SSD didasarkan pada mesin penyimpanan terbaru Tencent Cloud, media penyimpanan SSD NVMe, dan infrastruktur jaringan terbaru. SSD ini menggunakan mekanisme terdistribusi tiga salinan untuk menyediakan penyimpanan berperforma tinggi dengan latensi rendah, IOPS acak tinggi, I/O throughput tinggi, dan keamanan data hingga 99,9999999%, membuatnya cocok untuk aplikasi intensif I/O dengan persyaratan latensi tinggi, seperti database besar dan NoSQL. Uniknya, performa dan kapasitas disk cloud SSD yang Ditingkatkan dapat disesuaikan secara independen untuk memenuhi kebutuhan Anda.
- **Tremendous SSD** (SSD Tremendous)
SSD Tremendous didukung oleh mesin penyimpanan terdistribusi berperforma tinggi terbaru dari Tencent Cloud, infrastruktur jaringan berkecepatan tinggi, dan perangkat keras penyimpanan terbaru. Disk ini menawarkan performa jangka panjang dan stabil dengan latensi sangat rendah. Ini sangat cocok untuk beban kerja intensif I/O dan throughput yang membutuhkan latensi sangat rendah, seperti database besar (MySQL, HBase, Cassandra, dll.), model penyimpanan nilai utama (etcd, rocksdb, dll.), layanan pencarian log (Elasticsearch, dll.), dan bisnis bandwidth tinggi real-time (pemrosesan video, streaming langsung, dll.). Disk ini bekerja dengan baik dalam beban kerja transaksi utama, layanan database inti, layanan OLTP skala besar, pemrosesan video, dan skenario lainnya. Uniknya, performa dan kapasitas disk cloud SSD Tremendous dapat disesuaikan secara independen untuk memenuhi kebutuhan Anda.


## Metrik Performa
Tabel di bawah ini membandingkan performa keempat layanan CBS.

| Metrik Performa | SSD Tremendous | SSD yang Ditingkatkan | SSD | Penyimpanan Cloud Premium|
| ----| -----|---- | ----- | --|
| Ukuran maksimum (GB) | 32.000 | 32.000 | 32.000 | 32.000 |
| IOPS Maksimum | 1.100.000 | 100.000 | 26.000 | 6.000 |
| Performa IOPS acak | Performa dasar: IOPS acak = min{4000+100 × kapasitas (GiB), 50000}<br>Performa ekstra: IOPS maksimum = min{128 × performa ekstra, 1050000} <br> | Performa dasar: IOPS acak = min{1800 + 50 × kapasitas (GiB), 50000}<br>Performa ekstra: IOPS maksimum = min{128 × performa ekstra, 50000} <br>Untuk informasi selengkapnya, lihat [Performa SSD yang Ditingkatkan] (https://intl.cloud.tencent.com/document/product/362/39611) | IOPS acak = min{1800 + 30 × kapasitas (GiB), 26000} | IOPS acak = min{1800 + 8 × kapasitas (GiB), 6000} |
| Throughput maksimum (MB/dtk) | 4.000 MB/dtk | 1.000 MB/dtk | 260 MB/dtk | 150 MB/dtk |
| Performa throughput (MB/detik) | Performa dasar: throughput = min{120 + 0,5 × kapasitas (GiB), 350}<br>Performa ekstra: throughput = min{1 × performa ekstra, 3650} <br> | Performa dasar: throughput = min{120 + 0,5 × kapasitas (GiB), 350}<br>Performa ekstra: throughput = min{1 × performa ekstra, 650} <br>Untuk informasi selengkapnya, lihat [Performa SSD yang Ditingkatkan](https://intl.cloud.tencent.com/document/product/362/39611) | Throughput = min{120 + 0,2 × kapasitas (GiB), 260} | Throughput = min{100 + 0,15 × kapasitas (GiB), 150} |
| Latensi baca/tulis acak utas tunggal | 0,1-0,5 md | 0,3-1 md| 0,5-3 md | 0,8-5 md|
|Catatan| SSD Tremendous hanya dapat dibeli dengan instans [Standard Storage Optimized S5se](https://intl.cloud.tencent.com/document/product/213/11518), yang tidak dapat dibeli secara independen, atau digunakan pada jenis instans CVM lainnya. | Performa SSD yang Ditingkatkan hanya dijamin saat dipasang ke S5, M5, dan SA2 dan model generasi yang lebih baru. | Tidak ada | Tidak ada |


>?Perbedaan utama antar disk cloud adalah performa I/O.

## Kasus Penggunaan
**SSD yang Ditingkatkan lebih cocok untuk skenario yang sensitif terhadap latensi atau intensif I/O**, termasuk:
- Performa tinggi dan keandalan data tinggi: cocok untuk sistem bisnis misi-kritis dengan beban tinggi. SSD menyediakan redundansi data tiga salinan dan dilengkapi dengan kemampuan komprehensif untuk pencadangan data, snapshot, dan pemulihan data dalam hitungan detik.
- Database menengah dan besar: mendukung aplikasi database relasional menengah dan besar yang berisi tabel dengan jutaan baris, seperti MySQL, Oracle, SQL Server, dan MongoDB.
- NoSQL Besar: mendukung bisnis NoSQL seperti HBase dan Cassandra.
- ElasticSearch: mendukung penyimpanan ES latensi rendah.
- Layanan video: cocok untuk aplikasi dengan kebutuhan bandwidth penyimpanan yang tinggi, seperti encoding dan decoding audio/video, streaming langsung, dan pemutaran rekaman.
- Analisis data besar: cocok untuk analisis data, penambangan data, inteligensi bisnis, dan bidang lainnya. Menyediakan kemampuan pemrosesan terdistribusi untuk data di tingkat TB dan PB.

**SSD Tremendous lebih cocok untuk skenario sensitif latensi yang membutuhkan latensi sangat rendah**, termasuk:
- Penyimpanan nilai utama (KV): mendukung rocksdb, etcd, dll. Layanan penyimpanan KV umumnya menulis data ke disk dalam mode I/O serial yang memerlukan latensi sangat rendah. Dengan demikian, latensi 1 putaran menentukan performa sistem secara keseluruhan. SSD Tremendous menjamin latensi serendah puluhan mikrodetik, membuatnya cocok untuk sistem bisnis inti dengan persyaratan keandalan dan ketersediaan data tinggi.
- Database besar: mendukung aplikasi database relasional menengah dan besar yang berisi tabel dengan jutaan baris, seperti MySQL, Oracle, SQL Server, dan MongoDB.
- NoSQL Besar: mendukung bisnis NoSQL seperti HBase dan Cassandra.
- ElasticSearch: mendukung penyimpanan ES latensi rendah.
- Layanan video: cocok untuk aplikasi dengan kebutuhan bandwidth penyimpanan yang tinggi, seperti encoding dan decoding audio/video, streaming langsung, dan pemutaran rekaman.
- Sistem bisnis inti: cocok untuk aplikasi intensif I/O dan sistem bisnis inti lainnya dengan persyaratan keandalan data tinggi.
- Analisis data besar: cocok untuk analisis data, penambangan data, inteligensi bisnis, dan bidang lainnya. Menyediakan kemampuan pemrosesan terdistribusi untuk data di tingkat TB dan PB.
- Performa tinggi dan keandalan data tinggi: cocok untuk sistem bisnis misi-kritis dengan beban tinggi. SSD menyediakan redundansi data tiga salinan dan dilengkapi dengan kemampuan komprehensif untuk pencadangan data, snapshot, dan pemulihan data dalam hitungan detik.

**SSD berlaku untuk aplikasi dengan beban tinggi dan sedang**, termasuk:
- Database sedang: aplikasi database relasional menengah dan besar, seperti MySQL.
- Pemrosesan gambar: mendukung analisis data dan bisnis penyimpanan, seperti pemrosesan gambar.

**Premium Cloud Storage cocok terutama untuk skenario data berikut**:
- Database kecil dan menengah dan server Web/Aplikasi. Memberikan performa I/O jangka panjang dan stabil.
- Skenario yang membutuhkan kapasitas dan performa penyimpanan yang seimbang, seperti layanan kantor perusahaan.
- Pengujian bisnis inti dan debugging front and back end.

## Deskripsi Penagihan
Untuk detail harga disk cloud, lihat [Ikhtisar Harga](https://intl.cloud.tencent.com/document/product/362/2413).
