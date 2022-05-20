## Ikhtisar
Anda dapat memigrasikan instans ke zona ketersediaan (AZ) lain dalam wilayah yang sama. Semua atribut dan konfigurasi (termasuk alamat jaringan pribadi dan subnet) instans tetap tidak berubah setelah migrasi. Jumlah waktu yang dibutuhkan sebanding dengan volume data dalam instans. Semakin banyak data, semakin lama waktu migrasi data. Selain itu, akses instans tidak akan terpengaruh selama migrasi.

## Jenis Instans yang Didukung
- Instans utama edisi ketersediaan tinggi dan edisi kluster didukung.
>?Jika instans utama edisi ketersediaan tinggi atau edisi kluster memiliki instans baca saja atau menerapkan paradigma olah pesan pub/sub, Anda perlu [mengirimkan tiket](https://console.cloud.tencent.com/workorder/category) untuk memigrasikannya ke seluruh AZ.
- Instans edisi dasar tidak didukung.
- Instans Baca Saja tidak didukung.

## Prasyarat
Wilayah tempat instans berada harus memiliki beberapa AZ.

## Dampak
- Migrasi yang sedang berlangsung tidak dapat dibatalkan.
- Nama, IP akses, dan port akses instans tetap tidak berubah setelah penyesuaian konfigurasi.
- Migrasi data akan dilakukan selama migrasi instans ke AZ lain. Selama migrasi data, instans dapat diakses secara normal dan bisnis Anda tidak akan terpengaruh.
- Jumlah waktu yang dibutuhkan sebanding dengan volume data dalam instans. Semakin banyak data, semakin lama waktu migrasi data. 
- Peralihan instans akan dilakukan setelah migrasi, menyebabkan pemutusan flash. Anda dapat menentukan waktu peralihan.

## Petunjuk
### Migrasi di seluruh AZ
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman detail instans.
2. Di bagian **Basic Info** (Info Dasar), klik **Migrate across AZs** (Migrasi di seluruh AZ) untuk mengakses halaman migrasi lintas AZ.
![](https://qcloudimg.tencent-cloud.cn/raw/2de60347d9a5265ae2b227821a488d63.png)
3. Lihat AZ instans asli, tentukan AZ target, aktifkan/nonaktifkan deployment multi-AZ, pilih waktu peralihan, centang kotak untuk menyetujui aturan migrasi lintas AZ, dan klik **Submit** (Kirim).
>?Setelah Anda mengklik **Submit** (Kirim), data instans akan dimigrasikan ke AZ target di lapisan yang mendasarinya tanpa memengaruhi eksekusi dan akses instans.
>Setelah data instans dimigrasikan, peralihan instans akan terjadi (**setelah migrasi selesai** atau **selama waktu pemeliharaan**), menyebabkan pemutusan flash. Setelah peralihan selesai, seluruh proses migrasi lintas AZ selesai.
>
![](https://qcloudimg.tencent-cloud.cn/raw/a92d8a7615296b87a6d630887b503660.png)

### Melihat tugas migrasi
Anda dapat melihat tugas migrasi lintas AZ di kotak **Running Tasks** (Menjalankan Tugas) di sudut kanan atas tab **Database Management** (Manajemen Database).
<img src="https://qcloudimg.tencent-cloud.cn/raw/577730c9f93171b1b01277c71afa5146.png" style="zoom:50%;" />

### Melakukan peralihan langsung
Jika instans dijadwalkan untuk dialihkan selama waktu pemeliharaan sesuai dengan konfigurasi tugas migrasi lintas AZ-nya, tetapi Anda harus segera mengalihkannya dalam keadaan khusus, Anda dapat mengklik **Switch Now** (Alihkan Sekarang) di **Operation** (Operasi) dalam daftar instans di [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver).

