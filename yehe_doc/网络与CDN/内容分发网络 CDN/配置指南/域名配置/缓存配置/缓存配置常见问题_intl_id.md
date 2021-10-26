### Apa itu konfigurasi validitas cache?
Konfigurasi validitas cache mengacu pada serangkaian kebijakan kedaluwarsa yang harus diikuti oleh simpul cache CDN saat meng-cache konten bisnis Anda.
Semua sumber daya yang di-cache pada simpul CDN memiliki waktu kedaluwarsa.Untuk sumber daya yang belum kedaluwarsa, ketika permintaan mencapai simpul, simpul akan langsung mengembalikan sumber daya yang diminta kepada pengguna sehingga mempercepat perolehan sumber daya.Untuk sumber daya yang kedaluwarsa, simpul akan meneruskan permintaan pengguna ke server asal untuk memperoleh kembali sumber daya, lalu meng-cache sumber daya tersebut ke simpul dan mengembalikannya ke pengguna pada saat yang sama.Periode validitas cache yang wajar dapat secara efektif meningkatkan hit rate sumber daya dan menurunkan kecepatan tarik-asal, mengurangi penggunaan bandwidth.

### Apa itu konfigurasi validitas cache lanjutan?
1.Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn) dan klik **Domain Management** (Pengelolaan Domain) di bilah samping kiri untuk masuk ke halaman pengelolaan.
2.Klik **Manage** (Kelola) di sebelah kanan nama domain target.
![](https://main.qcloudimg.com/raw/53c1171f8b1fdec4ddd2f87f6c47fe12.png)
3.Buka tab **Cache Configuration** (Konfigurasi Cache), temukan bagian **Simpul Cache Validity Configuration** (Konfigurasi Validitas Cache Simpul), dan aktifkan switch **Advanced Cache Validity Configuration** (Konfigurasi Validitas Cache Lanjutan).
![](https://main.qcloudimg.com/raw/b1288410345c3dd92907002ad5929d38.png)
4.Hasil berikut kemudian dicapai.
Saat pengguna meminta sumber daya tertentu dari server asal dan header HTTP respons menyertakan bidang `Cache-Control` dengan nilai `max-age=xxxx`, periode validitas cache untuk sumber daya pada simpul akan menjadi yang lebih kecil di antara periode validitas yang ditetapkan dan nilai `max-age`:
- Misalnya, jika `max-age` yang diatur untuk `/index.html` dari server asal adalah 200 detik dan periode validitas cache yang ditetapkan untuk CDN adalah 600 detik, periode validitas cache aktual untuk file tersebut adalah 200 detik.
- Jika `max-age` yang diatur untuk `/index.html` dari server asal adalah 800 detik dan periode validitas cache yang ditetapkan untuk CDN adalah 600 detik, periode validitas cache aktual untuk file tersebut adalah 600 detik.

>! Jika bidang `Cache-Control` tidak ada di header respons server asal Anda, CDN menambahkan header `Cache-Control: max-age=600` secara default.

### Bagaimana cara mengontrol validitas cache file di peramban?
Anda dapat mengonfigurasi validitas cache peramban di konsol CDN.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Validitas Cache Peramban](https://intl.cloud.tencent.com/document/product/228/38932).

### Bagaimana cara menyesuaikan prioritas konfigurasi cache?
Silakan lihat petunjuk di [Konfigurasi Validitas Simpul Cache (Lama)](https://intl.cloud.tencent.com/document/product/228/35317).

### Saya menggunakan server saya sendiri sebagai server asal CDN.Bisakah saya mengonfigurasinya agar tidak menyimpan jenis file tertentu?Bisakah saya mengatur periode validitas cache ke "0" untuk menonaktifkan proses cache?
Anda dapat mengonfigurasi periode validitas cache yang berbeda untuk jenis direktori dan file yang berbeda.Jika periode validitas cache dikonfigurasi ke 0, simpul CDN tidak akan menyimpan sumber daya, dalam hal ini simpul CDN perlu menarik sumber daya terkait dari server asal setiap kali pengguna mengirim permintaan akses ke simpul.Untuk informasi lebih lanjut tentang konfigurasi cache, silakan lihat [Konfigurasi Validitas Simpul Cache (Lama)](https://intl.cloud.tencent.com/document/product/228/35317).

### Konfigurasi validitas cache apa yang didukung Tencent Cloud?
CDN Tencent Cloud mendukung konfigurasi validitas cache di berbagai dimensi, penyesuaian prioritas khusus, dan kebijakan pewarisan cache (konfigurasi validitas cache lanjutan).Periode validitas cache yang wajar dapat secara efektif meningkatkan hit rate sumber daya dan menurunkan kecepatan tarik-asal, mengurangi penggunaan bandwidth.

### Bagaimana konfigurasi cache default CDN?
Konfigurasi default adalah sebagai berikut ketika nama domain terhubung:
- Koneksi nama domain asal eksternal: secara default, periode validitas cache untuk semua file adalah 30 hari, kecuali untuk file dinamis (seperti .php, .jsp, .asp, .aspx).Periode validitas cache untuk file dinamis ini adalah 0 secara default, yang berarti setiap permintaan untuk file tersebut akan langsung diteruskan ke server asal.
- Koneksi nama domain asal COS: secara default, periode validitas cache untuk semua file adalah 30 hari.
- Konfigurasi validitas cache lanjutan dinonaktifkan secara default.

### Apa itu kebijakan pewarisan cache?
Saat pengguna membuat permintaan untuk sumber daya bisnis tertentu, header HTTP respons server asal menyertakan bidang `Cache-Control`.Kebijakan default-nya adalah sebagai berikut:
- Jika bidang `Cache-Control` adalah `max-age`, periode validitas cache untuk sumber daya ini akan menjadi periode yang diatur untuk sumber daya, dan tidak akan mewarisi nilai yang ditentukan oleh `max-age`.
- Jika bidang `Cache-Control` adalah `no-cache` atau `no-store`, simpul CDN tidak akan meng-cache sumber daya.

### Apa itu aturan pencocokan cache?
Ketika beberapa kebijakan caching diatur, prioritas entri ditentukan berdasarkan aturan bawah ke atas, dengan entri di bagian bawah daftar memiliki prioritas tertinggi dan entri di bagian atas memiliki prioritas terendah.Misalnya, kebijakan caching berikut diatur untuk nama domain:
```
Semua file (30 hari)
.php .jsp .aspx 0 detik
jpg .png .gif 300 detik
/test/*.jpg 400 detik
/test/abc.jpg 200 detik
```

Jika nama domain adalah `www.test.com`, dan sumber dayanya adalah `www.test.com/test/abc.jpg`, aturan pencocokannya adalah sebagai berikut:
1.Cocokkan dengan entri pertama.Jika merupakan hit, periode validitas cache adalah 30 hari.
2.Cocokkan dengan entri kedua.Ini bukan merupakan hit.
3.Cocokkan dengan entri ketiga.Ini merupakan hit, periode validitas cache adalah 300 detik.
4.Cocokkan dengan entri keempat.Ini merupakan hit, periode validitas cache adalah 400 detik.
5.Cocokkan dengan entri kelima.Ini merupakan hit, periode validitas cache adalah 200 detik.

Periode validitas cache terakhir tergantung pada hasil pencocokan terakhir sehingga periode validitas cache-nya adalah 200 detik.
