## Pencegahan Serangan DDoS
Saat menggunakan jaringan publik untuk terhubung dan mengakses instans TencentDB for MySQL, Anda mungkin mengalami serangan DDoS. Untuk mengatasi masalah ini, Tencent Cloud menyediakan fitur pembersihan dan pemblokiran lalu lintas yang dipicu dan dihentikan secara otomatis oleh sistem. Saat sistem Anti-DDoS mendeteksi bahwa instans Anda sedang diserang, sistem akan secara otomatis mengaktifkan pembersihan lalu lintas atau memblokir lalu lintas jika serangan tidak dapat dilawan dengan membersihkan atau mencapai ambang batas pemblokiran.
>!Anda disarankan mengakses instans TencentDB for MySQL melalui jaringan pribadi untuk menghindari serangan DDoS.

### Pembersihan lalu lintas
Ketika lalu lintas jaringan publik dari instans TencentDB for MySQL melebihi ambang batas, Anti-DDoS akan secara otomatis membersihkan lalu lintas masuk ke instans. Perutean berbasis kebijakan akan digunakan untuk mengarahkan lalu lintas dari rute jaringan asli ke perangkat pembersihan DDoS Anti-DDoS, yang akan mengidentifikasi lalu lintas jaringan publik, membuang lalu lintas serangan, dan meneruskan lalu lintas normal ke instans.

### Memblokir
Ketika lalu lintas serangan yang dialami oleh instans TencentDB for MySQL melebihi ambang pemblokiran, Tencent Cloud akan memblokir semua permintaan akses jaringan publik ke instans ini melalui layanan ISP yang berlaku untuk mencegah terpengaruhnya pengguna Tencent Cloud lainnya. Ini artinya jika bandwidth lalu lintas serangan yang dialami oleh instans Anda melebihi bandwidth perlindungan maksimalnya, Tencent Cloud akan memblokir semua permintaan akses jaringan publik ke sana.
- Saat kondisi berikut terpenuhi, pemblokiran akan dipicu:
 - Nilai bit per detik (bps) mencapai 2 Gbps.
 - Pembersihan lalu lintas tidak efektif.
- Saat kondisi berikut terpenuhi, pemblokiran akan dihentikan:
 - 2 jam berlalu setelah pemblokiran dimulai.
