## Ikhtisar
Ruang cadangan digunakan untuk menyimpan cadangan semua instans TencentDB for MySQL di wilayah tertentu. Cadangan ini dapat berupa pencadangan otomatis, manual, dan log.

TencentDB for MySQL menawarkan sejumlah kapasitas cadangan secara gratis berdasarkan wilayah. Kapasitas tersebut setara dengan jumlah kapasitas penyimpanan semua instans dua node dan tiga node (termasuk instans sumber dan pemulihan bencana) di wilayah tersebut. Untuk contoh perhitungan, lihat [Rumus Perhitungan](#jfgs).
>?
>- Ruang cadangan gratis disediakan saat membeli sumber atau instans pemulihan bencana tetapi tidak akan tersedia jika instans baca saja.
>- Kapasitas pencadangan dapat dilihat pada laman pencadangan database di [konsol TencentDB for MySQL](https://console.cloud.tencent.com/mysql/backup/index).

## Harga Pencadangan
Penggunaan kapasitas cadangan yang melebihi tingkat gratis akan dikenakan biaya sebesar 0,000127 USD/GB/jam di daratan Tiongkok. Untuk harga wilayah di luar daratan Tiongkok, lihat [Kalkulator Harga TencentDB for MySQL](https://buy.intl.cloud.tencent.com/price/cdb/calculator).
Jika kelebihan kapasitas cadangan kurang dari 1 GB, tidak ada biaya yang akan dikenakan. Jika kurang dari 1 jam, jangka waktunya akan dihitung sebagai 1 jam. TencentDB for MySQL mengadopsi kebijakan pemberian yang fleksibel, sehingga Anda biasanya tidak perlu membayar kapasitas cadangan untuk sebagian besar instans.

## Jadwal Penagihan untuk Kapasitas Pencadangan
- Penagihan resmi dimulai dari pukul 00.00 pada tanggal 2 Desember 2019 untuk Hong Kong (Tiongkok), Makao (Tiongkok), Taiwan (Tiongkok), dan wilayah lain di luar daratan Tiongkok.
- Penagihan resmi dimulai dari 00.00 pada 2 Desember 2019 untuk Tiongkok Barat Daya (wilayah Chengdu dan Chongqing).
- Penagihan resmi dimulai dari 00.00 pada tanggal 5 Desember 2019 untuk Tiongkok Selatan (wilayah Guangzhou).
- Penagihan resmi dimulai dari 00.00 pada tanggal 9 Desember 2019 untuk Tiongkok Utara (wilayah Beijing).
- Penagihan resmi dimulai pukul 00.00 pada 10 Desember 2019 untuk Tiongkok Timur (wilayah Shanghai).
- Penagihan dimulai secara default untuk wilayah yang ditambahkan setelah pukul 00.00 pada 10 Desember 2019.


## [Rumus Perhitungan](id:jfgs)
**Free backup capacity in one region = Sum of storage capacity of all TencentDB for MySQL two-node and three-node instances in that region** (Kapasitas pencadangan gratis di satu wilayah = Jumlah kapasitas penyimpanan semua instans dua node dan tiga node TencentDB for MySQL di wilayah tersebut)

**Paid backup capacity in one region = Data backup volume + log backup volume - free backup capacity (all values are for that region)** (Kapasitas cadangan berbayar di satu wilayah = Volume cadangan data + volume cadangan log - kapasitas cadangan gratis (semua nilai untuk wilayah tersebut))

>?Pencadangan instans TencentDB for MySQL di keranjang sampah juga akan dihitung ke dalam total kapasitas cadangan.

**Calculation Example** (Contoh Perhitungan)
Jika Anda menjalankan instans dua node TencentDB for MySQL dengan kapasitas penyimpanan database yang dibeli sebesar 500 GB/bulan di Zona Guangzhou 3 dan instans serupa lainnya dengan kapasitas penyimpanan database yang dibeli sebesar 200 GB/bulan di Zona Guangzhou 4, Anda akan dapatkan kapasitas cadangan gratis 700 GB/bulan di wilayah Guangzhou.

Penggunaan kapasitas cadangan yang melebihi tingkat gratis dihitung per jam sesuai dengan aturan berikut. Misalnya, jika cadangan data Anda mencapai 800 GB dan cadangan log mencapai 100 GB, total penggunaan kapasitas cadangan Anda di Guangzhou akan melebihi 700 GB, dan kapasitas cadangan yang dapat ditagih per jam Anda akan menjadi 200 GB (800 + 100 - 700 = 200).


## Siklus Hidup Pencadangan
### [Instans Bayar Sesuai Pemakaian](id:anliang_zhouqi)
- Pencadangan dapat berubah selama siklus hidup instans.
- Pencadangan dapat bekerja secara normal dalam waktu 24 jam setelah pembayaran instans terlambat.
- Setelah 24 jam sejak pembayaran instans terlambat, instans akan diisolasi ke dalam keranjang sampah. Saat ini, pencadangan otomatis berhenti, dan pengembalian serta pencadangan manual dilarang, tetapi pencadangan masih dapat diunduh (di [Daftar Cadangan](https://console.cloud.tencent.com/mysql/backup/list/data). Kapasitas cadangan yang berlebihan akan tetap ditagih hingga instans dihapus. Anda dapat memperbarui instans di keranjang sampah di konsol untuk memulihkannya.
- Setelah tiga hari sejak instans diisolasi di keranjang sampah, instans tersebut dihilangkan (yaitu, dihapus sepenuhnya) bersama dengan semua cadangan data. Harap simpan cadangan yang diperlukan tepat waktu.

## Pembayaran Jatuh Tempo
### Instans Bayar Sesuai Pemakaian
Setelah akun jatuh ke tunggakan, cadangan akan berubah dengan siklus hidup instans. Untuk informasi selengkapnya, lihat siklus hidup pencadangan instans bayar sesuai pemakaian seperti yang dijelaskan di atas.

## Layanan yang Ditingkatkan Tersedia Setelah Penagihan Cadangan Dimulai
>? Nilai yang tercantum dalam tabel di bawah ini adalah nilai maksimum yang didukung di wilayah yang sama di bawah satu akun Tencent Cloud.

| Peningkatan | Sebelum Peningkatan | Setelah Peningkatan |
| ------------------ | -------------- | --------------- |
| Periode retensi cadangan data | 30 hari | 1.830 hari |
| Periode retensi cadangan log | 5 hari | 1.830 hari |
| Tingkat kompresi cadangan | Umum | Sangat Tinggi |
| sentralisasi binlog | Penyimpanan lokal | Penyimpanan terpusat |

## Saran untuk Mengurangi Biaya Pencadangan
- Hapus cadangan manual yang tidak lagi diperlukan. Anda dapat masuk ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans, dan menghapus backup manual di tab **Backup and Restoration** (Pencadangan dan Pemulihan). Pencadangan otomatis tidak dapat dihapus secara manual di konsol. Sebaliknya, pencadangan secara otomatis dihapus setelah kedaluwarsa.
- Kurangi frekuensi pencadangan data otomatis untuk bisnis non-inti (Anda dapat menyesuaikan siklus pencadangan dan periode retensi di konsol, dan frekuensinya harus setidaknya dua kali seminggu).
>?[Fitur pengembalian](https://intl.cloud.tencent.com/document/product/236/7276) bergantung pada siklus pencadangan dan hari penyimpanan pencadangan data dan pencadangan log (binlog). Pengembalian akan terpengaruh jika Anda mengurangi frekuensi pencadangan otomatis dan periode retensi. Harap pilih parameter sesuai kebutuhan.
>
- Kurangi periode penyimpanan data dan pencadangan log untuk bisnis non-inti (periode penyimpanan 7 hari dapat memenuhi persyaratan sebagian besar skenario).

| Skenario Bisnis             | Periode Retensi Cadangan yang Direkomendasikan                                                 |
| -------------------- | ------------------------------------------------------------ |
| Bisnis inti             | 7-1.830 hari                                              |
| Bisnis non-inti dan non-data | 7 hari                                                      |
| Bisnis arsip             | 7 hari. Sebaiknya cadangkan data secara manual berdasarkan kebutuhan bisnis Anda dan segera hapus cadangan setelah digunakan |
| Bisnis pengujian | 7 hari. Sebaiknya cadangkan data secara manual berdasarkan kebutuhan bisnis Anda yang sebenarnya dan segera hapus cadangan setelah digunakan |

