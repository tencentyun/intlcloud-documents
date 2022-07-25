Di konsol CSS, Anda dapat dengan cepat mengonfigurasi berbagai fitur dasar, seperti manajemen nama domain, manajemen streaming langsung, transcoding, dan perekaman. Anda juga dapat melakukan operasi, seperti push web, konfigurasi akselerasi, dan pemantauan sumber daya. 

## Prasyarat

- Anda telah mengaktifkan [CSS](https://cloud.tencent.com/product/css). 
Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live/livestat).

## Ikhtisar

Klik **Overview** (Ikhtisar) di bilah sisi kiri untuk melihat berbagai data, mulai dari biaya lalu lintas kemarin, data streaming langsung real-time, jumlah saluran push saat ini, jumlah koneksi bersamaan, hingga tren terkini dalam bandwidth dan lalu lintas yang dapat dikenai tagihan, serta jumlah saluran push. Anda juga dapat mengganti mode penagihan atau mengubah perincian waktu. Anda dapat mengeklik **Beginner's Guide** (Panduan Pemula) di pojok kanan atas untuk melihat petunjuk untuk memulai penggunaan CSS.
![](https://qcloudimg.tencent-cloud.cn/raw/e8946c20fd1a4cad644cfbd4f637bb14.png)


### Today's Data (Data Hari Ini)

Bagian ini menampilkan bandwidth puncak downstream, penggunaan lalu lintas downstream, jumlah saluran push saat ini, dan jumlah koneksi bersamaan pada hari berjalan.

<table>
<thead><tr><th width="20%">Item Statistik</th><th width="80%">Deskripsi</th></tr></thead>
<tbody><tr>
<td>Current Downstream Bandwidth (Bandwidth Downstream Saat Ini)</td>
<td>Bandwidth puncak downstream saat ini yang dihasilkan oleh akselerasi pemutaran ulang untuk semua nama domain pemutaran ulang saat ini</td>
</tr>
<tr>
<td>Today's Downstream Traffic (Lalu Lintas Downstream Hari Ini)</td>
<td>Total lalu lintas downstream hari ini yang dihasilkan oleh akselerasi pemutaran ulang untuk semua nama domain pemutaran ulang</td>
</tr>
<tr>
<td>Current Push Channels (Saluran Push Saat Ini)</td>
<td>Jumlah saluran push saat ini</td>
</tr>
<tr>
<td>Concurrent Connections (Koneksi Bersamaan)</td>
<td><li/>Jika RTMP atau FLV digunakan sebagai protokol pemutaran ulang, nilai Koneksi Bersamaan sama dengan jumlah penonton online. <li/>Jika HLS digunakan sebagai protokol pemutaran ulang, nilai Koneksi Bersamaan tidak mencerminkan jumlah penonton online.</td>
</tr>
</tbody></table>

### Usage Trends (Tren Penggunaan)

Bagian ini menampilkan tren penggunaan streaming langsung untuk hari ini, kemarin, 7 hari terakhir, dan 30 hari terakhir, termasuk **Bandwidth Trend** (Tren Bandwidth), **Traffic Trend** (Tren Lalu Lintas), dan **Push Channels** (Saluran Push).

<table>
<thead><tr><th width="20%">Item Statistik</th><th width="80%">Deskripsi</th></tr></thead>
<tbody><tr>
<td>Bandwidth Trend (Tren Bandwidth)</td>
<td>Total bandwidth puncak downstream yang digunakan oleh layanan akselerasi untuk semua nama domain pemutaran ulang dalam periode kueri</td>
</tr>
<tr>
<td>Traffic Trend (Tren Lalu Lintas)</td>
<td>Total lalu lintas downstream yang digunakan oleh layanan akselerasi untuk semua nama domain pemutaran ulang dalam periode kueri</td>
</tr>
<tr>
<td>Push Channels (Saluran Push)</td>
<td>Jumlah saluran push untuk nama domain yang dipilih dalam periode kueri</td>
</tr>
</tbody></table>

#### Mengubah perincian waktu

Konsol CSS memungkinkan Anda mengubah perincian waktu saat melihat tren bandwidth, lalu lintas, dan saluran push yang dapat dikenai tagihan dengan mengeklik nilai di samping **Granularity** (Perincian) dan memilih opsi yang diinginkan.
![](https://main.qcloudimg.com/raw/8582c16fca9bd3e4c2f0fcd78625cbb5.png)

### Detail Penagihan

<table>
<thead><tr><th width="20%">Item Statistik</th><th width="80%">Deskripsi</th></tr></thead>
<tbody><tr>
<td>Yesterday's Traffic Usage (Penggunaan Lalu Lintas Kemarin)</td>
<td>Bagian ini menampilkan biaya yang dikenakan oleh lalu lintas/bandwidth downstream yang dihasilkan dalam pemutaran ulang langsung kemarin. Anda dapat beralih antara <strong>Daily bill-by-traffic (Tagihan berdasarkan lalu lintas harian)</strong> dan <strong>Daily bill-by-peak bandwidth (Tagihan berdasarkan bandwidth puncak harian)</strong>.</td>
</tr>
<tr>

</tbody></table>

- **Mengganti mode penagihan**
  Jika mode penagihan saat ini adalah penagihan harian, Anda dapat mengeklik **Switch** (Ubah) di **Yesterday's Traffic Usage** (Penggunaan Lalu Lintas Kemarin) untuk mengubah mode penagihan. Klik **Confirm** (Konfirmasi) di jendela pop-up untuk menyelesaikan perubahan. Informasi selengkapnya tentang perubahan mode penagihan dapat dilihat di [Changing Billing Mode (Mengubah Mode Penagihan)](https://intl.cloud.tencent.com/document/product/267/30411).


>? Informasi selengkapnya dapat dilihat di [Pricing Overview (Ikhtisar Harga)](https://intl.cloud.tencent.com/document/product/267/2819).

