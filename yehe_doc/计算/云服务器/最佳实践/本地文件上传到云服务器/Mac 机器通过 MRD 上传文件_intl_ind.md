## Skenario
Microsoft Remote Desktop (MRD) adalah perangkat lunak desktop jarak jauh oleh Microsoft. Artikel ini menjelaskan cara menggunakannya di MacOS untuk mengunggah file ke CVM dengan Windows Server 2012 R2 yang telah diinstal. 


## Prasyarat
- Unduh dan instal [Microsoft Remote Desktop untuk Mac](https://www.techspot.com/downloads/4698-microsoft-remote-desktop-for-mac.html).
- MRD mendukung MacOS 10.10 dan versi yang lebih baru. Pastikan Anda memiliki OS yang kompatibel.
- Membeli CVM Windows.


## Petunjuk
### Mendapatkan IP Publik CVM
Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index) dan catat alamat IP publik instans CVM Anda di halaman daftar instans, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)


### Mengunggah File
1. Mulai MRD dan klik **Add Desktop** (Tambahkan Desktop), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
2. Jendela **Add Desktop** (Tambahkan Desktop) akan muncul. Ikuti langkah-langkah yang diilustrasikan pada gambar berikut untuk memilih folder yang akan diunggah dan membuat koneksi dengan Windows CVM Anda:
![](https://main.qcloudimg.com/raw/fc241ce8e4744bde57476ea823fcef72.png)
  1. Di bidang teks **PC name** (Nama PC), masukkan IP publik CVM Anda.
  2. Klik **Folder** (Folder) untuk beralih ke tampilan daftar folder.
  3. Klik <img src="https://main.qcloudimg.com/raw/89e7a3ff040849307cd1eb8bd878a2db.png" style="margin:-3px 0px">. Di jendela pop-up, pilih folder yang akan diunggah. 
  4. Setelah selesai, periksa daftar folder yang akan diunggah dan klik **Add** (Tambahkan).
  5. Biarkan opsi lain sebagai default, lalu selesaikan prosesnya.
Entri Anda disimpan, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Klik dua kali entri yang baru ditambahkan. Masukkan nama pengguna dan kata sandi Anda untuk CVM, lalu klik **Continue** (Lanjutkan).
>
>- Akun default untuk CVM Windows adalah `Administrator`.
>- Jika Anda memilih untuk masuk dengan kata sandi acak, harap periksa di [Pusat Pesan](https://console.cloud.tencent.com/message).
>- Jika Anda lupa kata sandi, harap [atur ulang kata sandi instans](http://intl.cloud.tencent.com/document/product/213/16566).
>
5. Klik **Continue** (Lanjutkan) untuk membuat koneksi, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
Jika koneksi berhasil, halaman berikut akan muncul:
![](https://main.qcloudimg.com/raw/3d36c84ef12110a81879377f56a7e26c.png)
7. Di sudut kiri bawah, klik <img src="https://main.qcloudimg.com/raw/20fd46098cf037eb003dc41f1f913313.png" style="margin:-3px 0px;"/> lalu **My Computer** (Komputer Saya) untuk melihat daftar folder bersama.
8. Klik dua kali folder bersama untuk membukanya. Salin file lokal yang diinginkan ke drive lain di Windows CVM untuk menyelesaikan pengunggahan.
Misalnya, salin **a.txt** (a.txt) ke drive C di CVM Windows.

### Mengunduh File
Untuk mengunduh file dari CVM Windows ke komputer Anda, salin file yang diinginkan dari CVM ke folder bersama.


