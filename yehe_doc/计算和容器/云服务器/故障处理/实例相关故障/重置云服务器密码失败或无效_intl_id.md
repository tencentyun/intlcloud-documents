Dokumen ini menggunakan Windows Server 2012 sebagai contoh untuk menjelaskan cara memecahkan masalah atur ulang kata sandi CVM yang gagal atau tidak valid.

## Masalah

- Setelah kata sandi CVM diatur ulang, sistem akan memunculkan prompt "The system is busy, and your instance password failed to be reset (7617d94c)." (Sistem sedang sibuk, dan kata sandi instans Anda gagal diatur ulang (7617d94c).)
- Setelah kata sandi CVM diatur ulang, kata sandi baru tidak berlaku, dan kata sandi login harus menggunakan yang default.


## Kemungkinan Penyebab
Kemungkinan penyebabnya adalah:
- Komponen Cloudbase-Init di CVM rusak, dimodifikasi, dinonaktifkan, atau tidak diluncurkan.
- Komponen proses sistem diblokir oleh program keamanan (mis., 360 Safeguard) yang diinstal pada CVM.


## Pemecahan Masalah

Berdasarkan kemungkinan penyebabnya, atasi masalah sebagai berikut:

### Memeriksa layanan Cloudbase-Init

1. [Login ke instans Windows melalui VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Di desktop, klik kanan <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> dan pilih **Run** (Jalankan). Masukkan **services.msc** (services.msc) di kotak dialog **Run** (Jalankan), dan tekan **Enter** (Enter) untuk membuka jendela **Services** (Layanan).
3. Periksa apakah layanan cloudbase-init ada, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/2615f5c0e68a31174c16c9a80884455c.png)
 - Jika ya, lanjutkan ke langkah berikutnya.
 - Jika tidak, instal ulang layanan cloudbase-init. Untuk informasi selengkapnya, lihat [Menginstal Cloudbase-Init di Windows](https://intl.cloud.tencent.com/document/product/213/32364).
4. Klik dua kali layanan cloudbase-init untuk membuka kotak dialog properti cloudbase-init, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/10702cb2e359d6de36aec4960771c841.png)
5. Pilih tab **General** (Umum) dan periksa apakah jenis startup cloudbase-init adalah **Automatic** (Otomatis).
 - Jika ya, lanjutkan ke langkah berikutnya.
 - Jika tidak, atur jenis startup cloudbase-init ke **Automatic** (Otomatis).
6. Alihkan ke tab **Log On** (Login) dan periksa apakah **Local System account** (akun Sistem Lokal) dipilih untuk layanan cloudbase-init.
 - Jika ya, lanjutkan ke langkah berikutnya.
 - Jika tidak, pilih **Local System account** (akun Sistem Lokal) untuk layanan cloudbase-init.
7. Alihkan ke tab **General** (Umum), klik **Start** (Mulai) di **Service status** (Status layanan) untuk mengaktifkan layanan cloudbase-init secara manual, dan periksa apakah terjadi kesalahan.
 - Jika ya, [periksa program keamanan yang diinstal pada CVM](#CheckSecuritySoftware).
 - Jika tidak, lanjutkan ke langkah berikutnya.
8. Di desktop, klik kanan <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> dan pilih **Run** (Jalankan). Masukkan **regedit** (regedit) di kotak dialog **Run** (Jalankan), dan tekan **Enter** (Enter) untuk membuka jendela **Registry Editor** (Editor Registri).
9. Di panel navigasi registri di sebelah kiri, perluas hierarki berikut secara berurutan: **HKEY_LOCAL_MACHINE** (HKEY_LOCAL_MACHINE) > **SOFTWARE** (PERANGKAT LUNAK) > **Cloudbase Solutions** (Solusi Cloudbase) > **Cloudbase-Init** (Cloudbase-Init).
10. Temukan semua kunci registri "LocalScriptsPlugin" pada bagian **ins-xxx** (ins-xxx) dan periksa apakah nilai LocalScriptsPlugin adalah 2.
![](https://main.qcloudimg.com/raw/75580b56e3a28fb9e0559372eb33ff11.png)
 - Jika ya, lanjutkan ke langkah berikutnya.
 - Jika tidak, atur nilai LocalScriptsPlugin ke 2.
11. Di desktop, klik <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> dan pilih **This PC** (PC ini). Periksa apakah driver CD dimuat di bawah **Devices and drives** (Perangkat dan drive), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/8755719fb39bb5f841f4c32897545233.png)
 - Jika ya, [periksa program keamanan yang diinstal pada CVM](#CheckSecuritySoftware).
 - Jika tidak, luncurkan driver CD-ROM di Device Manager.

<span id="CheckSecuritySoftware"></span>
### Memeriksa program keamanan yang diinstal pada CVM

Pindai kerentanan CVM menggunakan program keamanan yang diinstal dan periksa apakah komponen Cloudbase-Init diblokir.
- Jika CVM memiliki kerentanan, perbaiki.
- Jika komponen inti diblokir, buka blokirnya.

Untuk mencegah pengaturan ulang kata sandi CVM yang gagal atau tidak valid, sebaiknya tambahkan direktori dan file berikut ke daftar yang diizinkan dan lokasi tepercaya dari program keamanan.
- Daftar direktori berikut dalam program keamanan yang diizinkan:
```
C:\Windows\System32\WindowsPowerShell\
C:\Program Files\Cloudbase Solutions\Cloudbase-Init\Python\Scripts
C:\Program Files\QCloud
C:\Program Files\Cloudbase Solutions\
```
- Tambahkan file berikut ke lokasi tepercaya:
```
C:\Windows\System32\cmd.exe
C:\Windows\SysWOW64\cmd.exe
```

