Dokumen ini menjelaskan cara menggunakan fitur migrasi data DTS untuk memigrasikan data dari SQL Server ke TencentDB for SQL Server.

## Catatan 
- Selama migrasi data penuh, DTS menggunakan sumber daya database sumber tertentu, yang dapat meningkatkan beban dan tekanan database sumber. Jika konfigurasi database Anda rendah, sebaiknya migrasikan data selama jam normal.
- Migrasi penuh diimplementasikan dengan tabel terkunci, saat operasi tulis akan diblokir selama beberapa detik.

## Prasyarat
- Anda telah membuat instans [TencentDB for SQL Server](https://intl.cloud.tencent.com/document/product/238/31571).
- Database sumber dan target harus memenuhi persyaratan untuk fitur dan versi migrasi seperti yang diinstruksikan dalam [Database yang Didukung oleh Migrasi Data](https://intl.cloud.tencent.com/document/product/571/42647).
- Anda telah menyelesaikan semua [persiapan](https://intl.cloud.tencent.com/document/product/571/42652).
- Jika database sumber bukan instans TencentDB for SQL Server atau Edisi Dasar TencentDB for SQL Server (seperti instans berbasis jaringan publik/CVM yang dibuat secara mandiri atau instans di cloud lain), akun dengan izin `sysadmin` perlu digunakan untuk migrasi, dan prosedur tersimpan `xp_cmdshell` harus dapat dijalankan. Jika data sumber adalah instans Edisi Ketersediaan Tinggi TencentDB for SQL Server atau Edisi Kluster, tidak ada batasan izin.
- Akun migrasi harus berupa `localsystem`.
- Layanan tempat database sumber berada harus membuka port berbagi file 445.
- Database sumber harus diatur ke "mode pemulihan penuh", dan sebaiknya Anda membuat cadangan lengkap sebelum migrasi.
- Ruang disk lokal dari database sumber harus cukup besar, sehingga ruang kosong yang tersisa dapat sesuai dengan ukuran database yang akan dimigrasikan. 

## Batasan Aplikasi
- Hanya satu tugas migrasi yang dapat dimulai setiap saat untuk instans sumber yang sama.
- Saat ini, migrasi lintas wilayah didukung antara daratan Tiongkok dan Hong Kong (Tiongkok) tetapi tidak antara wilayah lain.
- Hanya migrasi tingkat database yang didukung (yaitu, semua objek dalam database harus dimigrasikan bersama), sedangkan migrasi tabel tunggal tidak didukung.
- Login, agen pekerjaan, pemicu, dan tautan database (server tautan) di tingkat instans tidak dapat dimigrasikan.

## Pembatasan Operasi
- Jangan mengubah atau menghapus informasi pengguna (termasuk nama pengguna, kata sandi, dan izin) di database sumber dan target serta nomor port selama migrasi; jika tidak, tugas migrasi akan gagal.
- Jangan melakukan pencadangan log transaksi selama sinkronisasi tambahan; jika tidak, log transaksi akan terpotong dan terputus.
- Jika Anda hanya melakukan migrasi data penuh, jangan menulis data baru ke database sumber selama migrasi; jika tidak, data dalam database sumber dan target tidak akan konsisten. Dalam skenario dengan penulisan data, untuk memastikan konsistensi data secara real-time, sebaiknya pilih migrasi data penuh + tambahan.
- Untuk migrasi data lengkap + tambahan, setelah Anda mengklik **Complete** (Selesai) dan status tugas menjadi **Completed** (Selesai), jangan menulis data baru ke database sumber. Sebaiknya Anda berhenti menulis selama dua menit; jika tidak, data dalam database sumber dan target mungkin tidak konsisten.

## Operasi SQL yang Didukung
| Jenis Operasi | Operasi SQL yang Didukung |
| -------- | ------------------------------------------------------------ |
| DML | INSERT, UPDATE, DELETE, dan REPLACE |
| DDL | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, dan RENAEM TABLE <br>VIEW: CREATE VIEW, ALTER VIEW, dan DROP VIEW<br>INDEX: CREATE INDEX dan DROP INDEX <br>DATABASE: CREATE DATABASE, ALTER DATABASE, dan DROP DATABASE |

## Persyaratan Lingkungan
>?Sistem akan secara otomatis memeriksa persyaratan lingkungan berikut sebelum memulai tugas migrasi dan melaporkan kesalahan jika persyaratan tidak terpenuhi. Jika Anda dapat mengidentifikasi item pemeriksaan yang gagal, perbaiki seperti yang diinstruksikan di [Persyaratan untuk Item Pemeriksaan](https://intl.cloud.tencent.com/document/product/571/42552); jika tidak, tunggu verifikasi sistem selesai dan perbaiki masalah sesuai dengan pesan kesalahan.

| **Jenis** | **Persyaratan Lingkungan** |
| :------------- | :----------------------------------------------------------- |
| Persyaratan database sumber | <li>Layanan tempat database sumber berada harus membuka port berbagi file 445. <br><li>Database sumber dan target dapat dihubungkan. <br/><li>Server tempat database sumber berada harus memiliki bandwidth keluar yang cukup; jika tidak, kecepatan migrasi akan terpengaruh. |
| Persyaratan database target | <li>Hanya migrasi dari Edisi Dasar ke Edisi Ketersediaan Tinggi (termasuk Edisi Ketersediaan Tinggi Server Ganda dan Edisi Kluster) yang didukung, dan nomor versi database target harus di atas database sumber.<br/><li>Database target tidak boleh memiliki nama yang sama dengan database sumber. <br/><li>Ruang disk database target harus setidaknya 1,5 kali ukuran database sumber. <br/><li>Database target tidak dapat memiliki permintaan akses atau bisnis aktif; jika tidak, migrasi akan gagal. </li> |

## Petunjuk
1. Login ke [konsol DTS](https://console.cloud.tencent.com/dts/migration), pilih **Data Migration** (Migrasi Data) di bilah sisi kiri, dan klik **Create Migration Task** (Buat Tugas Migrasi) untuk masuk ke halaman **Create Migration Task** (Buat Tugas Migrasi).
2. Pada halaman **Create Migration Task** (Buat Tugas Migrasi), pilih wilayah database target dan klik **Free Trial** (Uji Coba Gratis). Saat ini, fitur migrasi data DTS tidak dikenakan biaya.
3. Di halaman **Set source and target databases** (Mengatur database sumber dan target), konfigurasikan tugas, database sumber, dan pengaturan database target. Setelah database sumber dan target lulus pengujian konektivitas, klik **Create** (Buat).
>?Jika pengujian konektivitas gagal, pecahkan masalah dan perbaiki masalah seperti yang diminta dan seperti yang diinstruksikan dalam [Panduan Memecahkan Masalah](https://intl.cloud.tencent.com/document/product/571/42552) dan coba lagi.
>
<table>
<thead><tr><th width="10%">Jenis Pengaturan</th><th width="20%">Item Konfigurasi</th><th width="70%">Deskripsi</th></tr></thead>
<tbody>
<tr>
<td rowspan=3>Konfigurasi Tugas</td>
<td>Nama Tugas</td>
<td>Tetapkan nama yang bermakna untuk identifikasi tugas yang mudah.</td></tr>
<tr>
<td>Mode Berjalan</td>
<td><ul><li>Eksekusi langsung: tugas akan segera dimulai setelah verifikasi tugas berlalu. Eksekusi terjadwal: Anda perlu mengonfigurasi waktu eksekusi tugas dan tugas akan dimulai secara otomatis.</li></ul></td></tr>
<tr>
<td>Tag</td>
<td>Tag digunakan untuk mengelola sumber daya menurut kategori dari dimensi yang berbeda. Jika tag yang ada tidak memenuhi persyaratan Anda, kelola tag di konsol.</td></tr>
<tr>
<td rowspan=6>Pengaturan Database Sumber</td>
<td>Jenis Database Sumber</td><td>Pilih jenis database sumber Anda. Dalam dokumen ini, pilih **SQL Server** (SQL Server).</td></tr>
<td>Jenis Akses</td><td>Pilih jenis berdasarkan skenario Anda. Dalam dokumen ini, **Database** (Database) dipilih sebagai contoh. Untuk persiapan berbagai jenis akses, lihat <a href="https://cloud.tencent.com/document/product/571/59968">Ikhtisar</a>.
<ul><li>Jaringan Publik: database sumber dapat diakses melalui IP publik.</li>
<li>Dibuat Secara Mandiri di CVM: database sumber di-deploy dalam instans <a href="https://cloud.tencent.com/document/product/213">CVM</a>.</li>
<li>Direct Connect: database sumber dapat dihubungkan dengan VPC melalui <a href="https://cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>Akses VPN: database sumber dapat saling terhubung dengan VPC melalui <a href="https://cloud.tencent.com/document/product/554">Koneksi VPN</a>.</li>
<li>Database: database sumber adalah database TencentDB.</li>
</ul>Untuk database cloud pihak ketiga, Anda dapat memilih **Public Network** (Jaringan Publik) secara umum atau memilih **VPC Access** (Akses VPC), **Direct Connect** (Direct Connect), atau **CCN** (CNN) berdasarkan kondisi jaringan Anda yang sebenarnya.</td></tr>
<tr>
<td>Wilayah</td><td>Pilih wilayah database sumber.</td></tr>
<tr>
<td>Instans Database</td><td>Pilih ID instans dari database target.</td></tr>
<tr>
<td>Akun</td><td>Akun dari database SQL Server sumber, yang harus memiliki izin yang diperlukan.</td></tr>
<tr>
<td>Kata Sandi</td><td>Kata sandi dari database SQL Server sumber.</td></tr>
<tr>
<td rowspan=6>Pengaturan Database Target</td>
<td>Jenis Database Target</td><td>Pilih **SQL Server** (SQL Server).</td></tr>
<tr>
<td>Jenis Akses</td><td>Pilih jenis berdasarkan skenario Anda. Dalam dokumen ini, pilih **Database** (Database).</td></tr>
<tr>
<td>Wilayah</td><td>Pilih wilayah database target.</td></tr>
<tr>
<td>Instans Database</td><td>Pilih ID instans dari database target.</td></tr>
<tr>
<td>Akun.</td><td>Akun database target, yang harus memiliki izin yang diperlukan.</td></tr>
<tr>
<td>Kata Sandi</td><td>Kata sandi dari database target.</td></tr>
</tbody></table>
4. Pada halaman **Set migration options and select migration objects** (Mengatur opsi migrasi dan pilih objek migrasi), konfigurasikan jenis dan objek migrasi, lalu klik **Save** (Simpan).
<img src="https://main.qcloudimg.com/raw/3a0d33529d07be6b6c2ed7d245a0cf52.png"  style="zoom:80%;">
<table>
<thead><tr><th>Item Konfigurasi</th><th>Deskripsi</th></tr></thead>
<tbody><tr>
<td>Jenis Migrasi</td>
<td>Pilih jenis berdasarkan skenario Anda.<ul><li>Migrasi penuh: seluruh database akan dimigrasikan.</li><li>Migrasi penuh + tambahan: seluruh database dan data tambahan berikutnya akan dimigrasikan. Jika ada penulisan data selama migrasi, dan Anda ingin memigrasikan data dengan lancar tanpa henti, pilih opsi ini.</li></ul></td></tr>
<tr>
<td>Objek yang Ditentukan</td>
<td>Hanya migrasi tingkat database yang didukung; yaitu, semua objek dalam database yang ditentukan harus dimigrasikan bersama. Pilih database yang akan dimigrasikan di **Source Database Object** (Objek Database Sumber) dan pindahkan ke kotak **Selected Object** (Objek yang Dipilih).</td></tr>
</tbody></table>
5. Pada halaman verifikasi tugas, verifikasi tugas. Setelah verifikasi lolos, klik **Start Task** (Mulai Tugas).
    Jika verifikasi gagal, perbaiki masalah seperti yang diinstruksikan di [Memperbaiki Kegagalan Verifikasi](https://intl.cloud.tencent.com/document/product/571/42552) dan mulai tugas verifikasi lagi.
 - Gagal: ini menunjukkan bahwa item cek gagal dan tugas diblokir. Anda perlu memperbaiki masalah dan menjalankan tugas verifikasi lagi.
 - Alarm: ini menunjukkan bahwa item cek tidak sepenuhnya memenuhi persyaratan, dan tugas dapat dilanjutkan, tetapi bisnis akan terpengaruh. Anda perlu menilai apakah akan mengabaikan alarm atau memperbaiki masalah dan melanjutkan tugas berdasarkan pesan alarm.
![](https://qcloudimg.tencent-cloud.cn/raw/acb446cee2725f999c8ced3614e85f2d.png)
6. Kembali ke daftar tugas migrasi data, dan Anda dapat melihat bahwa tugas telah memasuki status **Preparing** (Mempersiapkan). Setelah 1-2 menit, tugas migrasi data akan dimulai.
   - Pilih **Full migration** (Migrasi penuh): setelah selesai, tugas akan dihentikan secara otomatis.
   - Pilih **Full + Incremental migration** (Migrasi Penuh + Tambahan): setelah migrasi penuh selesai, tugas migrasi akan otomatis memasuki tahap sinkronisasi data tambahan, yang tidak akan berhenti secara otomatis. Anda perlu mengklik **Complete** (Selesai) untuk menghentikan sinkronisasi data tambahan secara manual.
      - Selesaikan sinkronisasi data tambahan dan peralihan bisnis secara manual pada waktu yang tepat.
      - Amati apakah tugas migrasi berada dalam tahap sinkronisasi tambahan dan tidak dalam status lag. Jika demikian, berhenti menulis data ke database sumber selama beberapa menit.
      - Selesaikan sinkronisasi tambahan secara manual saat kesenjangan data antara target dan database sumber adalah 0 MB dan jeda waktu antara keduanya adalah 0 detik.
7. (Opsional) Jika Anda ingin melihat, menghapus, atau melakukan operasi lain pada tugas, klik tugas dan pilih operasi target di kolom **Operation** (Operasi). Untuk informasi selengkapnya, lihat [Pengelolaan Tugas](https://intl.cloud.tencent.com/document/product/571/42637).
8. Setelah status tugas migrasi menjadi **Task successful** (Tugas berhasil), Anda dapat secara resmi menghentikan bisnis. Untuk informasi selengkapnya, lihat [Deskripsi Penghentian](https://intl.cloud.tencent.com/document/product/571/42612).
