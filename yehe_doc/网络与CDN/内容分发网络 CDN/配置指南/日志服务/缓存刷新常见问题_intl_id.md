### Apa itu pembersihan cache?
Pembersihan cache meliputi pembersihan URL, pembersihan direktori, dan pramuat URL. Untuk informasi selengkapnya, silakan lihat [Pembersihan Cache](https://intl.cloud.tencent.com/document/product/228/6299).
- Pembersihan URL berarti pembersihan cache file-demi-file.
- Pembersihan direktori berarti pembersihan semua file dalam suatu direktori file-demi-file.
- Pramuat URL berarti pramuat sumber daya file-demi-file.

Pembersihan vs. Pramuat:
- Setelah suatu sumber daya dibersihkan, cache-nya pada semua simpul CDN di seluruh jaringan akan dihapus. Jika suatu permintaan pengguna tiba di suatu simpul, simpul tersebut akan menarik sumber daya yang sesuai dari server asal, mengembalikannya ke pengguna tersebut, dan menyimpannya ke simpul tersebut untuk memastikan agar pengguna dapat memperoleh sumber daya terbaru.
- Jika suatu sumber daya dipramuat, sumber daya tersebut akan disimpan terlebih dahulu ke semua simpul CDN di seluruh jaringan. Jika suatu permintaan pengguna tiba di suatu simpul, sumber daya tersebut dapat langsung diperoleh pada simpul tersebut.


### Apa syarat pembersihan cache? Berapa lama pembersihan tersebut mulai diterapkan?
Pembersihan cache meliputi pembersihan URL, pembersihan direktori, dan pramuat URL.
- Pembersihan URL: maksimum 10.000 URL dapat dibersihkan setiap hari dan maksimum 1.000 URL dapat dikirimkan untuk setiap pembersihan. Diperlukan waktu sekitar 5 menit agar pembersihan berlaku. Jika periode validitas cache yang dikonfigurasikan untuk file tersebut kurang dari 5 menit, kami sarankan Anda menunggu waktu habis dan melakukan pembaruan daripada menggunakan alat pembersihan.
- Pembersihan direktori: maksimum 100 direktori dapat dibersihkan setiap hari dan maksimum 20 direktori URL dapat dikirimkan untuk setiap pembersihan. Diperlukan waktu sekitar 5 menit agar pembersihan berlaku. Jika periode validitas cache yang dikonfigurasikan untuk folder tersebut kurang dari 5 menit, kami sarankan Anda menunggu waktu habis dan melakukan pembaruan daripada menggunakan alat pembersihan.
- Pramuat URL: Jika sumber daya tersebut sudah di-cache ke simpul dan belum kedaluwarsa, sumber daya tersebut tidak akan diperbarui menjadi sumber daya terbaru. Jika Anda perlu memperbarui sumber daya pada semua simpul CDN menjadi sumber daya terbaru, Anda dapat membersihkannya sebelum melakukan pramuat. Maksimum 1.000 URL dapat dipramuat setiap hari dan maksimum 20 URL boleh dikirimkan untuk setiap pramuat. Diperlukan waktu sekitar 5 sampai 30 menit agar pramuat diterapkan, tergantung pada besarnya file.

### Apakah konten yang di-cache pada simpul cache CDN akan diperbarui secara real-time?
Tidak. Konten yang disimpan pada simpul cache CDN diperbarui berdasarkan [Konfigurasi Kedaluwarsa Cache](https://intl.cloud.tencent.com/document/product/228/35317) yang Anda konfigurasikan pada konsol. Jika Anda perlu memperbarui cache suatu file secara real-time, gunakan [Pembersihan Cache](https://intl.cloud.tencent.com/document/product/228/6299).

### Apakah CDN mendukung pembersihan direktori?
Ya. CDN mendukung pembersihan URL, pembersihan direktori, dan pramuat URL.
Metode 1: Anda dapat melakukan pembersihan direktori di [Konsol CDN](https://console.cloud.tencent.com/cdn/refresh). Untuk informasi selengkapnya, silakan lihat [Pembersihan Cache](https://intl.cloud.tencent.com/document/product/228/6299).
Metode 2: Pembersihan URL dengan memanggil [PembersihanCacheJalur](https://intl.cloud.tencent.com/document/product/228/33602) API.

### Bagaimana saya melihat riwayat pembersihan cache?
Anda dapat memeriksa riwayat pembersihan cache di Konsol CDN. Untuk informasi selengkapnya, silakan lihat **Operation Guide** (Panduan Pengoperasian) di [Pembersihan Cache](https://intl.cloud.tencent.com/document/product/228/6299#notes).

