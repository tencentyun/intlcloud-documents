## Skenario Operasi 
Dokumen ini menjelaskan cara memodifikasi tabel di Konsol TcaplusDB. Jika Anda ingin memodifikasi definisi struktur tabel, Anda dapat melakukannya dengan memodifikasi tabel dengan syarat definisi baru memenuhi aturan modifikasi tabel TcaplusDB.

## Prasyarat
Anda telah membuat tabel. Untuk informasi selengkapnya, silakan lihat [Membuat Tabel](https://intl.cloud.tencent.com/document/product/1016/32715).

## Petunjuk
1. Masuk ke halaman [Daftar Tabel](https://console.cloud.tencent.com/tcaplusdb/table) dan pilih tabel target. Pilih **More** (Lainnya) > **Modify** (Modifikasi) di kolom "Operation" (Operasi) atau pilih beberapa tabel dan klik **Batch Modify** (Modifikasi Massal) di bagian atas.
2. Di kotak dialog "Modify" (Modifikasi) yang muncul, unggah atau pilih file definisi tabel baru dan klik **Compare Difference** (Bandingkan Perbedaan).
> 
>- Bidang kunci utama tidak dapat dihapus.
>- Nama dan jenis bidang kunci utama tidak dapat dimodifikasi.
>- Anda tidak dapat menambahkan bidang kunci utama baru.
>- Bidang umum yang ditandai sebagai wajib tidak dapat dihapus.
>- Nama dan jenis bidang dengan pengidentifikasi yang sama tidak dapat dimodifikasi.
>- Bidang umum baru harus diberi nama sesuai dengan konvensi penamaan.
>
![](https://main.qcloudimg.com/raw/407bf6c819bf9b60d4ebd18928904a6b.png)
3. Di kotak dialog pop-up, Anda dapat melihat hasil perbandingan. Jika definisi tabel baru Anda tidak memenuhi aturan modifikasi tabel TcaplusDB, perintah akan ditampilkan.
![](https://main.qcloudimg.com/raw/087642d98430e6e1d066ae5dfc202f1a.png)
4. Klik **Preview** (Pratinjau) di kolom "Comparison Preview" (Pratinjau Perbandingan) untuk melihat perbandingan antara struktur tabel baru dan lama.
![](https://main.qcloudimg.com/raw/997d4e6cd91e2815a8534f44e2ee10de.png)
5. Setelah mengonfirmasi bahwa semuanya sudah benar, klik **Confirm** (Konfirmasi) untuk mengirimkan permintaan Anda untuk memodifikasi tabel, dan perintah akan ditampilkan jika modifikasi berhasil.
![](https://main.qcloudimg.com/raw/53fc68f54fcbaf6726874e9af3c26463.png)
   Setelah modifikasi, Anda dapat melihat struktur tabel baru di halaman konfigurasi tabel.
   
