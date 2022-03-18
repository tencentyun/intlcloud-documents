## Pengantar
Artikel ini menjelaskan cara menggunakan IIS untuk membuat situs FTP pada instans Tencent Cloud Virtual Machine (CVM) yang menjalankan Windows.

## Persyaratan Perangkat Lunak
Perangkat lunak berikut diperlukan untuk membuat layanan FTP:
 - OS: Windows Server 2012 
 - Server web: IIS 8.5

## Petunjuk
### Langkah 1: login ke CVM
- [Login ke CVM di Windows Menggunakan File RDP (Direkomendasikan)](http://intl.cloud.tencent.com/document/product/213/5435).
- [Login ke CVM Windows Menggunakan Desktop Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32498).

### Langkah 2: instal layanan FTP di IIS
1. Klik <img src="https://main.qcloudimg.com/raw/446c1e8cb7da2ce280d710c6a46b693d.png" style="margin:-3px 0px"> untuk membuka pengelola server. Jendela **Server Manager** (Pengelola Server) akan muncul.
2. Klik **Add Roles and Features** (Tambahkan Peran dan Fitur), seperti yang ditunjukkan pada gambar di bawah ini. Jendela **Guide to Adding Roles and Features** (Panduan untuk Menambahkan Peran dan Fitur) akan muncul.
![](https://main.qcloudimg.com/raw/1d941b3c877a420513e494971a834f37.png)
3. Klik **Next** (Selanjutnya). Halaman **Choose Installation Type** (Pilih Jenis Penginstalan) akan muncul.
4. Pilih **Role-based or Feature-based Installation** (Penginstalan Berbasis Peran atau Berbasis Fitur), dan klik **Next** (Selanjutnya). Halaman **Choose Target Server** (Pilih Server Target) akan muncul.
5. Jangan ubah pengaturan default, lalu klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar di bawah ini. Halaman **Choose Server Role** (Pilih Peran Server) akan muncul.
![](https://main.qcloudimg.com/raw/41f775ccbcd8e984b72bc096efa668d4.png)
6. Pilih **Web Server (IIS)** (Server Web (IIS)), lalu klik **Add Feature** (Tambahkan Fitur) di jendela yang ditampilkan, seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/f23fe1b8415c0f75c54309b652781aa4.png)
7. Klik **Next** (Selanjutnya) tiga kali. Halaman **Choose Role Service** (Pilih Layanan Peran) akan muncul.
8. Pilih **FTP Service** (Layanan FTP) dan **FTP Extension** (Ekstensi FTP), lalu klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/1fa84c69d96c16f2ea0f10e51b0607bb.png)
9. Klik **Install** (Instal) untuk mulai menginstal layanan FTP.
10. Setelah penginstalan selesai, klik **Close** (Tutup).
<span id="user"></span>
### Langkah 3: buat nama pengguna dan kata sandi FTP
> Langkah-langkah berikut membuat akun FTP dengan autentikasi kata sandi. Jika Anda hanya berencana untuk menggunakan akses anonim, lewati bagian ini.
>
1. Di jendela “Server Manager” (Pengelola Server), pilih **Tools** (Alat) -> **My Computer** (Komputer Saya) pada bilah navigasi di sudut kanan atas. Jendela **My Computer** (Komputer Saya) akan muncul.
2. Pilih **System Tools** (Alat Sistem) -> **Local Users and Groups** (Grup dan Pengguna Lokal) -> **Users** (Pengguna) di bilah sisi sebelah kiri.
3. Di sisi kanan antarmuka **Users** (Pengguna), klik kanan tempat kosong, dan pilih **New User** (Pengguna Baru), seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/60bad9ff725b8fe4386c2eed9c5ff63a.png)
4. Pada antarmuka “New User” (Pengguna Baru), atur nama pengguna dan kata sandi sesuai dengan petunjuk berikut. Klik **Create** (Buat), seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/1bc9cb2c2000361f6699c155e25d7630.png)
Parameter utama adalah sebagai berikut:
  - Nama pengguna: nama pengguna. Dalam hal ini, `ftpuser`.
  - Kata Sandi dan Konfirmasi kata sandi: kata sandi harus berisi huruf besar dan kecil serta angka. Dalam hal ini, `tf7295TFY`.
  - Hapus **User must change password in next login** (Pengguna harus mengubah kata sandi saat login berikutnya), dan pilih **Password never expired** (Kata sandi tidak pernah kedaluwarsa).
  Pilih opsi sesuai keinginan Anda. Untuk artikel ini, kami memilih **Password never expired** (Kata sandi tidak pernah kedaluwarsa).
5. Klik **Close** (Tutup) untuk menutup jendela “New User” (Pengguna Baru). Anda dapat melihat `ftpuser` pengguna yang baru dibuat dalam daftar.
	
### Langkah 4: atur izin folder bersama
> Dalam artikel ini, kami menggunakan `C:\test` sebagai folder bersama. Folder ini berisi file bernama `test.txt`. Buat folder bernama `test` pada bagian `C:\` dan file bernama `test.txt` pada bagian `C:\test`. Anda juga dapat menggunakan folder dan file lain.
>
1. Klik <img src="https://main.qcloudimg.com/raw/863967bab67b6cd83ce5f0924e1b19c8.png" style="margin:-3px 0px"> untuk membuka **This Computer** (Komputer Ini).
2. Perluas direktori pada bagian drive C. Pilih dan klik kanan `test`. Pilih **Properties** (Properti).
3. Di jendela **Properties** (Properti), pilih tab **Security** (Keamanan).
4. Pilih `Everyone` dan klik **Edit** (Edit), seperti yang ditunjukkan pada gambar di bawah ini:
Jika “Group or User Name” (Grup atau Nama Pengguna) tidak berisi `Everyone`, lihat [Menambahkan Semua Orang](#add) untuk menambahkan pengguna.
![](https://main.qcloudimg.com/raw/aec3d0557deef26ca3ff8005da86603f.png)
5. <span id="step5"></span>Pada antarmuka **Permissions** (Izin), atur izin untuk `Everyone` dan klik **OK** (OKE), seperti yang ditunjukkan pada gambar di bawah:
Dalam artikel ini, kami memberikan semua izin kepada `Everyone`.
![](https://main.qcloudimg.com/raw/ccdfda072d8a476a08773b7fcf979ec7.png)
6. Di jendela **Properties** (Properti), klik **OK** (OKE) untuk menyelesaikan pengaturan.


### Langkah 5: tambahkan situs FTP
1. Di jendela “Server Manager” (Pengelola Server), pilih **Tools** (Alat) -> **Internet Information Services (IIS) Manager** (Pengelola Layanan Informasi Internet (IIS)) di bilah navigasi di sudut kanan atas.
2. Di jendela **Internet Information Services (IIS) Manager** (Pengelola Layanan Informasi Internet (IIS)), perluas server Anda di bilah sisi kiri, klik kanan **Website** (Situs Web), dan pilih **Add FTP Site** (Tambahkan Situs FTP), seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/3d2c1a2708939cd5a8d7bf3bdf9aa1ff.png)
3. Pada antarmuka “Site Information” (Informasi Situs), masukkan informasi berikut. Klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/76761e667657b80bfdd2d2403d64ba3c.png)
    - **FTP site name** (Nama situs FTP): nama situs FTP Anda. Dalam artikel ini, `ftp` digunakan.
    - **Physical path** (Jalur fisik): jalur folder bersama. Pastikan Anda mengatur izin yang sesuai. Dalam artikel ini, `C:\test` digunakan.
4. Pada antarmuka **Binding and SSL Settings** (Pengaturan SSL dan Pengikatan), masukkan informasi berikut. Klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/355c3de0e19d7e1c161c51156bf0965f.png) 
Berikut ini adalah daftar parameter:
     - **Binding** (Pengikatan): opsi default untuk alamat IP adalah **None assigned** (Tidak ada yang ditetapkan); dan port default adalah port 21, nomor port FTP default. Anda dapat memilih nomor port Anda sendiri.
     - **SSL** (SSL): pilih opsi. Dalam artikel ini, **No SSL** (Tidak ada SSL) dipilih.
       - **No SSL** (Tidak ada SSL): tidak mendukung koneksi SSL.
       - **Allow SSL** (Izinkan SSL): izinkan server FTP terhubung dengan klien dengan atau tanpa SSL.
      - **Require SSL** (Memerlukan SSL): Enkripsi SSL diperlukan untuk komunikasi antara server FTP dan klien.
   Jika Anda memilih **Allow SSL** (Izinkan SSL) atau **Require SSL** (Memerlukan SSL), Anda dapat memilih sertifikat SSL yang ada di “SSL Certificates” (Sertifikat SSL), atau lihat [membuat sertifikat server](#ssl) untuk membuat sertifikat SSL.
5. Pada antarmuka “Identity Authentication and Authorization Information” (Autentikasi Identitas dan Informasi Otorisasi), masukkan informasi berikut. Klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/0f3be2c7ba449240cdac3f3c767e668c.png)
 - **Identity authentication** (Autentikasi identitas): pilih metode autentikasi identitas. Dalam artikel ini, **Basic** (Dasar) digunakan.
    - *Anonymous** (Anonim): mengizinkan pengguna mengakses konten tanpa autentikasi.
	 -. **Basic** (Dasar): mengharuskan pengguna untuk memberikan nama pengguna dan kata sandi yang valid sebelum mengizinkan mereka mengakses konten. Di bawah mode ini, kata sandi ditransfer tanpa enkripsi. Dengan demikian, pilih mode autentikasi ini hanya jika Anda mengetahui bahwa koneksi antara klien dan server FTP aman (misalnya, dengan menggunakan SSL).
 - **Authorize** (Izinkan): pilih opsi dari daftar drop-down izin akses. Dalam artikel ini, `ftpuser` digunakan.
	    - **All users** (Semua pengguna): semua pengguna, anonim atau teridentifikasi, dapat mengakses konten.
	    - **Anonymous users** (Pengguna anonim): pengguna anonim dapat mengakses konten.
	    - **Specified role or user group** (Peran atau grup pengguna tertentu): hanya peran atau anggota tertentu dari grup tertentu yang dapat mengakses konten. Jika Anda memilih opsi ini, Anda perlu menentukan peran atau grup pengguna.
	    - **Specified user** (Pengguna tertentu): hanya pengguna tertentu yang dapat mengakses konten. Jika Anda memilih opsi ini, Anda perlu menentukan nama pengguna.
 - **Permissions** (Izin): izin untuk konten yang dibagikan. Dalam artikel ini, **Read** (Baca) dan **Write** (Tulis) dipilih.
    - **Read** (Baca): mengizinkan pengguna yang berwenang membaca konten yang dibagikan.
    - **Write** (Tulis): mengizinkan pengguna yang berwenang untuk menulis ke dalam direktori.
7. Klik **Complete** (Selesai).

### Langkah 6: konfigurasikan grup keamanan dan firewall
1. Setelah situs FTP dibuat, tambahkan aturan masuk yang mengizinkan lalu lintas ke port FTP, yaitu 21 untuk tujuan artikel ini. Untuk informasi selengkapnya, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).
Jika Anda memilih port lain, Anda juga perlu menambahkan satu aturan masuk untuk setiap port yang dipilih.
2. (Opsional) Lihat [dokumentasi resmi Microsoft](https://docs.microsoft.com/en-us/previous-versions/orphan-topics/ws.11/hh831655(v=ws.11)) tentang cara mengonfigurasi firewall sehingga server FTP dapat menerima koneksi pasif dari firewall.

### Langkah 7: uji situs FTP
Anda dapat menggunakan klien FTP, browser, atau pengelola file untuk terhubung ke server FTP. Untuk tujuan artikel ini, pengelola file digunakan.
1. Konfigurasikan Internet Explorer
 - Jika Anda telah menambahkan aturan firewall yang sesuai, buka jendela Internet Explorer dan pilih **Tools** (Alat) -> **Internet Options** (Opsi Internet) -> **Advanced** (Lanjutan). Hapus **Use Passive FTP (used for compatibility between the firewall and DSL modem)** (Gunakan FTP Pasif (digunakan untuk kompatibilitas antara firewall dan modem DSL)) dan klik **OK** (OKE).
 - Jika Anda tidak menambahkan aturan firewall yang sesuai:
    1. Buka jendela Internet Explorer di **the FTP server** (server FTP) dan pilih **Tools** (Alat) -> **Internet Options** (Opsi Internet) -> **Advanced** (Lanjutan).  Hapus **Use Passive FTP (used for compatibility between the firewall and DSL modem)** (Gunakan FTP Pasif (digunakan untuk kompatibilitas antara firewall dan modem DSL)) dan klik **OK** (OKE).
    2. Buka jendela Internet Explorer di **client** (klien) dan pilih **Tools** (Alat) -> **Internet Options** (Opsi Internet) -> **Advanced** (Lanjutan). Hapus **Use Passive FTP (used for compatibility between the firewall and DSL modem)** (Gunakan FTP Pasif (digunakan untuk kompatibilitas antara firewall dan modem DSL)) dan klik **OK** (OKE).
2. Buka pengelola file di PC Anda dan ketik alamat berikut di kotak alamat browser dan tekan **Enter** (Enter), seperti yang ditunjukkan pada gambar berikut.
```
ftp://CVM_public_IP_address:21
```
![](https://main.qcloudimg.com/raw/d3d5a93170bb990f47ecd9f24c3e89ab.png)
3. Kotak dialog **Login identity** (Identitas login) akan muncul. Masukkan nama pengguna dan kata sandi yang dikonfigurasi di [Membuat nama pengguna dan kata sandi FTP](#user).
Dalam artikel ini, nama pengguna adalah `ftpuser`, dan kata sandinya adalah `tf7295TFY`.
4. Unggah dan unduh file setelah login.

## Lampiran
<span id="add"></span>
### Menambahkan Semua Orang
1. Di jendela **Properties** (Properti), pilih tab **Security** (Keamanan). Klik **Edit** (Edit), seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/f3f056e833fc63c97f23eef646ea8a10.png)
2. Pada kotak dialog **Properties** (Properti), klik **Add** (Tambahkan).
3. Pada kotak dialog “Choose User or Group” (Pilih Pengguna atau Grup), klik **Advanced** (Lanjutan).
4. Pada kotak dialog “Choose User or Group” (Pilih Pengguna atau Grup) yang ditampilkan, klik **Search Now** (Cari Sekarang).
5. Pada hasil pencarian, pilih `Everyone` dan klik **OK** (OKE), seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/32a9d44822ed4db0e82167d0cfb94835.png)
6. Pada kotak dialog “Choose User or Group” (Pilih Pengguna atau Grup), klik **OK** (OKE), seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/1245acedba4be051cf234423460a4345.png)
Login ke [Langkah 5](#step5) untuk mengatur izin pengguna `Everyone`.
<span id="ssl"></span>
### Membuat sertifikat server
1. Buka “Server Manager” (Pengelola Server) dan pilih **Tools** (Alat) -> **Internet Information Services (IIS) Manager** (Pengelola Layanan Informasi Internet (IIS)) pada bilah navigasi di sudut kanan atas.
2. Jendela **Internet Information Services (IIS) Manager** (Pengelola Layanan Informasi Internet (IIS)) akan muncul. Pilih server di bilah sisi kiri dan klik dua kali **Server Certificates** (Sertifikat Server) di antarmuka kanan, seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/8fc9f67a26475b891f4c50d9c670c08c.png)
3. Pilih **Create Self-Signature Certificate** (Buat Sertifikat Tanda Tangan Sendiri) di kolom operasi kanan.
4. Jendela **Create Self-Signature Certificate** (Buat Sertifikat Tanda Tangan Sendiri) muncul, masukkan nama sertifikat dan kelas penyimpanan, seperti yang ditunjukkan pada gambar di bawah ini:
Dalam dokumen ini, sertifikat SSL untuk penyimpanan pribadi dibuat.
![](https://main.qcloudimg.com/raw/0db81917b5b1e20af19d4d687d0d7fda.png)
5. Klik **OK** (OKE).
