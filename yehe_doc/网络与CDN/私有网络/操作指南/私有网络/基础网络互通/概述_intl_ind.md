Fitur Classiclink memungkinkan CVM berbasis VPC berkomunikasi dengan CVM berbasis jaringan klasik.  Misalnya,
+ CVM berbasis jaringan klasik dapat berkomunikasi dengan sumber daya VPC seperti CVM, TencentDB, CLB jaringan pribadi, Redis/CMEM, dll.
+ Sumber daya VPC hanya dapat mengakses CVM berbasis jaringan klasik, tetapi tidak dapat mengakses sumber daya lain di jaringan klasik, seperti TencentDB dan CLB 
![](https://main.qcloudimg.com/raw/5c4c66605c6ecd04591dfff5236231df.png) 

## Batas Penggunaan
- VPC hanya dapat terhubung dengan jaringan klasik **in the same region** (di wilayah yang sama).
+ Rentang IP VPC harus berada dalam `10.0.0.0/16-10.47.0.0/16` (termasuk subset), jika tidak, mungkin ada konflik IP, yang dapat menyebabkan kegagalan saat menghubungkan dan berkomunikasi dengan CVM berbasis jaringan klasik.
+ CVM berbasis jaringan klasik hanya dapat dihubungkan dengan satu VPC dalam satu waktu.
+ Satu VPC mendukung hubungan dengan hingga 100 CVM berbasis jaringan klasik.
+ Setelah CVM jaringan klasik dihubungkan dengan VPC, CVM berbasis jaringan klasik hanya dapat berkomunikasi dengan sumber daya di blok CIDR primer daripada blok CIDR sekunder pada VPC.
+ Instans CLB dalam VPC tidak dapat diikat ke CVM berbasis jaringan klasik yang saling terhubung dengan VPC yang sama.
+ Dalam situasi Classiclink, lalu lintas CVM hanya dapat dirutekan ke alamat IP pribadi di dalam VPC daripada tujuan di luar VPC.
>? CVM berbasis jaringan klasik tidak dapat mengakses sumber daya jaringan publik atau pribadi di luar VPC saat ini melalui perangkat jaringan seperti VPN gateway, gateway direct connect, public gateway, peering connection, dan NAT Gateway.  Demikian juga, peer dari VPN gateway, direct connect gateway, dan peering connection tidak dapat mengakses CVM berbasis jaringan klasik.



## Catatan
- Mengubah IP pribadi CVM berbasis jaringan klasik akan membatalkan hubungannya dengan VPC, dan menyebabkan konfigurasi menjadi tidak valid.  Untuk menghubungkannya, Anda perlu menambahkan Classiclink lagi di konsol VPC.
- Classiclink tidak akan terpengaruh oleh tindakan yang diambil terkait CVM seperti isolasi karena pembayaran yang jatuh tempo, isolasi keamanan, migrasi cold, failover, modifikasi konfigurasi, dan peralihan sistem operasi.
- CVM akan otomatis diputuskan hubungannya dari VPC jika CVM dikembalikan.


## Referensi
Untuk informasi selengkapnya tentang cara mengoperasikan Classiclink, lihat [Mengelola Classiclink](https://intl.cloud.tencent.com/document/product/215/41419).

