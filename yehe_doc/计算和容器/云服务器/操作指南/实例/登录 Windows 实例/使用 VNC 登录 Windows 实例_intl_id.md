## Skenario

Login VNC yang ditawarkan oleh Tencent memungkinkan pengguna terhubung dari jarak jauh ke CVM melalui browser web. Jika klien tidak menginstal login jarak jauh, metode tersebut tidak dapat digunakan atau login melalui cara lain, pengguna dapat terhubung ke CVM menggunakan login VNC untuk mengamati status CVM dan melakukan operasi manajemen CVM dasar menggunakan akun CVM.

## Batasan Penggunaan

- Fitur seperti salin/tempel, masukan bahasa Mandarin, dan unggah/unduh file saat ini tidak didukung pada CVM yang menggunakan login VNC.
- Browser umum harus digunakan saat menggunakan login VNC pada CVM, seperti Chrome, Firefox, dan IE 10 atau yang lebih baru.
- Login VNC adalah terminal khusus, artinya hanya satu pengguna yang dapat menggunakan login VNC pada satu waktu.

## OS yang Berlaku

Windows, Linux, atau macOS.

## Prasyarat

Anda harus sudah memiliki akun/kata sandi admin untuk login ke instans Windows dari jarak jauh.
- Jika Anda menggunakan kata sandi default sistem untuk login ke instans, dapatkan dengan membuka [Pesan Internal](https://console.cloud.tencent.com/message).
Jika Anda lupa kata sandi, [atur ulang kata sandi instans](http://intl.cloud.tencent.com/document/product/213/16566).

## Langkah-Langkah

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman manajemen instans, pilih Windows CVM tempat Anda ingin login, lalu klik **Log In** (Login), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. Di jendela pop-up **Log into Windows instance** (Login ke instans Windows), pilih **Alternative login methods (VNC)** (Metode login alternatif (VNC)), lalu klik **Log In Now** (Login Sekarang), seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/9f964c1ebdec90f7e371b42340e13662.png)
4. Di jendela login, pilih “Send Remote Command” (Kirim Perintah Jarak Jauh) di sudut kiri atas, lalu tekan **Ctrl-Alt-Delete** (Ctrl-Alt-Delete) untuk masuk ke antarmuka login sistem seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/c07755c1e0d0040e2ecb87f048b8be1b.png)



