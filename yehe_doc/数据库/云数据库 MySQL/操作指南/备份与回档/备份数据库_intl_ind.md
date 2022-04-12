Untuk menghindari kerugian atau kerusakan data, Anda dapat membuat cadangan database secara otomatis atau manual.

## Ikhtisar Cadangan
### Mode cadangan
Instans TencentDB for MySQL dua node dan tiga node mendukung **automatic backup** (pencadangan otomatis) dan **manual backup** (pencadangan manual) database.

### Jenis cadangan
Instans TencentDB for MySQL dua node dan tiga node mendukung dua jenis cadangan:
- **Physical backup** (Cadangan fisik), yang mereplikasi data fisik lengkap (tersedia untuk cadangan otomatis dan manual).
- **Logical backup** (Cadangan logis), yang mencadangkan pernyataan SQL (hanya tersedia untuk cadangan manual).
>?
>- Untuk memulihkan database dari cadangan fisik, xbstream diperlukan untuk mendekompresi file cadangan terlebih dahulu. Untuk informasi selengkapnya, lihat [Memulihkan Database dari Cadangan Fisik](https://intl.cloud.tencent.com/document/product/236/31910).
>- Jika jumlah tabel dalam satu instans melebihi satu juta, cadangan mungkin gagal dan pemantauan database mungkin terpengaruh. Harap pastikan jumlah tabel dalam satu instans tidak lebih dari satu juta.
>- Karena data tabel yang dibuat oleh mesin penyimpanan MEMORY disimpan dalam memori, cadangan fisik tidak dapat dibuat untuk tabel tersebut. Untuk menghindari kehilangan data, sebaiknya konversi data ke tabel InnoDB.
>- Jika ada banyak tabel dalam instans tanpa kunci utama, cadangan mungkin gagal dan ketersediaan tinggi instans mungkin terpengaruh. Harap buat kunci utama atau indeks sekunder untuk tabel tersebut.

| Keuntungan Cadangan Fisik | Kerugian Cadangan Logis |
|---------|---------|
| <li>Kecepatan cadangan tinggi. <li>Cadangan dan kompresi streaming didukung. <li>Tingkat keberhasilan yang tinggi. <li>Pemulihan sederhana dan efisien. <li>Operasipenyandingan berbasis pencadangan yang lebih cepat seperti menambahkan replika baca saja dan instans pemulihan bencana. <li>1/8 dari waktu rata-rata yang dibutuhkan untuk membuat cadangan logis. <li>Sepuluh kali lebih cepat daripada cadangan logis selama proses impor. | <li>Diperlukan waktu lama untuk memulihkan karena memakan waktu untuk menjalankan pernyataan SQL dan membangun indeks. <li>Kecepatan pencadangan rendah, terutama ketika ada sejumlah besar data. <li>Kemungkinan peningkatan penundaan replika sumber karena tekanan pada instans selama cadangan. <li>Kemungkinan hilangnya informasi presisi dari titik floating. <li>Potensi kegagalan cadangan karena pandangan yang salah dan masalah lainnya. <li>Operasipenyandingan berbasis cadangan yang lebih lambat seperti menambahkan replika baca saja dan instans pemulihan bencana. |

### Objek cadangan
| Cadangan Data | Cadangan Log |
|---------|---------|
| TencentDB for MySQL dua node dan tiga node: <li>Cadangan otomatis mendukung pencadangan fisik penuh. <li>Cadangan manual mendukung pencadangan fisik penuh, cadangan logis penuh, dan cadangan logis database tunggal/tabel. <li>Cadangan otomatis dan manual dapat dikompresi dan diunduh. | TencentDB for MySQL dua-node dan tiga-node mendukung cadangan binlog: <li>File log menempati ruang cadangan instans. <li>File log dapat diunduh tetapi tidak dapat dikompresi. <li>Periode penyimpanan dapat diatur untuk file log. |

## Catatan
- Sejak 26 Februari 2019, fitur cadangan otomatis TencentDB for MySQL hanya mendukung cadangan fisik (jenis default) dan tidak lagi menyediakan cadangan logis. Cadangan logis otomatis yang ada akan dialihkan ke cadangan fisik secara otomatis.
Tindakan ini tidak akan memengaruhi akses bisnis Anda, tetapi dapat memengaruhi kebiasaan cadangan otomatis Anda. Jika memerlukan cadangan logis, Anda dapat menggunakan fitur cadangan manual di [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb) atau memanggil [CreateBackup API](https://intl.cloud.tencent.com/document/product/236/15844) untuk membuat cadangan logis.
- File cadangan instans menempati ruang cadangan. Sebaiknya rencanakan penggunaan ruang cadangan dengan tepat. Penggunaan ruang cadangan yang melebihi tier gratis akan dikenakan biaya. Untuk informasi selengkapnya, harap lihat [Penagihan Ruang Cadangan](https://intl.cloud.tencent.com/document/product/236/32344).
- Cadangkan data Anda selama jam normal.
- Sebaiknya unduh file cadangan secara lokal sebelum dihapus setelah periode penyimpanan berakhir.
- Jangan melakukan operasi DDL selama proses cadangan untuk menghindari kegagalan cadangan karena penguncian tabel.
- Instans TencentDB for MySQL node tunggal tidak dapat dicadangkan.

## Mencadangkan Data MySQL Secara Otomatis
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans pada halaman daftar instans untuk mengakses halaman manajemen instans, dan pilih **Backup and Restore** (Cadangkan dan Pulihkan) > **Auto Backup Settings** (Pengaturan Cadangan Otomatis).
![](https://main.qcloudimg.com/raw/69fed1aac393a518bd8cc2ad1fea550f.png)
2. Pilih parameter cadangan di jendela pop-up (detail ditampilkan seperti di bawah) dan klik **OK** (OKE):
>?
>?[Fitur pengembalian](https://intl.cloud.tencent.com/document/product/236/7276) bergantung pada siklus cadangan dan hari dari penyimpanan cadangan data dan cadangan log (binlog). Pengembalian akan terpengaruh jika Anda mengurangi frekuensi cadangan otomatis dan periode penyimpanan. Harap pilih parameter sesuai kebutuhan.
>Misalnya, jika siklus pencadangan diatur pada hari Senin dan Kamis dan periode penyimpanan ditetapkan sebagai tujuh hari, Anda dapat mengembalikan database ke titik waktu mana pun dalam tujuh hari terakhir (yang merupakan hari penyimpanan aktual dari cadangan data dan cadangan log).
>- Cadangan otomatis tidak dapat dihapus secara manual. Anda dapat mengatur periode penyimpanan untuk cadangan otomatis, dan cadangan akan dihapus secara otomatis saat habis masa berlakunya.
>
<table>
<thead><tr><th>Parameter</th><th>Deskripsi</th></tr></thead>
<tbody>
<tr>
<td>Jadwal Cadangan</td><td>Untuk memastikan keamanan data, lakukan cadangan data minimal dua kali seminggu. Semua tujuh hari dalam seminggu akan dipilih secara default.</td></tr>
<tr>
<td>Waktu Mulai Cadangan</td><td><ul><li>Waktu mulai cadangan default ditetapkan secara otomatis oleh sistem. <li>Anda dapat mengatur waktu mulai sesuai kebutuhan. Sebaiknya atur ke jam normal. Ini hanyalah waktu mulai dari proses pencadangan dan tidak menunjukkan waktu akhir. <br>Misalnya, jika waktu mulai cadangan diatur pada pukul 02.00-06.00, sistem akan memulai cadangan pada suatu waktu selama pukul 02.00-06.00, yang bergantung pada kebijakan pencadangan backend dan kondisi sistem cadangan.</td></tr>
<tr>
<td>Waktu Penyimpanan Cadangan Data</td><td>File cadangan data dapat disimpan selama 7 (nilai default) hingga 1830 hari.</td></tr>
<tr>
<td>Waktu Penyimpanan Cadangan Log</td><td>File cadangan log dapat disimpan selama 7 (nilai default) hingga 1830 hari. </td></tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/a371d4ba960264aa5630b59a3bfe5096.png"  style="margin:0;">

## [Mencadangkan Data MySQL Secara Manual](id:manual-backup)
Fitur cadangan manual memungkinkan Anda memulai tugas pencadangan secara manual.
>?
>- Cadangan manual mendukung cadangan fisik penuh, cadangan logis penuh, dan cadangan logis database/tabel tunggal.
>- Cadangan manual dapat dihapus secara manual dari daftar cadangan di konsol. Anda dapat menghapus cadangan manual yang tidak lagi digunakan untuk mengosongkan ruang. Cadangan manual dapat disimpan secara permanen selama tidak dihapus.
>- Saat instans melakukan cadangan otomatis harian, tidak ada tugas cadangan manual yang dapat dimulai.
>
1. Pada halaman daftar instans, klik ID instans untuk mengakses halaman manajemen instans, dan pilih **Backup and Restore** (Cadangkan dan Pulihkan) > **Manual Backup** (Cadangan Manual).
2. Pilih mode dan objek cadangan di jendela pop-up, lalu klik **OK** (OKE).
![](https://main.qcloudimg.com/raw/a16e644f51756b6a98597945e45329cd.png)
>?Untuk cadangan logis database tunggal/tabel, pilih database atau tabel yang akan dicadangkan di **Select database & table** (Pilih database & tabel) di kolom kiri dan tambahkan item yang dipilih ke kolom kanan. Jika belum memiliki database, harap buat database/tabel terlebih dahulu.
>
![](https://main.qcloudimg.com/raw/76924e2c76ac348b68ed113d679d6907.png)

## Pertanyaan Umum
#### 1. Dapatkah saya mengunduh atau memulihkan file cadangan yang melebihi periode penyimpanan?
Kumpulan cadangan yang kedaluwarsa akan dihapus secara otomatis dan tidak dapat diunduh atau dipulihkan.
- Sebaiknya konfigurasikan periode penyimpanan cadangan berdasarkan kebutuhan bisnis atau mengunduh file cadangan secara lokal melalui [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb).
- Anda juga dapat mencadangkan data instans secara manual di konsol. Cadangan manual akan disimpan secara permanen.
>?Cadangan manual juga akan memerlukan ruang cadangan. Sebaiknya rencanakan penggunaan ruang cadangan dengan tepat untuk mengurangi biaya.

#### 2. Bisakah saya menghapus cadangan secara manual?
- Cadangan otomatis tidak dapat dihapus secara manual. Anda dapat mengatur periode penyimpanan untuk cadangan otomatis, dan cadangan akan dihapus secara otomatis saat habis masa berlakunya. 
- Cadangan manual dapat dihapus secara manual dari daftar cadangan di [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Cadangan manual dapat disimpan secara permanen selama tidak dihapus.

#### 3. Bisakah saya menonaktifkan cadangan data dan log?
Tidak. Namun, Anda dapat mengurangi frekuensi cadangan dan menghapus cadangan manual yang tidak lagi digunakan melalui [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb) untuk menurunkan penggunaan kapasitas.

#### 4. Bagaimana cara mengurangi biaya kapasitas cadangan?
- Hapus cadangan manual yang tidak lagi digunakan (Anda dapat login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans untuk mengakses halaman manajemen instans, dan hapus cadangan manual di tab **Backup and Restore** (Cadangkan dan Pulihkan)). 
- Kurangi frekuensi cadangan data otomatis untuk bisnis non-inti (Anda dapat menyesuaikan siklus cadangan dan periode penyimpanan di konsol, dan frekuensinya harus setidaknya dua kali seminggu).
>?[Fitur pengembalian](https://intl.cloud.tencent.com/document/product/236/7276) bergantung pada siklus pencadangan dan hari penyimpanan pencadangan data dan cadangan log (binlog). Pengembalian akan terpengaruh jika Anda mengurangi frekuensi cadangan otomatis dan periode penyimpanan. Harap pilih parameter sesuai kebutuhan.
>
- Kurangi periode penyimpanan data dan pencadangan log untuk bisnis non-inti (periode penyimpanan 7 hari dapat memenuhi persyaratan sebagian besar skenario).

| Skenario Bisnis             | Periode Penyimpanan Cadangan yang Direkomendasikan                                                 |
| -------------------- | ------------------------------------------------------------ |
| Bisnis inti             | 7-1830 hari                                              |
| Bisnis non-inti dan non-data | 7 hari                                                      |
| Bisnis arsip             | 7 hari. Sebaiknya cadangkan data secara manual berdasarkan kebutuhan bisnis Anda dan segera hapus cadangan setelah digunakan |
| Bisnis pengujian | 7 hari. Sebaiknya cadangkan data secara manual berdasarkan kebutuhan bisnis Anda yang sebenarnya dan segera hapus cadangan setelah digunakan |

