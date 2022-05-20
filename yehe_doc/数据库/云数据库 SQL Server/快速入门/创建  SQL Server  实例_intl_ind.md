
## Ikhtisar
Dokumen ini menjelaskan cara membuat instans di konsol TencentDB for SQL Server.

## Prasyarat
Anda telah [mendaftar](https://intl.cloud.tencent.com/document/product/378/17985) untuk akun Tencent Cloud dan menyelesaikan [verifikasi identitas](https://intl.cloud.tencent.com/document/product/378/3629).

## Petunjuk
### Membuat instans
1. Login ke [halaman pembelian TencentDB for SQL Server](https://buy.intl.cloud.tencent.com/sqlserver), pilih konfigurasi database yang diinginkan, baca dan berikan persetujuan Anda terhadap Ketentuan Layanan, pastikan semuanya sudah benar, dan klik **Buy Now** (Beli Sekarang).
 - Mode Penagihan: bayar sesuai pemakaian
 - Wilayah dan AZ: untuk informasi selengkapnya, lihat [Wilayah dan AZ](https://intl.cloud.tencent.com/document/product/238/7520).
 - Jaringan: VPC (direkomendasikan) dan jaringan klasik didukung. Untuk informasi selengkapnya tentang perbedaan dan pengujian konektivitasnya, lihat [Lingkungan Jaringan](https://intl.cloud.tencent.com/document/product/238/32562).
>?
>- Direkomendasikan bahwa instans CVM dan TencentDB harus berada di bawah akun yang sama dan di VPC yang sama di wilayah yang sama.
>- Karena sumber daya jaringan klasik menjadi semakin langka dan tidak dapat diperluas, akun Tencent Cloud yang terdaftar setelah 13 Juni 2017 dapat membuat instans (termasuk CVM dan TencentDB) hanya di VPC, bukan di jaringan klasik.
 - Jenis Instans: Edisi Ketersediaan Tinggi Server Ganda, Edisi Kluster, dan edisi Dasar didukung.
>?Edisi Kluster saat ini mendukung SQL Server 2017 Enterprise dan SQL Server 2019 Enterprise, yang menggunakan teknologi Always On untuk membangun kluster SQL Server dengan performa tinggi, ketersediaan, keandalan, dan kemudahan pemeliharaan.
 - Jenis Disk: SSD lokal performa tinggi, disk cloud performa tinggi, dan disk cloud SSD didukung.
>?Di daratan Tiongkok, jika Anda memerlukan disk cloud SSD untuk instans Edisi Dasar, [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk aplikasi.
<table>
<thead><tr><th>Jenis Disk</th><th>Deskripsi</th><th>Arsitektur Database yang Sesuai</th><th>Skenario yang Berlaku</th></tr></thead>
<tbody><tr>
<td>SSD lokal Performa Tinggi</td>
<td>Jenis penyimpanan disk lokal I/O tinggi.</td>
<td>Edisi Ketersediaan Tinggi/Edisi Kluster</td>
<td>Skenario bisnis yang memiliki persyaratan sangat tinggi untuk performa I/O penyimpanan dan arsitektur ketersediaan tinggi di lapisan aplikasi, seperti game online, ecommerce, layanan perangkat lunak ERP, streaming langsung video, dan media.</td></tr>
<tr>
<td>Disk cloud Performa Tinggi</td>
<td>Jenis penyimpanan hibrida. Ini memberikan kemampuan penyimpanan dengan performa tinggi yang dekat dengan SSD melalui mekanisme cache dan mengadopsi mekanisme terdistribusi tiga salinan untuk memastikan keandalan data.</td>
<td>Edisi Dasar</td>
<td>Skenario aplikasi kecil dan menengah yang memerlukan keandalan data tinggi dan performa sedang, seperti server web/aplikasi, pemrosesan logika bisnis, dan situs web kecil dan menengah.</td></tr>
<tr>
<td>Disk cloud SSD</td>
<td>Jenis penyimpanan disk cloud All-Flash dengan NVMe SSD sebagai media penyimpanan. Ini mengadopsi mekanisme penyimpanan terdistribusi tiga salinan untuk memberikan kemampuan I/O latensi rendah dan throughput tinggi dengan IOPS acak tinggi dan keamanan data 99,9999999%.</td>
<td>Edisi Dasar</td>
<td>Skenario aplikasi seperti aplikasi intensif I/O dan database relasional kecil dan menengah.</td></tr>
</tbody></table>
 - Versi Database: SQL Server 2008 R2, SQL Server 2012, SQL Server 2016, SQL Server 2017, dan SQL Server 2019 untuk Edisi Perusahaan dan Standar didukung. Setiap AZ mendukung versi database yang berbeda.
 - Pilih spesifikasi instans dan kapasitas disk yang diperlukan.
 - Multi-AZ: saat ini, hanya wilayah Shanghai, Beijing, Guangzhou, dan Hong Kong (Tiongkok) yang mendukung pemilihan multi-AZ. Dengan menggabungkan beberapa AZ menjadi satu "multi-AZ", mode deployment multi-AZ melindungi database dari kegagalan instans database dan penghentian AZ.
 - Periode Pemeliharaan dan Waktu Pemeliharaan: untuk memastikan stabilitas instans TencentDB for SQL Server Anda, sistem backend melakukan operasi pemeliharaan pada instans selama periode pemeliharaan dari waktu ke waktu. Kami sangat menyarankan Anda menetapkan waktu pemeliharaan yang dapat diterima untuk instans bisnis Anda, biasanya selama jam tidak sibuk, untuk meminimalkan potensi dampak pada bisnis Anda.
 - Daftar Proyek: TencentDB for SQL Server mendukung penetapan instans ke berbagai proyek untuk manajemen.
 - Grup Keamanan: berfungsi sebagai firewall virtual stateful dengan fitur pemfilteran untuk mengonfigurasi kontrol akses jaringan untuk satu atau lebih instans TencentDB. Ini adalah alat isolasi keamanan jaringan penting yang disediakan oleh Tencent Cloud.
 - Tag: memudahkan untuk mengategorikan dan mengelola sumber daya.
 - Pilih jumlah dan periode pembelian.
 - Ketentuan Layanan: untuk informasi selengkapnya, lihat [Ketentuan Layanan](https://intl.cloud.tencent.com/document/product/238/35546).
2. Setelah pembelian dilakukan, kembali ke [daftar instans](https://console.cloud.tencent.com/sqlserver#/) dan lihat instans yang dibuat. Saat status instans menjadi **Running** (Berjalan), instans berhasil dibuat.
![](https://main.qcloudimg.com/raw/7abd65a18810994b0c34c75450a41868.png)

### [Membuat akun database](id:cjzh)
1. Dalam daftar instans](https://console.cloud.tencent.com/sqlserver), klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada halaman manajemen instans, pilih **Account Management** (Manajemen Akun) > **Create Account** (Buat Akun) dan masukkan informasi yang relevan di jendela pop-up. Setelah memastikan semuanya sudah benar, klik **OK** (OKE).
>?Nama akun dan kata sandi yang dibuat akan digunakan saat menghubungkan ke TencentDB for SQL Server. Simpan dengan benar.
>

### Membuat database
1. Dalam [daftar instans](https://console.cloud.tencent.com/sqlserver), klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pilih tab **Database Management** (Manajemen Database), klik **Create Database** (Buat Database), dan masukkan informasi yang relevan di kotak dialog pop-up. Setelah memastikan semuanya sudah benar, klik **OK** (OKE)
 - Nama Database: dapat berisi hingga 32 huruf, angka, dan garis bawah, dan harus dimulai dengan satu huruf.
 - Kumpulan Karakter yang Didukung: pilih kumpulan karakter yang akan digunakan oleh database. Saat ini, sebagian besar kumpulan karakter asli didukung.
 - Otorisasi Akun: Anda dapat mengotorisasi akun yang ada untuk mengakses database. Jika Anda belum membuat akun, lihat [Membuat akun database](#cjzh).
 - Keterangan: dapat berisi hingga 256 karakter.
![](https://main.qcloudimg.com/raw/6bb212145f1cf97837ed7aa6be0bf05c.png)

