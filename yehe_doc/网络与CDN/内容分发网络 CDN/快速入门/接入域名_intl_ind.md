<style>
table th:nth-of-type(1) { width:18%; }
table th:nth-of-type(2){ width:82%; }
</style>

Setelah mengaktifkan CDN, Anda dapat masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn) dan pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri.Klik **Create a Distribution** (Buat Distribusi) untuk menambahkan nama domain akselerasi.Setelah nama domain ditambahkan, konfigurasinya akan disebarkan ke simpul cache CDN di seluruh jaringan tanpa memengaruhi bisnis Anda saat ini secara langsung.Untuk mengaktifkan akselerasi, Anda harus mengonfigurasi rekaman CNAME.Untuk mendapatkan petunjuk khusus, silakan baca [Konfigurasi CNAME](https://intl.cloud.tencent.com/document/product/228/3121).



## Membuat Distribusi
Klik **Domain Management** (Pengelolaan Domain) di bilah samping kiri lalu klik **Create a Distribution** (Buat Distribusi).
![](https://main.qcloudimg.com/raw/020628a1fba4d8529bf3b5be7f459170.png)

Halaman pembuatan distribusi berupa tiga bagian:

- Konfigurasi domain
- Konfigurasi asal
- Konfigurasi layanan

Berdasarkan konfigurasi nama domain dan server asal yang dipilih, CDN akan menyarankan konfigurasi cache, yang dapat dikirimkan tanpa modifikasi.

### Bagian 1:Konfigurasi domain
Masukkan nama domain bisnis Anda di kolom domain dan pilih jenis proyek, wilayah, dan layanan:
<img src="https://main.qcloudimg.com/raw/6ec038f7f063b01cc1d68ecbfe4cb5c8.png" style="height:280px"/>

**Configuration description:** (Deskripsi konfigurasi.)

| Konfigurasi | Deskripsi                                                     |
| -------- | ------------------------------------------------------------ |
| Domain     | 1.Nama domain dapat memuat hingga 50 karakter.<br/>2.Nama domain harus sudah mendapatkan pemberkasan ICP dari MIIT.<br/>3.Nama subdomain dalam format `a.test.com` atau `a.b.test.com` dan nama domain kartubebas dalam format `*.test.com` atau `*.a.test.com` didukung. <br/>4.Jika nama domain berupa domain kartubebas, yang baru terkoneksi untuk pertama kalinya, atau sudah terkoneksi oleh pengguna lain, Anda harus menyelesaikan [verifikasi kepemilikan nama domain](#m1).<br/><br/><strong>Catatan: </strong><br/>1.Setelah nama domain kartubebas terhubung, nama subdomain dan nama domain kartubebas level kedua tidak dapat dihubungkan ke akun lain. <br/>2.Nama domain dalam format `*.test.com` dan `*.a.test.com` tidak dapat dikonfigurasi secara bersamaan.</strong><br/>3.Nama domain yang berupa karakter Cina atau karakter Cina bebas tidak didukung. |
| Proyek | Proyek adalah serangkaian sumber daya yang sama-sama dimiliki oleh semua produk Tencent Cloud.Anda dapat mengelolanya di [Manajemen Proyek](https://console.cloud.tencent.com/project) page. |
| Wilayah | Tiongkok daratan: permintaan akses dari pengguna global akan dijadwalkan ke simpul cache di Tiongkok daratan untuk keperluan akselerasi. <br/>Di luar Tiongkok daratan: permintaan akses dari pengguna global akan dijadwalkan ke simpul cache di luar Tiongkok daratan untuk keperluan akselerasi. <br/>Global: permintaan akses dari pengguna global akan dijadwalkan ke simpul optimum terdekat untuk keperluan akselerasi. <br/><br/><strong>Catatan: </strong><br/>Layanan akselerasi di dalam dan di luar Tiongkok daratan dikenai tagihan secara terpisah.Untuk informasi selengkapnya tentang kebijakan penagihan, silakan baca [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/228/2949). |
| Jenis layanan | CDN mengoptimalkan performa akselerasi berdasarkan jenis layanan. <br/>Untuk mendapatkan hasil akselerasi terbaik, kami sarankan memilih jenis layanan yang mirip dengan jenis layanan bisnis aktual Anda. <br/><br/>Akselerasi statis: cocok untuk konteks akselerasi sumber daya skala kecil, seperti ecommerce, situs web, dan gambar game.<br/>Akselerasi unduhan: cocok untuk konteks unduhan, seperti penginstalan game, unduhan file audio/video sumber, dan distribusi firmware telepon seluler. <br/>Akselerasi streaming VOD: cocok untuk konteks pendidikan online dan VOD. |
| Akses IPv6<br>| Akses IPv6 dinonaktifkan secara default.Jika diaktifkan, simpul CDN dapat diakses lewat protokol IPv6.Setelah menambahkan nama domain, Anda dapat menonaktifkan dan mengaktifkannya sesuai kebutuhan.<br/><strong><br/>Catatan: </strong><br>• Beberapa platform sedang ditingkatkan, akses IPv6 saat ini tidak didukung.Jangan ketinggalan peluncuran resmi.<br/>• Akses IPv6 hanya tersedia di Tiongkok daratan.Nama domain akselerasi global, jika akses IPv6 diaktifkan, hanya akan aktif di Tiongkok daratan.Adapun di luar Tiongkok daratan, nama domain dengan akselerasi tidak dapat diaktifkan.|
| Tanda | Hingga 50 tanda dapat ditambahkan.<br/>Hanya tanda yang sudah ada yang didukung.<br/>Tombol dan nilai tanda bersifat wajib ketika Anda menambahkan sebuah tanda.Anda dapat menambahkan atau memodifikasi tanda di [Daftar Tanda](https://console.cloud.tencent.com/tag/taglist). |

### Bagian 2:Konfigurasi asal

Mengonfigurasi informasi server asal bisnis.Jika simpul CDN tidak memiliki cache sumber daya, simpul tersebut akan menarik sumber daya dari server asal dan meng-cache-nya.
![](https://main.qcloudimg.com/raw/947c24efc846a11b25dca0f8ea552422.png)

**Configuration description:** (Deskripsi konfigurasi.)

| Konfigurasi | Deskripsi                                                     |
| -------- | ------------------------------------------------------------ |
| Jenis asal | Eksternal: pilih ini jika Anda sudah memiliki server bisnis sendiri. (yaitu, server asal). <br/><a href = "https://intl.cloud.tencent.com/product/cos">COS origin</a>: jika sumber daya disimpan di COS, bucket dapat dipilih langsung sebagai server asal. |
| Alamat asal | Eksternal: <br/>1.Beberapa IP dapat dikonfigurasi sebagai server asal, yang akan dipotong selama tarik-asal. <br/>2.Anda dapat mengonfigurasi port (0 - 65535) dan bobot (1 - 100) dalam format `origin server:port:weight`.Port dapat dibuang sehingga formatnya menjadi `origin server::weight`.Protokol HTTPS saat ini hanya mendukung port 443. <br/>3.Anda dapat mengonfigurasi nama domain sebagai server asal, yang harus berbeda dengan nama domain akselerasi bisnis. |
| Protokol tarik-asal | Protokol ini dapat dipilih berdasarkan protokol yang didukung oleh server asal: <br/>HTTP:Permintaan akses HTTP/HTTPS menggunakan tarik-asal HTTP. <br/>HTTPS:Permintaan akses HTTP/HTTPS menggunakan tarik-asal HTTPS (server asal harus mendukung akses HTTPS). <br/>Ikuti protokol:Permintaan akses HTTP menggunakan tarik-asal HTTP, sedangkan permintaan akses HTTPS menggunakan tarik-asal HTTPS (server asal harus mendukung akses HTTPS). |
| Domain asal | Ini merujuk ke nama domain yang diakses di server asal oleh simpul CDN selama tarik-asal. <br/>Jika terhubung, nama subdomain akan sama dengan nama domain akselerasi secara default dan dapat disesuaikan. <br/>Jika terhubung, nama domain kartubebas akan menjadi nama subdomain akses aktual secara default dan dapat disesuaikan. |

### Bagian 3:Konfigurasi layanan
Mengonfigurasi layanan akselerasi simpul:
![](https://main.qcloudimg.com/raw/6e918f4e91d4c5249172589475f292a1.png)

**Configuration description:** (Deskripsi konfigurasi.)

| Konfigurasi | Deskripsi                                                     |
| :------- | :----------------------------------------------------------- |
| Konfigurasi dasar | Sebuah simpul meng-cache sumber daya dengan mengikuti pemetaan `Key-Value`, dengan `Key` adalah URL sumber daya.Jika "Ignore Query String" (Abaikan String Kueri) diaktifkan, parameter setelah "?" di URL akan diabaikan.Jika tidak, `Key` akan berupa URL sumber daya lengkap.Secara default, fitur ini diaktifkan untuk akselerasi unduhan dan streaming VOD, tetapi bukan untuk akselerasi statis. |
| Aktifkan Range GETs | Ini menentukan apakah akan memproses permintaan sebagian selama tarik-asal.Range GETs hanya dapat diaktifkan jika server asal mendukungnya.Secara default, fitur ini diaktifkan untuk akselerasi server asal COS dan streaming VOD. |
| Konfigurasi cache | Validitas cache simpulUntuk akselerasi statis, validitas cache dari semua file mengikuti server asal secara default.Untuk akselerasi unduhan dan streaming VOD, validitas cache dari semua file adalah 30 hari.Validitas cache yang terkonfigurasi mungkin merupakan waktu yang paling lama, validitas cache aktual berkaitan dengan sumber daya di simpul. |

## Menyelesaikan Konfigurasi

Klik **Submit** (Kirim) untuk menambahkan nama domain lalu tunggu sampai konfigurasi nama domain tersebar ke seluruh jaringan.Waktu yang dibutuhkan kira-kira 5 hingga 10 menit.
![](https://main.qcloudimg.com/raw/d5bcb556ac1b89946ec15642d3249676.png)

## Operasi Berikutnya
Ketika distribusinya selesai, CDN akan mengalokasikan alamat CNAME yang sesuai untuk Anda.Anda harus mengonfigurasi CNAME agar dapat menggunakan layanan CDN.Untuk mendapatkan petunjuk lengkap, silakan lihat [Konfigurasi CNAME](https://intl.cloud.tencent.com/document/product/228/3121).

[](id:m1)
## Memverifikasi Kepemilikan Nama Domain
Jika nama domain berupa domain kartubebas, yang baru terkoneksi untuk pertama kalinya, atau sudah terkoneksi oleh pengguna lain, Anda harus memverifikasi kepemilikan nama domain.Nama domain dapat dihubungkan atau diambil setelah lulus verifikasi.
Verifikasi kepemilikan nama domain dilakukan dengan memverifikasi informasi DNS lewat langkah-langkah berikut:
1.Klik **Verification Method** (Metode Verifikasi) guna mendapatkan informasi rekaman resolusi untuk ditambahkan sebagai syarat verifikasi DNS.Jangan tutup halaman ini sebelum verifikasi selesai.
![img](https://main.qcloudimg.com/raw/c05c0d869a71dbe68092ccee632c2d1a.png)
2.Buka penyedia layanan DNS Anda, tambahkan rekaman TXT dan masukkan `_cdnauth` sebagai rekaman host dan nilai rekaman yang dihasilkan secara acak di halaman "Verification Method" (Metode Verifikasi) sebagai nilai rekamannya.
3.Tunggu resolusi TXT hingga aktif lalu klik **Verify** (Verifikasikan).Jika verifikasi gagal, tunggu rekaman DNS menjadi aktif agar dapat mencoba lagi dan periksa apakah rekaman TXT sudah benar.
