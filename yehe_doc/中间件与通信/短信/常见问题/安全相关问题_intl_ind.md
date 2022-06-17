### Berapa batas frekuensi pengiriman SMS default?
Untuk memastikan keamanan bisnis dan saluran serta meminimalkan potensi kerugian finansial yang disebabkan oleh panggilan berbahaya dari API SMS, batas frekuensi pengiriman SMS default adalah sebagai berikut:
- Untuk pesan SMS dengan konten sama, maksimum satu pesan dengan konten sama dapat dikirim ke nomor ponsel yang sama dalam periode 30 detik.
- Maksimum 10 pesan dapat dikirim ke nomor ponsel yang sama pada satu hari kalender.

Pengguna organisasi dapat login ke [konsol SMS](https://console.cloud.tencent.com/smsv2) untuk mengatur atau mengubah kebijakan batas frekuensi pengiriman terkait. Untuk petunjuk mendetail, lihat [Mengatur Batas Frekuensi Pengiriman](https://intl.cloud.tencent.com/document/product/382/35469).
Catatan: pengguna individu tidak memiliki izin untuk mengubah batas frekuensi pengiriman. Untuk menggunakan fitur ini, ubah "Individual Identity" (Identitas Individu) menjadi "Organizational Identity" (Identitas Organisasi). Untuk informasi lebih lanjut tentang hak-hak pengguna organisasi, lihat [Perbedaan hak](https://intl.cloud.tencent.com/document/product/382/40653).

### Bagaimana cara menambahkan penerima alarm?
Untuk petunjuk mendetail, lihat [Configuring Alarm Recipient (Mengonfigurasikan Penerima Alarm)](https://intl.cloud.tencent.com/document/product/382/35470).

### Bagaimana cara mencegah bom SMS (kecurangan)?[](id:Q4)
Bom SMS (kecurangan) merujuk pada penggunaan program atau alat berbahaya dan pemanfaatan kerentanan di klien atau server situs web untuk mengirim sejumlah besar kode verifikasi SMS ke banyak nomor ponsel yang tidak relevan dalam periode waktu tertentu (misalnya dalam satu hari) sehingga menyebabkan gangguan pada para pengguna tersebut.
Bom SMS (kecurangan) tidak hanya menyebabkan gangguan pada pengguna yang tidak tahu apa-apa, tetapi juga menyebabkan tingginya jumlah keluhan, yang membuat saluran SMS tidak tersedia dan mengakibatkan kerugian ekonomi bagi pelanggan. Oleh karena itu, tindakan pencegahan harus dilakukan sebelumnya.
Gambar di bawah ini menunjukkan kasus nyata yang dihadapi oleh pelanggan (dalam keadaan normal, hanya puluhan pesan yang dikirim per hari, tetapi selama serangan bom SMS, puluhan ribu pesan dikirim per hari):
![](https://main.qcloudimg.com/raw/071fbb50d64aa2dcc1f44e0e12ced9eb.png)
Karena serangan bom SMS (kecurangan) umumnya dimulai oleh server, langkah-langkah komprehensif berikut sebaiknya diterapkan guna memberikan perlindungan:

- Batasi jumlah permintaan yang diizinkan per IP.
- Batasi jumlah tugas pengiriman yang diizinkan per nomor ponsel. Untuk melakukannya, Anda dapat [mengatur batas frekuensi pengiriman](https://intl.cloud.tencent.com/document/product/382/35469) dan [mengonfigurasikan penerima alarm](https://intl.cloud.tencent.com/document/product/382/35470).
- [Atur pemberitahuan pengiriman yang melebihi batas](https://intl.cloud.tencent.com/document/product/382/35469).
- Login ke [konsol SMS](https://console.cloud.tencent.com/smsv2) untuk melihat statistik tertentu dan memeriksa pengiriman SMS secara teratur (misalnya sekali setiap hari). Jika pengecualian ditemukan, Anda dapat menonaktifkan layanan SMS di konsol dalam keadaan darurat.

### Apa perbedaan antara SMS Tiongkok Daratan dan SMS Global?
Tanda tangan SMS harus disertakan dalam pesan SMS Tiongkok Daratan karena persyaratan operator, tetapi, untuk pesan SMS Global, ketentuan ini bersifat opsional dan bergantung pada Anda.
- Sebelum mengirim pesan SMS Tiongkok Daratan, Anda harus [membuat tanda tangan](https://intl.cloud.tencent.com/document/product/382/35456) dan [templat isi](https://intl.cloud.tencent.com/document/product/382/35457) serta memperoleh persetujuan terlebih dahulu.
- Sebelum mengirim pesan SMS Global, Anda harus [membuat templat isi](https://intl.cloud.tencent.com/document/product/382/35461) dan memperoleh persetujuan terlebih dahulu. Jika ingin menyertakan tanda tangan, Anda juga perlu [membuat tanda tangan](https://intl.cloud.tencent.com/document/product/382/35460) dan memperoleh persetujuan.

### Bagaimana cara memeriksa catatan pengiriman untuk setiap nomor ponsel?
Anda dapat login ke [konsol SMS](https://console.cloud.tencent.com/smsv2), lalu klik nama aplikasi target untuk masuk ke halaman detail aplikasi, dan pilih salah satu metode berikut untuk melakukan kueri sesuai dengan kebutuhan aktual Anda:
- SMS Tiongkok Daratan: pilih **Business Statistics** > **Chinese Mainland SMS** > **Message Records** (Statistik Bisnis > SMS Tiongkok Daratan > Catatan Pesan) dan masukkan nomor ponsel untuk melakukan kueri seperti yang ditunjukkan di bawah ini:
![](https://qcloudimg.tencent-cloud.cn/raw/a727c37158e9b9d3688ebfeabc13d512.png)
- SMS Global: pilih **Business Statistics** > **Global SMS** > **Message Records** (Statistik Bisnis > SMS Global > Catatan Pesan) untuk melakukan kueri.

### Bagaimana cara membuat dan melihat aplikasi (SDK AppID)?
SDK AppID digunakan untuk mengidentifikasi aplikasi. Setiap aplikasi SMS memiliki SDK AppID unik, yang dibuat secara otomatis oleh sistem setelah aplikasi dibuat. Untuk petunjuk mendetail, lihat [Creating Application (Membuat Aplikasi)](https://intl.cloud.tencent.com/document/product/382/35468).
Anda dapat login ke [konsol SMS](https://console.cloud.tencent.com/smsv2), lalu pilih **Application Management** > **Application List** (Manajemen Aplikasi > Daftar Aplikasi), dan klik nama aplikasi target untuk masuk ke halaman detail aplikasi dan melihat SDK AppID-nya.

### Bagaimana cara mengaktifkan daftar izin batas tingkat pengiriman untuk menguji dan memperingatkan nomor ponsel?
Untuk menghapus batas tingkat pengiriman guna menguji nomor ponsel, silakan hubungi [Bantuan SMS](https://tccc.qcloud.com/web/im/index.html#/chat?webAppId=8fa15978f85cb41f7e2ea36920cb3ae1&title=Sms).

### Bagaimana cara memeriksa apakah nomor ponsel tertentu telah menerima pesan?
Anda dapat login ke [konsol SMS](https://console.cloud.tencent.com/smsv2), lalu klik nama aplikasi target untuk masuk ke halaman detail aplikasi, dan pilih salah satu metode berikut untuk melakukan kueri atau mengekspor catatan sesuai dengan kebutuhan aktual Anda:
- SMS Tiongkok Daratan: pilih **Business Statistics** > **Chinese Mainland SMS** > **Message Records** (Statistik Bisnis > SMS Tiongkok Daratan > Catatan Pesan) untuk melakukan kueri atau mengekspor catatan dalam periode waktu tertentu.
- SMS Global: pilih **Business Statistics** > **Global SMS** > **Message Records** (Statistik Bisnis > SMS Global > Catatan Pesan) untuk melakukan kueri atau mengekspor catatan dalam periode waktu tertentu.

### Apakah ada batasan jumlah pesan SMS Global yang dapat dikirim?
Satu akun Tencent Cloud dapat mengirim maksimum 1.000 pesan SMS Global per hari. Untuk menyesuaikan batasan ini, Anda dapat menghubungi [Bantuan SMS](https://tccc.qcloud.com/web/im/index.html#/chat?webAppId=8fa15978f85cb41f7e2ea36920cb3ae1&title=Sms).
