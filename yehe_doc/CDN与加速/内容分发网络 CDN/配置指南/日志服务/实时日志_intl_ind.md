## Ikhtisar Fitur

CDN dapat mengumpulkan dan menerbitkan log akses secara real-time, memungkinkan pengambilan dan analisis data log dengan cepat. Anda dapat mengakses layanan pencatatan log satu atap yang komprehensif, stabil, dan andal dengan cepat seperti pengumpulan log, penyimpanan log, dan pencarian log di konsol CDN.

>? 
>- Log real-time sekarang secara resmi diluncurkan. Anda dapat masuk ke konsol dengan akun root dan mengaktifkannya. Perhatikan bahwa Anda harus menyelesaikan otorisasi dan mengaktifkan [Layanan Log Cloud](https://console.cloud.tencent.com/cls/search?region=ap-shanghai) sebelum menggunakannya untuk pertama kali.
>- Log real-time saat ini tidak mendukung pengiriman log di wilayah di luar Tiongkok Daratan.
>- Log real-time hanya dapat diaktifkan oleh akun root.
>- Nama domain CDN dan ECDN tidak dapat ditambahkan ke topik log yang sama.

## Ikhtisar
Fitur ini dapat digunakan untuk melihat dan menganalisis akses pengguna secara real-time.

## Konsep
### Logset
Logset adalah unit pengelolaan proyek dalam layanan log. Logset digunakan untuk membedakan antara log dengan proyek yang berbeda dan sesuai dengan item atau aplikasi. Logset CDN memiliki atribut dasar berikut:
+ Logset name (Nama logset): cdn_logset
+ Region (Wilayah): [wilayah](https://intl.cloud.tencent.com/document/product/614/18940) tempat logset berada
+ Retention period (Periode penyimpanan): periode penyimpanan data di logset saat ini
+ Creation time (Waktu pembuatan): waktu pembuatan logset

### Topik log
Topik log adalah unit pengelolaan dasar dalam layanan log. Satu logset dapat berisi beberapa topik log, dan satu topik log sesuai dengan satu jenis aplikasi atau layanan. Kami menyarankan agar Anda mengumpulkan log serupa pada komputer yang berbeda ke dalam topik log yang sama. Misalnya, jika proyek bisnis memiliki tiga jenis log: log operasi, log aplikasi, dan log akses, Anda dapat membuat topik log untuk setiap jenis log.

Sistem layanan log mengelola data log yang berbeda berdasarkan topik log yang berbeda. Setiap topik log dapat dikonfigurasi dengan sumber data, aturan indeks, dan aturan pengiriman yang berbeda. Oleh karena itu, topik log adalah unit dasar untuk mengonfigurasi dan mengelola data log di layanan log. Anda harus mengonfigurasi aturan terkait terlebih dahulu setelah membuat topik log sebelum Anda dapat melakukan pengumpulan, pencarian, analisis, dan pengiriman log.

Fitur topik log meliputi:
- Mengumpulkan log untuk mencatat topik.
- Menyimpan dan mengelola log berdasarkan topik log.
- Mencari dan menganalisis log berdasarkan topik log.
- Mengirim log ke platform lain berdasarkan topik log.
- Mengunduh dan mengonsumsi log dari topik log.

## Petunjuk
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), klik **Log Service** (Layanan Log) di bilah samping kiri, dan buka tab **Real-time Log** (Log real-time) untuk membuat pengiriman log real-time.
![](https://main.qcloudimg.com/raw/d6f22b7194f2e3433f9bbee4f4e4a1dc.png)

### Membuat topik log
Klik **Create** (Buat) untuk membuat topik log.
>! Hingga 10 topik log dapat dibuat dalam satu logset.
>
![](https://main.qcloudimg.com/raw/94136aa047219848f82948e19cd8dc06.png)

### Mengonfigurasi topik log
Masukkan nama topik log baru dan pilih nama domain yang akan diikat ke topik ini.
>!
>- Nama topik log baru tidak boleh sama dengan nama topik log yang sudah ada.
>- Nama domain hanya dapat diikat ke satu topik log.
>- Setelah informasi konfigurasi disimpan, diperlukan waktu sekitar 15 menit agar konfigurasi diterapkan.
>
![](https://main.qcloudimg.com/raw/6e820577732ecc679aae25386683c57e.png)

### Mengelola topik log
Setelah berhasil mengonfigurasi topik log, Anda dapat melakukan pengelolaan topik log. Khususnya, Anda dapat menghentikan/memulai pengiriman log ke topik log, mencari log di topik log, mengelola topik log, dan menghapus topik log.
![](https://main.qcloudimg.com/raw/46d8293f0819b693b4b17fa6a79ca78c.png)

#### Menghentikan/Memulai pengiriman log
Anda dapat menghentikan/memulai pengiriman log secara manual ke topik log.
>!
>- Setelah topik log dihentikan, semua log nama domain yang terikat ke topik log tidak akan lagi dikirimkan ke topik log tersebut. Log yang telah dikirim ke topik log tersebut akan disimpan. Operasi ini akan diterapkan dalam waktu sekitar 5–15 menit.
>- Setelah topik log dimulai, semua log nama domain yang terikat ke topik log akan dikirimkan ke topik log tersebut. Operasi ini akan diterapkan dalam waktu sekitar 5–15 menit.

#### String pencarian
Anda dapat mencari log berdasarkan topik log. Pilih topik log yang diinginkan dan klik **Search** (Cari) untuk mengakses halaman pencarian log.
+ Time Range (Rentang Waktu): Anda dapat mencari data log yang dicatat hari ini, selama interval 24 jam (salah satu dari 7 hari terakhir), dan selama 7 hari terakhir.
+ Sort (Urutkan): Anda dapat mengurutkan log dalam urutan menurun atau menaik berdasarkan waktu log.
+ Search (Cari): Pencarian dengan teks lengkap, nilai kunci, atau kata kunci fuzzy didukung. Untuk informasi selengkapnya, silakan lihat [Sintaks Pencarian CLS Lama](https://intl.cloud.tencent.com/document/product/614/37882). Untuk fitur pencarian dan analisis lainnya, gunakan [Layanan Log Cloud](https://console.cloud.tencent.com/cls/search?region=ap-shanghai).

![](https://main.qcloudimg.com/raw/dbc8e4aa6ae93062c22cadf4b9373e64.png)


#### Pengelolaan
Anda dapat mengelola topik log yang dibuat dan memperbarui daftar nama domain yang terikat pada topik log tersebut.
>? Konfigurasi baru akan diterapkan dalam waktu sekitar 5 hingga 15 menit.
>
![](https://main.qcloudimg.com/raw/ce1f6df0d8bde8ce66f7ebfb4a233e6e.png)

#### Menghapus
Anda dapat menghapus topik log secara manual.
>! Setelah topik log dihapus, semua log nama domain yang terikat ke topik log tidak akan lagi dikirimkan ke topik log tersebut, dan log yang telah dikirimkan ke topik log tersebut akan dihapus sepenuhnya. Operasi ini akan diterapkan dalam waktu sekitar 5–15 menit.

### Deskripsi data log

| Bidang Log      | Jenis Log Mentah | Jenis Layanan Log | Deskripsi                                                        |
| ------------- | ------------ | ------------ | ------------------------------------------------------------ |
| id_app       | Integer      | panjang         | Akun Tencent Cloud `APPID`                                             |
| ip_klien     | String       | teks         | IP Klien                                                    |
| ukuran_file     | Integer      | panjang         | Ukuran File                                                     |
| hit           | String       | teks         | Cache hit/miss. Kedua hit di server edge CDN dan simpul induk ditandai sebagai hit |
| host          | String       | teks         | Nama domain                                                         |
| kode_http     | Integer      | panjang         | Kode status HTTP                                                  |
| isp           | String       | teks         | ISP                                                       |
| metode        | String       | teks         | Metode HTTP                                                  |
| param         | String       | teks         | Parameter yang dibawa dalam URL                                              |
| proto         | String       | teks         | Pengidentifikasi protokol HTTP                                                |
| prov          | String       | teks         | Provinsi ISP                                                   |
| referer       | String       | teks         | Informasi referer, yaitu, alamat sumber HTTP                               |
| rentang_permintaan | String       | text         | Parameter rentang, yaitu, rentang permintaan                                         |
| waktu_permintaan  | Integer      | panjang         | Waktu respons (dalam milidetik), yang mengacu pada waktu yang dibutuhkan sebuah simpul untuk merespons klien dengan semua paket kembali setelah menerima permintaan |
| ukuran_rsp      | Integer      | panjang         | Jumlah byte yang dikembalikan                                                  |
| waktu          | Integer      | panjang         | Minta stempel waktu dalam format UNIX (dalam detik)                                        |
| ua            | String       | teks         | Informasi `User-Agent`                                               |
| url           | String       | teks         | Jalur permintaan                                                     |
| uuid          | String       | teks         | ID permintaan unik                                               |
| versi       | Integer      | panjang         | Versi log real-time CDN                                                 |
