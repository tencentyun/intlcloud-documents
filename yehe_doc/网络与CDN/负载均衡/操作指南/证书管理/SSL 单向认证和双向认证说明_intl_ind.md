Secure Sockets Layer (SSL) adalah protokol keamanan yang dirancang untuk memastikan keamanan dan integritas data dalam komunikasi Internet.Dokumen ini memperkenalkan autentikasi satu arah dan autentikasi bersama SSL.
>?Ketika membuat pendengar SSL TCP atau pendengar HTTPS untuk instance CLB, Anda dapat memilih autentikasi satu arah atau autentikasi bersama sebagai metode parsing SSL.Untuk informasi selengkapnya, lihat [Mengonfigurasi Pendengar SSL TCP](https://intl.cloud.tencent.com/document/product/214/32519) dan [Mengonfigurasi Pendengar HTTPS](https://intl.cloud.tencent.com/document/product/214/32516).

## Perbedaan Antara Autentikasi Satu Arah dengan Autentikasi Bersama SSL
- Untuk [autentikasi satu arah SSL](#dxrz), sertifikat hanya diperlukan di server tetapi klien tidak memerlukannya; sedangkan [autentikasi bersama SSL](#sxrz), sertifikat diperlukan baik di server maupun klien.
- Dibandingkan autentikasi bersama SSL, autentikasi satu arah tidak memerlukan verifikasi sertifikat klien dan negosiasi skema enkripsi di server.Meskipun skema enkripsi yang dikirimkan oleh server ke klien tidak dienkripsi, keamanan autentikasi SSL akan tetap terjaga.
- Aplikasi web umumnya memiliki banyak pengguna dan verifikasi identitas pengguna tidak diperlukan pada lapisan komunikasi sehingga autentikasi satu arah SSL dapat digunakan.Namun, klien yang ingin terhubung ke aplikasi keuangan mungkin memerlukan verifikasi identitas sehingga mereka harus menggunakan autentikasi bersama SSL.

<span id="dxrz"></span>
## Autentikasi Satu Arah SSL
Dalam autentikasi satu arah SSL, hanya identitas server yang perlu diverifikasi, identitas klien tidak perlu.Proses autentikasi satu arah SSL diperlihatkan dalam gambar di bawah ini:
<img src="https://main.qcloudimg.com/raw/000d0a44b1bad4b015cfc81ad6e17441.png" width="70%">
1.Klien membuat permintaan koneksi HTTPS ke server beserta versi protokol SSL yang didukung, algoritme enkripsi, nomor acak yang dihasilkan, dan informasi lainnya.
2.Server akan mengembalikan versi protokol SSL, algoritme enkripsi, nomor acak yang dihasilkan, sertifikat server (server.crt), dan informasi lainnya kepada klien.
3.Klien akan memverifikasi validitas sertifikat (server.crt) terkait faktor di bawah ini dan mengambil kunci publik server dari sertifikat.
- Apakah sertifikat telah kedaluwarsa.
- Apakah sertifikat dibatalkan.
- Apakah sertifikat tepercaya
- Apakah nama domain yang diminta sama dengan nama domain dalam sertifikat yang diterima.
4.Setelah sertifikat diverifikasi, klien akan membuat nomor acak (K kunci; yang digunakan sebagai kunci enkripsi simetri untuk komunikasi), mengenkripsinya menggunakan kunci publik yang diperoleh dari sertifikat server, lalu mengirimkannya ke server.
5.Setelah menerima informasi yang dienkripsi, server akan menggunakan kunci privatnya (server.key) untuk mendekripsi guna mendapatkan kunci enkripsi simetri (K kunci).
Kunci enkripsi simetri (K kunci) akan digunakan oleh server dan klien untuk berkomunikasi guna menjamin keamanan informasi.

<span id="sxrz"></span>
## Autentikasi Bersama SSL
Dalam autentikasi bersama SSL, identitas server maupun identitas klien perlu diverifikasi.Proses autentikasi bersama SSL diperlihatkan dalam gambar di bawah ini:
<img src="https://main.qcloudimg.com/raw/93c4567863719926db8737aa345e008c.png" width="70%">
1.Klien membuat permintaan koneksi HTTPS ke server beserta versi protokol SSL yang didukung, algoritme enkripsi, nomor acak yang dihasilkan, dan informasi lainnya.
2.Server akan mengembalikan versi protokol SSL, algoritme enkripsi, nomor acak yang dihasilkan, sertifikat server (server.crt), dan informasi lainnya kepada klien.
3.Klien akan memverifikasi validitas sertifikat (server.crt) terkait faktor di bawah ini dan mengambil kunci publik server dari sertifikat.
- Apakah sertifikat telah kedaluwarsa.
- Apakah sertifikat dibatalkan.
- Apakah sertifikat tepercaya
- Apakah nama domain yang diminta sama dengan nama domain dalam sertifikat yang diterima.
4.Server akan meminta klien untuk mengirimkan sertifikat klien (client.crt), dan klien akan melakukan permintaan tersebut.
5.Server memverifikasi sertifikat klien (client.crt).Setelah diverifikasi, server akan menggunakan sertifikat root untuk mendekripsi sertifikat klien dan mendapatkan kunci publik klien.
6.Klien akan mengirimkan skema enkripsi simetri yang didukung ke server.
7.Server akan memilih skema enkripsi dengan tingkat enkripsi tertinggi dari skema yang dikirimkan oleh klien, menggunakan kunci publik klien untuk mengenkripsi, lalu mengembalikannya kepada klien.
8.Klien akan menggunakan kunci privatnya (client.key) untuk mendekripsi skema enkripsi dan membuat nomor acak (K kunci; yang digunakan sebagai kunci enkripsi simetri untuk komunikasi), mengenkripsinya menggunakan kunci publik yang diperoleh dari sertifikat server, lalu mengirimkannya ke server.
9.Setelah menerima informasi yang dienkripsi, server akan menggunakan kunci privatnya (server.key) untuk mendekripsi guna mendapatkan kunci enkripsi simetri (K kunci).
Kunci enkripsi simetri (K kunci) akan digunakan oleh server dan klien untuk berkomunikasi guna menjamin keamanan informasi.

## Dokumen yang Relevan
[Persyaratan Sertifikat dan Konversi Format Sertifikat](https://intl.cloud.tencent.com/document/product/214/6155)