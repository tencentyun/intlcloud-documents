## Apa itu server asli?
Server asli adalah [instance CVM](https://intl.cloud.tencent.com/doc/product/213) yang terikat ke instance CLB yang dibuat untuk memproses permintaan.Saat mengonfigurasi [pendengar CLB](https://intl.cloud.tencent.com/document/product/214/6151), Anda harus mengikat instance CVM sebagai server asli.Melalui berbagai [metode polling](https://intl.cloud.tencent.com/document/product/214/6153), CLB meneruskan permintaan ke server asli untuk pemrosesan untuk memastikan kestabilan dan keandalan aplikasi.Anda bisa mengikat instance CVM menjadi satu zona ketersediaan atau lebih, di wilayah tempat instance CLB berada untuk meningkatkan ketahanan aplikasi dan memblokir satu titik kegagalan.

## Tindakan pencegahan
Saat menambahkan satu server asli, Anda sebaiknya:
- Menginstal server web (misalnya, Apache atau IIS) pada semua instance CVM untuk diikat ke instance CLB dan memastikan konsistensi aplikasi.
- Anda disarankan untuk mengaktifkan [persistensi sesi](https://intl.cloud.tencent.com/document/product/214/6154), agar CLB bisa mempertahankan koneksi TCP yang lebih panjang untuk digunakan ulang oleh beberapa permintaan sehingga mengurangi beban server web dan meningkatkan throughput CLB.
- Pastikan grup keamanan instance nyata memiliki aturan masuk untuk port pendengar CLB dan port pemeriksaan kesehatan.Untuk informasi selengkapnya, silakan lihat [Kendali Akses Server Asli](https://intl.cloud.tencent.com/document/product/214/6157).
