
## Batas Volume Data
TencentDB for MySQL memberlakukan pembatasan volume data pada semua jenis instans MySQL untuk mengisolasi masalah performa karena sumber daya yang terbatas. Dokumen ini menjelaskan dampak teknis dari satu instans atau tabel dengan volume data yang besar di MySQL.

**Instance with a high data volume** (Instans dengan volume data tinggi): mesin penyimpanan default untuk TencentDB adalah InnoDB. Jika buffer cache dapat menyimpan semua data dan halaman indeks dalam instans MySQL, instans dapat mendukung sejumlah besar permintaan akses bersamaan. Jika instans berisi terlalu banyak data, cache dan buffer akan sering bertukar data masuk/keluar; dalam hal ini, kendala performa MySQL akan segera menyebar ke IO, yang akan mengurangi throughput. Misalnya, instans TencentDB yang dirancang untuk mempertahankan hingga 8.000 permintaan akses per detik hanya dapat mendukung 700 permintaan akses per detik jika volume data dua kali ukuran cache dan buffer.

**Table with a high data volume** (Tabel dengan volume data tinggi): jika tabel berisi terlalu banyak data, biaya MySQL untuk mengelola sumber daya tabel (data, indeks, dll.) akan berubah, sehingga akan memengaruhi efisiensi pemrosesan tabel. Misalnya, jika ukuran tabel transaksi (InnoDB) melebihi 10 GB, latensi dalam operasi pembaruan akan meningkat, sehingga meningkatkan waktu respons untuk transaksi. Dalam hal ini, masalahnya hanya dapat diselesaikan melalui sharding dan migrasi.

>?Jika jumlah tabel dalam satu instans melebihi satu juta, pencadangan, pemantauan, dan peningkatan mungkin gagal dan pemantauan database mungkin terpengaruh. Pastikan jumlah tabel dalam satu instans di bawah satu juta.

## Batas Koneksi Maksimum
Jumlah maksimum koneksi ke instans MySQL ditentukan dengan variabel sistem MySQL `max_connections`. Ketika jumlah aktual melebihi `max_connections`, tidak ada lagi koneksi yang dapat dibuat.
Jumlah default koneksi ke TencentDB dapat dilihat dengan mengklik ID instans untuk masuk ke halaman **Database Management** (Pengelolaan Database) > **Parameter Settings** (Pengaturan Parameter) di [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), yang dapat disesuaikan sesuai kebutuhan. Namun, lebih banyak koneksi berarti lebih banyak sumber daya sistem yang akan dikonsumsi; jika jumlah koneksi melampaui apa yang dimungkinkan oleh kapasitas beban aktual pada sistem, kualitas layanan sistem pasti akan mengalami gangguan.
Untuk informasi selengkapnya tentang `max_connections`, lihat [dokumentasi resmi MySQL](https://dev.mysql.com/doc/).

## Batasan Versi Klien MySQL
Sebaiknya gunakan klien dan pustaka MySQL yang disertakan dengan CVM untuk terhubung ke instans TencentDB.

### Catatan tentang kueri yang lambat
- Untuk instans CVM Linux, Anda dapat menggunakan alat ekspor TencentDB untuk mendapatkan log kueri yang lambat. Untuk informasi selengkapnya, lihat [Memulihkan Database dari Cadangan Fisik](https://intl.cloud.tencent.com/document/product/236/31910).
- Untuk instans CVM Windows, log kueri lambat tidak dapat diperoleh secara langsung saat ini. Jika Anda membutuhkannya, [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk mendapatkan bantuan.

### Catatan tentang durasi retensi binlog TencentDB
Binlog TencentDB for MySQL dapat disimpan selama 7 (nilai default) hingga 1830 hari (dapat disesuaikan dengan mengklik ID instans untuk masuk ke halaman **Backup and Restoration** (Cadangan dan Pemulihan) > **Auto-Backup Settings** (Pengaturan Cadangan Otomatis)). 
Jika binlog disimpan untuk waktu yang lama atau berkembang terlalu cepat, ruang tambahan akan diperlukan untuk pencadangan, dan biaya akan dikenakan jika ruang melebihi tingkat kapasitas cadangan gratis.

### Catatan tentang kumpulan karakter
TencentDB for MySQL menggunakan kumpulan karakter UTF8 secara default.
Meskipun TencentDB mendukung pengubahan kumpulan karakter default, sebaiknya tentukan format pengenkodean tabel secara eksplisit saat membuatnya dan tentukan pengenkodean koneksi selama pembuatan koneksi. Dengan cara ini, aplikasi Anda akan lebih portabel.
Untuk informasi selengkapnya tentang sumber daya kumpulan karakter MySQL, lihat [dokumentasi resmi MySQL](https://dev.mysql.com/doc/).

Anda dapat memodifikasi kumpulan karakter melalui SQL atau di konsol TencentDB for MySQL.

#### Memodifikasi kumpulan karakter melalui SQL
1. Jalankan pernyataan SQL berikut untuk mengubah kumpulan karakter default untuk instans TencentDB:
```
SET @@global.character_set_client = utf8;
SET @@global.character_set_results = utf8;
SET @@global.character_set_connection = utf8;
SET @@global.character_set_server = utf8;
```
Setelah pernyataan dijalankan, `@@global.character_set_server` akan secara otomatis disinkronkan ke file lokal untuk persistensi dalam waktu sekitar 10 menit, sedangkan 3 variabel lainnya tidak. Nilai yang dikonfigurasi akan tetap tidak berubah bahkan setelah migrasi atau dimulai ulang.
2. Jalankan pernyataan berikut untuk mengubah pengenkodean kumpulan karakter untuk koneksi saat ini:
```
SET @@session.character_set_client = utf8;
SET @@session.character_set_results = utf8;
SET @@session.character_set_connection = utf8;
```
Atau
```
SET names utf8;
```
3. Untuk program PHP, Anda dapat mengonfigurasi pengenkodean kumpulan karakter untuk koneksi saat ini menggunakan fungsi berikut:
```
bool mysqli::set_charset(string charset);
```
Atau
```
bool mysqli_set_charset(mysqli link, string charset);
```
4. Untuk program Java, Anda dapat mengonfigurasi pengenkodean kumpulan karakter untuk koneksi saat ini seperti yang ditunjukkan di bawah ini:
```
jdbc:mysql://localhost:3306/dbname?useUnicode=true&characterEncoding=UTF-8
```

#### Memodifikasi kumpulan karakter di konsol TencentDB for MySQL
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb) dan klik ID instans di daftar instans untuk masuk ke halaman detail instans.
2. Temukan kumpulan karakter di **Basic Info** (Info Dasar), lalu klik ikon modifikasi untuk memodifikasinya.
![](https://qcloudimg.tencent-cloud.cn/raw/c970624cd5c1424b880719a2708c1e55.png)
3. Di jendela pop-up, pilih kumpulan karakter dan klik **OK** (OKE).
![](https://qcloudimg.tencent-cloud.cn/raw/53466da07103fff22b41c6fa6f5ca4e7.png)

### Batas operasi
1. Jangan memodifikasi informasi dan izin akun yang ada untuk instans MySQL; jika tidak, beberapa layanan kluster mungkin tidak tersedia.
2. InnoDB direkomendasikan untuk membuat database dan tabel, sehingga instans dapat lebih mendukung sejumlah besar permintaan akses bersamaan.
3. Jangan mengubah atau mengakhiri hubungan sumber-replika; jika tidak, pencadangan hot mungkin gagal.

### Batas nama tabel
Nama tabel dalam bahasa Mandarin tidak didukung karena dapat mengakibatkan kegagalan proses seperti pengembalian dan peningkatan.

## Izin Akun Database
TencentDB for MySQL tidak lagi memberikan izin pengguna super. Untuk memodifkasi parameter yang memerlukan izin ini, login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans untuk masuk ke halaman **Database Management** (Manajemen Database) > **Parameter Settings** (Pengaturan Parameter), dan ubah parameter tersebut.

## Pilihan Jaringan
Sebaiknya gunakan VPC. Di VPC, Anda dapat dengan bebas menentukan segmentasi rentang IP, alamat IP, dan kebijakan perutean. Dibandingkan dengan jaringan klasik, VPC lebih cocok untuk skenario yang memerlukan konfigurasi jaringan kustom. Untuk perbandingan VPC dan jaringan klasik, lihat [Mengelola Jaringan](https://intl.cloud.tencent.com/document/product/215/31807).

