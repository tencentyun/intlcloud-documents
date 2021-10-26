## Ikhtisar Konfigurasi

Jika Anda perlu memodifikasi URL permintaan tarik-asal ke URL yang cocok dengan server asal, Anda dapat menggunakan konfigurasi penulisan ulang URL asal di CDN Tencent Cloud.

>! Fitur ini tidak tersedia untuk nama domain ECDN.


## Petunjuk

### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya, dan beralihlah ke tab **Origin-pull Configuration** (Konfigurasi Tarik-asal) untuk menemukan bagian **Origin URL Rewrite Configuration** (Konfigurasi Tulis Ulang URL Asal).
![](https://main.qcloudimg.com/raw/e6721b8c8d3ebcb9b5a27fb36e6c6782.png)



### Menambahkan aturan

Anda dapat mengeklik **Add Rule** (Tambahkan Aturan) untuk menambahkan aturan penulisan ulang sesuai kebutuhan.
<img src="https://main.qcloudimg.com/raw/5f7d6907976fb0696f633af29321c99c.jpg" style="height:300px"/>


**Batasan konfigurasi**

- Setiap nama domain dapat memiliki hingga 100 aturan penulisan ulang.
- Anda dapat menyesuaikan prioritas untuk beberapa aturan. Aturan di bagian bawah daftar memiliki prioritas lebih tinggi.
- Current Origin URL (URL Asal Saat Ini): dimulai dengan “/”; pencocokan awalan digunakan secara default; mendukung pencocokan jalur lengkap (mis., /test/a.jpg) dan pencocokan kartubebas (*) (mis., /test/*/*.jpg). Jika Anda ingin menentukan direktori file, Anda tidak dapat mengakhiri jalur dengan “/” (mis., /test).
- Target Origin Domain (Domain Asal Target): nama domain saat ini digunakan secara default (tidak termasuk “http://” dan “https://”). Anda dapat memodifikasinya sesuai kebutuhan.
- Target Origin Path (Jalur Asal Target): dimulai dengan “/” (mis., /newtest/b.jpg); kartubebas “*” dapat ditangkap dengan “$n” (mis., jika n=1,2,3… maka /newtest/$1/$2.jpg). Jika Anda ingin menentukan direktori file, Anda tidak dapat mengakhiri jalur dengan “/” (mis., /test).
- Hingga 5 "*" dan 10 "$n" didukung.
- Domain asal target dapat memuat hingga 250 karakter. Konten lain dapat memuat hingga 1.024 karakter. 



## Sampel Konfigurasi:

Misalkan **Origin URL Rewrite Configuration** (Konfigurasi Tulis Ulang URL Asal) dari nama domain akselerasi www.test.com adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/c255f4e4643a15e2e47a29a608a9fd01.png)

Tarik-asal akan ditulis ulang sebagai berikut:
- Jika www.test.com/images/1.jpg diminta, permintaan tersebut mengenai hit aturan pertama dan ketiga. Saat aturan dijalankan dari bawah ke atas, URL akan ditulis ulang ke www.test.com/index.html.
- Jika www.test.com/images diminta, permintaan tersebut mengenai hit aturan pertama, kedua, dan ketiga. Saat aturan dijalankan dari bawah ke atas, URL akan ditulis ulang ke www.test.com/index.html.
