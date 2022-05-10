TencentDB for MySQL mendukung tiga jenis arsitektur: node tunggal (sebelumnya Edisi Dasar), dua-node (sebelumnya Edisi Ketersediaan Tinggi), dan tiga-node (sebelumnya Edisi Keuangan). Instans node tunggal umum sebelumnya dikenal sebagai instans Edisi IO Tinggi node tunggal.
>! Node tunggal (sebelumnya Edisi Dasar) sedang dalam proses rekonstruksi dan penataran, dan penjualan akan ditangguhkan selama periode ini.

## Melihat Arsitektur Instans
- Untuk instans yang akan dibeli, login ke [halaman pembelian TencentDB for MySQL](https://buy.cloud.tencent.com/cdb) dan pilih arsitektur di bagian **Architecture** (Arsitektur).
- Untuk instans yang dibeli, login ke [konsol MySQL](https://console.cloud.tencent.com/cdb), temukan instans yang diinginkan dalam daftar instans, dan lihat arsitekturnya di kolom **Configuration** (Konfigurasi).

## Perbandingan Arsitektur
<table>
<thead>
<tr><th>Arsitektur</th><th >Dua node</th><th>Tiga node</th><th colspan=2>Node tunggal</th>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/39794">Kebijakan isolasi sumber daya</a></td>
<td>Umum</td><td>Umum</td><td>Umum</td><td>Dasar</td></tr>
<tr>
<td>Versi yang didukung</td>
<td>MySQL 5.5, 5.6, 5.7, dan 8.0</td><td>MySQL 5.6, 5.7, dan 8.0</td><td>MySQL 5.6, 5.7, dan 8.0</td><td>MySQL 5.7</td></tr>
<tr>
<td>Node</td>
<td>Satu sumber, satu replika</td><td>Satu sumber, dua replika</td><td>Node tunggal</td><td>Node tunggal</td></tr>
<tr>
<td>Mode replikasi sumber-replika</td>
<td>Asinkron (default), semi-sinkronisasi</td><td>Asinkron (default), sinkronisasi canggih, dan semi-sinkron</td><td>-</td><td>-</td></tr>
<tr>
<td>Ketersediaan instans</td>
<td>99.95%</td><td>99.99%</td><td>-</td><td>-</td></tr>
<tr>
<td>Penyimpanan dasar</td>
<td>SSD NVMe Lokal</td><td>SSD NVMe Lokal</td><td>SSD NVMe Lokal</td><td>Disk cloud premium</td></tr>
<tr>
<td>Performa</td>
<td>Hingga 240.000 IOPS</td><td>Hingga 240.000 IOPS</td><td>-</td><td>rumus penghitungan IOPS: <br>{min 1,500 + 8 x disk capacity, max 4,500}</td></tr>
<tr>
<td>Kasus penggunaan</td>
<td>Game, internet, IoT, ritel, e-commerce, logistik, asuransi, sekuritas, dll.</td>
<td>Game, internet, IoT, ritel, e-commerce, logistik, asuransi, sekuritas, dll.</td>
<td>Aplikasi dengan persyaratan pemisahan baca/tulis</td>
<td>Pembelajaran pribadi, situs web kecil, sistem perusahaan kecil non-inti, serta pengembangan dan pengujian perusahaan menengah-ke-besar</td></tr>
</tbody></table>

## Dokumentasi
- TencentDB for MySQL mendukung MySQL 8.0, 5.7, 5.6, dan 5.5. Untuk informasi selengkapnya, silakan lihat [Versi Database](https://intl.cloud.tencent.com/document/product/236/31896).
- TencentDB for MySQL mendukung jenis instans berikut: instans sumber dan replika baca saja. Untuk informasi selengkapnya, silakan lihat [Jenis Instans Database](https://intl.cloud.tencent.com/document/product/236/7268).
- TencentDB for MySQL mendukung fitur yang berbeda dalam arsitektur yang berbeda. Untuk informasi selengkapnya, silakan lihat [Daftar Perbedaan Fitur](https://intl.cloud.tencent.com/document/product/236/36007).
