[](id:que1) 
### Dapatkah SES mengakses email yang saya kirim dan terima? 

SES menggunakan teknologi anti-spam internal untuk memfilter email yang berisi konten buruk. Selain itu, SES memindai semua email yang berisi lampiran untuk memeriksa virus dan konten berbahaya lainnya. SES tidak akan menyimpan konten email Anda.

[](id:que2) 
### Dapatkah email saya dienkripsi?
Selama transfer email, SES akan mengenkripsi konten email Anda.

[](id:que3) 
### Apakah SES menggunakan Transport Layer Security (TLS) untuk mengirim email melalui koneksi terenkripsi?
SES mendukung TLS 1.2, TLS 1.1, dan TLS 1.0 untuk koneksi TLS.

Secara default, SES menggunakan TLS. Artinya, SES akan selalu mencoba membuat koneksi aman dengan server email penerima. Jika tidak dapat membuat koneksi yang aman, SES akan mengirim email dengan cara yang tidak terenkripsi. Anda dapat mengubah opsi ini sehingga SES hanya akan mengirim email ketika koneksi aman dapat dibuat.

[](id:que4) 
### Bagaimana SES memastikan bahwa email yang masuk bukan spam dan bebas virus?
SES mengadopsi banyak langkah perlindungan spam dan virus. Tencent Cloud secara khusus mengelola pustaka alamat email yang diblokir dan memblokir email dari alamat tersebut untuk membantu Anda memfilter email berbahaya. SES memindai setiap email masuk yang berisi lampiran virus. Tindakan ini memberi Anda berbagai metode deteksi spam; misalnya selain hasil pemindaian spam dan virus, SES memberikan hasil pemeriksaan DKIM dan SPF.

[](id:que5) 
### Teknologi apa yang dapat mencegah pengguna SES mengirim spam? 

SES menggunakan teknologi penyaringan konten internal untuk mendeteksi spam. Selain itu, SES juga menyediakan alat penilaian kualitas email untuk membantu Anda memeriksa konten email sendiri. Jika ditemukan bahwa akun mengirim spam atau konten berbahaya, akun tersebut akan menangguhkan kemampuan untuk mengirim email lain.
>! Tidak menjadi spam bukan berarti email tidak akan masuk ke folder spam. Skor kualitas email hanya untuk referensi. Faktor termasuk konten email, reputasi domain, tingkat terbuka, dan keluhan pengguna memengaruhi apakah email masuk ke folder spam. Penyedia layanan email yang berbeda memiliki kebijakan folder spam yang berbeda, yang tidak dapat kami kontrol. Namun, SES dapat menjamin kualitas IP pengirim.

