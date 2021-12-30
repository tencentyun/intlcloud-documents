## Classiclink
### Skenario operasi
Secara default, VPC adalah ruang jaringan yang sepenuhnya terisolasi yang tidak dapat terhubung dengan instans VPC lain atau jaringan klasik melalui jaringan pribadi. [Peering connection](https://intl.cloud.tencent.com/document/product/553) memungkinkan instans VPC yang berbeda untuk berkomunikasi satu sama lain, dan Classiclink memungkinkan instans VPC untuk berkomunikasi dengan jaringan klasik.

CVM jaringan klasik dapat mengakses sumber informasi cloud di VPC, seperti CVM, database cloud, CLB jaringan pribadi, dan cache cloud. Namun, CVM di VPC hanya dapat mengakses CVM jaringan klasik yang saling terhubung dengannya tetapi tidak dapat mengakses sumber informasi komputasi lain dalam jaringan klasik.

>?Classiclink hanya tersedia untuk interkoneksi lintas dalam wilayah.

### Dampak konfigurasi dasar
- Alamat IP pribadi dari CVM jaringan klasik yang terhubung akan ditambahkan secara otomatis ke kebijakan lokal tabel rute VPC. Dengan cara ini, CVM di VPC dan CVM di jaringan klasik ini dapat berkomunikasi satu sama lain, tanpa perlu secara manual mengubah kebijakan tabel rute di VPC saat ini. 
- Setelah CVM jaringan klasik dihubungkan dengan VPC, firewall keamanan dan ACL jaringannya tetap efektif.
Anda dapat mengonfigurasi ACL jaringan untuk subnet VPC guna membatasi akses dari CVM jaringan klasik yang terhubung. Anda juga dapat mengonfigurasi aturan grup keamanan untuk CVM di jaringan klasik dan VPC untuk membatasi upaya akses jaringan di kedua arah.

### Batasan penggunaan
#### Pembatasan
- Hanya interkoneksi antara instans VPC dan jaringan klasik **in the same region** (di wilayah yang sama) yang didukung.
- Fitur Classiclink hanya tersedia untuk instans VPC dalam segmen jaringan `10.[0-47].0.0/16`. Rentang IP untuk instans VPC di segmen jaringan lain mungkin bertentangan dengan segmen IP jaringan klasik.
- CVM jaringan klasik dapat dihubungkan dengan satu VPC dalam satu waktu.
- VPC dapat dihubungkan maksimum dengan 100 CVM jaringan klasik.
- Sumber informasi VPC hanya dapat mengakses CVM di jaringan klasik daripada sumber informasi lain di jaringan klasik, seperti database cloud dan CLB.

#### Catatan
- Instans CLB dalam VPC tidak dapat diikat ke CVM jaringan klasik yang saling terhubung dengan VPC yang sama.
- Mengubah alamat IP pribadi CVM jaringan klasik akan membatalkan hubungan dengan VPC, yang berarti catatan hubungan asli akan menjadi tidak valid. Tambahkan rekaman lagi di Konsol VPC jika Anda ingin menghubungkannya lagi.
- Hubungan interkoneksi dengan VPC tidak akan terlepas dari tindakan yang dilakukan terkait CVM, seperti isolasi karena pembayaran yang terlambat, isolasi keamanan, migrasi cold, failover, modifikasi konfigurasi, dan peralihan sistem operasi.
- Hubungan interkoneksi dengan VPC akan otomatis terlepas jika CVM dikembalikan.
- Dalam situasi Classiclink, lalu lintas CVM hanya dapat dirutekan ke alamat IP pribadi di dalam VPC, tetapi tidak ke tujuan di luar VPC. Artinya, CVM jaringan klasik tidak dapat mengakses sumber informasi Internet atau VPC di luar VPC saat ini melalui perangkat jaringan seperti VPN gateway, direct connect gateway, public gateway, peering connection, dan NAT gateway. Demikian juga, rekan VPN gateway, direct connect gateway, dan peering connection tidak dapat mengakses CVM jaringan klasik.

### Langkah
Untuk informasi tentang cara mengoperasikan Classiclink, lihat [Mengelola Jaringan Klasik](https://intl.cloud.tencent.com/document/product/215/31807).

## Koneksi Terminal
Koneksi terminal adalah metode lain untuk menghubungkan instans VPC dan jaringan klasik. Ini menghubungkan instans dalam instans VPC dan non-CVM di jaringan klasik melalui jaringan pribadi. Produk jaringan klasik yang mendukung koneksi terminal termasuk CLB, MySQL, Memcached, Redis, dan MongoDB.

Koneksi terminal membuat pemetaan antara alamat IP instans jaringan klasik dan alamat IP VPC sehingga instans jaringan klasik dapat diakses dengan mengakses alamat IP VPC.

>?Koneksi terminal lintas wilayah atau antar-akun tidak didukung. Jika Anda perlu membuat koneksi terminal dalam situasi ini, kirimkan [tiket untuk mengajukan permohonan](https://console.cloud.tencent.com/workorder/category).


