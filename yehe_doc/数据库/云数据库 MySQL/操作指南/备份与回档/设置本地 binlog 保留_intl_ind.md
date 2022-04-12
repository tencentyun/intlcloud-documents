
Dokumen ini menjelaskan cara mengatur periode retensi binlog untuk instans TencentDB for MySQL di konsol.

## Deskripsi Binlog
Binlog berkembang pesat ketika instans TencentDB for MySQL melakukan transaksi besar atau banyak operasi DML. Binlog dibagi setiap 256 MB dan diunggah ke COS. Anda dapat melihat file binlog yang diunggah di daftar log di konsol.
![](https://main.qcloudimg.com/raw/bcf3d0d2ac291ccebbcfebea05fd11f1.png)

## Ikhtisar
Sebelum diunggah ke COS, file binlog disimpan di disk instans (yaitu, secara lokal). Anda dapat mengatur periode penyimpanan binlog lokal, mengontrol persentase maksimum ruang disk yang dapat digunakan binlog, atau memperluas ruang disk di konsol. Sebaiknya hapus data yang tidak lagi digunakan untuk menjaga penggunaan disk tetap di bawah 80%.
- Sinkronisasi data MySQL didasarkan pada binlog. Untuk memastikan pemulihan database, stabilitas, dan ketersediaan tinggi, binlog tidak dapat dinonaktifkan di TencentDB for MySQL.
- File binlog yang dihasilkan secara otomatis dicadangkan ke COS melalui [fitur pencadangan otomatis](https://intl.cloud.tencent.com/document/product/236/37796) yang disediakan oleh TencentDB for MySQL. File binlog yang cadangannya sudah diunggah ke COS akan dihapus sesuai dengan kebijakan penyimpanan binlog lokal. Untuk mencegah pengecualian, file binlog yang digunakan tidak dapat dihapus bahkan kedaluwarsa. Dengan demikaian, penghapusan binlog lokal mengalami penundaan.
>?Aturan untuk menghapus file binlog yang kedaluwarsa:
>File binlog lokal diperiksa setiap 60 detik sekali. Jika waktu mulai atau penggunaan ruang file binlog tidak memenuhi aturan penyimpanan yang ditetapkan, waktu tersebut akan ditambahkan ke antrean file yang akan dihapus. File binlog dalam antrean akan diurutkan berdasarkan waktu dan dihapus mulai dari file terlama satu per satu hingga antrean dihapus.

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb) dan klik ID instans di daftar instans untuk masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Backup and Restoration** (Cadangan dan Pemulihan) dan klik **Configure Local Binlog** (Konfigurasi Binlog Lokal).
3. Di jendela pop-up, tentukan periode penyimpanan dan ambang batas penggunaan ruang, lalu klik **OK** (OKE).

## Pertanyaan Umum
#### Apakah pemulihan database akan terpengaruh jika periode penyimpanan binlog lokal terlalu pendek?
Tidak, karena file binlog yang dihasilkan akan diunggah ke COS melalui fitur pencadangan otomatis secepatnya, dan yang belum diunggah tidak dapat dihapus. Namun, periode penyimpanan yang terlalu pendek akan memengaruhi kecepatan pengembalian.

#### Apa kebijakan penyimpanan default untuk binlog lokal?
Secara default, periode penyimpanan binlog lokal adalah 120 jam, dan pemanfaatan ruang binlog maksimum adalah 30%.

#### Apakah file binlog akan mengambil ruang disk instan?
Ya. Sebelum file binlog diunggah ke COS dan dihapus sesuai dengan kebijakan penyimpanan, file tersebut akan disimpan di disk instans.
