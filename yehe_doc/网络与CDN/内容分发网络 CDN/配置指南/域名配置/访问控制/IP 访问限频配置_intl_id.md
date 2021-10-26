## Ikhtisar Konfigurasi
Untuk mengontrol sumber akses ke sumber daya bisnis Anda, Anda dapat menggunakan fitur batas akses IP di CDN. Dengan membatasi jumlah permintaan akses ke simpul per detik dari IP klien, Anda dapat mempertahankan diri dari serangan CC frekuensi tinggi dan mencegah terjadinya hotlink oleh pengguna yang berniat buruk.


## Panduan Konfigurasi
### Melihat konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Buka tab **Access Control** (Kontrol Akses) untuk melihat bagian **IP Access Limit Configuration** (Konfigurasi Batas Akses IP). Bagian ini dinonaktifkan tanpa nilai yang ditetapkan secara default:
![](https://main.qcloudimg.com/raw/647b73c63e867b31dfc1116fec3225b0.png)

### Mengaktifkan konfigurasi

Alihkan switch, atur ambang batas, dan klik **OK**.
![](https://main.qcloudimg.com/raw/15303948df14017a03ed7b5890c3673a.png)
**Deskripsi konfigurasi**

+ Setelah konfigurasi diaktifkan, kesalahan 514 akan dikembalikan untuk permintaan yang melebihi batas QPS. Batas frekuensi akses yang rendah dapat memengaruhi penggunaan normal bisnis Anda oleh pengguna frekuensi tinggi. Konfigurasikan batas frekuensi yang tepat sesuai dengan kondisi bisnis dan skenario penggunaan aktual Anda.
+ Batas akses IP efektif untuk serangan dari satu IP ke satu simpul. Jika pengguna yang berniat buruk menggunakan sejumlah besar IP untuk menyerang simpul di seluruh jaringan Anda, fitur ini tidak lagi berlaku.

### Menonaktifkan konfigurasi
Anda dapat menonaktifkan switch untuk menonaktifkan fitur ini. Saat switch dinonaktifkan, fitur ini tidak diterapkan di lingkungan produksi meskipun ada konfigurasi yang sudah ada. Saat switch aktif, konfigurasi ini akan diterapkan di seluruh jaringan:
![](https://main.qcloudimg.com/raw/1f3c1893aed28e3845a1adaea9abf1d9.png)

> !Jika nama domain akselerasi Anda dikonfigurasi untuk akselerasi global, konfigurasi batas akses IP akan diterapkan secara global. Konfigurasi ini tidak membedakan antara permintaan dari wilayah di dalam dan di luar Tiongkok Daratan.

## Sampel Konfigurasi
Batas akses IP untuk nama domain akselerasi `www.test.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/0d78c86a122b3b58c35ca2ba8b3316b6.png)
Maka akses aktualnya adalah sebagai berikut:
1. Seorang pengguna dengan IP klien `1.1.1.1` meminta sumber daya `http://www.test.com/1.jpg` sebanyak 10 kali dalam satu detik, dan semua permintaan akses dibuat ke satu server pada simpul cache CDN A. 10 log akses akan dibuat di server ini, 9 di antaranya melebihi batas QPS. Kode status "514" akan dikembalikan.
2. Seorang pengguna dengan IP klien `2.2.2.2` meminta sumber daya `http://www.test.com/1.jpg` dua kali dalam satu detik, dan permintaan akses dapat didistribusikan ke dua simpul cache CDN untuk diproses karena kondisi jaringan. Setiap simpul akan mengembalikan konten secara normal.

