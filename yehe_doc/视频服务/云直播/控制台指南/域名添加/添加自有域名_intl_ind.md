Untuk menggunakan CSS, Anda harus memiliki setidaknya dua nama domain: satu untuk nama domain push dan satu untuk nama domain pemutaran ulang. Push dan pemutaran ulang tidak dapat menggunakan nama domain yang sama.

## Prasyarat
Anda telah mengaktifkan layanan [CSS](https://cloud.tencent.com/product/css).


## Petunjuk
[](id:step1)
### Langkah 1. Tambahkan nama domain Anda
1. Login ke [konsol CSS](https://console.cloud.tencent.com/live) dan buka halaman **Domain Management** (Manajemen Domain).
2. Klik **Add Domain** (Tambahkan Domain) untuk masuk ke halaman penambahan nama domain dan konfigurasikan sebagai berikut:
    1. Untuk menambahkan **push domain**, masukkan nama domain, pilih jenis sebagai **Push Domain** (Domain Push), dan klik **Confirm** (Konfirmasi).
    2. Untuk menambahkan **domain pemutaran ulang**, masukkan nama domain, pilih jenis sebagai **Playback Domain** (Domain Pemutaran Ulang), pilih wilayah akselerasi (**Chinese mainland** (Tiongkok Daratan) secara default), dan klik **Confirm** (Konfirmasi).

![](https://qcloudimg.tencent-cloud.cn/raw/bde55a20b40da9d2d0fe2eda9613b63b.png)

>! 
>- Nama domain terdiri dari maksimum **45** karakter dan tidak boleh berisi huruf besar.
>- Secara default, setiap akun dapat menambahkan hingga 100 nama domain. Untuk menambahkan lebih banyak nama domain, Anda dapat [mengirimkan tiket](https://console.cloud.tencent.com/workorder/category) untuk mengajukan permohonan peningkatan batas atas.
>- Setelah berhasil menambahkan nama domain, Anda dapat masuk ke daftar manajemen nama domain dan mengeklik nama domain target atau **Manage** (Kelola) di sebelah kanan untuk masuk ke halaman detail nama domain. Kemudian, pilih **Advanced Configuration** (Konfigurasi Lanjutan), klik **Edit** di area **Region Configuration** (Konfigurasi Wilayah), pilih kembali wilayah akselerasi, dan klik **Save** (Simpan).

[](id:step2)
### Langkah 2. Konfigurasikan rekaman CNAME nama domain
Setelah nama domain Anda ditambahkan, sistem akan secara otomatis menetapkan CNAME dengan akhiran `.tlivecdn.com` ke nama domain tersebut. CNAME hanya dapat diakses setelah Anda mengonfigurasinya di penyedia layanan nama domain Anda. Anda dapat menggunakan layanan CSS setelah konfigurasi diterapkan. Petunjuk mendetail dapat dilihat di [Configuring CNAME for Domain Name (Mengonfigurasi CNAME untuk Nama Domain)](https://intl.cloud.tencent.com/document/product/267/31057).

>? Cara mengelola nama domain yang telah ditambahkan dapat dipelajari di [Domain Management (Manajemen Domain)](https://intl.cloud.tencent.com/document/product/267/31056).

## Pertanyaan Umum
- [Apa saja persyaratan untuk nama domain pemutaran ulang di CSS?](https://intl.cloud.tencent.com/document/product/267/7968)
- [Apakah saya bisa menggunakan nama domain yang sama untuk pemutaran ulang dan push? Apakah saya bisa menggunakan nama domain tingkat kedua?](https://intl.cloud.tencent.com/document/product/267/7968)
