TencentDB for SQL Server mendukung penyesuaian cepat dari arsitektur, versi, dan spesifikasi instans dan memungkinkan operasi penskalaan yang fleksibel di konsol. Anda dapat menyesuaikan konfigurasi instans secara elastis sesuai dengan kondisi bisnis Anda yang sebenarnya (pada tahap awal, pada tahap pengembangan yang cepat, selama jam sibuk, atau selama jam normal), untuk memenuhi kebutuhan Anda dengan lebih baik seperti pemanfaatan sumber daya secara penuh dan optimalisasi biaya real-time.

## Prasyarat
Anda dapat menyesuaikan konfigurasi instans TencentDB for SQL Server dan instansnya yang terkait hanya jika mereka dalam status normal (Berjalan) dan tidak menjalankan tugas apa pun.

## Item Penyesuaian
| Item Penyesuaian | Deskripsi |
|---------|---------|
| Arsitektur | a. Edisi Ketersediaan Tinggi dapat ditingkatkan ke Edisi Kluster. <br>b. Edisi Dasar tidak dapat ditingkatkan ke Edisi Ketersediaan Tinggi/Edisi Kluster. Jika perlu, Anda dapat membeli instans Edisi Ketersediaan Tinggi/Edisi Kluster baru dan [memigrasikan data dengan DTS](https://intl.cloud.tencent.com/document/product/238/39006). |
| Versi | a. Edisi Ketersediaan Tinggi mendukung peningkatan versi. <br>b. Untuk meningkatkan versi instans Edisi Ketersediaan Tinggi/Edisi Kluster yang terkait dengan instans baca saja, [kirim tiket](https://console.cloud.tencent.com/workorder/category). |
| Spesifikasi instans | a. Semua jenis instans mendukung peningkatan dan penurunan spesifikasi. <br>b. Batas atas kapasitas disk di bawah spesifikasi yang sesuai adalah seperti yang ditampilkan pada halaman **Adjust Configuration** (Sesuaikan Konfigurasi) di konsol. |
| Kapasitas disk | a. Instans Edisi Ketersediaan Tinggi/Edisi Kluster mendukung perluasan/pengurangan kapasitas disk.<br/>b. Instans Edisi Dasar mendukung perluasan kapasitas disk tetapi tidak pengurangan. |

>?Jika Anda perlu menskalakan kemampuan baca database secara horizontal, gunakan instans baca saja untuk mengurangi tekanan pada instans utama seperti yang diinstruksikan di [Mengelola Instans Baca Saja](https://intl.cloud.tencent.com/document/product/238/43143).

## Pembatasan Peningkatan/Penurunan
| Jenis Instans | Peningkatan Versi | Peningkatan Arsitektur | Peningkatan Spesifikasi | Perluasan Kapasitas Disk | Penurunan Versi | Penurunan Arsitektur | Penurunan Spesifikasi | Pengurangan Kapasitas Disk |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
| Instans Edisi Dasar | X | X |   &#10003; |  &#10003; | X  | X  |  &#10003;  | X  |
| Instans Edisi Ketersediaan Tinggi |  &#10003; |  &#10003; |  &#10003; |  &#10003; | X  | X  |  &#10003;  |  &#10003;  |
| Instans Edisi Kluster | X | X |   &#10003; |   &#10003; | X  | X  |  &#10003;  | &#10003;  |
| Instans Baca Saja | X| X |   &#10003; |  &#10003; | X  | X  |  &#10003;  |  &#10003;  |
| Instans Edisi Ketersediaan Tinggi/Edisi Kluster dengan instans baca saja | Kirim tiket | Kirim tiket |  Kirim tiket |  Kirim tiker | X  | X  | Kirim tiket  |  Kirim tiket |

## Deskripsi Ruang Disk Instans
- Untuk memastikan kelangsungan bisnis, tingkatkan spesifikasi instans Anda atau beli kapasitas disk tambahan tepat waktu sebelum kapasitas disk habis.
- Jika ukuran data yang disimpan dalam instans Edisi Ketersediaan Tinggi/Edisi Kluster melebihi kapasitas disknya, fitur seperti impor database dan pengembalian akan menjadi tidak tersedia. Anda perlu memperluas kapasitasnya atau menghapus beberapa tabel database di konsol untuk mengosongkan ruang penyimpanan.
- Jika ukuran data yang disimpan dalam instans Edisi Dasar melebihi kapasitas disknya, database akan menjadi baca saja. Anda perlu memperluas kapasitasnya atau menghapus beberapa tabel database di konsol untuk mengosongkan ruang penyimpanan dan membuatnya dapat ditulis.

## Aturan Penyesuaian Konfigurasi
- Anda tidak dapat membatalkan operasi penyesuaian konfigurasi yang sedang berlangsung.
- Nama, IP akses, dan port akses instans tetap tidak berubah setelah penyesuaian konfigurasi.
- Migrasi data mungkin terlibat dalam penyesuaian konfigurasi. Selama migrasi data, instans TencentDB for SQL Server dapat diakses secara normal dan bisnis tidak akan terpengaruh.
- Peralihan instans mungkin terlibat setelah penyesuaian konfigurasi selesai (yaitu, instans SQL Server mungkin terputus selama beberapa detik). Sebaiknya konfigurasi fitur koneksi ulang otomatis untuk aplikasi Anda. Peralihan instans akan dilakukan selama waktu pemeliharaan instans. Untuk informasi selengkapnya, lihat [Mengatur Informasi Pemeliharaan Instans](https://intl.cloud.tencent.com/document/product/238/35785).

## Catatan
Karena instans Edisi Dasar hanya memiliki satu node database dan tidak ada node sekunder sebagai cadangan panas, saat node gagal atau melakukan tugas seperti penyesuaian konfigurasi dan peningkatan versi, node tersebut tidak akan tersedia dalam waktu yang lama. Jika bisnis Anda memiliki persyaratan tinggi untuk ketersediaan database, sebaiknya gunakan Edisi Ketersediaan Tinggi atau Edisi Kluster, bukan Edisi Dasar.

#### Aturan Penagihan
Untuk informasi selengkapnya, lihat [Deskripsi Biaya Penyesuaian Instans](https://intl.cloud.tencent.com/document/product/238/35799).

## Petunjuk
- [Menyesuaikan Instans Arsitektur](https://intl.cloud.tencent.com/document/product/238/44353)
- [Menyesuaikan Versi Instans](https://intl.cloud.tencent.com/document/product/238/44354)
- [Menyesuaikan Spesifikasi Instans](https://intl.cloud.tencent.com/document/product/238/35783)
