Artikel ini bertujuan untuk membantu pengguna meningkatkan keamanan dan keandalan instans CVM mereka.

## Keamanan dan Jaringan

- **Limited access** (Akses terbatas): membatasi akses menggunakan firewall ([Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/12452) yang hanya akan mengizinkan alamat tepercaya untuk mengakses instans. Grup keamanan juga harus memiliki aturan ketat seperti membatasi akses ke port dan berdasarkan alamat IP.
- **Security level** (Tingkat keamanan): aturan grup keamanan yang berbeda dapat dibuat untuk grup instans dengan tingkat keamanan yang berbeda untuk memastikan bahwa instans yang menjalankan bisnis penting tidak dapat diakses dengan mudah oleh sumber eksternal.
- **Network logical isolation** (Isolasi logika jaringan): menggunakan [VPC](https://intl.cloud.tencent.com/document/product/213/5227) untuk membagi sumber daya ke dalam zona logis.
- **Account permission management** (Pengelolaan izin akun): jika diperlukan untuk mengizinkan beberapa akun yang berbeda mengakses kumpulan sumber daya cloud yang sama, Anda dapat mengelola izin sumber daya cloud menggunakan [mekanisme kebijakan](https://intl.cloud.tencent.com/document/product/598/10601).
- **Secure login** (Login aman): login ke instans Linux Anda menggunakan [kunci SSH](https://intl.cloud.tencent.com/document/product/213/6092) jika memungkinkan. Jika Anda [login dengan kata sandi](https://intl.cloud.tencent.com/document/product/213/6093), sebaiknya ubah kata sandi secara berkala.

## Penyimpanan

- **Hardware storage** (Penyimpanan perangkat keras): untuk data yang memerlukan keandalan tinggi, gunakan disk cloud Tencent Cloud untuk memastikan penyimpanan dan keandalan data yang persisten. Cobalah untuk tidak menggunakan [Disk Lokal](https://intl.cloud.tencent.com/document/product/213/5798) untuk penyimpanan. Untuk informasi selengkapnya, lihat [Dokumentasi Produk Cloud Block Storage](https://intl.cloud.tencent.com/document/product/362).
- **Database:** (Database:) untuk database yang sering diakses dan kapasitasnya sering berubah, gunakan Tencent Cloud TencentDB.

## Pencadangan dan Pemulihan

- **Intra-region instance backup** (Pencadangan instans dalam wilayah): Anda dapat mencadangkan instans dan data bisnis Anda menggunakan **custom images** (citra kustom) dan **CBS snapshots** (snapshot CBS). Untuk informasi selengkapnya, lihat [Snapshot CBS](https://intl.cloud.tencent.com/document/product/362/31638) dan [Membuat Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4942).
- **Cross-region instance backup** (Pencadangan instans lintas wilayah): Anda dapat menyalin dan mencadangkan instans di seluruh wilayah dengan [Menyalin Citra](https://intl.cloud.tencent.com/document/product/213/4943).
- **Blocking instance failures** (Memblokir kegagalan instans): Anda dapat menggunakan [EIP](https://intl.cloud.tencent.com/document/product/213/5733) untuk pemetaan nama domain guna memastikan bahwa server dapat mengalihkan alamat IP layanan ke instans CVM lain dengan cepat saat tidak tersedia, sehingga melindungi kegagalan instans.

## Pemantauan dan Alarm
- **Monitoring and event response** (Pemantauan dan respons peristiwa): memeriksa data pemantauan dan mengatur alarm yang tepat secara berkala. Untuk informasi selengkapnya, lihat [Dokumentasi Produk Cloud Monitor](https://intl.cloud.tencent.com/document/product/248).
- **Handling request spikes** (Menangani lonjakan permintaan): dengan [Penskalaan Otomatis](https://intl.cloud.tencent.com/document/product/377), stabilitas CVM selama jam sibuk dapat dijamin dan instans yang tidak sehat dapat diganti secara otomatis.
