## 1\. **LATAR BELAKANG**

Modul ini berlaku jika Anda menggunakan Identitas Pelanggan dan Manajemen Akses (CIAM) ("**Fitur**”). Modul ini tergabung dalam Perjanjian Keamanan dan Pemrosesan Data yang terdapat di (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347 )”). Istilah-istilah yang digunakan tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditentukan dalam DPSA. Jika terdapat perbedaan antara DPSA dan Modul ini, maka Modul inilah yang akan berlaku apabila terjadi inkonsistensi.


## 2\. **PEMROSESAN**

Kami akan memproses data berikut sehubungan dengan Fitur:

| **Informasi Pribadi**                                     | **Penggunaan**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data  Konfigurasi Manajemen Pengguna:** Atribut pengguna prasetel yang ditentukan oleh Anda (deskripsi, kewarganegaraan, posisi pengguna, hari lahir, gender, dan alamat); Kelompok pengguna (daftar kelompok pengguna, nama, keterangan, waktu pembuatan, dan daftar pengguna yang disertakan). | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/> Harap diperhatikan bahwa data ini terintegrasi dengan, disimpan, dan dicadangkan dalam TencentBD for MongoDB (MongoDB) dan fitur kami, serta terintegrasi dengan fitur TencentDB for Redis (Redis) kami. |
| **Data Manajemen Aplikasi:** <br><li>Aplikasi M2M: ikon, nama aplikasi, jenis aplikasi, industri, ID Klien, kunci kata sandi, deskripsi aplikasi, validitas token akses, domain keamanan, dan URI CORS yang dikonfigurasi secara spesifik;<br><li>Aplikasi Program Mini: unduhan aplikasi gaya, panduan konfigurasi, ikon, nama aplikasi, jenis aplikasi, industri, ID Klien, kunci kata sandi, deskripsi aplikasi, URI pengalihan, URI pengalihan keluar, validitas token akses, token penyegaran, klaim, konfigurasi proses pendaftaran dan masuk, URI konfigurasi spesifik CORS domain keamanan;<br><li>Aplikasi seluler: ikon, nama aplikasi, jenis aplikasi, industri, ID Klien, kunci kata sandi, deskripsi aplikasi, URI pengalihan, URI pengalihan keluar, validitas token akses, token penyegaran, klaim, proses pendaftaran, proses masuk, proses MFA, proses lupa kata sandi, proses lupa nama pengguna, manajemen protokol, URI konfigurasi spesifik CORS domain keamanan;<br><li>Aplikasi web dan aplikasi web: ikon, nama aplikasi, jenis aplikasi, industri, ID Klien, kunci kata sandi, deskripsi aplikasi, URI pengalihan, URI pengalihan keluar, validitas token akses, token penyegaran, klaim, proses pendaftaran, proses masuk, proses MFA, proses lupa kata sandi, proses lupa nama pengguna, manajemen protokol, URI konfigurasi spesifik CORS domain keamanan. | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.  <br/>Harap diperhatikan bahwa data ini terintegrasi dengan, disimpan, dan dicadangkan dalam fitur Cloud Object Storage (COS) dan MongoDB kami. |
| **Data Pengaturan Sinkronisasi Data:** Nama sumber data, ID sumber data, deskripsi, panduan konfigurasi, ID Klien, kunci kata sandi klien, token, URL pengguna, URL kelompok. | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap diperhatikan bahwa data ini terintegrasi dengan, disimpan, dan dicadangkan dalam fitur MongoDB kami. |
| **Data Manajemen Sertifikasi:** <br><li>Sumber autentikasi umum: ikon sumber autentikasi, nama sumber autentikasi, atribut sumber autentikasi, deskripsi sumber autentikasi, kebijakan kata sandi, panjang kode verifikasi SMS, masa berlaku kode verifikasi SMS, panjang kode verifikasi email, masa berlaku kode verifikasi email; <br><li>Sumber autentikasi sosial: ikon sumber autentikasi, nama sumber autentikasi, deskripsi sumber autentikasi, AppID, kunci kata sandi aplikasi, pemetaan atribut. | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap diperhatikan bahwa data ini terintegrasi dengan, disimpan, dan dicadangkan dalam fitur COS dan MongoDB kami. Jika Anda telah membeli layanan Short Message Service (SMS) dan Simple Email Service (SES) kami, data sumber autentikasi umum juga terintegrasi dengan fitur SMS dan SES. |
| **Data Personalisasi:** <br><li>Pengaturan nama domain: nama domain yang diatur dan diberikan oleh Anda (atau, jika perlu, nama domain standar yang diberikan oleh kami) ; <br><li>Pengaturan templat (pengaturan konfigurasi terkait opsi untuk menggunakan SMS dan/atau fitur SES): Templat SMS (server SMS, tanda tangan masuk SMS, ID templat SMS); Templat kotak surat (server email, ID templat kode verifikasi, ID templat kata sandi penarikan, ID templat nama pengguna penarikan) ; <br><li>Templat autentikasi nama asli (penyedia layanan autentikasi nama asli, kredensial keamanan pemanggil API (ID rahasia, kunci rahasia)). | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap diperhatikan bahwa data ini terintegrasi dengan, disimpan, dan dicadangkan dalam fitur MongoDB kami. Jika Anda telah membeli layanan SMS dan SES kami, data pengaturan templat juga diintegrasi dengan fitur SMS dan SES kami. |
| **Data Atribut Pengguna Internal:** waktu salah masuk, waktu penguncian, ID pengguna Alipay, alamat email, waktu pembaruan, zona waktu pengguna, lokasi geografis, waktu masuk terakhir, nomor ponsel, waktu pembuatan, grup pengguna, kumpulan pengguna, nama panggilan pengguna, ID pengguna, nama pengguna, Open ID WeChat, apakah Anda masuk untuk pertama kali, sumber pengguna, ID Wechatunion, status pengguna, Open ID QQ, ID QQunion, apakah Anda memiliki autentikasi nama asli, metode autentikasi nama asli, Nama, nomor ID, apakah merupakan akun utama atau bukan | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap diperhatikan bahwa data ini terintegrasi dengan, disimpan, dan dicadangkan dalam MongoDB dan fitur kami, serta terintegrasi dengan fitur Redis kami. Jika Anda telah membeli layanan SMS dan SES kami, nomor ponsel juga terintegrasi dengan fitur SMS kami, dan alamat email terintegrasi dengan fitur SES kami. |


## 3\. **WILAYAH LAYANAN**

Sebagaimana ditentukan dalam DPSA.


## 4\. **SUB-PROSESOR**

Sebagaimana ditentukan dalam DPSA.


## 5\. **RETENSI DATA**

Kami akan menyimpan data pribadi yang diproses sehubungan dengan Fitur sebagai berikut:

| **Informasi Pribadi**                                    | **Kebijakan Retensi**                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Data Konfigurasi Manajemen Pengguna Data Manajemen Aplikasi Data Pengaturan Sinkronisasi Data Data Manajemen Sertifikasi Data Personalisasi  Data Atribut Pengguna Internal | Kami menyimpan data tersebut hingga Anda menghapusnya secara manual. Atau, saat Anda menghapus akun Anda atau menghentikan penggunaan Fitur, maka kami akan menghapus data tersebut. |

Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.


## 6\. **PERSYARATAN KHUSUS**

Anda harus memastikan bahwa Fitur ini hanya digunakan oleh pengguna akhir yang setidaknya berusia minimum yang memungkinkan individu untuk menyetujui pemrosesan data pribadi. Persyaratan ini mungkin berbeda-beda, tergantung pada wilayah hukum tempat pengguna akhir berada.