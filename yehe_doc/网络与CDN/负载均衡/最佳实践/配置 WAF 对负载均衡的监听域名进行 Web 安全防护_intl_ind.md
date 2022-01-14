Ketika mengikat nama domain dengan pendengar CLB, [CLB Web Application Firewall (WAF)](https://intl.cloud.tencent.com/document/product/627/17470) dapat mendeteksi dan memblokir lalu lintas HTTP atau HTTPS yang melewati pendengar CLB.Dokumen ini memperkenalkan cara menggunakan CLB WAF untuk menerapkan perlindungan keamanan Web untuk nama domain yang ditambahkan ke CLB.

## Prasyarat
- Saat ini CLB WAF tersedia dalam versi beta. Jika Anda ingin mencobanya, silakan Ajukan Permohonan.
- Anda telah berhasil membuat pendengar HTTP atau HTTPS, dan nama domainnya dapat diakses.Untuk informasi selengkapnya, silakan lihat [Memulai CLB](https://intl.cloud.tencent.com/document/product/214/8975).
- Anda telah berhasil membeli layanan CLB WAF.Untuk informasi selengkapnya, silakan lihat [Panduan Pembelian](https://intl.cloud.tencent.com/document/product/627/11730).

## Batas
Saat ini, hanya instance IPv4 CLB yang mendukung perlindungan CLB WAF, fitur ini tidak tersedia untuk IPv6 dan NAT64.

## Petunjuk
<span id ="step1"></span>
### Langkah 1:Konfirmasi konfigurasi nama domain CLB
Dokumen ini menggunakan nama domain `www.example.com` sebagai contoh.
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb), klik **CLB Instance List** (Daftar Instance CLB) di bilah sisi kiri untuk masuk ke halaman **Instance Management** (Pengelolaan Instance).
2.Pilih wilayah instance, kemudian klik **Configure Listener** (Konfigurasi Pendengar) di sebelah kanan instance target.
3.Pilih tab **Listener Management** (Manajemen Pendengar), di bagian **HTTP/HTTPS Listener** (Pendengar HTTP/HTTPS), klik tanda **+** di sebelah kiri pendengar target untuk melihat detail nama domain.
![](https://main.qcloudimg.com/raw/1d546d69bc1d88faf15ef7acc9270468.png)
4.Periksa konfigurasi nama domain CLB agar sesuai dengan konfigurasi berikut:ID instance CLB: `lb-f8lm****`; nama pendengar: `http-test`; nama domain: `www.example.com`; status perlindungan nama domain:**Not Enabled** (Tidak Aktif) (ID, nama, dan nama domain akan menyesuaikan dengan keadaan yang sebenarnya).

### Langkah 2:Tambahkan nama domain di konsol WAF dan ikat nama domain tersebut ke instance CLB
Untuk menerapkan perlindungan ke nama domain dengan layanan CLB WAF, Anda perlu menambahkan nama domain pendengar CLB di WAF dan mengikatnya dengan pendengar CLB.
1.Masuk ke [Konsol WAF](https://console.cloud.tencent.com/guanjia/waf/config), kemudian pilih **Web Application Firewall** -> **Defense Settings** (Firewall Aplikasi Web -> Pengaturan Pertahanan) di bilah sisi kiri.
2.Pilih tab **CLB**.
3.Klik **Add Domains** (Tambahkan Domain).
![](https://main.qcloudimg.com/raw/5dc4d9c0363a2fe2713f157606efce19.png)
4.Masukkan nama domain, lalu klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/fadb7336503e5ee808fe8a02d9b12005.png)
5.Pilih wilayah CLB Anda, kemudian nama domain yang ada di <a href="#step1">"Langkah 1:Konfirmasi konfigurasi nama domain CLB"</a>, lalu klik **Select a Listener** (Pilih Pendengar).
![](https://main.qcloudimg.com/raw/4b632c6769bbbe105027e8bdf0b3ba1a.png)
6.Di jendela pop-up, pilih pendengar CLB yang ada di <a href="#step1">"Langkah 1:Konfirmasi konfigurasi nama domain CLB"</a>, lalu klik **OK**.
![](https://main.qcloudimg.com/raw/2793320edb9a79b0c46e4ea4e92e38f6.png)
7.Klik **Finish** (Selesai) pada langkah **Select a Listener** (Pilih Pendengar) untuk menyelesaikan proses mengikat nama domain dengan pendengar CLB di WAF.
8.Kembalilah ke halaman **Domain List** (Daftar Domain), dan periksa nama domain, wilayah, ID instance CLB ikatan, pendengar, dan informasi lainnya.

### Langkah 3:Verifikasi hasilnya
1.Ikuti petunjuk di <a href="#step1">"Langkah 1:Konfirmasi konfigurasi nama domain CLB"</a> untuk memeriksa nama domain.Perlindungan nama domain akan berfungsi apabila perlindungan nama domainnya **Enabled** (Diaktifkan) dan mode lalu lintasnya adalah **Mirror** (Cermin).
-  Apabila Anda belum mengonfigurasi resolusi DNS untuk nama domain Anda, silakan lihat [Langkah 2.Melakukan Pengujian Lokal](https://intl.cloud.tencent.com/document/product/627/35652) untuk memastikan bahwa perlindungan WAF telah diaktifkan.
- Apabila Anda sudah mengonfigurasi resolusi DNS untuk nama domain Anda, silakan ikuti petunjuk di bawah ini untuk memastikan bahwa perlindungan WAF telah diaktifkan.
1.Buka `http://www.example.com/?test=alert(123)` lewat peramban.
2.Masuk ke [Konsol WAF](https://console.cloud.tencent.com/guanjia/waf/config), kemudian pilih **Log Services** -> **Attack Log** (Layanan Log -> Log Serangan) di bilah sisi kiri.
3.Pilih tab **Log Search** (Pencarian Log), pilih nama domain yang telah diberi perlindungan `www.example.com`, lalu klik **Search** (Cari).Perlindungan WAF untuk nama domain yang dikonfigurasi di CLB akan efektif apabila terdapat log **XSS Attack** (Serangan XSS) di daftar log.

