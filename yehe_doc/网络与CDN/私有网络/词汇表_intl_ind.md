## C

### CIDR

Lihat [CIDR](https://intl.cloud.tencent.com/document/product/215/4925).

## E

### EIP

Lihat [IP Elastis](https://intl.cloud.tencent.com/document/product/215/4925).

## G

### IP Publik

IP publik dapat diakses melalui Internet dan digunakan untuk komunikasi antara instans dan Internet atau sumber daya Tencent Cloud lainnya (seperti sumber daya database) dengan endpoint publik.

### Gateway publik

Gateway publik adalah CVM yang dapat meneruskan lalu lintas antara Internet dan VPC. CVM tanpa IP publik dapat mengakses Internet melalui gateway publik.

## J

### Jaringan klasik

Jaringan dasar adalah kumpulan sumber daya jaringan publik untuk semua pengguna Tencent Cloud. Tencent Cloud menetapkan IP pribadi ke CVM di jaringan klasik. Ini mengutamakan konfigurasi sederhana dan kemudahan penggunaan, sehingga cocok untuk pengguna yang membutuhkan kegunaan tinggi dan mulai cepat dengan CVM. Sebaliknya, VPC cocok untuk pengguna dengan kemampuan dan kebutuhan pengelolaan jaringan.
Untuk informasi selengkapnya, lihat [Berkomunikasi dengan Jaringan Klasik](https://intl.cloud.tencent.com/document/product/215/35505).

## K

## Zona ketersediaan

Zona ketersediaan adalah IDC fisik Tencent Cloud dengan catu daya dan jaringan independen di satu wilayah. Zona ini dapat memastikan stabilitas bisnis, karena kegagalan di satu AZ diisolasi tanpa memengaruhi AZ lain di wilayah yang sama.

## N

### IP Pribadi

IP pribadi adalah alamat IP yang ditetapkan ke instans di Tencent Cloud VPC atau jaringan klasik dan tidak dapat diakses melalui Internet. Ini dapat digunakan untuk komunikasi antar instans dalam VPC atau jaringan klasik.

## S

### VPC

VPC membangun ruang jaringan terisolasi di Tencent Cloud, yang mirip dengan jaringan tradisional yang dijalankan di IDC Anda. VPC meng-hosting sumber daya Tencent Cloud Anda, termasuk [Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213), [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214), [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236), dll. Daripada mengkhawatirkan pembelian dan OPS perangkat jaringan, Anda dapat fokus menyesuaikan rentang IP, alamat IP, kebijakan perutean, dll. Anda dapat mengakses Internet dengan mudah melalui [EIP](https://intl.cloud.tencent.com/document/product/213/16586), [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015) dan [Gateway Publik](https://intl.cloud.tencent.com/document/product/213/34835), dan menghubungkan VPC dengan IDC Anda melalui [VPN](https://intl.cloud.tencent.com/document/product/1037)/[Direct Connect](https://intl.cloud.tencent.com/document/product/216). Tencent Cloud VPC [Peering Connection](https://intl.cloud.tencent.com/document/product/553) memungkinkan Anda menerapkan server terpadu untuk akses global dan pemulihan bencana 2-region-3-DC. Selain itu, grup keamanan dan [ACL jaringan](https://intl.cloud.tencent.com/document/product/215/31850) dari Tencent Cloud VPC dapat sepenuhnya memenuhi kebutuhan Anda akan keamanan jaringan.

## T

### EIP

IP elastis adalah alamat IP publik yang dapat diterapkan secara independen. EIP ini mendukung pengikatan dan pelepasan dinamis. Anda dapat mengikatnya atau melepaskannya dari CVM (atau instans NAT Gateway) pada akun Anda. Kegunaan utamanya adalah:

1. Untuk mempertahankan IP. Pencatatan nama domain ICP diperlukan untuk IP dan DNS daratan Tiongkok.
2. Untuk menutupi kegagalan instans. Misalnya, nama DNS dipetakan ke alamat IP melalui pemetaan DNS dinamis. Mungkin diperlukan waktu hingga 24 jam untuk menyebarkan pemetaan ini ke seluruh Internet, sementara IP elastis memungkinkan pemetaan ulang IP dengan cepat dari satu CVM ke CVM lainnya. Jika satu CVM gagal, Anda dapat meluncurkan dan memetakan ulang instans lain untuk merespons kegagalan instans dengan cepat.

## V

### VPC

Lihat [VPC](https://intl.cloud.tencent.com/document/product/215/4925).

## W

### CIDR

Perutean Antar-Domain Tanpa Kelas adalah blok alamat ruang jaringan independen yang ditentukan pengguna. Ini menggabungkan IP dan masking untuk mencapai pembagian jaringan. Dalam contoh `10.1.0.0/16`, `10.1.0.0` adalah alamat IP dari blok jaringan, dan `16` adalah mask dari blok jaringan. Anda dapat mengubah ukuran blok jaringan dengan menyesuaikan ukuran mask. Jumlah IP dalam blok jaringan sama dengan 2 ^ (32-mask), dan blok jaringan `10.1.0.0/16` memiliki maksimal 65.536 alamat IP.