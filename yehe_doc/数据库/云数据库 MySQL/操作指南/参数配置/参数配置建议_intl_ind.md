Parameter di TencentDB for MySQL telah dioptimalkan berdasarkan nilai default resmi di MySQL. Kami sarankan Anda mengonfigurasi parameter berikut untuk instans TencentDB for MySQL setelah pembelian berdasarkan skenario bisnis Anda.

### character_set_server
- Nilai default: UTF8
- Diperlukan mulai ulang: ya
- Deskripsi: mengonfigurasi kumpulan karakter default untuk server MySQL. TencentDB for MySQL menawarkan empat kumpulan karakter: LATIN1, UTF8, GBK, dan UTF8MB4. Di antara mereka, LATIN1 mendukung karakter bahasa Inggris, dengan satu karakter memiliki satu byte; UTF8 umumnya digunakan untuk pengkodean internasional yang berisi semua karakter yang digunakan oleh semua negara, dengan satu karakter memiliki tiga byte; di GBK, setiap karakter memiliki dua byte; dan UTF8MB4 (superset dari UTF8) sepenuhnya kompatibel dan mendukung emoji, dengan satu karakter memiliki empat byte.
- Rekomendasi: setelah membeli instans, Anda perlu memilih kumpulan karakter yang sesuai berdasarkan format data yang diperlukan dalam bisnis Anda untuk memastikan bahwa klien dan server menggunakan kumpulan karakter yang sama, mencegah teks kacau dan mulai ulang yang tidak perlu.

### lower_case_table_names
- Nilai default: 0
- Diperlukan mulai ulang: ya
- Deskripsi: saat membuat database atau tabel, Anda dapat mengatur apakah penyimpanan dan operasi kueri peka huruf besar/kecil. Parameter ini dapat diatur ke 0 (peka huruf besar/kecil) atau 1 (peka huruf besar/kecil). Nilai defaultnya adalah 0.
- Rekomendasi: TencentDB for MySQL peka huruf besar-kecil secara default. Kami sarankan Anda mengonfigurasi parameter ini berdasarkan kebutuhan bisnis dan kebiasaan penggunaan Anda.

### sql_mode
- Nilai dasar:
```
NO_ENGINE_SUBSTITUTION (v5.6); ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION (v5.7)
```
- Diperlukan mulai ulang: tidak
- Keterangan: TencentDB for MySQL dapat beroperasi dalam mode SQL yang berbeda, yang menentukan sintaksis SQL dan pemeriksaan data yang harus didukungnya.
Nilai default parameter ini di v5.6 adalah `NO_ENGINE_SUBSTITUTION`, yang berarti bahwa jika mesin penyimpanan yang digunakan dinonaktifkan atau tidak dikompilasi, kesalahan akan muncul; di v5.7, nilai defaultnya adalah `ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION`.
Catatan:
 - Jika `ONLY_FULL_GROUP_BY` diaktifkan, MySQL menolak kueri yang daftar pilih, kondisi `HAVING`, atau daftar `ORDER BY` merujuk ke kolom nonagregasi yang tidak disebutkan namanya dalam klausul `GROUP BY` atau secara fungsional bergantung pada kolom `GROUP BY`.
 - `STRICT_TRANS_TABLES` mengaktifkan mode SQL yang ketat. `NO_ZERO_IN_DATE` mengontrol apakah server mengizinkan tanggal di mana bagian tahun bukan nol tetapi bagian bulan atau hari adalah nol. Efek `NO_ZERO_IN_DATE` bergantung pada apakah mode SQL ketat diaktifkan.
 - `NO_ZERO_DATE` mengontrol apakah server mengizinkan tanggal nol sebagai valid. Efeknya tergantung pada apakah mode SQL ketat diaktifkan.
 - `ERROR_FOR_DIVISION_BY_ZERO` berarti bahwa dalam mode SQL ketat, jika data dibagi dengan nol selama proses INSERT atau UPDATE, kesalahan daripada peringatan akan dihasilkan, sedangkan dalam mode SQL non-ketat, NULL akan dikembalikan.
 - `NO_AUTO_CREATE_USER` melarang pernyataan GRANT membuat pengguna yang kata sandinya kosong.
 - `NO_ENGINE_SUBSTITUTION` berarti jika mesin penyimpanan dinonaktifkan atau tidak dikompilasi, kesalahan akan terjadi.
- Rekomendasi: karena mode SQL yang berbeda mendukung sintaksis SQL yang berbeda, kami sarankan Anda untuk mengonfigurasinya berdasarkan kebutuhan bisnis dan kebiasaan pengembangan Anda.

### long_query_time
- Nilai default: 10
- Diperlukan mulai ulang: tidak
- Deskripsi: digunakan untuk menentukan ambang waktu untuk kueri lambat, dengan nilai default sebagai 10 detik. Jika eksekusi kueri membutuhkan waktu 10 detik atau lebih, detail eksekusi akan dicatat dalam log lambat untuk analisis di masa mendatang.
- Rekomendasi: karena skenario bisnis dan sensitivitas kinerja dapat berbeda-beda, kami sarankan Anda menetapkan nilai dengan mempertimbangkan analisis kinerja di masa mendatang.

