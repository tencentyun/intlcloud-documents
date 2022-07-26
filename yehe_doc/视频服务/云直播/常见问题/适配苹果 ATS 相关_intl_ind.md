
Dalam acara WWDC 2016, Apple Inc. mengumumkan bahwa secara default semua Aplikasi baru yang dikirimkan mulai 1 Januari 2017 tidak akan diizinkan menggunakan `NSAllowsArbitraryLoads=YES` untuk melewati pembatasan ATS. Tencent Cloud akan secara resmi mendukung HTTPS mulai tanggal 12 Desember. Mulai saat itu, Anda hanya perlu menggunakan versi SDK baru (API tetap sama) dan mengubah awalan URL video dari `http://` menjadi `https://`. SDK baru dapat secara otomatis disesuaikan dengan perubahan tersebut.



Harap perhatikan bahwa dibandingkan dengan HTTP, HTTPS memiliki keamanan yang lebih tinggi, tetapi tidak semua video membutuhkannya. Namun, kecepatan koneksi HTTPS lebih lambat dan penggunaan CPU-nya lebih tinggi. Jika Aplikasi Anda masih perlu menggunakan HTTP berdasarkan kebijakan baru Apple, Anda perlu memodifikasi Info.plist dengan menambahkan `myqcloud.com` ke `NSExceptionDomains`, seperti yang ditunjukkan oleh gambar berikut ini.  

![myqcloud](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/myqcloud.png)

Tim audit Apple dapat memberikan persetujuan penonaktifan ATS untuk nama domain tertentu, tetapi Anda mungkin perlu menjelaskan bahwa `myqcloud.com` adalah nama domain untuk pemutaran ulang video.

