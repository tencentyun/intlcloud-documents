
Indikasi Nama Server (SNI) didesain untuk menyelesaikan masalah bahwa satu server hanya bisa menggunakan satu sertifikat untuk meningkatkan perpanjangan SSL/TLS dari server dan klien.Jika suatu server mendukung SNI, artinya server tersebut bisa diikat ke beberapa sertifikat.Untuk menggunakan SNI untuk klien, nama domain yang akan disambungkan harus ditentukan sebelum koneksi SSL/TLS ke server tersambung, dan kemudian server akan mengembalikan sertifikat yang sesuai berdasarkan nama domain.

## Kasus Penggunaan
Pendengar CLB HTTPS lapisan 7 mendukung SNI, yaitu, mengikat beberapa sertifikat, yang bisa digunakan oleh nama-nama domain berbeda di aturan pendengaran.Contohnya, di pendengar `HTTPS:443` yang sama dari suatu instance CLB, Anda bisa menggunakan sertifikat 1 dan sertifikat 2 untuk `*.test.com` dan `*.example.com` masing-masing untuk meneruskan permintaan dari nama-nama domain ini ke dua set server yang berbeda.

## Prasyarat
Anda telah [membeli satu instance CLB](https://buy.cloud.tencent.com/lb?rid=1&type=2&vpcId=vpc-k9gii1kb).
>CLB klasik tidak mendukung penerusan berdasarkan nama domain dan URL; jadi, tidak mendukung SNI.

## Petunjuk
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb).
2.[Konfigurasi pendengar HTTPS](https://intl.cloud.tencent.com/document/product/214/32516#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E9.85.8D.E7.BD.AE.E7.9B.91.E5.90.AC.E5.99.A8) dan aktifkan SNI.
![](https://main.qcloudimg.com/raw/eb6958c5f3772c3b55ab3a2a1e92d341.png)
3.Saat menambahkan aturan penerusan pada pendengar, konfigurasikan sertifikat server berbeda untuk nama-nama domain berbeda.Kemudian, klik **Next** (Berikutnya) dan konfigurasikan pemeriksaan kesehatan dan persistensi sesi.
![](https://main.qcloudimg.com/raw/bf5150f1f263a133770f1ad5694f501c.png)
