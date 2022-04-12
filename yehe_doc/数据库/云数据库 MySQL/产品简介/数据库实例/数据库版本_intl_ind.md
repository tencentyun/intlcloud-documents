## Versi yang Didukung
Saat ini, TencentDB for MySQL mendukung MySQL v8.0, v5.7, v5.6, dan v5.5. Untuk informasi selengkapnya tentang fitur setiap versi, silakan lihat [dokumentasi resmi](https://dev.mysql.com/doc/refman/5.7/en/). Kebijakan dukungan siklus pemakaian resmi MySQL adalah seperti yang ditunjukkan di bawah ini:

| Rilis            | Tanggal GA | Dukungan Premier Berakhir | Dukungan Diperpanjang Berakhir | Dukungan Berkelanjutan Berakhir |
| :------------------ | :------- | :------------ | :------------- | :-----------|
| Database MySQL 5.0 | 05 Okt | 11 Des | Tidak Tersedia        | Tak terbatas             |
| Database MySQL 5.1 | Des-08 | 13 Des              | Tidak Tersedia        |Tak terbatas             |
| Database MySQL 5.5 | 10 Des | 15 Des              | 18 Des               |Tak terbatas             |
| Database MySQL 5.6 | 13 Februari | 18 Februari              | 21 Februari               | Tak terbatas             |
| Database MySQL 5.7 | 15 Okt | 20 Okt | 23 Okt               | Tak terbatas             |
| Database MySQL 8.0 | 18 April | 23 April | 26 April               | Tak terbatas             |

>?
> - Dukungan resmi diperpanjang untuk MySQL v5.5 berakhir pada Desember 2018. Belum ada pernyataan yang jelas tentang perpanjangan dukungan lebih lanjut, yang mungkin karena memperbaiki masalah membutuhkan lebih banyak waktu. Kami sangat menyarankan Anda menggunakan versi MySQL yang lebih tinggi.
> - MySQL v5.6 dan yang lebih tinggi tidak lagi mendukung mesin penyimpanan MyISAM, jadi kami sarankan Anda menggunakan mesin InnoDB, yang menampilkan performa yang lebih baik dan lebih stabil.
> - Saat ini, MySQL v5.6 dan yang lebih tinggi mendukung tiga mode replikasi: asinkron, semi-sinkronasi, dan sinkronasi yang canggih. Hanya mode asinkron yang tersedia di MySQL v5.5.


## Keunggulan TencentDB for MySQL v8.0
- Dikombinasikan dengan satu set lengkap layanan manajemen dan kernel TXSQL, TencentDB for MySQL menyediakan layanan database tingkat perusahaan yang lebih stabil dan lebih cepat untuk di-deploy. Ini berlaku untuk berbagai kasus penggunaan dan membantu Anda meningkatkan bisnis Anda.
- TXSQL 100% kompatibel dengan MySQL dan fork MySQL yang banyak digunakan.
- TencentDB for MySQL mendukung tiga sistem pemulihan bencana termasuk siaga panas, siaga dingin, dan peralihan multi-AZ. Ini dapat mencapai ketersediaan layanan hingga 99,95% dan keandalan data hingga 99,9996%.
- TencentDB for MySQL menyediakan satu set lengkap layanan manajemen database yang mudah digunakan, termasuk pemantauan, pencadangan, rollback, enkripsi, penskalaan otomatis, audit, serta diagnosis dan pengoptimalan cerdas, memungkinkan Anda untuk lebih fokus pada pengembangan bisnis.
- Instans TencentDB for MySQL dapat menangani 500.000+ QPS. TencentDB for MySQL sangat menyederhanakan pengembangan bisnis, OPS database, dan arsitektur bisnis, sehingga memudahkan Anda untuk mengelola database.
- Beragam arsitektur: node tunggal, dua node, dan tiga node
- Mendukung CStore, mesin penyimpanan kolumnar berperforma tinggi, mendukung jutaan penulisan real-time per detik dan kueri real-time dalam dimensi apa pun dari puluhan miliar data dalam milidetik. Untuk mendaftar CSStore, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).

## Perbandingan Fitur antara TencentDB for MySQL v8.0 dan Oracle MySQL v8.0

| Fitur | TencentDB for MySQL v8.0                                 | Oracle MySQL v8.0                                         |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Performa biaya | 1. Sumber daya elastis. <br>2. TXSQL kernel Tencent. <br>3. Fitur pencadangan dan pemulihan terintegrasi. <br>4. Satu set lengkap alat dan layanan SaaS. | 1. Biaya investasi satu kali yang besar. <br>2. Versi sumber daya terbuka tidak memiliki pengoptimalan performa. <br>3. Sumber daya dan biaya cadangan tambahan. <br>4. Biaya jaringan publik dan biaya nama domain yang tinggi. |
| Ketersediaan | 1. Tersedia sistem peralihan ketersediaan tinggi yang lengkap. <br>2. Replika baca-saja secara otomatis menyeimbangkan beban dan lalu lintas. <br>3. Instans pemulihan bencana disediakan untuk pemulihan bencana jarak jauh, memastikan ketersediaan tinggi. | 1. Anda perlu membeli server dan menunggu pengiriman. <br>2. Anda perlu men-deploy ketersediaan tinggi dan sistem penyeimbangan beban sendiri. <br>3. Biayanya banyak untuk membangun pusat data di banyak wilayah. |
| Keandalan | 1. Keandalan data hingga 99,9996%. <br>2. RPO/RTO rendah. <br>3. Replikasi data sumber-replika yang stabil. | 1. Keandalan data 99%, yang tergantung pada kemungkinan kerusakan pada satu disk. <br>2. Anda membutuhkan investasi R&D ekstra untuk mencapai RPO yang rendah. <br>3. Penundaan atau gangguan replikasi data dapat terjadi. |
| Kemudahan penggunaan | 1. Satu set lengkap layanan manajemen database disediakan dan database dapat dengan mudah dioperasikan di konsol. <br>2. Pemantauan tingkat detik dan alarm cerdas. <br>3. Sistem ketersediaan tinggi multi-AZ otomatis. <br>4. Peningkatan versi sekali klik. | 1. Anda perlu men-deploy ketersediaan tinggi dan sistem pencadangan dan pemulihan sendiri, yang membutuhkan waktu dan uang. <br>2. Anda membutuhkan investasi ekstra untuk membeli sistem pemantauan. <br>3. Biayanya banyak untuk menyiapkan pusat data di berbagai wilayah dengan biaya tenaga kerja di OPS. <br>4. Biaya peningkatan versi tinggi dan pemeliharaan membutuhkan waktu henti yang lama. |
| Performa | 1. Disk SSD lokal memiliki performa yang sangat baik dan perangkat keras khusus mendukung iterasi yang cepat. <br>2. TXSQL yang dioptimalkan memastikan performa tinggi. <br>3. DBbrain mendukung diagnosis cerdas dan optimalisasi MySQL. | 1. Oracle MySQL memiliki kecepatan iterasi perangkat keras yang lebih lambat daripada komputasi cloud, biasanya menghasilkan performa yang lebih rendah. <br>2. Biayanya bisa mahal karena database bergantung pada DBA senior. <br>3. Oracle MySQL tidak memiliki alat performa asli, jadi Anda harus membeli atau men-deploy-nya sendiri. |
| Keamanan | 1. Pencegahan sebelumnya: daftar yang diizinkan, grup keamanan, isolasi berbasis VPC. <br>2. Perlindungan selama operasi database: Enkripsi data TDE + KMS. <br>3. Audit setelah operasi database: Audit SQL. <br>4. TencentDB for MySQL diperbarui tepat setelah Oracle MySQL memiliki pembaruan keamanan. | 1. Biaya konfigurasi daftar yang diizinkan tinggi dan jaringan pribadi perlu diterapkan sendiri. <br>2. Anda perlu menerapkan enkripsi sendiri selama operasi database. <br>3. Sulit untuk mengaudit SQL setelah operasi database karena MySQL sumber terbuka tidak mendukung audit SQL. <br>4. Setelah MySQL diperbarui, OPS akan diminta untuk menginstal pembaruan atau database harus dimatikan untuk pemeliharaan. |

## Perbandingan Performa antara TencentDB for MySQL v8.0 dan Oracle MySQL v8.0
#### Performa baca
![](https://main.qcloudimg.com/raw/1bf9f7294ca6b4631f203333819ab2a1.png)

#### Performa tulis
![](https://main.qcloudimg.com/raw/f77b34eb5c769539325b2f04a539ad4f.png)

