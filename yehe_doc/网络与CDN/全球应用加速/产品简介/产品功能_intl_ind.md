Fitur utama GAAP termasuk konfigurasi proksi akselerasi, manajemen server asal, pengumpulan statistik akselerasi, pemantauan koneksi, dan akuisisi IP pengguna nyata.
## Proksi Akselerasi
- GAAP mendukung konfigurasi koneksi akselerasi berdasarkan wilayah pengguna target dan wilayah server asal. Ini akan secara otomatis memilih koneksi yang paling tepat berdasarkan wilayah pengguna target dan wilayah server asal untuk mencapai jalur terpendek dan optimal dari pengguna ke server asal, memberikan pengalaman akses yang lebih lancar. Untuk informasi selengkapnya, lihat [Manajemen Akses](https://intl.cloud.tencent.com/document/product/608/13765).
- Penerusan TCP dan UDP didukung.
- Penerusan aturan URL didukung untuk HTTP dan HTTPS.
- Satu pendengar dapat ditautkan ke beberapa server asal, dan satu koneksi dapat membuat beberapa pendengar.
- Konfigurasi dan modifikasi aturan penerusan didukung dan ini berlaku secara real-time dan tidak memengaruhi bisnis online.
- Konfigurasi fleksibel aturan penerusan akselerasi dalam koneksi memenuhi skenario yang memerlukan verifikasi uji beta secara langkah demi langkah. Untuk informasi selengkapnya tentang konfigurasi, lihat [Manajemen Pendengar](https://intl.cloud.tencent.com/document/product/608/13764).

## Manajemen Server Asal
- GAAP dapat mengelola sejumlah besar server asal yang jenisnya adalah IP dan nama domain, dan menambahkannya dalam batch.

## Kumpulan Statistik
- GAAP dapat mengumpulkan statistik koneksi akselerasi seperti bandwidth, kebersamaan, kehilangan paket, penundaan, dan volume penerusan paket. Berdasarkan statistik, Anda dapat secara fleksibel menyesuaikan batas kapasitas koneksi akselerasi sesuai kebutuhan. Untuk informasi selengkapnya, lihat [Statistik](https://intl.cloud.tencent.com/document/product/608/14425).

## Pemantauan Koneksi
- GAAP mendukung koneksi pemantauan dan status server asal. Ini segera memberi tahu Anda tentang masalah koneksi atau server asal untuk pemecahan masalah yang lebih mudah dan lebih cepat. Untuk informasi selengkapnya, lihat [Akses Pemantauan Cloud](https://intl.cloud.tencent.com/document/product/608/17541).

## Mendapatkan IP pengguna nyata
- GAAP mendukung modul TOA untuk mendapatkan IP pengguna nyata, memastikan passthrough IP yang efektif untuk tujuan analisis data. Untuk informasi selengkapnya, harap lihat [Mendapatkan IP Nyata Akses Pengguna](https://intl.cloud.tencent.com/document/product/608/14429).
