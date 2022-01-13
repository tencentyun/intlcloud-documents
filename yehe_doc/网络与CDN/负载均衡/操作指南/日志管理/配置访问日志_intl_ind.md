CLB mendukung konfigurasi log akses lapisan 7 (HTTP/HTTPS) yang dapat membantu Anda lebih memahami permintaan klien, memecahkan masalah, dan menganalisis perilaku pengguna.Saat ini, log akses dapat disimpan di CLS, dilaporkan dengan interval setiap menit, dan dicari secara online dengan beberapa aturan.

Log akses CLB umumnya digunakan untuk dengan cepat menemukan dan memecahkan masalah.Fitur pencatatan akses mencakup pelaporan log, penyimpanan, dan pencarian:
- Pelaporan log memberikan layanan terbaik, yaitu memprioritaskan penerusan layanan dibandingkan pelaporan log.
- Pencarian dan penyimpanan log memberikan SLA berdasarkan layanan penyimpanan yang saat ini digunakan.

>?
>- Saat ini, log akses dapat disimpan di CLS hanya untuk protokol lapisan 7 (HTTP/HTTPS) tetapi tidak untuk protokol lapisan 4 (TCP/UDP/TCP SSL).
- Menyimpan log akses CLB ke CLS kini bebas biaya.Anda hanya perlu membayar layanan CLS.
- Fitur ini hanya didukung di wilayah yang menyediakan CLS.Lihat [Wilayah Ketersediaan](https://intl.cloud.tencent.com/document/product/614/18940).



## Metode 1:Pencatatan Akses Instance Tunggal
### Langkah 1.Mengaktifkan penyimpanan log akses di CLS
1.Masuk [konsol CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3), lalu klik **Instance Management** (Manajemen Instance) di bilah sisi kiri.
2.Klik ID instance CLB untuk membuka halaman **Instance Management** (Manajemen Instance).
3.Klik ikon pensil pada modul **Access Log (Layer-7)** (Log Akses (Lapisan 7)) di halaman **Basic Information** (Informasi Dasar).
![](https://main.qcloudimg.com/raw/b3f9b4276b4ff2f28ac184478ce7964c.png)
4.Di jendela pop-up **Modify CLS Log Storage Location** (Modifikasi Lokasi Penyimpanan Log CLS), aktifkan pencatatan dan pilih logset tujuan serta topik log untuk penyimpanan log akses, lalu klik **Submit** (Kirim).Jika Anda belum membuat logset atau topik log, silakan [buat sumber daya yang relevan](https://console.cloud.tencent.com/cls/logset), lalu pilih sumber daya tersebut sebagai lokasi penyimpanan.
![](https://main.qcloudimg.com/raw/33386c84ae812881548d1b621fbe6a70.png)
>?Sebaiknya Anda menggunakan topik log yang ditandai dengan "CLB" dalam logset clb_logset.Perbedaan antara topik log yang bertanda "CLB" dengan topik log umum yaitu:
>- Topik log CLB secara otomatis dapat membuat indeks, sedangkan topik log umum harus membuat indeks secara manual.
>- Dasbor untuk topik log CLB disediakan secara default, tetapi untuk topik log umum harus dikonfigurasi secara manual.
6.Klik logset atau topik log untuk mengalihkan ke halaman pencarian log di CLS.
7.(Opsional) Untuk menonaktifkan pencatatan, klik ikon pensil untuk membuka jendela **Modify CLS Log Storage Location** (Modifikasi Lokasi Penyimpanan Log CLS), lalu nonaktifkan.

### Langkah 2.Mengonfigurasi indeks topik log
>?Jika log akses dikonfigurasi untuk satu instance, Anda harus mengonfigurasi indeks untuk topik log; jika tidak, log tidak akan dapat ditemukan.
>
Indeks yang direkomendasikan yaitu sebagai berikut:

| Indeks Nilai Utama    | Tipe Bidang | Pemisah |
| :---------- | :------- | :----- |
| server_addr | teks     | Tidak memerlukan pemisah     |
| server_nama | teks     | Tidak memerlukan pemisah     |
| http_host   | teks     | Tidak memerlukan pemisah     |
| status      | panjang     | -     |
| vip_vpcid   | panjang     | -     |

Langkah-langkah adalah sebagai berikut:
1.Masuk ke [Konsol CLS](https://console.cloud.tencent.com/cls), lalu klik **Log Topic** (Topik Log) di bilah sisi kiri.
2.Klik ID topik log target di halaman "Log Topic" (Topik Log).
3.Di halaman detail topik log, pilih tab **Index Configuration** (Konfigurasi Indeks), lalu klik **Edit** (Edit) untuk menambahkan indeks.Lihat [Mengonfigurasi Indeks](https://intl.cloud.tencent.com/document/product/614/39594) untuk informasi selengkapnya tentang konfigurasi indeks.
![](https://main.qcloudimg.com/raw/38b22da412497a25ac9d6d304766d1ac.png)
4.Hasil konfigurasi indeks seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/6e2393e34cd06c5d073faba88d34110f.png)

### Langkah 3.Melihat log akses
1.Masuk ke [Konsol CLS](https://console.cloud.tencent.com/cls), lalu klik **Search and Analysis** (Pencarian dan Analisis) di bilah sisi kiri.
2.Di halaman **Search Analysis** (Cari Analisis), pilih logset, topik log, dan rentang waktu, lalu klik **Search Analysis** (Cari Analisis) untuk mencari log akses yang dilaporkan oleh CLB ke CLS.Lihat [Sintaks Pencarian CLS Lama](https://intl.cloud.tencent.com/document/product/614/37882) untuk informasi selengkapnya tentang sintaks pencarian.
![](https://main.qcloudimg.com/raw/e15271ea2d1ffac0e735eb254224a5e5.png)

## Metode 2:Konfigurasi pencatatan akses secara batch
>?Fitur ini hanya tersedia untuk pengguna beta saat ini.Untuk menggunakan fitur ini, Anda perlu mengirimkan permohonan.
### Langkah 1.Membuat logset dan topik log[](id:step2)
Untuk mengonfigurasi log akses di CLS, Anda perlu membuat logset dan topik log terlebih dahulu.
Anda dapat langsung beralih ke [Langkah 2](#step3) jika sudah membuat logset dan topik log.
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb) dan pilih **Access Logs** (Log Akses) di bilah sisi kiri.
2.Di halaman **Access Logs** (Log Akses), pilih wilayah untuk logset, lalu klik **Create Logset** (Buat Logset) di bagian "Logset Information" (Informasi Logset).
3.Dalam kotak dialog pop-up **Create Logset**" (Buat Logset), atur periode retensi dan klik **Save** (Simpan).
>?Anda hanya dapat membuat satu logset bernama "clb_logset" di setiap wilayah.
4.Klik **Create Log Topic** (Buat Topik Log) di bagian **Log Topic** (Topik Log) di halaman "Access Logs" (Log Akses).
5.Di jendela pop-up, pilih instance CLB yang ingin ditambahkan ke daftar di sebelah kanan, lalu klik **Save** (Simpan).
>?
>- Ketika membuat topik log, Anda dapat menambahkan instance CLB sesuai kebutuhan.Untuk menambahkan instance, pilih topik log dalam daftar, lalu klik **Manage** (Kelola) di kolom operasi.Setiap instance CLB hanya dapat ditambahkan ke satu topik log.
>- Satu logset dapat berisi beberapa topik log.Anda dapat mengelompokkan log CLB dalam berbagai topik log yang akan ditandai dengan "CLB".
>
![](https://main.qcloudimg.com/raw/9f19f80439f0044768eac4cc235aae9d.png)
6.(Opsional) Untuk menonaktifkan pencatatan, cukup klik **Disable** (Nonaktifkan).

### Langkah 2.Melihat log akses[](id:step3)
Tanpa perlu konfigurasi manual apa pun, CLB telah dikonfigurasi otomatis dengan pencarian indeks menurut log akses penting.Anda dapat langsung membuat kueri log akses melalui pencarian dan analisis.
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb) dan pilih **Access Logs** (Log Akses) di bilah sisi kiri.
2.Pilih topik log, lalu klik **Search** (Pencarian) di kolom operasi untuk beralih ke halaman **Search Analysis** (Cari Analisis) di [Konsol CLS](https://console.cloud.tencent.com/cls/search).
3.Di halaman **Search Analysis** (Cari Analisis), masukkan sintaks pencarian dalam kotak input, pilih rentang waktu, lalu klik **Search Analysis** (Cari Analisis) untuk mencari log akses yang dilaporkan oleh CLB ke CLS.
>?Lihat [Sintaks dan Aturan](https://intl.cloud.tencent.com/document/product/614/30439) untuk informasi selengkapnya tentang sintaks pencarian.


## Format Log dan Deskripsi Variabel
### Format log
```
[$stgw_request_id] [$time_local] [$protocol_type] [$server_addr:$server_port]  [$server_name] [$remote_addr:$remote_port] [$status] [$upstream_addr] [$upstream_status] [$proxy_host] [$request] [$request_length] [$bytes_sent] [$http_host] [$http_user_agent] [$http_referer] [$request_time] [$upstream_response_time] [$upstream_connect_time] [$upstream_header_time] [$tcpinfo_rtt] [$connection] [$connection_requests] [$ssl_handshake_time] [$ssl_cipher] [$ssl_protocol] [$vip_vpcid] [$uri] [$server_protocol]
```

### Tipe bidang
Saat ini, CLS mendukung tiga tipe bidang berikut:

| Nama   | Deskripsi Tipe                 |
| :----- | :----------------------- |
| teks   | Tipe teks                 |
| long   | Tipe integer (Int 64)   |
| double | Tipe poin floating (64 bit) |

## Deskripsi variabel log
<table class="table"><thead><tr><th>Variabel</th><th>Deskripsi</th></tr></thead>Tipe Bidang</th></tr></thead>
<tbody><tr><td>stgw_request_id</td><td> ID Permintaan. </td></tr>text</td></tr>
<tr><td>time_local</td><td> Waktu akses dan zona waktu, misalnya "01/Jul/2019:11:11:00 +0800" dengan "+0800" mewakili UTC+8, yaitu waktu Beijing.</td><td>text</td></tr>
<tr><td>protocol_type</td><td> Tipe protokol (HTTP/HTTPS/SPDY/HTTP2/WS/WSS).</td><td>teks</td></tr>
<tr><td>server_addr</td><td>CLB VIP. </td><td>teks</td></tr>
<tr><td>server_port</td><td>CLB VPort, yaitu port pendengar.</td><td>long</td></tr>
<tr><td>server_name</td><td> `server_name` aturan, yaitu nama domain yang dikonfigurasi di pendengar CLB.</td><td>teks</td></tr>
<tr><td>remote_addr</td><td> IP Klien.</td><td>teks</td>
<tr><td>remote_port</td><td> Port klien.</td><td>long</td></tr>
<tr><td>status</td><td> Kode status yang dikembalikan kepada klien. </td><td>long</td></tr>
<tr><td>upstream_addr</td><td> Alamat RS.</td><td>teks</td>
<tr><td>upstream_status</td><td> Kode status yang dikembalikan oleh RS ke CLB. </td><td>teks</td></tr>
<tr><td>proxy_host</td><td> ID Stream. </td><td>teks</td>
<tr><td>request</td><td> Baris permintaan. </td><td>teks</td></tr>
<tr><td>request_length</td><td> Jumlah byte permintaan yang diterima dari klien.</td><td>long</td></tr>
<tr><td>bytes_sent</td><td> Jumlah byte yang dikirimkan kepada klien.<td>long</td></tr>
<tr><td>http_host</td><td> Nama domain permintaan, yaitu host header HTTP.</td><td>teks</td></tr>
<tr><td>http_user_agent</td><td> Bidang `user_agent` header HTTP.</td><td>teks</td></tr>
<tr><td>http_referer</td><td> Sumber permintaan HTTP. </td><td>teks</td></tr>
<tr><td>request_time</td><td> Waktu pemrosesan permintaan.Penghitungan waktu dimulai ketika byte pertama diterima dari klien dan berhenti ketika byte terakhir dikirimkan kepada klien, yaitu total waktu yang diperlukan untuk menyelesaikan seluruh proses, ketika permintaan klien mencapai instance CLB, instance CLB akan meneruskan permintaan ke RS, RS akan merespons dan mengirimkan data ke instance CLB, dan akhirnya instance CLB meneruskan data kepada klien.</td><td>double</td></tr>
<tr><td>upstream_response_time</td><td> Waktu yang diperlukan untuk menyelesaikan seluruh proses permintaan backend.Penghitungan waktu dimulai ketika instance CLB terhubung dengan RS dan berhenti ketika RS menerima permintaan dan merespons.<td>double</td></tr>
<tr><td>upstream_connect_time</td><td> Waktu yang diperlukan untuk membuat koneksi TCP dengan RS.Penghitungan waktu dimulai ketika instance CLB terhubung dengan RS dan berhenti ketika mengirimkan permintaan HTTP.</td><td>double</td></tr>
<tr><td>upstream_header_time</td><td> Waktu yang diperlukan untuk menerima header HTTP dari RS.Penghitungan waktu dimulai ketika instance CLB terhubung dengan RS dan berhenti ketika header respons HTTP diterima dari RS.</td><td>double</td></tr>
<tr><td>tcpinfo_rtt</td><td> RTT koneksi TCP. </td><td>long</td></tr>
<tr><td>connection</td><td> ID Koneksi. </td><td>long</td></tr>
<tr><td>connection_requests</td><td> Jumlah permintaan dalam koneksi. </td><td>long</td></tr>
<tr><td>ssl_handshake_time</td><td> Waktu yang diperlukan untuk menyelesaikan handshake SSL. </td><td>double</td></tr>
<tr><td>ssl_cipher</td><td> Rangkaian cipher SSL.</td><td>teks</td></tr>
<tr><td>ssl_protocol</td><td> Versi protokol SSL.</td><td>teks</td></tr>
<tr><td>vip_vpcid</td><td>ID VPC dari CLB VIP; `vip_vpcid` instance CLB jaringan publik yaitu `-1`.</td><td>long</td></tr>
<tr><td>request</td><td> Metode permintaan.Hanya mendukung permintaan POST dan GET.</td><td>teks</td></tr>
<tr><td>uri</td><td> Pengidentifikasi Sumber Daya.</td><td>teks</td></tr>
<tr><td>server_protocol</td><td>Protokol yang digunakan untuk CLB.</td><td>teks</td></tr>
</tbody></table>

### Item log pencarian default
Bidang berikut dapat ditemukan dalam logset dengan "CLB" secara default:
<table class="table"><thead><tr><th>Bidang Indeks</th><th>Deskripsi</th></tr>Tipe Bidang</th></tr></thead>
<tbody>
<tr><td>time_local</td><td> Waktu akses dan zona waktu, misalnya "01/Jul/2019:11:11:00 +0800" dengan "+0800" mewakili UTC+8, yaitu waktu Beijing.</td><td>text</td></tr>
<tr><td>protocol_type</td><td> Tipe protokol (HTTP/HTTPS/SPDY/HTTP2/WS/WSS).</td><td>teks</td></tr>
<tr><td>server_addr</td><td>CLB VIP. </td><td>teks</td></tr>
<tr><td>server_name</td><td> `server_name` aturan, yaitu nama domain yang dikonfigurasi di pendengar CLB.</td><td>teks</td></tr>
<tr><td>remote_addr</td><td> IP Klien.</td><td>teks</td>
<tr><td>status</td><td> Kode status yang dikembalikan kepada klien. </td><td>long</td></tr>
<tr><td>upstream_addr</td><td> Alamat RS.</td><td>teks</td>
<tr><td>upstream_status</td><td> Kode status yang dikembalikan oleh RS ke CLB. </td><td>teks</td></tr>
<tr><td>request_length</td><td> Jumlah byte permintaan yang diterima dari klien.</td><td>long</td></tr>
<tr><td>bytes_sent</td><td> Jumlah byte yang dikirimkan kepada klien.<td>long</td></tr>
<tr><td>http_host</td><td> Nama domain permintaan, yaitu host header HTTP.</td><td>teks</td></tr>
<tr><td>request_time</td><td> Waktu pemrosesan permintaan.Penghitungan waktu dimulai ketika byte pertama diterima dari klien dan berhenti ketika byte terakhir dikirimkan kepada klien, yaitu total waktu yang diperlukan untuk menyelesaikan seluruh proses, ketika permintaan klien mencapai instance CLB, instance CLB akan meneruskan permintaan ke RS, RS akan merespons dan mengirimkan data ke instance CLB, dan akhirnya instance CLB meneruskan data kepada klien.</td><td>double</td></tr>
<tr><td>upstream_response_time</td><td> Waktu yang diperlukan untuk menyelesaikan seluruh proses permintaan backend.Penghitungan waktu dimulai ketika instance CLB terhubung dengan RS dan berhenti ketika RS menerima permintaan dan merespons.<td>double</td></tr>
</tbody></table>
