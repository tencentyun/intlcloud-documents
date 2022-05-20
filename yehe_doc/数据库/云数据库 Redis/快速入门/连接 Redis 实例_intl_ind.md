Anda dapat terhubung ke instans TencentDB for Redis menggunakan alat klien, pusat manajemen database (DMC), dan SDK yang mendukung berbagai bahasa pemrograman.

## Persiapan
- Siapkan instans TencentDB for Redis. Untuk informasi selengkapnya, lihat [Membuat Instans TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/37712).
- Siapkan akun database. Untuk informasi selengkapnya, lihat [Mengelola Akun](https://intl.cloud.tencent.com/document/product/239/34590). Anda juga dapat menggunakan akun default secara langsung.
- Anda telah mengonfigurasi aturan grup keamanan untuk instans CVM dan instans TencentDB for Redis untuk mengizinkan IP atau rentang IP tertentu mengakses instans TencentDB for Redis. Untuk informasi selengkapnya, lihat [Mengonfigurasi Grup Keamanan](https://intl.cloud.tencent.com/document/product/239/31945)

## Menghubungkan Menggunakan Alat Klien
Instans CVM dapat digunakan untuk mengakses alamat pribadi yang ditetapkan secara otomatis ke instans TencentDB. Metode koneksi ini menggunakan jaringan pribadi Tencent Cloud berkecepatan tinggi dan fitur penundaan yang rendah. Kedua instans harus berada di bawah akun yang sama dan di [VPC](https://intl.cloud.tencent.com/document/product/215/535) yang sama di wilayah yang sama, atau keduanya di jaringan klasik.
>?
>- Instans CVM dan TencentDB di VPC yang berbeda (dalam akun yang sama atau berbeda di wilayah yang sama atau berbeda) dapat saling terhubung melalui jaringan pribadi melalui [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
>- Instans CVM dan TencentDB di VPC yang berbeda dapat dihubungkan melalui alamat jaringan publik seperti yang diinstruksikan di [Mengonfigurasi Alamat Jaringan Publik](https://intl.cloud.tencent.com/document/product/239/43452).

### Langkah 1. Mempersiapkan lingkungan
1. Login ke instans CVM Linux. Untuk informasi selengkapnya, lihat [Menyesuaikan Konfigurasi CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517).
2. Mengambil instans CVM pada CentOS sebagai contoh, instal klien Redis dengan menjalankan perintah berikut:
```
yum install redis -y
```
Jika `Complete!` ditampilkan, artinya klien berhasil diinstal.

### Langkah 2. Hubungkan ke instans
#### Instans bebas kata sandi
Jika instans Anda bebas kata sandi, perintah koneksi harus sebagai berikut:
```
redis-cli -h IP address -p port
```

#### Instans yang dilindungi kata sandi
Jika instans Anda dilindungi kata sandi, didukung perintah koneksi sumber terbuka berikut:
```
redis-cli -h IP address -p port -a password
```

Misalnya, jika kata sandi yang Anda tetapkan adalah `abcd1234`, perintah koneksi harus sebagai berikut:
```
redis-cli -h IP address -p port -a abcd1234
```
>?Untuk mengakses instans yang dibeli sebelum Januari 2018, Anda perlu mengganti "password" dengan "instance ID:password".
>Contoh: `redis-cli -h IP address -p port -a crs-bkuza6i3:abcd1234`


#### Instans yang mendukung akun
Jika Anda menggunakan [akun kustom](https://intl.cloud.tencent.com/document/product/239/34590) untuk koneksi, parameter kata sandi `account name@password` akan diautentikasi untuk mengakses TencentDB for Redis:
```
redis-cli -h IP address -p port -a account name@password
```

## Menghubungkan Menggunakan DMC
Anda dapat menggunakan Tencent Cloud [DMC](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login) untuk mengakses instans TencentDB for Redis, memanipulasi database dan tabel, mengelola sesi instans, memantau instans secara real-time, melihat lock wait InnoDB, dan menggunakan jendela SQL.

## Menghubungkan Menggunakan SDK
Untuk informasi selengkapnya, lihat [Koneksi Cache](https://intl.cloud.tencent.com/document/product/239/7042).

