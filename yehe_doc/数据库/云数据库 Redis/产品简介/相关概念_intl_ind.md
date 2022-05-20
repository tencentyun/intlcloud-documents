
TencentDB for Redis umumnya melibatkan konsep berikut:

**Instans**: Lingkungan database yang berjalan secara independen di Tencent Cloud. Satu instans database dapat berisi beberapa database yang dibuat oleh pengguna.

[**VPC**](http://intl.cloud.tencent.com/document/product/215/535): Sebuah ruang jaringan virtual kustom yang secara logis diisolasi dari sumber daya lain.

[**Grup keamanan**](https://intl.cloud.tencent.com/document/product/239/31945): Kontrol akses keamanan ke instans Redis dengan menentukan IP, protokol, dan aturan port untuk akses instans.

[**Wilayah dan zona ketersediaan**](http://intl.cloud.tencent.com/document/product/239/4106): Lokasi fisik instans Redis dan sumber daya lainnya.

[**Konsol Tencent Cloud**](https://console.cloud.tencent.com/cdb): UI berbasis web.

[**Proyek**](http://intl.cloud.tencent.com/document/product/378/10863): Fitur yang dikembangkan untuk memungkinkan pengembang mengelola produk Tencent Cloud dengan lebih baik berdasarkan konsep proyek. Anda dapat menerapkan manajemen proyek dengan menetapkan produk Tencent Cloud yang berbeda ke proyek yang berbeda.

[**Pemisahan baca-tulis**](https://intl.cloud.tencent.com/document/product/239/31935): TencentDB for Redis mendukung mengaktifkan atau menonaktifkan pemisahan Baca-Tulis.  TencentDB for Redis menargetkan skenario bisnis dengan lebih banyak Baca dan lebih sedikit Tulis, yang dapat dengan baik mengatasi permintaan Baca yang berkonsentrasi pada data hotspot. Mendukung hingga mode 1-master 5-slave untuk menawarkan skalabilitas kinerja 5x Baca.
