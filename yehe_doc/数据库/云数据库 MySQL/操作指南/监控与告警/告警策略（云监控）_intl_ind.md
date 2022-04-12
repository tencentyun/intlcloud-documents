Dokumen ini menjelaskan cara membuat kebijakan alarm dan mengaitkan objek alarm di konsol Cloud Monitor.

## Ikhtisar
Anda dapat membuat kebijakan alarm untuk memicu alarm dan mengirim pemberitahuan alarm saat status layanan Tencent Cloud berubah. Alarm yang dibuat menentukan apakah pemberitahuan alarm perlu dipicu sesuai dengan hasil perbandingan antara metrik pemantauan dan ambang batas tertentu pada setiap interval.
Anda dapat mengambil tindakan pencegahan atau perbaikan yang sesuai pada waktu yang tepat ketika alarm dipicu. Dengan demikian, alarm yang dibuat dengan benar dapat membantu Anda meningkatkan kecanggihan dan keandalan aplikasi Anda. Untuk informasi selengkapnya tentang alarm, lihat [Membuat Kebijakan Alarm](https://intl.cloud.tencent.com/document/product/248/38916) di Cloud Monitor.

Untuk mengirim alarm pada status produk tertentu, Anda harus membuat kebijakan alarm terlebih dahulu. Kebijakan alarm terdiri dari tiga komponen wajib, yaitu nama, jenis, dan kondisi pemicu alarm. Setiap kebijakan alarm adalah serangkaian kondisi pemicu alarm dalam hubungan logika OR, yaitu, selama salah satu kondisi pemicu terpenuhi, alarm akan dipicu. Alarm akan dikirim ke semua pengguna yang terkait dengan kebijakan alarm. Setelah menerima alarm, pengguna dapat melihat alarm dan mengambil tindakan yang sesuai secara tepat waktu.

>!Pastikan Anda telah mengatur penerima alarm default; jika tidak, kebijakan alarm default TencentDB tidak akan dapat mengirim pemberitahuan.

## Petunjuk
### Membuat kebijakan alarm
1. Login ke konsol [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) dan pilih **Alarm Configuration** (Konfigurasi Alarm) > **Alarm Policy** (Kebijakan Alarm) di bilah sisi kiri.
2. Dalam daftar kebijakan alarm, klik **Add** (Tambahkan).
3. Pada halaman **Create Alarm Policy** (Buat Kebijakan Alarm), tetapkan nama kebijakan, jenis kebijakan, objek alarm, dan kondisi pemicu.
 - **Policy Type** (Jenis Kebijakan): dibagi menjadi pemantauan sumber dan pemantauan replika, yang berlaku untuk berbagai jenis instans.
    - Deploy pemantauan pada sumber: ketika instans yang dipantau adalah instans sumber yang bukan merupakan replika instans apa pun, data pemantauan terkait replikasi tidak valid untuk sumbernya, dan utas IO dan SQL dinonaktifkan. Data pemantauan terkait replikasi valid dan IO serta utas SQL dapat diaktifkan hanya jika instans yang dipantau adalah pemulihan bencana atau replika baca-saja.
    - Menyebarkan pemantauan pada replika: instans sumber dua atau tiga node dan instans pemulihan bencana datang dalam arsitektur sumber/replika secara default. Akibatnya, data pemantauan terkait replikasi valid untuk replika hanya jika instans yang dipantau adalah sumber atau instans pemulihan bencana. Data pemantauan tersebut dapat mencerminkan jarak dan waktu penundaan replikasi antara sumber atau instans pemulihan bencana dan node replika tersembunyinya. Sebaiknya awasi data pemantauan replika tersebut. Jika sumber atau instans pemulihan bencana gagal, node replika tersembunyi yang dipantaunya dapat dipromosikan ke instans sumber dengan cepat.
  - **Alarm Object** (Objek Alarm): instans yang akan dikaitkan dengan alarm kebijakan. Anda dapat menemukan instans yang diinginkan dengan memilih wilayah tempat instans berada atau mencari ID-nya.
 - **Trigger Condition** (Kondisi Pemicu): pemicu alarm adalah kondisi semantik yang terdiri dari metrik, perbandingan, ambang batas, periode statistik, dan durasi. Misalnya, jika metriknya adalah penggunaan disk, perbandingannya adalah >, ambang batasnya adalah 80%, periode statistiknya adalah 5 menit, dan durasinya adalah dua periode statistik, data penggunaan disk suatu database akan dikumpulkan setiap satu kali dalam lima menit, dan alarm akan dipicu jika penggunaan disk melebihi 80% untuk dua kali berturut-turut.
 - **Configure Alarm Notification** (Konfigurasikan Pemberitahuan Alarm): templat default sistem dan templat kustom didukung. Setiap kebijakan alarm dapat dikaitkan dengan hingga tiga templat pemberitahuan.
4. Setelah mengonfirmasi bahwa semuanya sudah benar, klik **Complete** (Selesai).

### Mengaitkan objek alarm
Setelah kebijakan alarm dibuat, Anda dapat mengaitkan beberapa objek alarm dengan kebijakan tersebut. Ketika objek alarm memenuhi kondisi pemicu alarm, pemberitahuan alarm akan dikirim.
1. Dalam daftar [kebijakan alarm](https://console.cloud.tencent.com/monitor/alarm2/policy), klik nama kebijakan alarm untuk masuk ke halaman manajemen kebijakan alarm.
2. Klik **Add Object** (Tambahkan Objek) di bagian **Alarm Object** (Objek Alarm).
![](https://main.qcloudimg.com/raw/00833b7ad2a481ec65b1eb14c0d2cad4.png)
3. Pada kotak dialog pop-up, pilih objek alarm yang akan dikaitkan, dan klik **OK** (OKE).


