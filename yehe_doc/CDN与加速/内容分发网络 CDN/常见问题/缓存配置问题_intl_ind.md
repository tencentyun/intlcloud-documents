[](id:q1)

### Apa itu konfigurasi validitas cache?
Konfigurasi validitas cache adalah serangkaian kebijakan validitas yang harus diikuti simpul cache CDN saat meng-cache konten bisnis Anda.
Semua sumber daya yang di-cache pada simpul CDN memiliki validitas.Untuk sumber daya yang belum kedaluwarsa, jika suatu permintaan mencapai simpul, simpul tersebut akan langsung mengembalikan sumber daya yang diminta kepada pengguna sehingga mempercepat pemerolehan sumber daya tersebut.Untuk sumber daya yang kedaluwarsa, simpul tersebut akan meneruskan permintaan pengguna ke server asal, mendapatkan kembali sumber daya tersebut dan meng-cache-nya ke simpul tersebut, dan kemudian mengembalikannya kepada pengguna.Validitas cache yang benar dapat secara efektif meningkatkan kecepatan perolehan sumber daya dan mengurangi kecepatan tarik-asal sehingga mengurangi penggunaan bandwidth.


[](id:q2)
### Bagaimana saya mengatur validitas cache file di suatu peramban?
Anda dapat mengonfigurasi validitas cache peramban di konsol.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Validitas Cache Peramban](https://intl.cloud.tencent.com/document/product/228/38932).

[](id:q3)
### Saya menggunakan server milik sendiri sebagai server asal CDN.Bisakah saya mengonfigurasi CDN agar tidak meng-cache jenis file tertentu?Bisakah saya mengatur validitas cache menjadi "0" untuk menonaktifkan peng-cache-an?
Anda dapat mengonfigurasi masa validitas cache yang berbeda untuk jenis direktori dan file yang berbeda.Jika validitas cache dikonfigurasikan menjadi "0", simpul CDN tidak akan meng-cache sumber daya tersebut sehingga simpul CDN harus menarik sumber daya yang terkait dari server asal setiap kali pengguna mengirimkan permintaan akses ke simpul tersebut.Untuk informasi selengkapnya mengenai konfigurasi cache, silakan lihat [Konfigurasi Validitas Cache Simpul (Lama)](https://intl.cloud.tencent.com/document/product/228/35317).

[](id:q4)
### Apa konfigurasi validitas cache yang didukung Tencent Cloud?
Tencent Cloud CDN mendukung konfigurasi tindakan cache dan aturan validitas cache untuk berbagai jenis file, dan Anda juga dapat mengatur prioritas aturan cache khusus.Aturan validitas cache yang benar dapat secara efektif meningkatkan kecepatan perolehan sumber daya dan mengurangi kecepatan tarik-asal sehingga mengurangi penggunaan bandwidth.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Cache](https://intl.cloud.tencent.com/document/product/228/35315).

[](id:q5)
### Apa konfigurasi cache default CDN?
Saat menambahkan nama domain akselerasi, aturan default validitas cache simpul ditambahkan berdasarkan jenis layanan akselerasi yang berbeda dan dapat diubah jika perlu.
- Jika akselerasi statis dipilih, file dinamis umum (seperti file PHP, JSP, ASP, dan ASPX) tidak akan di-cache menurut pengaturan default, dan file lainnya akan diatur untuk mengikuti server asal menurut pengaturan default.
- Jika akselerasi unduh atau streaming VOD dipilih, validitas cache default semua file adalah 30 hari.


[](id:q6)
### Apa aturan pencocokan cache?
Jika banyak aturan cache yang ditetapkan, aturan di bagian bawah daftar memiliki prioritas lebih tinggi.Misalnya, jika suatu nama domain dikonfigurasikan sebagai berikut:
```
Semua file - 30 hari
.php .jsp .aspx - 0 detik
.jpg .png .gif - 300 detik
/test/*.jpg - 400 detik
/test/abc.jpg - 200 detik
```

Jika nama domainnya `www.test.com`, dan sumber dayanya `www.test.com/test/abc.jpg`, aturan pencocokannya adalah sebagai berikut:
1.Cocokkan dengan aturan pertama.Jika cocok, validitas cache-nya adalah 30 hari.
2.Cocokkan dengan aturan kedua.Tidak cocok.
3.Cocokkan dengan aturan ketiga.Jika cocok, validitas cache-nya 300 detik.
4.Cocokkan dengan aturan keempat.Jika cocok, validitas cache-nya 400 detik.
5.Cocokkan dengan aturan kelima.Jika cocok, validitas cache-nya 200 detik.

Validitas cache akhir tergantung pada hasil pencocokan terakhir sehingga validitas cache-nya adalah 200 detik.
