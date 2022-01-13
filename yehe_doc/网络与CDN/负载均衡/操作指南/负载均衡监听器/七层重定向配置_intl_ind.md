CLB mendukung pengalihan lapisan 7, agar Anda bisa mengonfigurasi pengalihan pada pendengar HTTP/HTTPS lapisan 7.
>?
>- Persistensi sesi: jika klien mengakses `example.com/bbs/test/123.html` dan persistensi sesi sudah diaktifkan di CVM backend, setelah pengalihan diaktifkan untuk meneruskan lalu lintas ke `example.com/bbs/test/456.html`, mekanisme persistensi sesi awalnya tidak akan berlaku.
- Pengalihan TCP/UDP: saat ini tidak mendukung pengalihan pada level IP + port, tetapi akan tersedia di versi berikutnya.
## Ikhtisar Pengalihan
1.Pengalihan otomatis
- Ikhtisar
Untuk pendengar `HTTPS:443` yang ada, pendengar HTTP (port 80) akan dibuat secara otomatis oleh sistem untuk penerusan.Permintaan yang dikirimkan ke `HTTP:80` akan dialihkan secara otomatis ke `HTTPS:443`.
- Kasus penggunaan
Pengalihan paksa HTTPS, misalnya, mengalihkan permintaan HTTP ke HTTPS.Saat pengguna mengakses layanan web di PC atau peramban seluler melalui HTTP, CLB akan mengalihkan semua permintaan yang dikirimkan ke `HTTP:80` ke `HTTPS:443` untuk penerusan.
- Keunggulan skema
- Konfigurasi atur-dan-lupakan: pengalihan paksa HTTPS bisa diimplementasikan untuk nama domain, yang hanya membutuhkan satu operasi konfigurasi.
- Pembaruan layanan: jika jumlah URL layanan HTTPS berubah, Anda hanya perlu menggunakan fitur ini lagi di konsol untuk menyegarkan.
2.Pengalihan manual
- Ikhtisar
Anda bisa mengonfigurasi pengalihan 1-ke1.Contohnya, di instance CLB, Anda bisa mengonfigurasi pengalihan `listener 1 / domain name 1 / URL 1` ke `listener 2 / domain name 2 / URL 2`.
- Kasus penggunaan
Pengalihan jalur tunggal.Contohnya, jika Anda ingin menonaktifkan bisnis web sementara waktu pada kasus seperti produk habis, pemeliharaan halaman, atau pembaruan dan peningkatan, halaman asal perlu dialihkan ke halaman baru.Jika tidak ada pengalihan yang dilakukan, alamat lama di favorit pengguna dan database mesin pencari akan menampilkan halaman pesan kesalahan `404/503`, menurunkan pengalaman pengguna dan mengakibatkan hilangnya lalu lintas.

## Pengalihan Otomatis
CLB mendukung pengalihan paksa satu klik dari HTTP ke HTTPS.
Dengan asumsi Anda perlu mengonfigurasi situs web `https://www.example.com`, agar pengguna akhir bisa mengunjunginya dengan aman melalui HTTPS terlepas dari apakah mereka mengirim permintaan HTTP (`http://www.example.com`) atau permintaan HTTPS (`https://www.example.com`) di peramban.
### Prasyarat
Pendengar `HTTPS:443` telah dikonfigurasikan.
### Petunjuk
1.Konfigurasikan pendengar HTTPS CLB di [Konsol CLB](https://console.cloud.tencent.com/clb) dan atur lingkungan web dari `https://example.com`.Untuk informasi selengkapnya, silakan lihat [Mengonfigurasi Pendengar HTTPS
](https://intl.cloud.tencent.com/document/product/214/32516).
2.Hasil konfigurasi pendengar HTTPS adalah seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/6eaf2d1220d140bc37537f3388d78509.png)
3.Pada tab "Redirection Configuration" (Konfigurasi Pengalihan) di detail instance CLB, klik **Create Redirection Configuration** (Buat Konfigurasi Pengalihan).
![](https://main.qcloudimg.com/raw/47fa6c0bd8b6f060332333b2685f8efe.png)
4.Pilih **Automatic Redirection Configuration** (Konfigurasi Pengalihan Otomatis), pilih pendengar dan nama domain HTTPS yang sudah dikonfigurasi, dan klik **Next:Configure Path** (Berikutnya: Konfigurasi Jalur).
![](https://main.qcloudimg.com/raw/4481d9beac8fa51ee7f6c252c3714a41.png)
5.Klik **Submit** (Kirim) untuk menyelesaikan konfigurasi.
![](https://main.qcloudimg.com/raw/435e1389eadacc7bc90966480a29a131.png)
6.Hasil setelah pengalihan dikonfigurasikan adalah seperti yang ditunjukkan di bawah ini.Seperti yang bisa Anda lihat, pendengar `HTTP:80` telah dikonfigurasi untuk pendengar `HTTPS:443` secara otomatis, dan semua lalu lintas HTTP akan dialihkan ke HTTPS secara otomatis.
![](https://main.qcloudimg.com/raw/c3249968deb68888fb591e59289194d9.png)

## Pengalihan Manual
CLB mendukung konfigurasi pengalihan 1-ke-1.
Contohnya, bisnis Anda menggunakan halaman `forsale` untuk kampanye promosi dan harus mengalihkan halaman kampanye `https://www.example.com/forsale` ke beranda baru `https://www.new.com/index` setelah kampanye berakhir.

### Prasyarat
- Pendengar HTTPS telah dikonfigurasikan.
- Nama domain yang diteruskan `https://www.example.com/forsale` telah dikonfigurasi.
- Nama domain dan jalur yang diteruskan `https://www.new.com/index` telah dikonfigurasi.


### Petunjuk
1.Konfigurasikan pendengar HTTPS CLB di [Konsol CLB](https://console.cloud.tencent.com/clb) dan atur lingkungan web dari `https://example.com`.Untuk informasi selengkapnya, silakan lihat [Mengonfigurasi Pendengar HTTPS](https://intl.cloud.tencent.com/document/product/214/32516).
2.Hasil konfigurasi HTTPS adalah seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/5c1fc217e1795a2f6a7b31c2a7ba3bfc.png)
3.Pada tab "Redirection Configuration" (Konfigurasi Pengalihan) di detail instance CLB, klik **Create Redirection Configuration** (Buat Konfigurasi Pengalihan).
![](https://main.qcloudimg.com/raw/47fa6c0bd8b6f060332333b2685f8efe.png)
4.Pilih **Manual Redirection Configuration** (Konfigurasi Pengalihan Manual), pilih port protokol frontend yang pertama diakses, `HTTPS:443` dan nama domain `https://www.example.com/forsale`, pilih port protokol frontend `HTTPS:443` dan nama domain `https://www.new.com/index` setelah pengalihan, dan klik **Next:Configure Path** (Berikutnya: Konfigurasi Jalur).
![](https://main.qcloudimg.com/raw/51106736b5ee61d6e87767652185d57a.png)
5.Pilih `/forsale` untuk jalur akses pertama dan `/index` untuk jalur akses setelah pengalihan, dan klik **Submit** (Kirim) untuk menyelesaikan konfigurasi.
![](https://main.qcloudimg.com/raw/5f59b88ecc291d912b7faf2cf1d3770e.png)
6.Hasil setelah konfigurasi pengalihan adalah seperti yang ditunjukkan di bawah ini.Seperti yang bisa Anda lihat, di pendengar `HTTPS:443`, `https://www.example.com/forsale` telah dialihkan ke `https://www.new.com/index`.
![](https://main.qcloudimg.com/raw/34364863bd44202df54e89ec3cb923f9.png)

