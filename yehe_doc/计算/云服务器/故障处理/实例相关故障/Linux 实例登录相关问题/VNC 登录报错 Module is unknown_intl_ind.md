## Deskripsi Kesalahan
Saya memasukkan kata sandi yang benar, tetapi masih tidak bisa login ke CVM menggunakan VNC. Pesan “Module is unknown” (Modul tidak diketahui) muncul.
![](https://main.qcloudimg.com/raw/117961622ff73a5859a56bd890011302.png)

## Kemungkinan Alasan
Masalah ini mungkin disebabkan oleh konfigurasi `/etc/pam.d/system-auth` di file `/etc/pam.d/login`. 
![](https://main.qcloudimg.com/raw/334e393e16d8a03eec44009be9265ea9.png)
Jika jalur modul `pam_limits.so` tidak dikonfigurasi dengan benar dalam file konfigurasi `system-auth`, proses login akan gagal.
![](https://main.qcloudimg.com/raw/36f36e0f2f5d0954f6fcebd39095d3b6.png)
<dx-alert infotype="explain" title="">
Modul `pam_limits.so` membatasi penggunaan sumber daya sistem pengguna selama sesi. Jika jalur modul tidak dikonfigurasi dengan benar sesuai dengan sistem operasi yang sebenarnya, autentikasi login akan gagal.

</dx-alert>



## Solusi
1. Lakukan [prosedur pemecahan masalah](#ProcessingSteps) untuk menemukan konfigurasi jalur `pam_limits.so` dalam file `system-auth`.
2. Perbaiki jalur modul `pam_limits.so`. 

[](id:ProcessingSteps)

## Prosedur Pemecahan Masalah

1. Coba [login ke CVM Linux melalui kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501).
 - Jika login berhasil, lanjutkan ke langkah berikutnya.
 - Jika login gagal, gunakan mode pengguna tunggal. Untuk informasi selengkapnya, lihat [Melakukan booting ke Mode Pengguna Tunggal Linux](https://intl.cloud.tencent.com/document/product/213/34819).
2. Jalankan perintah berikut untuk melihat log.
```
vim /var/log/secure
```
File ini mencatat informasi keamanan, sebagian besar log login CVM. Anda dapat memeriksa log kesalahan `/lib/security/pam_limits.so` seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/8f9f992d1835a9058020b435f1ef3c99.png)
3. Jalankan perintah berikut secara berurutan untuk masuk ke direktori `/etc/pam.d` dan cari `/lib/security/pam_limits.so`.
```
cd /etc/pam.d
```
```
find . | xargs grep -ri "/lib/security/pam_limits.so" -l
```
Jika hasil yang mirip dengan gambar berikut ditampilkan, /lib/security/pam_limits.so dikonfigurasi dalam file `system-auth`.
![](https://main.qcloudimg.com/raw/eab27cf686eccfeb8a8b796360010bb5.png)
4. Akses file `system-auth` untuk memperbaiki jalur modul `pam_limits.so`.
Misalnya, Anda dapat menggunakan jalur absolut `/lib64/security/pam_limits.so` atau jalur relatif `pam_limits.so` dalam sistem operasi 64-bit.


