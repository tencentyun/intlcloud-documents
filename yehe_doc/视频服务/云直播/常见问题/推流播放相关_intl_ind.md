[](id:que1)
### Apakah ada batas atas untuk jumlah pemirsa bersamaan?   
Secara default, CSS tidak membatasi jumlah pemirsa online untuk suatu streaming langsung jika jaringan dan kondisi lainnya memungkinkan. Namun, jika Anda mengonfigurasikan batas bandwidth, pemirsa baru tidak dapat menonton streaming langsung jika jumlah pemirsa yang sudah ada sangat banyak dan melebihi batas bandwidth. Dalam kasus ini, jumlah pemirsa online akan dibatasi.

[](id:que2)
### Bagaimana cara menggunakan transcoding untuk pemutaran ulang?
Anda dapat membuka [Live Transcoding (Transcoding Langsung)](https://console.cloud.tencent.com/live/config/transcode) untuk mengonfigurasi templat transcoding dengan beragam bitrate dan resolusi untuk berbagai kondisi jaringan. Informasi selengkapnya tentang transcoding dapat dilihat di [Live Remuxing and Transcoding (Transcoding dan Remuxing Langsung)](https://intl.cloud.tencent.com/document/product/267/31561).

[](id:multirate)
#### Definisi asli, HD, dan SD
Streaming definisi asli, HD, dan SD umum digunakan dalam skenario bisnis.
 - Untuk streaming asli, bitrate dan resolusi pemutaran ulang adalah nilai aslinya.
 - Untuk streaming HD, bitrate 2.000 Kbps dan resolusi 1080p direkomendasikan untuk pemutaran ulang.
 - Untuk streaming SD, bitrate 1.000 Kbps dan resolusi 720p direkomendasikan untuk pemutaran ulang.

[](id:que3)
### Bagaimana cara menggunakan pergeseran waktu untuk pemutaran ulang?
Anda dapat menggunakan fitur pergeseran waktu untuk memutar ulang sorotan. Untuk saat ini, fitur ini hanya mendukung protokol HLS. Informasi selengkapnya tentang pergeseran waktu dan cara mengaktifkannya dapat dilihat di [CSS Time Shifting (Pergeseran Waktu CSS)](https://intl.cloud.tencent.com/document/product/267/31565).

[](id:que4)
### Bagaimana cara menggunakan HTTPS untuk pemutaran ulang?
Agar domain pemutaran ulang dapat mendukung HTTPS, Anda harus menyiapkan sertifikat yang valid dan kunci privat yang valid dengan membuka [Domain Management (Manajemen Domain)](https://console.cloud.tencent.com/live/domainmanage), menemukan nama domain pemutaran ulang yang diinginkan, mengeklik **Manage** (Kelola), dan memilih **Advanced Configuration** > **HTTPS Configuration** (Konfigurasi Lanjutan > Konfigurasi HTTPS) untuk menambahkan konfigurasi. Setelah berhasil ditambahkan, konfigurasi akan diterapkan dalam 2 jam, dan setelah itu streaming Anda dapat diputar ulang dengan protokol HTTPS.

[](id:que5)
### Bagaimana cara menggunakan node akselerasi di luar Tiongkok Daratan untuk pemutaran ulang?
CSS memberikan node CDN yang stabil di Tiongkok Daratan dan seluruh dunia. Jika pengguna akhir Anda berada di luar wilayah Tiongkok Daratan, Anda dapat memilih **Global** atau **Outside Chinese mainland** (Luar Tiongkok Daratan) untuk **Acceleration Region** (Wilayah Akselerasi) saat mengonfigurasikan domain di [Domain Management (Manajemen Domain)](https://console.cloud.tencent.com/live/domainmanage).


[](id:que6)
### Bagaimana cara mengaktifkan perlindungan hotlink?
Anda harus mengaktifkan perlindungan hotlink untuk URL pemutaran ulang agar pengguna tidak sah tidak dapat menggunakan URL pemutaran ulang Anda, yang dapat meningkatkan penggunaan lalu lintas Tencent Cloud Anda dan menyebabkan kerugian. Perlindungan hotlink CSS untuk URL pemutaran ulang dikontrol oleh `txTime`, `key` (hash key), `txSecret`, dan masa berlaku.

| Parameter Perlindungan Hotlink | Deskripsi | Keterangan |
|---------|---------|---------|
| txTime | Waktu kedaluwarsa URL pemutaran ulang | Parameter ini menggunakan format waktu Unix heksadesimal.<br> Jika `txTime` lebih besar daripada waktu permintaan, streaming dapat diputar ulang tanpa masalah; jika tidak, permintaan akan ditolak.|
| key | Kunci MD5 | Anda dapat menyesuaikan parameter ini serta mengatur kunci utama dan kunci cadangan.<br> Jika kunci utama diketahui orang lain, Anda dapat menggunakan kunci cadangan untuk menyambungkan URL pemutaran ulang dan mengubah nilai kunci utama.|
| txSecret | Parameter enkripsi dalam URL pemutaran ulang | Nilai parameter ini dihitung berdasarkan `key`, `StreamName`, dan `txTime` menggunakan algoritma MD5. <br>`txSecret` = MD5 (key+StreamName+txTime) |
| Masa berlaku | Masa berlaku autentikasi | Nilai parameter ini harus lebih besar dari 0.<br> Jika Anda mengatur `txTime` ke waktu saat ini dan masa berlaku ke 300 detik, waktu kedaluwarsa URL pemutaran ulang sama dengan waktu saat ini ditambah 300 detik.|

[](id:calculate)
### Penghitungan URL perlindungan hotlink
Penghitungan URL perlindungan hotlink memerlukan tiga parameter: `key` (string acak), `StreamName` (nama streaming), dan `txTime` (dalam format heksadesimal).
Misalnya, Anda mengatur `key` ke **somestring** (string acak), `StreamName` ke **test** (uji), `txTime` ke **5c2acacc** (2019-01-01 10:05:00), bitrate HD ke **900 Kbps**, dan nama templat transcoding ke **900**.
Berikut adalah URL pemutaran ulang untuk streaming asli:
```
txSecret = MD5(somestringtest5c2acacc) = b77e812107e1d8b8f247885a46e1bd34
http://domain/live/test.flv?txTime=5c2acacc&txSecret=b77e812107e1d8b8f247885a46e1bd34
http://domain/live/test.m3u8?txTime=5c2acacc&txSecret=b77e812107e1d8b8f247885a46e1bd34
```
Berikut adalah URL pemutaran ulang untuk streaming HD:
```
txSecret = MD5(somestringtest_9005c2acacc) = 4beae959b16c77da6a65c7edda1dfefe
http://domain/live/test_900.flv?txTime=5c2acacc&txSecret=4beae959b16c77da6a65c7edda1dfefe
http://domain/live/test_900.m3u8?txTime=5c2acacc&txSecret=4beae959b16c77da6a65c7edda1dfefe
```

[](id:open)
#### Mengaktifkan perlindungan hotlink
1. Login ke konsol CSS dan klik [Domain Management (Manajemen Domain)](https://console.cloud.tencent.com/live/domainmanage).
2. Temukan dan klik nama domain pemutaran ulang Anda, atau klik **Manage** (Kelola) untuk masuk ke halaman detail nama domain.
3. Pilih **Access Control** (Kontrol Akses) dan klik **Edit**.
4. Aktifkan **Playback Authentication** (Autentikasi Pemutaran Ulang), lalu klik **Save** (Simpan).

>!
>- Penerapan konfigurasi memerlukan waktu **30 menit**.
>- HTTP-FLV: setelah `txTime` URL tercapai, pemutaran ulang yang sedang berlangsung akan dilanjutkan, tetapi permintaan pemutaran ulang baru melalui URL tersebut akan ditolak.
>- HLS: karena HLS membagi streaming menjadi beberapa bagian pendek, HLS akan terus meminta file M3U8 untuk mendapatkan segmen TS terkini. Misalnya, jika Anda mengatur `txTime` ke waktu saat ini dan masa berlaku ke 10 menit, permintaan URL pemutaran ulang HLS yang dikirim 10 menit setelah waktu saat ini akan ditolak. Untuk mencegah hal ini, Anda dapat memperbarui URL permintaan HLS di server dari waktu ke waktu atau mengatur titik waktu kedaluwarsa yang lebih lama.

[](id:que7)
### Persyaratan format apa saja yang harus dipenuhi kunci utama untuk autentikasi pemutaran ulang? Apakah ada pembatasan masa berlaku?
Kunci utama hanya boleh berisi huruf dan angka, dengan maksimum 256 karakter. Informasi lebih lanjut dapat dilihat di [Playback Authentication Configuration (Konfigurasi Autentikasi Pemutaran Ulang)](https://intl.cloud.tencent.com/document/product/267/31060).
Sebaiknya atur masa berlaku sesuai dengan durasi sesi streaming langsung.


[](id:que8)
### Apakah saya dapat membuat URL push dengan masa berlaku yang lama? Berapa lama durasi maksimum masa berlaku?
Pengaturan masa berlaku URL push ditujukan untuk autentikasi dan perlindungan. URL push yang berlaku secara permanen tidak dapat mencegah push tidak sah dan dapat menimbulkan kerugian bisnis.
Masa berlaku alamat push tidak dibatasi sehingga dapat diatur sesuai dengan kebutuhan bisnis Anda. Anda juga dapat menyambungkan beberapa alamat untuk membuat satu URL push dengan masa berlaku yang lebih lama. Informasi selengkapnya tentang aturan penyambungan dapat dilihat di [How to Splice a Push URL (Cara Menyambungkan URL Push)](https://intl.cloud.tencent.com/document/product/267/38393).

>? Kami tidak merekomendasikan pengaturan masa berlaku dengan durasi sangat lama untuk URL push karena hal tersebut dapat menyebabkan terjadinya kesalahan dan pelaporan kegagalan autentikasi ketika URL digunakan.

[](id:que9)
### Apakah logo Tencent Cloud akan ditampilkan di gambar streaming langsung? 
Tidak. 

[](id:que10)
### Berapa lama latensi dalam streaming langsung? 
Dalam kondisi normal, pemutaran ulang streaming FLV yang di-push melalui protokol RTMP memiliki latensi sekitar 2–3 detik. Latensi yang lebih tinggi umumnya menunjukkan adanya masalah. Informasi selengkapnya seputar cara mengatasi masalah dapat dilihat di [High Latency (Latensi Tinggi)](https://intl.cloud.tencent.com/document/product/267/7971).

[](id:que11)
### Dapatkah saya memodifikasi bitrate maksimum selama streaming langsung?
 Tidak. Bitrate maksimum hanya dapat diatur sebelum Anda melakukan push streaming sesuai dengan kecepatan pengunggahan jaringan. Selain itu, pengaturan bitrate yang terlalu tinggi dapat menyebabkan frame menurun dan kemacetan. 

[](id:que12)
### Bagaimana cara menghapus ruang streaming langsung yang tidak lagi digunakan? 
Push dan pemutaran ulang langsung terikat dengan ID streaming sehingga Anda tidak perlu menghapus ruang. Jika Anda menggunakan layanan IM dan ingin menghapus ruang IM untuk mencegah jumlah ruang mencapai batas atas, silakan pelajari [Disbanding a Group (Membubarkan Grup)](https://intl.cloud.tencent.com/document/product/1047/34896).
Jika Anda menggunakan mode saluran, panggil API `DeleteLVBChannel` dan masukkan ID saluran streaming langsung untuk menghapusnya secara massal.

> ! Mode saluran adalah mode lama yang tidak lagi diperbarui atau dipertahankan.
 
[](id:que13)
 ### Bagaimana penggunaan API untuk mengaktifkan/menonaktifkan push? 
API ini digunakan untuk menonaktifkan streaming ketika deteksi pornografi dilakukan. Misalnya, jika suatu streaming langsung terdeteksi berisi konten pornografi atau terorisme, Anda dapat menghentikan atau menonaktifkan streaming ini setiap saat.


[](id:que14)
### Bagaimana cara mengembangkan fitur pemutaran ulang audio di latar belakang?
Fitur pemutaran ulang audio di latar belakang disediakan oleh perangkat. Anda dapat mengembangkan fitur ini berdasarkan logika bisnis aktual. Selama streaming langsung tidak terhenti, audio dapat diputar ulang di latar belakang.


[](id:que15)
### Apa yang harus saya lakukan jika pesan "incorrect certificate" (sertifikat salah) ditampilkan saat saya memodifikasi konfigurasi HTTPS? 
 Pastikan jenis sertifikat Anda saat ini adalah Nginx karena CSS menggunakan Nginx untuk enkripsi.

[](id:que16)
### Setelah autentikasi dinonaktifkan untuk URL pemutaran ulang tertentu, mengapa URL tersebut tidak dapat digunakan untuk pemutaran ulang? 
 URL pemutaran ulang yang didukung autentikasi akan menjadi tidak valid setelah autentikasi dinonaktifkan, bahkan meski waktu kedaluwarsa belum tercapai. 

[](id:que17)
### Berapa batas atas untuk jumlah total permintaan API?
CSS mengatur batas atas untuk jumlah total permintaan yang dikirim oleh semua `SecretId` dalam satu akun. Setelah batas tercapai, permintaan baru tidak akan ditanggapi.
Misalnya, batas atas sebanyak 200 permintaan per detik menunjukkan bahwa server Tencent Cloud dapat menerima maksimum 200 permintaan yang dikirimkan oleh semua `SecretId` dari akun Anda dalam 1 detik. Sebanyak 200 permintaan dapat dikirimkan oleh satu atau beberapa pelanggan, dan dapat digunakan untuk membuat kueri untuk satu streaming atau lebih. 

[](id:que18)
### Apa yang harus saya lakukan jika "RTMP close" (RTMP ditutup) ditampilkan selama push dan push gagal, tetapi log memberi tahu bahwa push berhasil? 
Mungkin URL push Anda saat ini mengalami masalah. Sebaiknya gunakan [TCToolkit App (Aplikasi TCToolkit)](https://intl.cloud.tencent.com/document/product/1071/38147) untuk mengetahui URL berfungsi dengan normal atau tidak. Informasi selengkapnya seputar cara mengatasi masalah dapat dilihat di [Troubleshooting Push Failure (Mengatasi Masalah Kegagalan Push)](https://intl.cloud.tencent.com/document/product/267/33383).

[](id:que19)
### Apa yang harus saya lakukan jika push streaming tidak dapat berjalan dengan normal setelah saya memodifikasi frame rate, push harus dimulai ulang beberapa kali, dan streaming sering terhenti? 
Mungkin frame rate saat ini terlalu tinggi. Frame rate di atas 15 fps sudah cukup untuk memastikan pemutaran ulang video dapat berjalan dengan lancar. Namun, sebaiknya Anda mengatur frame rate ke nilai yang lebih rendah.  

[](id:que20)
### Kapan sistem akan menghentikan streaming yang tidak menghasilkan data dalam jangka waktu lama? 
Sistem akan menghentikan streaming jika perkecualian terjadi di perangkat push.
Perkecualian tersebut dapat berupa aplikasi mengalami crash, telepon seluler mati, dan alasan eksternal lainnya yang menyebabkan tidak adanya data streaming yang dikumpulkan di backend selama 70 detik sehingga sistem kemudian menghentikan streaming.

[](id:que21)
### Bagaimana cara mengonfigurasikan kunci API di konsol baru?
Kunci API digunakan untuk autentikasi API lama, yang telah ditingkatkan ke v3.0 di situs web resmi. Anda dapat memperoleh `SecretId` dan `Secretkey` di halaman **[API Key Management](https://console.cloud.tencent.com/cam/capi)** (Manajemen Kunci API) untuk menggunakan API 3.0.

[](id:que21)
### Mengapa video H.265 tidak dapat diputar ulang?
Karena H.265 tidak memiliki kompatibilitas yang sama dengan H.264, jika pemutar tidak mendukung H.265 dan pemutaran ulang gagal dilakukan, Anda dapat mengonfigurasikan [templat transcoding](https://intl.cloud.tencent.com/document/product/267/31071) untuk melakukan transcoding pada video ke H.264 agar pemutaran ulang dapat dilakukan.

[](id:que22)
### Bolehkah nama file M3U8 berisi karakter Mandarin?
File M3U8 diberi nama secara otomatis berdasarkan nama streaming. Nama streaming **tidak mendukung** karakter Mandarin.

[](id:que23)
### Bagaimana cara melihat jumlah pemirsa online?
Anda dapat melihat jumlah pemirsa online dengan memanggil API [DescribeStreamPlayInfoList](https://intl.cloud.tencent.com/document/product/267/37297), tetapi hasilnya mungkin tidak 100% akurat. Misalnya, jika 3 pengguna menggunakan alamat IP yang sama untuk pemutaran ulang secara bersamaan, ketiganya akan dihitung sebagai 1 pemirsa. Harap perhatikan bahwa data yang ditampilkan oleh API ini hanya relevan jika Anda menggunakan protokol pemutaran ulang RTMP atau FLV, dan tidak relevan jika Anda menggunakan protokol pemutaran ulang HLS.

[](id:que24)
### Apakah CSS mendukung streaming cadangan?
Streaming cadangan diaktifkan secara default dengan CSS. Jika Anda melakukan push pada dua streaming dengan nama streaming yang sama secara bersamaan, selama pemutaran ulang, hanya streaming pertama yang akan ditampilkan. Streaming kedua baru akan ditampilkan jika streaming pertama terhenti.
