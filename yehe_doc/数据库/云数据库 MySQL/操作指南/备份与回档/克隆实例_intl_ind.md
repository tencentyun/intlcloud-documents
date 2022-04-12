Dokumen ini menjelaskan cara mengkloning instans TencentDB for MySQL dan memulihkan data ke klon yang baru dibeli di konsol dengan cepat.

## Ikhtisar
Anda dapat memulihkan instans TencentDB for MySQL ke titik waktu mana pun dalam periode penyimpanan cadangan log atau dari cadangan fisik tertentu yang ditetapkan dengan kloning. Klon adalah instans baru yang dibuat dari data cadangan sesuai dengan titik pemulihan dalam waktu yang telah Anda tentukan. Setelah klon diverifikasi, Anda dapat memigrasikan datanya kembali ke instans asli dengan [DTS](https://intl.cloud.tencent.com/document/product/571/13709) atau Anda dapat mulai menggunakan klon.

#### Mode kloning
- Mengkloning sebuah instans dan memulihkan klon tersebut ke titik waktu mana pun dalam periode penyimpanan cadangan log yang Anda tetapkan.
- Mengkloning instans dan memulihkan klon dari kumpulan cadangan fisik tertentu dalam periode penyimpanan cadangan data yang Anda tetapkan.

#### Penagihan klon
- Klon mengadopsi mode penagihan bayar sesuai pemakaian. Untuk informasi selengkapnya tentang mode penagihan dan penghitungan biaya ini, harap lihat [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/236/18335).
- Kloning tidak akan ditagih sampai proses kloning selesai.  

## Prasyarat
- Arsitektur instans yang didukung: MySQL dua node atau tiga node
- Instans asli harus dalam status **Running** (Berjalan).
- Jika mode kloning diatur ke **By backup set** (Berdasarkan kumpulan cadangan), instans asli harus telah membuat setidaknya satu cadangan fisik. Anda dapat login ke [konsol](https://console.cloud.tencent.com/cdb), memilih **Database Backup** (Cadangan Database) di bilah sisi kiri, dan melihat status cadangan di tab **Backup List** (Daftar Cadangan).
- Saldo akun Anda harus mencukupi.

## Catatan
- Ruang hard disk instans kloning harus lebih besar dari jumlah data yang akan dikloning, atau tugas kloning mungkin gagal.
- Zona ketersediaan, versi database, mode replikasi, dan parameter database default klon harus sama dengan instans asli.
- Kloning tidak akan ditampilkan dalam daftar instans di konsol sampai proses kloning selesai.

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman manajemen instans.
2. Pilih **Backup and Restoration** (Cadangan dan Pemulihan) > **Data Backup List** (Daftar Cadangan Data), klik **Clone** (Kloning) di pojok kiri atas, atau cari cadangan yang diinginkan dan klik **Clone** (Kloning) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/b53e3c4f249a5f22638c32f4c92c7f75.png)
3. Pada halaman pembelian yang ditampilkan, tentukan mode kloning dan konfigurasi lainnya, lalu klik **Buy Now** (Beli Sekarang).
 - **By time point** (Berdasarkan titik waktu): Anda dapat memulihkan instans ke titik waktu mana pun dalam periode retensi cadangan log.
 - **By backup set** (Berdasarkan kumpulan cadangan): Anda dapat memulihkan data dari kumpulan cadangan ke instans baru. Kumpulan cadangan yang tersedia bergantung pada periode retensi cadangan data.
 >?Anda dapat login ke [konsol](https://console.cloud.tencent.com/cdb), pilih **Database Backup** (Cadangan Database) di bilah sisi kiri, dan lihat periode retensi cadangan di tab **Backup List** (Daftar Cadangan).
 >
![](https://main.qcloudimg.com/raw/f2fcdd5471326b60f6ee7ea8872f00bc.png)
4. Setelah pembelian, Anda dapat melihat detail kloning pada tab **Backup and Restore** (Cadangan dan Pemulihan) > **Cloned Instance List** (Daftar Instans yang Dikloning).
![](https://main.qcloudimg.com/raw/3b6a2781adafd4cbde550ea00f3898a8.png)
5. Setelah proses kloning selesai, Anda dapat melihat instans kloning yang baru dibuat dalam daftar instans.

## Dokumen Terkait
- Untuk informasi selengkapnya tentang pemulihan satu database dan tabel, harap lihat [Pengembalian Database](https://intl.cloud.tencent.com/document/product/236/7276).
- Untuk informasi selengkapnya tentang cara memulihkan data ke instans yang dibuat sendiri, harap lihat [Memulihkan Database dari Cadangan Fisik](https://intl.cloud.tencent.com/document/product/236/31910) dan [Memulihkan Database dari Cadangan Logis](https://intl.cloud.tencent.com/document/product/236/31909).

## Pertanyaan Umum
#### Apakah akses ke instans asli akan terpengaruh selama proses kloning?
Kumpulan cadangan asli dan binlog yang diunggah ke COS digunakan untuk kloning, yang tidak akan memengaruhi akses ke instans sumber.
