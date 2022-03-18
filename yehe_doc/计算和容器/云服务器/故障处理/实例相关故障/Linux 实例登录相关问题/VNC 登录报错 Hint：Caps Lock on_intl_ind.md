## Deskripsi Kesalahan
Ketika saya mencoba login ke CVM melalui VNC, pesan “Hint: Caps Lock on” (Petunjuk: Caps Lock aktif) muncul setelah saya memasukkan kata sandi.
![](https://main.qcloudimg.com/raw/345dfc1dbe0c44d8836c94b6637ef4b0.png)
Dan ketika saya mencoba login dari jarak jauh menggunakan kunci SSH, muncul pesan “Permission denied, please try again” (Izin ditolak, harap coba lagi).
![](https://main.qcloudimg.com/raw/db09e73d2a057fb8b297ffd31bf67b62.png)

## Kemungkinan Alasan
File log `/var/log/btmp` terlalu besar karena serangan brute force. File ini menyimpan log login yang gagal. Jika terlalu besar, log tidak dapat ditulis ke dalamnya, yang dapat menyebabkan kesalahan login.
![](https://main.qcloudimg.com/raw/c19f9e57a67ce6b1ed30cee22af9964c.png)

## Solusi
1. Periksa apakah file log `/var/log/btmp` terlalu besar seperti yang diinstruksikan dalam [Prosedur Pemecahan Masalah](#ProcessingSteps). 
2. Konfirmasikan apakah itu disebabkan oleh serangan brute force dan tingkatkan kebijakan keamanan.

[](id:ProcessingSteps)

## Prosedur Pemecahan Masalah

1. Coba [login ke CVM Linux melalui kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501).
	- Jika login berhasil, lanjutkan ke langkah berikutnya.
	- Jika login gagal, coba mode pengguna tunggal. Untuk informasi selengkapnya, lihat [Melakukan booting ke Mode Pengguna Tunggal Linux](https://intl.cloud.tencent.com/document/product/213/34819).
2. Akses `/var/log` dan periksa ukuran file log `/var/log/btmp`.
3. Jalankan perintah berikut untuk menghapus file log `/var/log/btmp` yang terlalu besar. Kemudian Anda dapat login secara normal.
```
cat /dev/null > /var/log/btmp
```
4. Periksa apakah penguncian akun disebabkan oleh kesalahan operasi atau serangan brute force. Dalam kasus selanjutnya, sebaiknya Anda memperkuat kebijakan keamanan sebagai berikut:
	- Ubah kata sandi CVM menjadi kata sandi yang lebih kuat yang berisi 12-16 karakter, yang menyertakan huruf besar, huruf kecil, karakter khusus, dan angka. Untuk informasi selengkapnya, lihat [Mengatur Ulang Kata Sandi Instans](https://intl.cloud.tencent.com/document/product/213/16566).
	- Hapus akun login CVM yang tidak digunakan.
	- Ubah port ssh default 22 ke port yang kurang umum antara 1024-65525. Untuk informasi selengkapnya, lihat [Mengubah Port Jarak Jauh Default pada CVM](https://intl.cloud.tencent.com/document/product/213/35376).
	- Kelola aturan grup keamanan terkait untuk hanya membuka port dan protokol yang diperlukan oleh bisnis Anda. Untuk informasi selengkapnya, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).
	- Tutup port untuk akses internet untuk aplikasi inti seperti database MySQL dan Redis. 
	- Instal perangkat lunak keamanan (seperti agen CWP), dan konfigurasikan alarm secara real time untuk mendapat pemberitahuan tentang login yang mencurigakan sesegera mungkin.
