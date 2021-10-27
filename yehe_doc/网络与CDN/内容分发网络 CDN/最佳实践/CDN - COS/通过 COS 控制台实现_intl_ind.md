Dokumen ini menguraikan cara mempercepat akses ke sumber daya di COS melalui CDN pada konsol COS.

## Prasyarat
1.Anda telah mendaftar akun Tencent Cloud dan memverifikasi identitas Anda.
2.Anda telah mengaktifkan layanan CDN.Untuk informasi selengkapnya, silakan baca [Memulai](https://intl.cloud.tencent.com/document/product/228/32978).

## Panduan Pengoperasian

### Membuat bucket
Untuk informasi selengkapnya mengenai cara membuat bucket, silakan lihat [Membuat Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

### Mengonfigurasi Akselerasi
1.Setelah membuat bucket, masuklah ke halaman pengelolaan konfigurasinya secara langsung.Anda juga bisa mengeklik **Configuration Management** (Pengelolaan Konfigurasi) pada kolom "Operasi" bucket di daftar bucket untuk masuk ke halaman pengelolaan konfigurasinya.
2.Aktifkan **default acceleration domain name** (nama domain akselerasi default).
Dihasilkan oleh sistem, **default acceleration domain name** (nama domain akselerasi default) merupakan nama domain yang melalui simpul cache CDN.Anda dapat memilih untuk mengaktifkan atau menonaktifkannya.
(1) Klik **Edit** (Edit) di sebelah **default acceleration domain name** (nama domain akselerasi default) untuk mengaktifkan atau menonaktifkannya secara manual di halaman konfigurasi akselerasi default.
![](https://main.qcloudimg.com/raw/260fde070f4b2f999c0d9d09bec13d55.png)
(2) Konfigurasikan akselerasi default:
![](https://main.qcloudimg.com/raw/2b72c25d2bf11f0c53a2e8286fcecf07.png)
**Origin server type** (Jenis server asal):Jenis default adalah **default origin server** (server asal default), tetapi jika Anda telah mengaktifkan situs web statis untuk bucket server asal dan ingin mempercepat pengiriman konten untuk situs web statis tersebut, pilih **static website origin server** (server asal situs web statis).
**Origin-Pull Authentication** (Autentikasi Tarik-Asal):Untuk bucket baca-publik, autentikasi tarik-asal tidak perlu diaktifkan.Untuk bucket baca-pribadi, autentikasi layanan CDN harus ditambahkan dan autentikasi tarik-asal harus diaktifkan secara manual.Untuk informasi selengkapnya, silakan lihat [Mengaktifkan Autentikasi Tarik-Asal](https://intl.cloud.tencent.com/document/product/436/31505).
**Otorisasi layanan CDN** (Otorisasi layanan CDN):Klik **Add CDN service authorization** (Tambahkan izin layanan CDN) untuk memilih dan memberikan akses CDN ke sumber daya pada bucket.
![](https://main.qcloudimg.com/raw/41e745800445225d042ef82c6febcc19.png)
(3) Setelah konfigurasi selesai, klik **Save** (Simpan) untuk mengaktifkan akselerasi CDN.
![](https://main.qcloudimg.com/raw/5ffc31cb49410b4685316e75860c9385.png)

> Untuk bucket baca-pribadi, jika autentikasi tarik-asal dan otorisasi layanan CDN diaktifkan, tanda tangan tidak diperlukan untuk akses ke server asal melalui CDN, dan sumber daya yang di-cache di CDN akan didistribusikan di jaringan publik, yang akan memengaruhi keamanan data.Karena itu, kami sarankan Anda mengaktifkan autentikasi CDN.
>
3.Aktifkan **custom acceleration domain name** (nama domain akselerasi khusus).
Anda dapat mengikatkan suatu nama domain khusus yang tersimpan ke bucket tersebut dan mengaktifkan akselerasi CDN.
> Maksimum 10 nama domain khusus dapat ditambahkan pada Konsol COS
>
(1) Klik **Add domain name** (Tambahkan nama domain) di modul **custom acceleration domain name** (nama domain akselerasi khusus) untuk menambahkan nama domain khusus yang tersimpan.
![](https://main.qcloudimg.com/raw/eda34cc24d82cebf109e3507a2ae142f.png)
(2) Konfigurasi untuk menambahkan nama domain:
**Domain Name** (Nama Domain):Masukkan nama domain khusus yang akan diikat (contohnya, `www.example.com`).Pastikan izin ICP untuk layanan di Tiongkok Daratan telah diperoleh dari MIIT untuk nama domain, dan CNAME yang sesuai telah dikonfigurasikan untuk nama domain tersebut di penyedia layanan DNS.Untuk informasi selengkapnya, silakan lihat [Konfigurasi CNAME](https://intl.cloud.tencent.com/document/product/228/3121).
**Origin-Pull Authentication** (Autentikasi Tarik-Asal): untuk bucket baca-pribadi, silakan aktifkan secara manual **origin-pull authentication** (autentikasi tarik-asal) untuk melindungi server asal.
Setelah konfigurasi selesai, klik **Save** (Simpan).
![](https://main.qcloudimg.com/raw/e21189d91929209ded554581d267a505.png)
> Untuk bucket baca-pribadi, jika autentikasi tarik-asal dan otorisasi layanan CDN diaktifkan, tanda tangan tidak diperlukan untuk akses ke server asal melalui CDN, dan sumber daya yang di-cache di CDN akan didistribusikan di jaringan publik, yang akan memengaruhi keamanan data.Karena itu, kami sarankan Anda mengaktifkan autentikasi CDN.
>
(3) Setelah konfigurasi disimpan, sakelar autentikasi CDN akan ditampilkan di kolom **CDN Authentication** (Autentikasi CDN).Anda dapat mengaktifkan secara manual autentikasi CDN untuk nama domain khusus.
**CDN Authentication** (Autentikasi CDN): Autentikasi label waktu dapat dikonfigurasikan untuk mencegah pencurian oleh pengguna yang berbahaya.Anda dapat mengaktifkan fitur ini setelah menambahkan nama domain.

Untuk informasi selengkapnya mengenai cara mengonfigurasi akselerasi CDN di Konsol COS, silakan lihat [Ikhtisar](https://intl.cloud.tencent.com/document/product/436/18424).
