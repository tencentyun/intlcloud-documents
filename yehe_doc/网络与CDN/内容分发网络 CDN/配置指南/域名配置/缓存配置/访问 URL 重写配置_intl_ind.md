## Ikhtisar Konfigurasi

Jika Anda perlu memodifikasi URL akses aktual ke URL yang cocok dengan server asal, Anda dapat menggunakan konfigurasi tulis ulang URL akses di CDN Tencent Cloud.

Anda dapat melakukan kustomisasi konfigurasi tulis ulang URL akses untuk mengalihkan URL 302 ke URL yang ditentukan.

## Panduan Konfigurasi

### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya, dan buka tab **Cache Configuration** (Konfigurasi Cache) untuk menemukan bagian **Access URL Rewrite Configuration** (Konfigurasi Tulis Ulang URL Akses).

**Access URL Rewrite Configuration** (Konfigurasi Tulis Ulang URL Akses) dinonaktifkan secara default.
![](https://main.qcloudimg.com/raw/01f93aaa70c523ae0bb1ab5debae8558.png)


### Menambahkan aturan

Anda dapat mengeklik **Add Rewrite Rule** (Tambahkan Aturan Tulis Ulang) untuk menambahkan aturan sesuai kebutuhan.
<img src="https://main.qcloudimg.com/raw/97ea8713395f3af8654c39be97f124d3.png"  style="height:300px"></img>

**Batasan konfigurasi**
+ Setiap nama domain dapat memiliki hingga 100 aturan tulis ulang.
+ Anda dapat menyesuaikan prioritas untuk beberapa aturan. Aturan di bagian bawah daftar memiliki prioritas lebih tinggi.
+ URL saat ini: dimulai dengan `/`; mendukung pencocokan jalur lengkap (mis., /test/a.jpg) dan pencocokan kartubebas (*) (mis., /test/*/*.jpg). Jika Anda ingin menentukan direktori file, Anda tidak dapat mengakhiri jalur dengan `/` (mis., /test).
+ Target Host (Host Target): ini adalah nama domain saat ini (dimulai dengan `http://`) secara default. Host Target dapat dimodifikasi ke nama domain lain yang dimulai dengan `http://` atau `https://`.
+ Target Path (Jalur Target): dimulai dengan `/` (mis., /newtest/b.jpg); kartubebas `*` dapat ditangkap dengan `$n` (mis., jika n=1,2,3… maka /newtest/$1/$2.jpg). Jika Anda ingin menentukan direktori file, Anda tidak dapat mengakhiri jalur dengan `/` (mis., /test).
+ Hingga 5 `*` dan 10 `$n` didukung.
+ Konten dapat berisi hingga 1.024 karakter dan karakter bahasa Mandarin tidak didukung.




## Sampel Konfigurasi

Jika **Access URL Rewrite Configuration** (Konfigurasi Tulis Ulang URL Akses) dari nama domain akselerasi `www.test.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/214b034e578d5eaac0a63cacd49f1e2d.png)

Maka akses aktualnya adalah sebagai berikut:

+ Seorang klien meminta `www.test.com/test/a.jpg` dan simpul CDN mengembalikan `www.test.com/newtest/b.jpg`.
+ Seorang klien meminta `www.test.com/test/a.png` dan simpul CDN mengembalikan `www.newtest.com/newtest/a.png`.



