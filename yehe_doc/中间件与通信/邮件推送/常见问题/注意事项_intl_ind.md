[](id:dns)
### Verifikasi validitas DNS

Anda dapat menggunakan [DNS Checker](https://www.whatsmydns.net/) untuk memverifikasi apakah konfigurasi DNS Anda valid.

[](id:add)
### Validitas alamat email
Tingkat pantulan email adalah metrik tetap untuk penilaian email oleh ISP. Alasan paling mungkin untuk pantulan email adalah alamat email yang tidak valid; yaitu, email dikirim ke alamat yang salah. Jika tingkat pantulan tetap tinggi, ISP akan menentukan pengirim sebagai berbahaya dan kemudian memasukkan email ke folder spam atau memblokir IP pengirim. Tingkat pantulan yang baik tidak boleh melebihi 5%. Jika alamat penerima berkualitas buruk, Anda perlu memproses dan memfilternya terlebih dahulu.

[](id:garbage)
### Folder spam
Tidak ada pengirim yang dapat menjamin bahwa email tidak akan masuk ke folder spam penerima. Terutama, ketika nama domain pengirim baru terdaftar dan dengan demikian tidak memiliki reputasi dengan ISP, email masuk ke folder spam adalah hal yang normal. Hal ini membutuhkan warm-up yang baik dan keterlibatan pengguna untuk meningkatkan reputasi nama domain. ISP akan menyesuaikan kebijakan spam secara dinamis berdasarkan reputasi dan akhirnya mengirim email ke kotak masuk penerima. Oleh karena itu, sebaiknya tambahkan perintah "Jika Anda tidak melihat email, silakan periksa folder spam Anda".

[](id:avoid)
### Tindakan untuk mencegah email ditandai sebagai spam
1. Tulis subjek email yang sesuai dan hindari menggunakan kata-kata pemasaran yang tidak biasa atau jelas.
2. Hindari "spam" dan konten ilegal yang jelas serta kata-kata yang dikomersilkan secara berlebihan, seperti undian berhadiah, perjudian, pornografi, narkoba, dan pencabulan.
3. Seimbangkan jumlah kata dan gambar, jangan menggunakan terlalu banyak gambar, dan hindari email yang hanya menggunakan gambar besar tanpa teks.
4. Lebih baik tidak menambahkan URL di konten email; jika tidak, email dapat dengan mudah diidentifikasi sebagai spam.
5. Gunakan font biasa ketimbang berbagai warna atau font artistik dalam konten email.
6. Pastikan untuk menambahkan tombol berhenti berlangganan visual yang mudah di konten email. Melakukannya dapat mencegah pengguna merasa terganggu dengan email Anda saat mereka tidak membutuhkan produk atau layanan yang Anda berikan, karena mereka cukup mengeklik tombol berhenti berlangganan ketimbang melaporkan atau memblokir email Anda. Langkah ini akan memberikan kesan positif pada pengguna dan mengurangi kemungkinan email Anda dikenali sebagai spam.
7. Standarkan kode HTML email, karena kode yang tidak sesuai dapat diidentifikasi sebagai spam oleh filter email. Anda harus memiliki pembuat kode profesional atau menggunakan templat email profesional.
8. Dorong pelanggan untuk menambahkan Anda sebagai teman atau kontak. Dengan cara ini, email Anda pasti akan masuk ke kotak masuk mereka, bukan folder spam.
9. Bersihkan daftar penerima secara teratur. Ketika Anda mengetahui bahwa email Anda gagal terkirim ke banyak penerima, filter spam dari sebagian besar penyedia layanan email akan memberi nama domain atau IP Anda skor indeks spam yang lebih tinggi.
10. Lakukan pengujian sebelum mengirim email secara formal. Sebelum mengirim email Anda ke penerima secara formal, Anda dapat menggunakan akun Anda sendiri untuk menguji pengiriman. Dengan cara ini, Anda juga dapat menyimpulkan jenis email apa yang lebih mungkin dikenali sebagai spam dan kemudian mengoptimalkan konten yang sesuai.

[](id:multiple)
### Pengiriman batch
1. Fitur **Batch** di konsol cocok untuk pengiriman batch email pemasaran atau pemberitahuan. Untuk mengirim email berbasis pemicu (seperti autentikasi dan email transaksional), sebaiknya panggil API `SendEmail`.
2. Warm-up otomatis dibangun dalam fitur pengiriman batch untuk secara cerdas menentukan reputasi domain/IP pengirim dan jumlah maksimum email terkirim yang diizinkan per hari. Ketika batas harian ini tercapai, pengiriman email akan berhenti dan email tambahan akan masuk ke antrean cache dan dikirim dalam waktu 24 jam kemudian. Untuk batas email harian untuk domain/IP yang belum di-warm-up, lihat [Rencana Warm-up Standar](https://intl.cloud.tencent.com/document/product/1084/43285#default).
3. Anda dapat menggunakan satu domain untuk beberapa tugas pengiriman. Ketika total volume email melebihi jumlah maksimum yang diizinkan per hari, email tambahan akan masuk ke antrean cache dan dikirim pada hari berikutnya.
4. Saat tugas memasuki antrean cache, statusnya adalah **Dijeda** dan bilah kemajuan pengiriman tetap statis. Setelah Anda memulai ulang tugas pada hari berikutnya, statusnya menjadi **Mengirim** dan bilah kemajuan bertambah.
