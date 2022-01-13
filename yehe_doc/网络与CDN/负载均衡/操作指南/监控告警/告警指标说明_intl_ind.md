## Deskripsi Alarm
Anda bisa membuat alarm untuk metrik instance tertentu agar instance CLB Anda akan mengirimkan informasi alarm ke grup pengguna target saat status berjalannya memenuhi syarat tertentu.Dengan melakukannya, Anda bisa mendeteksi pengecualian apa pun tepat waktu dan mengambil langkah tepat untuk memastikan kestabilan dan keandalan sistem.Untuk informasi selengkapnya, silakan lihat [Ikhtisar Alarm](https://intl.cloud.tencent.com/document/product/248/6126).
Kebijakan alarm CLB mencakup yang berikut ini:
- Pendengar jaringan publik
- Pendengar jaringan pribadi
- Port server (lainnya)
- Level pendengar
- Level port server
- Port server (tipe Klasik jaringan pribadi)
- Pemantauan protokol lapisan 7

## Pendengar Jaringan Publik/Pribadi
Saat ini, baik CLB jaringan publik dan CLB jaringan pribadi mendukung alarm di level pendengar dengan metrik berikut ini:

| Metrik | Unit | Deskripsi |
|----|------|----|
| Bandwidth masuk | Mbps | Bandwidth yang digunakan klien untuk mengakses CLB melalui jaringan publik dalam satu periode referensi. |
| Bandwidth keluar | Mbps | Bandwidth yang digunakan CLB untuk mengakses jaringan publik dalam satu periode referensi. |
| Jumlah paket masuk | Paket | Jumlah paket data permintaan yang diterima oleh CLB per detik dalam satu periode referensi. |
| Jumlah paket keluar | Paket | Jumlah paket data yang dikirim oleh CLB per detik dalam satu periode referensi. |

## Port Server (Lainnya)
Semua instance CLB kecuali Klasik jaringan pribadi mendukung alarm di dua level berikut:
1.Level pendengar
Anda bisa mengonfigurasikan jumlah port server asli luar biasa dari pendengar untuk statistik pengecualian dari semua port server terikat di bawah pendengar, yang akan memicu alarm sesuai ambang batas yang dikonfigurasi.Seperti yang ditunjukkan di bawah ini, jumlah port pengecualian dari semua server asli di bawah pendengar terpilih dikumpulkan satu kali setiap menit; jika jumlahnya lebih dari 10 per detik dalam dua periode referensi berturut-turut, dia akan memicu alarm satu kali per hari.
>?Untuk mengaktifkan alarm level pendengar, silakan [kirimkan tiket](https://console.cloud.tencent.com/workorder/category) untuk mendaftar.

- Konfigurasikan objek alarm:
![](https://main.qcloudimg.com/raw/bf26227edb359e6f7acd01febbbc38c9.png)
- Konfigurasikan syarat pemicu:
![](https://main.qcloudimg.com/raw/7cb8c5db9a1fb616f478e2e109d31097.png)
2.Level port server
Anda bisa mengonfigurasi alarm pengecualian untuk port tertentu dari server asli yang terikat pada satu pendengar sehingga alarm akan dikirim kapan pun port menjadi pengecualian.
- Konfigurasikan objek alarm:
![](https://main.qcloudimg.com/raw/e1d947188535eac4189254ba0e8a26cb.png)
- Konfigurasikan syarat pemicu:
![](https://main.qcloudimg.com/raw/80e4072ba35d426e4503a7b64ea63865.png)
>!
>- Pengecualian port server asli: artinya port server asli dianggap tidak tersedia oleh CLB; pada beberapa kasus, jitter jaringan juga bisa memicu pengecualian port.
>- Statistik pada level pendengar mencakup status port dari semua server di bawah pendengar, dari konvergensi alarm tunggal ke alarm ambang batas.Untuk menghindari dampak jitter jaringan, Anda sebaiknya menggunakan alarm level pendengar.

## Port Server (Tipe Klasik Jaringan Pribadi)
Anda bisa mengonfigurasi alarm pengecualian port server untuk CLB Klasik jaringan pribadi sesuai yang diinstruksikan di "Port Server (lainnya) > Level port server".
Anda bisa mengonfigurasi alarm pengecualian untuk port tertentu dari server asli yang terikat pada satu pendengar sehingga alarm akan dikirim kapan pun port menjadi pengecualian.

## Pemantauan Protokol Lapisan 7
Anda bisa mengonfigurasikan kebijakan alarm metrik pemantauan unik untuk semua pendengar lapisan 7 (HTTP/HTTPS).Metrik tertentunya adalah sebagai berikut:

| Metrik | Unit | Deskripsi |
|----|------|----|
| Bandwidth masuk | Mbps | Bandwidth yang digunakan klien untuk mengakses CLB melalui jaringan publik dalam satu periode referensi. |
| Bandwidth keluar | Mbps | Bandwidth yang digunakan CLB untuk mengakses jaringan publik dalam satu periode referensi. |
| Jumlah paket masuk | Paket | Jumlah paket data permintaan yang diterima oleh CLB per detik dalam satu periode referensi. |
| Jumlah paket keluar | Paket | Jumlah paket data yang dikirim oleh CLB per detik dalam satu periode referensi. |
| Jumlah koneksi baru | - | Jumlah koneksi baru yang dibuat per menit dalam satu periode referensi. |
| Jumlah koneksi aktif | - | Jumlah koneksi aktif per menit dalam satu periode referensi. |
| Waktu respons rata-rata | ms | Waktu respons rata-rata CLB dalam satu periode referensi. |
| Waktu respons maksimum | ms | Waktu respons maksimum CLB dalam satu periode referensi. |
| Kode status 2xx | - | Jumlah kode status 2xx yang dikembalikan oleh server asli dalam satu periode referensi. |
| Kode status 3xx | - | Jumlah kode status 3xx yang dikembalikan oleh server asli dalam satu periode referensi. |
| Kode status 4xx | - | Jumlah kode status 4xx yang dikembalikan oleh server asli dalam satu periode referensi. |
| Kode status 5xx | - | Jumlah kode status 5xx yang dikembalikan oleh server asli dalam satu periode referensi. |
| Kode status 404 | - | Jumlah kode status 404 yang dikembalikan oleh server asli dalam satu periode referensi. |
| Kode status 502 | - | Jumlah kode status 502 yang dikembalikan oleh server asli dalam satu periode referensi. |
| Kode status 3xx yang dikembalikan CLB | - | Jumlah kode status 3xx yang dikembalikan oleh CLB dalam satu periode referensi. |
| Kode status 4xx yang dikembalikan CLB | - | Jumlah kode status 4xx yang dikembalikan oleh CLB dalam satu periode referensi. |
| Kode status 5xx yang dikembalikan CLB | - | Jumlah kode status 5xx yang dikembalikan oleh CLB dalam satu periode referensi. |
| Kode status 404 yang dikembalikan CLB | - | Jumlah kode status 404 yang dikembalikan oleh CLB dalam satu periode referensi. |
| Kode status 502 yang dikembalikan CLB | - | Jumlah kode status 502 yang dikembalikan oleh CLB dalam satu periode referensi. |

