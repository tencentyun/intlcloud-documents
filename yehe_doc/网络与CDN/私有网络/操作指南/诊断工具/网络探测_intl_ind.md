Layanan probe jaringan Tencent Cloud digunakan untuk memantau kualitas koneksi jaringan VPC, termasuk latensi, tingkat kehilangan paket, dan metrik kunci lainnya.

Pada arsitektur jaringan cloud hibrida, Anda dapat menggunakan VPN atau Direct Connect untuk menghubungkan VPC di Tencent Cloud dengan IDC Anda sendiri. Untuk memantau kualitas jaringan koneksi secara real-time, Anda dapat membuat probe jaringan di subnet yang perlu berkomunikasi dengan IDC. Kemudian, Anda akan mendapatkan tingkat kehilangan paket dan latensi dari tautan yang diperiksa, dan memenuhi tujuan berikut:

- Pemantauan kualitas koneksi secara real-time
- Alarm kegagalan koneksi real-time

## Petunjuk

- Layanan probe jaringan mengadopsi metode ping dengan frekuensi 20 deteksi per menit.
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

![](https://main.qcloudimg.com/raw/2174c50676f92290be0e367d7efc6a22.png)
**Field description** (Deskripsi bidang)

<table>
<thead>
<tr>
<th>Bidang</th>
<th>Deskripsi</th>
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
<td>Hop selanjutnya</td>
<td>Anda dapat memilih untuk "Tentukan" atau "Jangan Tentukan" pada hop selanjutnya. <ul><li>Jika "Jangan Tentukan" dipilih, tidak ada hop selanjutnya yang akan dipilih.<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>Catatan:
</div>
<p>Jika Anda tidak ingin menentukan hop selanjutnya,<a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC&level3_id=185&radio_title=%E5%85%B6%E4%BB%96%E9%97%AE%E9%A2%98&queue=96&scene_code=16314&step=2">kirim tiket</a> untuk mengaktifkan fitur daftar yang diizinkan ini.</p></li><li>Jika Anda menentukan hop selanjutnya, pilih jenis dan instans hop selanjutnya. Kemudian, sistem secara otomatis menambahkan rute 32-bit yang sesuai ke tabel rute terkait subnet.</li></ul></td>
</tr>
</tbody></table>

5. **Verify** (Verifikasi) **Probe Destination IP** (IP Tujuan Probe)
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
3. Dalam daftar, cari probe jaringan yang akan diubah dan klik **Edit** (Edit) di kolom operasi.
![](https://main.qcloudimg.com/raw/04ada38a6d656c5d956a361067f90446.png)
4. Di jendela pop-up **Edit Network Probe** (Edit Probe Jaringan) (contoh ini tidak menentukan hop selanjutnya), buat perubahan yang diperlukan dan klik **Submit** (Kirim) untuk menyimpan perubahan.
![](https://main.qcloudimg.com/raw/d92a1320d63fc08151bd1f32f4c0ae3e.png)

## Menghapus Probe Jaringan
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih **Diagnostic Tools** (Alat Diagnostik) -> **Network Probe** (Probe Jaringan) di bilah sisi kiri untuk masuk ke halaman pengelolaan.
3. Dalam daftar, temukan probe jaringan yang akan dihapus dan klik **Delete** (Hapus) di kolom operasi.
4. Klik **Delete** (Hapus) di jendela pop-up untuk mengonfirmasi penghapusan.
 >!Menghapus probe jaringan juga menghapus semua rute terkait.

 ![](https://main.qcloudimg.com/raw/f4e41ac5686d3c3bff4722f35bde995c.png)
