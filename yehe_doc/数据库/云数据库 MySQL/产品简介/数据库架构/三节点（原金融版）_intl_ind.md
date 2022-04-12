TencentDB for MySQL mendukung tiga jenis arsitektur: node tunggal, dua node, dan tiga node. Dokumen ini menjelaskan arsitektur tiga node.

- Instans tiga node mengadopsi arsitektur satu sumber dua replika dan mendukung replikasi sinkronisasi yang canggih. Mereka menjamin konsistensi data yang merata melalui pencadangan real-time terkini dan memberikan keandalan tingkat keuangan dan ketersediaan tinggi.
- Instans tiga node mendukung dua kebijakan isolasi sumber daya: umum dan khusus. Untuk informasi selengkapnya, lihat [Kebijakan Isolasi Sumber Daya](https://intl.cloud.tencent.com/document/product/236/39794).

## Kasus Penggunaan
Instans tiga node ideal untuk industri seperti game, internet, IoT, ritel, e-commerce, logistik, asuransi, dan sekuritas.

## Fitur
- Arsitektur tiga node mendukung mode replikasi sumber/replika seperti asinkron (default), sinkronisasi yang canggih, dan semi-sinkronisasi.
- Arsitektur tiga node mendukung serangkaian fitur lengkap termasuk instans baca saja, grup keamanan, migrasi data, dan deployment multi-AZ. Untuk informasi selengkapnya, lihat [Keunggulan](https://intl.cloud.tencent.com/document/product/236/5148).
- Arsitektur tiga node memperoleh ketersediaan tinggi hingga 99,99%. Untuk informasi selengkapnya, lihat [Perjanjian Tingkat Layanan TencentDB (Versi Baru)](https://intl.cloud.tencent.com/document/product/301/30977).
- Instans tiga node menyediakan banyak replika untuk menjamin persistensi data. Data node sumber dapat disinkronkan ke node replika; data instans sumber dapat disinkronkan ke instans baca saja (jika ada). Arsitektur ini memastikan keamanan data dan mencapai persistensi data hingga 99,99999%.
- Arsitektur tiga node men-deploy node data pada perangkat keras yang canggih dan menggunakan disk NVMe SSD lokal sebagai penyimpanan dasar dengan IOPS hingga 240.000 (nilai ini adalah hasil pengujian dengan ukuran halaman default MySQL 16 KB dan hanya untuk referensi Anda. Nilai aktual tunduk pada konfigurasi tertentu, ukuran halaman, dan beban bisnis).
- Anda dapat men-deploy dua node replika dari instans tiga node di zona ketersediaan yang sama (mis., Zona Beijing 5), tetapi strategi distribusi node default TencentDB memastikan bahwa node tersebut di-deploy pada server fisik yang berbeda. Anda juga dapat men-deploy dua node replika di zona ketersediaan yang berbeda (misalnya, satu node replika di Zona Beijing 5 dan yang lainnya di Zona Beijing 7).


## Peningkatan
- Versi mesin TencentDB for MySQL dapat ditingkatkan. Untuk informasi selengkapnya, lihat [Meningkatkan Mesin Database](https://intl.cloud.tencent.com/document/product/236/8126).
- Versi minor kernel dari TencentDB for MySQL dapat ditingkatkan secara otomatis atau manual. Untuk informasi selengkapnya, lihat [Meningkatkan Versi Kernel Minor](https://intl.cloud.tencent.com/document/product/236/36816).

