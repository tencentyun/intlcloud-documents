## Pengantar
rdesktop adalah klien RDP sumber terbuka. Artikel ini menjelaskan cara menggunakannya untuk menghubungkan ke CVM yang menjalankan Windows Server 2012 R2 untuk mengunggah file.

## Prasyarat
Membeli instans CVM Windows.

## Petunjuk
### Mendapatkan IP Publik CVM
Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index) dan cari alamat IP publik CVM Windows Anda, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)



###. Menginstal rddesktop.
1. Buka jendela terminal dan jalankan perintah berikut untuk mengunduh rdesktop 1.8.3:
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
Jika Anda ingin menginstal versi baru, buka [beranda desktop di GitHub](https://github.com/rdesktop/rdesktop/releases) untuk menemukannya. Kemudian, ganti jalur dalam perintah dengan yang baru.
2. Jalankan perintah berikut untuk mendekompresi paket instal dan navigasikan ke direktorinya.
```
tar xvzf rdesktop-1.8.3.tar.gz
```
```
cd rdesktop-1.8.3
```
3. Jalankan perintah berikut untuk mengompilasi dan menginstal rdesktop.
```
./configure 
```
```
make
```
```
make install
```
4. Setelah penginstalan selesai, jalankan perintah berikut untuk memeriksa apakah rdesktop berhasil diinstal:
```
rdesktop
```

### Mengunggah File
1. Jalankan perintah berikut untuk menentukan folder bersama:
```
rdesktop cvm_ip  -u cvm_username -p cvm_password -r disk:shared_folder_path=local_folder_path
```
>
>- Nama pengguna default untuk CVM adalah `Administrator`.
>- Jika Anda memilih untuk masuk dengan kata sandi acak, harap periksa di [Pusat Pesan](https://console.cloud.tencent.com/message).
>- Jika lupa kata sandi Anda, harap [atur ulang kata sandi instans](http://intl.cloud.tencent.com/document/product/213/16566).
>
Misalnya, jalankan perintah berikut untuk membagikan folder `/home` di mesin Linux lokal Anda ke CVM yang ditentukan, dan ganti namanya menjadi `share`.
```
rdesktop 118.xx.248.xxx  -u Administrator -p 12345678 -r disk:share=/home
```
Jika operasi berhasil, Desktop Windows akan muncul.
Klik <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px"> lalu **My Computer** (Komputer Saya) untuk melihat folder bersama.
2. Klik dua kali folder bersama untuk membukanya. Salin file di folder bersama ke direktori pada disk Windows CVM untuk mengunggahnya.
Misalnya, salin **a.txt** (a.txt) di `share` ke drive C CVM Windows.

### Mengunduh file
Untuk mengunduh file dari CVM Windows ke komputer Linux Anda, salin file yang diinginkan dari CVM ke folder bersama.
