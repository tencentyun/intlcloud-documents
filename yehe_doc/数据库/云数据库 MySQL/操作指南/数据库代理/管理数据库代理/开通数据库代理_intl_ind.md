
Dokumen ini menjelaskan cara mengaktifkan proksi database di konsol TencentDB for MySQL.

[Proksi database](https://intl.cloud.tencent.com/document/product/236/42048) adalah layanan proksi jaringan antara layanan TencentDB dan layanan aplikasi. Ini digunakan untuk membuat proksi pada semua permintaan ketika layanan aplikasi mengakses database. Proksi ini menyediakan fitur canggih seperti pemisahan baca/tulis otomatis, kumpulan koneksi, dan persistensi koneksi dan menawarkan ketersediaan tinggi, performa tinggi, dukungan OPS, dan kemudahan penggunaan.


## Catatan
- Proksi database saat ini didukung di wilayah berikut:
  - Beijing (kecuali Zona 1, 2, dan 4), Shanghai (kecuali Zona 1), Guangzhou (kecuali Zona 1 dan 2), Chengdu (kecuali Zona 1), Chongqing, Nanjing, dan Hong Kong (Tiongkok) (kecuali Zona 1 ).
  - Tokyo (kecuali Zona 1), Bangkok (kecuali Zona 1), Virginia (kecuali Zona 1), Silicon Valley (kecuali Zona 1), Mumbai (kecuali Zona 1), dan Seoul (kecuali Zona 1).
- Proksi database saat ini didukung pada versi berikut: MySQL v5.7 dua node dan tiga node (versi minor kernel harus 20201230 atau yang lebih tinggi). Jika Anda meningkatkan versi minor kernel dari instans sumber, instans baca saja dan pemulihan bencana yang terkait akan ditingkatkan secara bersamaan. Untuk informasi selengkapnya, lihat [Meningkatkan Versi Minor Kernel](https://intl.cloud.tencent.com/document/product/236/36816).

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, pilih instans sumber yang akan mengaktifkan proksi database dan klik ID-nya atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Database Proxy** (Proksi Database) dan klik **Enable Now** (Aktifkan Sekarang).
![](https://main.qcloudimg.com/raw/46d9e9b30975b51bee00a16c64f31c8b.png)
3. Di jendela pop-up, pilih spesifikasi dan jumlah node, klik **OK** (OKE), dan muat ulang.
 - Jaringan: saat ini, hanya VPC yang didukung. VPC dari instans sumber dipilih secara default.
 - Spesifikasi Proksi: saat ini, hanya satu spesifikasi yang didukung.
 - Jumlah Node: jumlah node proksi. Sebaiknya atur kuantitas menjadi 1/8 (dibulatkan ke atas) dari jumlah total core CPU pada instans sumber dan baca saja; misalnya, jika instans sumber memiliki 4 core CPU, dan instans baca saja memiliki 8 core CPU, jumlah node yang direkomendasikan adalah (4 + 8) / 8 ≈ 2.
 - Grup Keamanan: ini merupakan sarana penting untuk isolasi keamanan jaringan. Anda dapat memilih grup keamanan yang ada atau membuat grup yang baru sesuai kebutuhan.
<img src="https://main.qcloudimg.com/raw/a3d8fafb1930d0298deb9cf2f08e706c.png"  style="zoom:80%;"> 
4. Setelah berhasil mengaktifkan layanan, Anda dapat mengelola node proksi dan melihat informasi dasarnya di halaman proksi database. Anda juga dapat mengubah alamat proksi database dan jenis jaringan serta menambahkan komentar di bagian **Connection Addres** (Alamat Koneksi).
>?
>- Anda dapat melihat **Connections** (Koneksi) dalam daftar node proksi atau melihat data pemantauan performa setiap node proksi untuk memeriksa apakah jumlah koneksi pada node tidak seimbang, sehingga Anda dapat mendistribusikan koneksi dengan mengklik * *Rebalance** (Penyeimbangan kembali).
>- Penyeimbangan kembali akan menyebabkan node proksi memulai ulang, dan layanan akan menjadi tidak tersedia untuk sementara waktu selama mulai ulang. Sebaiknya mulai ulang layanan selama jam normal. Pastikan bisnis Anda memiliki mekanisme koneksi ulang.
>
![](https://main.qcloudimg.com/raw/083d38858367fd7fe65e90fb92210178.png)
