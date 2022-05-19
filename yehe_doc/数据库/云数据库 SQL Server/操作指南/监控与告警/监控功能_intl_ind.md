Untuk memudahkan Anda melihat dan mengikuti perkembangan kondisi instans, TencentDB for SQL Server menyediakan beragam metrik pemantauan performa dan fitur pemantauan yang nyaman (seperti tampilan kustom, perbandingan waktu, dan metrik pemantauan gabungan).
>?Jika jumlah tabel dalam satu instans melebihi satu juta, pemantauan database mungkin terpengaruh. Pastikan jumlah tabel dalam satu instans di bawah satu juta.

## Jenis Instans untuk Pemantauan
Instans utama dan hanya baca TencentDB for SQL Server dapat dipantau, dan setiap instans disediakan dengan tampilan pemantauan terpisah untuk kueri yang mudah.

## Melihat Data Pemantauan
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pilih tab **System Monitoring** (Pemantauan Sistem) untuk melihat informasi pemantauan setiap metrik instans.
>?
>- Pemantauan TencentDB for SQL Server mendukung perincian hingga 10 detik.
>- Saat ini, Anda dapat melihat data pemantauan TencentDB for SQL Server dalam 180 hari terakhir.

## Metrik Pemantauan
Pemantauan TencentDB for SQL Server mendukung 37 metrik umum SQL Server. Anda dapat mengumpulkan statistik metrik lain dengan mengonfigurasi penghitung performa Studio Manajemen Server SQL (SSMS).
>?Untuk melihat metrik pemantauan di tingkat sistem, [kirim tiket](https://console.cloud.tencent.com/workorder/category). 

<table>
<thead>
<tr><th>Kategori</th><th>Metrik</th><th>Parameter</th><th>Unit</th><th>Deskripsi</th></tr></thead>
<tbody><tr>
<td>CPU</td>
<td>Total waktu prosesor</td><td>Total Waktu Prosesor</td><td>%</td><td>Penggunaan CPU aktual</td></tr>
<tr>
<td rowspan=3>Memori</td>
<td>Penggunaan memori</td><td>Memori server</td><td>MB</td><td>Ukuran memori total yang digunakan</td></tr>
<tr>
<td>Memori maksimum</td><td>Memori maksimum</td><td>KB</td><td>Memori maksimum</td></tr>
<tr>
<td>Penggunaan memori</td><td>Penggunaan Memori</td><td>%</td><td>Penggunaan memori</td></tr>
<tr>
<td rowspan=12>Penyimpanan</td>
<td>IOPS Disk</td><td>IOPS</td><td>jumlah/dtk</td><td>Jumlah pembacaan/penulisan disk</td></tr>
<tr>
<td>Pembacaan disk</td><td>Baca IOPS</td><td>jumlah/dtk</td><td>Jumlah pembacaan disk per detik</td></tr>
<tr>
<td>Penulisan disk</td><td>Tulis IOPS</td><td>jumlah/dtk</td><td>Jumlah penulisan disk per detik</td></tr>
<tr>
<td>Ruang penyimpanan yang digunakan</td><td>Ruang Penyimpanan</td><td>GB</td><td>Jumlah ruang yang digunakan oleh file database instans dan file log</td></tr>
<tr>
<td>Ruang penyimpanan kosong</td><td>Penyimpanan Gratis</td><td>%</td><td>Persentase ruang disk kosong dihitung dengan cara berikut: (ruang disk yang dibeli - ruang penyimpanan yang digunakan) / ruang disk yang dibeli</td></tr>
<tr>
<td>Waktu respons IO rata-rata yang dibaca</td><td>Rata-rata. Disk Sec/Read</td><td>md</td><td>Waktu respons rata-rata untuk setiap IO pembacaan (pemantauan di tingkat sistem)</td></tr>
<tr>
<td>Waktu respons IO tulis rata-rata</td><td>Rata-rata. Disk Sec/Write</td><td>md</td><td>Waktu respons rata-rata untuk setiap IO penulisan (pemantauan di tingkat sistem)</td></tr>
<tr>
<td>Waktu respons IO rata-rata</td><td>Rata-rata. Disk sec/Transfer</td><td>md</td><td>Waktu respons rata-rata untuk setiap permintaan IO (pemantauan di tingkat sistem)</td></tr>
<tr>
<td>IO pembacaan disk per detik</td><td>Pembacaan Disk /dtk</td><td>jumlah/dtk</td><td>Jumlah IO pembacaan disk per detik (pemantauan di tingkat sistem)</td></tr>
<tr>
<td>IO penulisan disk per dtk</td><td>Penulisan Disk/dtk</td><td>jumlah/dtk</td><td>Jumlah IO penulisan disk per detik (pemantauan di tingkat sistem)</td></tr>
<tr>
<td>Total IOPS disk</td><td>Transfer Disk/dtk</td><td>jumlah/dtk</td><td>Jumlah total IOPS disk (pemantauan di tingkat sistem)</td></tr>
<tr>
<td>Panjang antrean disk</td><td>Panjang Antrean Disk</td><td>-</td><td>Panjang antrean disk (pemantauan di tingkat sistem)</td></tr>
<tr>
<td rowspan=3>Jaringan</td>
<td>Lalu lintas masuk</td><td>Troughput Penerimaan Jaringan</td><td>KB/dtk</td><td>Jumlah semua paket masuk semua koneksi</td></tr>
<tr>
<td>Lalu lintas keluar</td><td>Troughput Transmisi Jaringan</td><td>KB/dtk</td><td>Jumlah semua paket keluar dari semua koneksi</td></tr>
<tr>
<td>Penundaan IO jaringan</td><td>Penundaan IO jaringan</td><td>md</td><td>Waktu penundaan IO jaringan rata-rata</td></tr>
<tr>
<td rowspan=3>Koneksi</td>
<td>Koneksi pengguna</td><td>Koneksi Pengguna</td><td>-</td><td>Jumlah rata-rata koneksi pengguna ke database per detik</td></tr>
<tr>
<td>Login/dtk</td><td>Login/dtk</td><td>jumlah/dtk</td><td>Jumlah login per detik</td></tr>
<tr>
<td>Logout/dtk</td><td>Logout/dtk</td><td>jumlah/dtk</td><td>Jumlah logout per detik</td></tr>
<tr>
<td rowspan=9>Akses</td>
<td>Kueri lambat</td><td>SlowQuery</td><td>-</td><td>Jumlah kueri yang berjalan selama lebih dari satu detik</td></tr>
<tr>
<td>Permintaan batch/dtk</td><td>Permintaan Batch</td><td>jumlah/dtk</td><td>Jumlah rata-rata permintaan per detik</td></tr>
<tr>
<td>Kompilasi SQ/dtk</td><td>Kompilasi SQL/dtk</td><td>jumlah/dtk</td><td>Jumlah rata-rata kompilasi SQL per detik</td></tr>
<tr>
<td>Kompilasi ulang SQL/dtk</td><td>Kompilasi ulang SQL/dtk</td><td>jumlah/dtk</td><td>Jumlah rata-rata kompilasi ulang SQL per detik</td></tr>
<tr>
<td>Pemindaian penuh/dtk</td><td>Pemindaian Penuh/dtk</td><td>jumlah/dtk</td><td>Jumlah pemindaian penuh per detik</td></tr>
<tr>
<td>Transaksi/dtk</td><td>Transaksi/dtk</td><td>jumlah/dtk</td><td>Jumlah transaksi per detik</td></tr>
<tr>
<td>Proses diblokir</td><td>Proses diblokir</td><td>-</td><td>Jumlah proses saat ini diblokir</td></tr>
<tr>
<td>Rasio hit cache rencana</td><td>Plan Cache:Rasio Hit Cache</td><td>%</td><td>Rasio hit dari rencana eksekusi setiap SQL</td></tr>
<tr>
<td>Rasio hit cache buffer</td><td>Rasio hit cache buffer</td><td>%</td><td>Rasio hit cache buffer (memori)</td></tr>
<tr>
<td rowspan=5>Kunci</td>
<td>Permintaan penguncian/dtk</td><td>Permintaan Penguncian/dtk</td><td>jumlah/dtk</td><td>Jumlah rata-rata permintaan penguncian per detik</td></tr>
<tr>
<td>Penundaan latch/dtk</td><td>Penundaan latch/dtk</td><td>hitungan/dtk</td><td>Jumlah waktu tunggu latch per detik</td></tr>
<tr>
<td>Waktu tunggu rata-rata</td><td>Waktu tunggu rata-rata</td><td>Md</td><td>Waktu tunggu rata-rata untuk setiap permintaan penguncian yang menyebabkan menunggu</td></tr>
<tr>
<td>Deadlock</td><td>Jumlah deadlock/dtk</td><td>jumlah/dtk</td><td>Jumlah permintaan penguncian yang menyebabkan deadlock per detik</td></tr>
<tr>
<td>Ambang proses yang diblokir</td><td>Ambang batas proses yang diblokir</td><td>dtk</td>
<td>Ini adalah ambang yang ditentukan untuk membuat laporan proses yang diblokir. Jika terlampaui, laporan proses yang diblokir akan dibuat. Secara default, tidak ada laporan proses yang diblokir yang akan dibuat</td></tr>
<tr>
<td>Lainnya</td>
<td>Kesalahan pengguna</td><td>Kesalahan Pengguna/dtk</td><td>jumlah/dtk</td><td>Jumlah rata-rata kesalahan per detik</td></tr>
</tbody></table>
