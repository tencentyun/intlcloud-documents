
## Ikhtisar
Dokumen ini menjelaskan cara meningkatkan mesin TencentDB for MySQL di konsol.
TencentDB for MySQL mendukung peningkatan mesin database:
- Dari MySQL 5.5 ke MySQL 5.6
- Dari MySQL 5.6 ke MySQL 5.7

>?
>- Penurunan mesin database tidak didukung.
>- Peningkatan di seluruh rilis utama tidak didukung. Misalnya, untuk meningkatkan instans TencentDB for MySQL 5.5 ke MySQL 5.7 atau yang lebih baru, Anda harus meningkatkannya ke MySQL 5.6 terlebih dahulu.
>- Saat ini, MySQL 5.7 tidak dapat ditingkatkan ke MySQL 8.0. 
<span id ="shengjiguize"></span>
## Aturan Peningkatan
- Sintaksis `create table …  as select …` tidak didukung.
- Sinkronisasi sumber-replika di TencentDB for MySQL 5.6 dan 5.7 diimplementasikan berdasarkan GTID. Hanya InnoDB yang didukung secara default.
- Tabel MyISAM akan diubah menjadi tabel InnoDB selama proses peningkatan dari MySQL 5.5 ke 5.6. **We recommend that you complete the conversion first before upgrading.** (Kami menyarankan Anda menyelesaikan konversi terlebih dahulu sebelum meningkatkan versi.)
- Selama peningkatan, TencentDB for MySQL akan menghapus tabel `slow_log`. Harap simpan log sebelum meningkatkan jika perlu.
- **If an instance to be upgraded is associated with other instances (e.g., the source instance and read-only replicas), these instances will be upgraded together to ensure data consistency.** (Jika instans yang akan ditingkatkan dikaitkan dengan instans lain (mis., instans sumber dan replika baca saja), instans ini akan ditingkatkan bersama untuk memastikan konsistensi data.)
- Peningkatan TencentDB for MySQL melibatkan migrasi data dan umumnya membutuhkan waktu yang relatif lama. Harap menunggu dengan sabar. Selama proses peningkatan, bisnis Anda tidak akan terpengaruh dan instans dapat diakses seperti biasa.
- Peralihan instans mungkin diperlukan setelah peningkatan versi selesai (yaitu, instans MySQL mungkin terputus selama beberapa detik). Kami menyarankan agar aplikasi dikonfigurasi dengan fitur rekoneksi otomatis dan peralihan instans dilakukan selama jendela pemeliharaan instans. Untuk informasi selengkapnya, lihat [Mengatur Jendela Pemeliharaan Instans](https://intl.cloud.tencent.com/document/product/236/10929).
- Jika jumlah tabel dalam satu instans melebihi satu juta, peningkatan mungkin gagal dan pemantauan database mungkin terpengaruh. Harap pastikan jumlah tabel dalam satu instans tidak lebih dari satu juta.

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/), cari instans yang diinginkan dalam daftar instans, dan pilih **More** (Lainnya) > **Upgrade Version** (Tingkatkan Versi) di kolom **Operation** (Operasi).
>?MySQL 8.0 tidak dapat ditingkatkan ke versi yang lebih baru.
>
2. Di jendela pop-up, pilih versi database yang akan ditingkatkan dan klik **Upgrade** (Tingkatkan).
Karena peningkatan database melibatkan migrasi data, setelah peningkatan selesai, maka dapat terjadi pemutusan hubungan yang sangat singkat dari database MySQL yang berlangsung hanya beberapa detik. Saat peningkatan dimulai, **Switch Time** (Waktu Peralihan) dapat dipilih sebagai **During maintenance time** (Selama waktu pemeliharaan), sehingga peralihan akan dimulai dalam **maintenance window** (jendela pemeliharaan) berikutnya setelah peningkatan instans selesai.
>!Jika Anda memilih **During maintenance time** (Selama waktu pemeliharaan), peralihan tidak akan terjadi segera setelah peningkatan spesifikasi database selesai; sebagai gantinya, sinkronisasi akan berlanjut hingga instans memasuki **maintenance window** (jendela pemeliharaan) berikutnya saat peralihan akan dilakukan. Dengan cara ini, keseluruhan waktu yang diperlukan untuk meningkatkan instans dapat diperpanjang.
>
![](https://qcloudimg.tencent-cloud.cn/raw/5fd7b83457ffb0cab80112ad32e8e0be.png)

## Pertanyaan Umum
#### Akankah TencentDB for MySQL secara otomatis mencadangkan data sebelum meningkatkan?
TencentDB for MySQL mengadopsi mekanisme pencadangan panas server ganda real-time harian yang mendukung pemulihan data tanpa kehilangan dari 7–732 hari terakhir berdasarkan pencadangan data dan pencadangan log (binlog).

#### Bisakah TencentDB for MySQL diturunkan dari MySQL 5.7 ke MySQL 5.6?
Tidak. Penurunan versi mesin database tidak didukung. Untuk menggunakan instans MySQL 5.6, Anda harus menghentikan atau mengembalikan instans MySQL 5.7 yang ada, lalu membeli instans MySQL 5.6.

#### Apakah akan ada penundaan sumber-replika selama peningkatan?
Peningkatan instans sumber memerlukan perbandingan data dan dapat menyebabkan penundaan replika sumber.

#### Apakah instans akan beralih setelah peningkatan versi mesin database memengaruhi instans TencentDB for MySQL saya?
Peningkatan tidak akan memengaruhi bisnis Anda, tetapi instans TencentDB for MySQL mungkin terputus selama beberapa detik. Kami menyarankan agar aplikasi dikonfigurasi dengan fitur rekoneksi otomatis dan peralihan instans dilakukan selama jendela pemeliharaan instans.

#### Berapa lama waktu yang dibutuhkan untuk meningkatkan versi mesin database dari instans TencentDB for MySQL? Bagaimana cara memeriksa kemajuan peningkatan?
Durasi peningkatan bergantung pada jumlah data dalam instans, kecepatan replikasi data, dll.
Peningkatan TencentDB for MySQL melibatkan migrasi data dan umumnya membutuhkan waktu yang relatif lama. Harap menunggu dengan sabar. Bisnis Anda tidak akan terpengaruh selama proses peningkatan dan dapat diakses secara normal.

#### Mengapa instans selalu dalam status "Waiting for switch" (Menunggu peralihan)?
Ini mungkin karena Anda memilih **During maintenance time** (Selama waktu pemeliharaan) sebagai **Switch Time** (Waktu Peralihan), dan peralihan akan dimulai dalam jendela pemeliharaan berikutnya setelah peningkatan versi instans selesai.
Untuk segera mengalihkan instans, klik **Switch Now** (Alihkan Sekarang) di kolom **Operation** (Operasi) di daftar instans. Koneksi mungkin terputus selama peralihan. Pastikan bahwa database memiliki mekanisme koneksi ulang.
