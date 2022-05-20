
TencentDB for Redis mendukung pencadangan otomatis dan manual.
>?Untuk menghindari dampak pada bisnis yang disebabkan oleh kelebihan beban pada database master, sumber cadangan data lengkap dari database Redis replika yang baru dibuat akan menjadi database replika lain dalam instans selama pencadangan data.
>
## Pencadangan Otomatis
Pencadangan otomatis harian didukung untuk instans dalam langkah-langkah berikut:
1. Masuk ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Backup and Restoration** (Pencadangan dan Pemulihan) dan klik **Auto-Backup Settings** (Pengaturan Pencadangan Otomastis).
3. Di jendela pop-up, konfigurasikan waktu mulai pencadangan dan periode penyimpanan, lalu klik **OK** (OKE).
>? 
>- Semua opsi dipilih untuk **Backup Schedule** (Jadwal Pencadangan) secara default dan tidak dapat diubah.
>- Cadangkan waktu penyimpanan default 7 hari, jika Anda perlu melakukan perubahan silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).  
![](https://main.qcloudimg.com/raw/02813e57aa17fab2c5db77a3922469b0.png)
4. Pencadangan akan dimulai pada jangka waktu yang ditentukan. Selama tugas pencadangan, Anda dapat melihat statusnya di Pusat Tugas. Setelah selesai, Anda dapat melihat cadangan yang dihasilkan di **Backup and Restoration** (Pencadangan dan Pemulihan).
>? Proses pencadangan mungkin tertunda jika dipengaruhi oleh proses yang relevan.

## Pencadangan Manual
Pada halaman detail instans, klik **Manual Backup** (Pencadangan Manual) di pojok kanan atas, edit keterangan, dan klik **OK** (OKE).

## Unduhan Cadangan
>? Saat ini, Anda hanya dapat mengunduh file cadangan di Redis Edisi Standar.
>
1. Masuk ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Backup and Restoration** (Pencadangan dan Pemulihan > **Backup List** (Daftar Cadangan) dan klik **Download** (Unduh) di kolom **Operation** (Operasi).
3. Di jendela pop-up, salin alamat unduhan atau klik **Download** (Unduh) untuk mengunduh file cadangan. Unduhan lintas-AZ tidak didukung.
>?Alamat jaringan pribadi dan alamat unduhan lokal berlaku selama 12 jam. Anda perlu mendapatkannya lagi setelah kedaluwarsa.
