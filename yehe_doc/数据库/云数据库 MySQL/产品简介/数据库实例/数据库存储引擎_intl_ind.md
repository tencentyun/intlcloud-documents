Mesin penyimpanan database mengacu pada jenis tabel dan menentukan cara tabel disimpan di komputer. Meskipun MySQL mendukung berbagai jenis mesin penyimpanan, tidak semuanya telah dioptimalkan untuk pemulihan dan persistensi data. Fitur TencentDB for MySQL seperti pemulihan point-in-time dan pemulihan snapshot memerlukan mesin penyimpanan yang mendukung pemulihan dan hanya tersedia di mesin penyimpanan InnoDB.

TencentDB for MySQL mendukung InnoDB secara default. Tidak lagi mendukung mesin MyISAM dan Memori di MySQL 5.6 serta yang lebih tinggi terutama karena alasan berikut:
- TencentDB for MySQL sangat mengoptimalkan kernel untuk InnoDB dan mencapai performa yang lebih tinggi.
- MyISAM mengadopsi mekanisme penguncian level tabel, sedangkan InnoDB menggunakan mekanisme level baris. Biasanya, InnoDB memiliki efisiensi penulisan yang lebih tinggi.
>?
>- Dengan cakupan kunci terluas, penguncian tingkat tabel adalah mengunci seluruh tabel yang sedang dimanipulasi di MySQL.
>- Dengan cakupan kunci paling kecil, penguncian tingkat baris hanya mengunci baris yang sedang dimanipulasi di MySQL.
- MyISAM memiliki cacat dalam melindungi integritas data, yang dapat menyebabkan kerusakan data atau bahkan kehilangan. Selain itu, banyak dari kerusakan ini akibat masalah desain dan tidak dapat diperbaiki tanpa merusak kompatibilitas.
- Migrasi dari MyISAM dan Memori ke InnoDB dapat dicapai dengan biaya rendah hanya dengan mengubah kode untuk membuat tabel untuk sebagian besar aplikasi.
- MyISAM memberikan landasan untuk InnoDB. Di MySQL 8.0 terbaru, semua tabel sistem dilengkapi dengan jenis InnoDB.
- Memori tidak dapat menjamin integritas data. Jika instans dimulai ulang atau mengalami penukaran sumber/replika, semua data dalam tabel akan hilang. Disarankan untuk bermigrasi ke InnoDB secepatnya.

Untuk informasi selengkapnya, silakan lihat [Ikhtisar InnoDB](https://dev.mysql.com/doc/refman/5.7/en/innodb-introduction.html) dan [Ikhtisar MyISAM](https://dev.mysql.com/doc/refman/5.7/en/myisam-storage-engine.html).

