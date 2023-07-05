
### Apa yang dimaksud dengan instans Big Data D1?

Instans Big Data D1 dirancang khusus untuk komputasi terdistribusi Hadoop, pemrosesan log masif, sistem file terdistribusi, gudang data besar, dan skenario bisnis lainnya. Jenis instans CVM ini terutama digunakan untuk memecahkan masalah komputasi cloud dan penyimpanan data bisnis dalam skala yang sangat besar.

### Pelanggan industri dan skenario bisnis mana yang berlaku untuk instans Big Data D1?

Instans Big Data D1 berlaku untuk pelanggan di Internet, game, keuangan, dan industri lain yang memerlukan komputasi big data dan analisis penyimpanan, serta skenario bisnis yang memerlukan penyimpanan data besar dan komputasi offline. Itu dapat memenuhi persyaratan penyimpanan, kapasitas, dan bandwidth jaringan pribadi dari bisnis komputasi terdistribusi yang diwakili oleh Hadoop.
Selain itu, dengan kerangka arsitektur bisnis komputasi terdistribusi yang sangat tersedia yang diwakili oleh Hadoop, instans Big Data D1 menampilkan desain penyimpanan lokal untuk mencapai biaya total yang mendekati biaya kluster Hadoop yang dibangun sendiri pada IDC offline, sambil memastikan kapasitas penyimpanan yang besar dan performa tinggi.

### Fitur instans Big Data D1

* Instans tunggal memiliki kapasitas throughput hingga 2,3 GB/dtk. Disk lokal HDD adalah pilihan terbaik untuk penyimpanan intensif throughput. Dengan throughput baca/tulis sekuensial yang stabil dan berperforma tinggi, instans Big Data D1 dirancang khusus untuk komputasi terdistribusi Hadoop, pemrosesan log yang besar, gudang data besar, dan skenario bisnis lainnya.
* Penyimpanan lokal memiliki harga satuan serendah 1/10. Instans Big Data D1 memiliki kapasitas penyimpanan yang besar dan performa tinggi, sekaligus memastikan efisiensi biaya yang optimal untuk skenario data besar. Ini memiliki total biaya yang mendekati kluster Hadoop yang dibangun sendiri pada IDC offline.
* Latensi baca/tulis diminimalkan menjadi 2 ms-5 ms. Instans Big Data D1, dengan model berperforma tinggi dan tingkat perusahaan, cocok untuk pengembang perusahaan.
*Mendukung metode penagihan bayar sesuai pemakaian.

### Spesifikasi instans Big Data D1

| Model | vCPU (inti) | Memori (GB) | Disk Data Lokal | Bandwidth Jaringan Pribadi | Catatan |
|-------|----|------|------|------|------|
| D1.2XLARGE32 | 8 | 32 | 2 × 3720 GB | 1,5 Gbps | - |
| D1.4XLARGE64 | 16 | 64 | 4 × 3720 GB | 3 Gbps | - |
| D1.6XLARGE96 | 24 | 96 | 6 × 3720 GB | 4,5 Gbps | - |
| D1.8XLARGE128 | 32 | 128 | 8 × 3720 GB | 6 Gbps | - |
| D1.14XLARGE224 | 56 | 224 | 12× 3720 GB | 10 Gbps | Eksklusif untuk host |

### Catatan tentang penyimpanan data lokal untuk instans Big Data D1

Instans Big Data D1 menggunakan disk lokal sebagai disk data, yang dapat menyebabkan **data loss** (kehilangan data) (misalnya, saat host mengalami kesalahan). Jika aplikasi Anda tidak dapat menjamin keandalan data, sebaiknya pilih instans yang dapat menggunakan cloud disk sebagai disk data.

Hubungan antara pengoperasian pada instans dengan disk lokal dan penyimpanan data adalah sebagai berikut:

| Operasi | Status Data Disk Lokal | Deskripsi |
|------|-----|-----|
| Mulai ulang sistem operasi/Mulai ulang konsol/Mulai ulang paksa | Dipertahankan | Penyimpanan disk lokal dipertahankan. Data dipertahankan. |
| Pematian sistem operasi/Penutupan konsol/Mati paksa | Dipertahankan | Penyimpanan disk lokal dipertahankan. Data dipertahankan. |
| Hentikan (instans) di konsol | Dihapus | Penyimpanan disk lokal dihapus. Tidak ada data yang disimpan. |

> Jangan menyimpan data bisnis yang perlu disimpan dalam waktu lama di disk lokal. Cadangkan data terlebih dahulu dan gunakan arsitektur dengan ketersediaan tinggi. Untuk penyimpanan jangka panjang, kami sarankan Anda menyimpan data di disk CBS.

### Bagaimana cara membeli disk lokal Big Data D1?

Disk lokal tidak dapat dibeli secara terpisah. Anda hanya dapat membeli disk lokal saat membuat instans D1. Jumlah dan kapasitas disk lokal bergantung pada spesifikasi instans.

### Apakah penyimpanan lokal instans Big Data D1 mendukung snapshot?
Tidak.

### Apakah instans Big Data D1 mendukung penyesuaian konfigurasi dan failover?

Penyesuaian konfigurasi tidak didukung.
Instans Big Data D1 menampilkan penyimpanan data yang sangat besar dan menggunakan HDD lokal sebagai disk data. Jenis instans ini tidak mendukung failover disk data (mis., saat host macet atau disk lokal rusak). Untuk mencegah kehilangan data, kami sarankan Anda menggunakan kebijakan redundansi, misalnya, sistem file yang mendukung redundansi dan toleransi kesalahan (seperti HDFS dan Mapr-FS). Selain itu, kami sarankan Anda untuk mencadangkan data secara rutin ke sistem penyimpanan persisten, seperti Tencent COS. Untuk informasi selengkapnya, lihat [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436).
Setelah disk lokal rusak, Anda harus mematikan instans CVM agar kami dapat mengubah disk lokal. Jika instans CVM macet, kami akan memberi tahu Anda dan memperbaikinya.

### Di wilayah mana saya dapat membeli instans Big Data D1?

Zona ketersediaan berikut didukung:
* Zona 2 Shanghai
* Zona 2 Beijing
* Zona 3 Guangzhou


### Mengapa saya tidak dapat menemukan disk data setelah membeli instans Big Data D1?

Disk lokal instans Big Data D1 tidak dipasang secara otomatis. Anda dapat memasangnya sesuai kebutuhan.

### Apa perbedaan antara instans Big Data D1 dan instans High IO I2?

Instans High IO I2 adalah instans CVM yang dirancang khusus untuk skenario bisnis dengan latensi rendah dan IO acak tinggi. Ini memiliki performa IOPS ultra-tinggi, dan digunakan terutama untuk database berperforma tinggi (database relasional, NoSQL, dll.). Instans Big Data D1 adalah instans CVM yang dirancang khusus untuk skenario bisnis yang memerlukan baca/tulis berurutan tinggi dan penyimpanan data masif berbiaya rendah. Instans ini dilengkapi penyimpanan berperforma tinggi dengan efisiensi biaya dan bandwidth jaringan pribadi yang dikonfigurasi dengan benar.

### Bagaimana throughput disk instans Big Data D1?

Ambil D1.14XLARGE224 sebagai contoh, throughput baca/tulis berurutan dari disk lokal instans Big Data D1 adalah sebagai berikut:
* Untuk satu disk, kecepatan baca/tulis berurutan adalah 190+ MB/dtk (ukuran blok 128 KB dan kedalaman 32).
* Untuk 12 disk, kecepatan baca/tulis berurutan secara bersamaan adalah 2,3+ GB/dtk (ukuran blok 128 KB dan kedalaman 32).

### Apa perbedaan antara disk lokal instans Big Data D1 dan CBS?

[Cloud Block Storage](https://intl.cloud.tencent.com/document/product/362) menyediakan perangkat penyimpanan yang sangat efisien dan andal untuk instans CVM. Ini adalah perangkat penyimpanan blok yang dapat disesuaikan dengan ketersediaan tinggi, keandalan tinggi, dan biaya rendah, dan dapat digunakan sebagai disk skalabel independen untuk CVM. Ini menyediakan penyimpanan data di tingkat blok data dan menggunakan mekanisme terdistribusi 3-salinan untuk memastikan keandalan data untuk instans CVM, memenuhi persyaratan skenario aplikasi yang berbeda. Disk lokal instans Big Data D1 dirancang khusus untuk skenario bisnis yang memerlukan baca/tulis sekuensial tinggi untuk kumpulan data lokal besar, seperti komputasi terdistribusi Hadoop, komputasi paralel skala besar, dan gudang data.

