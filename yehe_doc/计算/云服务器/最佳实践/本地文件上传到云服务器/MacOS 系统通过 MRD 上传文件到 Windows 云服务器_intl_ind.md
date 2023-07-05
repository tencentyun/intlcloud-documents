## Ikhtisar
Microsoft Remote Desktop (MRD) adalah perangkat lunak desktop jarak jauh yang dikembangkan oleh Microsoft. Dokumen ini menjelaskan cara menggunakannya di MacOS untuk mengunggah file ke Tencent Cloud CVM dengan Windows Server 2012 R2 yang telah diinstal. 

## Prasyarat
- Anda telah mengunduh dan menginstal MRD di komputer lokal Anda. Operasi berikut menggunakan Microsoft Remote Desktop untuk Mac sebagai contoh. Microsoft berhenti menyediakan tautan untuk mengunduh klien Remote Desktop pada tahun 2017. Saat ini, anak perusahaannya HockeyApp bertanggung jawab untuk merilis klien beta. Buka [Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac) untuk mengunduh versi Beta.
- MRD mendukung MacOS 10.10 dan versi yang lebih baru. Pastikan sistem operasi Anda kompatibel.
- Anda telah membeli CVM Windows.

## Petunjuk
### Mendapatkan IP publik
Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index), buka halaman **Instances** (Instans), dan catat IP publik CVM tempat Anda ingin mengunggah file, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)

### Mengunggah file
1. Mulai MRD dan klik **Add Desktop** (Tambahkan Desktop), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
2. Di jendela pop-up **Add Desktop** (Tambahkan Desktop), ikuti langkah-langkah di bawah ini untuk memilih folder yang akan diunggah dan membuat koneksi dengan CVM Windows Anda.
![](https://main.qcloudimg.com/raw/fc241ce8e4744bde57476ea823fcef72.png)
  1. Di bidang teks **PC name** (Nama PC), masukkan alamat IP publik CVM Anda.
  2. Klik **Folder** (Folder) untuk mengalihkan ke daftar folder.
  3. Klik <img src="https://main.qcloudimg.com/raw/89e7a3ff040849307cd1eb8bd878a2db.png" style="margin:-3px 0px"> di sudut kiri bawah dan pilih folder yang akan diunggah di jendela pop-up.
  4. Periksa daftar folder yang akan diunggah dan klik **Add** (Tambahkan).
  5. Pertahankan pengaturan default untuk opsi lain, lalu buat koneksi.
Entri Anda sekarang telah disimpan, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Klik dua kali entri baru. Masukkan nama pengguna dan kata sandi Anda untuk CVM, lalu klik **Continue** (Lanjutkan).
>?
>- Akun default untuk CVM Windows adalah `Administrator`.
>- Jika Anda menggunakan kata sandi default sistem untuk login ke instans, buka [Pusat Pesan](https://console.cloud.tencent.com/message) untuk mendapatkan kata sandi terlebih dahulu.
>- Jika Anda lupa kata sandi, harap [atur ulang kata sandi instans](http://intl.cloud.tencent.com/document/product/213/16566).
>
5. Di jendela pop-up, klik **Continue** (Lanjutkan) untuk membuat koneksi, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
Jika koneksi berhasil, akan muncul halaman berikut:
![](https://main.qcloudimg.com/raw/5a524210acd13624af7263b6de3aea54.png)
6. Klik <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px"> di sudut kiri bawah dan pilih **My Computer** (Komputer Saya) untuk melihat daftar folder bersama.
7. Klik dua kali folder bersama untuk membukanya. Salin file lokal yang diinginkan ke drive lain dari Windows CVM.
Misalnya, salin file A pada bagian folder ke drive C CVM Windows.

### Mengunduh file
Untuk mengunduh file dari CVM Windows ke komputer Anda, Anda hanya perlu menyalin file yang diinginkan dari CVM ke folder bersama.


