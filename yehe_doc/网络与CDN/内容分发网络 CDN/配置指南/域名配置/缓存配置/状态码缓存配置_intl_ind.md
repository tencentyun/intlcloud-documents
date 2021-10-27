
## Ikhtisar Konfigurasi
Biasanya, ketika simpul CDN berhasil menarik sumber daya yang diminta dari server asal (dengan kode status 2XX dikembalikan), simpul akan memproses sumber daya berdasarkan aturan dalam konfigurasi validitas cache simpul.
Jika server asal tidak dapat memproses permintaan non-2XX dengan cepat, dan Anda tidak ingin semua permintaan diteruskan ke server asal, Anda dapat mengonfigurasi periode validitas cache kode status. Dalam hal ini, simpul CDN akan langsung merespons permintaan non-2XX, membantu mengurangi tekanan pada server asal.
Kode status yang saat ini didukung adalah sebagai berikut:
- 4XX: 400, 401, 403, 404, 405, 407, 414
- 5XX: 500, 501, 502, 503, 504, 509, 514

>! 
>- Untuk saat ini, beberapa platform hanya mendukung kode 404 dan 403. Kami akan menyelesaikan peningkatan server sesegera mungkin.
>- Saat ini, hanya kode status 404 dan 403 yang didukung di wilayah di luar Tiongkok Daratan. Jika wilayah akselerasi nama domain adalah "Global", aturan cache kode status kecuali 404 dan 403 hanya akan berlaku di Tiongkok Daratan.


## Panduan Konfigurasi

### Melihat konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya, dan beralihlah ke tab **Cache Configuration** (Konfigurasi Cache) untuk menemukan bagian **Status Code Cache** (Cache Kode Status).
Ada aturan default, yang akan meng-cache 404 permintaan selama 10 detik.
![](https://main.qcloudimg.com/raw/508f716869f48fad3424fe6eeb77a67c.png)

### Menambahkan aturan
Anda dapat mengeklik **Add Rule** (Tambahkan Aturan) untuk menambahkan aturan cache kode status sesuai kebutuhan.
<img src="https://main.qcloudimg.com/raw/3f01868799d0ddeda302e52e634bbde1.png" style="height:185px"/>

Batasan konfigurasi
- Setiap kode status hanya dapat memiliki satu aturan unik.
- Waktu cache `0` berarti tidak meng-cache konten.
