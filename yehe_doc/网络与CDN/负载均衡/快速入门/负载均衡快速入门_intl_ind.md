Tencent Cloud CLB menyediakan berbagai protokol seperti TCP, UDP, TCP SSL, HTTP, dan HTTPS sehingga melengkapi bisnis dengan nama domain dan layanan penerusan berbasis URL.Dokumen ini memandu Anda untuk membuat instance CLB dengan cepat dan meneruskan permintaan klien ke dua instance CVM.

## Prasyarat
1.Anda telah membuat dua instance CVM (dokumen ini mengambil **rs-1** dan **rs-2** sebagai dua contoh instance).Untuk informasi tentang cara membuat instance CVM, lihat [Membuat Instance lewat Halaman Pembelian CVM](https://intl.cloud.tencent.com/document/product/213/4855).
2.Anda telah men-deploy layanan backend di dua instance CVM.Dokumen ini mengambil penerusan HTTP sebagai contoh.Server Nginx telah di-deploy di instance **rs-1** dan **rs-2** CVM, dan kedua instance tersebut mengembalikan dua halaman statis HTML dengan mengucapkan "Halo nginx!Ini adalah rs-1!"dan "Halo nginx!Ini adalah rs-2!"Untuk informasi selengkapnya, lihat [Men-deploy Nginx di CentOS](https://intl.cloud.tencent.com/document/product/214/32390).
>!
> - Dokumen ini menjelaskan langkah-langkah untuk akun tagihan-berdasarkan-IP.Untuk akun tagihan-berdasarkan-CVM, terlebih dahulu silakan membeli bandwidth jaringan publik untuk instance CVM.Jika Anda tidak tahu pasti jenis akun Anda, silakan lihat [Memeriksa Jenis Akun](https://intl.cloud.tencent.com/document/product/684/15246).
>- Dalam contoh ini, layanan berbeda yang di-deploy di server asli akan mengembalikan nilai yang berbeda.Dalam praktiknya, layanan yang di-deploy di server asli itu mirip untuk memberikan pengalaman yang konsisten bagi semua pengguna.

## Langkah 1:Membeli Instance CLB
Setelah pembelian berhasil, sistem akan otomatis menetapkan VIP ke instance CLB.VIP akan digunakan sebagai alamat IP untuk menyediakan layanan kepada klien.
1.Masuk ke konsol Tencent Cloud dan buka [halaman pembelian CLB](https://buy.cloud.tencent.com/lb).
2.Pertama, pilih wilayah yang sama dengan instance CVM Anda.Selanjutnya, pilih **Cloud Load Balancer** (Cloud Load Balancer) sebagai jenis instance, **Public Network** (Jaringan Publik) sebagai jenis jaringan.Untuk detail selengkapnya, silakan lihat [Pilihan Atribut Produk](https://intl.cloud.tencent.com/document/product/214/13629).
>?Pengujian beta IP jalur tunggal statis hanya tersedia di Jinan, Hangzhou, Fuzhou, Shijiazhuang, Wuhan, dan Changsha.Anda dapat mengirimkan aplikasi untuk menggunakannya.Setelah diizinkan, Anda dapat memilih ISP (China Mobile, China Unicom, atau China Telecom) di halaman pembelian.Jika Anda ingin mencobanya di Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, dan Chongqing, hubungi perwakilan penjualan Anda.
>
3.Klik **Buy Now** (Beli Sekarang) dan lakukan pembayaran.
4.Kembali ke halaman **Instance Management** (Manajemen Instance), pilih wilayah untuk melihat instance baru.
![](https://main.qcloudimg.com/raw/2c2afd943a9f6a6d03f55c00e62da8b5.png)

## Langkah 2:Mengonfigurasi Pendengar CLB
Pendengar CLB digunakan untuk meneruskan melalui protokol dan port yang ditentukan.Dokumen ini menjelaskan cara mengonfigurasi instance CLB untuk meneruskan permintaan HTTP klien.
### Konfigurasikan protokol dan port pendengar HTTP
Ketika seorang klien memulai permintaan, instance CLB akan menerima permintaan menurut protokol dan port pendengar, lalu meneruskan permintaan tersebut ke server asli.
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2.Di halaman **Instance Management** (Manajemen Instance), klik **Configure Listener** (Konfigurasikan Pendengar) di kolom **Operation** (Pengoperasian) dari instance CLB target.
3.Di halaman **Listener Management** (Manajemen Pendengar), klik **Create** (Buat) di bagian **HTTP/HTTPS Listener** (Pendengar HTTP/HTTPS).
![](https://main.qcloudimg.com/raw/782c60eeb4bf9aa334e4243cf4e068d5.png)
4.Di jendela **Create Listener** (Buat Pendengar), silakan konfigurasikan item berikut dan klik **Submit** (Kirim).
- Nama pendengar.
- Dengar port protokol (misalnya, **HTTP:80**).

### Konfigurasikan aturan penerusan pendengar
Jika seorang klien memulai permintaan, instance CLB akan meneruskan permintaan tersebut sesuai aturan penerusan pendengar yang sudah dikonfigurasi.
1.Di tab **Listener Management** (Manajemen Pendengar), klik **+** di sisi kanan pendengar baru.
![](https://main.qcloudimg.com/raw/f8ab76b69f8a0cfdd5b4332c8b80b1f2.png)
2.Di jendela **Create Forwarding Rules** (Buat Aturan Penerusan), konfigurasikan nama domain, URL, metode penyeimbangan, lalu klik **Next** (Selanjutnya)_.
- Nama domain: nama domain server asli Anda (misalnya, **www.example.com**).
- Nama domain default: jika permintaan seorang klien tidak cocok dengan nama domain pendengar, instance CLB akan meneruskan permintaan tersebut ke nama domain default (server default).Setiap pendengar dapat dikonfigurasi hanya dengan satu nama domain default.Jika pendengar tidak memiliki nama domain default, instance CLB akan meneruskan permintaan ke nama domain pertama.Contoh ini akan melewati langkah konfigurasi.
- URL: jalur akses ke server asli Anda (misalnya, `/image/`).
- Pilih **Weighted Round Robin** (Round Robin Tertimbang) sebagai metode penyeimbangan lalu klik **Next** (Berikutnya).Untuk informasi selengkapnya, lihat [Metode Penyeimbangan Muatan](https://intl.cloud.tencent.com/document/product/214/6153).
![](https://main.qcloudimg.com/raw/263b2486f8a5734ea8aa643ea3b34387.png)
3.Aktifkan pemeriksaan kesehatan.Gunakan nilai default untuk domain pemeriksaan dan bidang jalur, lalu klik **Next** (Berikutnya).
![](https://main.qcloudimg.com/raw/9d8c9bbe1191340e452e9feeafb20e73.png)
4.Nonaktifkan persistensi sesi lalu klik **Submit** (Kirim).

Untuk informasi selengkapnya tentang pendengar CLB, lihat [Ikhtisar Pendengar CLB](https://intl.cloud.tencent.com/document/product/214/6151).
>?
>- Aturan penerus: setiap pendengar dapat dikonfigurasikan dengan beberapa nama domain, dan setiap nama domain dapat dikonfigurasikan dengan beberapa URL.Anda dapat memilih nama pendengar atau domain, lalu klik ikon **+** untuk membuat aturan baru.
>- Persistensi sesi: jika persistensi sesi dinonaktifkan dan metode round-robin dipilih, permintaan dari klien yang sama akan ditetapkan ke berbagai server asli secara berurutan; jika persistensi sesi diaktifkan, atau dinonaktifkan tetapi metode penyeimbangan `ip_hash` digunakan, permintaan dari klien yang sama akan selalu ditetapkan ke server asli yang sama.

### Ikat server asli dengan pendengar
Jika seorang klien memulai permintaan, instance CLB akan meneruskan permintaan tersebut ke instance CVM yang terikat dengan pendengarnya untuk pemrosesan.
1.Di tab **Listener Management** (Manajemen Pendengar), klik **+** untuk memperluas pendengar baru.Klik URL, dan klik **Bind** (Ikat) di bagian **Forwarding Rules** (Aturan Penerusan) di sisi kanan.
![](https://main.qcloudimg.com/raw/ad3bab63556a4340792b1d5dadcc1b19.png)
2.Di jendela pop-up, pilih **CVM** sebagai jenis instance, pilih dua instance CVM **rs-1** dan **rs-2** (yang berada di wilayah yang sama dengan instance CLB), atur port keduanya ke **80** dan bobot ke **10** (nilai default), lalu klik **Confirm** (Konfirmasikan).
![](https://main.qcloudimg.com/raw/02a6cf1b63726a7133f97f5f56c10d74.png)
3. [](id:qrjkjc)Sekarang Anda dapat melihat instance CVM terikat dan status pemeriksaan kesehatannya di bagian **Forwarding Rules** (Aturan Penerusan).Jika status kesehatan port adalah **Healthy** (Sehat), instance CVM biasanya dapat memproses permintaan yang diteruskan oleh instance CLB.
![](https://main.qcloudimg.com/raw/8ef5732d0748b73dd1d71b3ab0aed1d4.png)
>!Satu aturan penerusan (protokol pendengar, port, nama domain, dan URL) dapat diikat dengan beberapa port dari instance CVM yang sama.Jika seorang pengguna men-deploy layanan yang sama di port **80** dan **81** dari **rs-1**, kedua port dapat diikat dengan aturan penerusan contoh dan keduanya akan menerima permintaan yang diteruskan oleh instance CLB.

## Langkah 3:Mengonfigurasi Grup Keamanan
Setelah membuat instance CLB, Anda dapat mengonfigurasi grup keamanan CLB untuk mengisolasi lalu lintas jaringan publik.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Grup Keamanan CLB](https://intl.cloud.tencent.com/document/product/214/14733).

Setelah mengonfigurasi grup keamanan, Anda dapat mengaktifkan atau menonaktifkan fitur **Allow Traffic by Default** (Izinkan Lalu Lintas secara Default):
### Metode 1:Aktifkan "Allow Traffic by Default in Security Group" (Izinkan Lalu Lintas secara Default di Grup Keamanan)
Untuk informasi selengkapnya, silakan lihat [Konfigurasi Grup Keamanan CLB](https://intl.cloud.tencent.com/document/product/214/14733).

### Metode 2:Izinkan IP klien khusus di grup keamanan CVM
Untuk informasi selengkapnya, silakan lihat [Konfigurasi Grup Keamanan CLB](https://intl.cloud.tencent.com/document/product/214/14733).

## Langkah 4:Memverifikasi Layanan CLB
Setelah mengonfigurasi instance CLB, Anda dapat memverifikasi efektivitasnya dengan mengakses berbagai server asli melalui **domain names and URLs** (nama domain dan URL) yang berbeda di instance CLB yang sama, atau memverifikasi fitur **Content-based Routing** (Perutean berbasis Konten).
### Metode 1:Konfigurasikan `hosts` dan petakan nama domain ke instance CLB
1.Di perangkat Windows, modifikasi file **hosts** (host) di direktori `C:\Windows\System32\drivers\etc`, dan petakan nama domain ke VIP dari instance CLB.
![](https://main.qcloudimg.com/raw/b12ee22250cb7c24d5e12ecb803e6355.png)
2.Untuk memverifikasi berhasil tidaknya konfigurasi **hosts** (host), Anda dapat menjalankan perintah **ping** di **cmd.exe** untuk menguji apakah nama domain berhasil diikat dengan VIP.Jika ada yang dikembalikan, paket data berhasil diikat.
![](https://main.qcloudimg.com/raw/b11b20840cba86bedbaffaa424b4e021.png)
3.Uji layanan CLB dengan mengakses http://www.example.com/image/ melalui peramban.Jika halaman Anda mengembalikan gambar berikut, berarti permintaan telah diteruskan oleh instance CLB ke CVM rs-1, dan CVM biasanya telah memproses permintaan tersebut dan mengembalikan halaman layanan.
![](https://main.qcloudimg.com/raw/cf61264a9406d141650ed79da21c6859.png)
4.Karena metode penyeimbangan pendengar berupa round robin tertimbang, dan bobot kedua instance CVM adalah 10, maka Anda dapat memuat ulang peramban untuk memulai permintaan lagi.Jika halaman Anda mengembalikan gambar berikut, berarti permintaan telah diteruskan oleh instance CLB ke CVM rs-2.
![](https://main.qcloudimg.com/raw/ab7db7b5c3952739919ae6e271bb1348.png)
>!**/** di **image/** tidak dapat dihilangkan. **/** menunjukkan bahwa **image** (gambar) adalah direktori default, bukan nama file.

## Mengonfigurasi Pengalihan (opsional)
CLB mendukung pengalihan otomatis dan pengalihan manual.Untuk informasi selengkapnya, silakan baca [Mengonfigurasi Pengalihan Lapisan-7](https://intl.cloud.tencent.com/document/product/214/8839).
- Pengalihan otomatis (HTTPS paksa): ketika PC atau peramban seluler mengakses layanan web dengan permintaan HTTP, respons HTTPS dikembalikan ke peramban setelah permintaan melewati proksi CLB sehingga memaksa peramban untuk mengakses halaman web menggunakan HTTPS.
- Pengalihan manual: jika Anda ingin menonaktifkan bisnis web sementara waktu untuk kasus-kasus seperti penjualan produk, pemeliharaan halaman, atau pembaruan dan peningkatan, Anda perlu mengalihkan halaman asal ke halaman baru.Jika tidak, alamat lama di database favorit dan mesin pencarian pengunjung akan mengembalikan halaman pesan kesalahan 404 atau 503 sehingga mengganggu pengalaman pengguna dan mengakibatkan pemborosan lalu lintas serta bahkan membatalkan akumulasi skor pada mesin pencarian.


## Operasi yang Relevan
- [Men-deploy Web Java di CentOS](https://intl.cloud.tencent.com/document/product/214/32391)
- [Menginstal dan Mengonfigurasi PHP](https://intl.cloud.tencent.com/document/product/213/10182)
