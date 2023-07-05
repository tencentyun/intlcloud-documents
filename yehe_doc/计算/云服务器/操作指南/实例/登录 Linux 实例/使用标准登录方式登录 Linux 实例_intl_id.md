### Skenario

WebShell adalah metode login yang direkomendasikan oleh Tencent Cloud. Meskipun OS lokal Anda adalah Windows, Linux, atau Mac OS, selama Anda telah membeli IP publik untuk instans, Anda dapat login melalui Web Shell. Dokumen ini menjelaskan cara login ke instans Linux melalui Web Shell.
Manfaat Web Shell:
- Mendukung operasi salin dan tempel dengan tombol pintas.
- Mendukung pengguliran dengan roda mouse.
- Mendukung masukan bahasa Mandarin.
- Fitur keamanan yang tinggi (kata sandi atau kunci diperlukan untuk setiap login).

## OS Lokal yang Berlaku

Windows, Linux, atau MacOS.

## Metode Autentikasi

**Password** (Kata Sandi) atau **Key** (Kunci)

## Prasyarat

- Anda harus sudah memiliki akun admin dan kata sandi (atau kunci) untuk instans yang digunakan untuk login.
 - Jika Anda memilih **Random Password** (Kata Sandi Acak) saat membuat instans, buka [Pesan Internal](https://console.cloud.tencent.com/message) untuk memeriksa kata sandi.
 - Jika lupa kata sandi Anda, [atur ulang kata sandi instans](https://intl.cloud.tencent.com/document/product/213/16566).
- Pastikan instans CVM memiliki IP publik, dan port 22 terbuka (jika CVM dibeli dengan “Konfigurasi Cepat”, port ini terbuka secara default.)

### Petunjuk

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman manajemen instans, pilih CVM Linux tempat Anda ingin login, lalu klik **Log In** (Login), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/cc5786b9f8b57ff4057b666503729bc0.png)
3. Di jendela pop-up **Log into Linux Instance** (Login ke Instans Linux), pilih **Standard login method** (Metode login standar), lalu klik **Log In Now** (Login Sekarang), seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/87ba7e511f8d0ffe48f220cecaa7b057.png)
4. Di jendela **Log into Instance** (Login ke Instans), pilih **Password Login** (Login Kata Sandi) atau **Key Login** (Login Kunci), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/9c321ad519c8f993c1f768e56fca0ab1.png)
Jika login berhasil, “Socket connection established” (Koneksi soket dibuat) akan muncul seperti yang ditampilkan di bawah ini:
![](https://main.qcloudimg.com/raw/6bcd152ff947909f52da67430aa7eda6.png)

## Operasi Selanjutnya

Setelah login ke CVM, Anda dapat membangun situs web atau forum pribadi di Tencent Cloud CVM atau melakukan operasi lain. Untuk informasi selengkapnya, lihat dokumen berikut:
- [Membuat situs WordPress pribadi](https://intl.cloud.tencent.com/document/product/213/8044)

