## Ikhtisar Konfigurasi
CDN Tencent Cloud membagi file menjadi beberapa pecahan untuk meningkatkan efisiensi penyimpanan saat meng-cache sumber daya. CDN juga mendukung permintaan Range. Misalnya, jika permintaan membawa header HTTP `Range: bytes = 0-999`, 1000 byte pertama file akan dikembalikan ke pengguna.

Setelah Range GETs diaktifkan, jika sebagian file yang diminta oleh pengguna telah kedaluwarsa, CDN akan melakukan Range GETs untuk menarik dan meng-cache sebagian file yang diperlukan dan mengembalikannya ke pengguna. Setelah Range GETs dinonaktifkan, bahkan jika pengguna hanya meminta sebagian file, CDN akan menarik seluruh file dan kemudian meng-cache file tersebut sebelum mengembalikan sebagian file yang diminta kepada pengguna.

Mengaktifkan Range GETs dapat sangat meningkatkan efisiensi pengiriman file besar, mengurangi waktu respons, dan tekanan pada server asal.

> ?
> - Setelah Range GETs diaktifkan, sumber daya akan di-cache dalam pecahan pada simpul. Pecahan ini memiliki periode validitas cache yang sama dan mengikuti aturan validitas cache yang ditentukan oleh pengguna.
> - Untuk mengaktifkan konfigurasi Range GETs, pastikan server asal mendukung permintaan Range, atau tarik-asal akan gagal.

## Panduan Konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Buka tab **Origin-pull Configuration** (Konfigurasi Tarik-asal) untuk melihat bagian **Range GETs Configuration** (Konfigurasi Range GETs).

Ini dinonaktifkan secara default. Jika nama domain memiliki asal COS, konfigurasi diaktifkan secara default. Anda dapat mengaktifkan dan menonaktifkannya sesuai kebutuhan.
![](https://main.qcloudimg.com/raw/04b9ec63d365b60ba2c3a8c16bc61c36.png)



## Sampel Konfigurasi
Jika konfigurasi Range GETs dari nama domain `cloud.tencent.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/04b9ec63d365b60ba2c3a8c16bc61c36.png)
Pengguna A membuat permintaan untuk sumber daya `http://cloud.tencent.com/test.apk`. Setelah simpul menerima permintaan dan menemukan bahwa file cache `test.apk` telah kedaluwarsa, simpul akan memulai permintaan Range GETs untuk mendapatkan dan meng-cache sumber daya berdasarkan pecahan. Jika pengguna B juga membuat permintaan Range saat ini dan pecahan yang disimpan pada simpul cocok dengan segmen byte yang ditentukan dalam permintaan Range, sumber daya akan langsung dikembalikan ke pengguna B meskipun pecahan tidak sepenuhnya diperoleh.

