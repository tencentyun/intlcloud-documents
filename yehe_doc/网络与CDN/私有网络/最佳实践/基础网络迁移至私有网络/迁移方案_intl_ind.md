Dokumen ini menjelaskan cara memigrasikan instans CVM, TencentDB for MySQL, dan TencentDB for Redis dari jaringan klasik ke VPC.

## Latar belakang
- Jaringan dasar adalah kumpulan sumber informasi jaringan publik untuk semua pengguna Tencent Cloud. IP pribadi dari semua CVM ditetapkan oleh Tencent Cloud. Anda tidak dapat menyesuaikan rentang IP atau alamat IP.
- VPC adalah ruang jaringan virtual yang terisolasi secara logis di Tencent Cloud. Di VPC, Anda dapat menyesuaikan rentang IP, alamat IP, dan kebijakan perutean, sehingga lebih cocok untuk kasus penggunaan yang memerlukan konfigurasi kustom.

Karena sumber informasi jaringan klasik menjadi semakin langka dan tidak dapat diperluas, mulai 13 Juni 2017, semua akun Tencent Cloud yang baru terdaftar hanya dapat membuat instans (termasuk instans CVM dan TencentDB) di VPC, bukan di jaringan klasik. Semakin banyak pengguna yang memigrasikan instans mereka dari jaringan klasik ke VPC.


## Petunjuk
Periksa petunjuk di bawah ini sesuai dengan jenis sumber informasi Anda.
<table>
<thead>
<tr>
<th width="20%">Jenis Sumber Informasi</th>
<th width="25%">Karakteristik</th>
<th width="35%">Batasan</th>
<th width="20%">Petunjuk</th>
</tr>
</thead>
<tbody><tr>
<td>CVM</td>
<td>Instans CVM yang dimigrasikan sama dengan yang dibuat di VPC.</td>
<td><li>Migrasi dari jaringan klasik ke VPC TIDAK DAPAT dikembalikan. Setelah migrasi, instans CVM tidak dapat berkomunikasi dengan layanan Tencent Cloud di jaringan klasik</li>
<li>Instans CVM perlu dimulai ulang</li>
<li>IP pribadi berubah dari IP jaringan klasik ke IP VPC</li></td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/20278" target="_blank">Beralih ke VPC</a></td>
</tr>
<tr>
<td>TencentDB for MySQL</td>
<td><li>Akses VPC terlihat hasilnya segera setelah migrasi.</li><li>Jaringan klasik asli tetap dapat diakses hingga 7 hari setelah migrasi.</li><li>Koneksi database tidak terpengaruh selama migrasi.</li></td>
<td><li>Migrasi dari jaringan klasik ke VPC TIDAK DAPAT dikembalikan. Setelah migrasi, instans TencentDB for MySQL tidak dapat berkomunikasi dengan layanan Tencent Cloud di jaringan klasik</li>
<li>IP pribadi berubah dari IP jaringan klasik menjadi IP VPC.</li></td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">Beralih Jaringan</a></td>
</tr>
<tr>
<td>TencentDB for Redis</td>
<td><li>Akses VPC terlihat hasilnya segera setelah migrasi.</li><li>Jaringan klasik asli tetap dapat diakses hingga 7 hari setelah migrasi.</li><li>Koneksi database tidak terpengaruh selama migrasi.</li></td>
<td><li>Migrasi dari jaringan klasik ke VPC TIDAK DAPAT dikembalikan. Setelah migrasi, instans TencentDB for Redis tidak dapat berkomunikasi dengan layanan Tencent Cloud di jaringan klasik</li>
<li>IP pribadi berubah dari IP jaringan klasik menjadi IP VPC.</li></td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31944?from=10680#.E6.9B.B4.E6.8D.A2-redis-.E7.BD.91.E7.BB.9C" target="_blank">Ubah Jaringan Redis</a></td>
</tr>
</tbody></table>

## Contoh Migrasi
>?Contoh ini hanya untuk referensi. Sebelum migrasi Anda secara aktual, harap nilai dampaknya terhadap bisnis Anda dan kembangkan rencana migrasi yang detail.
### Deskripsi

Misalkan layanan berbasis jaringan klasik menggunakan empat layanan Tencent Cloud, termasuk CLB, CVM, TencentDB for MySQL, dan TencentDB for Redis. Hubungan mereka ditampilkan di bawah ini: 
- CLB publik terikat dengan dua CVM sebagai server backend.
- TencentDB for MySQL dan TencentDB for Redis bertindak sebagai database untuk aplikasi yang di-deploy di dua CVM.
![](https://main.qcloudimg.com/raw/bf54dd1832d0e16c756984e305772e06.png)

## Arah Migrasi
1. Migrasikan instans TencentDB ke VPC. Setelah migrasi, akses jaringan klasik asli tetap tersedia untuk jangka waktu tertentu, sehingga menjaga koneksi database dan ketersediaan layanan Anda. Selama periode ini, Anda dapat menyelesaikan migrasi layanan lain.
![](https://main.qcloudimg.com/raw/427fe3f0445056c94332df90d4cd9bb3.png)
2. Buat dua CVM dan deploy layanan sesuai kebutuhan di VPC tempat database dimigrasikan. Kemudian uji apakah CVM dapat mengakses instans TencentDB.
![](https://main.qcloudimg.com/raw/4425f9af34e3df70a84f1a80e8a7ba40.png)
3. Buat CLB publik di VPC database, dan hubungkan dengan dua CVM yang dibuat pada langkah sebelumnya. Lakukan pemeriksaan kesehatan untuk menghindari gangguan layanan karena pengecualian.
![](https://main.qcloudimg.com/raw/8dab2d96a40f1df4eefa9ad04117cb2b.png)
4. Tunggu hingga migrasi selesai. Lepaskan sumber informasi CLB dan CVM jaringan publik asli di jaringan klasik.
![](https://main.qcloudimg.com/raw/cb567a4a3f88c4bc4c8d787d60f512f3.png)

