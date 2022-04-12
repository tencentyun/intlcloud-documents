
Untuk aplikasi dengan persyaratan tinggi pada kontinuitas layanan, keandalan data, dan kepatuhan, TencentDB for MySQL menyediakan solusi pemulihan bencana lintas-AZ dan lintas-wilayah untuk membantu meningkatkan kemampuan Anda dalam memberikan layanan berkelanjutan dengan biaya rendah dan meningkatkan keandalan data.

### Pemulihan Bencana Dalam Wilayah
Anda dapat membuat instans TencentDB [dua node](https://intl.cloud.tencent.com/document/product/236/38328) dan [tiga node](https://intl.cloud.tencent.com/document/product/236/38328) untuk MySQL guna mendukung deployment multi-AZ. Server fisik instans multi-AZ disebarkan di AZ yang berbeda di wilayah yang sama. Ketika AZ gagal, lalu lintas bisnis akan dialihkan ke AZ lain dengan cepat, yang tidak terlihat oleh bisnis dan tidak memerlukan perubahan pada lapisan aplikasi untuk mencapai pemulihan bencana dalam wilayah.
>?Karena node instans multi-AZ berada di AZ yang berbeda, mungkin ada penundaan sinkronisasi jaringan tambahan sebesar 2-3 md.

Untuk informasi selengkapnya tentang pemulihan bencana dalam wilayah, lihat [Ketersediaan Tinggi (Beberapa AZ)](https://intl.cloud.tencent.com/document/product/236/8459).

### Pemulihan Bencana Lintas Wilayah
Kemampuan pemulihan bencana dalam wilayah TencentDB for MySQL terbatas pada AZ yang berbeda di wilayah yang sama. Untuk lebih meningkatkan ketersediaan, TencentDB for MySQL juga mendukung pemulihan bencana data lintas wilayah.

Anda dapat mereplikasi data secara asinkron dalam instans TencentDB for MySQL di wilayah A ke instans lain (instans pemulihan bencana) di wilayah B melalui DTS. Instans pemulihan bencana memiliki alamat, akun, dan izin koneksi independen. Jika kegagalan besar terjadi di wilayah A dan tidak dapat diperbaiki dalam waktu singkat, Anda dapat melakukan failover kapan pun diperlukan. Secara khusus, Anda dapat dengan cepat meneruskan permintaan aplikasi ke instans pemulihan bencana hanya dengan memodifikasi konfigurasi koneksi database dalam aplikasi, sehingga memberikan ketersediaan database tingkat keuangan.

Untuk informasi selengkapnya tentang pemulihan bencana lintas wilayah, lihat [Instans Pemulihan Bencana](https://intl.cloud.tencent.com/document/product/236/7272).

