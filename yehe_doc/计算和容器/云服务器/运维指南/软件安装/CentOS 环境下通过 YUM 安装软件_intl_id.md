## Ikhtisar
YUM (Yellowdog Updater, Modified) memungkinkan Anda mengunduh dan menginstal perangkat lunak dengan mudah, dan menyederhanakan penginstalan Anda pada instans CVM, sehingga menghemat waktu dan tenaga Anda. Dengan demikian, Anda hanya perlu menjalankan perintah `yum` untuk menginstal perangkat lunak di lingkungan CentOS. Tencent Cloud menyediakan repositori YUM sehingga Anda dapat langsung menginstal paket perangkat lunak tanpa menambahkan sumber.

## Petunjuk

### Menginstal perangkat lunak
Login ke instans CVM Anda dengan akun root dan jalankan perintah berikut untuk menginstal perangkat lunak sesuai dengan sistem operasi CVM Anda.

#### CentOS 8 atau versi yang lebih baru
1. Jalankan perintah berikut untuk menginstal perangkat lunak.
```
dnf install [nama perangkat lunak]
```
Sistem akan mencari paket perangkat lunak dan dependensi yang relevan secara otomatis, dan meminta konfirmasi Anda.
Misalnya, setelah Anda menjalankan perintah `dnf install php` untuk menginstal PHP, perintah berikut akan muncul:
![](https://main.qcloudimg.com/raw/ab6cdf18a685debff13c8f978b38d43f.png)
2. Konfirmasikan bahwa paket perangkat lunak sudah benar. Masukkan `y` dan tekan **Enter** (Enter) untuk memulai penginstalan.
Perintah `Complete` menunjukkan penginstalan telah selesai.

#### CentOS 7 atau versi sebelumnya
1. Jalankan perintah berikut untuk menginstal perangkat lunak.
>! Mulai dari CentOS 7, MariaDB telah menjadi database default di repositori YUM. Jika Anda menggunakan CentOS 7 atau versi yang lebih baru, MySQL yang diinstal menggunakan `yum` tidak akan dapat digunakan. Anda dapat menggunakan MariaDB yang sepenuhnya kompatibel, atau [klik di sini](https://www.linode.com/docs/databases/mysql/how-to-install-mysql-on-centos-7) untuk mempelajari tentang cara menginstal versi MySQL yang lebih lama.
>
```
yum install [nama perangkat lunak]
``` 
Sistem akan mencari paket perangkat lunak dan dependensi yang relevan secara otomatis, dan meminta konfirmasi Anda.
Misalnya, setelah Anda menjalankan perintah `yum install PHP` untuk menginstal PHP, perintah berikut akan muncul:
![](https://main.qcloudimg.com/raw/18c4a59a3e0e92b0dcafff662d1e3673.png)
2. Konfirmasikan bahwa paket perangkat lunak sudah benar. Masukkan `y` dan tekan **Enter** (Enter) untuk memulai penginstalan.
Perintah `Complete` menunjukkan penginstalan telah selesai.

### Melihat informasi perangkat lunak yang diinstal

Setelah penginstalan perangkat lunak selesai, Anda dapat menjalankan perintah yang berbeda untuk melihat informasi terkait.
- Lihat direktori penginstalan paket perangkat lunak
```
rpm -ql [nama perangkat lunak]
```
Misalnya, jalankan `rpm -ql php` untuk melihat direktori penginstalan PHP, seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/fda98060c9f6ba359d7e705de8d336bb.png)
- Lihat versi paket perangkat lunak
```
rpm -q
```
Misalnya, jalankan `rpm -q php` untuk melihat versi PHP, seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/35e1ecee46bc55a5d2510dce59360ecc.png)

