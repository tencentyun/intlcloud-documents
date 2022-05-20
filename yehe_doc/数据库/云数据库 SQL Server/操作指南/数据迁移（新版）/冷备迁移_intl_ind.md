Dokumen ini menjelaskan cara memigrasikan data dari database SQL Server vendor cloud lain atau database SQL Server yang dibuat sendiri ke TencentDB for SQL Server.

## Ikhtisar
Migrasi cadangan dingin didasarkan pada pemulihan data dari cadangan .bak dan cocok untuk kasus penggunaan tempat bisnis dapat dihentikan untuk mencadangkan data. Anda dapat menggunakan cadangan dingin untuk memigrasikan data dari database SQL Server vendor cloud lain atau database SQL Server yang dibuat secara mandiri ke TencentDB for SQL Server.

TencentDB for SQL Server memungkinkan Anda mengunggah cadangan dari perangkat lokal Anda atau mengunggahnya ke [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436/6222).

## Catatan
- Sebelum migrasi, pastikan versi SQL Server dari instans target sama atau lebih baru dari instans sumber.
- Nama database yang dimigrasikan tidak boleh sama dengan nama target database TencentDB for SQL Server target.
- Untuk memigrasikan data menggunakan cadangan di COS, Anda harus mengunggah cadangan ke COS terlebih dahulu. Untuk informasi selengkapnya, lihat [Migrasi versi yang sama > Mengunggah file cadangan ke COS](https://intl.cloud.tencent.com/document/product/238/32558).

## Petunjuk
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver#/). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada halaman **Backup Restoration** (Pemulihan Cadangan), klik **Create** (Buat).
![](https://main.qcloudimg.com/raw/ce56a4edf2e8f436d0bdfc56cb700e7d.png)
3. Pada halaman **Backup Restoration Settings** (Pengaturan Pemulihan Cadangan), konfigurasikan tugas pemulihan cadangan, dan klik **Create Task** (Buat Tugas).
 - **Backup Upload Method** (Metode Unggah Cadangan): Anda dapat mengunggah cadangan dari perangkat lokal Anda atau mengunduhnya dari COS.
 - **Restoration Method** (Metode Pemulihan): cadangan penuh, cadangan penuh + log, dan cadangan penuh + cadangan diferensial didukung.
![](https://main.qcloudimg.com/raw/b062c9e46e390ba6275bc9adfeb195af.png)
4. Di halaman **Upload Backup File** (Mengunggah File Cadangan), unggah cadangan, dan klik **Save** (Simpan).
 - **Restoration Method** (Metode Pemulihan): jika **Full backups + Logs** (Cadangan penuh + Log) atau **Full backups + Differential backups** (Cadangan penuh + Cadangan diferensial) dipilih sebagai metode pemulihan, nama cadangan harus mengikuti konvensi penamaan di bawah ini. Klik **Get Backup Command** (Dapatkan Perintah Cadangan) untuk membuat perintah pencadangan yang dapat digunakan untuk membuat cadangan dengan nama dalam format yang benar.
    - Pemulihan dari cadangan penuh: tidak ada persyaratan untuk format nama cadangan.
    - Pulihkan dari cadangan penuh + cadangan diferensial:
      - Format nama cadangan lengkap: dbname_localtime_1full1_1noreconvery1.bak
       - Format nama cadangan tambahan: dbname_localtime_1diff1_1noreconvery1.bak
      - Format nama cadangan tambahan terakhir: dbname_localtime_1diff1_1reconvery1.bak
    - Pulihkan dari cadangan penuh + log:
      - Format nama cadangan penuh: dbname_localtime_2full2_2noreconvery2.bak
      - Format nama log: dbname_localtime_2log2_2noreconvery2.bak
      - Format nama log terakhir: dbname_localtime_2log2_2reconvery2.bak
 - **Download Settings** (Pengaturan Unduhan): pemulihan otomatis setelah pengunggahan selesai dan memulai pemulihan secara manual didukung.
    - Pemulihan otomatis setelah pengunggahan selesai: tugas pemulihan akan dimulai tepat setelah Anda mengklik **Save** (Simpan).
    - Mulai pemulihan secara manual: Anda harus memulai tugas pemulihan secara manual di halaman **Backup Restoration** (Pemulihan Cadangan) setelah mengklik **Save** (Simpan). Perhatikan bahwa cadangan yang diunggah akan disimpan hingga 24 jam.
 ![](https://main.qcloudimg.com/raw/e6393af999e08129e2e6fdd098d07261.png)
5. Kembali ke halaman **Backup Restoration** (Pemulihan Cadangan) dan lihat tugas pemulihan.
 - Pulihkan dari cadangan penuh: tugas pemulihan akan berakhir secara otomatis setelah proses pemulihan selesai.
 - Pulihkan dari cadangan penuh + cadangan diferensial atau cadangan penuh + log: setelah pemulihan dari cadangan lengkap selesai, Anda dapat mengunggah cadangan atau log diferensial ke subtugasnya. Setelah file terakhir diunggah ke subtugas, seluruh tugas pemulihan akan otomatis berakhir setelah subtugas selesai.
