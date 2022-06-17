### Apa yang harus saya lakukan jika pengguna tidak dapat menerima pesan SMS?
Login ke [konsol SMS](https://console.cloud.tencent.com/smsv2), lalu pilih **Business Statistics** > **Chinese Mainland SMS** (or **Global SMS**) > **Message Records** (Statistik Bisnis > SMS Tiongkok Daratan (atau SMS Global) > Catatan Pesan) untuk melihat **Sending Status** (Status Pengiriman) dan **Remarks** (Keterangan) untuk nomor ponsel.
- Jika **Sending Status** (Status Pengiriman) adalah "Failed" (Gagal), Anda dapat menyelesaikan masalah tersebut berdasarkan penyebabnya seperti yang dijelaskan dalam **Remarks** (Keterangan). Penyebabnya mungkin permintaan telah mencapai kebijakan kontrol batas tingkat pengiriman, format pesan SMS salah, atau nomor ponsel diblokir karena langganan dihentikan.
- Jika **Sending Status** (Status Pengiriman) adalah "Succeeded" (Berhasil), tetapi kode kesalahan ditampilkan di **Remarks** (Keterangan), selesaikan masalah berdasarkan [kode kesalahan] tertentu (https://intl.cloud.tencent.com/document/product/382/34861).
- Jika **Sending Status** (Status Pengiriman) adalah "Succeeded" (Berhasil) dan **Remarks** (Keterangan) menampilkan bahwa "The user has successfully received the message" (Pengguna telah berhasil menerima pesan), tetapi pengguna sebenarnya belum menerima pesan, Anda dapat menyelesaikan masalah dengan mengikuti langkah-langkah di bawah ini:
 - Ponsel mati atau nomor ponsel kehabisan pulsa atau berada di luar jangkauan: periksa status ponsel/nomor ponsel, misalnya dengan melakukan panggilan ke nomor tersebut.
 - Nomor ponsel diblokir: periksa kemungkinan pengguna telah melakukan komplain kepada operator atau berhenti berlangganan dari layanan.
 - Ponsel tidak dapat menerima pesan SMS karena sudah lama tidak dimatikan: coba mulai ulang ponsel.
 - Ponsel tidak dapat menerima pesan SMS karena penerimaan yang buruk: periksa penerimaan dan coba mulai ulang ponsel jika perlu.
 - Kotak masuk SMS ponsel penuh: coba hapus pesan tidak penting.
 - Ponsel tidak dapat menerima pesan SMS karena masalah pengaturan atau perangkat keras: coba ubah pengaturan atau keluarkan kartu SIM dan masukkan ke ponsel lain untuk mengujinya (jika ponsel memiliki slot kartu SIM ganda, coba keluarkan kartu SIM dan masukkan ke slot kartu lain untuk mengujinya).
 - Pesan telah diblokir oleh sistem/perangkat lunak di ponsel: periksa daftar blokir.

Jika masalah berlanjut, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).

### Apa yang harus saya lakukan jika diperlukan waktu lama untuk memanggil API?[](id:jump)
Jika merasa bahwa waktu yang diperlukan untuk memanggil API SMS Tencent Cloud lama, Anda dapat menyelesaikan masalah dengan langkah-langkah berikut:
1. Jalankan perintah `dig yun.tim.qq.com` untuk memeriksa digunakan atau tidaknya DNS privat, jika DNS privat digunakan, pilih IP SMS Tencent Cloud terdekat dari operator yang sama untuk mengonfigurasikan host, lalu periksa terselesaikan atau tidaknya masalah.
  - Jika masalah telah terselesaikan, penyebabnya mungkin karena resolusi DNS macet atau ada latensi yang disebabkan oleh akses lintas wilayah atau lintas operator. Anda sebaiknya menggunakan proksi DNS atau menyiapkan server DNS publik.
  - Jika masalah berlanjut, ikuti [langkah 2](#Q2step2).
2. Periksa mode koneksi mana yang digunakan dan digunakan atau tidaknya kumpulan koneksi.[](id:Q2step2)
 - Jika koneksi persisten tunggal digunakan, menurut model permintaan/respons HTTP, jika permintaan macet, permintaan berikutnya pada koneksi tersebut akan terpengaruh. Model "koneksi persisten + kumpulan koneksi" direkomendasikan.
 - Jika koneksi non-persisten digunakan, jalankan `netstat` untuk memeriksa jumlah koneksi lokal telah mencapai batas atas atau tidak. Jika batas atas sudah tercapai, model "koneksi persisten + kumpulan koneksi" direkomendasikan.
 - Jalankan `netstat` untuk memeriksa atau jalankan `tcpdump` untuk mengambil paket guna memeriksa ada atau tidaknya tumpukan Recv-Q dan Send-Q yang terhubung, dan jika ada, model "koneksi persisten + kumpulan koneksi" direkomendasikan.
 - Jika tidak ada permintaan yang dikirim melalui suatu koneksi untuk periode waktu yang lama (90 detik), untuk mencegah perangkat jaringan perantara mengambil alih kembali koneksi, pemohon disarankan untuk menutup koneksi dan membuat koneksi lagi saat memulai permintaan baru dan saat tidak ada cukup koneksi di kumpulan koneksi.

### Mengapa diperlukan waktu lama bagi pengguna untuk menerima pesan SMS?

1. Lihat waktu terkirim permintaan yang dicatat di sistem lokal dan waktu terkirim pesan SMS yang dicatat di konsol, lalu hitung selisihnya.
 - Jika selisihnya besar (misalnya kira-kira atau bahkan lebih dari 10 menit), penyebabnya mungkin karena ada penundaan pada panggilan API. Silakan selesaikan masalah dengan merujuk ke [Hal yang harus dilakukan jika diperlukan waktu lama untuk memanggil API?](#jump).
 - Jika selisihnya kecil, silakan ikuti [langkah 2](#Q3step2).
2. Periksa **Sending Time** (Waktu Pengiriman) dan **Status Report Time** (Waktu Laporan Status) untuk pesan SMS dan hitung selisihnya.[](id:Q3step2)
 - Jika selisihnya besar (misalnya lebih dari 10 detik untuk SMS biasa atau lebih dari 5 menit untuk SMS pemasaran), penyebabnya mungkin pesan SMS sedang ditinjau karena mengandung kata-kata sensitif, penerimaan ponsel buruk, atau nomor ponsel dalam kondisi tidak biasa (misalnya pulsa habis atau tidak ada layanan).
 - Jika selisihnya kecil, penyebabnya mungkin karena penerimaan ponsel yang buruk atau ponsel dalam kondisi tidak biasa (misalnya dimatikan).
3. Jika masalah berlanjut, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).

### Apa itu daftar blokir nomor ponsel?

Saat ini, terdapat daftar blokir dengan jenis-jenis sebagai berikut:
- Daftar pengguna yang berhenti berlangganan. Setelah pengguna membalas "T", "N", "TD", "Unsubscribe", "QX", atau "0000" (tidak peka huruf besar/kecil) untuk berhenti berlangganan, sistem akan menempatkan nomor ponsel pengguna di daftar blokir setelah menerima balasan. Ketika pesan SMS dikirim lagi, pesan "Failed to send" (Gagal mengirim) akan ditampilkan, dengan keterangan "1015 The mobile number is blocked" (1015 Nomor ponsel diblokir), dan pengguna tidak dapat menerima pesan SMS tersebut.
 Anda dapat login ke [konsol SMS](https://console.cloud.tencent.com/smsv2), lalu pilih **General Management** > **Unsubscribed Users** (Manajemen Umum > Pengguna yang Berhenti Berlangganan), dan ajukan permohonan pembatalan berhenti berlangganan, yang akan berlaku setelah disetujui.
- Daftar blokir operator. Jenis pengguna ini diblokir oleh operator karena berbagai alasan. Ketika pesan SMS dikirim, pesan "Sent successfully" (Berhasil terkirim) akan ditampilkan, tetapi pesan SMS tersebut mungkin tidak diterima oleh pengguna karena diblokir oleh gateway operator atau karena alasan lain.

### Apa yang harus saya lakukan jika kesalahan 1004 ditampilkan?
Saat Anda memanggil API SMS Tencent Cloud untuk mengirim pesan SMS, jika paket respons menampilkan kesalahan 1004, Anda dapat menyelesaikan masalah dengan langkah-langkah berikut:
1. Periksa permintaan yang dikirim menggunakan format JSON standar atau tidak. Kami menyarankan Anda mencari pemeriksa format JSON di internet untuk mengidentifikasi masalah. Misalnya, tanda kutip ganda harus digunakan untuk format JSON standar, tetapi tanda kutip tunggal, alih-alih tanda kutip ganda, digunakan secara tidak sengaja.
2. Periksa kesesuaian nama parameter.
3. Periksa kesesuaian jenis bidang permintaan dengan yang dijelaskan dalam [dokumentasi API](https://intl.cloud.tencent.com/document/product/382/34689). Sebagai contoh, string JSON dan bilangan bulat JSON digunakan secara salah (misalnya `{"Name":"Tom", "Age":23}`, yang seharusnya "Name" (Nama) harus berupa string JSON, dan "Age" (Usia) harus berupa bilangan bulat JSON).
4. Periksa nilai bidang permintaan ada dalam rentang nilai seperti yang dijelaskan dalam dokumentasi API atau tidak. Misalnya, bidang `international` (internasional) hanya dapat diisi dengan nilai 0 atau 1.
5. Periksa panggilan API dimulai seperti yang dijelaskan dalam dokumentasi API atau tidak. Misalnya, saat Anda memanggil API untuk mengirim pesan massal, Anda tidak boleh menggunakan isi untuk mengirim pesan ke satu penerima.
6. Jika masalah berlanjut, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).

### Apa yang harus saya lakukan jika kesalahan 1014 ditampilkan?
Saat Anda memanggil API SMS Tencent Cloud untuk mengirim pesan SMS, jika paket respons menampilkan kesalahan 1014, Anda dapat menyelesaikan masalah dengan langkah-langkah sebagai berikut:
1. Periksa kesesuaian format templat konten yang diajukan. Misalnya, "{}" dalam templat konten harus dalam tanda kurung bahasa Inggris, dan angka dalam tanda kurung harus dimulai dari 1, yaitu {1}, {2}, dan seterusnya.
2. Periksa templat berisi nilai variabel atau tidak. Jika templat berisi nilai variabel, Anda harus memasukkan variabel saat mengirim pesan. Jika beberapa nilai variabel diatur dalam templat, Anda juga harus memasukkan beberapa variabel saat mengirim pesan.
3. Periksa telah disetujui atau belumnya templat terkait.
4. Periksa sama atau tidaknya nilai parameter `type` (jenis) dalam paket permintaan dengan jenis templat konten yang diajukan (0 menunjukkan SMS biasa, sedangkan 1 menunjukkan SMS pemasaran).
5. Periksa digunakan atau tidaknya format yang sama dalam konten permintaan dan templat konten yang diajukan. Misalnya, **ketidakcocokan dapat terjadi karena karakter yang tidak terlihat, seperti spasi.**
6. Jika konten berisi karakter bahasa Mandarin, pastikan karakter tersebut perlu dikodekan dalam UTF-8.
7. Templat SMS Tiongkok Daratan hanya dapat digunakan untuk mengirim pesan ke nomor ponsel di Tiongkok Daratan, sedangkan templat SMS Global hanya dapat digunakan untuk mengirim pesan ke nomor ponsel di luar Tiongkok Daratan.
8. Jika masalah berlanjut, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).

### Apa yang harus saya lakukan jika kesalahan 1016 ditampilkan?
Saat Anda memanggil API SMS Tencent Cloud untuk mengirim pesan SMS, jika paket respons menampilkan kesalahan 1016, Anda dapat menyelesaikan masalah dengan langkah-langkah berikut:
1. Periksa kesesuaian `AppID` dan `AppKey`.
2. Periksa kesesuaian format nomor ponsel. **Nomor ponsel yang benar tidak boleh berisi spasi.**
3. Periksa kesesuaian nama bidang.


### Apa yang harus saya lakukan jika kesalahan 60008 ditampilkan?
Saat Anda memanggil API SMS Tencent Cloud untuk mengirim pesan SMS, jika paket respons menampilkan kesalahan 60008, Anda dapat menyelesaikan masalah dengan langkah-langkah berikut:
1. Jika kode kesalahan 60008 ditampilkan dalam satu detik sebagai respons atas permintaan tersebut, harap periksa penggunaan format HTTP standar dalam permintaan tersebut.
2. Periksa kesesuaian format URL dan isi permintaan dengan API tersebut.
3. Periksa sama atau tidaknya `Content-Type` permintaan dengan `Content-Type` isi (`Content-Type: application/json;charset=utf-8` untuk SMS).
4. Periksa konfigurasi DNS untuk memastikan bahwa server DNS publik digunakan.
5. Koneksi persisten HTTP dan kumpulan koneksi direkomendasikan untuk meningkatkan kualitas jaringan.
6. Jika masalah berlanjut, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).

### Apa yang harus saya lakukan jika kesalahan 1001 (verifikasi sig gagal) ditampilkan?
Saat Anda memanggil API SMS Tencent Cloud untuk mengirim pesan SMS, jika paket respons menampilkan kesalahan 1001, Anda dapat menyelesaikan masalah dengan langkah-langkah berikut:
1. Periksa sama atau tidaknya nomor acak yang dihasilkan oleh `sig` dengan nomor acak yang ada di URL.
2. Periksa kesesuaian `SDK AppID` (dimulai dengan 1400) dan `AppKey` dalam kode.
3. Periksa sama atau tidaknya kode yang digunakan dengan kode sampel dan konsistensi kode semu `sig` yang dihasilkan dari parameter.

### Bagaimana cara mendapatkan SecretId dan SecretKey API SMS?
1. Login ke konsol Tencent Cloud.
2. Buka halaman konsol [Kelola Kunci API](https://console.cloud.tencent.com/cam/capi).
3. Di halaman **Manage API Key** (Kelola Kunci API), klik **Create Key** (Buat Kunci) untuk membuat pasangan kunci.

**SecretId**: mengidentifikasi pengguna yang memanggil API, yang mirip dengan nama pengguna.
**SecretKey**: mengautentikasi pengguna yang memanggil API, yang mirip dengan kata sandi.

>?
>- Anda harus menjaga kerahasiaan kredensial keamanan Anda dan tidak mengungkapkannya; jika tidak, aset Anda dapat disusupi. Jika kredensial keamanan Anda diketahui orang lain, silakan nonaktifkan sesegera mungkin.
>- `SecretId` SMS sama dengan `AccessKey ID` SMS.


### Bagaimana cara mendapatkan SDK AppID dan AppKey SMS?
`SDK AppID` dan `AppKey` adalah akun dan kunci akses aplikasi yang diberikan oleh Tencent Cloud saat Anda mengajukan aplikasi baru. Anda dapat melihatnya setelah berhasil membuat aplikasi.
- **SDK AppID**: ID unik aplikasi SMS Tencent Cloud seperti yang ditunjukkan di bawah ini:
![](https://qcloudimg.tencent-cloud.cn/raw/9f7f80e6a447fc4d50104e35fa47fe51.png)
- **AppKey**: kata sandi yang digunakan untuk memverifikasi validitas permintaan pengiriman SMS, yang dapat memastikan reliabilitas sumber aplikasi dalam kondisi teknis tertentu.



### Mengapa saya tidak dapat diarahkan ke halaman yang ditentukan setelah mengeklik URL pendek di Program Mini WeChat?
Silakan masukkan jalur halaman program mini yang diakses melalui kode skema di bidang `path` (jalur) di halaman **Short URL Management** (Manajemen URL Pendek). Jalur tersebut harus merupakan halaman yang ada di program mini yang dirilis, dan Anda akan diarahkan ke beranda program mini jika jalur kosong. Anda dapat menemukan jalur di **WeChat Mini Program** > ** Statistics** > **Usage Analysis** > **Page Analysis** (Program Mini WeChat > Statistik > Analisis Penggunaan > Analisis Halaman).

### Apakah penerima dapat membalas pesan SMS Tencent Cloud? Apakah ada batas waktu untuk melakukannya?
Penerima harus membalas dalam waktu 72 jam, dan balasan dapat dilihat.

### Apakah saya dapat melihat atau menerima balasan pengguna?
Ya, dan tidak ada biaya tambahan yang akan dikenakan untuk balasan SMS. Balasan dapat dilihat di bagian [Catatan Balasan](https://console.cloud.tencent.com/smsv2/statistics-csms/record) di konsol atau diperoleh dengan mengatur alamat callback.

### Berapa nomor yang digunakan untuk mengirim pesan SMS setelah saya mengaktifkan SMS Tencent Cloud?
- Untuk SMS Tiongkok Daratan: nomor berisi 13–20 digit yang dimulai dengan 1069 dan diakhiri dengan nomor acak yang ditetapkan oleh operator.
- Untuk SMS Global: tidak ada nomor, dan hanya Qsms atau Qcloud yang akan ditampilkan.

### Apakah saya dapat mengirim pesan SMS yang berbeda ke nomor ponsel yang berbeda secara bersamaan?
Anda dapat mengirim pesan SMS yang berbeda ke nomor ponsel yang berbeda dengan memanggil API untuk mengirim pesan kepada satu penerima dalam beberapa proses.

### Apa yang harus saya lakukan jika saya tidak dapat menyelesaikan masalah yang terjadi saat mengirim pesan SMS?
Anda dapat [mengirim tiket](https://console.cloud.tencent.com/workorder/category) untuk meminta bantuan.

### Permohonan telah disetujui, tetapi pesan SMS gagal terkirim, dan catatan menunjukkan bahwa pesan berisi kata-kata sensitif. Apa sebabnya?
Kosakata untuk kata-kata sensitif disediakan oleh operator. Anda dapat [mengirim tiket](https://console.cloud.tencent.com/workorder/category) dan mencantumkan nomor ponsel tujuan pesan gagal dikirim. Agen layanan pelanggan akan menghubungi operator untuk mengatasi masalah tersebut.

### Apakah setiap pesan SMS akan ditinjau setelah tanda tangan dan isi SMS disetujui?
Pengguna individu harus mendapatkan persetujuan terlebih dahulu sebelum menggunakan konsol untuk mengirim pesan SMS dan disarankan untuk memverifikasi identitas organisasi.


### Saya mengirim pesan SMS ke nomor ponsel tertentu, tetapi pesan tidak diterima, dan nomor ponsel tersebut tidak dapat ditemukan di konsol. Apa yang harus saya lakukan?
- Jika pesan dikirim melalui konsol, Anda sebaiknya memeriksa kemungkinan adanya karakter tambahan di nomor ponsel dalam file yang dikirim, dan jika ada, silakan hapus.
- Jika pesan dikirim melalui API, Anda sebaiknya memeriksa permintaan telah dikirim dengan benar atau tidak ke Tencent Cloud dan ada atau tidaknya respons yang ditampilkan.


### Apakah saya dapat menggunakan server di luar Tiongkok Daratan untuk mengirim pesan SMS?
Server di luar Tiongkok Daratan dapat digunakan untuk memanggil API untuk mengirim pesan SMS, dan nama domain dapat diselesaikan di dekatnya. Anda dapat menggunakan API `curl` untuk mengujinya terlebih dahulu.

### Apakah saya dapat mengirim SMS massal?
Ya, Anda dapat mengirim pesan SMS ke hingga 200 nomor ponsel sekaligus dengan memanggil [API SendSms](https://intl.cloud.tencent.com/document/product/382/34859) atau ke hingga 100.000 nomor ponsel melalui konsol.

### Apakah deduplikasi nomor didukung?
Saat Anda mengimpor nomor ke konsol, platform akan menghapus duplikasi batch nomor dengan atribut yang sama secara otomatis.
Dalam satu permintaan pengiriman SMS, platform akan memeriksa adanya duplikasi nomor penerima untuk konten pesan yang sama dan hanya mengirimkan pesan satu kali ke nomor yang diduplikasi.

### Apakah faktur tersedia?
Jika memerlukan faktur, Anda dapat mengajukan permohonan di halaman **Invoice** (Faktur) di [konsol Pusat Penagihan](https://console.intl.cloud.tencent.com/expense/invoicing).

### Mengapa nomor berisi tanda bintang saat saya melihat pratinjau pesan SMS? Misalnya, `Pelanggan yang terhormat, pembayaran top-up Anda sebesar 1**2 USD telah dipotong dari akun Anda. Silakan periksa di sistem!`.
Konsol akan mengenkripsi nomor yang disimpan sehingga nomor akan berisi tanda bintang saat dilihat dalam pratinjau, tetapi pesan SMS yang diterima oleh pengguna akan ditampilkan sepenuhnya.

### Apa yang dimaksud dengan kode negara/wilayah?
Untuk informasi lebih lanjut tentang kode negara/wilayah, lihat [Pricing (Penetapan Harga)](https://intl.cloud.tencent.com/document/product/382/8414).

### Apa itu wilayah?
Wilayah adalah area geografis tempat pusat data fisik berada. Saat ini, SMS Internasional Tencent Cloud mendukung dua wilayah: Singapura dan Frankfurt (Eropa). Wilayah sepenuhnya terisolasi satu sama lain, yang berarti data hanya disimpan di wilayah lokal dan tidak dapat disimpan di wilayah lain. Kami menyarankan Anda untuk memilih wilayah sesuai dengan persyaratan penyimpanan data di berbagai wilayah. Fitur dan harga layanan SMS di setiap wilayah sama, tetapi datanya tidak saling terhubung. Hanya tanda tangan dan templat yang disetujui yang dapat disalin di seluruh wilayah.

### Bagaimana cara memilih wilayah yang sesuai?
Fitur dan harga layanan SMS di setiap wilayah sama, tetapi wilayah sepenuhnya terisolasi satu sama lain, yang berarti data hanya disimpan di wilayah lokal dan tidak dapat disimpan di wilayah lain. Anda sebaiknya memilih wilayah sesuai dengan persyaratan penyimpanan data di berbagai wilayah. Misalnya, pilih Frankfurt (Eropa) jika pengguna Anda berada di UE. Anda dapat mengganti wilayah di bilah judul di konsol SMS atau menentukan bidang `region` (wilayah) melalui API. Untuk informasi lebih lanjut, lihat [Daftar Wilayah](https://intl.cloud.tencent.com/document/api/382/40466?lang=en#region-list).
