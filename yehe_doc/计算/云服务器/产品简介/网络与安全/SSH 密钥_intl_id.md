Untuk memastikan keamanan dan keandalan instans, Tencent Cloud memberi pengguna dua metode login terenkripsi. Pengguna bisa masuk melalui [kata sandi masuk](/doc/product/213/6093) atau pasangan kunci SSH. Dokumen ini menjelaskan cara login dengan pasangan kunci SSH.
Anda bisa memilih pasangan kunci SSH sebagai metode login CVM terenkripsi saat [Menyesuaikan Konfigurasi CVM Linux](/doc/product/213/10517#.E8.AE.BE.E7.BD.AE.E4.BF.A1.E6. 81.AF).

## Ikhtisar Kunci SSH
Kami menyarankan **menggunakan pasangan kunci SSH** untuk login ke instans Linux. Pasangan kunci berisi kunci publik dan kunci pribadi. Pasangan kunci ini dibuat dengan metode enkripsi RSA 2048-bit.
- **Kunci publik**: saat pasangan kunci SSH dibuat, Tencent Cloud hanya menyimpan kunci publik, dan menyimpannya di file `~/.ssh/authorized_keys`.
- **Kunci pribadi**: Anda perlu mengunduh kunci pribadi dan menyimpannya secara rahasia. Kunci pribadi hanya dapat diunduh satu kali. Tencent Cloud tidak akan menyimpan kunci pribadi Anda. Siapa pun yang memiliki kunci pribadi Anda dapat mengakses instans Anda. Pastikan untuk menyimpannya dengan aman.

Anda bisa menggunakan pasangan kunci untuk terhubung ke CVM dengan aman. Cara ini lebih aman daripada login dengan kata sandi. Anda hanya perlu menentukan pasangan kunci saat membuat instans Linux, atau mengikat pasangan kunci ke instans yang ada, sehingga Anda bisa menggunakan kunci pribadi untuk login ke instans tanpa memasukkan kata sandi.

## Fitur dan Keunggulan
Dibandingkan dengan metode autentikasi kata sandi tradisional, login pasangan kunci SSH memiliki keunggulan sebagai berikut:
- Login pasangan kunci SSH lebih kompleks dan sulit untuk diserang oleh brute-force.
- Login pasangan kunci SSH lebih mudah digunakan. Anda bisa login ke instans dari jarak jauh dengan beberapa langkah konfigurasi sederhana di konsol dan klien lokal Anda, dan tidak perlu memasukkan kata sandi saat login lagi.

## Batasan Penggunaan
- Login pasangan kunci SSH hanya tersedia untuk instans Linux.
- Setiap akun Tencent Cloud bisa memiliki hingga 100 pasangan kunci SSH.
- Tencent Cloud tidak akan menyimpan kunci pribadi Anda. Anda perlu mengunduh kunci pribadi setelah membuat kunci SSH, dan menyimpannya dengan aman.
- Untuk memastikan keamanan data, Anda harus mematikan instans sebelum memuat kunci.
- Untuk meningkatkan keamanan CVM, Anda tidak bisa menggunakan metode login kata sandi setelah mengikat pasangan kunci ke instans.


## Kasus Penggunaan
- Untuk mempelajari tentang cara membuat, mengikat, melepas ikatan, atau menghapus kunci, lihat [Mengelola Pasangan Kunci SSH](https://intl.cloud.tencent.com/document/product/213/16691).
- Untuk mempelajari tentang cara login ke instans CVM dari jarak jauh dengan menggunakan pasangan kunci SSH, lihat
 - [Login ke Instans Linux melalui Fitur Login Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32502)
 - [Login ke Instans Linux melalui Kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501)



