
## Ikhtisar
TencentDB for MySQL tidak akan mengubah data Anda. Data yang rusak karena alasan pribadi dapat dipulihkan melalui pengembalian secara mandiri. Fitur pengembalian disediakan untuk mengembalikan database atau tabel di Tencent Cloud berdasarkan cadangan data dan cadangan binlog. Pengembalian data real-time didukung.

Dengan menyusun ulang citra berkala dan transaksi real-time, fitur pengembalian TencentDB for MySQL dapat memutar kembali database atau tabel ke titik waktu yang ditentukan dan irisan waktu dari semua data dijamin identik. Database atau tabel baru akan dibuat dalam instans asli, dan selama proses tersebut, database atau tabel asli dapat diakses secara normal. Setelah pengembalian selesai, Anda dapat melihat database atau tabel baru dan asli.

## Cara Kerja Pengembalian
Fitur pengembalian dapat mengembalikan database atau tabel ke titik waktu tertentu berdasarkan `cadangan data cold dan cadangan binlog yang sesuai`.
![](https://main.qcloudimg.com/raw/89ab32296ba576cf8e087d760b5a8109.png)
1. Data diekspor dari replika MySQL dan diimpor ke sistem cadangan cold setiap hari.
2. Untuk mengembalikan database atau tabel, minta instans pengembalian sementara dari sistem pengembalian. Ekspor data dingin dari sistem cadangan cold dan impor ke instans pengembalian temp (jenis data yang diimpor berbeda-beda tergantung pada metode pengembalian).
3. Buat hubungan sumber-replika antara instans pengembalian dan instans sumber MySQL, atur waktu pengembalian, dan tentukan database atau tabel yang akan dikembalikan.
4. Replikasi database atau tabel pengembalian ke instans sumber MySQL.

## Batasan Fitur
- Hanya instans sumber yang dapat dibatalkan. Replika baca saja atau instans pemulihan bencana tidak dapat dibatalkan.
- Hanya database atau tabel tertentu yang dapat dikembalikan. Database atau tabel setelah pengembalian akan diganti namanya dan direplikasi ke instans sumber.

## Catatan
- Fitur pengembalian tunduk pada siklus pencadangan dan hari penyimpanan yang ditetapkan untuk pencadangan otomatis. Hal ini memungkinkan pengembalian data berdasarkan pencadangan data dan pencadangan binlog sesuai dengan hari penyimpanan yang dikonfigurasi dan siklus pencadangan. Untuk pengaturan siklus pencadangan, harap lihat [Mencadangkan Data MySQL Secara Otomatis](https://intl.cloud.tencent.com/document/product/236/37796). Untuk memastikan keamanan data MySQL, atur siklus pencadangan otomatis setidaknya dua kali seminggu.
- Jika database atau tabel yang akan dikembalikan tidak ada atau telah dihapus, Anda harus login ke instans TencentDB dan membuatnya terlebih dahulu sebelum melakukan pengembalian di konsol.
- Jika cadangan cold sebelum pengembalian tidak berisi tabel, pengembalian akan gagal.

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, pilih satu atau beberapa instans dan klik **More** (Lainnya) > **Rollback** (Pengembalian).
>?
>- Jika pengembalian hanya dilakukan pada satu instans, Anda juga dapat membuka halaman manajemen instans dan mengklik **Rollback** (Pengembalian) di sudut kanan atas.
>- Hingga 5 tugas pengembalian dapat dimulai pada satu waktu di bawah APPID yang sama.
>
![](https://main.qcloudimg.com/raw/abd517cf8b6db3db57b622f13d365893.png)
2. Pada halaman pengembalian, atur metode pengembalian (dijelaskan seperti di bawah), pilih database atau tabel yang akan dikembalikan, dan klik **Next step: set the rollback time and database table name** (Langkah selanjutnya: atur waktu pengembalian dan nama tabel database).
   - Cepat: cadangan penuh instans diimpor, dan database atau tabel yang dipilih akan dikembalikan. Mode pengembalian ini lambat tetapi tidak memiliki batas.
   - Lebih cepat: cadangan penuh dan binlog tingkat database diimpor. Untuk operasi lintas database, jika database terkait tidak dipilih pada saat yang sama, pengembalian mungkin gagal.
   - Sangat cepat: cadangan penuh dan binlog tingkat tabel diimpor. Untuk operasi lintas tabel, jika tabel terkait tidak dipilih pada saat yang sama, pengembalian mungkin gagal.
>?
>- Hanya database/tabel yang namanya berisi angka, huruf, garis bawah, atau kombinasinya yang dapat dibatalkan. Database/tabel dengan nama yang mengandung karakter khusus tidak didukung.
>- Dalam mode saat database/tabel tertentu hanya dapat dikembalikan, maksimum 500 database/tabel dalam instans yang sama dapat dikembalikan sekaligus.
>- Jika pengembalian melibatkan operasi gabungan pada database atau tabel lain selama eksekusi binlog, pernyataan SQL mungkin gagal.
>- Jika pengembalian melibatkan kunci asing dan batasan tabel lainnya selama eksekusi binlog, pernyataan SQL mungkin gagal.
>
![](https://main.qcloudimg.com/raw/6cb2fa4d3e8b0d795bd5bf19f8d69d86.png)
3. Atur database setelah dikembalikan atau nama tabel dan waktu pengembalian, lalu klik **Rollback** (Pengembalian).
>?
>- Waktu pengembalian hanya dapat diatur sekali waktu untuk setiap instans.
>- Jika Anda memilih untuk mengatur waktu pengembalian batch, semua database atau tabel akan dikembalikan pada waktu yang ditentukan.
>- Jika Anda memilih untuk mengatur waktu pengembalian satu tabel, tabel akan dikembalikan pada waktu pengembalian masing-masing.
>- Nama database atau tabel setelah pengembalian dapat berisi hingga 64 huruf, angka, atau simbol (.-\_$).
>
![](https://main.qcloudimg.com/raw/62377981b147bdb453d79631b3557d12.png)
4. Setelah pengiriman, buka **Operation Log** (Log Operasi) > **Rollback Log** (Log Pengembalian) untuk melihat kemajuan pengembalian. Klik **View Details** (Lihat Detail) untuk melihat log pengembalian secara real-time.
![](https://main.qcloudimg.com/raw/b5206b3c23d532553fb54dfc4fe7bfd0.png)
5. Setelah pengembalian selesai, buka **Database Management** (Manajemen Database) > **Database List** (Daftar Database) untuk melihat database atau tabel baru setelah pengembalian di instans asli.
![](https://main.qcloudimg.com/raw/9b939d9a6a7da59092df0051f452b5cd.png)

