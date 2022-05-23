
TencentDB for Redis mendukung arsitektur standar dan arsitektur kluster. Untuk membantu Anda memproses data bisnis yang terus berkembang, ini memungkinkan Anda meningkatkan dari arsitektur standar ke arsitektur kluster jika performa dan kapasitas arsitektur standar tidak mencukupi.

## Deskripsi Peningkatan
- Untuk Redis 4.0 atau yang lebih baru, instans arsitektur standar dapat ditingkatkan ke instans arsitektur kluster pada versi yang sama; misalnya, Anda dapat meningkatkan dari Arsitektur Standar Redis 4.0 ke Arsitektur Kluster Redis 4.0.
- Pembaruan arsitektur lintas versi tidak didukung; misalnya, Anda tidak dapat memutakhirkan dari Arsitektur Standar Redis 4.0 ke Arsitektur Kluster Redis 5.0.
- Arsitektur Redis 2.8 tidak dapat ditingkatkan.
- Arsitektur kluster tidak dapat diturunkan ke arsitektur standar.
- Peningkatan arsitektur Lintas-AZ tidak didukung.
- Peningkatan arsitektur kluster tidak didukung untuk instans bayar sesuai pemakaian.
- Setelah arsitektur standar ditingkatkan ke arsitektur kluster, biaya akan dibebankan berdasarkan arsitektur kluster sehingga akan terjadi peningkatan. Untuk informasi selengkapnya, lihat [Harga](https://intl.cloud.tencent.com/document/product/239/9894).

## Cara Kerja Peningkatan
- Arsitektur standar Redis dapat langsung ditingkatkan ke arsitektur kluster (pecahan tunggal) dalam waktu tiga menit tanpa perlu migrasi data.
- Pada Redis 4.0 atau yang lebih baru, jika arsitektur standar ditingkatkan ke arsitektur kluster, hanya mode runtime instans yang akan berubah dari tidak memiliki batas slot menjadi memiliki batas slot, tetapi migrasi data tidak akan terlibat.

## Persiapan Peningkatan (Pemeriksaan Kompatibilitas)
Untuk menghindari kegagalan bisnis yang disebabkan oleh masalah kompatibilitas selama migrasi ke arsitektur kluster, periksa kompatibilitas sebelum meningkatkan:
- Arsitektur kluster menyimpan data secara terdistribusi, dan perbedaan terbesarnya dibandingkan arsitektur standar terletak pada apakah satu perintah mendukung akses multikunci. Untuk arsitektur kluster, perintah dapat dikategorikan menjadi didukung, sebagian didukung, dan tidak didukung. Untuk daftar lengkap perintah yang kompatibel, lihat [Kompatibilitas Perintah](https://intl.cloud.tencent.com/document/product/239/31958).
- Untuk informasi selengkapnya tentang pemeriksaan kompatibilitas, lihat [Periksa Migrasi dari Arsitektur Standar ke Arsitektur Kluster](https://intl.cloud.tencent.com/document/product/239/37594).

## Pengaruh Peningkatan ke CLB Baru
- Umumnya, peningkatan dapat diselesaikan dalam tiga menit.
- Selama peningkatan, koneksi yang ada akan ditutup sementara; oleh karena itu, bisnis Anda harus memiliki mekanisme koneksi ulang.

## Petunjuk Peningkatan
1. Login ke [Konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), pilih wilayah daftar instans, dan klik ID instans untuk masuk ke halaman detail instans.
2. Pada halaman detail instans, klik **Upgrade Architecture** (Tingkatkan Arsitektur).
![](https://main.qcloudimg.com/raw/ebc4ecc50af95d99be2fa23f45d11278.png)
3. Di kotak dialog pop-up, pilih arsitektur dan waktu beralih, berikan persetujuan Anda terhadap pemberitahuan tentang risiko kompatibilitas, dan klik **OK**.
Peningkatan arsitektur mendukung opsi **Switch Now** (Beralih Sekarang) dan **Switch in Maintenance Time** (Beralih dalam Waktu Pemeliharaan). Anda dapat mengubah waktu pemeliharaan di **Maintenance Time** (Waktu Peralihan) di halaman detail instans.
![](https://main.qcloudimg.com/raw/f584ccc7b3004feb662e72e8ddcf819a.png)
4. Setelah pembayaran selesai, Anda akan diarahkan ke daftar instans. Setelah status instans berubah menjadi **Berjalan**, instans dapat digunakan secara normal.
