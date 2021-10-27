## Ikhtisar Konfigurasi

Untuk bisnis yang telah terhubung ke CDN Tencent Cloud, Anda dapat melihat informasi seperti waktu pembuatan nama domain, nama domain CNAME yang sesuai, wilayah akselerasi, proyek, jenis layanan, dan protokol yang didukung pada modul informasi dasar dari nama domain tersebut. Anda juga dapat memodifikasi informasi seperti wilayah akselerasi, jenis layanan, dan proyek sesuai kebutuhan.

## Panduan Konfigurasi

### Melihat informasi dasar

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Informasi dasar nama domain ada di tab **Basic Configuration** (Konfigurasi Dasar).
![](https://main.qcloudimg.com/raw/5b6d2f8572ba022c5a18bb787953b1d0.png)



### Memodifikasi wilayah akselerasi nama domain

Klik **Modify** (Modifikasi) di sebelah kanan wilayah akselerasi untuk mengubahnya.
- Jika nama domain dikonfigurasi untuk akselerasi global, permintaan akan dijadwalkan ke simpul cache CDN global terdekat. Secara umum, simpul di dalam dan di luar Tiongkok Daratan masing-masing melayani pengguna di dalam dan di luar Tiongkok Daratan.
- Jika nama domain dikonfigurasi untuk akselerasi di Tiongkok Daratan, permintaan akses dari pengguna global akan dilayani oleh simpul cache di Tiongkok Daratan.
- Jika nama domain dikonfigurasi untuk akselerasi di luar Tiongkok Daratan, permintaan akses dari pengguna global akan dilayani oleh simpul cache di luar Tiongkok Daratan.



> ! Layanan akselerasi di dalam dan di luar Tiongkok Daratan ditagihkan secara terpisah dengan harga yang berbeda. Untuk informasi selengkapnya, silakan [klik di sini](https://intl.cloud.tencent.com/document/product/228/2949).


### Memodifikasi proyek

Klik **Modify** (Modifikasi) di sebelah kanan proyek nama domain untuk mengubahnya.


> !
> - Harap dicatat bahwa modifikasi proyek akan mengubah statistik berbasis proyek dan izin subpengguna. Silakan modifikasi dengan hati-hati.
> - Untuk membuat proyek atau mengelola proyek yang sudah ada, buka halaman [Pengelolaan Proyek](https://console.cloud.tencent.com/project).






### Memodifikasi jenis layanan

CDN Tencent Cloud mengoptimalkan kinerja akselerasi berdasarkan jenis layanan. Untuk hasil akselerasi terbaik, sebaiknya pilih jenis layanan yang serupa dengan bisnis aktual Anda. Jika Anda ingin menyesuaikannya, klik **Modify** (Modifikasi) di sebelah kanan:


> !
> - Memodifikasi jenis layanan akan mengubah platform akselerasi CDN yang mendasarinya, yang dapat menyebabkan sejumlah kecil permintaan yang gagal dan meningkatkan bandwidth tarik-asal. Kami menyarankan Anda untuk memodifikasi jenis layanan selama jam tidak sibuk.
> - Jika Anda tidak dapat menemukan tombol **Modify** (Modifikasi) di samping nama domain Anda, silakan [hubungi kami](https://intl.cloud.tencent.com/zh/contact-sales) untuk mendapatkan bantuan.

### Memodifikasi akses IPv6
Alihkan switch akses IPv6 untuk mengaktifkan atau menonaktifkannya. Simpul CDN dapat diakses melalui protokol IPv6 setelah akses IPv6 diaktifkan.

>! 
>- Beberapa platform sedang ditingkatkan, akses IPv6 saat ini tidak didukung. Silakan tunggu peluncuran resminya.
>- Akses IPv6 hanya tersedia di Tiongkok Daratan. Untuk nama domain akselerasi global, jika akses IPv6 diaktifkan, akses tersebut hanya akan diterapkan di Tiongkok Daratan. Adapun di luar Tiongkok Daratan, nama domain dengan akselerasi tidak dapat diaktifkan.|
>- Untuk nama domain akselerasi global dengan akses IPv6 diaktifkan, jika wilayah akselerasi dialihkan ke wilayah di luar Tiongkok Daratan, akses IPv6 akan dinonaktifkan secara otomatis dan tidak dapat diaktifkan.


