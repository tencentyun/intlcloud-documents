## Ikhtisar Fitur

Dengan mengonfigurasi validitas cache peramban, Anda dapat menyesuaikan kebijakan cache peramban klien untuk mengurangi tingkat tarik-asal.

> ?Ketika permintaan datang, jika sumber daya yang diminta di-cache di peramban, permintaan tersebut akan langsung dikembalikan.Jika tidak, permintaan akan diteruskan ke simpul cache CDN.Jika sumber daya masih tidak dapat ditemukan di simpul cache, permintaan akan diteruskan ke server asal.

## Panduan Konfigurasi

### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya.Buka tab **Cache Configuration** (Konfigurasi Cache) untuk menemukan bagian **Browser Cache Validity Configuration** (Konfigurasi Validitas Cache Peramban).
![](https://main.qcloudimg.com/raw/d74acc06100e385c87176d62459f12a6.png)



### Menambahkan aturan

Klik **Add Rule** (Tambahkan Aturan) untuk menambahkan aturan validitas cache peramban untuk jenis file, direktori file, jalur file, dan beranda tertentu.
<img src="https://main.qcloudimg.com/raw/d98a14185f9e9d41d682fb356601e9e5.jpg" style="height:220px"/>

- Follow origin server (Ikuti server asal): ikuti header `Cache-Control` dari server asal.Jika server asal tidak memiliki header CC atau header CC-nya adalah `no-cache/no-store/private`, peramban tidak akan meng-cache sumber daya.
- Cache: jika header CC dari server asal bukan `no-cache/no-store/private`, aturan validitas cache peramban akan diterapkan; jika tidak, peramban tidak akan meng-cache sumber daya.
- No cache (Tidak ada cache): tidak ada sumber daya yang di-cache di peramban.


**Batasan konfigurasi**

- Setiap nama domain dapat memiliki hingga 20 aturan.Hanya satu aturan "All Files" (Semua File) dan "Homepage" (Beranda) yang dapat ditambahkan.
- Anda dapat menyesuaikan prioritas untuk beberapa aturan.Aturan di bagian bawah daftar memiliki prioritas lebih tinggi.
- Di setiap aturan jenis file, direktori file, dan jalur file tertentu, hingga 50 grup konten dapat dimasukkan.Silakan gunakan ";" untuk memisahkan konten yang berbeda, mis., Jenis File Tertentu: jpg;png.
- Karakter bahasa Mandarin tidak didukung.

### Kebijakan default
Jika tidak ada aturan yang dikonfigurasi atau cocok dengan permintaan, kebijakan default akan diterapkan:
- Saat pengguna membuat permintaan untuk sumber daya bisnis tertentu, jika header respons HTTP dari server asal memuat bidang `Cache-Control`, `Cache-Control` tersebut akan diikuti.
- Jika header respons HTTP dari server asal tidak memuat bidang `Cache-Control`, validitas cache sumber daya pada peramban akan menjadi 600 detik.

Saat ada aturan validitas cache simpul yang dikonfigurasi (panduan konfigurasi: [Konfigurasi Validitas Cache Simpul (Baru)](https://intl.cloud.tencent.com/document/product/228/38424)) atau dicocokkan:
- Jika header respons HTTP dari server asal tidak memuat bidang `Cache-Control`, peramban tidak akan meng-cache sumber daya.
- Jika header respons HTTP dari server asal memuat bidang `Cache-Control`, cache peramban akan mengikuti `Cache-Control`.
