## Ikhtisar Konfigurasi

CDN mendukung berbagai konfigurasi khusus dan Anda dapat menyesuaikannya berdasarkan kebutuhan bisnis Anda.

### Konfigurasi dasar

Konfigurasi dasar adalah konten yang diperlukan untuk akselerasi CDN, termasuk konfigurasi server asal dan informasi layanan akselerasi dasar seperti wilayah akselerasi dan jenis layanan, dll.

| Konfigurasi                                                     | Deskripsi                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Informasi Dasar](https://intl.cloud.tencent.com/document/product/228/7864) | Memodifikasi informasi dasar seperti proyek, wilayah akselerasi, dan jenis layanan, dll.         |
| [Konfigurasi Server Asal](https://intl.cloud.tencent.com/document/product/228/6289) | Mengonfigurasi tarik-asal round-robin multi-IP, tarik-asal berbasis nama domain, tarik-asal round-robin berbobot, domain asal, dan protokol tarik-asal.<br/>Mendukung konfigurasi server asal hot backup.<br/ >**Untuk nama domain akselerasi global, akselerasi di dalam dan di luar Tiongkok Daratan dapat dikonfigurasi secara terpisah.** |

### Kontrol akses

Anda dapat mengonfigurasi berbagai aturan berdasarkan permintaan pengguna untuk mengizinkan atau memblokir permintaan akses.

| Konfigurasi                                                     | Deskripsi                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Perlindungan Hotlink](https://intl.cloud.tencent.com/document/product/228/6292) | Mendukung pengaturan daftar izin dan daftar blokir referer untuk menentukan apakah mengizinkan atau menolak permintaan akses HTTP berdasarkan header referer permintaan.<br/>**Untuk nama domain akselerasi global, akselerasi di dalam dan di luar Tiongkok Daratan dapat dikonfigurasi secara terpisah.** |
| [Daftar Blokir/Daftar Izin IP](https://intl.cloud.tencent.com/document/product/228/6298) | Mendukung pengaturan daftar izin dan daftar blokir IP untuk menentukan apakah mengizinkan atau menolak permintaan akses HTTP berdasarkan IP klien permintaan.<br/>**Untuk nama domain akselerasi global, akselerasi di dalam dan di luar Tiongkok Daratan dapat dikonfigurasi secara terpisah.** |
| [Batas Akses IP](https://intl.cloud.tencent.com/document/product/228/6420) | Membatasi frekuensi dengan IP dapat mengakses satu simpul untuk menolak permintaan akses dari IP klien yang melebihi batas. |
| [Autentikasi](https://intl.cloud.tencent.com/document/product/228/35237) | Mendukung berbagai algoritme tanda tangan stempel waktu dan aturan untuk konfigurasi anti-hotlink.<br/>**Untuk nama domain akselerasi global, akselerasi di dalam dan di luar Tiongkok Daratan dapat dikonfigurasi secara terpisah.** |
| [Menyeret Video](https://intl.cloud.tencent.com/document/product/228/8111) | Ini dirancang untuk akselerasi VOD streaming.<br/>Dengan mengaktifkan fitur menyeret video, Anda dapat menentukan titik awal video melalui parameter `start`.|
| [Daftar Izin/Daftar Blokir UA](https://intl.cloud.tencent.com/document/product/228/37256) | Menentukan apakah akan menolak atau mengizinkan permintaan menurut header permintaan HTTP `User-Agent`. |
| [Batas Kecepatan Downstream](https://intl.cloud.tencent.com/document/product/228/37257) | Mengontrol bandwidth akses CDN dengan mengatur batas kecepatan downstream pada URL. |

### Konfigurasi cache

Konfigurasi cache mengontrol cache pada simpul CDN.

| Konfigurasi                                                     | Deskripsi                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Abaikan String Kueri](https://intl.cloud.tencent.com/document/product/228/35316) | Untuk cache sumber daya, ini mendukung konfigurasi apakah akan mengabaikan parameter setelah "?" di URL akses.<br/>**Sebaiknya nonaktifkan fitur ini jika parameter setelah "?" menunjukkan konten bisnis Anda yang berbeda.** |
| [Validitas Cache Simpul](https://intl.cloud.tencent.com/document/product/228/35317) | Mendukung konfigurasi validitas cache file pada simpul berdasarkan jalur dan jenis file. |
| [Cache Kode Status](https://intl.cloud.tencent.com/document/product/228/35318) | Mendukung konfigurasi validitas cache kode status untuk simpul CDN untuk merespons kode status 2XX secara langsung sehingga mengurangi tekanan pada server asal. |
| [Cache Header HTTP](https://intl.cloud.tencent.com/document/product/228/35319) | Ini dapat dinonaktifkan sesuai kebutuhan. Simpul CDN meng-cache semua header respons server asal secara default. |
| [Cache Abaikan Huruf Besar-Kecil URL](https://intl.cloud.tencent.com/document/product/228/35316) | Cache simpul CDN tidak mengabaikan huruf besar-kecil secara default. Huruf besar dapat diabaikan sesuai kebutuhan. |
| [Tulis Ulang URL Akses](https://intl.cloud.tencent.com/document/product/228/38074)| Mendukung penyesuaian konfigurasi penulisan ulang URL untuk mengalihkan permintaan dari URL dengan kode status 302 ke URL target.|


### Konfigurasi tarik-asal

Konfigurasi tarik-asal mengontrol proses penerusan permintaan dari simpul CDN ke server asal.

| Konfigurasi                                                     | Deskripsi                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Range GETs](https://intl.cloud.tencent.com/document/product/228/7184) | Range GETs digunakan untuk tarik-asal secara default. Jika tidak didukung oleh server asal Anda, Anda dapat menonaktifkannya. |
| [Header Permintaan](https://intl.cloud.tencent.com/document/product/228/37037) | Menambahkan header yang ditentukan selama tarik-asal seperti IP klien sebenarnya. |
| [Ikuti 301/302](https://intl.cloud.tencent.com/document/product/228/7183) | Ini dapat diaktifkan untuk tarik-asal sesuai kebutuhan. |
| [Waktu Habis Origin-pull](https://intl.cloud.tencent.com/document/product/228/35227) | Mengonfigurasi periode waktu habis koneksi TCP (yang secara default adalah 5 detik) dan periode pemuatan (yang secara default adalah 10 detik) dari tarik-asal. |

### Konfigurasi akselerasi HTTPS

Akselerasi HTTPS mendukung berbagai konfigurasi terkait HTTPS.

| Konfigurasi                                                     | Deskripsi                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Konfigurasi HTTPS](https://intl.cloud.tencent.com/document/product/228/35213) | Mendukung pengunggahan sertifikat milik sendiri atau sertifikat yang di-hosting untuk mengaktifkan akselerasi HTTPS. |
| [Konfigurasi HTTP2.0](https://intl.cloud.tencent.com/document/product/228/35215) | Dengan mengaktifkannya, server edge CDN dapat mendukung HTTP2.0.<br/>**Silakan konfigurasikan sertifikat terlebih dahulu untuk mengaktifkan HTTP2.0.** |
| [Konfigurasi Pengalihan Paksa](https://intl.cloud.tencent.com/document/product/228/35214) | Pengalihan paksa dari HTTPS ke akses HTTP dapat dicapai dengan atau tanpa sertifikat.<br/>Pengalihan paksa dari akses HTTP ke HTTPS memerlukan sertifikat. |
| [OCSP Stapling](https://intl.cloud.tencent.com/document/product/228/35216) | Dengan mengaktifkan konfigurasi ini, OCSP stapling didukung.<br/>**Lakukan konfigurasi dulu pada sertifikat untuk mengaktifkan OCSP stapling.** |
| [Konfigurasi HSTS](https://intl.cloud.tencent.com/document/product/228/37036) | Jika diaktifkan, header `strict-transport-security` akan ditambahkan.<br/>**Lakukan konfigurasi dulu pada sertifikat untuk mengaktifkan konfigurasi HSTS.** |

### Konfigurasi lanjutan

| Konfigurasi                                                     | Deskripsi                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Konfigurasi Batas Pemakaian Bandwidth](https://intl.cloud.tencent.com/document/product/228/7541) | Mendukung konfigurasi batas pemakaian bandwidth untuk akselerasi di dalam dan di luar Tiongkok Daratan. Layanan akselerasi dapat dihentikan sesuai kebutuhan jika batasnya terlampaui. <br/>**Untuk nama domain akselerasi global, akselerasi di dalam dan di luar Tiongkok Daratan dapat dikonfigurasi secara terpisah.** |
| [Konfigurasi SEO](https://intl.cloud.tencent.com/document/product/228/35219) | Mendukung secara otomatis untuk mengenali apakah IP akses milik mesin pencari.<br/>Jika ya, permintaan dari IP akan diteruskan ke server asal untuk menjamin stabilitas bobot mesin pencari. |
| [Konfigurasi Header Respons](https://intl.cloud.tencent.com/document/product/228/35320) | Menetapkan header respons HTTP sesuai kebutuhan dan menambahkannya ke permintaan respons ke klien. |
| [Konfigurasi Kompresi Pintar](https://intl.cloud.tencent.com/document/product/228/35220) | Melakukan kompresi Gzip atau Brotli pada file tertentu berdasarkan jenis dan rentang file. |


