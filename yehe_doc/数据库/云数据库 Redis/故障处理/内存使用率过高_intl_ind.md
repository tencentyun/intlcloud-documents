
## Deskripsi Kesalahan
- Gejala 1: Anda menerima alarm tentang penggunaan memori yang terlalu tinggi.
- Gejala 2: nilai metrik penggunaan memori tinggi.
- Gejala 3: lebih banyak kunci yang dihapus dan latensi respons meningkat.

## Kemungkinan Alasan
- Bisnis Anda membutuhkan pengoptimalan.
- Memori saat ini tidak dapat memenuhi persyaratan bisnis Anda.

## Solusi
- Analisis penyebab penggunaan memori yang tinggi dan atasi masalah yang sesuai.
- Perluas kapasitas instans di konsol jika masalah terus berlanjut.

## Prosedur Pemecahan Masalah
### Memperluas kapasitas instans Edisi Memori dalam arsitektur standar
>!
>- Setelah konfigurasi disesuaikan, instans akan dikenakan biaya konfigurasi baru.
>- Untuk memperluas kapasitas instans Edisi Memori dalam arsitektur standar, jika sisa kapasitas mesin fisik yang tersedia tidak mencukupi, migrasi akan terjadi, yang tidak akan memengaruhi akses Anda ke instans. Namun, jika instans menjalankan Redis 2.8, pemutusan kilat akan terjadi setelah migrasi selesai, jadi sebaiknya bisnis Anda memiliki mekanisme koneksi ulang.
>- Karena kapasitas maksimum instans Edisi Memori dalam arsitektur standar adalah 64 GB, Anda tidak dapat memperluas kapasitasnya hingga lebih dari 64 GB.

1. Login ke [konsol TencentDB for Redis]](https://console.cloud.tencent.com/redis), temukan instans yang diinginkan dalam daftar instans, dan pilih **Configure** (Konfigurasikan) > **Expand Node** (Perluas Node) di kolom **Operation** (Operasi).
2. Di kotak dialog pop-up, sesuaikan konfigurasi dan klik **OK** (OKE).
3. Kembali ke daftar instans. Setelah status instans berubah menjadi **Running** (Berjalan), instans dapat digunakan secara normal.

### Memperluas kapasitas instans Edisi Memori dalam arsitektur klaster
>!
>- Setelah konfigurasi disesuaikan, instans akan dikenakan biaya konfigurasi baru.
>- Saat shard ditambahkan, sistem akan menyeimbangkan secara otomatis konfigurasi slot dan memigrasikan data.
>- Selama perluasan dan pengurangan kapasitas, perintah pemblokiran seperti `BLPOP`, `BRPOP`, `BRPOPLPUSH`, dan `SUBSCRIBE` dapat mengalami kegagalan satu kali atau lebih (yang terkait dengan jumlah shard). Harap mempertimbangkan dampaknya terhadap bisnis Anda sebelum memulai perluasan dan pengurangan kapasitas.
>

1. Login ke [konsol TencentDB for Redis]](https://console.cloud.tencent.com/redis), cari instans yang diinginkan dalam daftar instans, dan pilih **Configure** (Konfigurasikan) > **Add Shard** (Tambahkan Shard) atau **Expand Node** (Perluas Node) di kolom **Operation** (Operasi).
2. Di kotak dialog pop-up, sesuaikan konfigurasi dan klik **OK** (OKE).
3. Kembali ke daftar instans. Setelah status instans berubah menjadi **Running** (Berjalan), instans dapat digunakan secara normal.


>?Jika masalah ini berlanjut, silakan [kirim tiket](https://console.intl.cloud.tencent.com/workorder/category).
