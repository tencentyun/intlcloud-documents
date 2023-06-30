Ubuntu secara resmi berhenti menyediakan pemeliharaan untuk Ubuntu 10.04 LTS, oleh karena itu Tencent Cloud juga telah menonaktifkan citra publik Ubuntu 10.04.

Pohon direktori untuk Ubuntu 10.04 LTS telah dihapus dari repositori sumber resmi terbaru. Untuk memastikan konsistensi dengan repositori sumber resmi, repositori perangkat lunak Tencent Cloud tidak lagi mendukung Ubuntu 10.04 LTS dalam pohon direktori sumber resmi. Dengan demikian, sebaiknya mengupgrade citra ke versi yang lebih baru.

Untuk pengguna lama yang berharap untuk terus menggunakan sumber perangkat lunak Ubuntu 10.04, kami memberikan dukungan dengan cara berikut:

## Metode 1: Memperbarui File Konfigurasi Secara Manual
Untuk meningkatkan pengalaman pengguna, repositori perangkat lunak Tencent Cloud menarik sumber arsip resmi `http://old-releases.ubuntu.com/ubuntu/` Ubuntu 10.04 LTS (http://old-releases.ubuntu.com/ubuntu/) untuk pengguna. Pengguna dapat menggunakan repositori seperti biasa dengan memodifikasi file konfigurasi secara manual:

Buka file konfigurasi sumber apt `vi/etc/apt/sources.list` dan ubah potongan kode berikut:

```
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid main limited universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-updates main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-security main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-backports main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-updates main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-security main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-backports main restricted universe multiverse
```

## Metode 2: Menjalankan Skrip Otomatis
Gunakan skrip [old-archive.run](http://ubuntu10-10016717.cos.myqcloud.com/old-archive.run) yang disediakan oleh Tencent Cloud untuk konfigurasi. Untuk melakukan ini, unduh file ke CVM dengan Ubuntu 10.04 dan jalankan perintah berikut:

```
chmod +x old-archive.run
./old-archive.run
```