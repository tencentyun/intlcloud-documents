## Latar belakang
CentOS 6 mencapai end-of-life (EOL) pada 30 November 2020, dan tidak lagi dikelola oleh komunitas Linux. Dengan demikian, sumber CentOS 6 tidak tersedia di `http://mirror.centos.org/centos-6/` dan situs citra pihak ketiga. Situs Tencent Cloud, `http://mirrors.cloud.tencent.com/` dan `http://mirrors.tencentyun.com/`, tidak dapat memperoleh sumber CentOS 6. Jika Anda terus menggunakan sumber CentOS 6 default yang dikonfigurasi di Tencent Cloud, kesalahan mungkin terjadi.



>? Sebaiknya tingkatkan sistem operasi Anda ke CentOS 7 atau versi yang lebih baru. Jika Anda masih perlu menggunakan dependensi CentOS 6, alihkan sumber CentOS 6 seperti yang diinstruksikan di bawah ini.



## Petunjuk
1. Login ke instans Linux menggunakan Web Shell (Lihat [dokumentasi](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang lebih mudah bagi Anda:
	- [Login ke Instans Linux melalui Fitur Masuk Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32502)
	- [Login ke Instans Linux melalui Kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501)
2. Jalankan perintah berikut untuk memeriksa versi CentOS dari sistem operasi saat ini.
```
cat /etc/centos-release
```
Seperti yang ditunjukkan pada gambar berikut, versi sistem operasinya adalah CentOS 6.9.
![](https://main.qcloudimg.com/raw/de65529a43dc5bfee695c08d5f7bff80.png)
3. Jalankan perintah berikut untuk mengedit file `CentOS-Base.repo`.
```
vim /etc/yum.repos.d/CentOS-Base.repo 
```
4. Tekan **i** (i) untuk masuk ke mode edit dan ubah `baseurl` sesuai dengan versi CentOS dan lingkungan jaringan.
>?
>Tentukan sumber yang diperlukan untuk instans Anda seperti yang diinstruksikan di [Akses Jaringan Pribadi](https://intl.cloud.tencent.com/document/product/213/5225) dan [Akses Internet](https://intl.cloud.tencent.com/document/product/213/5224) 
>
>- Sumber untuk akses jaringan pribadi: `http://mirrors.tencentyun.com/centos-vault/6.x/`
>- Sumber untuk akses jaringan publik: `https://mirrors.cloud.tencent.com/centos-vault/6.x/`

Dokumen ini menggunakan instans berbasis CentOS 6.9 yang memerlukan akses jaringan pribadi sebagai contoh. File <code>CentOS-Base.repo</code> yang dimodifikasi adalah sebagai berikut:
<img src="https://main.qcloudimg.com/raw/1d2485a9be0df6d5f7c46151fc50d73b.png"/>
5. Tekan **ESC** (ESC), masukkan **:wq** (:wq), dan tekan **Enter** (Enter) untuk menyimpan modifikasi.
6. Jalankan perintah berikut untuk memodifikasi file `CentOS-Epel.repo`.
```
vim /etc/yum.repos.d/CentOS-Epel.repo 
```
7. Tekan **i** (i) untuk masuk ke mode edit dan memodifikasi `baseurl` berdasarkan lingkungan jaringan.
Dalam contoh ini, ubah `baseurl=http://mirrors.tencentyun.com/epel/$releasever/$basearch/` menjadi `baseurl=http://mirrors.tencentyun.com/epel-archive/6/$basearch/`. Hasilnya harus sebagai berikut:
![](https://main.qcloudimg.com/raw/9c4b3eaf65d005b3d6819f013037443d.png)
8. Tekan **ESC** (ESC), masukkan **:wq** (:wq), dan tekan **Enter** (Enter) untuk menyimpan modifikasi.
9. Sekarang Anda dapat menggunakan perintah `yum install` untuk menginstal perangkat lunak yang diperlukan.
