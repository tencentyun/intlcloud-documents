<span id="que1"></span>
### Bagaimana cara menambahkan nama domain ke CSS?

1. Login ke [CSS Console (Konsol CSS)](https://console.cloud.tencent.com/live), lalu masuk ke **Domain Management** (Manajemen Domain).
2. Tambahkan nama domain push atau pemutaran ulang Anda. Informasi selengkapnya dapat dilihat di [Adding Domain Name (Menambahkan Nama Domain)](https://intl.cloud.tencent.com/document/product/267/35970).
3. Konfigurasikan CNAME. Informasi selengkapnya dapat dilihat di [CNAME Configuration (Konfigurasi CNAME)](https://intl.cloud.tencent.com/document/product/267/31057).
4. Setelah konfigurasi berhasil, Anda dapat melakukan push dan pemutaran ulang dengan nama domain sendiri.

<span id="que2"></span>
### Mengapa setelah konfigurasi, CNAME masih ditampilkan sebagai belum dikonfigurasikan?

Setelah mengonfigurasikan CNAME sesuai dengan petunjuk di [CNAME Configuration (Konfigurasi CNAME)](https://intl.cloud.tencent.com/document/product/267/31057), harap tunggu karena penerapan konfigurasi memerlukan waktu 15‒30 menit. Selain itu, Anda dapat memeriksa berhasil atau tidaknya konfigurasi CNAME dengan mengikuti langkah-langkah di [Verifying the Effect of CNAME Record (Memverifikasi Efek Rekaman CNAME)](https://intl.cloud.tencent.com/document/product/267/31057).
>?
> - Resolusi DNS harus dilakukan melalui jaringan publik di Linux/macOS/Windows.
> - Jika konfigurasi CNAME tetap gagal, hubungi pendaftar nama domain Anda.

<span id="que3"></span>
### Bagaimana jika saya tidak menambahkan nama domain saya sendiri?
Jika mengaktifkan layanan CSS setelah tanggal 17 Oktober 2018, Anda harus menambahkan nama domain Anda untuk pemutaran ulang; jika tidak, Anda tidak dapat memutar ulang konten streaming langsung.

Jika Anda mengaktifkan layanan sebelum tanggal tersebut, CSS memberikan nama domain default untuk Anda, tetapi kami merekomendasikan agar Anda menggantinya dengan nama domain Anda sendiri. Tencent Cloud secara bertahap mulai menghentikan nama domain default sejak tanggal 31 Desember 2018.

> ! Nama domain default adalah nama domain sistem yang ditetapkan oleh CSS dalam format `bizid.liveplay.com`` dan `bizid.tlivecdn.com`.

<span id="que4"></span>
### Saya telah mengonfigurasikan beberapa item khusus untuk nama domain default. Apakah nama domain saya bisa diubah menjadi nama domain default?
Untuk menggunakan nama domain baru, hubungkan nama domain baru ke CSS dari awal. Sebaiknya Anda menambahkan dan mengonfigurasikan nama domain Anda sendiri di Konsol CSS.



