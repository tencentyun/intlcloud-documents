CLB mendukung konfigurasi khusus, membuat Anda bisa mengatur parameter konfigurasi untuk instance CLB tunggal, seperti `client_max_body_size` dan `ssl_protocols`, agar sesuai kebutuhan unik Anda.
>?
>- Setiap wilayah bisa memiliki hingga 200 entri konfigurasi khusus.
>- Konfigurasi khusus dibatasi pada 64K byte.
>- Saat ini, setiap instance hanya bisa diikat pada satu entri konfigurasi khusus.
>- Konfigurasi khusus hanya valid untuk pendengar CLB HTTP/HTTPS CLB (sebelumnya CLB Aplikasi) lapisan 7.

## Parameter Konfigurasi Khusus CLB
Saat ini, konfigurasi khusus CLB mendukung bidang-bidang berikut ini:

| Bidang Konfigurasi |   Nilai Default/Nilai yang Direkomendasikan  |    Rentang Parameter  | Deskripsi  |
| :-------- | :-------- | :------ |:------ |
|ssl_protocols | TLSv1 TLSv1.1 TLSv1.2 |TLSv1 TLSv1.1 TLSv1.2 TLSv1.3 | Versi protokol TLS yang digunakan |
|  ssl_ciphers  | Lihat lebih lanjut di bawah ini.| Lihat lebih lanjut di bawah ini.| Rangkaian enkripsi |
|  client_header_timeout  | 60s |  [30-120]s | Periode waktu habis untuk memperoleh header permintaan klien; jika waktu habis, kesalahan 408 akan dikembalikan.|
|  client_header_buffer_size | 4k |[1-256]k | Ukuran buffer default tempat header permintaan klien disimpan. |
|  client_body_timeout | 60s |  [30-120]s | Periode waktu habis untuk memperoleh bodi permintaan klien, yang bukan merupakan waktu untuk memperoleh seluruh bodi, tetapi merujuk pada periode diam tanpa transmisi data; jika waktu habis, kesalahan 408 akan dikembalikan. |
|  client_max_body_size | 60M |[1-10240]M| <ul><li>Rentang konfigurasi default:1 MB – 256 MB; ini bisa dikonfigurasi secara langsung.</li><li>Ukuran maksimum:2,048 MB; jika `client_max_body_size` lebih dari 256 MB, nilai <a href="#buffer">proxy_request_buffering</a> harus "off".</li></ul> |
|  keepalive_timeout | 75s | [0-900]s| Waktu tunggu koneksi persisten `Client-server`; jika diatur ke 0, koneksi persisten dilarang.Jika Anda ingin mengaturnya hingga lebih dari 900, silakan kirim aplikasi(https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1).Nilai maksimum yang bisa Anda atur adalah 3600. |
|  add_header |Khusus| - | Bidang header khusus yang dikembalikan kepada klien dalam format `add_header xxx yyy`. |
|  more_set_headers |Khusus| - | Bidang header khusus yang dikembalikan kepada klien dalam format `more_set_headers "A:B"`. |
|  proxy_connect_timeout | 4s | [4-120]s |Periode waktu habis koneksi backend upstream.|
|  proxy_read_timeout |60s |[30-3600]s|Periode waktu habis pembacaan respons backend upstream.|
|  proxy_send_timeout |60s |[30-3600]s|Periode waktu habis pengiriman permintaan ke backend upstream.|
|  server_tokens | on | on, off | <ul><li>`on`: menampilkan informasi versi;</li><li>`off`: menyembunyikan informasi versi.</li></ul>|
|  keepalive_requests | 100 | [1-10000] |Jumlah permintaan maksimum yang bisa dikirimkan ke koneksi persisten `client-server`.|
|  proxy_buffer_size | 4k |[1-64]k| Ukuran header respons server, yang merupakan ukuran buffer tunggal yang diatur di `proxy_buffer` secara default; untuk menggunakan `proxy_buffer_size`, `proxy_buffers` harus diatur di saat yang sama.|
|  proxy_buffers | 8 4k |[3-8] [4-8]k|Kuantitas dan ukuran buffer.|
|  <span id="buffer">proxy_request_buffering</span> | on |on, off|<ul><li>`on`: menyimpan bodi permintaan klien; instance CLB meng-cache permintaan dan meneruskannya ke instance CVM backend dalam beberapa bagian setelah permintaan itu diterima sepenuhnya.</li><li>`off`: tidak menyimpan bodi permintaan klien; setelah menerima permintaan, instance CLB meneruskannya secara langsung ke instance CVM backend, yang menambah tekanan pada performa CVM backend.</li></ul>|
|  proxy_set_header   |X-Real-Port $remote_port|<ul><li>X-Real-Port $remote_port</li><li>X-clb-stgw-vip $server_addr</li><li>Stgw-request-id $stgw_request_id</li><li>X-Forwarded-Port $vport</li><li>X-Method $request_method</li><li>X-Uri $uri</li><li>X-Forwarded-Proto </li></ul>|<ul><li>`X-Real-Port $remote_port`: port klien.</li><li>`X-clb-stgw-vip $server_addr`:VIP CLB.</li><li>`Stgw-request-id $stgw_request_id`: ID permintaan (hanya digunakan di CLB).</li><li>`X-Forwarded-Port`:Port pendengar CLB.</li><li>`X-Method`: metode permintaan klien.</li><li>`X-Uri`: URI permintaan klien.</li><li>`X-Forwarded-Proto`: protokol untuk port pendengar CLB (didukung secara default).</li></ul> |
|  send_timeout | 60s |[1-3600]s|Periode waktu habis transfer data dari server ke klien, yang merupakan interval waktu antara dua tindakan transfer data yang berurutan, bukan seluruh periode transfer permintaan.|
|  ssl_verify_depth |  1 |[1, 10]|Kedalaman verifikasi rantai sertifikat klien.|
|proxy_redirect | http:// https:// | http:// https://  | Jika server upstream mengembalikan permintaan untuk dialihkan atau disegarkan, contohnya, kode respons 301 atau 302 HTTP, `proxy_redirect` akan mereset http menjadi https di bidang "Location" atau "Refresh" di header HTTP untuk pengalihan yang aman.  |
| ssl_early_data  |  off |on, off| Mengaktifkan atau menonaktifkan TLS 1.3 0-RTT.Hanya jika nilai bidang `ssl_protocols` mengandung `TLSv1.3`, `ssl_early_data` bisa berlaku.**You shall consider the risk of replay attacks before enabling `ssl_early_data`** (Anda harus mempertimbangkan risiko serangan putar ulang sebelum mengaktifkan `ssl_early_data`).|
|http2_max_field_size|4k|[1-256]k|Membatasi ukuran maksimum header permintaan yang dikompresi dalam HPACK.|
|error_page|-|error_page code [ = [ respons]] uri|URL yang telah ditentukan akan ditampilkan untuk kode kesalahan tertentu.Kode respons default diatur secara default ke 302.URI harus diawali dengan `/`.|


>?Persyaratan pada nilai `proxy_buffer_size` dan `proxy_buffers`: 2 * maks (proxy_buffer_size, proxy_buffers.size) ≤ (proxy_buffers.num - 1)\* proxy_buffers.size; Contohnya, jika `proxy_buffer_size` adalah "24k", `proxy_buffers` adalah "8 8k"; 2 * 24k = 48k, (8 - 1)\* 8k = 56k; dan 48k ≤ 56k, jadi tidak akan ada kesalahan konfigurasi.
>
## Instruksi Konfigurasi ssl_ciphers
Rangkaian enkripsi ssl_ciphers yang dikonfigurasi harus dalam format yang sama dengan yang digunakan OpenSSL.Daftar algoritme adalah satu `<cipher strings>` atau lebih; beberapa algoritme harus dipisah dengan ":"; ALL mewakili semua algoritme, "!" menandakan agar tidak mengaktifkan algoritme, dan "+" menandakan agar memindahkan algoritme ke tempat terakhir.
Algoritme enkripsi untuk penonaktifan paksa default adalah: `!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE`.

**Nilai default:**
```plaintext
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE:3DES;
```

**Rentang parameter:**
```plaintext
ECDH-ECDSA-AES128-SHA256:ECDH-RSA-AES256-SHA:ECDH-ECDSA-AES256-SHA:SRP-DSS-AES-256-CBC-SHA:SRP-AES-128-CBC-SHA:ECDH-RSA-AES128-SHA256:DH-RSA-AES128-SHA256:DH-RSA-CAMELLIA128-SHA:DH-DSS-AES256-GCM-SHA384:DH-RSA-AES256-SHA256:AES256-SHA256:SEED-SHA:CAMELLIA256-SHA:ECDH-RSA-AES256-SHA384:ECDH-ECDSA-AES128-GCM-SHA256:DH-RSA-AES128-SHA:DH-RSA-AES128-GCM-SHA256:DH-DSS-AES128-SHA:ECDH-RSA-AES128-SHA:DH-DSS-CAMELLIA256-SHA:SRP-AES-256-CBC-SHA:DH-DSS-AES128-SHA256:SRP-RSA-AES-256-CBC-SHA:ECDH-ECDSA-AES256-GCM-SHA384:ECDH-RSA-AES256-GCM-SHA384:DH-DSS-AES256-SHA256:ECDH-ECDSA-AES256-SHA384:AES128-SHA:DH-DSS-AES128-GCM-SHA256:AES128-SHA256:DH-RSA-SEED-SHA:ECDH-ECDSA-AES128-SHA:IDEA-CBC-SHA:AES128-GCM-SHA256:DH-RSA-CAMELLIA256-SHA:CAMELLIA128-SHA:DH-RSA-AES256-GCM-SHA384:SRP-RSA-AES-128-CBC-SHA:SRP-DSS-AES-128-CBC-SHA:ECDH-RSA-AES128-GCM-SHA256:DH-DSS-CAMELLIA128-SHA:DH-DSS-SEED-SHA:AES256-SHA:DH-RSA-AES256-SHA:kEDH+AESGCM:AES256-GCM-SHA384:DH-DSS-AES256-SHA:HIGH:AES128:AES256:AES:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE
```

## Contoh Konfigurasi Khusus CLB
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance/index?rid=8) dan klik **Custom Configuration** (Konfigurasi Khusus) di bilah sisi kiri.
2.Klik **Create** (Buat), isi item-item konfigurasinya dan akhiri dengan ";".
![](https://main.qcloudimg.com/raw/7ef70a06f9509ba8759e5a923515a471.png)
3.Klik **Completed** (Selesai).
4.Klik **Bind to Instance** (Ikat ke Instance).
5.Di jendela pop-up, pilih instance CLB dari wilayah yang sama, dan klik **Submit** (Kirim).
![](https://main.qcloudimg.com/raw/ad8fb7874b9ce1fe7bf5c9366c7e64e7.png)
6.Anda kini bisa melihat informasi konfigurasi khusus terkait di halaman daftar instance.
![](https://main.qcloudimg.com/raw/d07bdbc134480fa89f732c93c3861243.png)
Kode sampel konfigurasi default:
```plaintext
ssl_protocols   TLSv1 TLSv1.1 TLSv1.2;
client_header_timeout   60s;
client_header_buffer_size   4k;
client_body_timeout    60s;
client_max_body_size   60M;
keepalive_timeout    75s;
add_header     xxx yyy;
more_set_headers      "A:B";
proxy_connect_timeout    4s;
proxy_read_timeout    60s;
proxy_send_timeout    60s;
```

