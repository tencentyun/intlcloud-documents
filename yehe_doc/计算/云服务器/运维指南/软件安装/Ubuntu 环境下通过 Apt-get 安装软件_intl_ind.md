## Pengantar
Advanced Package Tool (APT) adalah antarmuka pengguna perangkat lunak gratis yang berfungsi dengan pustaka inti untuk menangani penginstalan dan penghapusan perangkat lunak pada berbagai distribusi Linux. APT menawarkan antarmuka terpusat untuk pengelolaan perangkat lunak dan pengalaman yang lebih baik daripada harus mengunduh dan menginstal perangkat lunak satu per satu. Tencent Cloud menghosting sumber APT sehingga Anda dapat menginstal perangkat lunak tanpa menambahkan sumber.

## Prasyarat
Login ke instans CVM Linux yang menjalankan Ubuntu.

## Petunjuk
> Dalam hal berikut, Nginx digunakan sebagai contoh.
>

### Mencantumkan perangkat lunak yang tersedia
Jalankan perintah berikut untuk membuat daftar perangkat lunak yang tersedia:
```
sudo apt-cache search all
```

### Menginstal perangkat lunak
Jalankan perintah berikut untuk menginstal Nginx: 
```
sudo apt-get install nginx
```
Pastikan ini adalah perangkat lunak yang ingin Anda instal dan masukkan `Y` untuk menyetujui penginstalan. Tunggu hingga penginstalan perangkat lunak selesai, seperti ditunjukkan pada gambar di bawah ini:
![](https://mc.qcloudimg.com/static/img/d03f55bba1690ff30532b73148ccc1e9/45.png)

### Mengkueri perangkat lunak yang diinstal
Anda dapat menjalankan perintah yang berbeda untuk mengkueri perangkat lunak yang diinstal.
- Jalankan perintah berikut untuk mengkueri direktori paket perangkat lunak dan semua file dalam paket perangkat lunak.
``` 
sudo dpkg -L software_name 
```
- Jalankan perintah berikut untuk mengkueri informasi versi paket perangkat lunak.
``` 
sudo dpkg -l software_name 
```

Lihat informasi tentang Nginx yang diinstal, seperti yang ditunjukkan pada gambar di bawah ini:
![](https://mc.qcloudimg.com/static/img/8bbc99d7a31e8463da36f3dc2221c028/46.png)
