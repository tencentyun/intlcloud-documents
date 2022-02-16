Desain database penting dalam siklus pemakaian pengembangan perangkat lunak. Dokumen ini memberikan panduan dan praktik terbaik untuk desain database.

## Panduan Definisi Struktur Tabel
- Nama bidang atau tabel tidak boleh berisi karakter khusus apa pun, dan panjang yang direkomendasikan tidak lebih dari 32 byte.
- Nama bidang atau tabel harus bermakna dan hindari singkatan yang membingungkan jika memungkinkan.
- Anda harus memilih jenis data yang tepat dan tidak kehilangan presisi angka yang dibutuhkan.
- Kunci primer dan shardkey harus sangat diskrit untuk penyeimbangan dan penskalaan beban yang lebih mudah.
- Jumlah indeks yang Anda buat tergantung pada kueri yang dibutuhkan. Indeks tidak boleh memiliki definisi yang sama dengan kunci primer.
- Kami merekomendasikan jenis INT untuk alamat IP bisnis Anda.
- Sebaiknya gunakan jenis LONG untuk menyimpan data waktu dalam hitungan detik.
- Untuk menjamin atomik operasi, sebaiknya tempatkan bidang yang terkait secara logis dalam tabel yang sama.
- Jika Anda memiliki persyaratan tinggi pada performa database, Anda dapat mengadopsi desain redundansi data.
- Kunci primer dan shardkey harus sangat diskrit untuk penskalaan yang lebih mudah.
- Kunci primer harus dapat dibaca untuk kueri dan pemecahan masalah yang lebih mudah. Sebaiknya jangan gunakan kunci primer biner.
- Anda harus menggunakan kunci primer singkat jika memungkinkan, yang akan membuat kueri lebih cepat.
- Anda harus menentukan ukuran bidang berdasarkan kebutuhan Anda. Hindari situasi seperti itu saat bidang yang ditentukan dengan ukuran besar memiliki nilai kecil saat benar-benar digunakan.
- Anda harus menambahkan komentar ke semua tabel dan bidang.

## Panduan Desain Database Game
- Jika database perlu menghasilkan ID unik global, sebaiknya gunakan perintah `increase`.
- Anda harus menghindari kelebihan database saat merancang arsitektur database. Misalnya, Anda dapat menambahkan mekanisme antrean.
- Anda harus menyimpan data yang relevan dalam tabel yang sama untuk menghindari inkonsistensi data.
- Sebaiknya jangan terapkan semua fitur dalam satu tabel. Fitur yang terpisah dari fitur lain memerlukan tabel sendiri.
- Jika tabel sering digunakan dan memiliki banyak catatan, Anda perlu mendesain tabel profil sehingga aplikasi tidak perlu mengakses data dari tabel asli, yang meringankan beban database.
- Karena obrolan di lobi game dapat berbagi memori dan obrolan dalam satu game dapat didorong secara real-time, sebaiknya jangan gunakan database dalam skenario tersebut. Namun, database cocok untuk obrolan pribadi offline.
- Sebaiknya gunakan jenis array yang disediakan oleh database untuk menangani data, email, dan laporan game historis. Jenis data ini mendukung pengantrean/penghapusan antrean dan `TopN` dalam urutan data yang diantrekan.
- Sebaiknya gunakan komponen sortir dalam desain daftar peringkat. Jika fitur peringkat diterapkan di server game, sebaiknya simpan hasil peringkat di database secara asinkron.
- Operasi marginal dan memakan waktu dalam game membutuhkan proses yang berbeda, yang dapat menghindari memengaruhi logis utama dari server game.
- Siklus pengembangan game berlangsung panjang dan kompleks secara logis. Selama proses pengembangan, struktur data logis cenderung berubah. Untuk skalabilitas dan kemudahan pemeliharaan, sebaiknya tentukan data yang dapat diubah sebagai data BLOB dalam fase desain tabel database game. Jenis data ini diserialisasi sebelum disimpan ke dalam database untuk menghindari seringnya perubahan tabel database karena perubahan struktur data.

## Definisi Tabel TDR
- Kunci primer harus sangat diskrit sehingga permintaan dari server game dapat didistribusikan ke beberapa node lapisan akses.
- Sebaiknya kunci primer tidak identik dengan kunci indeks dalam definisi tabel, karena kunci identik akan memboroskan sumber daya jaringan dan disk.
- Untuk mendefinisikan bidang kunci non-primer sebagai array, atribut `refer` harus ditambahkan (`count` adalah ukuran yang ditentukan, dan `refer` adalah ukuran sebenarnya), sehingga ukuran `count` dapat diperluas nanti, dan jejak data dalam transmisi jaringan dan pada disk dapat dikurangi.
- Kedalaman bidang berlapis dibatasi hingga tiga dan bidang kunci non-primer harus berada di tingkat berlapis pertama.
- Bidang kunci primer biner tidak direkomendasikan karena berfungsi secara tidak efisien dalam pemecahan masalah.
- Hingga delapan indeks dapat ditentukan per tabel. Sebaiknya tentukan dua atau tiga indeks per tabel. Terlalu banyak indeks akan mengurangi performa database, jadi harap tentukan indeks berdasarkan kebutuhan Anda.

## Definisi Tabel Buffer Protokol
- Kunci primer harus sangat diskrit sehingga permintaan dari server game dapat didistribusikan ke beberapa node lapisan akses.
- Bidang kunci non-primer dapat didefinisikan sebagai struktur berlapis. Akses data akan disusupi jika tingkat berlapis terlalu dalam.

## Contoh Desain yang telah Usang
- Desain tidak dapat memenuhi permintaan
Desain tersebut menyebabkan banyak modifikasi. Untuk proyek tepat sebelum fase peluncuran, biaya modifikasi bahkan lebih tinggi.
- Performa rendah
Ada terlalu banyak batasan antara tabel dengan data dalam jumlah besar; Pernyataan kueri SQL rumit karena kurangnya bidang yang didesain dengan baik untuk kueri; tidak ada metode yang efektif untuk menangani tabel dengan data dalam jumlah besar; ada terlalu banyak tampilan atau tampilan tidak digunakan secara efisien.
- Hilangnya integritas data
Kunci primer atau kunci asing yang didesain dengan buruk menyebabkan kesalahan program setelah operasi pembaruan dan penghapusan; data yang telah dihapus atau dilepas digunakan.
- Skalabilitas yang buruk
Tabel memiliki afinitas tinggi dengan bisnis dan tidak memiliki kemampuan untuk menskalakan, beradaptasi dengan perubahan, atau memenuhi permintaan baru.
- Banyak data sampah yang redundan
Banyak data sampah yang redundan menghabiskan sumber daya dan mengurangi efisiensi kueri.
- Bidang tidak efisien dalam perhitungan atau statistik
Tidak ada bidang yang didesain untuk perhitungan atau statistik; bidang yang digunakan untuk perhitungan dan statistik tersebar di beberapa tabel, sehingga membuat proses perhitungan dan statistik menjadi rumit atau bahkan tidak mungkin dilakukan.
- Tidak ada catatan data mendetail
Tidak ada bidang yang dapat digunakan untuk melacak perubahan data dan operasi pengguna, atau menganalisis data.
- Penyandingan ketat antar tabel
Tabel sangat bergantung satu sama lain. Perubahan pada satu tabel akan memengaruhi tabel lainnya.
- Bidang yang didesain dengan buruk
Panjang bidang terlalu pendek atau jenis bidang sulit diubah nanti. Bidang tersebut akan mengurangi skalabilitas.



