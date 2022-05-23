
## Deskripsi Kesalahan
- Gejala 1: Anda menerima alarm tentang penggunaan CPU yang tinggi.
- Gejala 2: nilai metrik penggunaan CPU tinggi.
- Gejala 3: throughput keseluruhan menjadi lebih rendah dan respons menjadi lebih lambat.

## Kemungkinan Alasan
- Perintah dengan kompleksitas waktu yang tinggi
- Beban tinggi, seperti akses yang sering ke hot key
- Koneksi yang sering dibuat
- Akses tidak biasa

## Solusi
1. [Optimalkan bisnis Anda](#ywyh)
 1. Buka tab **System Monitoring** (Pemantauan Sistem) di konsol TencentDB for Redis untuk memeriksa apakah QPS (Kueri per Detik) tinggi dan apakah ada hot key yang tidak terduga.
 2. Optimalkan logika bisnis Anda setelah memecahkan masalah akses tidak biasa. Misalnya, optimalkan perintah dengan kompleksitas waktu yang tinggi, hot key, dan koneksi nonpersisten. Jika masalah berlanjut, tingkatkan instans.

2. [Tingkatkan instans](#slsj)
 - Jika beban baca berat, Anda dapat menambahkan replika untuk membagikan beban baca. Pastikan bahwa bisnis Anda mengizinkan data yang tidak konsisten sebelum mengaktifkan pemisahan baca/tulis, karena setelah diaktifkan, data yang tidak konsisten dapat dibaca dari node replika dan node master (node replika tertinggal di belakang node master).
 - Jika beban tulis berat, Anda dapat meningkatkan instans dari arsitektur standar ke arsitektur klaster untuk meningkatkan daya pemrosesan CPU. Sebelum peningkatan, Anda perlu memeriksa kompatibilitasnya. Untuk informasi selengkapnya, lihat [Memeriksa Migrasi dari Arsitektur Standar ke Arsitektur Klaster](https://intl.cloud.tencent.com/document/product/239/37594).

## Prosedur Pemecahan Masalah
### [Mengoptimalkan bisnis Anda](id:ywyh)
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pada tab **System Monitoring** (Pemantauan Sistem), periksa apakah QPS tinggi atau ada hot key yang tidak terduga.
3. Setelah memecahkan masalah akses tidak biasa, optimalkan logika bisnis Anda:
 - Hot key: Anda dapat membagi hot key dari struktur data yang kompleks menjadi beberapa kunci baru dan mendistribusikannya ke seluruh node Redis untuk mengurangi tekanan. Misalnya, jika hot key hash dua tingkat memiliki banyak elemen hash, Anda dapat membaginya.
 - Big key: jika nilainya terlalu besar, Anda dapat membagi objek menjadi beberapa nilai kunci sehingga beberapa node Redis akan berbagi tekanan. Jika ada terlalu banyak kunci, Anda dapat menyimpan beberapa kunci dalam struktur hash.

### [Tingkatkan instans](id:slsj)
#### Beban baca berat
[Tambahkan replika](#zjfb) dan aktifkan [pemisahan baca/tulis](https://intl.cloud.tencent.com/document/product/239/31935)untuk berbagi beban baca.
>!Pastikan bahwa bisnis Anda mengizinkan data yang tidak konsisten sebelum mengaktifkan pemisahan baca/tulis, karena setelah diaktifkan, data yang tidak konsisten dapat dibaca dari node replika dan node master (node replika tertinggal di belakang node master). Untuk informasi selengkapnya, lihat [Mengubah Spesifikasi Instans](https://intl.cloud.tencent.com/document/product/239/31934).

[](id:zjfb)
1. Login ke [konsol TencentDB for Redis]](https://console.cloud.tencent.com/redis), cari instans yang diinginkan dalam daftar instans, dan pilih **Configure** (Konfigurasikan) > **Add Replica** (Tambahkan Replika) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/53a2005cd6050ee2bbcdb32b4b64e48d.png)
2. Di kotak dialog pop-up, sesuaikan konfigurasi dan klik **OK** (OKE).
3. Kembali ke daftar instans. Setelah status instans berubah menjadi **Running** (Berjalan), instans dapat digunakan secara normal.

#### Beban tulis berat
- **Arsitektur klaster**
1. Login ke [konsol TencentDB for Redis]](https://console.cloud.tencent.com/redis), cari instans yang diinginkan dalam daftar instans, dan pilih **Configure** (Konfigurasikan) > **Add Shard** (Tambahkan Shard) di kolom **Operation** (Operasi).
>?
>- Setelah konfigurasi disesuaikan, instans akan dikenakan biaya konfigurasi baru.
>- Saat shard ditambahkan, sistem akan secara otomatis menyeimbangkan konfigurasi slot dan memigrasikan data, yang mungkin gagal. Disarankan untuk melakukan operasi tersebut selama jam normal untuk menghindari dampak migrasi pada akses bisnis.
>- Tambahkan shard sesuai kebutuhan: setiap shard mendukung 80.000 hingga 100.000 QPS.
>

- **Arsitektur standar** 
Tingkatkan instans dari arsitektur standar ke arsitektur klaster untuk meningkatkan daya pemrosesan CPU. Sebelum peningkatan, Anda perlu memeriksa kompatibilitasnya. Untuk informasi selengkapnya, lihat [Memeriksa Migrasi dari Arsitektur Standar ke Arsitektur Klaster](https://intl.cloud.tencent.com/document/product/239/37594).
 1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans di daftar instans, dan masuk ke halaman detail instans.
 2. Di blok **Specs Info** (Info Spesifikasi), klik **Upgrade Architecture** (Tingkatkan Arsitektur).
![](https://main.qcloudimg.com/raw/03fc7dc818b3a893c904f8d15d61c3c6.png)
 3. Setelah peningkatan selesai, buka daftar instans dan pilih **Configure**  (Konfigurasikan) > **Add Shard** (Tambahkan Shard) di kolom **Operation** (Operasi).
