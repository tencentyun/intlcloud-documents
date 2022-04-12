Virtual Private Cloud (VPC) adalah ruang jaringan virtual yang terisolasi secara logis di Tencent Cloud. Dengan VPC, Anda dapat mengonfigurasi ruang jaringan yang terisolasi secara logis untuk sumber daya Anda seperti [CVM](https://intl.cloud.tencent.com/document/product/213/495) dan [database cloud](https://intl.cloud.tencent.com/document/product/236). Produk ini memberikan keamanan sumber daya cloud yang lebih baik dan dapat memenuhi kebutuhan Anda dalam berbagai skenario.

Dokumen ini memperkenalkan komponen inti, mode koneksi, dan keamanan VPC.
## Komponen Inti
Instans VPC memiliki tiga komponen inti: Rentang IP VPC, subnet, dan tabel rute.
### Rentang IP VPC
Saat membuat VPC, Anda perlu menentukan [blok CIDR (classless inter-domain routing)(http://intl.cloud.tencent.com/document/product/215/4925) sebagai grup alamat IP VPC.

Tencent Cloud VPC mendukung blok CIDR di salah satu rentang IP pribadi berikut:
- **10.0**.0.0 - **10.255**.255.255 (**the mask range must be 16 to 28** (rentang mask harus 16 hingga 28))
- **172.16**.0.0 - **172.31**.255.255 (**the mask range must be 16 to 28** (rentang mask harus 16 hingga 28))
- **192.168**.0.0 - **192.168**.255.255 (**the mask range must be 16 to 28** (rentang mask harus 16 hingga 28))

### Subnet
VPC terdiri dari setidaknya satu subnet. Semua sumber daya cloud di VPC (seperti CVM dan database cloud) harus di-deploy di subnet, dan blok CIDR subnet harus berada di dalam blok CIDR VPC.

VPC disiapkan di tingkat [wilayah](https://intl.cloud.tencent.com/document/product/215/31786) (seperti Guangzhou), sedangkan subnet diatur di level [zona ketersediaan](https://intl.cloud.tencent.com/document/product/215/31786) (seperti Zona Guangzhou 1). Anda setidaknya dapat membagi VPC menjadi satu subnet. Subnet pada VPC yang sama dapat saling terhubung secara default, sementara subnet pada VPC yang berbeda diisolasi secara default.
![](https://main.qcloudimg.com/raw/9fe1af6b2ee439449a6fefa64663215c.png)

### Tabel rute
Saat Anda membuat VPC, sistem secara otomatis membuat tabel rute default untuk memastikan bahwa semua subnet di VPC saling terhubung. Jika kebijakan perutean di tabel rute default tidak dapat memenuhi kebutuhan bisnis Anda, Anda bisa membuat tabel rute kustom.

Untuk informasi selengkapnya tentang tabel rute, lihat [Ikhtisar Tabel Rute](https://intl.cloud.tencent.com/document/product/215/31810).

## Koneksi VPC
Tencent Cloud menyediakan berbagai solusi koneksi VPC untuk berbagai skenario.
- CVM dan database cloud di VPC dapat terhubung ke Internet melalui IP Elastis dan NAT Gateway.
- Koneksi Peering dan Jaringan Cloud Connect digunakan untuk mengaktifkan komunikasi antar VPC.
- VPC dan IDC lokal saling terhubung melalui Koneksi VPN, Direct Connect, dan Cloud Connect Network. 


## Keamanan VPC
- VPC adalah ruang jaringan virtual yang terisolasi secara logis di Tencent Cloud. VPC yang berbeda saling terisolasi untuk melindungi keamanan bisnis.
- Grup keamanan: grup keamanan adalah firewall virtual stateful yang mampu memfilter. Grup keamanan ini mengontrol lalu lintas masuk dan keluar pada tingkat instans dan merupakan sarana penting untuk isolasi keamanan jaringan.
- Access Control List (ACL) Jaringan: jaringan ACL adalah firewall virtual stateless untuk memfilter paket di tingkat subnet. Dapat digunakan untuk mengontrol aliran data masuk dan keluar subnet pada protokol dan granularitas port.
- Cloud Access Management (CAM): CAM membantu Anda mengelola akses ke sumber daya Tencent Cloud dengan aman. Misalnya, CAM menyediakan manajemen identitas dan manajemen kebijakan agar Anda dapat mengontrol siapa yang memiliki akses ke VPC Anda.

Untuk informasi selengkapnya tentang keamanan VPC, lihat [Manajemen Keamanan](https://intl.cloud.tencent.com/document/product/215/31848).
