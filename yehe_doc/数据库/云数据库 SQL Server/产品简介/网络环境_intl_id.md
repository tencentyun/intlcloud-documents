
TencentDB for SQL Server mendukung dua jenis lingkungan jaringan: [VPC dan jaringan klasik](https://intl.cloud.tencent.com/document/product/215/35505).

## Pembatasan Jaringan
Produk Tencent Cloud di wilayah yang berbeda tidak dapat saling berkomunikasi melalui jaringan pribadi.
- Instans CVM dalam VPC dapat berkomunikasi dengan instans TencentDB for SQL Server pada jaringan klasik di AZ yang berbeda di wilayah yang sama hanya setelah subnet dikonfigurasi dan IP VPC ditetapkan.
- Layanan Tencent Cloud di wilayah yang berbeda tidak dapat saling berkomunikasi melalui jaringan pribadi. Layanan Tencent Cloud dapat berkomunikasi di seluruh VPC hanya setelah [peering connection](https://intl.cloud.tencent.com/document/product/553/18827) dikonfigurasi.
Saat ini, TencentDB for SQL Server tidak mendukung IP publik. Jika Anda perlu menggunakan IP publik, Anda dapat menggunakan fitur pemetaan port SSH2 untuk menghubungkan, mengonfigurasi, dan mengelola instans dari internet. Untuk informasi selengkapnya, harap lihat [Menghubungkan ke Instans](https://intl.cloud.tencent.com/document/product/238/11627).
> Saat membeli TencentDB for SQL Server, sebaiknya pilih wilayah yang sama dengan instans CVM Anda guna mengurangi penundaan akses.

## Pengujian Konektivitas Jaringan
Alat pengujian konektivitas jaringan yang disediakan di [halaman pembelian TencentDB for SQL Server](https://buy.cloud.tencent.com/sqlserver#/) dapat digunakan untuk memeriksa apakah ada instans CVM di wilayah/AZ yang dipilih dan jenis jaringan yang dapat berkomunikasi dengan TencentDB for SQL Server melalui jaringan pribadi.
![](https://main.qcloudimg.com/raw/d1bca3859d60633ed0fb5669c88daf13.png)
Klik **View Details** (Lihat Detail) untuk melihat informasi instans CVM yang memenuhi syarat, termasuk ID/nama instans, AZ, konfigurasi (CPU, memori, disk, dan jaringan), dan alamat IP master. Anda juga dapat menggunakan fungsi pencarian untuk menentukan dengan cepat apakah instans CVM tertentu dapat berkomunikasi dengan TencentDB for SQL Server melalui jaringan pribadi.
![](https://main.qcloudimg.com/raw/8c76d06d19734b7fe8f85ba2f14b64a1.png)
