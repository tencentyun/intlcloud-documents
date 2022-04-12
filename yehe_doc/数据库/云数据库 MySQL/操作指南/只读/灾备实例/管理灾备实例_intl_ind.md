## Ikhtisar
Untuk aplikasi dengan persyaratan tinggi pada kontinuitas layanan, keandalan data, dan kepatuhan, TencentDB for MySQL menyediakan instans pemulihan bencana lintas-wilayah untuk membantu meningkatkan kemampuan Anda dalam memberikan layanan berkelanjutan dengan biaya rendah dan meningkatkan keandalan data.
>?Biaya instans pemulihan bencana sama dengan instans sumber yang terkait. Untuk informasi selengkapnya, lihat [Harga Produk](https://buy.cloud.tencent.com/price/cdb).

#### Fitur
- Dengan alamat koneksi database terpisah, instans pemulihan bencana dapat menawarkan kemampuan akses baca untuk berbagai skenario seperti akses lokal dan analisis data dengan biaya redundansi perangkat yang lebih rendah.
- Arsitektur sumber/replikanya yang sangat tersedia membantu menghindari satu titik kegagalan untuk database.
- Data disinkronkan melalui jaringan pribadi dengan latensi lebih rendah dan stabilitas lebih tinggi dibandingkan dengan jaringan publik. 
- Saat ini, data yang disinkronkan melalui jaringan pribadi gratis selama promosi. Jika biaya diperlukan, kami akan memberi tahu Anda sebelumnya.

#### Cara kerjanya
- Jika instans TencentDB digunakan sebagai database pemulihan bencana, instans ini akan menjadi cadangan instans sumber.
- Ketika ada perubahan yang terjadi di instans sumber, informasi log yang mencatat perubahan akan disalin ke instans pemulihan bencana dan kemudian sinkronisasi data akan diimplementasikan melalui pemutaran ulang log.
- Jika terjadi kegagalan pada instans sumber, instans pemulihan bencana dapat diaktifkan dalam hitungan detik untuk menyediakan kemampuan baca/tulis penuh.

## Batasan Fitur
- Instans pemulihan bencana hanya dapat dibeli untuk instans sumber berkemampuan GTID yang tersedia tinggi di MySQL versi 5.6 atau yang lebih tinggi dengan mesin InnoDB dengan spesifikasi memori 1 GB dan kapasitas disk 50 GB atau lebih. Jika instans sumber Anda di bawah spesifikasi ini, harap tingkatkan terlebih dahulu.
>?Jika GTID tidak diaktifkan, Anda dapat mengaktifkannya di halaman detail instans di [konsol](https://console.cloud.tencent.com/cdb/). Operasi ini memerlukan waktu lama, dan instans akan terputus selama beberapa detik. Sebaiknya lakukan proses ini selama jam tidak sibuk dan tambahkan mekanisme koneksi ulang dalam program yang mengakses database.
- Spesifikasi minimum instans pemulihan bencana adalah memori 1 GB dan kapasitas disk 50 GB dan harus setidaknya 1,1 kali kapasitas penyimpanan yang digunakan oleh instans sumber.
- Satu instans sumber dapat memiliki paling banyak satu instans pemulihan bencana. Meskipun instans pemulihan bencana yang ada sedang diisolasi, Anda tidak dapat membuat instans baru.
- Instans pemulihan bencana tidak mendukung fitur berikut: mentransfer proyek, pengembalian, operasi SQL, pengaturan parameter, mengubah serangkaian karakter, manajemen akun, mengubah port, impor data, log rollback, dan instans baca saja.

## Petunjuk
### Membuat instans pemulihan bencana
#### Langkah 1. Buat instans pemulihan bencana
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail instans.
2. Pastikan fitur GTID diaktifkan dengan melihat informasi dasar instans di halaman **Instance Details** (Detail Instans). Klik **Add Disaster Recovery Instance** (Tambahkan Instans Pemulihan Bencana) dalam diagram arsitektur instans untuk masuk ke halaman pembelian instans pemulihan bencana.
![](https://main.qcloudimg.com/raw/d41ae3d97935763b180f2e8a26cb2364.png)
3. Di halaman pembelian, atur informasi dasar instans pemulihan bencana seperti **Billing Mode** (Mode Penagihan), **Region** (Wilayah), dan **Sync Policy** (Kebijakan Sinkronisasi).
 - Jika kebijakan sinkronisasi adalah **Sync Now** (Sinkronkan Sekarang), data akan segera disinkronkan saat instans pemulihan bencana dibuat.
 - Jika kebijakan sinkronisasi adalah **Sync After Creation** (Sinkronkan Setelah Dibuat), Anda perlu mengonfigurasi tautan sinkronisasi pemulihan bencana setelah instans berhasil dibuat. Untuk petunjuk mendetail, harap lihat [Membuat tautan sinkronisasi](#cjtblj) di bawah.
>?
>- Waktu yang diperlukan untuk menyelesaikan pembuatan bergantung pada jumlah data, selama tidak ada operasi yang dapat dilakukan pada instans sumber di konsol. Harap lakukan langkah ini pada waktu yang tepat.
>- Hanya seluruh data instans yang dapat disinkronkan. Harap pastikan bahwa ruang disk memadai.
>- Anda perlu memastikan bahwa instans sumber dalam keadaan berjalan dan tidak ada tugas penyesuaian konfigurasi, tugas mulai ulang, dan tugas modifikasi lainnya yang dijalankan. Jika tidak, tugas sinkronisasi mungkin gagal.  
4. Setelah mengonfirmasi bahwa semuanya sudah benar, klik **Buy Now** (Beli Sekarang) dan tunggu pengiriman instans pemulihan bencana.
5. Kembali ke daftar instans. Setelah status instans berubah menjadi "Running" (Berjalan), instans dapat digunakan secara normal.

#### [Langkah 2. Buat tautan sinkronisasi (opsional)](id:cjtblj)
>?Jika **Sync Policy** (Kebijakan Sinkronisasi) yang Anda pilih selama pembelian instans adalah **Sync After Creation** (Sinkronkan Setelah Dibuat), Anda perlu mengonfigurasi tautan sinkronisasi pemulihan bencana setelah instans berhasil dibuat. Dengan demikian, Anda dapat menerapkan pemulihan bencana jarak jauh.

1. Di halaman **Instance Details** (Detail Instans) dari instans sumber, Anda dapat melihat status sinkronisasi instans pemulihan bencana. Klik **Create Sync Task** (Buat Tugas Sinkronisasi) untuk membuat tautan sinkronisasi jaringan pribadi dengan instans sumber untuk instans pemulihan bencana.
![](https://main.qcloudimg.com/raw/f2f941ccf588d54cb2687cc0a9d0a961.png)
2. Masukkan nama tugas, konfirmasi informasi database sumber dan target, dan klik **Save and Next** (Simpan dan Berikutnya).
![](https://main.qcloudimg.com/raw/5a2b3ef40de69af903cc60396d8f1a84.png)
3. Pilih objek yang akan disinkronkan. Sinkronisasi seluruh instans atau tabel tertentu didukung. Jenis sinkronisasi tidak dapat disesuaikan saat ini.
![](https://main.qcloudimg.com/raw/ac3f2db7c68f708ac07bb597a420ae83.png)
4. Klik **Save and Check** (Simpan dan Periksa) untuk memeriksa tugas. Setelah pemeriksaan berhasil, klik **Start Task** (Mulai Tugas). Kemudian, Anda dapat melihat detail tugas di halaman **Disaster Recovery Sync** (Sinkronisasi Pemulihan Bencana) di konsol.
![](https://main.qcloudimg.com/raw/4cc319646447bb20a5a76982a0783a49.png)

### Mengelola instans pemulihan bencana
- **View a disaster recovery instances** (Lihat instans pemulihan bencana)
Instans pemulihan bencana dapat dilihat dari wilayah tempat instans tersebut berada. Anda dapat menggunakan daftar instans untuk memfilter semua instans di wilayah tertentu.
![](https://main.qcloudimg.com/raw/1ade1aa59f7c5cd74b2cf30299d31cac.png)
- **View the relationship between the source instance and the disaster recovery instance** (Lihat hubungan antara instans sumber dan instans pemulihan bencana)
Klik ikon di sebelah kanan instans pemulihan bencana atau instans sumber untuk melihat hubungannya.
![](https://main.qcloudimg.com/raw/4b98a6b2831c027af52a37050aa16f2d.png)
![](https://main.qcloudimg.com/raw/f08c6d3dd53a40ea544bdadc9e111ee8.png)
- **View sync delay** (Lihat penundaan sinkronisasi)
Lihat penundaan sinkronisasi antara instans sumber dan instans pemulihan bencana di bagian atas halaman **Instance Details** (Detail Instans) dari instans pemulihan bencana.
![](https://main.qcloudimg.com/raw/d06a9c821f5ebd04173ee6e453ef5ef2.png)
- **Disaster recovery instance features** (Fitur instans pemulihan bencana)
Instans pemulihan bencana memiliki berbagai fitur, seperti tampilan detail instans, pemantauan instans, pengelolaan pencadangan, dan pencatatan kueri yang lambat.
 
### Mempromosikan instans pemulihan bencana ke instans sumber
Anda dapat mempromosikan instans pemulihan bencana ke instans sumber di konsol sesuai kebutuhan.
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans pemulihan bencana yang akan dipromosikan dalam daftar instans, dan akses halaman pengelolaan instans.
2. Klik **Promote to Source Instance** (Promosikan ke Instans Sumber) di sudut kanan atas untuk mempromosikan instans pemulihan bencana ke instans sumber. Setelah promosi, tautan sinkronisasi dengan instans sumber akan terputus, sehingga instans yang dipromosikan bisa mendapatkan kemampuan menulis data dan fungsi MySQL penuh.
>!Tautan sinkronisasi yang terputus tidak dapat dihubungkan kembali. Harap lanjutkan dengan hati-hati.
> 
![](https://main.qcloudimg.com/raw/c4e1517d56c630ff845c89060402e657.png)

