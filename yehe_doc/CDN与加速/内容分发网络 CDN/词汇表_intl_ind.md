## B

### Server Edge

- Di Tencent Cloud Content Delivery Network (CDN), server edge berupa simpul jaringan yang digunakan CDN untuk meng-cache konten di server asal Anda agar dapat menanggapi permintaan pengguna dari berbagai wilayah dengan cepat.
- Di Tencent Cloud Global Content Delivery (GCD), server edge berupa simpul jaringan yang digunakan GCD untuk meng-cache konten di server asal Anda agar dapat menanggapi permintaan pengguna dari berbagai wilayah dengan cepat.
- Di Tencent Cloud Edge Computing Machine (ECM), server edge berupa IDC yang dibangun di dekat lokasi fisik pengguna dan menyediakan sumber daya fisik dasar untuk komputasi edge.

## C

### Rekaman CNAME

Rekaman CNAME (Nama Kanonik) merujuk pada rekaman alias di dalam resolusi nama domain.
Misalnya, sebuah server bernama `host.example.com` memberikan layanan WWW dan MAIL sekaligus.Untuk lebih memudahkan pengguna dalam mengakses layanan tersebut, dua rekaman CNAME dapat ditambahkan untuk server ini (`www.example.com` dan `mail.example.com`) di penyedia layanan DNS-nya sehingga semua permintaan untuk mengakses dua rekaman CNAME ini akan diteruskan ke `host.example.com`.

### Nama domain CNAME

- Di CDN, nama domain CNAME adalah nama domain yang berakhiran `.cdn.dnsv1.com` yang ditetapkan oleh sistem ke nama domain akselerasi terkoneksi yang dikonfigurasi di Konsol CDN.Anda harus mengonfigurasi rekaman CNAME di penyedia layanan nama domain Anda.Setelah rekaman tersebut aktif, CDN akan mengelola resolusi nama domain dan semua permintaan yang dikirim ke nama domain ini akan diteruskan ke penyedia edge CDN.
- Di GCD, nama domain CNAME adalah nama domain yang berakhiran `.cdn.dnsv1.com` yang ditetapkan oleh sistem ke nama domain akselerasi terkoneksi yang dikonfigurasi di Konsol GCD.Anda harus mengonfigurasi rekaman CNAME di penyedia layanan nama domain Anda.Setelah rekaman tersebut aktif, GCD akan mengelola resolusi nama domain dan semua permintaan yang dikirim ke nama domain ini akan diteruskan ke penyedia edge GCD.
- Di Tencent Cloud Enterprise Content Delivery Network (ECDN), nama domain CNAME adalah nama domain yang berakhiran `.cdn.dnsv1.com` yang ditetapkan oleh sistem ke nama domain akselerasi terkoneksi yang dikonfigurasi di Konsol ECDN.Anda harus mengonfigurasi rekaman CNAME di penyedia layanan nama domain Anda.Setelah rekaman tersebut aktif, resolusi nama domain akan dikelola oleh ECDN dan semua permintaan yang dikirim ke nama domain ini akan diteruskan ke simpul ECDN.

## D

### Konten Dinamis

Ini merujuk ke waktu pengguna mengirimkan beberapa permintaan untuk sumber daya yang sama, konten yang dikembalikan bervariasi, seperti API dan file .jsp, .asp, .php, .perl, dan .cgi.

## F

### Log Akses

Di CDN, log akses merujuk ke log terperinci permintaan akses pengguna ke nama domain Anda, meliputi waktu permintaan, IP klien, nama domain akses, jalur file, jumlah byte, kode unik, kode ISP, kode status HTTP, referer, Waktu-Permintaan, UA, rentang, metode HTTP, pengidentifikasi protokol, dan hit/miss cache.

## H

### Tarik-Asal

Di CDN, arti tarik-asal adalah bahwa ketika seorang pengguna mengirim permintaan dari peramban, server yang menanggapi permintaan tersebut adalah server dari situs web sumber, bukan server cache di simpul CDN.Secara umum, jika konten tidak di-cache di server cache atau diubah di server asal, konten tersebut akan ditarik dari server asal.

### Header Host

Di CDN, header host merujuk pada nama domain sebuah situs web yang diakses di server asal oleh simpul CDN selama tarik-asal.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Header Host] (https://intl.cloud.tencent.com/document/product/228/6293).

## J

### Konten Statis

Ini merujuk pada waktu pengguna mengirim beberapa permintaan untuk sumber daya yang sama, konten yang dikembalikan tetap sama, seperti file html, css, dan js, gambar, video, paket penginstalan perangkat lunak, file APK, dan file kompresi.

## M

### Hit Rate

Di CDN, hit rate adalah persentase permintaan hit dari total jumlah permintaan.Ketika seorang pengguna akhir menggunakan layanan CDN untuk mengakses sumber daya, sedangkan sumber daya yang diakses sudah di-cache di simpul CDN, sumber daya tersebut dapat dikembalikan langsung ke pengguna akhir. Itulah yang disebut "hit".Jika tidak, sumber daya tersebut harus diambil dari server asal, yang disebut "miss".

## S

### Latensi

Ini merujuk pada waktu yang dibutuhkan data untuk berpindah dari satu ujung jaringan ke ujung lainnya.

## Y

### Nama Domain

Nama domain berupa sederet alamat server yang mudah diingat dan digunakan dengan mudah oleh pengguna yang bisa berupa situs web, email, FTP, dll. Nama domain digunakan untuk mengidentifikasi lokasi elektronik (kadang-kadang disebut dengan lokasi geografis) komputer selama transfer data.

## Z

### Server Perantara

Ini adalah server tarik-asal di lapis tengah antara server bisnis (server asal) dan server edge.Server perantara dapat meng-cache permintaan tarik-asal dari beberapa server edge.Untuk permintaan dengan konten sama, server perantara hanya perlu melakukan satu tarik-asal untuk menayangkan konten ke setiap server edge sehingga mengurangi tekanan akses pada server bisnis (server asal).

### Server asal milik sendiri

Ini merujuk ke server untuk men-deploy layanan web Anda sendiri.Ketika melakukan koneksi ke nama domain akselerasi, Anda dapat memasukkan alamat IP publik milik server sebagai server asal.