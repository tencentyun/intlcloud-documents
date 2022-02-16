## Ikhtisar Mode Kapasitas Baca/Tulis
TcaplusDB menggunakan mode kapasitas baca/tulis untuk menghitung volume permintaan baca/tulis tabel.

### Unit kapasitas (CU)
Ini adalah unit permintaan minimal akses sumber daya dan unit statistik minimal pembacaan/penulisan data yang diminta.

### Unit kapasitas baca (RCU)
Ini adalah unit minimal permintaan baca. Data respons yang dihasilkan untuk permintaan dapat berisi beberapa RCU. Nilai maksimal RCU adalah 4 KB, yaitu, RCU menunjukkan bahwa permintaan baca dapat dilakukan pada catatan yang berukuran hingga 4 KB. Jika perlu membaca data lebih dari 4 KB, Anda memerlukan lebih banyak RCU.

Jumlah dasar RCU adalah 4 KB. Ukuran permintaan di bawah 4 KB dihitung sebagai 4 KB, dan ukuran permintaan di atas 4 KB dihitung sebagai kelipatan 4 KB (sisa di bawah 4 KB dihitung sebagai 4 KB).
Di bawah ini adalah contoh:
**Read request capacity** (Kapasitas permintaan baca)
  Anda mengirim permintaan untuk mengkueri bidang dalam catatan yang berukuran 10 KB, dan database mengembalikan nilai bidang catatan yang ditentukan. Dalam hal ini, data respons adalah 10 KB, yaitu 3 RCU.

### Unit kapasitas tulis (WCU)
Ini adalah unit minimal permintaan tulis. Data tertulis yang dihasilkan untuk permintaan tulis mungkin berisi beberapa WCU. Nilai maksimal sebuah WCU adalah 4 KB, yaitu setiap 4 KB data tertulis akan dihitung sebagai satu WCU.
Jumlah dasar WCU adalah 4 KB. Ukuran permintaan di bawah 4 KB dihitung sebagai 4 KB, dan ukuran permintaan di atas 4 KB dihitung sebagai kelipatan 4 KB (sisa di bawah 4 KB dihitung sebagai 4 KB).
Anda dapat memilih apakah akan mengaktifkan fitur flag hasil saat melakukan operasi tulis. Jika diaktifkan, sistem akan secara otomatis menghitung CU yang dikembalikan sebagai WCU.
Jumlah WCU yang digunakan = CU yang dihasilkan oleh penulisan data + CU yang dikembalikan

Di bawah ini adalah contoh:
- **Write request** (Tulis permintaan)
  Anda mengirim permintaan untuk memperbarui konten 5 KB, dan backend membaca catatan (total 50 KB) yang berisi data target dari disk ke dalam memori.
  Kemudian, backend memperbarui catatan dan membuang konten 50 KB ke dalam disk setelah pembaruan.
  Jika telah mengaktifkan flag hasil, konten 5 KB akan dikembalikan.
- **Result flag enabled** (Flag hasil diaktifkan)
  13 CU (50 KB data yang ditulis ke dalam disk) + 2 CU (5 KB data yang dikembalikan) = 15 WCU yang dihasilkan
- **Result flag not enabled** (Flag hasil tidak diaktifkan)
  13 CU (50 KB data yang ditulis ke dalam disk) = 13 WCU yang dihasilkan

### Mode prasetel
Jika memilih mode prasetel, Anda perlu menyesuaikan kapasitas baca/tulis tabel prasetel berdasarkan perubahan akses. Operasi ini dapat membantu mengontrol penggunaan TcaplusDB agar tetap pada atau di bawah tingkat permintaan yang ditentukan sehingga Anda dapat memprediksi biayanya.
Untuk mengonfigurasi kapasitas prasetel dengan lebih baik, Anda perlu memperkirakan lalu lintas aplikasi terlebih dahulu.

#### Baca cadangan
Ini mengacu pada prakonfigurasi RCU dari tabel. Anda perlu memperkirakan konsumsi RCU tertinggi per detik dari tabel pada hari itu dan menetapkan nilainya sebagai RCU yang dicadangkan.

#### Tulis cadangan
Ini mengacu pada prakonfigurasi WCU dari tabel. Anda perlu memperkirakan konsumsi WCU tertinggi per detik dari tabel pada hari itu dan menetapkan nilainya sebagai WCU yang dicadangkan.

#### Kapasitas cadangan
Ini mengacu pada prakonfigurasi penggunaan kapasitas disk dari tabel. Anda perlu memperkirakan kapasitas yang digunakan oleh tabel pada hari itu.

#### Permintaan batas dan kuota
Karena nilai RCU atau WCU yang dikonfigurasi mungkin terlalu rendah atau jumlah permintaan akses mungkin melonjak, TcaplusDB membatasi permintaan yang melebihi 40% RCU atau WCU cadangan secara default. Batas ini tidak memblokir permintaan; sebaliknya, ini membuat permintaan mengantre untuk mengurangi frekuensi akses yang dapat menyebabkan waktu habis dalam program. Anda dapat menggunakan fitur pemantauan dan peringatan untuk mengetahui apakah jumlah permintaan saat ini melebihi kapasitas yang telah dikonfigurasikan sebelumnya.

Batas ini dapat mencegah aplikasi Anda menggunakan terlalu banyak CU. Namun, jika permintaan terbatas, permintaan tersebut akan gagal, dan banyak kesalahan sistem akan terjadi.

Anda dapat menggunakan pemantauan tabel TcaplusDB untuk memantau RCU/WCU aktual dan memodifikasi kuota tabel jika perlu.
