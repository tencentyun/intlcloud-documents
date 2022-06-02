[](id:que1) 
### Dapatkah saya mengirim email dari alamat email mana pun?
**Tidak**, Anda dapat menggunakan SES untuk mengirim email hanya dari alamat atau domain yang Anda miliki.

Pertama, Anda harus memverifikasi domain untuk membuktikan bahwa Anda pemiliknya. Setiap akun Tencent Cloud dapat memiliki hingga 10 domain. Untuk informasi selengkapnya tentang memverifikasi alamat email dan domain, lihat **Langkah 4. Konfigurasikan Domain Pengirim** di [Memulai](https://intl.cloud.tencent.com/document/product/1084/39332).

[](id:que2) 
### Apakah ada batasan ukuran email yang dikirim melalui SES?
Ya, email (termasuk gambar dan lampiran) tidak boleh melebihi 4 MB.

[](id:que3) 
### Apakah ada batasan jumlah email yang dapat saya kirim?
Setiap akun SES memiliki serangkaian batas pengiriman, termasuk:

- Pengiriman harian maksimum: jumlah email maksimum yang dapat Anda kirim dalam waktu 24 jam. Secara default, batas ini adalah 300.000 email per hari per akun. Namun, Anda dapat meningkatkan batas ini.
- Tingkat pengiriman maksimum: jumlah maksimum email yang dapat Anda kirim per detik. Secara default, batas ini adalah 20 email per detik per akun.
- Batas maksimum pengiriman ke alamat email yang sama per jam: 10 (default). Jika batas ini terlampaui, email tambahan ke alamat ini akan diblokir. Anda dapat mengirim ulang setelah 1 jam. Mekanisme ini untuk menghindari pengecualian bisnis dan push.

>! 
>- Ketiga batasan di atas dapat disesuaikan. Hubungi dukungan teknis Tencent Cloud dan berikan skenario pengiriman dan alasan jika Anda perlu mengajukan penyesuaian.
>- Jika kami menemukan masalah dengan kualitas email Anda, seperti tingkat keluhan atau tingkat pantulan yang tinggi, kami berhak menghentikan Anda mengirim email melalui SES.

[](id:que4) 
### Apakah ada batasan pada format subjek email?
Subjek email harus dalam format UTF-8 dan berisi tidak lebih dari 998 karakter. Jika tidak, email tidak akan dikirim. Tencent Cloud merekomendasikan Anda untuk mempertahankan subjek dalam kisaran 78 karakter.

[](id:que5) 
### Apakah ada batasan pada alamat email penerima saat mengirim email melalui panggilan API?
Tidak. Namun, alamat email penerima harus valid (tidak diperoleh dengan di-crawl atau dibeli dari pihak ketiga) dan pemicu aktif atau langganan dari penerima diperlukan.

[](id:que6) 
### Apa yang harus saya lakukan agar dapat mengirim konten kustom?
Anda hanya dapat mengirim email menggunakan templat.
