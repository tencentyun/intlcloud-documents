

## Ikhtisar Konfigurasi
HTTP2.0 adalah versi HTTP terbaru yang sangat meningkatkan kinerja web dan mengurangi penundaan jaringan lebih jauh. HTTP2.0 dapat langsung diaktifkan untuk nama domain dengan sertifikat yang dikonfigurasi dan akselerasi HTTPS yang diaktifkan.
> !Saat ini, hanya akses HTTP2.0 yang didukung. Tarik-asal HTTP2.0 tidak didukung.


## Panduan Konfigurasi
### Melihat konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Buka tab **HTTPS Configuration** (Konfigurasi HTTPS) untuk menemukan **HTTP2.0 Configuration** (Konfigurasi HTTP2.0), yang diaktifkan secara default.
![](https://main.qcloudimg.com/raw/78075916f06b8cc5b03a75ac86786fe3.png)

### Memodifikasi konfigurasi
Alihkan switch untuk mengaktifkan atau menonaktifkan HTTP2.0. Jika sertifikat nama domain dihapus, HTTP2.0 akan dinonaktifkan secara otomatis.
![](https://main.qcloudimg.com/raw/b4e746132ced3995845c0af895408324.png)

> !Jika nama domain dikonfigurasi untuk akselerasi global, konfigurasi HTTP2.0 akan diterapkan ke wilayah global, terlepas dari apakah wilayah tersebut berada di dalam atau di luar Tiongkok Daratan.
> 