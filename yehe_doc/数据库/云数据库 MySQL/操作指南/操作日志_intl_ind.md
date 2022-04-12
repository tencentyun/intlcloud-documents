## Ikhtisar
Kueri pernyataan SQL yang membutuhkan waktu lebih lama dari nilai yang ditentukan disebut sebagai "kueri lambat", dan pernyataan terkait disebut "pernyataan kueri lambat". Proses tempat administrator database (DBA) menganalisis pernyataan kueri lambat dan menemukan alasan mengapa kueri lambat terjadi dikenal sebagai "analisis kueri lambat".

Anda dapat melihat detail log lambat, detail log kesalahan, dan log pengembalian instans, serta mengunduh log lambat pada halaman log operasi di konsol. Anda juga dapat melihat dan mengunduh log database melalui antarmuka baris perintah (CLI) atau TencentDB API. Untuk informasi selengkapnya, harap lihat [DescribeSlowLogs](https://intl.cloud.tencent.com/document/product/236/15845) dan [DescribeBinlogs](https://intl.cloud.tencent.com/document/product/236/15843).

>?Instans TencentDB for MySQL (tidak termasuk instans node tunggal dasar) mendukung manajemen log operasi.
>

#### Catatan tentang kueri lambat di MySQL
- long_query_time: parameter ambang batas kueri lambat yang akurat hingga level mikrodetik. Nilai default adalah 10 detik. Ketika pernyataan SQL memerlukan lebih banyak waktu daripada ambang batas untuk dieksekusi, pernyataan tersebut akan dicatat dalam log yang lambat. 
Saat parameter `long_query_time` disesuaikan, log lambat yang ada tidak akan terpengaruh. Misalnya, jika parameter ambang log lambat adalah 10 detik, catatan log lambat yang melebihi 10 detik akan dilaporkan. Setelah nilai ini diubah menjadi 1 detik, log yang dilaporkan sebelumnya akan tetap disimpan.
- log_queries_not_using_indexes: apakah akan mencatat kueri yang tidak diindeks. Nilai default adalah OFF.


## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman manajemen instans.
2. Pada tab **Operation Log** (Log Operasi), Anda dapat melihat detail log lambat, detail log kesalahan, dan log pengembalian instans serta mengunduh log lambat.
<table>
<thead><tr><th>Fitur</th><th>Deskripsi</th></tr></thead>
<tbody><tr>
<td>Detail log lambat</td><td>Mencatat pernyataan SQL yang memerlukan lebih dari 10 detik untuk dieksekusi di database selama sebulan terakhir</td></tr>
<tr>
<td>Unduhan log lambat</td><td>Mengunduh log lambat</td></tr>
<tr>
<td>Detail log kesalahan</td><td>Mencatat informasi terperinci dari setiap pengaktifan dan penonaktifan serta semua peringatan dan kesalahan serius selama operasi</td></tr>
<tr>
<td>Log pengembalian</td><td>Mencatat status dan kemajuan tugas pengembalian</td></tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/c229d0fe6a4869998d3472b0a35efa28.png"  style="margin:0;">
3. Untuk mengunduh slow log, pada tab **Download Slow Log** (Unduh Log Lambat), klik **Download** (Unduh) di kolom **Operation** (Operasi).
4. Salin alamat unduhan di kotak dialog pop-up, [login ke CVM Linux di VPC yang sama dengan instans TencentDB](https://intl.cloud.tencent.com/document/product/213/10517), dan jalankan `wget` untuk mengunduh file melalui jaringan pribadi berkecepatan tinggi .
>?
>- Log dengan ukuran 0 KB tidak dapat diunduh.
>- Anda juga dapat mengklik **Download** (Unduh) untuk mengunduhnya secara langsung. Namun, ini mungkin memakan waktu lebih lama.
>- `wget` format perintah: wget -c 'log file download address' -O custom filename.log
>
Contoh:
```
wget -c 'http://szx.dl.cdb.tencentyun.com:303/cfdee?appid=1210&time=1591&sign=aIGM%3D' -O test.log
```
