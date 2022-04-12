Dokumen ini menjelaskan fitur pemisahan baca/tulis otomatis dari layanan proksi database di TencentDB for MySQL dan keunggulan serta aturan peruteannya.

## [Pemisahan Baca/Tulis Otomatis](id:zddxfl)
Saat ini, bisnis dari banyak pengguna di lingkungan produksi memiliki masalah seperti lebih banyak membaca dan menulis lebih sedikit dan beban bisnis yang tidak terduga. Dalam skenario aplikasi dengan sejumlah besar permintaan baca, satu instans mungkin tidak dapat menahan tekanan permintaan baca, yang bahkan dapat memengaruhi bisnis. Untuk menerapkan penskalaan otomatis kemampuan baca dan mengurangi tekanan pada database, sebaiknya buat satu atau beberapa instans baca saja dan menggunakannya untuk mempertahankan jumlah pembacaan database yang tinggi. Namun, solusi ini mengharuskan bisnis dapat diubah untuk mendukung pemisahan baca/tulis, dan kecanggihan kode menentukan kualitas pemisahan baca/tulis bisnis, yang memberlakukan persyaratan teknis yang tinggi dan memiliki fleksibilitas dan skalabilitas yang rendah.

Oleh karena itu, setelah membuat instans baca saja, Anda dapat membeli proksi database, mengaktifkan pemisahan baca/tulis, dan mengonfigurasi alamat proksi database di aplikasi Anda sehingga secara otomatis meneruskan permintaan tulis ke instans sumber dan permintaan baca ke instans baca saja. Selain itu, metode ini memberikan solusi alami untuk tantangan bisnis lainnya seperti yang dijelaskan di bawah ini:
- **Applications with unpredictable workloads** (Aplikasi dengan beban kerja yang tidak terduga)
Aplikasi yang mendukung beban kerja yang sangat beragam mungkin mencoba membuka koneksi database baru untuk menangani lonjakan lalu lintas. Pengelolaan koneksi dalam proksi database khusus memungkinkan Anda untuk secara tepat menskalakan aplikasi yang memproses beban kerja yang tidak terduga dengan menggunakan kembali koneksi database secara efektif.
Pertama, fitur ini memungkinkan beberapa koneksi aplikasi untuk berbagi koneksi database yang sama untuk menggunakan sumber daya database secara efektif. Kedua, memungkinkan Anda untuk menyesuaikan jumlah koneksi database terbuka untuk mempertahankan performa database yang dapat diprediksi. Ketiga, ini memungkinkan Anda untuk menghapus permintaan aplikasi yang tidak dapat digunakan untuk menjamin performa dan ketersediaan aplikasi secara keseluruhan.

- **Applications frequently opening/closing database connections** (Aplikasi sering membuka/menutup koneksi database)
Aplikasi yang dibangun berdasarkan teknologi seperti tanpa server, PHP, atau Ruby on Rails mungkin sering membuka dan menutup koneksi database untuk memproses permintaan aplikasi.
Proksi database khusus dapat membantu Anda memelihara kumpulan koneksi database untuk mencegah tekanan yang tidak perlu pada komputasi data dan memori yang digunakan untuk membuat koneksi baru.

- **Applications with open but idle connections** (Aplikasi dengan koneksi terbuka tapi tidak aktif)
Aplikasi SaaS dan aplikasi ecommerce tradisional dapat membuat koneksi database jeda untuk meminimalkan waktu respons saat pengguna terhubung kembali. Anda dapat menggunakan proksi database khusus untuk mempertahankan koneksi tidak aktif dan membuat koneksi database untuk permintaan aktif sesuai kebutuhan, bukan meningkatkan ambang batas secara berlebihan atau menyediakan layanan database dengan spesifikasi lebih tinggi untuk mendukung sebagian besar koneksi tidak aktif.

- **Applications requiring highly smooth failover** (Aplikasi yang memerlukan failover yang sangat mulus)
Dengan proksi database khusus, Anda dapat membangun aplikasi yang dapat mentolerir kegagalan database aktif dan pasif dengan cara yang tidak terlihat tanpa menulis kode pemrosesan kegagalan yang kompleks. Proksi database khusus akan secara otomatis mengarahkan lalu lintas baca ke instans database baru sambil mempertahankan koneksi aplikasi.

![](https://main.qcloudimg.com/raw/a5f23e2235bc918b1a7e816c8f2c947b.png)

## Keunggulan
- Permintaan Baca/Tulis secara otomatis dipisahkan dengan alamat akses terpadu.
- Dukungan penautan native meningkatkan performa dan mengurangi biaya pemeliharaan.
- Anda dapat mengatur bobot dan ambang batas secara fleksibel.
- Failover didukung, sehingga meskipun proksi database gagal, permintaan dapat mengakses database sumber secara normal.
- Ketika instans sumber dialihkan, atau konfigurasinya diubah, atau instans baca saja ditambahkan/dihapus, proksi database dapat memuat ulang konfigurasi hot secara dinamis tanpa menyebabkan pemutusan jaringan atau restart.

## Aturan Perutean Pemisahan Baca/Tulis
### Mengirim ke instans sumber
- Pernyataan DDL seperti `CREATE`, `ALTER`, `DROP`, dan `RENAME`.
- Pernyataan DML seperti `INSERT`, `UPDATE`, dan `DELETE`.
- Pernyataan `SELECT FOR UPDATE`.
- Pernyataan yang terkait dengan tabel temp.
- Panggilan fungsi sistem tertentu (seperti `last_insert_id()`) dan semua panggilan fungsi kustom.
- Pernyataan yang terkait dengan `LOCK`.
- Pernyataan setelah transaksi diaktifkan (termasuk `set autocommit=0`)
- Prosedur tersimpan.
- Beberapa pernyataan yang digabungkan dengan ";".
- `KILL` (pernyataan SQL, bukan perintah)
- Semua pertanyaan dan perubahan variabel pengguna.

### Mengirim ke instans baca saja
- Baca (`SELECT`) pernyataan di luar transaksi.

### Mengirim ke semua instans
- Pernyataan `show processlist`.
- Semua perubahan variabel sistem (perintah `SET`).
- Perintah `USE`.
