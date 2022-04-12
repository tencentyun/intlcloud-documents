
Replikasi instans database berarti menyinkronkan data dengan mengonfigurasi satu atau lebih database cadangan untuk server untuk mendistribusikan data di MySQL ke beberapa sistem. TencentDB for MySQL mendukung tiga mode replikasi data:

>?
>- "Sumber" mengacu pada node sumber dalam sebuah instans, sedangkan "replika" mengacu pada node replika dalam instans.
>- Saat ini, MySQL v5.6, v5.7, dan v8.0 mendukung tiga mode replikasi: asinkron, semi-sinkronasi, dan sinkronisasi yang canggih. Hanya mode asinkron yang tersedia di MySQL v5.5.


### Replikasi Asinkron
Aplikasi memulai pembaruan data (termasuk operasi INSERT, UPDATE, dan DELETE). Setelah menyelesaikan operasi pembaruan, sumber segera mengirimkan respons ke aplikasi, kemudian mereplikasi data ke replika.

Selama pembaruan data, sumber tidak perlu menunggu respons dari replika, sehingga instans database yang direplikasi secara asinkron sering kali memiliki performa yang lebih tinggi, dan ketidaktersediaan replika tidak akan memengaruhi penyediaan layanan oleh sumber. Namun, karena data tidak disinkronkan ke replika secara real time, jika sumber gagal saat terjadi penundaan pada replika, ada sedikit kemungkinan inkonsistensi data.
Replikasi asinkron diimplementasikan pada TencentDB satu-sumber dengan satu-replika untuk MySQL.

### Replikasi Semi-Sinkronisasi
Aplikasi memulai pembaruan data (termasuk operasi INSERT, UPDATE, dan DELETE). Setelah menyelesaikan operasi pembaruan, sumber segera mereplikasi data ke replika. Setelah **receiving and writing the data into relay log (bypassed)** (menerima dan menulis data ke dalam log relai (diteruskan)), replika menampilkan pesan sukses ke sumbernya. Hanya setelah menerima pesan dari replika, sumber dapat menampilkan respons ke aplikasi.

Hanya ketika pengecualian terjadi dengan replikasi data (node ​​replika menjadi tidak tersedia atau pengecualian terjadi dengan jaringan yang digunakan untuk replikasi data), sumber akan menangguhkan respons ke aplikasi (selama sekitar 10 detik secara default di MySQL), dan replikasi akan diturunkan ke replikasi asinkron. Ketika replikasi data kembali ke status normal, replikasi semi-sinkronisasi akan dipulihkan.
Replikasi semi-sinkronisasi diimplementasikan pada TencentDB satu-sumber-satu-replika untuk MySQL.

### Replikasi Sinkronisasi yang Canggih
Aplikasi memulai pembaruan data (termasuk operasi INSERT, UPDATE, dan DELETE). Setelah menyelesaikan operasi pembaruan, sumber segera mereplikasi data ke replika. Setelah **receiving and writing the data into relay log (bypassed)** (menerima dan menulis data ke dalam log relai (diteruskan)), replika menampilkan pesan sukses ke sumbernya. Hanya setelah menerima pesan dari replika, sumber dapat menampilkan respons ke aplikasi.

Saat pengecualian terjadi dengan replikasi data (node ​​replika menjadi tidak tersedia atau pengecualian terjadi dengan jaringan yang digunakan untuk replikasi data), **the replication won't be downgraded** (replikasi tidak akan diturunkan versinya) dan sumber akan menangguhkan respons ke aplikasi hingga pengecualian ditangani untuk memastikan konsistensi data.

Replikasi sinkronisasi yang canggih diimplementasikan pada TencentDB satu-sumber dengan dua-replika untuk MySQL. Sumber dapat menerima pesan sukses selama salah satu dari dua replika berhasil memperbarui data, mencegah tidak tersedianya satu replika memengaruhi operasi pada sumber, dan meningkatkan ketersediaan kluster replikasi sinkronisasi yang canggih.


