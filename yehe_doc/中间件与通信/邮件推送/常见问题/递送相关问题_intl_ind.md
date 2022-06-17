[](id:que1) 
### Bagaimana SES memastikan transmisi email yang andal?
Setelah Anda membuat templat email, kami akan meninjau konten templat untuk memastikan apakah telah memenuhi persyaratan ISP. Untuk lebih meningkatkan tingkat pengiriman email Anda, SES menyediakan mekanisme umpan balik yang mencakup pantulan email, keluhan, dan pemberitahuan pengiriman.

[](id:que2) 
### Dapatkah SES memastikan pengiriman email saya berhasil?
Baik itu SES atau layanan email lainnya, tidak dapat menjamin 100% keberhasilan pengiriman setiap email, ini karena dipengaruhi oleh berbagai faktor, seperti konten email, reputasi nama domain, tingkat terbuka, dan keluhan pengguna. Untuk informasi selengkapnya, lihat [Bagaimana cara mencegah email saya ditandai sebagai spam?](https://intl.cloud.tencent.com/document/product/1084/42369).


[](id:que3) 
### Berapa lama email yang dikirim melalui SES akan terkirim ke kotak masuk penerima?
Umumnya, email akan terkirim ke kotak masuk penerima dalam waktu 3 detik hingga 5 menit, maksimal 72 jam. Beberapa email mungkin tertunda karena faktor seperti konten email dan kebijakan penyedia layanan email. Oleh karena itu, sudah sewajarnya email akan terkirim dalam waktu lebih dari 5 menit.

[](id:que4) 
### Apakah pantulan atau keluhan email yang disebabkan oleh pengguna SES lain akan memengaruhi tingkat pengiriman email saya?
Biasanya, jika Anda menggunakan IP bersama, pantulan atau keluhan email yang disebabkan oleh pengguna SES lain mungkin berdampak pada tingkat pengiriman email Anda. Jika Anda menggunakan IP khusus, tidak akan ada pengaruhnya.

[](id:que5) 
### Apa yang harus saya lakukan jika gambar dalam email tidak ditampilkan?
Anda dapat memecahkan masalah seperti di bawah ini:

1. Periksa apakah URL gambar sudah benar.
2. Periksa apakah klien email Anda melarang pemuatan gambar. Jika ya, klik tombol **Show Image** (Tampilkan Gambar).
3. Periksa apakah gambar diblokir oleh penerima.

[](id:que6) 
### Apa yang harus saya lakukan jika email saya yang dikirim melalui SES diblokir oleh layanan email perusahaan?
Biasanya, layanan email perusahaan memblokir email iklan, jadi jangan sertakan konten iklan dalam subjek dan konten email Anda kecuali diperlukan.

[](id:que7) 
### Mengapa email saya gagal terkirim?
Periksa dokumen kode kesalahan terlebih dahulu untuk menentukan jenis kesalahan.

Kemudian, pecahkan masalah dalam urutan berikut:
1. Apakah akun memiliki izin `QcloudFullAccess` dan apakah `SecretId` dan `SecretKey` sudah benar.
2. Apakah domain pengirim diverifikasi. (Jangan ubah DNS yang dikonfigurasi setelah lulus verifikasi.)
3. Apakah alamat email penerima sudah benar.
4. Apakah templat disetujui dan apakah format `TemplateData` sudah benar.
5. "Anda hanya dapat mengirim email menggunakan templat" menunjukkan bahwa Anda tidak dapat mengirim email secara langsung. Kirim email Anda menggunakan templat.

Jika masalah masih berlanjut, hubungi [tim teknis Tencent Cloud](https://console.cloud.tencent.com/workorder/category) untuk mendapatkan dukungan.

[](id:que8) 
### Bagaimana cara melakukan berhenti berlangganan?
Saat pengguna akhir berhenti berlangganan dari email yang dikirim oleh pelanggan, Tencent Cloud akan memberi tahu pelanggan tentang peristiwa berhenti berlangganan dan mencatat status berhenti berlangganan pengguna akhir. Selain itu, domain pengirim yang sesuai tidak akan dapat lagi mengirim email ke pengguna akhir ini.

[](id:que9) 
### Mengapa beberapa email diblokir?
Tencent Cloud mengelola database alamat yang diblokir dan memblokir pengiriman email ke alamat yang diblokir ini. Ini membantu pelanggan menyaring permintaan email berbahaya. Selain itu, untuk melindungi reputasi pengirim pelanggan, Tencent Cloud menambahkan alamat penerima yang baru-baru ini ditolak ke database daftar blokir. Database daftar blokir dibagikan ke semua akun, sehingga daftar blokir alamat yang dibuat di akun berbeda ditambahkan ke database yang sama. Alamat email di database daftar blokir akan diblokir selama 14 hari. Anda dapat login ke [konsol SES](https://console.cloud.tencent.com/ses/stats) atau memanggil API untuk membuka pemblokirannya. Jika alamat penerima valid dan tidak ada dalam daftar blokir Anda, alamat tersebut mungkin diblokir oleh akun lain. Dalam hal ini, Anda dapat menghubungi [tim teknis Tencent Cloud](https://console.cloud.tencent.com/workorder/category) untuk membatalkan pemblokirannya.


[](id:use)
### Tingkat terbuka pengguna
Tingkat terbuka pengguna juga merupakan metrik penting apakah email akan terkirim ke kotak masuk. Semakin tinggi tingkat keterlibatan pengguna, semakin besar kemungkinan ISP akan meningkatkan kredibilitas nama domain yang sesuai. Secara umum, sudah sewajarnya jika tingkat pembukaan email terdaftar di atas 80%. Untuk email pemberitahuan, metrik ini bergantung pada skenario bisnis. Untuk email pemasaran, Anda harus terus mengoptimalkan subjek email dan konten untuk melibatkan pengguna. Jika metrik ini di bawah 50%, email yang dikirim kemungkinan akan masuk ke kotak spam.


