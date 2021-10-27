### Server asal
Server ini merujuk ke server bisnis Anda yang berjalan stabil.Di Konsol CDN, Anda dapat memilih server eksternal atau COS sebagai server asal.

### Asal eksternal
Ini merujuk ke server untuk men-deploy layanan web Anda sendiri.Ketika melakukan koneksi ke nama domain akselerasi, Anda dapat memasukkan alamat IP publik milik server sebagai server asal.

### Asal COS
Jika sumber daya sudah tersimpan di COS, bucket dapat dipilih sebagai server asal.

### Server edge
Ini merujuk ke simpul jaringan yang digunakan CDN untuk meng-cache konten dari server asal agar dapat menanggapi permintaan pengguna dari berbagai wilayah dengan cepat.

### Rekaman CNAME
Rekaman CNAME (Nama Kanonik) merujuk pada rekaman alias di dalam resolusi nama domain.
Misalnya, sebuah server bernama `host.example.com` memberikan layanan WWW dan MAIL sekaligus.Untuk lebih memudahkan pengguna dalam mengakses layanan tersebut, dua rekaman CNAME (`www.example.com` dan `mail.example.com`) dapat ditambahkan untuk server ini di penyedia layanan DNS-nya sehingga semua permintaan untuk mengakses dua rekaman CNAME ini akan diteruskan ke `host.example.com`.

### Nama domain CNAME
Ini merujuk ke nama domain yang berakhiran `.cdn.dnsv1.com` yang ditetapkan oleh sistem ke nama domain akselerasi terkoneksi yang dikonfigurasi di Konsol CDN.Anda harus mengonfigurasi rekaman CNAME di penyedia layanan nama domain Anda.Setelah rekaman tersebut aktif, CDN akan mengelola resolusi nama domain dan semua permintaan yang dikirim ke nama domain ini akan diteruskan ke penyedia edge CDN.

### Konten statis
Ini merujuk ke konten yang tetap sama dalam menanggapi beberapa permintaan untuk sumber daya yang sama.
Contoh-contohnya meliputi html, css, dan berupa file, gambar, video, paket penginstalan perangkat lunak, file APK, dan file kompresi.

### Konten dinamis
Ini merujuk ke konten yang berubah-ubah dalam menanggapi beberapa permintaan untuk sumber daya yang sama.
Contoh-contohnya meliputi API dan file .jsp, .asp, .php, .perl, dan .cgi.

### Tarik-asal
Di CDN, arti tarik-asal adalah bahwa ketika seorang pengguna mengirim permintaan dari peramban, server yang menanggapi permintaan tersebut adalah server dari situs web sumber, bukan server cache di simpul CDN.Secara umum, jika konten tidak di-cache di server cache atau diubah di server asal, konten tersebut akan ditarik dari server asal.

### Domain asal
Ini merujuk ke nama domain situs yang diakses di server asal oleh simpul CDN selama tarik-asal.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Server Asal](https://intl.cloud.tencent.com/document/product/228/6289).

### Nama domain
Ini merujuk ke sederet alamat server yang dapat diingat dan digunakan dengan mudah oleh pengguna yang bisa berupa situs web, email, FTP, dll. Nama domain ini digunakan untuk mengidentifikasi lokasi elektronik komputer (kadang-kadang disebut lokasi geografi) selama transfer data.
