## Ikhtisar
TencentDB for SQL Server mendukung migrasi data dengan menggunakan file COS. Metode migrasi yang dijelaskan dalam dokumen ini juga berlaku untuk migrasi dari instans SQL Server yang dibeli di penyedia layanan cloud lain atau instans yang dibuat sendiri ke instans TencentDB for SQL Server pada versi yang berbeda.
>!
>- Sebelum migrasi, pastikan bahwa versi SQL Server dari instans target lebih tinggi dari instans sumber.
>- Untuk file .bak yang digunakan untuk migrasi, pastikan bahwa setiap file .bak hanya berisi satu database.
>- Nama database yang dimigrasikan tidak boleh sama dengan nama instans TencentDB for SQL Server.

## Migrasi Cadangan Penuh
### Menyiapkan file cadangan

Ada dua cara untuk menyiapkan file cadangan penuh:

#### Cadangan penuh setelah dimatikan
- Anda menonaktifkan instans SQL Server yang dibeli di penyedia layanan cloud lain atau instans yang dibuat secara mandiri, mencadangkan seluruh database, lalu mengekspor file cadangan (yang harus dalam format `.bak`). Server harus dimatikan sampai migrasi selesai.
- Jika Anda memilih migrasi cadangan penuh setelah dimatikan, Anda tidak perlu melakukan migrasi cadangan tambahan secara terpisah.

#### Cadangan penuh tanpa dimatikan
>?
>- Hentikan pencadangan data Anda sendiri dan catat pekerjaan pencadangan hingga migrasi (penuh dan tambahan) selesai.
>- Nama file cadangan tidak dapat disesuaikan dan harus mengikuti konvensi penamaan dalam skrip.
>- Setelah cadangan penuh dilakukan, lakukan pemulihan cadangan tambahan hingga data pada instans sumber sama dengan data pada instans target.
>- Jika nama file berisi `2full2`, ini adalah cadangan penuh.
>- Dalam skenario pemulihan tambahan, setelah unggahan cadangan dan migrasi data selesai, database akan berada dalam status "restoring" (memulihkan) sebelum cadangan dan pemulihan tambahan terakhir dilakukan. Saat ini, database tidak dapat diakses, dan hal ini normal. Anda perlu melakukan pencadangan dan pemulihan tambahan terakhir untuk membuat database dapat diakses.

Anda tidak perlu mematikan instans SQL Server yang dibeli di penyedia layanan cloud lain atau instans yang dibuat secara mandiri. Lakukan pencadangan penuh database dan ekspor file cadangan.
```
declare @dbname varchar(100)
declare @localtime varchar(20)
declare @str varchar(8000)
set @dbname='db'
set @localtime =replace(replace(replace(CONVERT(varchar, getdate(), 120 ),'-',''),' ',''),':','')
set @str='BACKUP DATABASE [' + @dbname + '] TO  DISK = N''d:\dbbak\' + @dbname + '_' + @localtime + '_2full2_2noreconvery2.bak'' WITH INIT'
exec(@str)
go
```

<span id = "shangchuan_beifen"></span>
### Mengunggah file cadangan ke COS
1. Login ke [Konsol COS](https://console.cloud.tencent.com/cos5).
2. Pilih **Bucket List** (Daftar Bucket) di bilah sisi kiri dan klik **Create Bucket** (Buat Bucket).
3. Di halaman pembuatan yang muncul, masukkan informasi yang relevan dan klik **OK** (OKE).
 - Wilayah bucket harus sama dengan instans SQL Server untuk bermigrasi.
 - Migrasi lintas wilayah dengan COS tidak didukung.  
4. Kembali ke daftar bucket dan klik nama bucket atau **Configuration Management** (Manajemen Konfigurasi) di kolom "Operasi".
5. Pilih halaman **File List** (Daftar File), klik **Upload Files** (Unggah File), dan pilih satu atau beberapa file yang akan diunggah.
6. Setelah file diunggah, klik nama bucket dan dapatkan **alamat objek** dari informasi dasar di bagian konfigurasi dasar.
![](https://main.qcloudimg.com/raw/27f6a4907b0161e6feb55e891d66bf6e.png)

<span id = "qianyi_shuju"></span>

### Memigrasikan data melalui file sumber di COS
1. Login ke [Konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver).
2. Pilih **Data Transfer** (Transfer Data) di bilah sisi kiri dan klik **Create Task** (Buat Tugas) untuk membuat tugas migrasi offline.
  - Nama Tugas: kustom.
  - Jenis Instans Sumber: pilih **SQL Server backup recovery (COS mode)** (Pemulihan cadangan SQL Server (mode COS)).
  - Wilayah: wilayah database sumber harus sama dengan file sumber di COS.
  - Tautan ke File Sumber di COS: Anda dapat melihat informasi file untuk mendapatkan alamat objek COS setelah mengunggah file sumber.
  - Jenis dan Wilayah Database Target: dibuat secara otomatis oleh sistem berdasarkan konfigurasi database sumber.
  - ID Instans: pilih instans target. Anda hanya dapat memilih instans di wilayah yang sama.
![](https://main.qcloudimg.com/raw/bbc54177bc114bb133a1fadd99597b26.png)
3. Setelah konfigurasi selesai, klik **Next** (Selanjutnya).
4. Saat ini, jenis dan pengaturan database dapat diubah. Klik **Create Task** (Buat Tugas).
5. Kembali ke daftar tugas. Saat ini, status tugas adalah **initializing** (menginisialisasi). Pilih tugas di bagian atas daftar dan klik **Start** (Mulai) untuk menyinkronkan tugas.
6. Setelah sinkronisasi data selesai (yaitu, bilah kemajuan menunjukkan 100%), Anda perlu mengeklik **Complete** (Selesai) di bagian atas daftar untuk mengakhiri proses sinkronisasi. Anda dapat memeriksa apakah migrasi berhasil berdasarkan **status** (status).
 - Jika status tugas adalah **task successful** (tugas berhasil), artinya migrasi data berhasil.
 - Jika statusnya **task failed** (tugas gagal), artinya migrasi data gagal. Periksa informasi kegagalan, perbaiki dengan benar, lalu migrasikan lagi.

 

## Migrasi Cadangan Tambahan
### Menyiapkan file cadangan
>?
>- Nama file cadangan tidak dapat disesuaikan dan harus mengikuti konvensi penamaan dalam skrip.
>- Jika nama file berisi `2log2`, ini adalah cadangan tambahan.
>

- (Opsional) Jika ada beberapa file cadangan tambahan, semuanya kecuali yang terakhir dapat dibuat dengan cara berikut. File harus diunggah untuk migrasi data secara berurutan; jika tidak, migrasi akan gagal.
>!Setelah "pembuatan cadangan, pengunggahan cadangan, dan migrasi data" selesai, database akan berada dalam status "restoring" (memulihkan). Saat ini, database tidak dapat diakses, dan hal ini normal. Anda dapat mengulangi operasi ini hingga unggahan dan migrasi cadangan terakhir, lalu lakukan langkah berikutnya (yaitu, "cadangan tambahan terakhir setelah server dimatikan").
>
```
declare @dbname varchar(100)
declare @localtime varchar(20)
declare @str varchar(8000)
set @dbname='db'
set @localtime =replace(replace(replace(CONVERT(varchar, getdate(), 120 ),'-',''),' ',''),':','')
set @str='BACKUP LOG [' + @dbname + '] TO  DISK = N''d:\dbbak\' + @dbname + '_' + @localtime + '_2log2_2noreconvery2.bak'' WITH FORMAT, INIT'
exec(@str)
go
```
- Matikan server, lakukan pencadangan tambahan, ekspor file cadangan, unggah, lalu migrasikan data.
>!Hanya setelah operasi ini dilakukan database dapat diakses secara normal.
>
```
declare @dbname varchar(100)
declare @localtime varchar(20)
declare @str varchar(8000)
set @dbname='db'
set @localtime =replace(replace(replace(CONVERT(varchar, getdate(), 120 ),'-',''),' ',''),':','')
set @str='BACKUP LOG [' + @dbname + '] TO  DISK = N''d:\dbbak\' + @dbname + '_' + @localtime + '_2log2_2reconvery2.bak'' WITH FORMAT, INIT'
exec(@str)
go
```



### Mengunggah file cadangan dan memigrasikan data
1. Setelah menyiapkan file cadangan, lakukan pengunggahan file berikutnya dan migrasi data seperti yang diinstruksikan di [Mengunggah File Cadangan ke COS](#shangchuan_beifen) dan [Memigrasikan Data Melalui File Sumber di COS](#qianyi_shuju).
2. Setelah file cadangan tambahan terakhir (yaitu, file .bak yang berisi `_2log2_2reconvery2`) diimpor, status instans target akan berubah dari baca saja menjadi dapat digunakan, dan Anda dapat mengalihkan bisnis Anda ke instans TencentDB for SQL Server.



