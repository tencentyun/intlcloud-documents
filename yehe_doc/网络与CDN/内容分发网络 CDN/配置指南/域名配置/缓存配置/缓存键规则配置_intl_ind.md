


## Ikhtisar Konfigurasi

CDN Tencent Cloud menggunakan format `Key-Value` (Kunci-Nilai) untuk memetakan sumber daya selama caching, dengan `Key` (Kunci) berarti kunci cache dan pengidentifikasi unik dari sumber daya yang di-cache.Dengan mengonfigurasi aturan kunci cache, Anda dapat mengonfigurasi fitur Ignore Query String (Abaikan String Kueri) dan Cache Ignore URL Case (Cache Abaikan Huruf Besar-Kecil URL) untuk konten berbagai jenis file untuk mengoptimalkan kunci cache.



### Ignore Query String (Abaikan String Kueri)

- Ketika pengguna mengakses sumber daya melalui URL, permintaan akses dapat membawa beberapa parameter untuk tujuan khusus.Misalnya, URL berikut digunakan untuk mewakili dua gambar berbeda:
`http://cloud.tencent.com/1.jpg?version=1`
`http://cloud.tencent.com/1.jpg?version=2`
Dalam skenario ini, Anda perlu menonaktifkan Ignore Query String (Abaikan String Kueri) dan menggunakan URL lengkap sebagai kunci cache untuk meng-cache gambar dan membedakan sumber daya.

- Jika Anda menggunakan parameter tanda tangan stempel waktu untuk autentikasi akses dalam skenario audio/video:
`http://cloud.tencent.com/1.mp4?sign=XXXXXX`
Dalam skenario ini, Anda perlu mengaktifkan Ignore Query String (Abaikan String Kueri) dan menggunakan bagian URL sebelum "?" (yaitu, `http://cloud.tencent.com/1.mp4`) sebagai kunci cache.Simpul kemudian hanya akan meng-cache satu sumber daya, dan cache dapat langsung terkena hit melalui autentikasi tanda tangan bahkan jika tanda tangan stempel waktu terus berubah.

### Cache Ignore URL Case (Cache Abaikan Huruf Besar-Kecil URL)

Jika huruf besar dari jalur URL sumber daya relevan dengan konten sumber daya dalam bisnis Anda, Anda dapat menonaktifkan "Cache Ignore URL Case" (Cache Abaikan Huruf Besar-Kecil URL).
Jika huruf besar dari jalur URL sumber daya tidak relevan dengan konten sumber daya dalam bisnis Anda, Anda dapat mengaktifkan "Cache Ignore URL Case" (Cache Abaikan Huruf Besar-Kecil URL) untuk meningkatkan hit rate.
>!Platform sedang ditingkatkan dan Cache Ignore URL Case (Cache Abaikan Huruf Besar-Kecil URL) tidak dapat diaktifkan saat ini.

## Panduan Konfigurasi

### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya.Pilih tab **Cache Configuration** (Konfigurasi Cache) untuk menemukan bagian **Cache Key Rule Configuration** (Konfigurasi Aturan Kunci Cache).

Saat menambahkan nama domain akselerasi, Ignore Query String (Abaikan String Kueri) diaktifkan atau dinonaktifkan secara default berdasarkan jenis bisnis akselerasi yang berbeda.

- Jika akselerasi statis dipilih, Ignore Query String (Abaikan String Kueri) dinonaktifkan secara default.Dalam konfigurasi kunci cache, Ignore Query String (Abaikan String Kueri) dari semua aturan file akan disinkronkan ke **Not Filter** (Tidak Difilter).
- Jika mengunduh atau melakukan streaming akselerasi VOD dipilih, Ignore Query String (Abaikan String Kueri) diaktifkan secara default.Dalam konfigurasi kunci cache, Ignore Query String (Abaikan String Kueri) dari semua aturan file akan disinkronkan ke **Filter All** (Filter Semua).


![](https://main.qcloudimg.com/raw/1f53ed863618b442233dd3e1bba6229b.png)

### Menambahkan aturan

Anda dapat menambahkan aturan cache sesuai kebutuhan.
<img src="https://main.qcloudimg.com/raw/48becf925518b2595097eddf7b4ec6d5.png" height="250" width="438" />

#### Batasan konfigurasi

- Setiap nama domain dapat dikonfigurasi dengan hingga 20 aturan kunci cache (termasuk aturan default).
- Prioritas aturan dapat disesuaikan: aturan di bagian bawah daftar memiliki prioritas lebih tinggi (prioritas aturan default tidak dapat disesuaikan).
- Di setiap aturan jenis file, folder, dan file jalur lengkap yang ditentukan, hingga 100 grup konten dapat dimasukkan.Silakan gunakan ";" untuk memisahkan konten yang berbeda, mis., "Jenis file tertentu - jpg;png".
- Ignore Query String (Abaikan String Kueri) - Cadangkan Parameter Tertentu.
- All files (Semua file): hingga 6 nama parameter dapat dimasukkan; masing-masing dapat berisi hingga 20 karakter.
- Jenis file/folder/file jalur lengkap tertentu: hingga 5 nama parameter dapat dimasukkan; masing-masing dapat berisi hingga 20 karakter.
Pisahkan setiap nama parameter dengan ";".Misalnya: key1;key2;key3.

### Memodifikasi aturan

Anda dapat mengeklik **Modify** (Modifikasi) untuk memodifikasi aturan kunci cache yang ditambahkan.

>!Aturan default mendukung modifikasi konfigurasi Ignore Query String (Abaikan String Kueri) dan Cache Ignore URL Case (Cache Abaikan Huruf Besar-Kecil URL), sedangkan jenis dan konten tidak dapat dimodifikasi.

### Menghapus aturan

Anda dapat mengeklik **Delete** (Hapus) untuk menghapus aturan kunci cache yang ditambahkan (kecuali aturan default).


## Sampel Konfigurasi

Jika konfigurasi aturan kunci cache dari nama domain akselerasi `www.test.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/8c3f7f534c5fa849ca1594a0a244d840.png)

Maka akses aktualnya adalah sebagai berikut:

Seorang klien mengakses sumber daya `www.test.com/abc.jpg?version=1&colour=red` dan `www.test.com/abc.JPG?version=1&colour=red`, dua permintaan tiba di simpul CDN X yang sumber dayanya tidak di-cache.

- Server asal akan ditarik untuk gambar `abc.jpg`, dan gambar tersebut akan di-cache pada simpul CDN X. Karena Ignore Query String (Abaikan String Kueri) diaktifkan dan **Filter All** (Filter Semua) dipilih, bagian URL `www.test.com/abc.jpg` sebelum "?" akan digunakan sebagai kunci cache.
- Klien mengakses sumber daya `www.test.com/abc.JPG?version=1&colour=red`, dan karena Cache Ignore URL Case (Cache Abaikan Huruf Besar-Kecil URL) dinonaktifkan, sumber daya yang di-cache `www.test.com/abc.jpg` tidak akan terkena hit, server asal akan ditarik untuk gambar `abc.JPG`, gambar tersebut akan di-cache pada simpul CDN X, dan `www.test.com/abc.JPG` akan digunakan sebagai kunci cache.



