>!Dokumen ini menjelaskan fitur manajemen akses **SMS**. Informasi selengkapnya tentang manajemen akses untuk layanan Tencent Cloud lainnya dapat dilihat di [CAM-Enabled Products (Produk yang Didukung CAM)](https://intl.cloud.tencent.com/document/product/598/10588).

Manajemen akses SMS pada dasarnya mengikat sub-akun ke kebijakan atau memberikan kebijakan ke sub-akun. Anda dapat menggunakan kebijakan default secara langsung di konsol untuk menerapkan beberapa operasi otorisasi sederhana. Untuk operasi otorisasi yang lebih rumit, silakan lihat [Custom Policies (Kebijakan Kustom)](https://intl.cloud.tencent.com/document/product/382/38456).

Saat ini, SMS menyediakan kebijakan default berikut:

| Nama Kebijakan | Deskripsi |
|--------------------------|--------------|
| QcloudSMSFullAccess     | Izin akses penuh |
| QcloudSMSReadonlyAccess | Izin akses Baca-Saja |

## Kasus Penggunaan Kebijakan Default
### Membuat sub-akun dengan izin akses penuh
1. Akses halaman [Daftar Pengguna](https://console.cloud.tencent.com/cam) di Konsol CAM menggunakan Tencent Cloud [akun root](https://intl.cloud.tencent.com/document/product/598/32633) dan klik **Create User** (Buat Pengguna).
2. Pada halaman "Create User" (Buat Pengguna), pilih **Custom Creation** (Buat Kustom) untuk masuk ke halaman "Create Sub-user" (Buat Sub-pengguna).
>?Lakukan langkah-langkah sebelum masuk ke halaman "User Permissions" (Izin Pengguna) seperti yang diinstruksikan dalam [Membuat Sub-pengguna Kustom](https://intl.cloud.tencent.com/document/product/598/13674).
3. Pada halaman "User Permissions" (Izin Pengguna):
	1. Cari dan pilih kebijakan default `QcloudSMSFullAccess`.
	2. Klik **Next** (Selanjutnya).
4. Klik **Complete** (Selesai) di kolom "Review" (Tinjauan). Setelah sub-pengguna berhasil dibuat, unduh tautan login dan kredensial keamanan seperti yang ditunjukkan di bawah ini dan jaga kerahasiaannya.
<table>
<thead>
<tr>
<th>Informasi</th>
<th>Sumber</th>
<th>Deskripsi</th>
<th>Penyimpanan yang Diperlukan</th>
</tr>
</thead>
<tbody><tr>
<td>Tautan login</td>
<td>Salin pada halaman</td>
<td>Mempermudah login ke konsol tanpa harus masuk ke akun root</td>
<td>Tidak</td>
</tr>
<tr>
<td>Nama pengguna</td>
<td>File kredensial keamanan dalam format CSV</td>
<td>Diperlukan untuk login konsol</td>
<td>Ya</td>
</tr>
<tr>
<td>Kata sandi</td>
<td>File kredensial keamanan dalam format CSV</td>
<td>Diperlukan untuk login konsol</td>
<td>Ya</td>
</tr>
<tr>
<td>SecretId</td>
<td>File kredensial keamanan dalam format CSV</td>
<td>Diperlukan untuk memanggil API server. Untuk informasi selengkapnya, lihat "Access Key" (Kunci Akses)</td>
<td>Ya</td>
</tr>
<tr>
<td>SecretKey</td>
<td>File kredensial keamanan dalam format CSV</td>
<td>Diperlukan untuk memanggil API server. Untuk informasi selengkapnya, lihat "Access Key" (Kunci Akses)</td>
<td>Ya</td>
</tr>
</tbody></table>
5. Dengan tautan login dan kredensial keamanan di atas, Anda dapat menggunakan sub-pengguna ini untuk melakukan semua operasi dalam SMS (seperti mengakses konsol SMS dan memanggil API server SMS).

## Memberikan Akses Penuh Sub-akun yang Ada ke SMS
1. Akses **[Daftar Pengguna](https://console.cloud.tencent.com/cam)** di konsol CAM menggunakan Tencent Cloud [akun root](https://intl.cloud.tencent.com/document/product/598/32633) dan klik sub-akun target.
2. Klik **Add Policy** (Tambahkan Kebijakan) di bawah tab "Permissions" (Izin) pada halaman "User Details" (Detail Pengguna). Jika izin sub-akun tidak kosong, klik **Associate Policy** (Kaitkan Kebijakan).
3. Klik **Select policies from the policy list** (Pilih kebijakan dari daftar kebijakan), cari dan periksa kebijakan prasetel `QcloudSMSFullAccess`, lalu selesaikan otorisasi sesuai petunjuk yang diberikan.

## Menghapus Akses Penuh Sub-akun ke SMS
1. Akses **[Daftar Pengguna](https://console.cloud.tencent.com/cam)** di konsol CAM menggunakan Tencent Cloud [akun root](https://intl.cloud.tencent.com/document/product/598/32633) dan klik sub-akun target.
2. Cari kebijakan prasetel `QcloudSMSFullAccess` di bawah tab "Permissions" (Izin) pada halaman "User Details" (Detail Pengguna), klik **Disassociate** (Hapus Kaitan) di sebelah kanan, lalu selesaikan penghapusan otorisasi sesuai petunjuk yang diberikan.

