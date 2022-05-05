Dokumen ini menjelaskan cara mengatur replikasi tertunda untuk instans baca saja dan mengaktifkan/menonaktifkan replikasi di konsol TencentDB for MySQL. Anda dapat mengatur replikasi tertunda (yaitu, penundaan antara instans baca saja dan instans sumbernya) dan memilih untuk memutar ulang berdasarkan posisi flashback atau pengidentifikasi transaksi global (GTID) selama penundaan untuk secara efisien mengembalikan data dan memperbaiki kegagalan.
- Replikasi Tertunda: Anda dapat mengaktifkan dan mengonfigurasi penundaan replikasi antara instans baca saja dan instans sumbernya pada halaman konfigurasi grup RO atau halaman pengelolaan.
- Mengaktifkan/Menonaktifkan Replikasi: Anda dapat secara manual mengaktifkan atau menonaktifkan sinkronisasi data antara instans baca saja dan instans sumbernya.

## Deskripsi Replikasi Tertunda
- Setelah diaktifkan untuk instans baca saja, replikasi tertunda akan dihapus dari grup RO dengan bobotnya diatur ke 0, dan alarm penghapusan akan dipicu. Pada titik ini, lalu lintas tidak akan diteruskan ke instans yang dihapus jika RO VIP digunakan untuk mengakses grup RO. Terlebih lagi, instans yang dihapus hanya dapat diakses melalui VIP instans.
- Setelah replikasi tertunda dinonaktifkan untuk instans baca saja ( grup RO yang sesuai telah mengaktifkan penghapusan instans-replikasi-baca-saja), bobot instans baca saja ini dalam grup RO akan dipulihkan hanya jika waktu tunda instans ini kurang dari ambang batas penundaan grup RO.  Dan alarm pemulihan akan dipicu pada saat yang bersamaan.
- Selama pemutaran ulang dengan posisi flashback, Anda tidak dapat memulai ulang instans, menyesuaikan konfigurasinya, meningkatkan versinya, atau meningkatkan versi minor kernelnya.

## Mengaktifkan Replikasi Tertunda
>?**Delayed Replication** (Replikasi Tertunda) **disabled** (dinonaktifkan) untuk instans baca saja secara default. Jika diaktifkan, waktu replikasi yang tertunda akan ditampilkan.

### Mengaktifkan di halaman konfigurasi grup RO instans baca saja
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Di daftar instans, klik ID instans untuk masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Read-Only Instance** (Instans Baca Saja), cari grup RO yang diinginkan, dan klik **Configuration** (Konfigurasi) untuk masuk ke halaman konfigurasi grup RO.
![](https://qcloudimg.tencent-cloud.cn/raw/87041c7addd9dcfd058b2d3f7c417625.png)
3. Pada halaman konfigurasi grup RO, aktifkan **Delayed Replication** (Replikasi Tertunda), atur **Replication Delay** (Penundaan Replikasi), dan klik **OK** (OKE).
   Anda dapat mengatur replikasi tertunda dan memilih untuk memutar ulang dengan posisi flashback atau pengidentifikasi transaksi global (GTID) selama penundaan untuk secara efisien mengembalikan data dan memperbaiki kegagalan.
   - **Replication Delay** (Penundaan Replikasi): Anda dapat mengonfigurasi waktu replikasi tertunda antara instans baca saja dan instans sumbernya. Rentang nilainya adalah 1–259200 detik.
   - **Remove Delayed RO Instances** (Hapus Instans RO Tertunda): opsi ini menunjukkan apakah akan mengaktifkan kebijakan penghapusan. Jika instans baca saja dihapus saat penundaannya melebihi ambang batas, bobotnya akan diatur ke 0 secara otomatis, dan alarm akan dikirim (untuk informasi selengkapnya tentang cara mengonfigurasi alarm dan penerima penghapusan instans baca saja, lihat [Alarm Kebijakan (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457)).
   - **Delay Threshold** (Ambang Batas Penundaan): ini menetapkan ambang batas penundaan untuk instans baca saja. Jika ambang batas terlampaui, instans akan dihapus dari grup baca saja.
   - **Least RO Instances** (Instans RO Terkecil): ini adalah jumlah minimum instans yang harus dipertahankan dalam grup RO. Ketika ada lebih sedikit instans dalam grup RO, meski melebihi ambang batas penundaan, instans tidak akan dihapus.
   - **Assign Read Weight** (Tetapkan Bobot Baca): grup RO mendukung dua metode penetapan bobot: penetapan otomatis oleh sistem dan penetapan kustom. Nilai bobot harus berupa bilangan bulat antara 0 dan 100.
   - **Load Rebalancing** (Penyeimbangan Ulang Beban):
    - Memodifikasi bobot hanya akan memengaruhi beban baru jika penyeimbangan ulang dinonaktifkan. Operasi tidak berdampak pada instans baca saja yang diakses oleh koneksi persisten yang ada dan tidak menyebabkan pemutusan database semantara.
    - Jika penyeimbangan ulang diaktifkan, semua koneksi ke database akan terputus sementara, dan beban koneksi yang baru ditambahkan akan diseimbangkan sesuai dengan bobot yang ditetapkan.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c40a92c3a6dcc083ac92f01169b259ff.png"  style="zoom:50%;">

### Mengaktifkan pada halaman manajemen instans baca saja
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans baca saja atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman detail instans baca saja.
2. Pada halaman detail instans baca saja, klik **Enable** (Aktifkan) di **Deployment Info** (Info Deployment) > **Delayed Replication** (Replikasi Tertunda).
![](https://qcloudimg.tencent-cloud.cn/raw/280f08c04f692445f51b1ab4aa556f58.png)
3. Di jendela pop-up, atur penundaan dan klik **OK** (OKE).
>?Penundaan berkisar antara 1 hingga 259.200 detik.
>Instans Baca Saja dalam grup RO yang sama berbagi penundaan replikasi yang sama. Jika satu instans dimodifikasi, sisanya akan dimodifikasi secara otomatis pada saat yang bersamaan.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/32877ca9c8ab4bb3030bbb508c899374.png"  style="zoom:80%;">

## Memodifikasi Replikasi Tertunda
### Memodifikasi halaman konfigurasi grup RO instans baca saja
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Di daftar instans, klik ID instans untuk masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Read-Only Instance** (Instans Baca Saja), cari grup RO yang diinginkan, dan klik **Configuration** (Konfigurasi) untuk masuk ke halaman konfigurasi grup RO.
3. Pada halaman konfigurasi grup RO, ubah **Replication Delay** (Penundaan Replikasi) dan klik **OK** (OKE).
<img src="https://qcloudimg.tencent-cloud.cn/raw/437d781e478652416c166449b4420910.png"  style="zoom:60%;">

### Memodifikasi pada halaman manajemen instans baca saja
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb) dan klik ID instans baca saja di daftar instans untuk masuk ke halaman detail instans baca saja.
2. Pada halaman detail instans baca saja, klik **Modify** (Modifikasi) di **Deployment Info** (Info Deployment) > **Delayed Replication** (Replikasi Tertunda).  

<img src="https://qcloudimg.tencent-cloud.cn/raw/5098762edf0e478942ad060c5bd80da5.png"  style="zoom:80%;">
3. Di jendela pop-up, atur penundaan dan klik **OK** (OKE).

## Menonaktifkan Replikasi Tertunda
### Menonaktifkan pada halaman konfigurasi grup RO instans baca saja
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Di daftar instans, klik ID instans untuk masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Read-Only Instance** (Instans Baca Saja), cari grup RO yang diinginkan, dan klik **Configuration** (Konfigurasi) untuk masuk ke halaman konfigurasi grup RO.
3. Pada halaman konfigurasi grup RO, klik **Delayed Replication** (Replikasi Tertunda) dan klik **OK** (OKE).
<img src="https://qcloudimg.tencent-cloud.cn/raw/9191e1c61694da2970323b59a21c59f3.png"  style="zoom:70%;">

### Menonaktifkan pada halaman manajemen instans baca saja
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb) dan klik ID instans baca saja di daftar instans untuk masuk ke halaman detail instans baca saja.
2. Pada halaman detail instans baca saja, klik **Disable** (Nonaktifkan) di **Deployment Info** (Info Deployment) > **Delayed Replication** (Replikasi Tertunda).

<img src="https://qcloudimg.tencent-cloud.cn/raw/5f3a33f7b23513b8766eb62455406478.png"  style="zoom:80%;">
3. Di kotak dialog pop-up, konfirmasikan bahwa semuanya sudah benar dan klik **OK** (OKE).
>?Jika replikasi tertunda dinonaktifkan, waktu replikasi tertunda akan menjadi 0 detik, yaitu, sinkronisasi data real-time dilanjutkan antara instans baca saja dan instans sumbernya. 
> 

## Mengaktifkan Replikasi Data
>?**Replication Status** (Status Replikasi) dari instans baca saja adalah **Normal** (Normal) secara default. Jika Anda mengatur replikasi tertunda dan menghapus data secara tidak sengaja selama periode waktu replikasi tertunda, Anda dapat memulihkan instans baca saja ke posisi yang ditentukan atau GTID file binlog untuk menerapkan pemulihan data cepat.
>
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb) dan klik ID instans baca saja di daftar instans untuk masuk ke halaman detail instans baca saja.
2. Pada halaman detail instans baca saja, klik **Enable** (Aktifkan) di **Deployment Info** (Info Deployment) > **Replication Status** (Status Replikasi).
<img src="https://qcloudimg.tencent-cloud.cn/raw/29703db36415992fda7e1767a7b830e8.png"  style="zoom:80%;">
3. Di jendela pop-up, klik **OK** (OKE).
>? Setelah replikasi diaktifkan, sinkronisasi data antara instans baca saja dan instans sumber akan dilanjutkan.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/ab58491f328ffe447f8790105699f13b.png"  style="zoom:80%;">
4. Anda juga dapat memilih **Replay by Flashbacked Position** (Putar Ulang menurut Posisi Flashback) di **Deployment Info** (Info Deployment) > **Operation** (Operasi). Kemudian, data dapat dikembalikan ke titik waktu yang ditentukan atau GTID yang sesuai. Setelah pemulihan, replikasi instans baca saja akan dinonaktifkan hingga mode mulai dialihkan ke **Replicate all** (Replikasi semua).
    - Waktu: Anda dapat memilih titik waktu antara waktu akhir replikasi dan waktu saat ini dari instans sumber.
    - GTID: Anda dapat memilih semua log setelah binlog tidak diterapkan. Jika GTID dipilih, data akan direplikasi hingga GTID yang ditentukan tercapai.
Panjang instans `server_uuid` ditetapkan pada 36 bit, dan GTID harus dalam format `server_uuid:transaction_id`.
>!
>- Jika posisi binlog yang dimasukkan telah diterapkan pada instans baca saja atau setelah posisi instans sumber, replikasi akan gagal diaktifkan.
>- Saat Anda mengaktifkan replikasi, jika ada breakpoint di binlog, replikasi akan gagal diaktifkan.
>- Untuk menghindari penggunaan berlebihan ruang disk dari instans baca saja yang tertunda saat replikasi dinonaktifkan untuknya, utas I/O dari instans baca saja akan dijeda saat ruang disk yang tersedia di bawah 5 GB.
> 
<img src="https://qcloudimg.tencent-cloud.cn/raw/92671ad35d5ef5acbfdf3bfbb47f967a.png"  style="zoom:85%;">
5. Selama proses pemutaran ulang menurut posisi flashback, Anda dapat mengklik **Replaying** (Memutar ulang) setelah **Replication Status** (Status Replikasi) untuk mengkueri dan memuat ulang detail tugas.  

<img src="https://qcloudimg.tencent-cloud.cn/raw/39274c3aa8e92e6c4dfe0a242de0392e.png"  style="zoom:85%;">
6. Setelah replikasi selesai, klik **Enable** (Aktifkan) setelah **Replication Status** (Status Replikasi), dan instans baca saja dapat terus mereplikasi.  

<img src="https://qcloudimg.tencent-cloud.cn/raw/b27f75181ebae1e8c9b833762ba9388d.png"  style="zoom:85%;">


## Menonaktifkan Replikasi Data
>?
>- Hanya setelah diaktifkan, replikasi tertunda dapat dinonaktifkan; jika tidak, tombol **Disable** (Nonaktifkan) akan berwarna abu-abu.
>- Setelah replikasi dinonaktifkan, utas I/O dan SQL juga akan diakhiri.
>
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb) dan klik ID instans baca saja di daftar instans untuk masuk ke halaman detail instans baca saja.
2. Pada halaman detail instans baca saja, klik **Disable** (Nonaktifkan) di **Deployment Info** (Info Deployment) > **Replication Status** (Status Replikasi).
<img src="https://main.qcloudimg.com/raw/8921d228b70bf42ca5120d6fcf44e92c.png"  style="zoom:85%;">
3. Di kotak dialog pop-up, konfirmasikan bahwa semuanya sudah benar dan klik **OK** (OKE).

## Pertanyaan Umum
#### Bagaimana cara mendapatkan GTID?
Sebaiknya jalankan perintah `flush log` untuk mendapatkan file binlog untuk menemukan posisi dan GTID dari kesalahan operasi.

#### Bagaimana cara melihat penundaan?
Anda dapat melihat penundaan antara instans baca saja dan instans sumbernya pada halaman detail instans di [konsol](https://console.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/0b975dfca0c575735b94445f11e30d67.png)

#### Bagaimana cara melihat informasi tugas pemutaran ulang menurut posisi flashback?
Anda dapat melihat kemajuan dan detail tugas pada halaman daftar tugas di [konsol](https://console.cloud.tencent.com/mysql/task).


