[](id:q1)
### Berapa lama habis waktu default untuk simpul Tencent Cloud CDN?
Waktu habis default adalah 10 detik.

[](id:q2)
### Apa yang akan terjadi pada file di simpul CDN jika saya mematikan nama domain yang terhubung di konsol CDN?
Jika Anda mematikan layanan nama domain terhubung CDN, simpul CDN akan menyimpan konfigurasi hubungan nama domain tersebut, lalu lintas CDN tidak lagi akan dihasilkan, dan nama domain tersebut tidak dapat diakses.

[](id:q3)
### Apa yang harus saya lakukan jika saya tidak bisa membuka situs web saya setelah menghubungkannya ke CDN?
Pertama, karena situs web tersebut tidak dapat dibuka jika status CDN nama domain terhubung tersebut **Disabled** (Dinonaktifkan), silakan periksa statusnya.Jika statusnya tidak **Disabled** (Dinonaktifkan), selanjutnya Anda dapat memeriksa:
+ Jalankan `ping` atau `nslookup` untuk memeriksa apakah resolusi CNAME nama domain tersebut sudah berlaku.Jika CNAME belum ditambahkan, silakan hubungi penyedia DNS Anda dan tambahkan CNAME sesuai petunjuk di [Konfigurasi CNAME](https://intl.cloud.tencent.com/document/product/228/3121).
+ Setelah CNAME berlaku, Anda dapat memeriksa apakah server asal sudah dapat diakses.

Jika masih bermasalah, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk meminta bantuan.

[](id:q4)
### Bagaimana saya menentukan simpul CDN mana yang diakses oleh pengguna?
Dengan menjalankan perintah `nslookup` dan `ping`, Anda bisa mendapatkan informasi dasar penanggulangan masalah, seperti IP, latensi, dan kehilangan paket simpul CDN yang diakses oleh pengguna.

[](id:q5)
### Mengapa saya mengalami kecepatan perolehan data yang rendah?
Ini biasanya disebabkan oleh masalah berikut:
+ Ada masalah konfigurasi cache, seperti masa validitas cache yang singkat.
+ Header HTTP menghambat penyimpanan data.Periksa konfigurasi `Cache-Control` atau `Expires` server asal.
+ Hanya sedikit konten yang dapat di-cache untuk jenis server asal tersebut.
+ Situs web tersebut mendapat sedikit kunjungan dan masa validitasnya singkat.Kecepatan perolehan file yang rendah menyebabkan seringnya permintaan tarik-asal.

[](id:q6)
### Mengapa pengguna mengalami koneksi yang lambat saat mereka mengakses CDN?
Silakan periksa kecepatan unduh untuk file besar dan latensi untuk file kecil.Pertama, dapatkan URL yang lambat diakses bagi pengguna dan tentukan apakah akses tersebut lambat dengan menggunakan situs web penguji kecepatan seperti [17ce](http://www.17ce.com) (disarankan).
Jika hasil pengujian membuktikan kecepatan yang lambat dan server asal merupakan server asal eksternal, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).Kami akan membantu pengguna memeriksa apakah unduhan dan bandwidth dibatasi pada mesin server asal.

[](id:q7)
### Bagaimana saya mengatakan apakah akses pengguna telah memperoleh cache CDN?
Lihat informasi `X-Cache-Lookup` pada header pengembalian permintaan.Jika banyak entri `X-Cache-Lookup` yang dikembalikan pada waktu yang sama, itu normal.Jika `Cache Hit`/`Hit From MemCache`/`Hit From Disktank` dikembalikan, itu berarti bahwa cache CDN telah diperoleh.
![](https://mc.qcloudimg.com/static/img/64ac912c895b36f0241a927df6da3543/image.png)
+ `X-Cache-Lookup:Hit From MemCache`: memori simpul CDN telah diperoleh.
+ `X-Cache-Lookup:Hit From Disktank`: disk simpul CDN telah diperoleh.

[](id:q8)
### Mengapa file dengan nama sama yang dikembalikan oleh simpul tersebut memiliki ukuran yang berbeda?
Karena semua jenis file di-cache menurut pengaturan default, mungkin ada versi file yang berbeda pada simpul CDN tersebut.Untuk mengatasi masalah ini, Anda dapat:
+ Membersihkan file secara manual dan segera memperbarui cache tersebut.
+ Menggunakan nomor versi, misalnya, ```http://www.xxx.com/xxx.js?version=1```.
+ Mengubah nama file untuk menghindari penggunaan file dengan nama yang sama.

Jika masih bermasalah, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk meminta bantuan.

[](id:q9)
### Apa yang harus saya lakukan jika situs web saya tidak dapat diakses setelah daftar izin perlindungan hotlink dikonfigurasikan di CDN?

Silakan pilih **Allow blank referer** (Izinkan pengirim kosong) saat mengonfigurasi daftar izin perlindungan hotlink sehingga situs web tersebut dapat dibuka secara normal di peramban (dengan pengirim kosong).
![Image description](https://main.qcloudimg.com/raw/3ec77732d4f5266278af2e8f569b08a2.png)

[](id:q10)
### Bisakah konfigurasi batas lalu lintas bertahan menghadapi serangan DDoS?

CDN berfokus terutama pada akselerasi pengiriman konten daripada pencegahan DDoS.Anda dapat menggunakan fitur batas bandwidth CDN untuk mengumpulkan secara otomatis data statistik penggunaan bandwidth dalam 5 menit.Jika ambang batas tersebut tercapai, CDN akan merespons sesuai dengan konfigurasi tersebut.**The maximum threshold is 10,000 Tbps** (Ambang batas maksimal adalah 10.000 Tbps).

[](id:q11)
### Bisakah CDN memberikan semua IP simpulnya?
Tidak. Karena pertimbangan keamanan, CDN tidak bisa memberikan daftar lengkap IP simpul.Namun, Anda dapat mengueri wilayah IP di halaman **Verify Tencent Cloud CDN IP** (Verifikasikan IP Tencent Cloud CDN).Untuk informasi selengkapnya, silakan lihat [Verifikasi IP Tencent](https://intl.cloud.tencent.com/document/product/228/10747).
