## Kasus Penggunaan

Setelah Anda menghubungkan nama domain ke CDN Tencent Cloud, Anda dapat masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), lalu memilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri untuk melihat daftar nama domain akselerasi.

Anda dapat menyesuaikan kolom yang ditampilkan, mengaktifkan/menonaktifkan dalam batch pada layanan akselerasi untuk nama domain dan melakukan perubahan dalam batch pada proyek, tag, dan konfigurasi nama domain.

## Panduan Pengoperasian

### Menyesuaikan kolom yang ditampilkan

Klik ikon ![img](https://main.qcloudimg.com/raw/c8528c5a51cbea35ecb7e0414b51267e.png) di sebelah kanan bilah pencarian untuk melihat semua kolom yang tersedia.Pilih kolom yang ingin Anda tampilkan, batalkan kolom yang ingin Anda sembunyikan dan sesuaikan urutannya:
![img](https://main.qcloudimg.com/raw/790ae4b6c47b8b5ccd72e517701d34db.png)



### Mengekspor daftar konfigurasi

Klik ikon ![img](https://main.qcloudimg.com/raw/16b5654ecd298d7cadc63b243413a31d.png) di sebelah kanan bilah pencarian untuk mengekspor detail daftar nama domain dalam format file Excel.Anda dapat memilih hingga 1000 nama domain untuk diekspor dalam satu waktu.



### Mengubah proyek

Anda dapat mengubah proyek menjalankan nama domain.

- Mengubah proyek satu nama domain: di sebelah kanan nama domain target, klik **More** -> **Modify Project** (Lainnya -> Modifikasi Proyek).

- Mengubah proyek beberapa nama domain dalam batch: beri centang pada nama domain target dan klik **More Actions** -> **Edit Project** (Tindakan Lainnya -> Edit Proyek) di bagian atas.Anda dapat mengubah proyek hingga 50 nama domain sekaligus.




### Mengedit tag

- Mengubah tag satu nama domain: klik nama domain target untuk masuk ke halaman konfigurasinya, buka tab **Basic Configuration** (Konfigurasi Dasar), klik ikon pensil di sebelah kanan **Tag** di bagian **Basic Information** (Informasi Dasar).
- Mengubah tag dari beberapa nama domain dalam batch: beri centang pada nama domain target dan klik **More Actions** -> **Edit Tag** (Tindakan Lainnya -> Edit Tag) di bagian atas.Anda dapat mengubah tag hingga 50 nama domain sekaligus.Perubahan ini tidak langsung diterapkan, silakan segarkan untuk melihat tag baru.



### Menonaktifkan layanan akselerasi

Anda dapat menonaktifkan layanan akselerasi untuk nama domain yang berjalan normal.Setelah layanan akselerasi dinonaktifkan untuk nama domain, konfigurasinya akan dinonaktifkan pada simpul cache CDN di seluruh jaringan.Jika permintaan akses ke nama domain masih dialihkan ke simpul CDN, kesalahan 404 akan ditampilkan.Oleh karena itu, sebelum menonaktifkan nama domain, pastikan data CNAME-nya diselesaikan ke alamat CNAME non-CDN.

> !Penggunaan tidak akan dihasilkan lagi setelah layanan akselerasi dinonaktifkan sepenuhnya.

- Menonaktifkan layanan akselerasi untuk satu nama domain: di sebelah kanan nama domain target, klik **More** -> **Disable** (Lainnya -> Nonaktifkan).
- Menonaktifkan layanan akselerasi untuk beberapa nama domain dalam batch: beri centang pada nama domain yang diaktifkan dan klik **More Actions** -> **Disable Acceleration** (Tindakan Lainnya -> Nonaktifkan Akselerasi) di bagian atas.



### Mengaktifkan layanan akselerasi

Anda dapat mengaktifkan layanan akselerasi untuk nama domain yang dinonaktifkan untuk mendistribusikan konfigurasinya ke simpul cache di seluruh jaringan lagi.

- Mengaktifkan layanan akselerasi untuk satu nama domain: di sebelah kanan nama domain yang dinonaktifkan, klik **More** -> **Enable** (Lainnya -> Aktifkan).
- Mengaktifkan layanan akselerasi untuk beberapa nama domain dalam batch: beri centang pada nama domain yang dinonaktifkan dan klik **More Actions** -> **Enable Acceleration** (Tindakan Lainnya -> Aktifkan Akselerasi) di bagian atas.

> !Jika nama domain yang diaktifkan tidak memiliki operasi atau penggunaan selama 3 bulan, nama domain tersebut akan dianggap tidak aktif dan CDN akan menonaktifkan layanan akselerasinya secara otomatis.



### Menghapus nama domain akselerasi

Jika nama domain berada dalam status **Disabled** (Nonaktif), Anda dapat menghapusnya.Setelah dihapus, konfigurasinya akan dihapus dan tidak dapat dipulihkan, dan data statistiknya tidak dapat dilihat lagi.Harap operasikan dengan hati-hati.

- Menghapus satu nama domain: di sebelah kanan nama domain target, klik **More**-> **Delete** (Lainnya -> Hapus).
- Menghapus beberapa nama domain dalam batch: beri centang pada nama domain yang dinonaktifkan dan klik **More Actions** -> **Delete** (Tindakan Lainnya -> Hapus) di bagian atas.



### Mengubah konfigurasi dalam batch

Fitur Batch Change Configuration (Ubah Konfigurasi Dalam Batch) memungkinkan Anda untuk mengubah item konfigurasi dari beberapa nama domain secara bersamaan.Untuk informasi selengkapnya, silakan lihat [Mengubah Konfigurasi Dalam Batch](https://intl.cloud.tencent.com/document/product/228/39911).




### Menyalin konfigurasi

Fitur Copy Configuration (Salin Konfigurasi) memungkinkan Anda membuat duplikat konfigurasi nama domain akselerasi yang ada ke satu atau beberapa nama domain akselerasi yang baru.Untuk informasi selengkapnya, silakan lihat [Menyalin Konfigurasi](https://intl.cloud.tencent.com/document/product/228/38936).






