Dokumen ini menjelaskan cara mengaktifkan/menonaktifkan alamat jaringan publik di konsol TencentDB for Redis. Anda dapat menggunakan nama domain dan port yang ditetapkan sistem untuk mengakses instans melalui jaringan publik, memfasilitasi pengujian harian, pengelolaan, penggunaan, dan pengembangan database.

>?
>- Waktu henti layanan instans yang disebabkan oleh kesalahan jaringan publik tidak akan dihitung ke dalam "Waktu Henti Layanan Instans Tunggal" dalam Perjanjian Tingkat Layanan (SLA) Redis.
>- Akses jaringan publik akan merusak keamanan instans, dan ketersediaan layanan tidak dijamin oleh SLA. Oleh karena itu, sebaiknya akses Redis melalui jaringan publik hanya saat menguji, mengelola, atau membantu mengelola database. Di lingkungan produksi, akses Redis melalui jaringan pribadi.

## Prasyarat
- Hanya instans di VPC yang dapat mengaktifkan alamat jaringan publik.
- Untuk saat ini, hanya instans di wilayah Chengdu, Beijing, Shanghai, dan Guangzhou yang dapat mengaktifkan alamat jaringan publik.

## Mengaktifkan Alamat Jaringan Publik
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis) dan klik ID instans di daftar instans, dan masuk ke halaman detail instans.
2. Klik **Enable** (Aktifkan) di samping **Public Network Address** (Alamat Jaringan Publik) di blok **Network Info** (Info Jaringan).
![](https://qcloudimg.tencent-cloud.cn/raw/45ba379ace466f7256e489387661bacb.png)
3. Di kotak dialog pop-up, konfirmasikan bahwa semuanya sudah benar dan klik **OK** (OKE).
![](https://qcloudimg.tencent-cloud.cn/raw/7644853f0a294487b0fd44e0d9657479.png)
4. Kembali ke halaman detail instans, tempat Anda melihat instans dalam status **Mengaktifkan jaringan publik**. Jika status tetap sama untuk waktu yang lama, harap muat ulang halaman.
5. Jika **Alamat Jaringan Publik** menunjukkan alamat yang terdiri dari nama domain dan port, alamat tersebut berhasil diaktifkan. Sekarang Anda dapat menggunakannya untuk mengakses Redis melalui jaringan publik.
>?Setelah akses jaringan publik ke TencentDB for Redis diaktifkan, selanjutnya akan dikontrol oleh kebijakan grup keamanan. Untuk informasi selengkapnya, silakan lihat [Mengonfigurasi Grup Keamanan](https://intl.cloud.tencent.com/document/product/239/31945).
>
![](https://qcloudimg.tencent-cloud.cn/raw/14843fcd53a18df45726b3456b44f465.png)

## Menonaktifkan Alamat Jaringan Publik
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis) dan klik ID instans di daftar instans, dan masuk ke halaman detail instans.
2. Klik **Disable** (Nonaktifkan) di samping **Public Network Address** (Alamat Jaringan Publik) di blok **Network Info** (Info Jaringan).
![](https://qcloudimg.tencent-cloud.cn/raw/4bcd7d4d286ccce548c393433bece283.png)
3. Di kotak dialog pop-up, konfirmasikan bahwa semuanya sudah benar dan klik **OK** (OKE).
4. Kembali ke halaman detail instans untuk melihat instans dalam status **Menonaktifkan jaringan publik** dan **Alamat Jaringan Publik** tidak menampilkan apa pun.

