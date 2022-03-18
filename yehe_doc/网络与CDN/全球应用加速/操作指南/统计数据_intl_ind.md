Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap), lalu pilih **Statistics** (Statistik) di bilah sisi kiri. Halaman **Statistics** (Statistik) menampilkan data dalam empat dimensi berikut: koneksi, grup koneksi, pendengar, dan server asal.

## Koneksi

Anda dapat melihat statistik koneksi, seperti yang ditunjukkan di bawah ini:

- **Connection Type** (Jenis Koneksi): diatur secara default ke koneksi tunggal. Anda juga dapat memilih grup koneksi yang telah dibuat sebelumnya.
- **Connection** (Koneksi): Pilih koneksi di **Access Management** (Manajemen Akses) atau di grup koneksi.
- **Data Type** (Jenis Data): Pilih satu atau semua jenis data (bandwidth, lalu lintas, volume paket, koneksi bersamaan, HTTP QPS, HTTPS QPS, latensi, dan tingkat kehilangan paket).
- **Time Period** (Periode Waktu): Pilih periode waktu.
- **Time Granularity** (Perincian Waktu): Pilih perincian waktu. Waktu kueri maksimum adalah 15 hari untuk perincian 1 menit, 31 hari untuk perincian 5 menit, 93 hari untuk perincian 1 jam, dan 186 hari untuk perincian 1 hari.

![](https://main.qcloudimg.com/raw/ebcbf2519d0189f9437d5375aa50ece9.png)

## Grup Koneksi

Anda dapat melihat statistik grup koneksi, seperti yang ditunjukkan di bawah ini:

- **Connection Group** (Grup Koneksi): Pilih satu atau beberapa grup koneksi.
- **Data Type** (Jenis Data): Pilih satu atau semua jenis data (bandwidth dan lalu lintas).
- **Time Period** (Periode Waktu): Pilih periode waktu.
- **Time Granularity** (Perincian Waktu): Pilih perincian waktu. Waktu kueri maksimum adalah 15 hari untuk perincian 1 menit, 31 hari untuk perincian 5 menit, 93 hari untuk perincian 1 jam, dan 186 hari untuk perincian 1 hari.

![](https://main.qcloudimg.com/raw/7517ea8a6d1bffccd5436b64882d7c8f.png)

## Pendengar

Anda dapat melihat statistik pendengar, seperti yang ditunjukkan di bawah ini:

- **Connection/Connection Group** (Koneksi/Grup Koneksi): Pilih koneksi atau grup koneksi untuk pendengar.
- **Listener** (Pendengar): Pilih pendengar.
- **Data Type** (Jenis Data): Pilih satu atau semua jenis data (bandwidth, lalu lintas, volume paket, dan koneksi bersamaan).
- **Time Period** (Periode Waktu): Pilih periode waktu.
- **Time Granularity** (Perincian Waktu): Pilih perincian waktu. Waktu kueri maksimum adalah 15 hari untuk perincian 1 menit, 31 hari untuk perincian 5 menit, 93 hari untuk perincian 1 jam, dan 186 hari untuk perincian 1 hari.

![](https://main.qcloudimg.com/raw/150adb14a909f5d954fb52b579d1cd72.png)

## Server Asal

Anda dapat melihat statistik status kesehatan server asal, seperti yang ditunjukkan di bawah ini:

- **Connection/Connection Group** (Koneksi/Grup Koneksi): Pilih koneksi atau kelompok koneksi untuk server asal.
- **Listener** (Pendengar): Pilih pendengar untuk server asal.
- **Origin** (Asal): Pilih server asal.
- **Time Period** (Periode Waktu): Pilih periode waktu.
- **Time Granularity** (Perincian Waktu): Pilih perincian waktu. Waktu kueri maksimum adalah 15 hari untuk perincian 1 menit, dan 31 hari untuk perincian 5 menit.

![](https://main.qcloudimg.com/raw/cb936fbfbca6c9a7e370d0401f4b6c55.png)

## Mengekspor Data

Buka halaman **Statistics** (Statistik), lalu klik ikon unduh untuk mengekspor data.
![](https://main.qcloudimg.com/raw/fada34020a50842ff1c7625cdee437f7.png)

## Mengonfigurasi Kebijakan Alarm
Buka halaman [Statistik](https://console.cloud.tencent.com/gaap/data), lalu klik **Configure Alarm** (Konfigurasi Alarm) di pojok kanan atas untuk mengonfigurasi kebijakan alarm. Untuk detail selengkapnya, lihat [Akses Pemantauan Cloud](https://intl.cloud.tencent.com/document/product/608/17541).
