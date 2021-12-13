### Apa yang harus saya lakukan jika sistem Windows gagal membuat citra kustom?

Jika sistem Windows gagal membuat citra kustom, Anda dapat memecahkan masalah sebagai berikut:
1. Pembuatan citra kustom bergantung pada Penginstal Modul Windows yang disediakan oleh Microsoft. Pastikan layanan ini berfungsi dengan baik.
2. Beberapa alat anti-virus atau Safedog dapat memblokir skrip pembuatan citra kustom agar tidak dijalankan. Agar tidak terjadi kegagalan pembuatan, sebaiknya Anda menonaktifkan alat ini sebelum membuat citra kustom.
3. Jika fitur pembuatan citra terganggu oleh pop-up sistem, login ke CVM dari jarak jauh lalu periksa dan sesuaikan konfigurasi CVM untuk memblokir pop-up.

### Apakah citra kustom bisa dibuat dari snapshot disk data?
Tidak. Citra kustom bisa dibuat dari snapshot disk sistem, tetapi tidak dari snapshot disk data.
Jika Anda perlu menyimpan data pada disk data instans asli saat meluncurkan instans baru, Anda dapat mengambil snapshot disk data terlebih dahulu, lalu menggunakan snapshot disk data ini untuk membuat disk data CBS yang baru. Untuk informasi selengkapnya, lihat [Membuat Disk Cloud menggunakan Snapshot](https://intl.cloud.tencent.com/document/product/362/5757).

### Bagaimana cara mengonfirmasi bahwa disk data sudah dilepas dan citra kustom dapat dibuat?
1. Konfirmasikan bahwa baris pernyataan partisi disk data yang dipasang secara otomatis telah dihapus dalam file `/etc/fstab`.
2. Jalankan perintah `mount` (pasang) untuk mengkueri informasi pemasangan semua perangkat. Pastikan bahwa hasil eksekusi tidak menyertakan informasi partisi disk data yang sesuai.

### Apakah citra kustom akan tetap ada setelah instans dirilis?
Ya.

### Bisakah saya mengubah sistem operasi instans yang dibuat dari citra kustom? Setelah saya mengubah sistem operasi, apakah saya masih bisa menggunakan citra kustom asli?
Ya. Anda dapat terus menggunakan citra kustom asli setelah mengubah sistem operasi.


### Bisakah saya meningkatkan CPU, memori, bandwidth, disk, dan konfigurasi lain pada instans CVM yang diaktifkan oleh citra kustom?
Ya. Anda dapat meningkatkan semuanya. Untuk informasi selengkapnya, lihat [Mengubah Konfigurasi Instans](https://intl.cloud.tencent.com/document/product/213/2178) dan [Menyesuaikan Konfigurasi Jaringan](https://intl.cloud.tencent.com/document/product/213/15517).

### Apakah citra kustom bisa digunakan di seluruh wilayah?
Tidak. Citra kustom hanya bisa digunakan di wilayah yang sama. Misalnya, Anda tidak dapat langsung meluncurkan instans CVM di Tiongkok Timur (Nanjing) menggunakan citra kustom yang dibuat dari instans CVM di Tiongkok Timur (Shanghai).
Untuk menggunakan citra kustom di seluruh wilayah, salin citra ke wilayah target terlebih dahulu. Untuk informasi selengkapnya, lihat [Menyalin Citra](https://intl.cloud.tencent.com/document/product/213/4943).

### Di mana saya dapat melihat perkembangan pembuatan citra? Berapa lama waktu yang dibutuhkan untuk membuat citra?
Anda dapat melihat perkembangan pembuatan citra di halaman **Images** (Citra) di Konsol CVM. Waktu yang diperlukan untuk membuat citra bergantung pada ukuran data instans.


