### Bagaimana cara mengonfigurasikan akselerasi push langsung di luar Tiongkok Daratan?
Buka konsol CSS > [Domain Management (Manajemen Domain)](https://console.cloud.tencent.com/live/domainmanage), tempat nama domain push default dikonfigurasikan sebelumnya dengan akselerasi push di luar Tiongkok Daratan. Jika Anda ingin menggunakan nama domain push sendiri, tambahkan nama domain push Anda, lalu selesaikan operasi terkait CNAME sesuai dengan petunjuk untuk mengonfigurasikan akselerasi di luar Tiongkok Daratan untuk nama domain tersebut.
		
### Bagaimana cara mengakselerasi push untuk nama domain pemutaran ulang di luar Tiongkok Daratan?
Buka konsol CSS > [Domain Management](https://console.cloud.tencent.com/live/domainmanage) > Add Playback Domain (Manajemen Domain > Tambahkan Domain Pemutaran Ulang) untuk memilih salah satu di antara dua jenis akselerasi sesuai dengan kebutuhan: **Global Acceleration** (Akselerasi Global), yang mengharuskan nama domain untuk telah mendapatkan izin ICP di Tiongkok Daratan; jika tidak, konfigurasi akan gagal; **Acceleration in Hong Kong/Macao/Taiwan (China Region) and other regions** (Akselerasi di Hong Kong/Makau/Taiwan (Wilayah Tiongkok) dan wilayah lain), yang dapat dikonfigurasikan sesuai dengan petunjuk, tetapi pemutaran ulang tidak tersedia di Tiongkok Daratan dalam kasus ini.
	 
### Bagaimana cara memeriksa apakah akselerasi di luar Tiongkok Daratan telah dikonfigurasikan atau belum untuk nama domain saya?
Anda dapat menggunakan server di luar Tiongkok Daratan untuk menjalankan perintah `ping` pada nama domain push dan pemutaran ulang; jika IP server merupakan IP node terdekat, akselerasi di luar Tiongkok Daratan telah dikonfigurasikan. Anda juga dapat menggunakan [alat ini](https://tools.ipip.net/dns.php) untuk menguji nama domain Anda dan memeriksa perubahan IP sudah sesuai dengan wilayah akselerasi atau belum.
	 
### Bagaimana cara mengatasi masalah kegagalan pemutaran ulang langsung di luar Tiongkok Daratan?
Saat ini, pemutaran ulang di luar Tiongkok Daratan mendukung HTTP-FLV, HLS, dan RTMP. Anda dapat mengatasi masalah pemutaran ulang dengan cara berikut:
1. **Apakah nama domain dapat di-ping?**
Jika tidak, periksa lingkungan jaringan saat ini.
2. **Apakah kode status HTTP yang diperoleh 200?**
	Jika kode status HTTP yang diperoleh bukan 200, ada beberapa kemungkinan penyebab kegagalan tersebut. Secara umum, jika kode statusnya 403, yang menunjukkan kegagalan autentikasi, Anda perlu memastikan bahwa format perhitungan perlindungan hotlink telah memenuhi persyaratan. Jika kode statusnya 404, yang menunjukkan bahwa streaming yang diputar ulang tidak tersedia di platform, Anda perlu memeriksa push dapat berjalan dengan normal atau tidak. Untuk kode kesalahan lainnya, [kirimkan tiket](https://console.cloud.tencent.com/workorder/category) untuk mendapatkan bantuan.
	 
### Protokol apa saja yang didukung push langsung di luar Tiongkok Daratan?
Saat ini, protokol yang didukung hanya RTMP.
	 
### Apakah pemutaran ulang langsung di luar Tiongkok Daratan mendukung HTTPS?
Ya. Buka konsol CSS > [Domain Management](https://console.cloud.tencent.com/live/domainmanage) > Playback Domain > Manage > Advanced Configuration > HTTPS Configuration (Manajemen Domain > Domain Pemutaran Ulang > Kelola > Konfigurasi Lanjutan > Konfigurasi HTTPS) untuk menambahkan sertifikat HTTPS ke nama domain tempat Anda ingin mengonfigurasikan penarikan HTTPS.
	 
### Apakah saya dapat memodifikasi wilayah akselerasi pemutaran ulang langsung di luar Tiongkok Daratan?
Ya. Anda dapat melakukannya melalui konsol CSS > Domain Management (Manajemen Domain). Penerapan perubahan memerlukan waktu sekitar 15 menit.
	 
### Apakah akselerasi push di luar Tiongkok Daratan mendukung penjadwalan HttpDNS?
Ya, tetapi Anda perlu [mengirimkan tiket](https://console.cloud.tencent.com/workorder/category) untuk konfigurasi di backend.
