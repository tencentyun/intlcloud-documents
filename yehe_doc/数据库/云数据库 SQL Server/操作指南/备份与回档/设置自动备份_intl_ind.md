TencentDB for SQL Server mendukung cadangan otomatis dan cadangan manual.
Dokumen ini menjelaskan cara mengonfigurasi cadangan otomatis di konsol.
>!
>- File cadangan disimpan di ruang cadangan terpisah dan tidak menempati ruang disk lokal instans.
>- Jangan melakukan operasi DDL selama proses cadangan untuk menghindari kegagalan cadangan yang disebabkan oleh penguncian tabel.
>- Cadangkan data Anda di luar jam sibuk.
>- Cadangan mungkin memakan waktu lama jika volume data besar.

## Catatan tentang Cadangan
1. Meningkatkan periode penyimpanan data dan pencadangan log dapat menyebabkan biaya ruang cadangan tambahan.
2. Memperpendek periode penyimpanan cadangan log dapat memengaruhi siklus pengembalian data instans.
3. Tier gratis untuk pencadangan terbatas, dan kelebihan apa pun akan ditagih berdasarkan bayar sesuai pemakaian.

## Petunjuk
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver).
2. Pilih wilayah di bagian atas, temukan instans target, dan klik ID instans target atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman manajemen instans.
![](https://qcloudimg.tencent-cloud.cn/raw/cbf37d2a491b4f8ba2089edb597ee4d1.png)
3. Pada halaman manajemen instans, pilih **Backup Management** (Manajemen Cadangan) dan klik **Auto-Backup Settings** (Pengaturan Cadangan Otomatis).
4. Di jendela pop-up, baca dan pilih **Backup Space Billing Description** (Deskripsi Penagihan Ruang Cadangan) dan klik **Save** (Simpan).
   - **Start Time** (Waktu Mulai): Waktu ini dapat disesuaikan dan direkomendasikan agar dilakukan di luar jam sibuk.
Misalnya, jika rentang waktu diatur ke 01.00–02.00, sistem akan memulai pencadangan pada titik waktu selama 01.00–02.00, yang bergantung pada kebijakan pencadangan backend dan kondisi sistem pencadangan.
   - **Data Backup Retention Period** (Periode Penyimpanan Cadangan Data): Lama waktunya adalah tujuh hari secara default dan dapat disesuaikan.
   - **Backup Cycle** (Siklus Cadangan): Setiap saat antara Senin dan Minggu dapat dipilih untuk cadangan.
>!Untuk memastikan kesinambungan antara waktu mulai dan periode penyimpanan data:
>- Jika periode penyimpanan cadangan diatur ke nilai yang lebih singkat dari tujuh hari, siklus cadangan akan dilakukan setiap hari, dengan memilih Senin hingga Minggu secara default.
>- Jika periode penyimpanan cadangan diatur ke nilai yang sama dengan atau lebih lama dari tujuh hari, setidaknya pencadangan akan dilakukan setiap minggu dua kali. Jika Anda memilih hanya satu, Anda tidak dapat mengeklik **Save** (Simpan).
   - **Next Time** (Lain Kali): Atur waktu kapan siklus pencadangan yang dikonfigurasi akan dimulai.
   - **Log Backup Retention Period** (Periode Penyimpanan Cadangan Log): Periode ini sama dengan periode penyimpanan cadangan data secara default dan tidak dapat diubah. Kumpulan cadangan yang kedaluwarsa akan dihapus secara otomatis.
   - **Log Backup Frequency** (Frekuensi Cadangan Log): Pencadangan dilakukan setiap 30 menit sekali secara default.
![](https://qcloudimg.tencent-cloud.cn/raw/66d0f3a95e970e0246d02aabf1967066.png)


