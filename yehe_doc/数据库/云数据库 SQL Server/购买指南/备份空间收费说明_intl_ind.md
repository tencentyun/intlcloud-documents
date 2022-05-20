
## Ikhtisar
Ruang cadangan digunakan untuk menyimpan file cadangan semua instans TencentDB for SQL Server di suatu wilayah, termasuk pencadangan data otomatis, pencadangan data manual, dan pencadangan log.

**Backup space range** (Rentang ruang cadangan)
Ruang cadangan akun digunakan untuk menyimpan file cadangan semua instans TencentDB for SQL Server (Edisi Dasar/Edisi Ketersediaan Tinggi/Edisi Kluster) di suatu wilayah. Itu dihitung secara terpisah untuk setiap wilayah; yaitu, file cadangan semua instans di wilayah Beijing dan Shanghai dihitung dalam dua kumpulan sumber daya yang berbeda.

**Backup space composition** (Komposisi ruang cadangan)
File cadangan di ruang cadangan mencakup pencadangan data otomatis, pencadangan data manual, dan pencadangan log.

**Total size of backup files** (Total ukuran file cadangan)
Ukuran total file cadangan di satu wilayah = Volume cadangan data (otomatis + manual) + volume cadangan log (semua nilai untuk wilayah)

**Free backup space** (Ruang cadangan gratis)
TencentDB for SQL Server menawarkan sejumlah ruang cadangan gratis berdasarkan wilayah, yang setara dengan jumlah ruang penyimpanan semua instans utama Edisi Dasar, Edisi Ketersediaan Tinggi, dan Edisi Kluster di suatu wilayah. Untuk contoh perhitungan, lihat [Rumus Perhitungan Ruang Cadangan](#bfkjjsgs).

>?
>- Ruang cadangan gratis hanya tersedia saat Anda membeli instans utama.
>- Ruang cadangan dapat dilihat di halaman pencadangan database di [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver).

## Harga Pencadangan
Cadangan di luar tier gratis (penyimpanan disk 100%) adalah bayar sesuai pemakaian menurut wilayah dengan 0,0001261 ​​USD/GB/jam di daratan Tiongkok dan 0,0001418 USD/GB/jam di luar Tiongkok daratan.
>?Ruang yang dapat ditagih kurang dari 1 GB tidak ditagih, dan jangka waktu yang dapat ditagih kurang dari satu jam dihitung sebagai satu jam.

## Jadwal Penagihan untuk Ruang Pencadangan
Penagihan secara resmi akan dimulai pada pukul 00:00 pada tanggal 1 Juni 2022 untuk cadangan di luar tier gratis.

## [Rumus Perhitungan Ruang Pencadangan](id:bfkjjsgs)
**Free backup space in one region = Sum of the 100% disk storage space (billable space) of all TencentDB for SQL Server instances in the region
Billable backup space in one region = Data backup volume (automatic + manual) + log backup volume - free backup space (all values are for the region)**
(Ruang cadangan gratis di satu wilayah = Jumlah ruang penyimpanan disk 100% (ruang yang dapat ditagih) dari semua instans TencentDB for SQL Server di wilayah tersebut
Ruang cadangan yang dapat ditagih dalam satu wilayah = Volume cadangan data (otomatis + manual) + volume cadangan log - ruang cadangan gratis (semua nilai untuk wilayah))

>!
>- Biaya pencadangan tergantung pada ukuran pencadangan tetapi bukan penggunaan ruang penyimpanan, karena pencadangan tidak menempati ruang penyimpanan.
>- Saat menganalisis biaya pencadangan, Anda perlu memeriksa ukuran cadangan daripada penggunaan ruang penyimpanan.
>- Cadangan instans yang terisolasi juga akan dihitung ke dalam ruang cadangan.

**Calculation example** (Contoh perhitungan)
Jika Anda memiliki instans TencentDB for SQL Server Cluster Edition yang sedang berjalan dengan ruang penyimpanan database yang dibeli sebesar 500 GB/bulan di Zona Beijing 5 dan instans serupa lainnya dengan 200 GB/bulan di Zona Beijing 3, Anda akan mendapatkan ruang cadangan gratis sebesar 700 GB/bulan di wilayah Beijing.

Jika cadangan data Anda mencapai 800 GB dan cadangan log mencapai 100 GB pada jam saat ini, total ruang cadangan yang digunakan di wilayah Beijing akan melebihi 700 GB, dan Anda akan ditagih untuk kelebihan 200 GB (800 + 100 - 700 = 200) untuk jam saat ini dan seterusnya.

## Siklus Hidup Pencadangan
Cadangan instans yang berjalan atau terisolasi akan ditagih hingga dinonaktifkan.

**Pay-as-you-go instance** (Instans bayar sesuai pemakaian)
- Pencadangan dapat berubah selama siklus hidup instans.
- Fitur pencadangan dapat digunakan secara normal dalam waktu 24 jam setelah instans kedaluwarsa, di mana cadangan di luar tier gratis akan tetap ditagih.
- Setelah 24 jam, instans akan diisolasi ke keranjang sampah. Pada titik ini, pengembalian dan pencadangan manual akan dilarang, tetapi pencadangan otomatis masih dapat dilakukan, dan Anda masih dapat mengunduh cadangan (dengan mengeklik **More** (Lainnya) > **Backup Download** (Unduh Cadangan) di kolom **Operation** (Operasi) dari instans di konsol). Anda dapat memperbarui instans di keranjang sampah di konsol untuk memulihkannya.
- Setelah tiga hari isolasi di keranjang sampah (yaitu, pada hari kelima setelah kedaluwarsa), instans akan dinonaktifkan dan dihentikan, bersama dengan semua cadangan data. Dengan demikian, Anda perlu segera menyimpan file cadangan yang diperlukan.

## Pembayaran Jatuh Tempo
**Pay-as-you-go instance** (Instans bayar sesuai pemakaian)
- Setelah akun Anda memiliki pembayaran yang jatuh tempo, cadangan akan berubah dengan siklus hidup instans. Untuk informasi selengkapnya, lihat siklus hidup pencadangan instans bayar sesuai pemakaian.

## Layanan yang Ditingkatkan Tersedia Setelah Penagihan Cadangan Dimulai
| Peningkatan | Sebelum Peningkatan | Setelah Peningkatan |
|---------|---------|---------|
| Periode penyimpanan cadangan data | Tujuh hari secara default. | Dapat disesuaikan antara 3 dan 1.830 hari. |
| Siklus pencadangan data | Sekali setiap 24 jam secara default. | Ini sekali setiap 24 jam secara default jika periode penyimpanan cadangan data kurang dari tujuh hari. Ini dapat disesuaikan jika periode penyimpanan cadangan data lebih dari atau sama dengan tujuh hari; namun, untuk memastikan kesinambungan pencadangan, Anda perlu mengatur dua atau lebih pencadangan setiap minggu. |
| Cadangan log | Cadangan log tidak dapat dilihat atau diunduh. | Cadangan log dapat dilihat dan diunduh. Periode penyimpanan cadangan log sama dengan periode penyimpanan cadangan data yang dikonfigurasi, dan frekuensi pencadangan log adalah sekali setiap 30 menit. |
| Ikhtisar statistik pencadangan tingkat semua instans | Tidak didukung. | Ini didukung dan memudahkan Anda untuk melihat statistik ruang cadangan dan tren semua instans di setiap wilayah di bawah akun Anda, penggunaan tier gratis, serta statistik ruang cadangan real-time dari setiap instans, termasuk: <li>Total cadangan: Menampilkan statistik dan ikhtisar semua pencadangan, pencadangan data, dan pencadangan log.<br><li>Statistik pencadangan real-time: Menampilkan statistik ukuran real-time dari ruang cadangan setiap instans di setiap dimensi. |
| Instans terisolasi | Cadangan tidak dapat dilihat atau diunduh. | Cadangan dapat dilihat dan diunduh. |
| Pengoptimalan pencadangan database tunggal | / | <li>Database dapat dicari berdasarkan nama.<li>Cadangan database tunggal dapat diurutkan berdasarkan ukuran dalam urutan menaik atau menurun.<li>Ukuran file cadangan database tunggal dapat ditampilkan secara gabungan. |
| Pengoptimalan daftar cadangan | / | <li>Cadangan dapat difilter dan dilihat berdasarkan jangka waktu, termasuk semua, hari ini, tujuh hari terakhir, 15 hari terakhir, 30 hari terakhir, dan jangka waktu khusus.<li>Cadangan dapat ditampilkan sebagai dan dicari berdasarkan file.</li> |

## Saran untuk Mengurangi Biaya Pencadangan
- Hapus cadangan manual yang tidak lagi digunakan (di halaman **Instance Management** (Manajemen Instans) > **Backup Management** (Manajemen Cadangan) di [TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver)). 
- Kurangi frekuensi pencadangan data otomatis untuk bisnis non-inti (Anda dapat menyesuaikan siklus pencadangan dan periode penyimpanan file cadangan di konsol, yang harus setidaknya dua kali seminggu).
>?[Fitur pengembalian](https://intl.cloud.tencent.com/document/product/238/7522) bergantung pada siklus pencadangan dan periode penyimpanan pencadangan data dan pencadangan log, tetapi mengurangi frekuensi dan periode penyimpanan pencadangan otomatis akan memengaruhi rentang waktu pengembalian untuk data instans, Anda perlu mengonfigurasikan cadangan dengan tepat berdasarkan kebutuhan aktual Anda.
>
- Mempersingkat periode penyimpanan data dan pencadangan log untuk bisnis non-inti (periode penyimpanan 7 hari dapat memenuhi kebutuhan dalam banyak kasus)

| Skenario Bisnis | Periode Penyimpanan Cadangan yang Direkomendasikan |
| -------------------- | ------------------------------------------------------------ |
| Bisnis inti | 7–1.830 hari |
| Bisnis non-inti, non-data | Tujuh hari |
| Bisnis arsip | Tujuh hari. Sebaiknya cadangkan data secara manual berdasarkan kebutuhan bisnis aktual Anda dan segera menghapus cadangan setelah digunakan |
| Bisnis pengujian | Tujuh hari. KSebaiknya cadangkan data secara manual berdasarkan kebutuhan bisnis aktual Anda dan segera menghapus cadangan setelah digunakan |


