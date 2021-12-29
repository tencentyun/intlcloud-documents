## Membuat Pendengar HTTP/HTTPS

1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap), masuk ke halaman **Access Management** (Manajemen Akses), dan klik **ID/Connection Name** (ID/Nama Koneksi) dari koneksi yang ditentukan.
2. Pada halaman yang muncul, pilih **HTTP/HTTPS Listener Management** (Manajemen Pendengar HTTP/HTTPS) > **Create** (Buat). Anda dapat memilih protokol HTTP atau HTTPS. (Catatan: saat ini, konfigurasi pendengar HTTP/HTTPS tidak didukung untuk koneksi IPv6.)
3. Konfigurasi spesifiknya adalah sebagai berikut:
   1. Jika HTTP dipilih, hanya nomor port yang diperlukan, dan pendengar akan meneruskan paket melalui protokol HTTP secara default.
![](https://main.qcloudimg.com/raw/0096d45b44fbd916012317a49a97a884.png)
   2. Jika HTTPS dipilih, sertifikat dan informasi tambahan perlu dikonfigurasi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/941665ba354633d345929e3fbd02fa8c.png)
      - **Listeners communicate with the origin server using HTTP protocol** (Pendengar berkomunikasi dengan server asal menggunakan protokol HTTP) berarti protokol HTTPS digunakan antara klien dan koneksi akselerasi VIP, sedangkan protokol HTTP digunakan antara VIP dan server asal, yang perlu membuka port HTTP di server asal;
        **Listeners communicate with the origin server using HTTP protocol** (Pendengar berkomunikasi dengan server asal menggunakan protokol HTTP) berarti protokol HTTPS digunakan antara klien dan server asal, yang memerlukan port HTTPS untuk dibuka di server asal.
      - Parsing SSL: autentikasi satu arah dan dua arah didukung.
      - Sertifikat Server/Klien: Anda perlu mengunggah sertifikat atau memperbaruinya di **Certificate Management** (Pengelolaan Sertifikat) di konsol GAAP, lalu memilihnya saat membuat/memodifikasi pendengar HTTPS. Untuk informasi selengkapnya, lihat [Pengelolaan Otorisasi](https://intl.cloud.tencent.com/document/product/608/42343).

## Mengonfigurasi Pendengar HTTP/HTTPS

Buka tab **HTTP/HTTPS Listener Management** (Manajemen Pendengar HTTP/HTTPS) dan klik **Set Rule** (Tetapkan Aturan) di kolom **Operation** (Operasi) untuk memasukkan nama domain dan halaman manajemen URL.

### Menambahkan nama domain

Untuk menambahkan nama domain untuk pendengar HTTP, Anda hanya perlu memasukkannya dalam format yang ditentukan, dan hanya pencocokan yang akurat yang didukung. Nama domain dapat berisi 3–80 karakter dalam jenis berikut: `a–z`, `0–9`, `_`, dan `–`.
 ![](https://qcloudimg.tencent-cloud.cn/raw/fed0aa02e83804a36799763b0f88cf33.png)
Untuk menambahkan nama domain untuk pendengar HTTPS, Anda harus memasukkannya dan memilih sertifikat server yang sesuai. Sertifikat yang dipilih selama pembuatan pendengar digunakan di konsol secara default. Jika Anda mengunggah sertifikat baru, nama domain akan diautentikasi dengan sertifikat baru.
 ![](https://qcloudimg.tencent-cloud.cn/raw/27131602718160d5f4c096db488dccf6.png)

### Menambahkan aturan

Setelah menambahkan nama domain, Anda dapat mengeklik **Add Rule** (Tambah Aturan) untuk menambahkan URL yang sesuai dan memilih jenis server asal. Anda dapat menambahkan hingga 20 aturan URL untuk satu nama domain seperti yang ditunjukkan di bawah ini:

1. Konfigurasi dasar:
   ![](https://main.qcloudimg.com/raw/fcf56bdf702b67b81990cc4dedd89f0d.png)
   - URL: dapat berisi 1–80 karakter dengan jenis berikut: `a–z`, `A–Z`, `0–9`, `_`, `.`, `-`, dan `/`.
   - Jenis Server Asal: ini dapat berupa IP atau nama domain, tetapi hanya satu jenis yang dapat dipilih untuk satu pendengar. 
2. Kebijakan pemrosesan server asal:
   Tetapkan aturan penerusan server asal; yaitu, jika pendengar terikat ke beberapa server asal, Anda harus memilih kebijakan penjadwalan untuk server asal.
    ![](https://main.qcloudimg.com/raw/bb6f7d4cf05d2fb6e623c5ed28904dbc.png)
   - RR: beberapa server asal melakukan origin-pull sesuai dengan kebijakan RR.
   - RR Tertimbang: beberapa server asal melakukan origin-pull sesuai dengan rasio bobot (konfigurasi ini tidak didukung jika jenis server asal adalah nama domain).
   - Koneksi Terkecil: ini berarti menjadwalkan server asal dengan jumlah koneksi paling sedikit terlebih dahulu.
3. Mekanisme pemeriksaan kesehatan server asal:
   Anda dapat memilih untuk mengaktifkan mekanisme pemeriksaan kesehatan untuk nama domain saat ini dan mengatur URL pemeriksaan independen. Metode permintaan HEAD dan GET didukung. Periksa kode status termasuk http_1xx, http_2xx, http_3xx, http_4xx, dan http_5xx, satu atau beberapa dapat dipilih. Ketika kode status tertentu terdeteksi, pendengar menganggap server asal backend normal. Jika tidak ada kode status yang terdeteksi, pendengar menganggap server asal backend pengecualian.
![](https://main.qcloudimg.com/raw/20d08ec6efd43a94734b6a408afc2d10.png)

### Memodifikasi nama domain

Setelah menambahkan nama domain, Anda dapat mengeklik **Modify Domain Name** (Modifikasi Nama Domain) untuk memodifikasi nama domain.
 ![](https://main.qcloudimg.com/raw/c61efa495d61009bc93ebff1a8891de5.png)

### Menghapus nama domain

Setelah menambahkan nama domain, Anda dapat mengeklik **Delete** (Hapus) untuk menghapus nama domain. Jika aturan dalam nama domain telah diikatkan ke server asal, Anda harus memilih **Force deletion of listeners bound with origin server** (Penghapusan paksa pendengar yang terikat ke server asal).
 ![](https://main.qcloudimg.com/raw/3a7a088320acb13f1c822b1ec34c9ba1.png)

### Memodifikasi aturan

Ikuti langkah-langkah yang dijelaskan dalam "Menambahkan aturan" di atas. Perbedaan utamanya adalah nama domain dan jenis server asal tidak dapat dimodifikasi.

### Mengikat server asal

Untuk informasi selengkapnya, lihat Mengikat Server Asal. Anda dapat mengikat port yang berbeda ke server asal yang berbeda. Untuk informasi selengkapnya tentang fitur **Cover Port** dan **Complement Port**, lihat Mengikat TCP/UDP Pendengar ke Server Asal.

> ! Aturan dapat diikatkan ke hingga 100 server asal.

### Menghapus aturan

Setelah menambahkan aturan, Anda dapat mengeklik **Delete** (Hapus) untuk menghapus aturan. Jika aturan telah diikatkan ke server asal, Anda harus memilih **Force deletion of listeners bound with origin server** (Penghapusan paksa pendengar yang terikat ke server asal) terlebih dahulu.
 ![](https://main.qcloudimg.com/raw/2fd560217ca2f53847033d501eb90e1a.png)

### Mengonfigurasi header permintaan origin-pull

1. Setelah menambahkan aturan, Anda dapat memilih **More** (Lainnya) di kolom **Operation** (Operasi) aturan dan klik **Set Origin-Pull Request Header** (Atur Header Permintaan Origin-Pull).
   ![](https://qcloudimg.tencent-cloud.cn/raw/9dc95f9ef0c564ec6435c4b7f0635cdd.png)
2. Klik **Add Parameter** (Tambahkan Parameter) untuk menambahkan parameter nama dan nilai header permintaan. Nilai variabel dari header yang membawa IP nyata pengguna adalah `$remote_addr` (secara default, header `X-Forwarded-For` membawa IP klien untuk origin-pull). Saat ini, kecuali variabel `$remote_addr`, variabel lain dengan `$` tidak didukung.

> !
> 1. Nilai `Key` dari nama header HTTP dapat berisi 1–100 digit (0–9), huruf (a–z, A–Z), dan simbol khusus (-, _, :, dan spasi). `Nilai` dapat berisi 1–100 karakter. Kecuali `$remote_addr`, item konfigurasi lainnya tidak dapat berisi karakter `$`;
> 2. Hingga 10 header permintaan HTTP origin-pull dapat dikonfigurasi untuk setiap aturan;
> 3. Header standar yang tercantum di bawah ini tidak dapat diatur/ditambah/dihapus secara mandiri.

<table>
    <tr>
        <td>www-authenticate</td>
        <td>authorization</td>
        <td>proxy-authenticate</td>
        <td>proxy-authorization</td>
    </tr>
    <tr>
        <td>age</td>
        <td>cache-control</td>
        <td>clear-site-data</td>
        <td>expires</td>
    </tr>
    <tr>
        <td>pragma</td>
        <td>warning</td>
        <td>accept-ch</td>
        <td>accept-ch-lifetime</td>
    </tr>
    <tr>
        <td>early-data</td>
        <td>content-dpr</td>
        <td>dpr</td>
        <td>device-memory</td>
    </tr>
    <tr>
        <td>save-data</td>
        <td>viewport-width</td>
        <td>width</td>
        <td>last-modified</td>
    </tr>
    <tr>
        <td>etag</td>
        <td>if-match</td>
        <td>if-none-match</td>
        <td>if-modified-since</td>
    </tr>
    <tr>
        <td>if-unmodified-since</td>
        <td>vary</td>
        <td>connection</td>
        <td>keep-alive</td>
    </tr>
    <tr>
        <td>accept</td>
        <td>accept-charset</td>
        <td>expect</td>
        <td>max-forwards</td>
    </tr>
    <tr>
        <td>access-control-allow-origin</td>
        <td>access-control-max-age</td>
        <td>access-control-allow-headers</td>
        <td>access-control-allow-methods</td>
    </tr>
    <tr>
        <td>access-control-expose-headers</td>
        <td>access-control-allow-credentials</td>
        <td>access-control-request-headers</td>
        <td>access-control-request-method</td>
    </tr>
    <tr>
        <td>origin</td>
        <td>timing-allow-origin</td>
        <td>dnt</td>
        <td>tk</td>
    </tr>
    <tr>
        <td>content-disposition</td>
        <td>content-length</td>
        <td>content-type</td>
        <td>content-encoding</td>
    </tr>
    <tr>
        <td>content-language</td>
        <td>content-location</td>
        <td>forwarded</td>
        <td>x-forwarded-host</td>
    </tr>
    <tr>
        <td>x-forwarded-proto</td>
        <td>via</td>
        <td>from</td>
        <td>host</td>
    </tr>
    <tr>
        <td>referer-policy</td>
        <td>allow</td>
        <td>server</td>
        <td>accept-ranges</td>
    </tr>
    <tr>
        <td>range</td>
        <td>if-range</td>
        <td>content-range</td>
        <td>cross-origin-embedder-policy</td>
    </tr>
    <tr>
        <td>cross-origin-opener-policy</td>
        <td>cross-origin-resource-policy</td>
        <td>content-security-policy</td>
        <td>content-security-policy-report-only</td>
    </tr>
    <tr>
        <td>expect-ct</td>
        <td>feature-policy</td>
        <td>strict-transport-security</td>
        <td>upgrade-insecure-requests</td>
    </tr>
    <tr>
        <td>x-content-type-options</td>
        <td>x-download-options</td>
        <td>x-frame-options(xfo)</td>
        <td>x-permitted-cross-domain-policies</td>
    </tr>
    <tr>
        <td>x-powered-by</td>
        <td>x-xss-protection</td>
        <td>public-key-pins</td>
        <td>public-key-pins-report-only</td>
    </tr>
    <tr>
        <td>sec-fetch-site</td>
        <td>sec-fetch-mode</td>
        <td>sec-fetch-user</td>
        <td>sec-fetch-dest</td>
    </tr>
    <tr>
        <td>last-event-id</td>
        <td>nel</td>
        <td>ping-from</td>
        <td>ping-to</td>
    </tr>
    <tr>
        <td>report-to</td>
        <td>transfer-encoding</td>
        <td>te</td>
        <td>trailer</td>
    </tr>
    <tr>
        <td>sec-websocket-key</td>
        <td>sec-websocket-extensions</td>
        <td>sec-websocket-accept</td>
        <td>sec-websocket-protocol</td>
    </tr>
    <tr>
        <td>sec-websocket-version</td>
        <td>accept-push-policy</td>
        <td>accept-signature</td>
        <td>alt-svc</td>
    </tr>
    <tr>
        <td>date</td>
        <td>large-allocation</td>
        <td>link</td>
        <td>push-policy</td>
    </tr>
    <tr>
        <td>retry-after</td>
        <td>signature</td>
        <td>signed-headers</td>
        <td>server-timing</td>
    </tr>
    <tr>
        <td>service-worker-allowed</td>
        <td>sourcemap</td>
        <td>upgrade</td>
        <td>x-dns-prefetch-control</td>
    </tr>
    <tr>
        <td>x-firefox-spdy</td>
        <td>x-pingback</td>
        <td>x-requested-with</td>
        <td>x-robots-tag</td>
    </tr>
    <tr>
        <td>x-ua-compatible</td>
        <td>max-age</td>
        <td></td>
        <td></td>
    </tr>
</table>

## Menghapus Pendengar HTTP/HTTPS

Buka tab **HTTP/HTTPS Listener Management** (Manajemen Pendengar HTTP/HTTPS) dan klik **Delete** (Hapus) di kolom **Operation** (Operasi) dari pendengar yang ditentukan untuk dihapus. Jika pendengar terikat ke server asal, Anda perlu memeriksa **Allow force deletion of listeners with bound origin servers** (Izinkan penghapusan paksa pendengar dengan server asal terikat) terlebih dahulu. Setelah penghapusan, layanan akselerasi untuk port pendengar akan berhenti.
 ![](https://main.qcloudimg.com/raw/5df2bff2fb4f07ce2631824792429147.png)