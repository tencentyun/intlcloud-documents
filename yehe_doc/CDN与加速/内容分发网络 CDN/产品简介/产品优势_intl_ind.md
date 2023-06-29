## Cadangan Sumber Daya yang Luas
### Simpul di Tiongkok daratan
CDN memiliki lebih dari 2000 simpul cache yang di-deploy ke semua provinsi di Tiongkok daratan dengan total cadangan bandwidth di atas 110 Tbps.Semua simpul cache tersebut merupakan pusat data Tencent Cloud berperforma tinggi dan sangat aman dengan jaringan ISP berkualitas.Selain itu, Tencent Cloud telah memperkuat koneksi dengan China Mobile, China Unicom, China Telecom, dan lebih dari 50 ISP ukuran kecil dan sedang serta sudah membangun empat simpul sentral untuk meningkatkan efek akselerasi CDN secara signifikan.
![img](https://main.qcloudimg.com/raw/c7af2903e117b831a68bbaaf13967181.png)

### Simpul di luar Tiongkok daratan
CDN sudah lama menggarap akselerasi global sejak 2017.Hingga Mei 2021, CDN memiliki lebih dari 800 simpul cache di lebih dari 70 negara dan wilayah dengan total cadangan bandwidth di atas 50 Tbps sehingga memudahkan dan mempercepat bisnis Anda terjun ke kancah global.
![image-20200210165753661](https://main.qcloudimg.com/raw/034a95d5f46fb8bf848c0a53dd265611.png)

| Wilayah | Distribusi |
| ------ | ------------------------------------------------------------ |
| Asia   | Hong Kong (Tiongkok), Taiwan (Tiongkok), Makau (Tiongkok), Jepang, Korea, Vietnam, Singapura, Thailand, <br/>Filipina, Malaysia, Indonesia, India, Turki, Arab Saudi, UEA, Myanmar, <br/>Kamboja, Irak, Kuwait, Qatar, Oman, Israel, Mongolia |
| Amerika Utara   | Amerika Serikat, Kanada, Meksiko                                         |
| Amerika Selatan   | Brasil, Argentina, Kolombia, Peru, Ekuador, Chili                 |
| Eropa   | Inggris, Jerman, Italia, Polandia, Swedia, Irlandia, Romania, <br/>Spanyol, Portugal, Prancis, Belanda, Belgia, Austria, Denmark, Finlandia |
| Afrika   | Afrika Selatan, Mesir, Tanzania                                         |
| Oseania | Australia, Selandia Baru                                             |

## Penjadwalan Cerdas Global

Ketika mengakses sumber daya, beragam faktor termasuk jaringan ISP, wilayah klien, dan bandwidth jaringan dari server asal IDC dapat memengaruhi waktu tanggapan dan pengalaman pengguna.

Melalui pemantauan real-time terhadap tautan di seluruh jaringan dan pemanfaatan sistem penjadwalan GSLB rancangan Tencent Cloud sendiri serta teknologi perutean cerdas, CDN menjadwalkan permintaan akses pengguna ke simpul edge untuk mendapatkan akselerasi.Hal ini memberikan kepastian akses sumber daya yang cepat dan stabil bagi pengguna.

## Konfigurasi Cepat
Anda dapat menggunakan CDN untuk mempercepat layanan melalui proses konfigurasi yang sederhana dan cepat tanpa membutuhkan modifikasi tambahan.

Setelah mendaftar akun Tencent Cloud dan menyelesaikan verifikasi identitas, Anda dapat mengaktifkan layanan CDN.Tidak perlu pembayaran di muka.Tambahkan nama domain bisnis Anda di Konsol CDN dan tunggu sekitar 5 menit sampai konfigurasi nama domain tersebar ke simpul cache di seluruh jaringan.Selama proses ini, bisnis Anda tidak akan terpengaruh karena layanan akselerasi belum aktif..

Ketika mengaktifkan layanan akselerasi, Anda perlu mengubah konfigurasi resolusi CNAME melalui penyedia layanan nama domain Anda.Layanan akselerasi akan aktif ketika DNS aktif.

## Berbagai Fitur

CDN memiliki konsol yang mudah digunakan dan berfitur lengkap sehingga memudahkan Anda mengubah item konfigurasi dan melihat data pemantauan sesuai kebutuhan:

**Domain management** (Pengelolaan domain)
+ Anda dapat menambahkan, menghapus, mengaktifkan, dan menonaktifkan nama domain.
+ Anda dapat beralih wilayah akselerasi dan memilih ""Tiongkok Daratan"", ""Di Luar Tiongkok Daratan"", atau ""Global"" untuk lingkup akselerasi.
+ Anda dapat menyesuaikan halaman daftar nama domain untuk menampilkan, memfilter, dan mengueri item konfigurasi.

**Domain configuration** (Konfigurasi domain)
+ Anda dapat mengonfigurasi server asal eksternal (daftar IP atau nama domain) atau menggunakan COS sebagai server asal.Server asal dengan corak round robin, tarik-asal berbobot, dan hot backup didukung.
+ Anda dapat mengonfigurasi kebijakan kontrol akses khusus, seperti daftar blokir/daftar izin referer, daftar blokir/daftar izin IP, perlindungan hotlink stempel waktu, dan batas frekuensi akses IP.
+ Anda dapat menyesuaikan waktu kedaluwarsa simpul cache, status cache kode, dan HTTP header cache.
+ CDN mendukung pengoptimalan konfigurasi untuk tautan lintas batas tarik-asal, range GETs, dan 301/302 tarik-asal ikuti-alihkan.
+ CDN mendukung akselerasi HTTPS, akselerasi HTTP/2, dan pengarahan kembali permintaan terpaksa.
+ Anda dapat mengonfigurasi batas bandwidth dan menyesuaikan item konfigurasi lanjut, seperti header tanggapan HTTP, kompresi otomatis, dan SEO.

*Cache purge** (Pembersihan cache)
+ Pembersihan mandiri terhadap seluruh cache jaringan, pembersihan direktori, dan pembersihan URL didukung semuanya.

**Real-time monitoring** (Pemantauan real-time)
+ CDN mendukung pemantauan real-time terhadap lalu lintas bandwidth, lalu lintas hit rate, jumlah permintaan, dan semua kode status yang dihasilkan oleh permintaan akses hingga sekecil 1 menit.Statistik dapat difilter berdasarkan proyek, nama domain, provinsi, ISP, dan protokol sehingga dapat menyajikan tampilan status layanan yang menyeluruh.
+ CDN mendukung pemantauan real-time terhadap bandwidth tarik-asal, lalu lintas, jumlah permintaan, tingkat kegagalan, dan semua kode status yang dihasilkan oleh permintaan tarik-asal hingga sekecil 1 menit.Statistik dapat difilter berdasarkan nama proyek atau domain untuk memudahkan Anda melihat status server asal.
+ Anda dapat melihat laporan real-time persebaran pengguna berdasarkan wilayah di seluruh dunia atau berdasarkan ISP di Tiongkok daratan.
+ CDN memberikan laporan operasional harian, mingguan, dan bulanan untuk terus mengabari Anda tentang fluktuasi bisnis.

**Log service** (Layanan log)
+ Semua log yang dihasilkan oleh permintaan akses dikelompokkan berdasarkan jam dan dapat diunduh.
+ Log akses CDN dapat dikumpulkan dan dipublikasikan secara real time agar dapat mencari dan menganalisis data log dengan cepat.

**CDN APIs** (CDN API)
CDN memberikan [API](https://intl.cloud.tencent.com/document/product/228/31719) untuk semua fitur yang didukung dan tercantum di atas untuk mengaktifkan penggunaan layanan yang sudah disesuaikan.Anda bersama tim dapat dengan mudah mengelola, memantau, menampilkan, dan menganalisis bisnis melalui API tersebut.
