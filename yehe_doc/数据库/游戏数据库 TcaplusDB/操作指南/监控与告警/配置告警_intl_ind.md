## Skenario Operasi
Anda dapat membuat alarm untuk memperingatkan Anda tentang perubahan status produk cloud dan mengirim pesan terkait. Alarm yang dibuat menentukan apakah pemberitahuan alarm perlu dipicu sesuai dengan hasil perbandingan antara metrik pemantauan dan ambang batas tertentu pada setiap interval.
Anda dapat mengambil tindakan pencegahan atau perbaikan yang tepat pada waktu yang tepat ketika alarm dipicu. Dengan demikian, alarm yang dibuat dengan benar dapat membantu Anda meningkatkan kecanggihan dan keandalan aplikasi Anda. Untuk informasi selengkapnya tentang alarm, silakan lihat [Konfigurasi Alarm](https://intl.cloud.tencent.com/document/product/248/38916) di Cloud Monitor.

Jika Anda ingin mengirim pesan alarm untuk status produk tertentu, Anda harus membuat kebijakan alarm terlebih dahulu, yang terdiri dari tiga komponen wajib: nama, jenis, dan kondisi pemicu alarm. Setiap kebijakan alarm adalah serangkaian kondisi pemicu alarm dalam hubungan logika OR, yaitu, selama salah satu kondisi pemicu terpenuhi, alarm akan dipicu. Pemberitahuan alarm akan dikirim ke semua pengguna yang terkait dengan kebijakan alarm. Pengguna dapat mengambil tindakan yang sesuai setelah menerima pemberitahuan.

>Pastikan Anda telah mengatur penerima alarm default; jika tidak, kebijakan alarm default TencentDB tidak akan dapat mengirim pemberitahuan.


## Petunjuk
### Membuat kebijakan alarm
1. Masuk ke [Konsol Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) dan pilih **Alarm Configuration** (Konfigurasi Alarm) > **Alarm Policy** (Kebijakan Alarm) di bilah sisi kiri.
2. Dalam daftar kebijakan alarm, klik **Add** (Tambahkan).
3. Atur nama kebijakan, jenis kebijakan, produk target, objek alarm, dan kondisi pemicu.
 - Jenis Kebijakan: pilih "TcaplusDB".
 - Objek Alarm: pilih semua objek atau tabel tertentu. Objek yang akan dikaitkan dapat ditemukan dengan memilih wilayah tempat objek berada atau mencari ID objek.
 - Kondisi Pemicu: pemicu alarm adalah kondisi semantik yang terdiri dari metrik, hubungan perbandingan, ambang batas, periode statistik, dan durasi.
 - Saluran alarm yang didukung termasuk SMS dan email.
4. Setelah mengonfirmasi bahwa semuanya sudah benar, klik **Complete** (Selesai).

### Mengaitkan objek
Setelah kebijakan alarm dibuat, Anda dapat mengaitkan beberapa objek alarm dengan kebijakan tersebut. Ketika objek alarm memenuhi kondisi pemicu alarm, pemberitahuan alarm akan dikirim.
1. Dalam daftar kebijakan alarm, klik nama kebijakan alarm untuk masuk ke halaman manajemen kebijakan alarm.
2. Klik **Add Object** (Tambahkan Objek) di halaman manajemen kebijakan alarm.
![](https://main.qcloudimg.com/raw/00833b7ad2a481ec65b1eb14c0d2cad4.png)
3. Pilih layanan Tencent Cloud yang diinginkan dan klik **Apply** (Terapkan) untuk mengaitkannya dengan kebijakan alarm.

### Mengatur penerima alarm
Penerima alarm adalah mereka yang akan menerima pesan alarm.
1. Dalam daftar kebijakan alarm, klik nama kebijakan alarm.
2. Pada halaman manajemen kebijakan alarm, pilih **Alarm Recipient Object** (Objek Penerima Alarm) dan klik **Edit** (Edit).
3. Pilih grup pengguna yang akan diberi tahu, atur opsi yang relevan, lalu klik **Save** (Simpan).

