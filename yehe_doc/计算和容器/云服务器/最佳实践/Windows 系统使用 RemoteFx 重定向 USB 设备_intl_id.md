## Skenario

RemoteFx adalah versi yang ditingkatkan dari Windows Remote Desktop Protocol (RDP). Dari RDP 8.0, RemoteFx dapat digunakan untuk mengarahkan perangkat USB lokal ke desktop jarak jauh melalui saluran data RDP, yang memastikan bahwa CVM dapat menggunakan perangkat USB ini.

Dokumen ini menggunakan versi lingkungan berikut sebagai contoh untuk menjelaskan cara mengaktifkan fitur pengalihan USB RemoteFx dari RDP untuk mengalihkan perangkat USB ke CVM.
- Klien: Windows 10
- Server: Windows Server 2016

## Batasan Penggunaan

Karena RDP 8.0 dan versi yang lebih baru mendukung fitur pengalihan USB RemoteFx, Windows 8, Windows 10, Windows Server 2016, dan Windows Server 2019 semuanya mendukung fitur ini. Jika sistem operasi PC lokal Anda memiliki salah satu versi ini, Anda tidak perlu menginstal patch pembaruan RDP 8.0. Jika PC lokal Anda memiliki Windows 7 atau Windows Vista, harap buka [situs web resmi Microsoft](https://support.microsoft.com/en-us) untuk mendapatkan dan menginstal patch pembaruan RDP 8.0.


## Petunjuk

### Mengonfigurasi server

1. [Login ke instans Windows menggunakan file RDP (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5435).
2. Di desktop, klik <img src="https://main.qcloudimg.com/raw/ab9a3a22baf69f63a90a43476f12db94.png" style="margin: 0;"></img> dan pilih **Server Manager** (Pengelola Server) untuk membuka Pengelola Server.
3. Di jendela "Server Manager" (Pengelola Server), klik **Add roles and features** (Tambahkan peran dan fitur), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/4ee64b60cf2993013698c2f641ea8dc1.png)
4. Di jendela pop-up "Add Roles and Features Wizard" (Wizard Tambahkan Peran dan Fitur), klik **Next** (Selanjutnya) untuk membuka halaman "Select installation type" (Pilih jenis penginstalan).
5. Pada halaman "Select installation type" (Pilih jenis penginstalan), pilih **Role-based or feature-based installation** (Penginstalan berbasis peran atau berbasis fitur) dan klik **Next** (Selanjutnya).
6. Pada halaman "Select destination server" (Pilih server tujuan), pertahankan konfigurasi default dan klik **Next** (Selanjutnya).
7. Pada halaman "Select server roles" (Pilih peran server), pilih **Remote Desktop Services** (Layanan Desktop Jarak Jauh) dan klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/76481a67eb8aa5b98e2e8a8de5895263.png)
8. Pertahankan konfigurasi default dan klik **Next** (Selanjutnya) sebanyak 2 kali.
9. Pada halaman "Select role services" (Pilih layanan peran), pilih **Remote Desktop Session Host** (Host Sesi Desktop Jarak Jauh), **Remote Desktop Connection Broker** (Broker Koneksi Desktop Jarak Jauh), dan **Remote Desktop Licensing** (Lisensi Desktop Jarak Jauh). Di jendela pop-up, klik **Add Features** (Tambahkan Fitur), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/38d46bf2c391f82684c5c82c439df3ec.png)
10. Klik **Next** (Selanjutnya).
11. Klik **Install** (Instal).
12. Setelah penginstalan selesai, mulai ulang CVM.
13. Di desktop, klik <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>, masukkan **gpedit.msc** (gpedit.msc), dan tekan Enter untuk membuka "Local Group Policy Editor" (Editor Kebijakan Grup Lokal).
14. Di pohon navigasi sebelah kiri, pilih **Computer Configuration** (Konfigurasi Komputer) > **Administrative Templates** (Templat Administratif) > **Windows Components** (Komponen Windows) > **Remote Desktop Services** (Layanan Desktop Jarak Jauh) > **Remote Desktop Session Host** (Host Sesi Desktop Jarak Jauh) > **Device and Resource Redirection** (Pengalihan Sumber Daya dan Perangkat), dan klik dua kali **Do not allow supported Plug and Play device redirection** (Jangan izinkan pengalihan perangkat Plug and Play yang didukung), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/9d62d199cb34482f6c80f3dddb47bb0e.png)
15. Di jendela pop-up, pilih **Disabled** (Dinonaktifkan) dan klik **OK** (OKE), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/a76cf6ec239df644f6905eca7de3a2bd.png)
16. Mulai ulang CVM.


### Mengonfigurasi klien

1. Pada PC lokal, klik kanan <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> dan pilih **Run** (Jalankan) untuk membuka kotak dialog "Run" (Jalankan), seperti yang ditunjukkan pada gambar berikut:
2. Di kotak dialog "Run" (Jalankan), masukkan **gpedit.msc** (gpedit.msc) dan klik **OK** (OKE) untuk membuka "Local Group Policy Editor" (Editor Kebijakan Grup Lokal).
3. Di pohon navigasi sebelah kiri, pilih **Computer Configuration** (Konfigurasi Komputer) > **Administrative Templates** (Templat Administratif) > **Windows Components** (Komponen Windows) > **Remote Desktop Services** (Layanan Desktop Jarak Jauh) > **Remote Desktop Connection Client** (Klien Koneksi Desktop Jarak Jauh) > **RemoteFx USB Redirection ** (Pengalihan USB RemoteFx) dan klik dua kali **Allow RDP redirection of other supported RemoteFx USB devices** (Izinkan pengalihan RDP dari perangkat USB RemoteFx lain yang didukung), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/e65d8e43fcf5531c701d08e257daa20f.png)
4. Di jendela pop-up, pilih **Enabled** (Diaktifkan) dan atur izin akses pengalihan USB RemoteFx ke **Administrators and Users** (Administrator dan Pengguna), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/8fc197ed25e82d2f85ad32144b197a06.png)
5. Klik **OK** (OKE).
6. Mulai ulang PC lokal.

### Memverifikasi hasil konfigurasi

1. Di PC lokal Anda, masukkan perangkat USB, klik kanan <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> dan pilih **Run** (Jalankan) untuk membuka kotak dialog "Run" (Jalankan).
2. Pada kotak dialog "Run" (Jalankan), masukkan **mstsc** (mstsc) dan tekan Enter untuk membuka kotak dialog koneksi desktop jarak jauh, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/5478a5d46f6825cdfe604600a1391f4d.png)
3. Masukkan alamat IP publik server Windows di **Computer** (Komputer), lalu klik **Options** (Opsi).
4. Pada halaman tab **Local Resources** (Sumber Daya Lokal), klik **More** (Lainnya) di bawah "Local devices and resources" (Sumber daya dan perangkat lokal), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/f9c676bba12a01e029d727d9771faa38.png)
5. Di jendela pop-up, perluas **Other supported RemoteFx USB devices** (Perangkat USB RemoteFx lainnya yang didukung), pilih perangkat USB yang dimasukkan, dan klik **OK** (OKE).
![](https://main.qcloudimg.com/raw/681b010102c112bd99309c2c325d53c2.png)
6. Klik **Connect** (Hubungkan).
7. Di jendela pop-up **Windows Security** (Keamanan Windows), masukkan akun dan kata sandi admin instans, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/f87c5e1240ce07fe0ac28b48d88e61fd.png)
8. Klik **OK** (OKE) untuk login ke instans Windows.
Jika <img src="https://main.qcloudimg.com/raw/73fe2b3cfa740517e44e4596a222840a.png" style="margin: 0;"></img> muncul di halaman operasi instans Windows, artinya konfigurasi berhasil.
![](https://main.qcloudimg.com/raw/af5b70150d4032a29e1ded2db75858b6.png)


## Operasi yang Relevan

Windows RDP menyediakan koneksi yang dioptimalkan untuk perangkat USB standar. Perangkat seperti driver dan kamera dapat dipetakan secara langsung tanpa mengaktifkan fitur RemoteFx. Fitur pengalihan USB RemoteFX diperlukan untuk perangkat USB yang jarang digunakan. Tabel berikut mencantumkan metode pengalihan untuk perangkat USB ini.
![](https://main.qcloudimg.com/raw/715de06c08753eefe6e4ff5cc3bca270.png)

