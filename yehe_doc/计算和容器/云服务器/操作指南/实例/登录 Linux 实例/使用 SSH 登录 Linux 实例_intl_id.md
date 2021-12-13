## Ikhtisar

Dokumen ini menjelaskan cara menggunakan kunci SSH untuk login ke instans Linux dari Linux, Mac OS, atau Windows lokal.

## Sistem yang Didukung

Linux, Mac OS, atau Windows (termasuk Windows 10 dan Windows Server 2019)

## Metode Autentikasi

**Password** (Kata Sandi) atau **Key** (Kunci)

## Prasyarat
- Anda harus sudah memiliki akun admin dan kata sandi (atau kunci) untuk login ke instans.
 - Jika Anda menggunakan kata sandi default sistem untuk masuk ke instans, buka [Pusat Pesan](https://console.cloud.tencent.com/message) untuk mendapatkan kata sandi terlebih dahulu.
 - Jika Anda [menggunakan kunci](#LoginWithKey) untuk login, Anda harus membuat kunci dan mengikatnya ke CVM ini. Untuk informasi selengkapnya, lihat [Mengelola Kunci SSH](https://intl.cloud.tencent.com/document/product/213/16691).
 - Jika lupa kata sandi Anda, harap [atur ulang kata sandi instans Anda](https://intl.cloud.tencent.com/document/product/213/16566).
- IP publik telah dibeli untuk instans CVM Anda, dan port 22 terbuka (ini terbuka secara default untuk CVM yang dibeli dengan konfigurasi cepat).

## Petunjuk

### Menggunakan kata sandi

1. Jalankan perintah berikut untuk terhubung ke CVM Linux.
>? Jika komputer lokal Anda menggunakan Mac OS, Anda harus membuka terminal yang disediakan oleh sistem, lalu menjalankan perintah berikut.
> Jika komputer lokal Anda menggunakan Linux, Anda dapat langsung menjalankan perintah berikut.
> Jika komputer lokal Anda menggunakan Windows 10 atau Windows Server 2019, Anda harus terlebih dahulu membuka command prompt CMD, lalu menjalankan perintah berikut.
>
```
ssh <username>@<hostname or IP address>
```
 - `username` mengacu pada nama akun default yang diperoleh sebagai prasyarat.
 - `hostname or IP address` mengacu pada alamat IP publik atau nama domain kustom dari instans Linux Anda.
2. Masukkan kata sandi yang sudah Anda peroleh, lalu tekan **Enter** (Enter) untuk login.

<span id="LoginWithKey"></span>
### Menggunakan kunci

1. Jalankan perintah berikut untuk mengatur file kunci pribadi yang hanya dapat dibaca oleh Anda.
 - Jika komputer lokal menggunakan Mac OS, Anda harus terlebih dahulu membuka terminal yang disediakan oleh sistem, lalu menjalankan perintah berikut.
 - Jika komputer lokal Anda menggunakan Linux, Anda dapat langsung menjalankan perintah berikut.
```
chmod 400 <The absolute path of the private key downloaded to be associated with the CVM>
```
 - Jika komputer lokal Anda menggunakan Windows 10, Anda harus terlebih dahulu membuka command prompt CMD, lalu menjalankan perintah berikut.
```
icacls <The absolute path of the private key downloaded to be associated with the CVM> /grant <Windows user account>:F
```
```
icacls <The absolute path of the private key downloaded to be associated with the CVM> /inheritancelevel:r
```
2. Jalankan perintah berikut untuk login jarak jauh.
```
ssh -i <The absolute path of the private key downloaded to be associated with the CVM> <username>@<hostname or IP address>
```
 - `username` mengacu pada nama akun default yang diperoleh sebagai prasyarat.
 - `hostname or IP address` mengacu pada alamat IP publik atau nama domain kustom dari instans Linux Anda.

 Misalnya, jalankan perintah `ssh -i "Mac/Downloads/shawn_qcloud_stable.pem" ubuntu@192.168.11.123` untuk login ke CVM Linux dari jarak jauh.

## Operasi Selanjutnya

Setelah login ke CVM, Anda dapat membangun situs web atau forum pribadi atau melakukan operasi lain. Untuk informasi selengkapnya, lihat:
- [Membuat Situs Web WordPress Secara Manual](https://intl.cloud.tencent.com/document/product/213/8044)


