## Ikhtisar

Remote Desktop Protocol (RDP) adalah protokol multi-saluran yang dikembangkan oleh Microsoft yang memungkinkan komputer lokal terhubung ke komputer jarak jauh. Sebaiknya gunakan RDP untuk login ke CVM Windows Anda. Dokumen ini menjelaskan cara login ke instans Windows menggunakan file RDP.

## Sistem yang Didukung
Anda dapat login ke CVM Anda dari Windows, Linux, dan MacOS menggunakan RDP.

## Prasyarat

- Anda harus memiliki akun admin dan kata sandi untuk login ke instans Windows dari jarak jauh.
 - Jika Anda menggunakan kata sandi default sistem untuk login ke instans, Anda dapat memperoleh kata sandi di [Pusat Pesan](https://console.cloud.tencent.com/message).
 - Jika Anda lupa kata sandi, harap [atur ulang kata sandi instans](https://intl.cloud.tencent.com/document/product/213/16566).
- Anda telah membeli IP publik untuk instans CVM Anda dan port 3389 terbuka. (port ini terbuka secara default untuk CVM yang dibeli dengan konfigurasi cepat).

## Petunjuk

### Login ke CVM Anda di Windows menggunakan RDP
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman **Instances** (Instans), cari CVM Windows tempat Anda ingin login, lalu klik **Log In** (Login) seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. Di jendela pop-up **Log into Windows instance** (Login ke instans Windows), pilih **Log in with RDP file** (Login dengan file RDP) dan klik **Download RDP file** (Unduh file RDP) untuk mengunggah file RDP ke komputer lokal Anda.
>?Jika Anda telah mengubah port login jarak jauh, tambahkan alamat IP dengan `:port` di file RDP.
>
![](https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png)
4. Klik dua kali file RDP yang diunduh, masukkan kata sandi, lalu klik **OK** (OKE) untuk menyambungkan ke CVM Windows Anda dari jarak jauh.
 - Jika Anda menggunakan kata sandi default sistem untuk login ke instans, Anda dapat memperoleh kata sandi di [Pusat Pesan](https://console.cloud.tencent.com/message).
 - Jika Anda lupa kata sandi, harap [atur ulang kata sandi instans](https://intl.cloud.tencent.com/document/product/213/16566).

### Login ke CVM Anda di Linux menggunakan RDP

>? Sebaiknya gunakan rdesktop sebagai klien desktop jarak jauh. Untuk informasi selengkapnya, lihat [pengantar resmi rdesktop](http://www.rdesktop.org/).
>
1. Jalankan perintah berikut untuk memeriksa apakah rdesktop telah diinstal.
```
rdesktop
```
 - Jika ya, lakukan [langkah 4](#step04).
 - Jika tidak, Anda akan diminta dengan "command not found" (perintah tidak ditemukan). Dalam hal ini, lakukan [langkah 2](#step02).
2. <span id="step02"></span>Buka jendela terminal, lalu jalankan perintah berikut untuk mengunduh rdesktop. Langkah ini menggunakan rdesktop v1.8.3 sebagai contoh.
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
Jika Anda ingin menginstal versi terbaru, buka [halaman desktop di GitHub](https://github.com/rdesktop/rdesktop/releases) untuk menemukannya. Kemudian, ganti jalur dalam perintah dengan versi terbaru.
3. Di direktori tempat rdesktop akan diinstal, jalankan perintah berikut untuk mendekompresi dan menginstal rdesktop.
```
tar xvzf rdesktop-<x.x.x>.tar.gz ## Ganti x.x.x dengan nomor versi rdesktop yang diunduh. 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. <span id="step04">Jalankan perintah berikut untuk terhubung ke instans Windows jarak jauh.</span>
>? Ganti parameter dalam contoh dengan parameter Anda sendiri.
>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator` mengacu pada akun admin yang disebutkan di bagian prasyarat.
 - `<your-password>` mengacu pada kata sandi login yang Anda tetapkan.
   Jika Anda menggunakan kata sandi default sistem untuk masuk ke instans, Anda dapat memperoleh kata sandi di [Pusat Pesan](https://console.cloud.tencent.com/message). Jika Anda lupa kata sandi Anda, harap [atur ulang kata sandi instans](https://intl.cloud.tencent.com/document/product/213/16566).
 - `<hostname or IP address>` mengacu pada alamat IP publik atau nama domain kustom dari instans Windows Anda.
 
### Login ke CVM Anda di MacOS menggunakan RDP

>?
>- Operasi berikut menggunakan Microsoft Remote Desktop untuk Mac sebagai contoh. Microsoft berhenti menyediakan tautan untuk mengunduh klien Remote Desktop pada tahun 2017. Saat ini, anak perusahaannya, HockeyApp, bertanggung jawab untuk merilis klien beta. Buka [Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac) untuk mengunduh versi Beta.
>- Operasi berikut menggunakan CVM pada Windows Server 2012 R2 sebagai contoh.
>
1. Unduh dan instal Microsoft Remote Desktop untuk Mac di komputer lokal Anda.
2. Mulai MRD dan klik **Add Desktop** (Tambahkan Desktop), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. Di jendela pop-up **Add Desktop** (Tambahkan Desktop), ikuti langkah-langkah yang diilustrasikan pada citra berikut untuk membuat koneksi ke CVM Windows Anda.
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1. Di kolom teks **PC name** (Nama PC), masukkan alamat IP publik CVM Anda.
    2. Klik **Add** (Tambahkan).
    3. Pertahankan pengaturan default untuk opsi lain, lalu buat koneksi.
    Entri Anda sekarang telah disimpan, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Klik dua kali entri baru. Masukkan nama pengguna dan kata sandi Anda untuk CVM, lalu klik **Continue** (Lanjutkan).
 - Jika Anda menggunakan kata sandi default sistem untuk login ke instans, Anda dapat memperoleh kata sandi di [Pusat Pesan](https://console.cloud.tencent.com/message).
 - Jika Anda lupa kata sandi, harap [atur ulang kata sandi instans](https://intl.cloud.tencent.com/document/product/213/16566).
5. Di jendela pop-up, klik **Continue** (Lanjutkan) untuk membuat koneksi, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
Jika koneksi berhasil, akan muncul halaman berikut:
![](https://main.qcloudimg.com/raw/20db4a1d63384bc0575ded68a8fe912d.png)
