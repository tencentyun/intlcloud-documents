
## Ikhtisar
Instans Edisi Kluster TencentDB for Redis yang lama (dibeli sebelum 1 Januari 2018) menggunakan versi dan arsitektur yang lebih lama, yang dapat menimbulkan risiko terhadap stabilitas instans. Kami sarankan Anda memigrasikan data mereka ke Edisi Memori 4.0 TencentDB for Redis (arsitektur standar atau kluster).
TencentDB for Redis 4.0 hadir dengan konfigurasi yang lebih fleksibel, kinerja yang lebih tinggi, dan fitur yang lebih komprehensif. Dokumen ini menjelaskan cara memigrasikan data dari instans lama Anda ke instans Edisi Memori 4.0 TencentDB for Redis (arsitektur [standar](https://intl.cloud.tencent.com/document/product/239/31959) atau [kluster](https://intl.cloud.tencent.com/document/product/239/18336)).

>!Untuk menghindari kehilangan data, Anda harus berhenti menulis ke instans lama Anda sebelum memigrasikan datanya ke instans Edisi Memori TencentDB for Redis (arsitektur standar atau kluster), karena hot migration tidak didukung dalam kasus ini.
Anda dapat mengonfigurasi grup keamanan atau mengatur ulang kata sandi untuk memblokir semua permintaan akses. Anda dapat memeriksa QPS di halaman pemantauan: jika nol, berarti semua permintaan akses berhasil diblokir.

## Prasyarat
- Anda telah membeli instans Edisi Memori TencentDB for Redis (arsitektur standar atau kluster).
>?Jika data Anda saat ini kurang dari 12 GB dengan data tambahan yang diharapkan tidak lebih dari 60 GB dan QPS tidak lebih dari 40.000, atau Anda perlu menggunakan perintah transaksi, disarankan Edisi Memori 4.0 TencentDB for Redis (arsitektur standar); jika tidak, Edisi Memori 4.0 TencentDB for Redis (arsitektur kluster) adalah pilihan terbaik Anda. Arsitektur kluster kompatibel dengan semua perintah dari instans lama, kecuali jika tidak mendukung perintah transaksi.
- Anda memiliki instans CVM yang siap untuk mengimpor data, yang harus memiliki kapasitas disk yang cukup untuk mengakomodasi data yang ada.
- Alat impor data, redis-port, telah diinstal. Untuk informasi selengkapnya tentang penggunaan alat dan alamat unduhan, lihat [Migrasi dengan port ulang](https://intl.cloud.tencent.com/document/product/239/31940).

## Petunjuk
1. Berhenti menulis ke instans Edisi Kluster Redis yang lama.
2. Cadangkan datanya di konsol TencentDB for Redis. Waktu pencadangan yang dibutuhkan bergantung pada jumlah data. Setelah pencadangan selesai, file RDB akan dibuat.
3. Setelah pencadangan selesai, Anda dapat melihat file cadangan dalam daftar cadangan. Klik **Export** (Ekspor) untuk membuat file RDB dengan tautan unduhan, salin tautan, dan gunakan untuk mengunduh file cadangan dari instans CVM melalui jaringan pribadi. Unduhan Lintas-AZ tidak didukung.
4. Inisialisasi kata sandi instans Edisi Memori 4.0 TencentDB for Redis (arsitektur standar atau kluster) yang baru dibeli, dan gunakan port ulang untuk mengimpor file RDB ke dalamnya.
```
./redis-restore dump.rdb -t 127.0.0.1:6379
```
5. Setelah impor data selesai, periksa apakah berhasil dengan melihat penggunaan memori di blok **Specs Info** (Info Spesifikasi) pada halaman detail instans.
6. Migrasikan aplikasi Anda ke instans baru dengan mengganti IP instans lama dalam kode dengan instans baru.

