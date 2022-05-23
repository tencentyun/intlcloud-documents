
## Deskripsi Kesalahan
- Gejala 1: Anda menerima alarm tentang pembatasan lalu lintas keluar karena metrik lalu lintas keluar mencapai nilai maksimum yang diizinkan.
- Gejala 2: latensi respons meningkat.

## Kemungkinan Penyebab
Penyebabnya adalah sebagai berikut:
- Big key
- Konfigurasi instans tidak mencukupi

## Solusi
1. Sesuaikan bandwidth instans di konsol TencentDB for Redis untuk mengatasi masalah.
2. Periksa dan optimalkan big key dengan cara berikut:
 - Pisahkan big key.
 - Kurangi akses ke big key selama bisnis Anda tidak terpengaruh.
 - Hapus big key yang tidak berguna.
3. Jika masalah batas atas bandwidth tetap ada setelah pengoptimalan, tingkatkan instans untuk meningkatkan kemampuannya menangani lebih banyak lalu lintas. 

## Prosedur Pemecahan Masalah
### Langkah 1. Sesuaikan bandwidth
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans di daftar instans, dan masuk ke halaman detail instans.
2. Sesuaikan bandwidth di blok **Network Info**  (Info Jaringan) (bandwidth tambahan saat ini gratis).
>?
>- Meningkatkan bandwidth tidak berdampak pada bisnis Anda. Namun, jika bandwidth berkurang, lalu lintas yang melebihi bandwidth mungkin dibatasi.
>- Bandwidth standar: bandwidth per node (master atau replika) dalam instans.
>- Bandwidth replika Baca Saja: setiap replika baca-saja memiliki bandwidth yang sama dengan bandwidth master.
>- Bandwidth tambahan: jika bandwidth standar tidak dapat memenuhi kebutuhan Anda, Anda dapat menambahkan bandwidth tambahan.
>- Total bandwidth instans = bandwidth tambahan * jumlah shard + bandwidth standar * jumlah shard * jumlah replika. (Ada satu shard dalam arsitektur standar. Jika instans tidak memiliki replika, jumlah replika dalam rumus ini adalah satu.)
>
![](https://main.qcloudimg.com/raw/00c7d78cc03dabf405ffff8fbc40eae5.png)

### Langkah 2. Optimalkan big key
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans dalam daftar instans, dan masuk ke halaman manajemen instans.
2. Pada tab **System Monitoring** (Pemantauan Sistem), lihat bagan distribusi ukuran kunci dan optimalkan big key dengan cara berikut:
 - Pisahkan big keys.
 - Kurangi akses ke big key selama bisnis Anda tidak terpengaruh.
 - Hapus big key yang tidak berguna.

Jika masalah batas atas bandwidth tetap ada, lanjutkan ke [Langkah 3. Tingkatkan instans](#sjsl).

### Langkah 3. Tingkatkan instans](id:sjsl)
#### Meningkatkan instans Edisi Memori dalam arsitektur standar
>!
>- Setelah konfigurasi disesuaikan, instans akan dikenakan biaya konfigurasi baru.
>- Untuk memperluas kapasitas instans Edisi Memori dalam arsitektur standar, jika sisa kapasitas mesin fisik yang tersedia tidak mencukupi, migrasi akan terjadi, yang tidak akan memengaruhi akses Anda ke instans. Namun, jika instans menjalankan Redis 2.8, pemutusan kilat akan terjadi setelah migrasi selesai, jadi sebaiknya bisnis Anda memiliki mekanisme koneksi ulang.
>- Karena kapasitas maksimum instans Edisi Memori dalam arsitektur standar adalah 64 GB, Anda tidak dapat memperluas kapasitasnya hingga lebih dari 64 GB.

1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), cari instans yang diinginkan dalam daftar instans, dan pilih **Configure** (Konfigurasikan) > **Add Replica** (Tambahkan Replika) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/d4dbc95ee670595149c7609f03d8d92f.png)
2. Di kotak dialog pop-up, sesuaikan konfigurasi dan klik **OK** (OKE).
3. Kembali ke daftar instans. Setelah status instans berubah menjadi **Running** (Berjalan), instans dapat digunakan secara normal.

#### Meningkatkan instans Edisi Memori dalam arsitektur klaster
>!
>- Setelah konfigurasi disesuaikan, instans akan dikenakan biaya konfigurasi baru.
>- Saat shard ditambahkan, sistem akan menyeimbangkan konfigurasi slot secara otomatis dan memigrasikan data.
>- Selama perluasan dan pengurangan kapasitas, perintah pemblokiran seperti `BLPOP`, `BRPOP`, `BRPOPLPUSH`, dan `SUBSCRIBE` dapat mengalami kegagalan satu kali atau lebih (yang terkait dengan jumlah shard). Harap pertimbangkan dampaknya terhadap bisnis Anda sebelum memulai perluasan dan pengurangan kapasitas.
>

1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), cari instans yang diinginkan dalam daftar instans, dan pilih **Configure** (Konfigurasikan) > **Add Replica** (Tambahkan Replika) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/9c24103c52a67fbcd463e6f359ab0369.png)
2. Di kotak dialog pop-up, sesuaikan konfigurasi dan klik **OK** (OKE).
3. Kembali ke daftar instans. Setelah status instans berubah menjadi **Running** (Berjalan), instans dapat digunakan secara normal.

