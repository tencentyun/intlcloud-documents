## Ikhtisar Konfigurasi

- Penyeretan video umumnya terjadi dalam skenario VOD. Saat pengguna menyeret bilah kemajuan video, permintaan yang mirip dengan yang ditunjukkan di bawah ini akan dikirim ke server:
`http://www.test.com/test.flv?start=10`
  Dalam hal ini, data akan dikembalikan mulai dari byte ke-10. File video dalam skenario VOD semuanya di-cache di berbagai simpul CDN; oleh karena itu, simpul dapat langsung merespons permintaan tersebut setelah konfigurasi ini diaktifkan.
- Konfigurasi Ignore Query String (Abaikan String Kueri) harus diaktifkan untuk menyeret video. Yaitu, Ignore Query String (Abaikan String Kueri) dari semua aturan di [Konfigurasi Aturan Kunci Cache](https://intl.cloud.tencent.com/document/product/228/35316) harus dikonfigurasi sebagai "Filter All" (Filter Semua), dan server asal harus mendukung permintaan Range. Format file yang didukung adalah MP4, FLV, dan TS.

| Jenis File | Informasi Meta                                                 | Deskripsi Parameter (mulai)             | Sampel Permintaan                                       |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| MP4 | Untuk video di server asal, informasi meta harus ditempatkan di header file. Video dengan informasi meta yang terletak di akhir file tidak didukung. | Parameter `start` menentukan titik waktu (dalam detik) dan menggunakan desimal untuk menentukan milidetik. Misalnya, "start = 1.01" berarti waktu mulai adalah 1,01 detik. CDN akan menemukan keyframe terakhir sebelum waktu yang ditentukan oleh `start` jika `start` bukan keyframe. | `http://www.test.com/demo.mp4?start=10` menunjukkan bahwa video akan diputar ulang mulai dari detik ke-10. |
| FLV | Video di server asal harus memiliki informasi meta.                                   | Parameter `start` menentukan satu byte. CDN akan secara otomatis menemukan keyframe terakhir sebelum byte yang ditentukan oleh `start` jika `start` bukan keyframe.| `http://www.test.com/demo.flv?start=10` menunjukkan bahwa video akan diputar ulang mulai dari byte ke-10. |
| TS | Tidak ada persyaratan khusus.                                                   | Parameter `start` menentukan titik waktu (dalam detik) dan menggunakan desimal untuk menentukan milidetik. Misalnya, "start = 1.01" berarti waktu mulai adalah 1,01 detik. CDN akan menemukan keyframe terakhir sebelum waktu yang ditentukan oleh `start` jika `start` bukan keyframe. | `http://www.test.com/demo.ts?start=10` menunjukkan bahwa video akan diputar ulang mulai dari detik ke-10. |


## Melihat Konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik nama domain akselerasi VOD streaming untuk masuk ke halaman konfigurasi. Buka tab **Access Control** (Kontrol Akses) untuk menemukan bagian **Video Dragging** (Seret Video). Seret video dinonaktifkan secara default.
![img](https://main.qcloudimg.com/raw/515a46c56b93b9932f5bbcab39a8293e.png)
