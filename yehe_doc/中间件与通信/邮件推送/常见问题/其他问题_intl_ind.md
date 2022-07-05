[](id:que1) 
### Apakah SES mendukung pengiriman email ke alamat email di luar daratan Tiongkok?
Ya. Tencent Cloud SES tersedia di lebih dari 200 negara/wilayah, sehingga membantu Anda mengirimkan email secara instan ke alamat email di seluruh dunia. Layanan ini dilengkapi pengiriman 97% (kecuali untuk alamat email yang tidak valid dan kotak surat perusahaan terbatas) dan mendukung penyedia layanan email utama seperti Gmail, Yahoo, Hotmail, 163.com, dan QQmail. Secara umum, SES memiliki stabilitas layanan dan pengiriman email yang tinggi.


[](id:que2) 
### Dokumentasi API menyatakan bahwa `Region` hanya mendukung Hong Kong (Tiongkok). Bisakah saya mengirim email ke wilayah lain?
**Ya.** `Region` hanya menunjukkan lokasi server dan tidak memengaruhi wilayah tujuan pengiriman email.

[](id:que3) 
### Apakah SES mendukung pengiriman email ke beberapa penerima sekaligus tanpa mereka saling bertemu?
Tidak.

[](id:que4) 
### Apakah ada batasan versi untuk SES?
Versi umum dapat memenuhi kebutuhan pengguna. Namun, jika versi lingkungan Anda terlalu usang, Anda perlu meningkatkan versi SDK seperti yang diinstruksikan.

[](id:que5) 
### Bagaimana cara membuat kueri untuk catatan pengiriman email?
Anda dapat membuat kueri untuk catatan pengiriman email melalui panggilan API. Untuk informasi selengkapnya, lihat [GetSendEmailStatus](https://intl.cloud.tencent.com/document/product/1084/39502).
 
 [](id:que6) 
### Metode pengiriman apa yang didukung SES?
SES mendukung tiga metode pengiriman, yaitu pengiriman melalui konsol, API, dan SMTP.


[](id:que7) 
### Kenapa email saya terkirim di kotak masuk tapi tingkat terbukanya 0?
- Untuk email HTML, Tencent Cloud dapat merekam peristiwa terbuka dan menghitung tingkat terbukanya.
- Untuk email teks biasa, Tencent Cloud tidak dapat menghitung tingkat terbukanya.
