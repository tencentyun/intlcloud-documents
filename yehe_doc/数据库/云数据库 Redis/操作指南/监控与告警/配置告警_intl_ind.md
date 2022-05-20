
## Ikhtisar
Agar operasi normal sistem Anda tidak terpengaruh saat metrik pemantauan mencapai nilai tertentu, Anda dapat mengonfigurasi aturan alarm untuk metrik ini. Ketika data pemantauan memenuhi kondisi yang dikonfigurasi, sistem dapat secara otomatis memeriksanya dan mengirim notifikasi alarm ke admin. Ini membantu Anda tetap berada di atas pengecualian bisnis dan menyelesaikannya dengan cepat. 

## Penagihan
- CM memungkinkan Anda mengonfigurasi kebijakan alarm untuk memantau metrik kunci instans dan menawarkan uji coba gratis.
- Saat ini, hanya **alarm SMS messages** (pesan SMS alarm) yang dikenakan biaya. Untuk informasi selengkapnya, lihat [Panduan Pembelian](https://intl.cloud.tencent.com/document/product/248/18728).

## Prasyarat
- Anda telah mengaktifkan CM.
- Instans database dalam status **Running** (Berjalan).
- Anda telah mengumpulkan informasi tentang penerima notifikasi alarm, seperti alamat email dan nomor telepon.

## Petunjuk
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis).
2. Di atas **instance list** (daftar instans) di sebelah kanan, pilih wilayah.
3. Dalam daftar instans, temukan instans target.
4. Di baris instans target, masuk ke halaman **Create Policy** (Buat Kebijakan) dari CM dengan salah satu cara berikut:
   - Klik <img src="https://qcloudimg.tencent-cloud.cn/raw/8e01de7cd5dd07c6d2626aaba4c2288c.png" style="zoom: 50%;" /> di kolom **Monitoring/Status/Task** (Pemantauan/Status/Tugas) dan klik **Configure Alarms** (Konfigurasikan Alarm) di sudut kanan atas panel data pemantauan instans.
     ![](https://main.qcloudimg.com/raw/ee9553aef95de034ecb4c505a573d75f.png)
   - Di daftar instans, klik **Instance ID** (ID instans) dengan warna biru untuk masuk ke halaman **Instance Details** (Detail Instans). Kemudian, klik tab **System Monitoring** (Pemantauan Sistem), pilih tab **Monitoring Metrics** (Metrik Pemantauan), dan klik **Set Alarms** (Atur Alarm).
     ![](https://qcloudimg.tencent-cloud.cn/raw/9b942bdb2f05a028fda4639c3946065b.png)
5. Pada halaman **Create Policy** (Buat Kebijakan), konfigurasikan kebijakan seperti yang ditunjukkan di bawah ini. Untuk informasi selengkapnya, lihat [Membuat Kebijakan Alarm](https://intl.cloud.tencent.com/document/product/248/38916).
   ![](https://main.qcloudimg.com/raw/e164f26773457a00ca7e153383f51390.png)
<table>
<thead><tr><th>Deskripsi</th><th>Parameter</th></tr></thead>
<tbody><tr>
<td>Nama Kebijakan</td><td>Sesuaikan nama kebijakan alarm untuk identifikasi yang lebih mudah.</td></tr>
<tr>
<td>Keterangan</td><td>Jelaskan secara singkat kebijakan alarm untuk identifikasi yang lebih mudah.</td></tr>
<tr>
<td>Jenis Pemantauan</td><td>Pilih <strong>Pemantauan Produk Cloud</strong>.</td></tr>
<tr>
<td>Jenis Kebijakan</td>
<td>Pilih <strong>TencentDB/Redis/Edisi Memori (Granularitas 5 Detik)/Node Redis</strong> atau <strong>TencentDB/Redis/Edisi Memori (Granularitas 1 Menit)/Node Redis</strong> sesuai kebutuhan.</td></tr>
<tr>
<td>Proyek</td>
<td>Tentukan proyek untuk kebijakan alarm. Anda dapat menemukan semua kebijakan alarm proyek dengan cepat dalam daftar kebijakan alarm.</td></tr>
<tr>
<td>Objek Alarm</td>
<td>Pilih objek alarm berdasarkan <strong>ID instans</strong> atau <strong>grup instans</strong>. Untuk informasi selengkapnya tentang grup instans, lihat <a href="https://intl.cloud.tencent.com/document/product/248/35268">Grup Instans</a>.</td></tr>
<tr>
<td rowspan=3>Kondisi Pemicu</td>
<td>Konfigurasikan kondisi pemicu alarm dengan <strong>memilih templat</strong> atau melalui <strong>konfigurasi manual</strong>. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/248/38916">Membuat Kebijakan Alarm</a>.</td></tr>
<tr>
<td>Notifikasi Alarm</td>
<td>Pilih templat notifikasi prasetel atau kustom. Setiap kebijakan alarm dapat terikat ke maksimal tiga templat notifikasi. Untuk informasi selengkapnya, <a href="https://cloud.tencent.com/document/product/248/50394">Templat Notifiikasi Alarm</a>.</td></tr>
</tbody></table>
6. Setelah mengonfirmasi bahwa semuanya sudah benar, klik **Complete** (Selesai). Untuk informasi selengkapnya tentang alarm, lihat [Ikhtisar Alarm](https://Intl.cloud.tencent.com/document/product/248/6126).

## API Terkait
| API                                                      | Deskripsi |
| :----------------------------------------------------------- | :------------------- |
| [CreateAlarmPolicy](https://intl.cloud.tencent.com/document/product/248/39326) | Membuat kebijakan alarm CM |


