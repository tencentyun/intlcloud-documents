
## Ikhtisar
Anda dapat membuat snapshot untuk disk cloud untuk menyimpan datanya pada titik waktu tertentu.Snapshot tambahan hanya merekam perubahan data dibandingkan dengan snapshot terakhir.Proses ini cepat jika datanya sedikit berubah.Selain itu, menghapus snapshot tidak akan memengaruhi penggunaan data snapshot Anda.Anda juga dapat memulihkan disk cloud dengan menggunakan snapshot yang tersisa.
Anda dapat membuat snapshot untuk disk cloud dalam keadaan apa pun, tetapi snapshot hanya dapat menangkap data tertulis daripada data yang sedang ditulis oleh aplikasi atau proses.Sebelum membuat snapshot, Anda dapat memilih untuk menangguhkan semua operasi I/O disk, atau [melepaskan](https://intl.cloud.tencent.com/document/product/362/32400) disk cloud dan [melampirkan]( https://intl.cloud.tencent.com/document/product/362/32401) nanti untuk membuat snapshot lengkap.

## Prasyarat
- Anda telah [membuat disk cloud](https://intl.cloud.tencent.com/document/product/362/5744).
- Anda belum mencapai batas atas untuk jumlah dan ukuran total snapshot di wilayah saat ini.Lihat [Batas Penggunaan Snapshot](https://intl.cloud.tencent.com/document/product/362/32406).

## Catatan
Snapshot hanya dapat menangkap data tertulis tetapi tidak men-cache data dalam memori (seperti file di direktori `/run` pada CVM Linux) dari disk cloud.Kami menyarankan Anda untuk mematikan instance, atau menulis semua data memori ke disk dan menangguhkan operasi I/O disk sebelum membuat snapshot.Ini dapat dilakukan pada dua tingkat berikut.
### Tingkat basis data
Untuk layanan basis data, kami menyarankan Anda untuk mengunci semua tabel dalam basis data sebagai hanya-baca untuk memastikan bahwa snapshot menangkap semua data.Dengan menggunakan MySQL sebagai contoh, prosedurnya adalah sebagai berikut:
1.Jalankan perintah `FLUSH TABLES WITH READ LOCK` untuk menutup semua tabel dan gunakan kunci baca global untuk mengunci semua tabel di setiap basis data, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/287ad27cec557a52a3386a60b937dc9b.png)
2.Buat snapshot untuk disk cloud.
3.Jalankan perintah `UNLOCK TABLES` untuk membuka kunci tabel, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/8a5fdcb0df254f0f9afcf3ef86679fc0.png)

### Tingkat sistem
Untuk kinerja sistem yang lebih baik, data disimpan dalam buffer memori sebelum ditulis ke disk cloud pada saat yang tepat.Oleh karena itu, snapshot yang dibuat untuk disk cloud tidak berisi data yang disimpan di buffer memori dan belum ditulis ke disk cloud.Akibatnya terjadi inkonsistensi data.
Untuk mengatasi masalah ini, jalankan perintah `sync` untuk secara paksa menulis data di buffer memori sistem file segera ke disk cloud, lalu mencegah data baru ditulis ke disk cloud.Jika tidak ada pesan kesalahan yang dikembalikan setelah perintah dijalankan, data di buffer memori telah berhasil ditulis ke disk cloud, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/e1b0ac245e325281a0693f7ae43946ff.png)



## Petunjuk[](id:CreateSnapshot)
### Membuat snapshot melalui konsol
1.Masuk ke [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
2.Pilih disk cloud target, dan klik **Create a snapshot** (Buat snapshot) di bawah kolom **Operation** (Pengoperasian), seperti yang ditunjukkan di bawah ini:

3.Di jendela pop-up, masukkan nama snapshot dan klik **OK**.

### Membuat snapshot melalui API
Anda dapat menggunakan API `CreateSnapshot` untuk membuat snapshot.Untuk informasi selengkapnya, lihat [Buat Snapshot](https://intl.cloud.tencent.com/document/product/362/15648).



