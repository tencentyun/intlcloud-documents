Fitur panggilan balik dinonaktifkan secara default untuk push CSS. Setelah nama domain push terikat ke konfigurasi panggilan balik, fitur panggilan balik akan diaktifkan untuk semua alamat push dengan nama domain ini. Jika peristiwa panggilan balik terpicu oleh templat yang telah dikonfigurasikan selama streaming langsung, Tencent Cloud akan mengirimkan permintaan ke server Anda yang bertanggung jawab atas respons tersebut. Setelah autentikasi, paket JSON yang berisi informasi panggilan balik deteksi pornografi dapat diperoleh.
Dokumen ini menjelaskan cara mengikat/melepaskan ikatan nama domain push ke/dari templat panggilan balik guna mengaktifkan/menonaktifkan fitur panggilan balik.



 
## Catatan
- Konfigurasi templat akan diterapkan dalam waktu sekitar 5–10 menit.
- Saat peristiwa CSS terpicu setelah fitur panggilan balik diaktifkan, Anda dapat menerima informasi peristiwa melalui [event message notification (pemberitahuan pesan peristiwa)](https://intl.cloud.tencent.com/document/product/267/38080).
- Templat panggilan balik dikelola di tingkat nama domain di konsol, dan aturan yang dibuat oleh API tidak dapat dibatalkan untuk saat ini. Jika Anda sudah mengikat templat ke streaming tertentu melalui API panggilan balik dan ingin melepaskan ikatan tersebut, Anda perlu memanggil API [DeleteLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30813).
- Satu nama domain hanya dapat diikatkan ke satu templat panggilan balik. Setelah pengikatan, panggilan balik akan dilakukan pada semua streaming yang diikat sesuai dengan templat ini.

## Prasyarat
- Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live) dan menambahkan [nama domain push](https://intl.cloud.tencent.com/document/product/267/35970).
- Anda telah membuat [templat panggilan balik](https://intl.cloud.tencent.com/document/product/267/31074).
<span id="related"></span>
## Mengikat Templat Panggilan Balik
1. 	Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **push domain name** (nama domain push) yang akan dikonfigurasikan atau **Manage** (Kelola) untuk membuka halaman detail nama domain.
2. 	Pilih **Template Configuration** (Konfigurasi Templat) dan klik **Edit** di bagian **Callback Configuration** (Konfigurasi Panggilan Balik).
![](https://main.qcloudimg.com/raw/d3e31f428ab1463335e234007c663311.png)
3. 	Pilih templat panggilan balik dan klik **Confirm** (Konfirmasi).
![](https://main.qcloudimg.com/raw/27f9da682e20283e25cc2478e1a53a0b.png)
<span id="untie"></span>
## Melepaskan Ikatan Templat Panggilan Balik

1. Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **push domain name** (nama domain push) yang akan dikonfigurasikan atau **Manage** (Kelola) untuk membuka halaman detail nama domain.
2. Pilih **Template Configuration** (Konfigurasi Templat) dan klik **Edit** di bagian **Callback Configuration** (Konfigurasi Panggilan Balik).
3. Hapus templat dan klik **Confirm** (Konfirmasi).
![](https://main.qcloudimg.com/raw/0f8ec4ae49d2f1c5329bdb509f056366.png)
