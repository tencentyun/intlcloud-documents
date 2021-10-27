[](id:q1)
### Bagaimana cara menambahkan nama domain?
Anda dapat menghubungkan suatu nama domain pada konsol CDN.Untuk informasi selengkapnya, silakan baca [Menambahkan Nama Domain](https://intl.cloud.tencent.com/document/product/228/5734).

[](id:q2)
### Apakah ada persyaratan untuk menghubungkan suatu nama domain ke CDN?
YaBerikut ini persyaratan untuk menghubungkan nama domain ke CDN:
1.Panjang nama domain tidak boleh melebihi 50 karakter.Nama domain dalam bahasa Mandarin, meskipun telah ditranskode, saat ini tidak didukung.
2.Jika menggunakan CDN Tiongkok daratan, nama domain tersebut harus memiliki izin ICP yang dikeluarkan oleh MIIT, dan konten bisnis server asal harus sesuai dengan hukum.
3.Nama domain merupakan nama subdomain dalam format `a.test.com` atau `a.b.test.com` atau nama domain kartubebas dalam format `*.test.com` atau `*.a.test.com`.
4.Verifikasi kepemilikan nama domain diperlukan saat menghubungkan suatu nama domain untuk pertama kali, nama domain kartubebas, atau nama domain terhubung.

[](id:q3)
### Apakah CDN mendukung penghubungan nama domain kartubebas?
Ya, CDN mendukung penghubungan nama domain kartubebas, yang mengharuskan verifikasi kepemilikan nama domain.Setelah diverifikasi, nama domain dapat dihubungkan atau diambil.
Selain itu:
1.Jika nama domain kartubebas, seperti `*.test.com`, sudah terhubung ke Tencent Cloud, nama subdomainnya tidak dapat dihubungkan ke Tencent Cloud oleh akun lain.
2.Jika nama domain kartubebas `*.test.com` sudah dihubungkan ke Tencent Cloud oleh akun Anda, nama domain kartubebas dalam format, seperti `*.path.test.com`, tidak dapat dihubungkan ke Tencent Cloud oleh akun Anda.

[](id:q4)
### Berapa lama waktu yang diperlukan agar konfigurasi CDN berlaku?
Umumnya, diperlukan waktu kurang dari 30 menit agar konfigurasi CDN berlaku.Jika konfigurasi tersebut tidak aktif dalam 30 menit, Anda dapat [mengirim tiket](https://console.cloud.tencent.com/workorder/category) untuk meminta bantuan.

[](id:q5)
### Bisakah saya mengonfigurasi lebih dari satu IP server asal?
YaSetelah Anda mengonfigurasi lebih dari satu IP, CDN akan mengakses secara acak salah satu dari IP tersebut saat meneruskan suatu permintaan ke server asal.Jika jumlah kegagalan tarik-asal dengan IP ini melebihi ambang batas, IP tersebut akan diisolasi selama 300 detik secara default, dan selama itu tidak ada permintaan tarik-asal yang akan diteruskan ke IP tersebut.

[](id:q6)
### Bagaimana cara mengikatkan CNAME ke suatu nama domain setelah nama domain tersebut terhubung ke CDN?
Lihat [Konfigurasi CNAME](https://intl.cloud.tencent.com/document/product/228/3121) untuk mengetahui cara mengikat CNAME dengan penyedia layanan DNS Anda.

[](id:q7)
### Saya hanya bisa menonaktifkan suatu nama domain tetapi tidak bisa menghapusnya.
Silakan periksa apakah pengguna adalah kolaborator.Kolaborator harus mendapatkan izin yang sesuai dari pembuat operasi tersebut.Jika Anda yakin bahwa kolaborator telah diberi izin tetapi masih tidak bisa melaksanakan operasi tersebut, [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk meminta bantuan.

[](id:q8)
### Apakah konfigurasi nama domain akan dipertahankan setelah layanan akselerasi dimatikan?
YaSetelah layanan akselerasi dimatikan, konfigurasi nama domain akan dipertahankan, tetapi layanan akselerasi tidak lagi tersedia.Kode status 404 akan dikembalikan untuk permintaan pengguna.

[](id:q9)
### Apakah konfigurasi nama domain akan dipertahankan setelah nama domain akselerasi dihapus?
Tidak. Setelah nama domain dihapus, konfigurasinya tidak akan dipertahankan.

[](id:q10)
### Bagaimana cara mematikan layanan akselerasi?
Anda dapat mematikan layanan akselerasi di konsol CDN.Untuk mendapatkan petunjuk lengkap, silakan lihat "Mematikan layanan akselerasi" pada [Operasi Nama Domain](https://intl.cloud.tencent.com/document/product/228/5736).

[](id:q11)
### Bagaimana cara menghapus nama domain akselerasi?
Anda dapat menghapus nama domain akselerasi di konsol CDN.Untuk mendapatkan petunjuk lengkap, silakan lihat "Menghapus nama domain akselerasi" pada [Operasi Nama Domain](https://intl.cloud.tencent.com/document/product/228/5736).

[](id:q12)
### Bagaimana cara membuka blokir suatu nama domain?
Silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk meminta bantuan.

[](id:q13)
### Apa jenis bisnis yang didukung CDN?
Jenis layanan yang dipilih menentukan platform sumber daya yang digunakan oleh nama domain tersebut.Konfigurasi akselerasi bervariasi menurut platform sumber daya.Silakan pilih jenis layanan yang sesuai dengan bisnis Anda:
- Akselerasi statis:Cocok untuk skenario akselerasi sumber daya statis, seperti ecommerce, situs web, dan gambar game.
- Akselerasi unduhan:Cocok untuk skenario, seperti penginstalan game, unduhan audio/video, dan distribusi paket firmware telepon seluler.
- Akselerasi streaming VOD:Cocok untuk skenario aplikasi, seperti akselerasi audio/video VOD.

[](id:q14)
### Bagaimana cara mengubah proyek nama domain di CDN?

Masuk ke [konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sisi kanan nama domain, buka tab **Basic Configuration** (Konfigurasi Dasar), lalu ubah proyek nama domain.Untuk mengubah proyek lebih dari satu nama domain secara batch, silakan centang nama domain sasaran di halaman **Domain Management** (Pengelolaan Domain), klik daftar turun **More Actions** (Tindakan Selengkapnya), dan pilih **Edit Project** (Edit Proyek).Hingga 50 nama domain dapat dioperasikan sekaligus.

>!Para pengguna di sistem perizinan CDN harus berhati-hati karena operasi ini dapat menyebabkan perubahan pada izin subpengguna.


[](id:m1)
### Nama domain saya sudah memperoleh izin ICP dari MIIT.Mengapa sistem mengingatkan bahwa sistem tidak memiliki izin ICP ketika saya berusaha menghubungkannya ke CDN?
Setelah Anda mendapatkan izin ICP, diperlukan waktu untuk menyinkronkan informasi dari MIIT dengan Tencent Cloud CDN.Silakan tunggu 24 jam dan coba lagi.

[](id:q16)
### Bisakah saya mengonfigurasi port untuk nama domain akselerasi atau server asal?
- Port nama domain akselerasi CDN: saat ini, port akselerasi CDN hanya bisa 80, 443, dan 8080.
- Port server asal: port 1 sampai 65535 dapat dikonfigurasikan sesuai alamat server asal.

[](id:q17)
### Apa itu konfigurasi domain asal CDN?
Domain asal merupakan nama domain situs web yang diakses di server asal selama tarik-asal di simpul CDN.Server asal dan domain asal:IP atau nama domain yang dikonfigurasikan di server asal mengizinkan simpul CDN untuk mencari server asal yang sesuai selama tarik-asal.Bisa terdapat lebih dari satu situs web di server tersebut, dan domain asal menunjukkan di situs web mana terdapat suatu sumber daya.

[](id:q18)
### Bagaimana cara mengetahui apakah CDN telah berlaku?

Anda dapat menjalankan perintah `nslookup` untuk mengueri resolusi DNS nama domain akselerasi CDN Anda.Jika nama domain hasil resolusi tersebut berakhiran `dnsv1.com` (rekaman CNAME) seperti ditunjukkan pada gambar, itu menunjukkan bahwa layanan akselerasi CDN untuk nama domain Anda telah berlaku.
![](https://main.qcloudimg.com/raw/4576b46fd8a04b726e6893a08f3fe61f.png)


[](id:q19)
### Apa yang harus saya lakukan jika file tidak dapat diunduh dari CDN?

Jika file tidak dapat diunduh dari CDN, kami sarankan untuk menanggulangi masalah tersebut dengan cara berikut:
1.Periksa apakah file dapat diunduh secara normal dari server asal.
2.Periksa apakah nama domain dikonfigurasikan dengan benar di konsol CDN (lihat domain asal di tab **Basic Configuration** (Konfigurasi Dasar)).Pastikan bahwa domain asal yang dikonfigurasikan dapat diakses secara normal.Jika tidak bisa, tarik-asal bisa gagal, yang akan memengaruhi bisnis Anda.
3.Periksa kebijakan keamanan server asal.Silakan periksa apakah kegagalan tarik-asal disebabkan oleh kebijakan keamanan yang dikonfigurasikan pada server asal, dan jika ya, silakan [hubungi kami](https://intl.cloud.tencent.com/support) untuk mendapatkan rentang IP perantara dan menambahkan server asal ke daftar izin.

[](id:q20)
### Apa yang harus saya lakukan jika saya tidak bisa masuk ke backend WordPress setelah akselerasi CDN dikonfigurasikan?
WordPress melibatkan permintaan dinamis.Jika konfigurasi cache tidak sesuai, pengecualian masuk dapat terjadi.Kami menyarankan pengaturan validitas cache jenis file dinamis yang sesuai ke 0 sehingga file jenis ini tidak akan di-cache secara otomatis.Jenis file dinamis yang umum meliputi .asp, .jsp, .php, .perl, dan .cgi.Untuk mendapatkan petunjuk lengkap, silakan lihat [Konfigurasi Validitas Cache Simpul (Lama)](https://intl.cloud.tencent.com/document/product/228/35317).


