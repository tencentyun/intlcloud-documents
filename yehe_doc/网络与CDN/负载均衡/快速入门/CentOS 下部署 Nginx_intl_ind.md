Dokumen ini menjelaskan cara men-deploy proyek-proyek Nginx di CentOS dan cocok untuk setiap pengguna baru Tencent Cloud.
## Versi Perangkat Lunak
Versi alat perangkat lunak yang digunakan dalam dokumen ini adalah sebagai berikut, yang mungkin berbeda dengan versi perangkat lunak Anda selama operasi aktual.
- Sistem operasi:CentOS 7.5
- Nginx:Nginx 1.16.1

## Menginstal Nginx
1.Setelah menyelesaikan pembelian, klik **Masuk** (Masuk) di halaman detail CVM untuk masuk ke instance CVM Anda lalu masukkan nama pengguna dan kata sandi guna menyiapkan lingkungan Nginx.Untuk informasi selengkapnya tentang cara membuat instance CVM, lihat [Membuat Instance CVM](https://cloud.tencent.com/document/product/213/4855).
```
# Instal Nginx
yum -y instal nginx
# Lihat versi Nginx
nginx -v
# Lihat direktori penginstalan Nginx
rpm -ql nginx
# Mulai Nginx
mulai layanan nginx
```
2.Akses alamat IP publik dari instance CVM dan jika muncul halaman berikut, Nginx berhasil di-deploy:
![](https://main.qcloudimg.com/raw/8807f9fd819eb93d46c5646ba3572fac.png)
3.Direktori root default dari Nginx adalah `/usr/share/nginx/html`.Modifikasi halaman statis `index.html` dalam direktori `html` untuk menandai kekhususan halaman ini.Operasi yang relevan adalah sebagai berikut:
1.Jalankan perintah berikut untuk masuk ke halaman statis `index.html` di `html`:
```bash
vim /usr/share/nginx/html/index.html
```
2.Tekan "i" untuk masuk ke mode pengeditan dan tambahkan berikut ini ke dalam tag `<body></body>`:
```bash
# Anda sebaiknya langsung masuk ke bagian `<body>`
Halo nginx , Ini adalah rs-1!
URL adalah index.html
```
![](https://main.qcloudimg.com/raw/02e833dd08a6873d5d015f4531d24645.png)
3.Tekan "Esc" (Esc) dan masukkan `:wq` untuk menyimpan perubahan.
4.CLB (sebelumnya "Aplikasi CLB") dapat meneruskan permintaan menurut jalur server asli dan men-deploy halaman statis di jalur `/image`.Operasi yang relevan adalah sebagai berikut:
1.Jalankan perintah-perintah berikut untuk membuat dan masuk ke direktori `image`:
```bash
mkdir /usr/share/nginx/html/image
cd /usr/share/nginx/html/image
```
2.Jalankan perintah berikut untuk membuat halaman statis `index.html` di dalam direktori `image`:
```
vim index.html
```
3.Tekan “i” untuk masuk ke mode pengeditan dan tambahkan berikut ini ke halaman:
```bash
Halo nginx , Ini adalah rs-1!
URL adalah image/index.html
```
4.Tekan "Esc" (Esc) dan masukkan `:wq` untuk menyimpan perubahan.
>!Port default Nginx adalah `80`.Untuk mengubah port, silakan modifikasi file konfigurasi dan mulai ulang Nginx.

## Memverifikasi Layanan Nginx
Akses IP publik dan jalur instance CVM Anda.Jika halaman statis yang di-deploy ditampilkan, Nginx telah berhasil di-deploy.
- halaman `index.html` dari `rs-1`:
![](https://main.qcloudimg.com/raw/ede62fecd2106869d53bf142ad51903e.png)
- halaman `/image/index.html` dari `rs-1`:
![](https://main.qcloudimg.com/raw/f0f87422487177722291c2260cac9d35.png)
