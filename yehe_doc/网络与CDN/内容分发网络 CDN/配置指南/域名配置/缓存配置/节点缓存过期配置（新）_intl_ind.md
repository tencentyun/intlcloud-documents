
## Ikhtisar Konfigurasi

Cache sumber daya di CDN Tencent Cloud dipicu oleh permintaan.Ketika pengguna memulai permintaan akses ke sumber daya, jika simpul CDN yang menerima permintaan tidak menyimpan sumber daya yang diminta, simpul tersebut akan meneruskan permintaan ke server asal untuk menarik sumber daya.Setelah sumber daya berhasil ditarik oleh simpul (dengan kode status 2XX dikembalikan), sumber daya tersebut akan di-cache pada simpul dan dikembalikan ke pengguna.

Anda tidak dapat secara langsung mengelola sumber daya yang di-cache pada simpul CDN.Jika Anda khawatir sumber daya di server asal akan berubah tetapi simpul CDN masih akan meng-cache sumber daya lama dan mengembalikannya ke pengguna, Anda dapat mengonfigurasi aturan cache simpul.


## Panduan Konfigurasi

### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya, dan beralihlah ke tab **Cache Configuration** (Konfigurasi Cache) untuk menemukan bagian **Simpul Cache Validity Configuration** (Konfigurasi Validitas Cache Simpul).

Saat menambahkan nama domain akselerasi, aturan validitas cache simpul default ditambahkan berdasarkan jenis layanan akselerasi yang berbeda dan dapat dimodifikasi sesuai kebutuhan.
- Jika akselerasi statis dipilih, file dinamis umum (seperti file PHP, JSP, ASP, dan ASPX) tidak akan di-cache secara default, dan file lain akan diatur untuk mengikuti server asal secara default.
![](https://main.qcloudimg.com/raw/5f48bc5246397975544baadf5ac81f4e.png)
- Jika akselerasi VOD unduhan atau streaming dipilih, validitas cache default semua file adalah 30 hari.
![](https://main.qcloudimg.com/raw/cdd00154330b8cb217287874f4f40693.png)

### Menambahkan aturan

Aturan cache simpul dapat diterapkan ke jenis file, folder, dan file jalur lengkap yang ditentukan:
<img src="https://main.qcloudimg.com/raw/5454a77683dca1cfb491eccdae839aa4.png" height="207" width="408" />


- Follow origin server (Ikuti server asal): ikuti header `Cache-Control` dari server asal.
- Saat header respons HTTP dari server asal berisi bidang `Cache-Control`:
Jika `Cache-Control` adalah `max-age`, nilai max-age akan digunakan sebagai validitas cache simpul.
Jika `Cache-Control` adalah `no-cache/no-store/private`, simpul CDN tidak akan meng-cache sumber daya.
- Jika header respons HTTP dari server asal tidak berisi bidang `Cache-Control`, simpul CDN tidak akan meng-cache sumber daya.
**Catatan:** Beberapa platform mungkin memiliki kebijakan default:Saat sumber daya diminta untuk pertama kalinya, permintaan akan diteruskan ke server asal dan simpul CDN akan menyimpan sumber daya tersebut.Jika sumber daya diminta lagi dan simpul terkena hit, CDN akan menambahkan header respons `Cache-Control: max-age=600`.
- Cache: mengonfigurasi validitas cache sumber daya pada simpul.
- Force cache (Paksa cache): mengonfigurasi apakah akan mengabaikan `Cache-Control: no-cache/no-store/private` dari server asal.Item ini diatur secara default ke "No" (Tidak).
**Catatan:** Jika paksa cache dikonfigurasi sebagai "Yes" (Ya), validitas cache simpul akan diatur ke nilai yang dikonfigurasi di sini.
Jika paksa cache dikonfigurasi sebagai "No" (Tidak) dan bidang `Cache-Control` dari server asal adalah `no-cache/no-store/private`, simpul CDN tidak akan meng-cache sumber daya bahkan saat validitas cache dikonfigurasi.
- No cache (Tidak ada cache):Simpul CDN tidak meng-cache sumber daya.






#### Batasan konfigurasi

- Maksimum 20 aturan caching dapat ditambahkan untuk satu nama domain.
- Prioritas aturan dapat disesuaikan: aturan di bagian bawah daftar memiliki prioritas lebih tinggi.
**Catatan:** Fitur "No max-age" sedang ditingkatkan dan saat ini tidak didukung.Silakan tunggu peluncuran resminya.Jika Anda telah mengonfigurasi aturannya, silakan hapus atau ubah aturan menjadi "All Files" (Semua File).
- Di setiap aturan jenis file, folder, dan file jalur lengkap yang ditentukan, hingga 100 grup konten dapat dimasukkan.Silakan gunakan ";" untuk memisahkan konten yang berbeda, mis., "Jenis file tertentu - jpg;png".


>! Jika ada konfigurasi validitas cache simpul lama (yaitu, mode dasar), konfigurasi tersebut akan ditingkatkan secara komprehensif setelah dikirimkan sebagai mode lanjutan dan tidak dapat lagi dikembalikan ke mode dasar.



### Kebijakan default

Kebijakan default di bawah ini akan diterapkan jika tidak ada aturan yang dikonfigurasi atau di-hit.
- Saat pengguna membuat permintaan untuk sumber daya bisnis tertentu, jika header respons HTTP dari server asal memuat bidang `Cache-Control`, `Cache-Control` tersebut akan diikuti.
- Jika header respons HTTP dari server asal tidak berisi bidang `Cache-Control`, validitas cache sumber daya pada simpul akan menjadi 600 detik.

## Sampel Konfigurasi

Konfigurasi validitas cache simpul untuk nama domain akselerasi `www.test.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/c1402003c4549d2e6035420921f67bd0.png)

Cache aktual adalah sebagai berikut:

- Meskipun `Cache-Control` adalah `no-cache/no-store/private`, validitas `www.test.com/abc.jpg` adalah 10 hari.
- `www.test.com/def.php` tidak akan di-cache ke simpul.



