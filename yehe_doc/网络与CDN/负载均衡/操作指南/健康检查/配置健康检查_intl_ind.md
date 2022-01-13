Ketika mengonfigurasi pendengar, Anda dapat mengaktifkan pemeriksaan kesehatan untuk mendapatkan informasi ketersediaan tentang server asli.Untuk informasi selengkapnya tentang pemeriksaan kesehatan, lihat [Gambaran Umum Pemeriksaan Kesehatan](https://intl.cloud.tencent.com/document/product/214/6097).

<span id="postreq"></span>
## Prasyarat
1.Buat instance CLB.Untuk informasi selengkapnya, silakan lihat [Membuat Instance CLB](https://intl.cloud.tencent.com/document/product/214/6149).
2.Buat pendengar CLB
- Untuk membuat pendengar TCP, lihat informasi selengkapnya di [Mengonfigurasi Pendengar TCP](https://intl.cloud.tencent.com/document/product/214/32517).
- Untuk membuat pendengar UDP, lihat informasi selengkapnya di [Mengonfigurasi Pendengar UDP](https://intl.cloud.tencent.com/document/product/214/32518).
- Untuk membuat pendengar TCP SSL, lihat informasi selengkapnya di [Mengonfigurasi Pendengar TCP SSL](https://intl.cloud.tencent.com/document/product/214/32519).
- Untuk membuat pendengar HTTP, lihat informasi selengkapnya di [Mengonfigurasi Pendengar HTTP](https://intl.cloud.tencent.com/document/product/214/32515).
- Untuk membuat pendengar HTTPS, lihat informasi selengkapnya di [Mengonfigurasi Pendengar HTTPS](https://intl.cloud.tencent.com/document/product/214/32516).

## Pendengar TCP
Pendengar TCP lapisan 4 mendukung tiga tipe pemeriksaan kesehatan, antara lain pemeriksaan kesehatan TCP lapisan 4, pemeriksaan kesehatan HTTP lapisan 7, dan pemeriksaan protokol khusus.
- Pemeriksaan kesehatan TCP dilakukan dengan paket SYN, yaitu handshake tiga arah TCP yang dilakukan untuk mendapatkan informasi status instance CVM backend.
- Pemeriksaan kesehatan HTTP dilakukan dengan mengirimkan permintaan HTTP untuk mendapatkan informasi status instance CVM backend.
- Pemeriksaan kesehatan protokol khusus dilakukan dengan menyesuaikan konten input dan output protokol lapisan aplikasi untuk mendapatkan informasi status instance CVM backend.

### Mengonfigurasi pemeriksaan kesehatan TCP
1.Konfigurasi pendengar menggunakan langkah **Health Check** (Pemeriksaan Kesehatan) sesuai petunjuk dalam [Prasyarat](#postreq).
2.Dalam langkah **Health Check** (Pemeriksaan Kesehatan), pilih **TCP** sebagai protokol.
<table>
<tr>
<th>Parameter</th><th>Deskripsi</th>
</tr>
<tr>
<td>Pemeriksaan kesehatan</td><td>Dapat diaktifkan atau dinonaktifkan.Sebaiknya aktifkan pemeriksaan kesehatan agar dapat melakukan pemeriksaan otomatis terhadap instance CVM backend dan menghapus port abnormal.</td>
</tr>
<tr>
<td>Protokol</td><td>Pemeriksaan kesehatan TCP akan dilakukan jika <b>TCP</b> dipilih.</td>
</tr>
<tr>
<td>Port</td><td>Bersifat opsional.Sebaiknya jangan tentukan port, kecuali Anda perlu memeriksa port tertentu.Port server asli akan diperiksa jika port tidak ditentukan di sini.</td>
</tr>
<tr>
<td>Tampilkan opsi lanjutan</td><td>Untuk informasi selengkapnya, lihat <a href="#advance">Opsi Lanjutan</a>.</td>
</tr>
</table>

### Mengonfigurasi pemeriksaan kesehatan HTTP
1.Konfigurasi pendengar menggunakan langkah **Health Check** (Pemeriksaan Kesehatan) sesuai petunjuk dalam [Prasyarat](#postreq).
2.Dalam langkah **Health Check** (Pemeriksaan Kesehatan), pilih **HTTP** sebagai protokol.
<table>
<tr>
<th>Parameter</th><th>Deskripsi</th>
</tr>
<tr>
<td>Pemeriksaan kesehatan</td><td>Dapat diaktifkan atau dinonaktifkan.Sebaiknya aktifkan pemeriksaan kesehatan agar dapat melakukan pemeriksaan otomatis terhadap instance CVM backend dan menghapus port abnormal.</td>
</tr>
<tr>
<td>Protokol</td><td>Pemeriksaan kesehatan HTTP akan dilakukan jika <b>HTTP</b> dipilih.</td>
</tr>
<tr>
<td>Port</td><td>Bersifat opsional.Sebaiknya jangan tentukan port, kecuali Anda perlu memeriksa port tertentu.Port server asli akan diperiksa jika port tidak ditentukan di sini.</td>
</tr>
<tr>
<td>Domain pemeriksaan</td><td>Persyaratan terkait nama domain untuk pemeriksaan kesehatan:
<ul>
<li>Panjang: 1 hingga 80 karakter.</li>
<li>Merupakan nama domain penerusan secara default.</li>
<li>Tidak mendukung ekspresi reguler.Jika nama domain penerusan Anda menggunakan kartubebas, Anda perlu menetapkan nama domain tetap (non-reguler) sebagai nama domain pemeriksaan kesehatan.</li>
<li>Karakter yang didukung: huruf kecil (a hingga z), digit (0 hingga 9), poin desimal (,), dan tanda hubung (-).</li>
</ul></td>
</tr>
<tr>
<td>Jalur</td><td>Persyaratan terkait jalur pemeriksaan kesehatan:
<ul>
<li>Panjang: 1 hingga 200 karakter.</li>
<li>`/` adalah nilai default dan harus digunakan sebagai karakter pertama.</li>
<li>Tidak mendukung ekspresi reguler.Sebaiknya tentukan URL tetap (halaman web statis) untuk pemeriksaan kesehatan.</li>
<li>Karakter yang didukung: huruf kecil (a hingga z), huruf kapital (A hingga Z), digit (0 hingga 9), poin desimal (,), tanda hubung (-), garis bawah (_), garis miring (/), tanda sama dengan (=), dan tanda tanya (?).</li>
</ul></td>
</tr>
<tr>
<td>Metode permintaan HTTP</td><td>Metode permintaan HTTP pada pemeriksaan kesehatan.Opsi:GET (metode default) dan HEAD.
<ul>
<li>Jika HEAD dipilih, server hanya akan mengembalikan informasi header HTTP, yang dapat mengurangi overhead backend dan meningkatkan efisiensi permintaan.Server asli harus mendukung HEAD.</li>
<li>Jika GET dipilih, server asli harus mendukung GET.</li>
</ul></td>
</tr>
<tr>
<td>Versi HTTP</td><td>Versi HTTP server asli.
<ul>
<li>Jika server asli mendukung versi HTTP 1.0, bidang host permintaan tidak akan memerlukan autentikasi, artinya, domain pemeriksaan tidak perlu dikonfigurasi.</li>
<li>Jika server asli mendukung versi HTTP 1.1, bidang host permintaan memerlukan autentikasi, artinya, domain pemeriksaan perlu dikonfigurasi atau Anda akan mendapatkan kode kesalahan 404.</li>
</ul></td>
</tr>
<tr>
<td>Kode status normal</td><td>Jika kode status merupakan kode yang telah dipilih, server asli akan dianggap aktif (sehat).Opsi: http_1xx, http_2xx, http_3xx, http_4xx, dan http_5xx.Anda dapat memilih beberapa opsi.</td>
</tr>
<tr>
<td>Tampilkan opsi lanjutan</td><td>Untuk informasi selengkapnya, lihat <a href="#advance">Opsi Lanjutan</a>.</td>
</tr>
</table>

### Mengonfigurasi pemeriksaan kesehatan protokol khusus
1.Konfigurasi pendengar menggunakan langkah **Health Check** (Pemeriksaan Kesehatan) sesuai petunjuk dalam [Prasyarat](#postreq).
2.Dalam langkah **Health Check** (Pemeriksaan Kesehatan), pilih **HTTP** sebagai protokol.
<table>
<tr>
<th>Parameter</th><th>Deskripsi</th>
</tr>
<tr>
<td>Pemeriksaan kesehatan</td><td>Dapat diaktifkan atau dinonaktifkan.Sebaiknya aktifkan pemeriksaan kesehatan agar dapat melakukan pemeriksaan otomatis terhadap instance CVM backend dan menghapus port abnormal.</td>
</tr>
<tr>
<td>Protokol</td><td>Pemeriksaan kesehatan protokol khusus akan dilakukan jika <b>Custom Protocol</b> (Protokol Khusus) dipilih.</td>
</tr>
<tr>
<td>Port</td><td>Bersifat opsional.Sebaiknya jangan tentukan port, kecuali Anda perlu memeriksa port tertentu.Port server asli akan diperiksa jika port tidak ditentukan di sini.</td>
</tr>
<tr>
<td>Format input</td><td>Mendukung teks dan string heksadesimal.
<ul>
<li>Jika Teks dipilih, teks tersebut akan dikonversi menjadi string biner untuk mengirimkan permintaan dan membandingkan hasil yang dikembalikan.</li>
<li>Jika Heksadesimal dipilih, string heksadesimal akan dikonversi menjadi string biner untuk mengirimkan permintaan dan membandingkan hasil yang dikembalikan.</li>
</ul></td>
</tr>
<tr>
<td>Permintaan</td><td>Konten permintaan pemeriksaan kesehatan khusus.</td>
</tr>
<tr>
<td>Hasil pengembalian</td><td>Ketika menyesuaikan permintaan pemeriksaan kesehatan, Anda perlu memasukkan hasil pemeriksaan kesehatan yang dikembalikan.</td>
</tr>
<tr>
<td>Tampilkan opsi lanjutan</td><td>Untuk informasi selengkapnya, lihat <a href="#advance">Opsi Lanjutan</a>.</td>
</tr>
</table>


## Pendengar UDP
Pendengar UDP mendukung pemeriksaan kesehatan UDP, yang dapat dilakukan dengan memeriksa port dan menjalankan perintah Ping.

### Mengonfigurasi pemeriksaan kesehatan UDP - pemeriksaan port
1.Konfigurasi pendengar menggunakan langkah **Health Check** (Pemeriksaan Kesehatan) sesuai petunjuk dalam [Prasyarat](#postreq).
2.Dalam langkah **Health Check** (Pemeriksaan Kesehatan), pilih **Port** sebagai protokol.
<table>
<tr>
<th>Parameter</th><th>Deskripsi</th>
</tr>
<tr>
<td>Pemeriksaan kesehatan</td><td>Dapat diaktifkan atau dinonaktifkan.Sebaiknya aktifkan pemeriksaan kesehatan agar dapat melakukan pemeriksaan otomatis terhadap instance CVM backend dan menghapus port abnormal.</td>
</tr>
<tr>
<td>Protokol</td><td>Jika Port dipilih, paket deteksi UDP akan dikirimkan ke instance CVM backend melalui VIP (yaitu alamat IP yang digunakan oleh instance CLB untuk menyediakan layanan kepada klien), dan ping akan dikirimkan ke IP instance CVM backend untuk mendapatkan status instance CVM backend.</td>
</tr>
<tr>
<td>Port</td><td>Bersifat opsional.Sebaiknya jangan tentukan port, kecuali Anda perlu memeriksa port tertentu.Port server asli akan diperiksa jika port tidak ditentukan di sini.</td>
</tr>
<tr>
<td>Format input</td><td>Mendukung teks dan string heksadesimal.
<ul>
<li>Jika Teks dipilih, teks tersebut akan dikonversi menjadi string biner untuk mengirimkan permintaan dan membandingkan hasil yang dikembalikan.</li>
<li>Jika Heksadesimal dipilih, string heksadesimal akan dikonversi menjadi string biner untuk mengirimkan permintaan dan membandingkan hasil yang dikembalikan.</li>
</ul></td>
</tr>
<tr>
<td>Permintaan</td><td>Bersifat opsional.Konten permintaan pemeriksaan kesehatan khusus.</td>
</tr>
<tr>
<td>Hasil pengembalian</td><td>Bersifat opsional.Ketika menyesuaikan permintaan pemeriksaan kesehatan, Anda perlu memasukkan hasil pemeriksaan kesehatan yang dikembalikan.</td>
</tr>
<tr>
<td>Tampilkan opsi lanjutan</td><td>Untuk informasi selengkapnya, lihat <a href="#advance">Opsi Lanjutan</a>.</td>
</tr>
</table>


### Mengonfigurasi pemeriksaan kesehatan UDP - Perintah ping
1.Konfigurasi pendengar menggunakan langkah **Health Check** (Pemeriksaan Kesehatan) sesuai petunjuk dalam [Prasyarat](#postreq).
2.Dalam langkah **Health Check** (Pemeriksaan Kesehatan), pilih **PING** sebagai protokol.
<table>
<tr>
<th>Parameter</th><th>Deskripsi</th>
</tr>
<tr>
<td>Pemeriksaan kesehatan</td><td>Dapat diaktifkan atau dinonaktifkan.Sebaiknya aktifkan pemeriksaan kesehatan agar dapat melakukan pemeriksaan otomatis terhadap instance CVM backend dan menghapus port abnormal.</td>
</tr>
<tr>
<td>Protokol</td><td>Jika PING dipilih, ping akan dikirimkan ke IP instance CVM backend untuk mendapatkan status instance CVM backend.</td>
</tr>
<tr>
<td>Tampilkan opsi lanjutan</td><td>Untuk informasi selengkapnya, lihat <a href="#advance">Opsi Lanjutan</a>.</td>
</tr>
</table>


## Pendengar TCP SSL

### Mengonfigurasi pemeriksaan kesehatan TCP
1.Konfigurasi pendengar menggunakan langkah **Health Check** (Pemeriksaan Kesehatan) sesuai petunjuk dalam [Prasyarat](#postreq).
2.Dalam langkah **Health Check** (Pemeriksaan Kesehatan), pilih **TCP** sebagai protokol.
<table>
<tr>
<th>Parameter</th><th>Deskripsi</th>
</tr>
<tr>
<td>Pemeriksaan kesehatan</td><td>Dapat diaktifkan atau dinonaktifkan.Sebaiknya aktifkan pemeriksaan kesehatan agar dapat melakukan pemeriksaan otomatis terhadap instance CVM backend dan menghapus port abnormal.</td>
</tr>
<tr>
<td>Protokol</td><td>Pemeriksaan kesehatan TCP akan dilakukan jika <b>TCP</b> dipilih.</td>
</tr>
<tr>
<td>Port</td><td>Port pemeriksaan kesehatan dan port pendengar untuk pendengar TCP SSL menggunakan port yang sama.</td>
</tr>
<tr>
<td>Tampilkan opsi lanjutan</td><td>Untuk informasi selengkapnya, lihat <a href="#advance">Opsi Lanjutan</a>.</td>
</tr>
</table>

### Mengonfigurasi pemeriksaan kesehatan HTTP
1.Konfigurasi pendengar menggunakan langkah **Health Check** (Pemeriksaan Kesehatan) sesuai petunjuk dalam [Prasyarat](#postreq).
2.Dalam langkah **Health Check** (Pemeriksaan Kesehatan), pilih **HTTP** sebagai protokol.
<table>
<tr>
<th>Parameter</th><th>Deskripsi</th>
</tr>
<tr>
<td>Pemeriksaan kesehatan</td><td>Dapat diaktifkan atau dinonaktifkan.Sebaiknya aktifkan pemeriksaan kesehatan agar dapat melakukan pemeriksaan otomatis terhadap instance CVM backend dan menghapus port abnormal.</td>
</tr>
<tr>
<td>Protokol</td><td>Pemeriksaan kesehatan HTTP akan dilakukan jika <b>HTTP</b> dipilih.</td>
</tr>
<tr>
<td>Port</td><td>Port pemeriksaan kesehatan dan port pendengar untuk pendengar TCP SSL menggunakan port yang sama.</td>
</tr>
<tr>
<td>Domain pemeriksaan</td><td>Persyaratan terkait nama domain untuk pemeriksaan kesehatan:
<ul>
<li>Panjang: 1 hingga 80 karakter.</li>
<li>Merupakan nama domain penerusan secara default.</li>
<li>Tidak mendukung ekspresi reguler.Jika nama domain penerusan Anda menggunakan kartubebas, Anda perlu menetapkan nama domain tetap (non-reguler) sebagai nama domain pemeriksaan kesehatan.</li>
<li>Karakter yang didukung: huruf kecil (a hingga z), digit (0 hingga 9), poin desimal (,), dan tanda hubung (-).</li>
</ul></td>
</tr>
<tr>
<td>Jalur</td><td>Persyaratan terkait jalur pemeriksaan kesehatan:
<ul>
<li>Panjang: 1 hingga 200 karakter.</li>
<li>`/` adalah nilai default dan harus digunakan sebagai karakter pertama.</li>
<li>Tidak mendukung ekspresi reguler.Sebaiknya tentukan URL tetap (halaman web statis) untuk pemeriksaan kesehatan.</li>
<li>Karakter yang didukung: huruf kecil (a hingga z), huruf kapital (A hingga Z), digit (0 hingga 9), poin desimal (,), tanda hubung (-), garis bawah (_), garis miring (/), tanda sama dengan (=), dan tanda tanya (?).</li>
</ul></td>
</tr>
<tr>
<td>Metode permintaan HTTP</td><td>Metode permintaan HTTP pada pemeriksaan kesehatan.Opsi:GET (metode default) dan HEAD.
<ul>
<li>Jika HEAD dipilih, server hanya akan mengembalikan informasi header HTTP, yang dapat mengurangi overhead backend dan meningkatkan efisiensi permintaan.Server asli harus mendukung HEAD.</li>
<li>Jika GET dipilih, server asli harus mendukung GET.</li>
</ul></td>
</tr>
<tr>
<td>Versi HTTP</td><td>Versi HTTP server asli.Hanya mendukung HTTP 1.1.Jika server asli perlu mengautentikasi bidang host permintaan, artinya, domain pemeriksaan perlu dikonfigurasi atau Anda akan mendapatkan kode kesalahan 404.
</td>
</tr>
<tr>
<td>Kode status normal</td><td>Jika kode status merupakan kode yang telah dipilih, server asli akan dianggap aktif (sehat).Opsi: http_1xx, http_2xx, http_3xx, http_4xx, dan http_5xx.Anda dapat memilih beberapa opsi.</td>
</tr>
<tr>
<td>Tampilkan opsi lanjutan</td><td>Untuk informasi selengkapnya, lihat <a href="#advance">Opsi Lanjutan</a>.</td>
</tr>
</table>

<span id="http"></span>
## Pendengar HTTP
### Mengonfigurasi pemeriksaan kesehatan HTTP
1.Konfigurasi pendengar menggunakan langkah **Health Check** (Pemeriksaan Kesehatan) sesuai petunjuk dalam [Prasyarat](#postreq).
<table>
<tr>
<th>Parameter</th><th>Deskripsi</th>
</tr>
<tr>
<td>Pemeriksaan kesehatan</td><td>Dapat diaktifkan atau dinonaktifkan.Sebaiknya aktifkan pemeriksaan kesehatan agar dapat melakukan pemeriksaan otomatis terhadap instance CVM backend dan menghapus port abnormal.</td>
</tr>
<tr>
<td>Domain pemeriksaan</td><td>Persyaratan terkait nama domain untuk pemeriksaan kesehatan:
<ul>
<li>Panjang: 1 hingga 80 karakter.</li>
<li>Merupakan nama domain penerusan secara default.</li>
<li>Tidak mendukung ekspresi reguler.Jika nama domain penerusan Anda menggunakan kartubebas, Anda perlu menetapkan nama domain tetap (non-reguler) sebagai nama domain pemeriksaan kesehatan.</li>
<li>Karakter yang didukung: huruf kecil (a hingga z), digit (0 hingga 9), poin desimal (,), dan tanda hubung (-).</li>
</ul></td>
</tr>
<tr>
<td>Jalur</td><td>Jalur pemeriksaan kesehatan dapat diatur ke direktori root server asli atau URL tertentu.Persyaratannya adalah sebagai berikut:
<ul>
<li>Panjang: 1 hingga 200 karakter.</li>
<li>`/` adalah nilai default dan harus digunakan sebagai karakter pertama.</li>
<li>Tidak mendukung ekspresi reguler.Sebaiknya tentukan URL tetap (halaman web statis) untuk pemeriksaan kesehatan.</li>
<li>Karakter yang didukung: huruf kecil (a hingga z), huruf kapital (A hingga Z), digit (0 hingga 9), poin desimal (,), tanda hubung (-), garis bawah (_), garis miring (/), tanda sama dengan (=), dan tanda tanya (?).</li>
</ul>
</td>
</tr>
<tr>
<td>Waktu habis respons</td><td><ul><li>Waktu habis respons maksimum untuk pemeriksaan kesehatan</li><li>Jika server asli tidak merespons dalam periode waktu habis, server akan dianggap abnormal.</li><li>Rentang nilai: 2-60 detik.</li></ul></td>
</tr>
<tr>
<td>Interval pemeriksaan</td><td><ul><li>Interval antara dua pemeriksaan kesehatan.</li><li>Rentang nilai: 5-300 detik.</li></ul></td>
</tr>
<tr>
<td>Ambang batas tidak sehat</td><td><ul><li>Jika hasil pemeriksaan kesehatan gagal sebanyak n (nilai dapat disesuaikan) kali, instance CVM backend akan dianggap tidak heat, dan konsol akan menampilkan status <b>Abnormal</b>.</li><li>Rentang nilai: 2-10 kali.</li></ul></td>
</tr>
<tr>
<td>Ambang batas sehat</td><td><ul><li>Jika hasil pemeriksaan kesehatan berhasil sebanyak n (nilai dapat disesuaikan) kali, instance CVM backend akan dianggap sehat, dan konsol akan menampilkan status <b>Healthy</b> (Sehat).</li><li>Rentang nilai: 2-10 kali. </li></ul></td>
</tr>
<tr>
<td>Metode permintaan HTTP</td><td>Metode permintaan HTTP pada pemeriksaan kesehatan.Opsi:GET (metode default) dan HEAD.
<ul>
<li>Jika HEAD dipilih, server hanya akan mengembalikan informasi header HTTP, yang dapat mengurangi overhead backend dan meningkatkan efisiensi permintaan.Server asli harus mendukung HEAD.</li>
<li>Jika GET dipilih, server asli harus mendukung GET.</li>
</ul></td>
</tr>
<tr>
<td>Kode status normal</td><td>Jika kode status merupakan kode yang telah dipilih, server asli akan dianggap aktif (sehat).Opsi: http_1xx, http_2xx, http_3xx, http_4xx, dan http_5xx.Anda dapat memilih beberapa opsi.</td>
</tr>
</table>

## Pendengar HTTPS
>?Jika HTTP dipilih sebagai protokol backend aturan penerusan pendengar HTTPS, pemeriksaan kesehatan HTTP akan dilakukan; jika HTTPS dipilih, pemeriksaan kesehatan HTTPS akan dilakukan.
>
Untuk konfigurasi pemeriksaan kesehatan pada pendengar HTTPS, lihat <a href="#http">Pendengar HTTP</a>.

<span id="advance"></span>
## Opsi Lanjutan
| Konfigurasi Pemeriksaan Kesehatan    | Deskripsi                    | Nilai Default                              |
| ------- | ------------------------ | ---------------------------------------- |
| Waktu habis respons | <li>Waktu habis respons maksimum untuk pemeriksaan kesehatan.</li><li>Jika server asli tidak merespons dalam periode waktu habis, pemeriksaan kesehatan dianggap abnormal.</li><li>Rentang nilai: 2 - 60 detik.</li> | 2 detik |
| Interval pemeriksaan | <li>Interval antara dua pemeriksaan kesehatan.</li><li>Rentang nilai: 5 - 300 detik.</li> | 5 detik |
| Ambang batas tidak sehat | <li>Jika hasil pemeriksaan kesehatan gagal sebanyak n (nilai dapat disesuaikan) kali, instance CVM backend akan dianggap tidak sehat, dan konsol akan menampilkan status <b>Abnormal</b>.</li><li>Rentang nilai: 2-10 kali.</li> | 3 kali |
| Ambang batas sehat | <li>Jika hasil pemeriksaan kesehatan berhasil sebanyak n (nilai dapat disesuaikan) kali, instance CVM backend akan dianggap sehat, dan konsol akan menampilkan status <b>Healthy</b> (Sehat).</li><li>Rentang nilai: 2-10 kali.</li> | 3 kali |
