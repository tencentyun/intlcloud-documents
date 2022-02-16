## Skenario Operasi
Dokumen ini menjelaskan cara membuat tabel di Konsol TcaplusDB.

## Prasyarat
- Anda telah membuat [kluster](https://intl.cloud.tencent.com/document/product/1016/32714) dan [grup tabel](https://intl.cloud.tencent.com/document/product/1016/32716) TcaplusDB.
- Anda telah menyiapkan file tabel sesuai dengan [contoh file deskripsi tabel](https://intl.cloud.tencent.com/document/product/1016/36560).

## Petunjuk
1. Masuk ke [Konsol TcaplusDB](https://console.cloud.tencent.com/tcaplusdb/table), pilih **Table List** (Daftar Tabel) di bilah sisi kiri, dan klik **Create Table** (Buat Tabel).
2. Konfigurasi tabel pada halaman pembuatan tabel.
 -**Cluster and Table Group** (Kluster dan Grup Tabel): pilih kluster target dan grup tabel.
 - **Table File** (File Tabel): Anda dapat mengunggah file definisi tabel dari sistem file lokal, memilih file yang telah diunggah sebelumnya, atau memadupadankan. Namun, nama file harus unik. Untuk informasi selengkapnya, silakan lihat contoh file tabel PB [game_players.proto](
https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/game_players.proto).
 - **Remarks** (Keterangan): masukkan keterangan tabel.
   ![](https://main.qcloudimg.com/raw/5621a15042a9d73b4364fe19b9a9268b.png)
3. Klik **Next** (Selanjutnya) dan sistem akan memverifikasi file definisi tabel yang dipilih.
 - Jika verifikasi gagal, kesalahan akan dikembalikan, dan Anda harus memodifikasi file yang sesuai dan mengunggahnya lagi.
 - Jika verifikasi berhasil, metadata tabel yang ditentukan dalam file akan ditampilkan, dan Anda dapat melanjutkan ke langkah selanjutnya.
4. Pada halaman konfigurasi tabel, pilih tabel yang akan dibuat dan masukkan kapasitas serta parameter baca dan tulis yang dicadangkan. Biaya harian tabel akan dihitung secara otomatis.
![](https://main.qcloudimg.com/raw/32aa5c8a292df17249a62e88b6fca4e6.png)
5. Setelah mengonfirmasi bahwa informasi tabel benar, klik **Create** (Buat) dan sistem akan menunjukkan bahwa pembuatan berhasil.
![](https://main.qcloudimg.com/raw/7a39640da609a65df7040fc9c1d7be3d.png)
