Dokumen ini menjelaskan cara melihat ruang cadangan di konsol.

## Ikhtisar
Ruang cadangan yang ditempati oleh file cadangan instans TencentDB for SQL Server dialokasikan berdasarkan wilayah. Ini setara dengan total kapasitas penyimpanan yang digunakan oleh semua cadangan database di suatu wilayah, termasuk cadangan data otomatis, cadangan data manual, dan cadangan log.
Meningkatkan periode atau frekuensi penyimpanan cadangan akan menggunakan lebih banyak ruang cadangan database. Anda dapat melihat statistik ruang cadangan dan tren semua instans di setiap wilayah di bawah akun Anda serta statistik ruang cadangan real-time dari setiap instans.

## Melihat Total Cadangan
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver).
2. Di bilah sisi kiri, pilih **Database Backup** (Cadangan Database).
3. Pada halaman **Database Backup** (Cadangan Database), pilih wilayah untuk melihat total cadangan pada tab **Overview** (Ikhtisar), termasuk ruang cadangan yang digunakan dan jumlah semua cadangan, cadangan data, dan cadangan log di wilayah tersebut.
![](https://qcloudimg.tencent-cloud.cn/raw/f4e0c1edddfa628009eb6642f8e81482.png)
>?
>- Jika nilai total cadangan ditampilkan dalam warna hijau, total ruang cadangan yang digunakan tidak melebihi tier gratis.
>- Jika nilai total cadangan ditampilkan dalam warna oranye, total ruang cadangan yang digunakan telah melebihi tier gratis dan biaya yang harus dikeluarkan.

## Melihat Statistik Cadangan Real-Time
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver).
2. Di bilah sisi kiri, pilih **Database Backup** (Cadangan Database).
3. Pada halaman **Database Backup** (Cadangan Database), pilih wilayah untuk melihat statistik cadangan real-time di bagian bawah tab **Overview** (Ikhtisar), termasuk ID/nama instans, ruang cadangan, cadangan data, cadangan log, cadangan otomatis, dan cadangan manual.
![](https://qcloudimg.tencent-cloud.cn/raw/90f8494adce2e4d09f544a32470a9cd1.png)
>?Pada halaman statistik cadangan, Anda dapat mencari instans berdasarkan ID instans untuk melihat statistik cadangan real-time. Anda juga dapat melakukan berbagai operasi seperti menyortir bidang statistik berdasarkan ukuran spasi, memuat ulang halaman statistik, dan mengunduh data.
![](https://qcloudimg.tencent-cloud.cn/raw/1bf6258e6937995769dc51d9f60c6f38.png)

