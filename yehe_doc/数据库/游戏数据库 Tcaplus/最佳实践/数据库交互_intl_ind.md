## Praktik Terbaik untuk Server Game
1. Dalam kasus penggunaan saat tidak semua bidang perlu dibaca dari atau ditulis, sebaiknya hanya baca dan perbarui bidang wajib diisi untuk menghindari pengambilan data yang tidak valid. Tindakan ini dapat mengurangi ukuran data yang dikirimkan melalui jaringan dan mengurangi jumlah pembacaan dan penulisan disk.
2. Jika catatan data perlu dikembalikan saat operasi penulisan dilakukan, sebaiknya atur `result_flag` sesuai kebutuhan. Misalnya, jika catatan data yang diperbarui diperlukan setelah operasi pembaruan dilakukan, `result_flag` harus diatur ke 2. Jika catatan data tidak diperlukan selama operasi penulisan, `result_flag` diatur ke 0.
3. Untuk kata perintah dalam tugas pemrosesan batch, seperti `batchget`, `listgetall`, dan `getbypartkey`, sebaiknya dapatkan catatan data berdasarkan `offest` dan `limit`. Sebaiknya atur `limit` ke 200 dan aktifkan pengembalian multi-paket di server game.
4. Untuk tabel yang mendukung jenis data LIST, saat operasi `listaddafter` dilakukan, aturan enqueue/dequeue harus diatur jika daftar penuh. Sebaiknya aturan menambahkan catatan baru ke depan dan hapus catatan dari belakang, atau sebaliknya.
5. Untuk tabel yang mendukung jenis data LIST, indeks yang benar harus diteruskan untuk operasi `listreplace`, `listdelete`, dan `listbatchdelete`.
6. Sebelum server game membaca data, pastikan bidang kunci non-primer dari catatan data yang akan dibaca tidak kosong. Misalnya, ketika ada tiga bidang kunci non-primer: A, B dan C, jika server game hanya mendapatkan A dan B, hal ini menandakan bahwa bidang C kosong. Harap periksa bidang sebelum membaca catatan data.
7. Server game harus mengontrol waktu habis secara lokal, dan sebaiknya jangan tentukan waktu habis berdasarkan paket respons yang dikirim dari server game.
8. Saat server game melakukan penjelajahan, sebaiknya akses data dari node sekunder di lapisan penyimpanan, untuk menghindari memengaruhi performa node primer.
9. Sebaiknya jangan lakukan operasi `memset` pada bidang besar untuk menghindari penggunaan sumber daya CPU. Anda dapat mengatur nilai beberapa bidang dalam struktur data besar ke 0 sebelum inisialisasi.
10. Saat memproses permintaan ke TcaplusDB dan respons dari TcaplusDB, server game harus menggunakan metode divide-and-conquer untuk memproses sebagian permintaan yang dikirim ke TcaplusDB terlebih dahulu, lalu memproses respons yang dikembalikan dari TcaplusDB.

## Praktik Terbaik untuk Desain Sistem
1. Buat tabel terpisah untuk bidang yang sering digunakan dan bidang tempat operasi atom satu kali perlu dilakukan.
2. Saat server game menulis kembali data, sebaiknya batasi lalu lintas dan diskritkan data berdasarkan waktu.
3. Anda dapat memodifikasi struktur tabel saat menggunakan tabel, dan plugin konversi data tabel disediakan.
4. Kembalikan ke titik waktu cold backup Anda atau ke waktu yang tepat di tingkat tabel/logging dalam mode semua-server/semua-wilayah didukung.
5. Node pada lapisan akses dan lapisan penyimpanan dapat diskalakan secara dinamis untuk mode semua-server/semua-wilayah dan mode multi-server/multi-wilayah. Sebaiknya gunakan mode multi-server/multi-wilayah.
6. Bidang dengan hubungan logis harus digabungkan menjadi satu tabel untuk menghindari masalah transaksi yang terdistribusi.
7. Sebaiknya aktifkan fitur kompresi, termasuk kompresi paket dan log permintaan/respons.