Untuk memudahkan Anda melihat dan terus mengetahui kondisi instans, TencentDB for SQL Server menyediakan berbagai metrik pemantauan kinerja dan fitur pemantauan yang nyaman (seperti tampilan kustom, perbandingan waktu, dan metrik pemantauan gabungan).
>?Jika jumlah tabel dalam satu instans melebihi satu juta, pemantauan database mungkin terpengaruh. Pastikan jumlah tabel dalam satu instans di bawah satu juta.

## Jenis Instans untuk Pemantauan
Instans utama dan baca saja TencentDB for SQL Server dapat dipantau, dan setiap instans dilengkapi dengan tampilan pemantauan terpisah untuk kueri yang mudah

## Melihat Data Pemantauan
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pilih tab **System Monitoring** (Pemantauan Sistem) untuk melihat informasi pemantauan setiap metrik instans.
>?
>- Pemantauan TencentDB for SQL Server mendukung glanularitas hingga 10 detik.
>- Saat ini, Anda dapat melihat data pemantauan TencentDB for SQL Server dalam 180 hari terakhir.

## Metrik Pemantauan
Pemantauan TencentDB for SQL Server mendukung 37 metrik umum SQL Server. Anda dapat mengumpulkan statistik metrik lain dengan cara mengonfigurasi penghitung kinerja SQL Server Management Studio (SSMS).
>?Untuk melihat metrik pemantauan di tingkat sistem, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category). 

<table>
<thead>
<tr><th>Kategori</th><th>Metrik</th><th>Parameter</th><th>Unit</th><th>Deskripsi</th></tr></thead>
<tbody><tr>
<td>CPU</td>
<td>Total waktu prosesor</td><td>Total waktu prosesor</td><td>%</td><td>Penggunaan CPU yang sebenarnya</td></tr>
<tr>
<td rowspan=3>Memori</td>
<td>Penggunaan memori</td><td>Memori server</td><td>MB</td><td>Ukuran yang digunakan dari total memori</td></tr>
<tr>
<td>Memori maksimal</td><td>Memori maksimal</td><td>KB</td><td>Memori maksimal</td></tr>
<tr>
<td>Pemanfaatan memori</td><td>Penggunaan Memori</td><td>%</td><td>Pemanfaatan memori</td></tr>
<tr>
<td rowspan=12>Penyimpanan</td>
<td>Disk IOPS</td><td>IOPS</td><td>hitungan/detik</td><td>Jumlah pembacaan/penulisan disk</td></tr>
<tr>
<td>Pembacaan disk</td><td>Membaca  IOPS</td><td>hitungan/detik</td><td>Jumlah pembacaan disk per detik</td></tr>
<tr>
<td>Penulisan disk</td><td>Menulis  IOPS</td><td>hitungan/detik</td><td>Jumlah penulisan disk per detik</td></tr>
<tr>
<td>Ruang penyimpanan yang digunakan</td><td>Ruang Penyimpanan</td><td>GB</td><td>Jumlah ruang yang digunakan oleh file database instans dan file log</td></tr>
<tr>
<td>Ruang penyimpanan kosong</td><td>Penyimpanan Kosong</td><td>%</td><td>Persentase ruang disk kosong yang dihitung dengan cara berikut: (ruang disk yang dibeli - ruang penyimpanan yang digunakan) / ruang disk yang dibeli</td></tr>
<tr>
<td>waktu respons IO baca rata-rata</td><td>Rata-rata. Disk Detik/Baca</td><td>milidetik</td><td>Waktu respons rata-rata setiap IO baca (pemantauan di tingkat sistem)</td></tr>
<tr>
<td>Waktu respons IO tulis rata-rata</td><td>Rata-rata. Penulisan Disk/Detik</td><td>milidetik</td><td>Waktu respons rata-rata setiap IO tulis (pemantauan di tingkat sistem)</td></tr>
<tr>
<td>Waktu respons IO rata-rata</td><td>Rata-rata. Transfer Disk/detik</td><td>milidetik</td><td>Waktu respons rata-rata setiap permintaan IO (pemantauan di tingkat sistem)</td></tr>
<tr>
<td>Pembacaan disk IO per detik</td><td>Pembacaan Disk/detik</td><td>hitungan/detik</td><td>Jumlah pembacaan disk IO per detik (pemantauan di tingkat sistem)</td></tr>
<tr>
<td>Penulisan disk IO per detik</td><td>Penulisan Disk/detik</td><td>hitungan/detik</td><td>Jumlah penulisan disk IO per detik (pemantauan di tingkat sistem)</td></tr>
<tr>
<td>Total IOPS disk</td><td>Transfer Disk/detik</td><td>hitungan/detik</td><td>Jumlah total IOPS disk (pemantauan di tingkat sistem)</td></tr>
<tr>
<td>Panjang antrian disk</td><td>Panjang Antrian Disk</td><td>-</td><td>Panjang antrian disk (pemantauan di tingkat sistem)</td></tr>
<tr>
<td rowspan=3>Jaringan</td>
<td>Lalu lintas masuk</td><td>Throughput Terima Jaringan</td><td>KB/detik</td><td>Jumlah semua paket masuk dari semua koneksi</td></tr>
<tr>
<td>Lalu lintas keluar</td><td>Throughput Transmisi Jaringan</td><td>KB/detik</td><td>Jumlah semua paket keluar dari semua koneksi</td></tr>
<tr>
<td>Jaringan IO menunggu</td><td>Jaringan IO menunggu</td><td>milidetik</td><td>Waktu tunda IO jaringan rata-rata</td></tr>
<tr>
<td rowspan=3>Koneksi</td>
<td>Koneksi pengguna</td><td>Koneksi Pengguna</td><td>-</td><td>Jumlah rata-rata koneksi pengguna ke database per detik</td></tr>
<tr>
<td>Login/detik</td><td>Login/detik</td><td>hitungan/detik</td><td>Jumlah login per detik</td></tr>
<tr>
<td>Logout/detik</td><td>Logout/detik</td><td>hitungan/detik</td><td>Jumlah logout per detik</td></tr>
<tr>
<td rowspan=9>Akses</td>
<td>Kueri lambat</td><td>KueriLambat</td><td>-</td><td>Jumlah kueri yang berjalan selama lebih dari satu detik</td></tr>
<tr>
<td>Permintaan batch/detik</td><td>Permintaan Batch</td><td>hitungan/detik</td><td>Jumlah rata-rata permintaan per detik</td></tr>
<tr>
<td>Kompilasi SQL/detik</td><td>Kompilasi SQL/detik</td><td>hitungan/detik</td><td>Jumlah rata-rata kompilasi SQL per detik</td></tr>
<tr>
<td>Kompilasi ulang SQL/detik</td><td>Kompilasi Ulang SQL/detik</td><td>hitungan/detik</td><td>Jumlah rata-rata kompilasi ulang SQL per detik</td></tr>
<tr>
<td>Pemindaian penuh/detik</td><td>Pemindaian Penuh/detik</td><td>hitungan/detik</td><td>Jumlah pemindaian penuh per detik</td></tr>
<tr>
<td>Transaksi/detik</td><td>Transaksi/detik</td><td>hitungan/detik</td><td>Jumlah transaksi per detik</td></tr>
<tr>
<td>Proses diblokir</td><td>Proses diblokir</td><td>-</td><td>Jumlah saat ini proses yang diblokir</td></tr>
<tr>
<td>Rencana rasio hit cache</td><td>Rencana Cache:Rasio Hit Cache</td><td>%</td><td>Rasio hit dari rencana eksekusi setiap SQL</td></tr>
<tr>
<td>Rasio hit cache buffer</td><td>Rasio hit cache buffer</td><td>%</td><td>Rasio hit cache buffer (memori)</td></tr>
<tr>
<td rowspan=5>Kunci</td>
<td>Permintaan kunci/detik</td><td>Permintaan kunci/detik</td><td>hitungan/detik</td><td>Jumlah rata-rata permintaan kunci per detik</td></tr>
<tr>
<td>Latch menunggu/detik</td><td>Latch menunggu/detik</td><td>hitungan/detik</td><td>Jumlah latch menunggu per detik</td></tr>
<tr>
<td>Waktu tunggu rata-rata</td><td>Waktu tunggu rata-rata</td><td>Milidetik</td><td>Waktu tunggu rata-rata untuk setiap permintaan kunci yang menyebabkan menunggu</td></tr>
<tr>
<td>Deadlock</td><td>Jumlah deadlock/detik</td><td>hitungan/detik</td><td>Jumlah permintaan kunci yang menyebabkan deadlock per detik</td></tr>
<tr>
<td>Ambang batas proses yang diblokir</td><td>Ambang batas proses yang diblokir</td><td>detik</td>
<td>Ini adalah ambang batas yang ditentukan untuk menghasilkan laporan proses yang diblokir. Jika terlampaui, laporan proses yang diblokir akan dibuat. Secara default, laporan proses yang diblokir tidak akan dibuat</td></tr>
<tr>
<td>Lainnya</td>
<td>Kesalahan pengguna</td><td>Kesalahan Pengguna/detik</td><td>hitungan/detik</td><td>Jumlah rata-rata kesalahan per detik</td></tr>
</tbody></table>
