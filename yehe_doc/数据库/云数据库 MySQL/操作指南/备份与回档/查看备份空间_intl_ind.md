Dokumen ini menjelaskan cara melihat ruang cadangan instans MySQL dan tier gratis di konsol.

## Ikhtisar
Ruang cadangan yang ditempati oleh file cadangan instans TencentDB for MySQL dialokasikan berdasarkan wilayah. Ini setara dengan total ruang penyimpanan yang digunakan oleh semua cadangan database MySQL di suatu wilayah, termasuk cadangan data otomatis, cadangan data manual, dan cadangan log. Meningkatkan waktu penyimpanan cadangan atau frekuensi pencadangan manual akan menggunakan lebih banyak ruang cadangan database.

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb) dan pilih **Database Backup** (Cadangan Database) di bilah sisi kiri.
2. Pilih wilayah di bagian atas untuk melihat informasi pencadangannya di tab **Overview** (Ikhtisar), termasuk pencadangan total, tren pencadangan, dan statistik pencadangan real-time.
 - Total Cadangan: bagian ini menampilkan ukuran dan jumlah semua, data, dan cadangan log serta tier gratis yang ditempati oleh semua cadangan. 
>?
>- Hijau: total ruang cadangan yang digunakan tidak melebihi tier gratis.
>- Oranye: total ruang cadangan yang digunakan telah melebihi tier gratis dan biaya yang timbul. Untuk informasi selengkapnya, harap lihat [Penagihan Ruang Cadangan](https://intl.cloud.tencent.com/document/product/236/32344).
>
![](https://main.qcloudimg.com/raw/e9489e74614d7708d357de6943837c3c.png)
 - Tren Cadangan: bagian ini menampilkan tren pencadangan total, pencadangan data, pencadangan log, dan ruang kosong.
 - Statistik Cadangan Real-Time: bagian ini menampilkan ID/nama instans (Anda dapat mengklik ID/nama untuk masuk ke halaman detail instans), ruang cadangan (yang dapat diurutkan berdasarkan ukuran), dan cadangan data/log di pilihan wilayah. Anda dapat mencari instans berdasarkan ID/nama di kotak pencarian di sudut kanan atas.
3. Pilih **Backup List** (Daftar Cadangan) di bagian atas, di mana daftar cadangan dibagi menjadi **Data Backup List** (Daftar Cadangan Data) dan **Log Backup List** (Daftar Cadangan Log). Di daftar instans, klik ID instans untuk masuk ke halaman detail. Daftar cadangan mendukung pemfilteran berdasarkan periode waktu dan pencarian fuzzy berdasarkan ID/nama instans.
![](https://main.qcloudimg.com/raw/0587e4f22b33960c349b2e2dbbe81d10.png)
 - **Data backup list** (Daftar cadangan data)
    - Pemfilteran menurut bidang daftar didukung:
Jenis: semua, cadangan dingin logis, cadangan dingin fisik.
Mode Cadangan: semua, otomatis, manual.
Metode Pencadangan: saat ini, hanya pencadangan penuh yang didukung.
    - Cadangan dapat diurutkan berdasarkan waktu pencadangan, waktu mulai tugas, waktu selesai tugas, dan ukuran cadangan.
    - Klik **Detail** (Detail) di kolom **Operation** (Operasi) untuk masuk ke halaman cadangan dan pemulihan instans, tempat Anda dapat mengklik **Download** (Unduh) untuk mengunduh cadangan. Hanya cadangan manual yang dapat dihapus.
 - **Log backup list** (Daftar cadangan log)
    - Cadangan dapat diurutkan berdasarkan waktu mulai dan waktu berakhir data log.
    - Klik **Details** (Detail) di kolom **Operation** (Operasi) untuk masuk ke halaman cadangan dan pemulihan instans, tempat Anda dapat mengklik **Download** (Unduh) untuk mengunduh log.

## Pertanyaan Umum
#### Bagaimana ruang cadangan melebihi tagihan tier gratis? Bagaimana cara mengurangi biaya ruang cadangan?
Untuk informasi selengkapnya, harap lihat [Penagihan Ruang Cadangan](https://intl.cloud.tencent.com/document/product/236/32344).
