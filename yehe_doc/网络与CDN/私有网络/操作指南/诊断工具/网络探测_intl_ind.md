Layanan probe jaringan Tencent Cloud digunakan untuk memantau kualitas koneksi jaringan VPC, termasuk latensi, tingkat kehilangan paket, dan metrik kunci lainnya.

Dengan arsitektur jaringan cloud hibrida, Anda membuat probe jaringan di subnet yang perlu berkomunikasi dengan IDC Anda untuk memantau tingkat kehilangan paket dan latensi dari tautan yang di-probe. Konfigurasi memungkinkan Anda untuk: 
- Memantau kualitas koneksi
- Menerima peringatan jika terjadi kegagalan koneksi

## Petunjuk
- Layanan probe jaringan mengadopsi metode ping dengan frekuensi 20 ping per menit.
- Hingga 50 probe diperbolehkan untuk setiap VPC.
- Maksimal 20 subnet di bawah VPC yang sama dapat memiliki probe jaringan.

## Membuat Probe Jaringan
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih **Diagnostic Tools** (Alat Diagnostik) -> **Network Probe** (Probe Jaringan) di bilah sisi kiri untuk masuk ke halaman pengelolaan.
3. Klik **+New** (+Baru) di bagian atas halaman **Network Probe** (Probe Jaringan).
4. Di jendela pop-up **Create Network Probe** (Buat Probe Jaringan), isi bidang yang relevan.
>?
>- Rute probe jaringan ditetapkan oleh sistem dan tidak dapat diubah.
>- Saat Anda mengganti rute subnet, rute default ini akan dihapus dari tabel rute asli yang terkait dengan subnet, dan ditambahkan ke tabel rute baru yang terkait.
>
![](https://main.qcloudimg.com/raw/2174c50676f92290be0e367d7efc6a22.png)
**Field description** (Deskripsi bidang)
<table>
<thead>
<tr>
<th>Bidang</th>
<th>Konfigurasi</th>
</tr>
</thead>
<tbody><tr>
<td>Nama</td>
<td>Nama probe jaringan.</td>
</tr>
<tr>
<td>VPC</td>
<td>VPC tempat IP sumber probe berada.</td>
</tr>
<tr>
<td>Subnet</td>
<td>Subnet tempat IP sumber probe berada.</td>
</tr>
<tr>
<td>IP Tujuan Probe</td>
<td>Maksimal dua IP tujuan didukung untuk probe jaringan. Pastikan bahwa Anda telah mengaktifkan kebijakan firewall ICMP untuk server tujuan probe jaringan.</td>
</tr>
<tr>
<td>Sumber Hop Selanjutnya</td>
<td>Anda dapat memilih <b>Tentukan</b> atau <b>Jangan Tentukan</b> pada hop selanjutnya. <ul><li>Jika <b>Jangan Tentukan</b> dipilih, tidak ada hop selanjutnya yang akan dipilih.<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>Catatan:
</div>
<p>**Do Not Specify** (Jangan Tentukan) sekarang hanya tersedia untuk pengguna beta. Untuk mengaktifkannya, harap <a href="https://console.cloud.tencent.com/workorder/category">kirim tiket</a>.</p></li><li>Jika Anda menentukan hop selanjutnya, pilih jenis dan instans hop selanjutnya. Kemudian, sistem secara otomatis menambahkan rute 32-bit yang sesuai ke tabel rute terkait subnet. Saat ini, jenis hop selanjutnya yang didukung mencakup NAT Gateway, peering connection, VPN gateway, direct connect gateway, CVM, dan CCN.<p>
<dx-alert infotype="explain" title="">
Jika Anda menentukan CCN sebagai hop selanjutnya dan IP tujuan probe menjadi milik dua VPC dalam CCN, rentang IP dengan mask terpanjang akan dicocokkan dan diterapkan.
</dx-alert>
</li></ul></td>
</tr>
</tbody></table>
5. (Opsional) **Verify** (Verifikasi) **Probe Destination IP** (IP Tujuan Probe)
>?Lewati langkah ini jika Anda tidak menentukan hop selanjutnya.
 - Jika koneksi berhasil, klik **OK** (Oke).
 - Jika koneksi gagal, periksa apakah rute subnet dikonfigurasi dengan benar, dan apakah perangkat yang diperiksa mengaktifkan ACL Jaringan, grup keamanan, atau firewall lain, yang dapat memblokir koneksi. Untuk informasi selengkapnya, lihat [Mengelola ACL Jaringan](https://intl.cloud.tencent.com/document/product/215/31852) dan [Memodifikasi Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35515).

## Memeriksa Latensi dan Paket Hilang dari Probe Jaringan

1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih **Diagnostic Tools** (Alat Diagnostik) -> **Network Probe** (Probe Jaringan) di bilah sisi kiri untuk masuk ke halaman pengelolaan.
3. Klik ikon pemantauan instans probe jaringan target untuk melihat latensi dan tingkat kehilangan paketnya.
	![](https://main.qcloudimg.com/raw/b1a8a96df051a50cf58fd6f34b09a228.png)

## Memodifikasi Probe Jaringan
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih **Diagnostic Tools** (Alat Diagnostik) -> **Network Probe** (Probe Jaringan) di bilah sisi kiri untuk masuk ke halaman pengelolaan.
3. Dalam daftar, cari probe jaringan yang akan diubah dan klik **Edit** (Edit) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/04ada38a6d656c5d956a361067f90446.png)
4. Di jendela pop-up **Edit Network Probe** (Edit Probe Jaringan), buat perubahan yang diperlukan dan klik **Submit** (Kirim) untuk menyimpan perubahan.
>?
>- Contoh ini belum menentukan hop selanjutnya.
>- Jika tidak ada hop selanjutnya yang ditentukan, nama, IP tujuan probe, dan catatan dari probe jaringan dapat dimodifikasi.
>- Jika hop selanjutnya ditentukan, nama, IP tujuan probe, sumber hop selanjutnya, dan catatan dari probe jaringan dapat dimodifikasi.
> 
 ![](https://main.qcloudimg.com/raw/d92a1320d63fc08151bd1f32f4c0ae3e.png)

## Menghapus Probe Jaringan
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih **Diagnostic Tools** (Alat Diagnostik) -> **Network Probe** (Probe Jaringan) di bilah sisi kiri untuk masuk ke halaman pengelolaan.
3. Dalam daftar, temukan probe jaringan yang akan dihapus dan klik **Delete** (Hapus) di kolom operasi.
4. Klik **Delete** (Hapus) di jendela pop-up untuk mengonfirmasi penghapusan.
>!Menghapus probe jaringan juga menghapus semua kebijakan yang peringatan yang terhubung dan rute yang dikonfigurasi. Periksa apakah bisnis Anda akan terpengaruh sebelum melanjutkan.
>
  ![](https://main.qcloudimg.com/raw/f4e41ac5686d3c3bff4722f35bde995c.png)

## Mengonfigurasi Kebijakan Alarm
Anda dapat mengonfigurasi kebijakan alarm untuk layanan probe jaringan, sehingga Anda dapat segera mendeteksi pengecualian rute apa pun untuk membantu mengalihkan rute dengan cepat dan memastikan ketersediaan bisnis.
1. Login ke konsol CM dan buka halaman [**Alarm Policy** (Kebijakan Alarm)](https://console.cloud.tencent.com/monitor/alarm2/policy).
2. Klik **Create** (Buat).
3. Di jendela pop-up **Create Alarm Policy** (Buat Kebijakan Alarm), masukkan nama kebijakan, pilih **Network Probe** (Probe Jaringan) untuk jenis kebijakan, konfigurasikan objek alarm, kondisi pemicu alarm, dan kebijakan alarm, lalu klik **Complete** (Selesai).
