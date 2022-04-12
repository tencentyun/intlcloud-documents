Deployment multi-AZ melindungi database Anda agar tidak terpengaruh oleh kegagalan instans database dan pemadaman AZ. Untuk informasi selengkapnya, silakan lihat [Wilayah dan AZ](https://intl.cloud.tencent.com/document/product/236/8458).
Skema deployment multi-AZ TencentDB for MySQL menjamin ketersediaan tinggi dan kemampuan failover instans database dengan menggabungkan beberapa AZ menjadi satu "multi-AZ".

>?
>- Tidak peduli apakah instans TencentDBfor MySQL dalam kluster database berjalan di beberapa AZ atau tidak, setiap instans memiliki slave untuk pencadangan real-time terkini untuk memastikan ketersediaan database yang tinggi.
>- Dengan deployment multi-AZ, TencentDB for MySQL secara otomatis mengatur dan memelihara replika slave sinkronisasi di AZ yang berbeda.
>- Instans database master direplikasi secara sinkron ke replika slave di seluruh AZ untuk menyediakan redundansi data, menghilangkan pembekuan I/O, dan meminimalkan latensi selama pencadangan sistem.

### Wilayah yang Didukung
Skema deployment multi-AZ TencentDB for MySQL saat ini tersedia di wilayah Guangzhou, Shanghai, Beijing, Chengdu, dan Virginia.

### Deployment Multi-AZ
1. Login ke [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/) dan klik **Create** (Buat) di Daftar Instans untuk masuk ke halaman pembelian.
2. Pada halaman pembelian TencentDB for MySQL, pilih wilayah yang didukung, dan pilih AZ slave yang diinginkan di opsi **Slave AZ** (Slave AZ).
>?Hanya AZ tertentu yang dapat dipilih sebagai slave AZ. Untuk informasi selengkapnya, silakan lihat halaman pembelian.
>
![](https://main.qcloudimg.com/raw/aec9d1b540ceff3426968c213cfe9435.png)
3. Setelah memastikan bahwa semuanya sudah benar, klik **Buy Now** (Beli Sekarang). Setelah melakukan pembayaran, Anda dapat kembali ke daftar instans untuk melihat instans multi-AZ yang baru dibeli.

### Failover
TencentDB for MySQL memproses failover secara otomatis, sehingga operasi database dapat dilanjutkan secepat mungkin tanpa memerlukan intervensi administratif. Instans database master akan secara otomatis beralih ke replika slave di slave AZ dalam kondisi berikut:
- Pemadaman AZ.
- Kegagalan instans database master.
