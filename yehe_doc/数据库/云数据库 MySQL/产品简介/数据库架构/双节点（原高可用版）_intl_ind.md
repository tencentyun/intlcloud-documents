TencentDB for MySQL mendukung tiga jenis arsitektur: node tunggal, dua node, dan tiga node. Dokumen ini menjelaskan arsitektur dua node.

- Instans dua node mengadopsi arsitektur satu sumber dengan satu-replika yang sangat tersedia dan mendukung pencadangan real-time terkini, deteksi kegagalan otomatis, dan kegagalan otomatis.
- Instans dua node mendukung dua kebijakan isolasi sumber daya: umum dan khusus. Untuk informasi selengkapnya, lihat [Kebijakan Isolasi Sumber Daya](https://intl.cloud.tencent.com/document/product/236/39794).

## Kasus Penggunaan
Instans dua node ideal untuk industri seperti game, internet, IoT, ritel, e-commerce, logistik, asuransi, dan sekuritas.

## Fitur
- Arsitektur dua node menawarkan dua mode replikasi sumber/replika: asinkron (default) dan semi-sinkronisasi. Anda dapat mengubah mode replikasi atau [meningkatkan ke arsitektur tiga node](https://intl.cloud.tencent.com/document/product/236/35986) (dengan mode sinkronisasi canggih untuk satu-sumber dengan dua-replika) pada halaman detail instans di [konsol](https://console.cloud.tencent.com/cdb).
- Arsitektur dua node mendukung serangkaian fitur lengkap termasuk instans baca saja, grup keamanan, migrasi data, dan deployment multi-AZ. Untuk informasi selengkapnya, lihat [Keunggulan](https://intl.cloud.tencent.com/document/product/236/5148).
- Arsitektur dua node mencapai ketersediaan tinggi hingga 99,95%. Untuk informasi selengkapnya, lihat [Perjanjian Tingkat Layanan TencentDB (Versi Baru)](https://intl.cloud.tencent.com/document/product/301/30977).
- Instans dua node menyediakan banyak replika untuk menjamin persistensi data. Data node sumber dapat disinkronkan ke node replika; data instans sumber dapat disinkronkan ke instans baca saja (jika ada). Arsitektur ini memastikan keamanan data dan mencapai persistensi data hingga 99,99999%.
- Arsitektur dua node men-deploy node data pada perangkat keras yang canggih dan menggunakan disk NVMe SSD lokal sebagai penyimpanan dasar dengan IOPS hingga 240.000 (nilai ini adalah hasil pengujian dengan ukuran halaman default MySQL 16 KB dan hanya untuk referensi Anda. Nilai aktual tunduk pada konfigurasi tertentu, ukuran halaman, dan beban bisnis).

## Diagram Kerangka Dasar
![Teks alternatif](https://main.qcloudimg.com/raw/19d5619f983d3dc550b3218c0520b447.png)

## Peningkatan
- Versi mesin TencentDB for MySQL dapat ditingkatkan. Untuk informasi selengkapnya, lihat [Meningkatkan Mesin Database](https://intl.cloud.tencent.com/document/product/236/8126).
- TencentDB for MySQL dapat ditingkatkan dari arsitektur dua node ke arsitektur tiga node. Untuk informasi selengkapnya, lihat [Meningkatkan Dua Node Instans ke Tiga Node](https://intl.cloud.tencent.com/document/product/236/35986).
- Versi minor kernel dari TencentDB for MySQL dapat ditingkatkan secara otomatis atau manual. Untuk informasi selengkapnya, lihat [Meningkatkan Versi Minor Kernel](https://intl.cloud.tencent.com/document/product/236/36816).
