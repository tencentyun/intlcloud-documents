
Dokumen ini menjelaskan cara mengaktifkan pemisahan baca/tulis proksi database di konsol TencentDB for MySQL.

Dengan fitur [pemisahan baca/tulis proksi database](https://intl.cloud.tencent.com/document/product/236/41093), Anda dapat mengonfigurasi alamat proksi database di aplikasi Anda sehingga dapat meneruskan permintaan tulis ke instans sumber dan permintaan baca ke instans baca saja secara otomatis.

## Prasyarat
- Anda telah [mengaktifkan proksi database](https://intl.cloud.tencent.com/document/product/236/41087).
- Anda telah [membuat instans baca saja](https://intl.cloud.tencent.com/document/product/236/7270) untuk instans sumber. Jika tidak ada instans baca saja yang dibuat, halaman pengaktifan fitur akan meminta Anda agar membelinya.

## Petunjuk
1. Login ke [Konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, pilih instans sumber dengan proksi yang diaktifkan dan klik ID-nya atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih **Database Proxy** (Proksi Database) > **Read/Write Separation** (Pemisahan Baca/Tulis) > **Enable Now** (Aktifkan Sekarang).
![](https://main.qcloudimg.com/raw/b07508f045b727ca63c294b707159474.png)
3. Di jendela yang ditampilkan, atur item konfigurasi seperti **Remove Delayed RO Instances** (Hapus Instans RO yang Tertunda) dan bobot, lalu klik **OK** (OKE).
>!
>- Hanya instans sumber dan baca saja yang berada dalam status **Running** (Berjalan) yang dapat ditambahkan ke proksi database.
>- Saat ini, instans baca saja jarak jauh atau tertunda tidak dapat dipasang ke proksi database.
>
 - **Remove Delayed RO Instances** (Hapus Instans RO yang Tertunda): tentukan apakah akan mengaktifkan kebijakan penghapusan. Jika pengecualian replikasi (seperti penundaan atau gangguan replikasi) terjadi pada instans baca saja, proksi database akan menghapus instans dari pemisahan baca/tulis untuk sementara. Batas penundaan adalah 10 detik secara default, dan setidaknya 1 instans baca saja harus dipertahankan.
 >?Pengaturan **Delay Threshold** (Batas Penundaan) dan **Least RO Instance** (Instans RO Terkecil) hanya berlaku untuk koneksi baru.
 >
    - Jika penundaan instans baca saja melebihi ambang batas, instans akan dihapus, bobotnya akan secara otomatis diatur ke 0 setelah penghapusan, dan sistem akan mengirimkan alarm kepada Anda (Anda harus berlangganan alarm "penghapusan node yang terpasang pada database proksi" terlebih dahulu. Untuk konfigurasi, silakan lihat [Kebijakan Alarm (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457)).
    - Instans akan dimasukkan kembali ke proksi database saat penundaannya turun di bawah ambang batas. Terlepas dari apakah penghapusan instans baca saja yang tertunda diaktifkan, instans baca saja yang dihapus karena kegagalan instans akan bergabung kembali dengan proksi database saat diperbaiki.
    - Setelah **Least RO Instances** (Instans RO Terkecil) diatur, jika proksi database menemukan bahwa jumlah instans baca saja yang dirutekan lebih kecil dari nilai yang ditetapkan, maka akan menambahkan instans baca saja yang luar biasa ke pemisahan baca/tulis hingga jumlah instans dalam pemisahan baca/tulis lebih besar dari atau sama dengan nilai yang ditetapkan.
Catatan: jika kegagalan fatal (seperti waktu henti) terjadi pada instans baca saja, itu tidak dapat dipertahankan dan dihitung ke dalam **Least RO Instances** (Instans RO Terkecil).
 - **Assign Read Weight** (Tetapkan Bobot Baca): dua metode penetapan bobot (penetapan otomatis oleh sistem dan penetapan kustom) didukung untuk mengonfigurasi bobot baca dari sumber dan instans baca saja. Nilai bobot harus berupa bilangan bulat antara 0 dan 100.
 >?Penetapan bobot baca yang dikonfigurasi segera berlaku untuk semua koneksi.
 >
    - Proksi database akan menetapkan lalu lintas permintaan baca sesuai dengan bobot yang ditetapkan; misalnya, jika bobot dua instans baca saja masing-masing adalah 10 dan 20, lalu lintas permintaan bacanya akan ditetapkan dengan rasio 1:2.
    - Bobot di sini mengacu pada bobot permintaan baca saja, karena permintaan tulis diarahkan langsung ke database sumber tanpa berpartisipasi dalam penghitungan bobot; misalnya, jika klien mengirim 10 pernyataan tulis dan 10 pernyataan baca, dan rasio bobot instans sumber dan baca saja adalah 1:1, instans sumber akan menerima 10 pernyataan tulis dan 5 pernyataan baca, dan  instans baca saja akan menerima 5 pernyataan baca saja.
    - Jika Anda memilih **Assigned by system** (Ditetapkan oleh sistem), sistem akanmenetapkan bobot secara otomatis berdasarkan spesifikasi CPU dan memori instans, dan dalam hal ini, Anda hanya dapat mengatur bobot instans sumber.
    - Jika bobot instans baca saja adalah 0, proksi database tidak akan terhubung ke instans. Jika bobotnya diubah dari 0 ke nilai lain, bobotnya hanya berlaku untuk koneksi baru.
 - **Failover** (Failover): sebaiknya Anda mengaktifkan parameter ini, sehingga proksi database dapat mengirim permintaan baca ke instans sumber jika semua instans baca saja adalah pengecualian.
 >?Kemampuan failover yang dikonfigurasi hanya berlaku untuk koneksi baru.
 >
Jika parameter ini dinonaktifkan, saat instans baca saja adalah pengecualian, permintaan baca tidak akan dikirim ke instans sumber (untuk mencegah instans sumber terpengaruh oleh beban baca yang tinggi). Namun, semua permintaan baca akan gagal, setelah itu, proksi database akan secara proaktif menutup koneksi ke klien.
 - **Apply to Newly Added RO Instances** (Terapkan ke Instans RO yang Baru Ditambahkan): setelah parameter ini diaktifkan, instans baca saja yang dibuat selanjutnya untuk instans sumber akan ditambahkan secara otomatis ke proksi database.
![](https://main.qcloudimg.com/raw/f2eb858b2b37fd134913738b243a17e8.png)
4. Setelah berhasil mengaktifkan fitur pemisahan baca/tulis, Anda dapat melihat informasi dasar dan diagram arsitekturnya serta memodifikasi item konfigurasi yang relevan pada tab **Read/Write Separation** (Pemisahan Baca/Tulis).
  - Anda dapat mengklik **Modify** (Ubah) di sudut kanan atas untuk mengonfigurasi **Remove Delayed RO Instances** (Hapus Instans RO yang Tertunda), menetapkan bobot, dan mengubah item konfigurasi lainnya lagi.
  - Anda dapat mengklik **Disable Read/Write Separation** (Nonaktifkan Pemisahan Baca/Tulis) di sudut kanan atas untuk menonaktifkan pemisahan baca/tulis dari proksi database.
![](https://main.qcloudimg.com/raw/098c9fae971719881b6d20eee6ba0e73.png)
