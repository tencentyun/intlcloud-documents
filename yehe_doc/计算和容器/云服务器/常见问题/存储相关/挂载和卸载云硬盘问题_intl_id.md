### Apa itu nama perangkat (titik pemasangan)?
Nama perangkat (titik pemasangan) adalah lokasi disk cloud yang dipasang ke instans CVM pada bus pengontrol disk. Nama perangkat yang dipilih cocok dengan nomor perangkat disk di Linux dan cocok dengan nomor urut disk manajer disk di Windows.

### Apakah saya bisa memasang satu disk cloud ke beberapa instans CVM?
Tidak. Anda dapat memasang maksimal 20 disk cloud ke CVM yang sama, tetapi Anda tidak dapat memasang disk cloud yang sama ke beberapa CVM. Anda hanya bisa berbagi data dengan [melepas disk cloud](https://intl.cloud.tencent.com/document/product/362/32400) dari CVM A lalu [memasangnya](https://intl.cloud.tencent.com/document/product/362/32401) ke CVM B.

### Apakah saya perlu mempartisi disk cloud setelah membeli dan memasangnya ke instans CVM?
Ya. Setelah membeli disk cloud, Anda harus memasangnya ke instans CVM di zona ketersediaan yang sama, lalu menginisialisasinya dengan memformat, mempartisi, dan membuat sistem file sebelum menggunakannya sebagai disk data. Untuk informasi selengkapnya, lihat [Memasang Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31645) dan [Menginisialisasi Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31645).

### Mengapa saya tidak bisa menemukan disk data yang saya beli untuk instans Linux?
Jika Anda membeli disk data secara terpisah, Anda harus mempartisi, memformat, dan memasangnya ke instans untuk dapat melihat dan menggunakan ruang penyimpanannya. Untuk informasi selengkapnya, lihat [Memasang Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31645) dan [Menginisialisasi Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31645).

### Berapa banyak disk cloud yang dapat dipasang ke satu instans CVM?
Maksimal 20 disk data dapat dipasang ke satu instans CVM.

### Mengapa saya tidak bisa menemukan CVM tempat saya ingin memasang disk cloud?
Pastikan instans CVM belum dirilis dan pastikan instans tersebut berada di wilayah dan zona ketersediaan yang sama dengan tempat disk cloud berada.

### Apakah saya bisa memasang disk cloud ke instans CVM di zona ketersediaan lain?
Tidak. Cloud disk hanya bisa dipasang atau dilepas dari instans CVM di zona ketersediaan yang sama dengan tempat disk cloud berada.

### Saat saya melepas disk cloud (disk data), apakah datanya akan hilang?
Data di disk cloud tidak akan diubah selama pemasangan atau pelepasan. Untuk memastikan konsistensi data, sebaiknya ikuti langkah-langkah di bawah ini:
- Di Windows, sebaiknya Anda menghentikan semua operasi baca dan tulis di semua sistem file disk cloud untuk memastikan integritas data. Jika tidak, data yang belum selesai dibaca atau ditulis akan hilang.
- Di Linux, masuk ke instans CVM dan jalankan perintah `umount` (lepaskan) pada disk cloud. Setelah perintah dijalankan, masuk ke Konsol CVM untuk melepas disk cloud.

### Bagaimana cara melepas disk cloud?
Untuk informasi selengkapnya, lihat [Melepas Disk Cloud](https://intl.cloud.tencent.com/document/product/362/32400).

### Apakah disk cloud bisa dipasang dan dilepas?
- Disk cloud dapat dipasang dan dilepas.
- Disk sistem tidak dapat dipasang atau dilepas.

### Apakah disk cloud bisa dipasang dan dilepas secara berkelompok?
- Disk cloud dapat dipasang dan dilepas secara berkelompok.
- Disk sistem tidak dapat dipasang atau dilepas.

### Apakah disk sistem bisa dilepas?
Tidak.


