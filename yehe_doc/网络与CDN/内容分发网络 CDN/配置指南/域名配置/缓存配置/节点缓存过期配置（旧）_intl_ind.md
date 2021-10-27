Konfigurasi validitas cache simpul diperbarui dengan mode lanjutan, yang mendukung konfigurasi yang lebih disempurnakan.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Validitas Cache Simpul (Baru)](https://intl.cloud.tencent.com/document/product/228/38424).

## Ikhtisar Konfigurasi
Cache sumber daya di CDN Tencent Cloud dipicu oleh permintaan.Ketika pengguna memulai permintaan akses ke sumber daya, jika simpul CDN yang menerima permintaan tidak menyimpan sumber daya yang diminta, simpul tersebut akan meneruskan permintaan ke server asal untuk menarik sumber daya.Setelah sumber daya berhasil ditarik oleh simpul (dengan kode status 2XX dikembalikan), sumber daya tersebut akan di-cache pada simpul dan dikembalikan ke pengguna.

Anda tidak dapat secara langsung mengelola sumber daya yang di-cache pada simpul CDN.Jika Anda khawatir sumber daya di server asal akan berubah tetapi simpul CDN masih akan meng-cache sumber daya lama dan mengembalikannya ke pengguna, Anda dapat mengonfigurasi aturan cache simpul.

Setiap sumber daya yang di-cache pada simpul CDN memiliki validitas.Jika sumber daya yang di-cache yang diminta telah kedaluwarsa, sumber daya tersebut akan dianggap tidak valid bahkan jika sumber daya tersebut masih di-cache di simpul.Simpul akan menarik sumber daya dari server asal lagi.Aturan cache simpul memungkinkan Anda mengonfigurasi periode validitas cache untuk sumber daya dalam jenis, direktori, dan jalur tertentu.Anda dapat mengonfigurasi item ini berdasarkan skenario bisnis aktual Anda.

## Panduan Konfigurasi
### Melihat konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya, dan beralihlah ke tab **Cache Configuration** (Konfigurasi Cache) untuk menemukan bagian **Simpul Cache Validity Configuration** (Konfigurasi Validitas Cache Simpul).
![](https://main.qcloudimg.com/raw/834d620b98c9d7d387547e59a7e6a1f4.png)

### Menambahkan aturan

CDN saat ini mendukung konfigurasi aturan validitas cache simpul dalam empat jenis berikut:
+ File: periode validitas cache dapat dikonfigurasi dengan ekstensi file yang dimasukkan.Ekstensi file yang berbeda harus dipisahkan dengan `;`, yaitu, `jpg;css`.
+ Folder: periode validitas cache dapat dikonfigurasi dengan jalur direktori yang dimasukkan dalam format `/test` dan tidak perlu diakhiri dengan `/`.Direktori yang berbeda harus dipisahkan dengan `;`.
+ Full-path file (File jalur lengkap): periode validitas cache dapat dikonfigurasi dengan jalur file lengkap yang dimasukkan dalam format `/index.html`.Jalur file lengkap dan jenis file dapat digabungkan untuk pencocokan, seperti `/test/*.jpg`.
+ Homepage (Beranda): periode validitas cache dapat dikonfigurasi oleh direktori root.

<img src="https://main.qcloudimg.com/raw/1a72478ce0bc4fc1ef6a22bcb8064a6b.png" style="width:400px"/>

**Batasan konfigurasi:**
- Setiap nama domain dapat dikonfigurasi dengan hingga 20 aturan cache.
- Anda dapat menyesuaikan prioritas untuk beberapa aturan.Aturan di bagian bawah daftar memiliki prioritas lebih tinggi.
- Di setiap aturan jenis file, folder, dan file jalur lengkap yang ditentukan, hingga 100 grup konten dapat dimasukkan.Silakan gunakan ";" untuk memisahkan konten yang berbeda, mis., "Jenis file tertentu - jpg;png".
- Validitas cache dapat diatur hingga 365 hari.

>! Jika **Advanced Mode** (Mode Lanjutan) dipilih untuk sebuah aturan, aturan tersebut akan ditingkatkan secara komprehensif sebagai mode lanjutan setelah dikirimkan dan tidak dapat lagi dipulihkan ke mode dasar.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Validitas Cache Simpul (Baru)](https://intl.cloud.tencent.com/document/product/228/38424).


#### Konfigurasi validitas cache lanjutan
Setelah diaktifkan, CDN akan membandingkan validitas cache dari aturan cache yang cocok dengan nilai "max-age" server asal, dan kemudian mengadopsi nilai yang lebih kecil sebagai validitas cache.

- Jika `Max-Age` yang dikonfigurasi untuk `/index.html` dari server asal adalah 200 detik, dan validitas cache yang dikonfigurasi untuk CDN adalah 600 detik, validitas cache file aktual adalah 200 detik.
- Jika `Max-Age` yang dikonfigurasi untuk `/index.html` dari server asal adalah 800 detik, dan validitas cache yang dikonfigurasi untuk CDN adalah 600 detik, validitas cache file aktual adalah 600 detik.

>! Setelah diaktifkan, jika server asal tidak mengembalikan bidang `Last-Modified` (Modifikasi Terakhir), CDN akan menambahkannya secara default dan mengubah nilainya setiap 10 menit sekali.

#### Ikuti server asal
Setelah diaktifkan, jika permintaan tidak cocok dengan aturan cache apa pun, server asal akan diikuti.

>! Switch ikuti server asal dan switch konfigurasi validitas cache lanjutan tidak dapat diaktifkan secara bersamaan.


### Kebijakan default
Jika tidak ada fitur yang diaktifkan, tidak ada aturan yang dikonfigurasi atau cocok dengan permintaan, kebijakan default akan diterapkan:
- Saat pengguna membuat permintaan untuk sumber daya bisnis tertentu, jika header respons HTTP dari server asal memuat bidang `Cache-Control`, `Cache-Control` tersebut akan diikuti.
- Jika header respons HTTP dari server asal tidak berisi bidang `Cache-Control`, validitas cache sumber daya pada simpul akan menjadi 600 detik.


## Sampel Konfigurasi
Konfigurasi validitas cache simpul untuk nama domain akselerasi `cloud.tencent.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/a585a6b560cb0e555b71e08bea179353.png)
Validitas cache aktual adalah sebagai berikut:

1. 400 detik untuk file `/test/def.jpg`.
2. 5 menit untuk file `/test/1.png`.
3. 30 hari untuk file lainnya.
