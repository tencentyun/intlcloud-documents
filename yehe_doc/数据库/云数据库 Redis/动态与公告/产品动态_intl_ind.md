## Januari 2022
<table>
<tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=20%>Dokumentasi</th></tr>
<tr>
<td>Replikasi global yang didukung</td>
<td>Fitur replikasi global memungkinkan Anda untuk menambah dan menghapus instans, mengganti peran instans, dan menghapus grup replikasi.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/45602" target="">Ikhtisar</td></tr>
<tr>
<td>Periode penyimpanan cadangan khusus yang didukung</td>
<td>Anda dapat mengajukan permohonan untuk menyesuaikan periode penyimpanan file cadangan melalui daftar yang diizinkan.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/7071" target="">Mencadangkan Data</td></tr>
<tr>
<td>Menambahkan API untuk simulasi kegagalan</td>
<td>Instans dalam dukungan AZ yang sama memanggil `KillMasterGroup` API untuk pengujian simulasi kegagalan.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/41430" target="">KillMasterGroup</td></tr>
<tr>
<td>Menambahkan API untuk peralihan master/replika</td>
<td>Instans dalam dukungan AZ yang sama memanggil `ChangeReplicaToMaster` API untuk mempromosikan node replika (grup) ke node master untuk peralihan master/replika.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/41037" target="">ChangeReplicaToMaster</td></tr>
</table>



## Desember 2021
<table>
<tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumentasi</th></tr>
<tr>
<td>Mendukung spesifikasi memori 256 MB untuk Edisi Memori TencentDB for Redis 4.0 dan 5.0 (Arsitektur Standar)</td>
<td>Spesifikasi memori minimum Edisi Memori TencentDB for Redis 4.0 dan 5.0 (Arsitektur Standar) dapat mencapai 256 MB. Saat ini, edisi ini hanya didukung di Zona Shanghai 5, Zona Beijing 6, dan Zona Guangzhou 6.</td>
<td>2021-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/17952" target="">Performa</td></tr>
</table>
## November 2021
<table>
<tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumentasi</th></tr>
<tr>
<td>Templat parameter default didukung</td>
<td>TencentDB for Redis kini menyediakan templat parameter default yang berlaku untuk arsitektur standar Redis 2.8, arsitektur standar Redis 4.0, arsitektur kluster Redis 4.0, arsitektur standar Redis 5.0, dan arsitektur kluster Redis 5.0. Anda dapat melihatnya di halaman templat parameter di konsol.</td>
<td>11-2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/41810" target="">Menggunakan Templat Parameter</td></tr>
<tr>
<td>Alamat jaringan publik dapat diaktifkan</td>
<td>Anda sekarang dapat mengaktifkan alamat jaringan publik untuk instans TencentDB for Redis di konsol <a href="https://console.cloud.tencent.com/redis#/" target="_blank"></a>, sehingga instans ini dapat terhubung ke CVM di VPC yang berbeda melalui jaringan publik.</td>
<td>2021-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/43452" target="_blank">Mengonfigurasi Alamat Jaringan Publik</a></td></tr>
</table>


## Juli 2021
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Mendukung konfigurasi pengambilan data perubahan (CDC)</td>
<td>Anda dapat mengonfigurasi CDC di konsol Anda sendiri. CDC mencatat informasi semua perubahan dalam tabel dan nilai median entri data yang diubah, yang membantu Anda melacak perubahan tabel dengan lebih baik.</td>
<td>07-2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/41608" target="_blank">CDC</a></td></tr>
<tr>
<td>Mendukung konfigurasi pelacakan perubahan (CT)</td>
<td>Anda dapat mengonfigurasi CT di konsol sendiri. CT mencatat perubahan baris tabel dan memungkinkan Anda untuk langsung mendapatkan data terbaru dari tabel trek.</td>
<td>07-2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/41607" target="_blank">CT</a></td></tr>
<tr>
<td>Mendukung konfigurasi penyusutan database</td>
<td>Anda dapat langsung menyusutkan database di konsol untuk menghindari pemborosan ruang.</td>
<td>07-2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/41606" target="_blank">Menyusutkan Database</a></td></tr>
<tr>
<td>Mendukung konfigurasi parameter di konsol</td>
<td>Anda dapat melihat dan langsung mengubah parameter di konsol dan melihat log modifikasi parameter, yang membuat modifikasi parameter lebih mudah.</td>
<td>07-2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/41609" target="_blank">Mengatur Parameter Instans</a></td></tr>
<tr>
<td>Peluncuran 11 metrik pemantauan sistem dan instans baru</td>
<td>4 metrik pemantauan penghitung performa memori dan kunci dan 7 metrik pemantauan sistem alat berat fisik ditambahkan untuk pengguna kelas perusahaan guna memantau performa database secara komprehensif.</td>
<td>07-2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7524" target="_blank">Pemantauan</a></td></tr>
</tbody></table>

## Juni 2021
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Peluncuran instans spesifikasi tinggi</td>
<td>Edisi Ketersediaan Tinggi Server Ganda, Edisi Kluster, spesifikasi 64-core 512 GB dan 90-core 720 GB, memenuhi kebutuhan pengguna kelas perusahaan.</td>
<td>2021-06</td>
<td>-</td></tr>
<tr>
<td>Peluncuran layanan di Zona Tokyo 2</td>
<td>TencentDB for SQL Server sekarang tersedia di Zona Tokyo 2.</td>
<td>2021-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520" target="_blank">Wilayah dan AZ</a></td></tr>
</tbody></table>

## Mei 2021
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Peluncuran TencentDB for SQL Server 2019</td>
<td>TencentDB for SQL Server 2019 secara resmi diluncurkan dan mendukung instans Dasar, Ketersediaan Tinggi, dan Edisi Kluster, yang memiliki peningkatan besar dalam performa, kemudahan penggunaan, ketersediaan tinggi, dan keamanan.</td>
<td>2021-05</td>
<td>-</td></tr>
<tr>
<td>Peluncuran layanan di Zona Beijing 7</td>
<td>TencentDB for SQL Server sekarang tersedia di Zona Beijing 7.</td>
<td>2021-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520" target="_blank">Wilayah dan AZ</a></td></tr>
</tbody></table>


## Desember 2020
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Mendukung peningkatan versi dan arsitektur layanan mandiri</td>
<td>Anda dapat meningkatkan versi dan arsitektur serta menskalakan instans di konsol secara mandiri untuk menyesuaikan instans dengan mudah berdasarkan kebutuhan bisnis Anda.</td>
<td>2020-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35783" target="_blank">Menyesuaikan Spesifikasi Instans</a></td></tr>
</tbody></table>

## November 2020
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Mendukung penggunaan tag</td>
<td>TencentDB for SQL Server mendukung penggunaan tag. Anda dapat menggunakan tag untuk menandai penggunaan sumber daya, pengguna, dan skenario bisnis yang berbeda di bawah akun Anda.</td>
<td>2020-11</td>
<td>-</td></tr>
<tr>
<td>Peluncuran layanan di wilayah Chengdu</td>
<td>TencentDB for SQL Server sekarang tersedia di Wilayah Chengdu.</td>
<td>2020-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520" target="_blank">Wilayah dan AZ</a></td></tr>
</tbody></table>

## Oktober 2020
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Mendukung migrasi dengan DTS dan migrasi cold backup yang dioptimalkan</td>
<td>DTS mendukung migrasi data dari database SQL Server yang dibuat sendiri di IDC, cloud, dan vendor cloud lainnya ke TencentDB for SQL Server serta migrasi data antara instans TencentDB for SQL Server.<br>Migrasi cold backup memulihkan data dari file .bak, yang berlaku untuk migrasi data dari database SQL Server di vendor cloud lain dan database SQL Server yang dibuat sendiri ke TencentDB for SQL Server. Beberapa metode migrasi memberikan pengalaman migrasi data yang lebih mudah dan ramah pengguna.</td>
<td>2020-10</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/238/39005" target="_blank">Migrasi Cold Backup</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/39006" target="_blank">Migrasi dengan DTS</a></li></td></tr>
</tbody></table>


## Juli 2020
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Meluncurkan TencentDB for SQL Server Basic (Standalone) Edition</td>
<td>Edisi Dasar TencentDB for SQL Server diluncurkan, yang mendukung izin `sysadmin` cloud. Menyediakan satu set lengkap solusi database berlisensi dengan ketersediaan tinggi, keamanan, dan performa dan OPS ringan.</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/3254" target="_blank">Arsitektur</a></td></tr>
</tbody></table>

## Maret 2020
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Mendukung akun admin</td>
<td>TencentDB for SQL Server mendukung izin admin. Seorang admin memiliki izin baca/tulis untuk semua database pada instans dan izin pengelolaan utas dan dapat secara otomatis menemukan database baru dan mendapatkan izin baca/tulisnya.</td>
<td>2020-03</td>
<td>-</td></tr>
</tbody></table>

## Januari 2020
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Mendukung kluster Always On</td>
<td>Instans Edisi Perusahaan TencentDB for SQL Server 2017 mendukung penambahan instans baca saja. Arsitektur Always On yang mendasari mengimplementasikan kontrol kemampuan kluster, seperti replikasi data otomatis, penyeimbangan beban lalu lintas instans baca saja, dan switch primer/replika instans primer.</td>
<td>2020-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/3254" target="_blank">Arsitektur</a></td></tr>
</tbody></table>

## Desember 2019
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody>
<tr>
<td>Mendukung pengaturan waktu pemeliharaan perangkat</td>
<td>TencentDB for SQL Server mendukung pengaturan waktu pemeliharaan. Untuk memastikan stabilitas instans TencentDB, sistem backend melakukan operasi pemeliharaan pada instans selama waktu pemeliharaan pada interval yang tidak teratur.</td>
<td>2019-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35785" target="_blank">Mengatur Informasi Pemeliharaan Instans</a></td></tr>
</tbody></table>


## Oktober 2019
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Mendukung konfigurasi grup keamanan</td>
<td><a href="https://cloud.tencent.com/doc/product/213/500">Grup keamanan</a> adalah firewall virtual stateful yang mampu memfilter. Sebagai sarana penting untuk isolasi keamanan jaringan, solusi ini dapat digunakan untuk mengatur kontrol akses jaringan untuk satu atau beberapa instans TencentDB.</td>
<td>2019-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35789" target="_blank">Mengonfigurasi Grup Keamanan</a></td></tr>
<tr>
<td>Mendukung keranjang sampah</td>
<td>Setelah instans berlangganan atau bayar sesuai pemakaian bulanan kedaluwarsa atau dihentikan secara manual, instans tersebut dapat secara otomatis dimasukkan ke keranjang sampah untuk disimpan.</td>
<td>2019-10</td>
<td>-</td></tr>
</tbody></table>

## September 2019
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Mendukung pembuatan database dengan beberapa kumpulan karakter yang tersedia di konsol</td>
<td>TencentDB for SQL Server mendukung beberapa kumpulan karakter SQL Server yang disediakan oleh Microsoft di konsol untuk pilihan Anda saat membuat database.</td>
<td>2019-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35780" target="_blank">Membuat Database</a></td></tr>
</tbody></table>

## Juli 2019
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Peluncuran layanan di wilayah Seoul</td>
<td>TencentDB for SQL Server sekarang tersedia di Wilayah Seoul.</td>
<td>2019-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/7520" target="_blank">Wilayah dan AZ</a></td></tr>
</tbody></table>

## Juni 2019
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Mendukung mode penagihan bayar sesuai pemakaian</td>
<td>TencentDB for SQL Server mendukung mode penagihan bayar sesuai pemakaian. Anda dapat memilih mode penagihan berdasarkan kebutuhan bisnis Anda.</td>
<td>2019-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35798" target="_blank">Ikhtisar Penagihan</a></td></tr>
</tbody></table>

## Mei 2019
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Mendukung peningkatan konfigurasi instans</td>
<td>Spesifikasi instans database dapat ditingkatkan, dan kapasitasnya dapat diperluas.</td>
<td>2019-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/35783" target="_blank">Menyesuaikan Spesifikasi Instans</a></td></tr>
</tbody></table>

## September 2017
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Peluncuran SQL Server 2016</td>
<td>TencentDB for SQL Server sekarang tersedia di SQL Server 2016.</td>
<td>2017-09</td>
<td>-</td></tr>
</tbody></table>


## Desember 2016
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Mendukung mode baca saja untuk server replika</td>
<td>TencentDB for SQL Server mendukung mode baca saja untuk server replika. Anda dapat memilih memori dan disk sesuai kebutuhan guna menyesuaikan spesifikasi database untuk bisnis aktual Anda. Mode baca saja diimplementasikan melalui snapshot, memfasilitasi analisis data online. Mode ini tidak meningkatkan biaya, memengaruhi performa database utama, atau membahayakan ketersediaan tinggi.</td>
<td>2016-12</td>
<td>-</td></tr>
</tbody></table>


## Mei 2016
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Mendukung Edisi Perusahaan SQL Server 2012</td>
<td>TencentDB for SQL Server sekarang tersedia di Edisi Perusahaan SQL Server 2012, yang kompatibel dengan semua fitur SQL Server 2008.</td>
<td>2016-05</td>
<td>-</td></tr>
</tbody></table>


## Desember 2015
<table>
<thead><tr><th width=20%>Pembaruan</th><th width=50%>Deskripsi</th><th width=10%>Tanggal Rilis</th><th width=20%>Dokumen</th></tr></thead>
<tbody><tr>
<td>Peluncuran TencentDB for SQL Server secara resmi</td>
<td>TencentDB for SQL Server secara resmi diluncurkan dan menyediakan berbagai fitur seperti manajemen instans, detail instans, pemantauan sistem, manajemen database, manajemen akun, dan pencadangan.</td>
<td>2015-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/238/2016" target="_blank">Ikhtisar</a></td></tr>
</tbody></table>

