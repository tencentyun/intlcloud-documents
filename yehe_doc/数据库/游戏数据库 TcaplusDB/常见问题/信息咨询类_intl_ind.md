- [Apakah TcaplusDB mendukung penghapusan data?](#41)
- [Bagaimana struktur data TcaplusDB?](#43)
- [Berapa kapasitas memori instans tunggal dan penggunaan CPU dari TcaplusDB SDK?](#67)
- [Berapa banyak tabel dalam grup tabel di TcaplusDB?](#68)
- [Apa batasan pada bidang kunci dan nilai di TcaplusDB?](#69)
- [Berapa lama file cadangan TcaplusDB akan disimpan?](#72)
- [Apakah server game terhubung ke semua tcaproxy (lapisan akses)?](#73)
- [Bagaimana cara melakukan analisis data TcaplusDB?](#74)
- [Berapa ukuran maksimum tabel tunggal di TcaplusDB? Berapa batas jumlah catatan?](#82)
- [Apakah TcaplusDB mendukung operasi transaksi multi-tabel dan operasi penulisan batch?](#85)
- [Apakah peningkatan TcaplusDB API kompatibel dengan versi sebelumnya?](#88)

<span id="41"></span>
### Apakah TcaplusDB mendukung penghapusan data?
TcaplusDB mendukung penghapusan data tingkat tabel, tempat data dihapus sesuai dengan terakhir kali ditulis.

<span id="43"></span>
### Apa saja struktur data TcaplusDB?
TcaplusDB mendukung struktur data seperti berbagai daftar, kueri berdasarkan bagian kunci (indeks), nilai kunci, objek kunci (yaitu, nilai kunci tunggal dapat berupa struktur data arbitrer, misalnya, server game dapat membuat serial `lua table` ke dalam bidang nilai).

<span id="67"></span>
### Berapa kapasitas memori instans tunggal dan penggunaan CPU dari TcaplusDB SDK?
Pemakaian memori instans tunggal maksimum adalah 73 MB, dan penggunaan CPU maksimum adalah 30%.

<span id="68"></span>
### Berapa banyak tabel dalam grup tabel di TcaplusDB?
Di TcaplusDB, grup tabel dapat memiliki hingga 256 tabel. Jika ada lebih dari 256 tabel dalam grup tabel, Anda dapat menambahkan grup tabel baru atau menggabungkan tabel. Jika Anda memerlukan dukungan teknis, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category) dan pilih **Other** (Lainnya) di halaman **Select the related product** (Pilih produk terkait).

<span id="69"></span>
### Apa batasan pada bidang kunci dan nilai di TcaplusDB?
Jumlah bidang kunci dari tabel umum adalah 4, jumlah bidang kunci dari tabel daftar adalah 3, dan ukuran bidang kunci tunggal adalah 1.024 B. Jumlah bidang nilai dari tabel generik adalah 128, jumlah bidang nilai tabel daftar adalah 127, ukuran bidang nilai tunggal adalah 256 KB, dan ukuran maksimum catatan adalah 1 MB.

<span id="72"></span>
### Berapa lama file cadangan TcaplusDB akan disimpan?
File mesin yang dicadangkan oleh TcaplusDB disimpan selama 7 hari, dan Ulog disimpan selama 7 hari. Periode penyimpanan di lingkungan TcaplusDB berbeda-beda. Untuk periode penyimpanan lingkungan TcaplusDB tertentu, Anda dapat [menghubungi layanan pelanggan](https://intl.cloud.tencent.com/support).

<span id="73"></span>
### Apakah server game terhubung ke semua tcaproxy (lapisan akses)?
Untuk mengurangi biaya pemeliharaan koneksi TCP antara server game dan tcaproxy (lapisan akses), server game mendukung pemilihan beberapa tcaproxy (lapisan akses) untuk membuat koneksi.

<span id="74"></span>
### Bagaimana cara melakukan analisis data pada data TcaplusDB?
Data TcaplusDB dapat diekspor dalam format apa pun, termasuk json, pb, dan format lainnya, dan dapat diimpor ke sistem analisis data seperti TDW. TcaplusDB mendukung impor data real-time ke database MySQL dan sebagainya.

<span id="82"></span>
### Berapa ukuran maksimum satu tabel di TcaplusDB? Berapa batasan jumlah catatan?
Satu tabel dapat dibagi lagi menjadi 10.000 pecahan data, setiap pecahan data berukuran 256 GB, yaitu, ukuran total satu tabel adalah 10.000 * 256 GB. Satu tabel tidak memiliki batasan jumlah catatan, dan jumlah catatan dalam satu tabel terkait dengan ukuran catatan tunggal.

<span id="85"></span>
### Apakah TcaplusDB mendukung operasi transaksi multi-tabel dan operasi penulisan batch?
TcaplusDB tidak mendukung operasi transaksi multi-tabel atau operasi penulisan batch. Untuk melakukan operasi transaksi multi-tabel, perubahan harus dilakukan di sisi bisnis Anda. Di TcaplusDB, operasi harus dilakukan secara berurutan. Misalnya, ketika beberapa operasi dikirimkan secara bersamaan, semua operasi yang telah selesai akan dibatalkan jika salah satu dari operasi berikutnya gagal. Setelah pemutaran kembali, Anda dapat mengirimkan operasi ini lagi. Untuk operasi penting, sebaiknya simpan log.

<span id="88"></span>
### Apakah peningkatan TcaplusDB API kompatibel dengan versi sebelumnya?
Peningkatan TcaplusDB API kompatibel dengan versi sebelumnya, dan API, kata perintah, dan fitur yang ada tidak akan dimodifikasi.
