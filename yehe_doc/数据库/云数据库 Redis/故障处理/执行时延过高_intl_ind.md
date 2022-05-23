## Deskripsi Kesalahan
- Gejala 1: latensi eksekusi tinggi.
![](https://qcloudimg.tencent-cloud.cn/raw/54be4ba25f7a821e9686972690a942cb.png)
- Gejala 2: bisnis terpengaruh.

## Penyebab Umum
- Jumlah total permintaan terlalu tinggi.
- Lalu lintas dan koneksi dibatasi.
- Ada perintah kompleks seperti KEYS \* dan MGET.

## Solusi
Anda dapat memeriksa apakah masalah di atas ada berdasarkan data pemantauan di konsol dan logika bisnis Anda sendiri dan membuat pengoptimalan yang ditargetkan.

## Prosedur Pemecahan Masalah
1. Jika jumlah total permintaan tinggi, lihat [Jumlah Permintaan Total Tinggi](https://intl.cloud.tencent.com/document/product/239/44295).
2. Jika lalu lintas dibatasi, lihat [Lalu Lintas Keluar Tinggi](https://intl.cloud.tencent.com/document/product/239/41812). Jika jumlah koneksi dibatasi, lihat [Penggunaan Koneksi Tinggi](https://intl.cloud.tencent.com/document/product/239/44296).
3. Optimalkan perintah kompleks. Jika ada perintah \*KEYS, Anda dapat mempertimbangkan untuk menggunakan perintah SCAN guna melakukan penjelajahan dalam batch alih-alih menggunakan KEYS dengan kompleksitas waktu yang lebih tinggi. Jika ada perintah MGET, Anda dapat mempertimbangkan untuk membaginya menjadi n operasi untuk mendapatkan n kunci.


>?Jika masalah berlanjut, [hubungi kami](https://cloud.tencent.com/online-service?from=connect-us).
