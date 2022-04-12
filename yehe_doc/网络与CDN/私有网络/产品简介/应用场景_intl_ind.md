## Mengakses Internet
### Satu CVM
Ketika lalu lintas ke bisnis Anda rendah dan hanya satu CVM yang tersedia, Anda dapat menerapkan untuk alamat IP publik dan mengikatnya dengan CVM untuk mendapatkan akses ke Internet.
![](https://main.qcloudimg.com/raw/623ba575db31584481e7b660f8b1dec0.png)

### Beberapa CVM
Bila Anda memiliki beberapa CVM yang perlu mengakses Internet secara bersamaan dan Anda tidak ingin alamat jaringan pribadi CVM terekspos, Anda dapat menggunakan [Gateway NAT](https://intl.cloud.tencent.com/document/product/1015). Gateway NAT menyediakan fitur SNAT dan memungkinkan beberapa CVM untuk mengakses Internet dengan alamat IP publik di gateway NAT. Selain itu, tanpa konfigurasi fitur DNAT, pengguna eksternal tidak dapat mengakses langsung gateway NAT, yang memastikan keamanannya. Ketika beberapa alamat IP publik ada di gateway NAT, gateway NAT secara otomatis melakukan penyeimbangan beban.
![](https://main.qcloudimg.com/raw/79cf9f746c93cdce4a2e01bb6ece0297.png)

## Menyediakan Layanan ke Internet
### Satu CVM
Anda dapat mengelola layanan (seperti layanan situs web) pada CVM berbasis VPC dan menggunakan alamat IP publik untuk menyediakan layanan kepada pengguna eksternal.
![](https://main.qcloudimg.com/raw/1e0f8b71f125b857f6d421629e90e94f.png)

### Beberapa CVM
Ketika Anda memiliki banyak CVM untuk men-deploy layanan kompleks dan lalu lintas Internet tinggi, Anda dapat menggunakan [Cloud Load Balancer (CLB)](https://intl.cloud.tencent.com/document/product/214). CLB dapat secara otomatis mendistribusikan lalu lintas akses aplikasi di antara instans CVM di cloud, yang meningkatkan toleransi kesalahan untuk aplikasi.
![](https://main.qcloudimg.com/raw/d943efd83cc5d6df07e3e78954e681af.png)

## Pemulihan Bencana untuk Aplikasi
### Pemulihan Bencana Zona Ketersediaan Lintas
Subnet dikaitkan dengan zona ketersediaan. Anda dapat membuat subnet di zona ketersediaan yang berbeda dari satu VPC di suatu wilayah. Secara default, subnet yang berbeda dari VPC yang sama saling terhubung melalui jaringan pribadi. Anda dapat men-deploy sumber daya di subnet dari zona ketersediaan yang berbeda untuk mencapai pemulihan bencana zona lintas-ketersediaan.
![](https://main.qcloudimg.com/raw/32d62386d6369d631163749a0007396e.png)

### Pemulihan Bencana Lintas-Wilayah
Anda dapat men-deploy bisnis di seluruh wilayah (misalnya, solusi 2-region-3-DC) untuk mencapai pemulihan bencana lintas wilayah.
![](https://main.qcloudimg.com/raw/89fa56523b51e4ad09d1ae238c74b1cb.png)

## Men-deploy Cloud Hibrida
### Menghubungkan ke IDC Lokal
VPC menyediakan beberapa mode koneksi, seperti koneksi langsung dan koneksi VPN, yang dapat menghubungkan IDC lokal Anda dengan instans VPC di cloud untuk membuat arsitektur cloud hibrida dengan mudah. Menggunakan IDC lokal memastikan keamanan data inti Anda. Anda dapat memperluas sumber daya (seperti CVM dan TencentDB) di cloud berdasarkan volume bisnis Anda untuk mengurangi biaya Operasi TI.
![](https://main.qcloudimg.com/raw/40bd0f4a3920409a0e08c15568551a5c.png)

### Interkoneksi Multi-Titik Global
Saat Anda memiliki bisnis yang di-deploy di beberapa wilayah di seluruh dunia dan memerlukan interkoneksi lintas wilayah, Anda dapat menggunakan produk seperti [CCN](https://intl.cloud.tencent.com/document/product/1003) dan [Direct Connect](https://intl.cloud.tencent.com/document/product/216) untuk mengaktifkan interkoneksi multi-titik global melalui akses titik-tunggal.
![](https://main.qcloudimg.com/raw/cdcded11e541ee50f4b050d48c251b43.png)
