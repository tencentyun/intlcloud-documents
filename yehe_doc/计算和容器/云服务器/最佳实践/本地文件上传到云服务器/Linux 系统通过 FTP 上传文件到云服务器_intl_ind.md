## Ikhtisar

Dokumen ini menjelaskan cara menggunakan layanan FTP untuk mengunggah file dari komputer Linux lokal ke CVM.

## Prasyarat

Anda telah membangun layanan FTP di CVM.
- Untuk menggunakan FTP untuk mengunggah file ke CVM Linux, lihat [Membangun Layanan FTP (Linux)](https://intl.cloud.tencent.com/document/product/213/10912)
- Untuk menggunakan FTP untuk mengunggah file ke CVM Windows, lihat [Membangun Layanan FTP (Windows)](https://intl.cloud.tencent.com/document/product/213/10414)

## Petunjuk

### Menghubungkan ke CVM
1. Jalankan perintah berikut untuk menginstal layanan FTP.
> Jika layanan FTP telah terinstal di komputer Linux lokal, lewati langkah ini.
>
```
yum -y install ftp
```
2. Jalankan perintah berikut untuk terhubung ke CVM dan masukkan nama pengguna dan kata sandi layanan FTP seperti yang diminta.
```
ftp <CVM IP address>
```
Jika antarmuka berikut muncul, koneksi telah berhasil dibuat.
![](https://main.qcloudimg.com/raw/9d93f45167addf70e023a21543af59f8.png)

### Mengunggah file
Jalankan perintah berikut untuk mengunggah file lokal ke CVM.
```
put local-file [remote-file]
```
Misalnya, untuk mengunggah file `/home/1.txt` lokal ke CVM, jalankan perintah berikut.
```
put /home/1.txt 1.txt
```

### Mengunduh file
Jalankan perintah berikut untuk mengunduh file dari CVM ke direktori lokal.
```
get [remote-file] [local-file]
```
Misalnya, untuk mengunduh file `A.txt` dari CVM ke direktori `/home` lokal, jalankan perintah berikut.
```
get A.txt /home/A.txt
```

