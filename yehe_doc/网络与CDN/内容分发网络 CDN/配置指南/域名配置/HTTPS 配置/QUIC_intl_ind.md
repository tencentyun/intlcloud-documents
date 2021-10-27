## Ikhtisar Fitur

Quick UDP Internet Connections (QUIC) adalah protokol jaringan umum, yang menjamin keamanan jaringan dan mengurangi latensi dalam transfer dan koneksi untuk mencegah kemacetan jaringan. Anda dapat mengaktifkan protokol QUIC untuk klien untuk mengakses simpul CDN dengan keamanan transfer data dan efisiensi akses yang ditingkatkan.

Saat ini, versi QUIC berikut didukung secara default: draft h3-28, h3-Q050, h3-Q046, h3-Q043, Q046, dan Q043.

Versi beta dari QUIC CDN Tencent Cloud telah dirilis. Anda dapat [mengajukan permohonan](https://intl.cloud.tencent.com/apply/p/g0lwu71z0i7), dan setelah itu kami akan meninjau permohonan Anda dalam waktu 15 hari kerja.



## Panduan Beta

Jika permohonan Anda disetujui, Anda dapat membuka konsol CDN untuk mengaktifkan QUIC untuk nama domain baru Anda untuk melakukan pengujian.
>!
>- Setelah permohonan Anda disetujui, QUIC hanya dapat diaktifkan untuk nama domain baru tetapi tidak untuk nama domain yang sudah ada.
>- QUIC saat ini tersedia dalam versi beta di konsol CDN, oleh karena itu, kami sarankan hanya aktifkan QUIC untuk nama domain pengujian Anda, bukan nama domain bisnis apa pun.
>- Berpindah jenis layanan menyangkut penjadwalan sumber daya antar platform. Kami menyarankan untuk tidak mengganti jenis layanan untuk nama domain setelah mengaktifkan QUIC.
>- Tarik-asal QUIC saat ini tidak didukung.


Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn) dan beri centang pada kotak untuk mengaktifkan QUIC saat menghubungkan nama domain baru:
![](https://main.qcloudimg.com/raw/2098308cd8a8c1a0321c0164646b7700.png)
**Batasan konfigurasi:**

- QUIC saat ini tidak dapat diaktifkan untuk nama domain apa pun dari jenis layanan akselerasi streaming VOD.
- QUIC tidak dapat diaktifkan untuk nama domain apa pun dengan IPv6 yang diaktifkan.


Setelah berhasil menghubungkan nama domain, Anda dapat mengeklik **Domain Management** (Pengelolaan Domain) di bilah samping kiri, masuk ke halaman detail nama domain, dan buka tab **HTTPS Configuration** (Konfigurasi HTTPS) untuk menemukan bagian konfigurasi QUIC. Konfigurasinya dinonaktifkan secara default, dan Anda dapat mengaktifkannya secara langsung.
**Catatan:** Silakan konfigurasikan sertifikat HTTPS terlebih dahulu untuk mengaktifkannya.
![](https://main.qcloudimg.com/raw/e697e32b39948d56610285c80043f1de.png)



## Penagihan

QUIC saat ini dalam versi beta di konsol CDN. Ini adalah layanan bernilai tambah dan saat ini tersedia secara gratis.

