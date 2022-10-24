## Ikhtisar
Untuk operasi seperti manajemen kata sandi, perbaikan dan pemeliharaan SSHD sebelum pemasangan disk, pengguna Linux harus masuk ke mode pengguna tunggal. Dokumen ini menjelaskan cara melakukan boot ke dalam mode ini di distribusi Linux arus utama.

## Petunjuk
1. Di konsol CVM, pilih VNC untuk login ke CVM. Untuk petunjuk mendetail, lihat [Login ke Instans Linux melalui VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Di jendela login VNC, pilih **Send CtrlAltDel** (Kirim CtrlAltDel) di sudut kiri atas, tekan **Ctrl-Alt-Delete** (Ctrl-Alt-Delete), lalu klik **OK** (OKE) di kotak perintah.
3. Saat pesan kegagalan koneksi muncul, tekan panah Atas atau Bawah untuk memuat ulang halaman dan arahkan kursor ke menu `grub`, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/350187ce0a771d00e6d54e929291ebae.png)
4. Tekan **e** (e) untuk masuk ke mode grub rescue.
5. Lakukan langkah-langkah yang sesuai dengan versi sistem operasi Anda.
<dx-tabs>
::: CentOS\s6.x
1. Pilih kernel dalam mode grub, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/5abc9f57184cc74bba927513fb1c4a88.png)
2. Tekan **e** (e) untuk masuk ke halaman edit kernel, pilih baris **kernel** (kernel) menggunakan panah Atas atau Bawah, dan tekan **e** (e) lagi, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/1a596a48df87d1d619e415d8d5b0cb65.png)
3. Masukkan **single** (tunggal) di akhir baris, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/e1f74a4ce211a34301c4f74ffcc790b8.png)
4. Tekan **Enter** (Enter), lalu tekan **b** (b) untuk melakukan boot pada baris perintah yang dipilih dan masuk ke mode pengguna tunggal, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/b379937bfc15e93f0823ec50095d1dc6.png)
Gambar berikut menunjukkan bahwa sistem melakukan boot ke mode pengguna tunggal.
![](https://main.qcloudimg.com/raw/517c4d2c24864f3fc8f5002bd1e2c2a1.png)
<dx-alert infotype="explain" title="">
Anda dapat menjalankan perintah `exec /sbin/init` untuk keluar dari mode pengguna tunggal.
</dx-alert>
:::
::: CentOS\s7.x
1. Pilih kernel dalam mode grub, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/2ddc7d1e4416d9fa763922e23b59d580.png)
2. Tekan **e** (e) untuk masuk ke halaman edit kernel. Cari baris yang dimulai dengan “linux16” menggunakan panah Atas atau Bawah dan ganti `ro` dengan `rw init=/bin/bash` atau `/usr/bin/bash`, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/1b861ba0ecee1cd82da4364523e8a1c6.png)
3. Tekan **Ctrl+X** (Ctrl+X) untuk melakukan boot ke mode pengguna tunggal, seperti yang ditunjukkan di bawah ini:
Gambar berikut menunjukkan bahwa sistem melakukan boot ke mode pengguna tunggal.
![](https://main.qcloudimg.com/raw/fbe8cfcf43aa4c914882edc4c3ee5faf.png)
<dx-alert infotype="explain" title="">
 Anda dapat menjalankan perintah `exec /sbin/init` untuk keluar dari mode pengguna tunggal.
</dx-alert>
:::
::: CentOS\s8.0
1. Pilih kernel dalam mode grub, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/a6ce701e5845141929d822635bd42b9a.png)
2. Tekan **e** (e) untuk masuk ke halaman edit kernel. Temukan baris yang dimulai dengan “linux” menggunakan panah Atas atau Bawah dan ganti `ro` dengan `rw init=/sysroot/bin/bash`, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/d06effc3cab12d545fd7bc92f4577b14.png)
3. Tekan **Ctrl+X** (Ctrl+X) untuk melakukan boot ke mode pengguna tunggal, seperti yang ditunjukkan di bawah ini:
Gambar berikut menunjukkan bahwa sistem melakukan boot ke mode pengguna tunggal.
![](https://main.qcloudimg.com/raw/126dcdb5916e57815c3632e9e4b24412.png)
:::
::: Ubuntu\satau\sDebian
1. Pilih kernel dalam mode grub, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/c3c0be766481edf3f6521f7764f8d4cb.png)
2. Tekan **e** (e) untuk masuk ke halaman edit kernel. Temukan baris yang dimulai dengan “linux” menggunakan panah Atas atau Bawah dan tambahkan `quiet splash rw init=/bin/bash` ke akhir baris, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/40882cf22d755c0338ea9d7c106bc280.png)
3. Tekan **Ctrl+X** (Ctrl+X) untuk melakukan boot ke mode pengguna tunggal, seperti yang ditunjukkan di bawah ini:
Gambar berikut menunjukkan bahwa sistem melakukan boot ke mode pengguna tunggal.
![](https://main.qcloudimg.com/raw/df55d20b7eb087744fb6283c5124e7fc.png)
:::
::: SUSE
1. Pilih kernel dalam mode grub, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/4da4d0c5c98e4f0dbe4990e920a11daf.png)
2. Tekan **e** (e) untuk masuk ke halaman edit kernel. Temukan baris yang dimulai dengan “linux” menggunakan panah Atas atau Bawah, tambahkan `rw` di awal dan `1` di akhir parameter `splash`, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/013a0099ccb5c19d04441dd60ea7558b.png)
3. Tekan **Ctrl+X** (Ctrl+X) untuk melakukan boot ke mode pengguna tunggal, seperti yang ditunjukkan di bawah ini:
:::
::: tlinux
1. Pilih kernel dalam mode grub, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/c497e63321b76e5cd1f0eea06f53cdb2.png)
2. Tekan **e** (e) untuk masuk ke halaman edit kernel, pilih baris **kernel** (kernel) menggunakan panah Atas atau Bawah, dan tekan **e** (e) lagi, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/06c66e0f30163e9fc7e6aafbf9463645.png)
3. Tambahkan spasi dan **1** (1) ke bagian akhir baris (yaitu setelah **256M** (256M)), seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/06efb32e3a2edb39f32e13be1ab8527f.png)
4. Tekan **Enter** (Enter) untuk masuk ke mode pengguna tunggal.
:::
</dx-tabs>
