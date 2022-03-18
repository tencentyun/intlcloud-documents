## Menambahkan Pendengar HTTP/HTTPS

1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap). Masuk ke halaman **Access Management** (Manajemen Akses). Klik **ID/Connection Name** (ID/Nama Koneksi) koneksi tertentu.
2. Di halaman yang muncul, pilih **HTTP/HTTPS Listener Management** > **Create** (Manajemen Pendengar HTTP/HTTPS > Buat). Anda dapat memilih protokol HTTP atau HTTPS. (Catatan: saat ini, konfigurasi pendengar HTTP/HTTPS tidak didukung untuk koneksi IPv6.)
3. Detail terkait konfigurasi dapat dilihat di bagian berikut:
   1. Jika **HTTP** dipilih, hanya nomor port pendengar yang diperlukan, dan pendengar akan meneruskan paket menggunakan protokol HTTP secara default.
![](https://main.qcloudimg.com/raw/0096d45b44fbd916012317a49a97a884.png)
   2. Jika **HTTPS** dipilih, sertifikat dan informasi tambahan perlu dikonfigurasi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/941665ba354633d345929e3fbd02fa8c.png)
      - **Listeners communicate with the origin server using HTTP protocol** (Pendengar berkomunikasi dengan server asal menggunakan protokol HTTP) berarti bahwa protokol HTTPS digunakan antara klien dan koneksi akselerasi VIP, sedangkan protokol HTTP digunakan antara VIP dan server asal, yang mengharuskan port HTTP dibuka di server asal;
        **Listeners communicate with the origin server using HTTPS protocol** (Pendengar berkomunikasi dengan server asal menggunakan protokol HTTPS) berarti bahwa protokol HTTPS digunakan antara klien dan server asal, yang mengharuskan port HTTPS dibuka di server asal.
      - **SSL Parsing** (Parsing SSL): Autentikasi satu arah dan dua arah didukung.
      - **Server/Client Certificate** (Sertifikat Server/Klien): Unggah/Perbarui sertifikat di **Certificate Management** (Manajemen Sertifikat) di konsol GAAP, lalu pilih sertifikat tersebut saat membuat/memodifikasi pendengar HTTPS. Untuk informasi selengkapnya, lihat [Manajemen Sertifikat](https://intl.cloud.tencent.com/document/product/608/42343).

## Mengonfigurasi Pendengar HTTP/HTTPS

Di tab **HTTP/HTTPS Listener Management** (Manajemen Pendengar HTTP/HTTPS), klik **Set a Rule** (Tetapkan Aturan) di kolom operasi untuk memasukkan nama domain dan halaman manajemen URL.

## Membuat distribusi

1. Untuk menambahkan nama domain untuk pendengar HTTP, masukkan nama domain yang valid. Nama domain harus terdiri dari 3 hingga 80 karakter, dan karakter yang dapat digunakan adalah [a-z], [0–9], dan [.-]. Hanya pencocokan persis yang didukung.
 ![](https://qcloudimg.tencent-cloud.cn/raw/fed0aa02e83804a36799763b0f88cf33.png)
2. Untuk menambahkan nama domain untuk pendengar HTTPS, masukkan nama domain yang valid, lalu pilih sertifikat server yang sesuai.
 ![](https://qcloudimg.tencent-cloud.cn/raw/27131602718160d5f4c096db488dccf6.png)
	- **Domain**: panjangnya 3 hingga 80 karakter, dan karakter yang dapat digunakan adalah [a-z], [0–9], dan [.-]. Hanya pencocokan persis yang didukung.
	- **Server Certificate** (Sertifikat Server): secara default, ini adalah sertifikat yang digunakan untuk membuat pendengar. Jika Anda mengunggah sertifikat lain, nama domain diautentikasi dengan sertifikat yang diunggah.
	- **HTTP3 Transfer** (Transfer HTTP3): memungkinkannya mendukung QUIC. Jika klien tidak mendukung protokol ini, HTTP2.0 dan versi sebelumnya akan digunakan untuk akses.

### Menambahkan aturan

Setelah nama domain ditambahkan, klik **Add Rule** (Tambahkan Aturan) untuk menambahkan URL yang sesuai dan memilih jenis server asal. Anda dapat menambahkan hingga 20 aturan URL untuk satu nama domain seperti yang ditunjukkan di bawah ini:

1. Konfigurasi dasar:
   ![](https://main.qcloudimg.com/raw/fcf56bdf702b67b81990cc4dedd89f0d.png)
   - **URL**: panjangnya antara 1-80 karakter, dan berikut adalah jenis karakter yang dapat digunakan: [a-z], [0–9], dan [_.-/].
   - **Origin Server Type** (Jenis Server Asal): mendukung IP atau nama domain. Satu pendengar hanya mendukung satu jenis. 
2. Kebijakan pemrosesan untuk server asal:
   Konfigurasi kebijakan pemrosesan server asal, yaitu, jika pendengar terikat ke beberapa server asal, Anda harus memilih kebijakan penjadwalan untuk server asal.
    ![](https://main.qcloudimg.com/raw/bb6f7d4cf05d2fb6e623c5ed28904dbc.png)
   - **RR**: beberapa server asal melakukan origin-pull sesuai dengan kebijakan RR.
   - **Weighted RR** (RR Tertimbang): beberapa server asal melakukan origin-pull sesuai dengan rasio bobot (konfigurasi ini tidak didukung jika jenis server asal adalah nama domain).
   - **Least Connections** (Koneksi Terkecil): menjadwalkan server asal dengan jumlah koneksi paling sedikit terlebih dahulu.
3. Mekanisme pemeriksaan kesehatan server asal:
   Mekanisme pemeriksaan kesehatan dapat diaktifkan. Untuk nama domain saat ini, Anda dapat mengonfigurasi URL pemeriksaan independen. Metode permintaan HEAD dan GET didukung. Centang kode status http_1xx, http_2xx, http_3xx, http_4xx, dan http_5xx, dan satu atau beberapa kode dapat dipilih. Ketika kode status tertentu terdeteksi, pendengar menganggap bahwa server asal backend normal. Jika tidak ada kode status yang terdeteksi, pendengar menganggap bahwa server asal backend memiliki pengecualian.
![](https://main.qcloudimg.com/raw/20d08ec6efd43a94734b6a408afc2d10.png)

### Memodifikasi nama domain

Setelah menambahkan nama domain, Anda dapat mengeklik **Modify Domain Name** (Modifikasi Nama Domain) untuk memodifikasi nama domain.
 ![](https://main.qcloudimg.com/raw/c61efa495d61009bc93ebff1a8891de5.png)

### Menghapus nama domain

Setelah menambahkan nama domain, Anda dapat mengeklik **Delete** (Hapus) untuk menghapus nama domain. Jika aturan dalam nama domain telah diikatkan ke server asal, Anda harus memilih **Force deletion of listeners bound with origin server** (Penghapusan paksa pendengar yang terikat ke server asal).
 ![](https://main.qcloudimg.com/raw/3a7a088320acb13f1c822b1ec34c9ba1.png)

### Konfigurasi HTTP3

Konfigurasi HTTP3 menentukan didukung atau tidaknya HTTP3 (QUIC). Saat ini, HTTP3 hanya dapat dikonfigurasi untuk pendengar HTTPS.
![](https://qcloudimg.tencent-cloud.cn/raw/77cd9b19beeed46f427983d71bc23f7e.png)

### Memodifikasi aturan

Lihat bagian **Menambahkan aturan** di atas. Perbedaan utamanya adalah nama domain dan jenis server asal tidak dapat dimodifikasi.

## Mengikat server asal

Untuk informasi selengkapnya, lihat Mengikat Server Asal. Anda dapat mengikat port yang berbeda ke server asal yang berbeda. Untuk informasi selengkapnya tentang fitur **Cover Port** dan **Complement Port**, lihat Mengikat Pendengar TCP/UDP ke Server Asal.

> ! Aturan dapat diikatkan ke maksimum 100 server asal.

### Menghapus aturan

Setelah menambahkan aturan, Anda dapat mengeklik **Delete** (Hapus) untuk menghapus aturan. Jika aturan telah diikatkan ke server asal, Anda harus memilih **Force deletion of listeners bound with origin server** (Penghapusan paksa pendengar yang terikat ke server asal) terlebih dahulu.
 ![](https://main.qcloudimg.com/raw/2fd560217ca2f53847033d501eb90e1a.png)



### Mengonfigurasi header permintaan origin-pull

1. Setelah menambahkan aturan, Anda dapat memilih **More** (Lainnya) di kolom **Operation** (Operasi) aturan dan mengeklik **Set Origin-Pull Request Header** (Atur Header Permintaan Origin-Pull).
   ![](https://qcloudimg.tencent-cloud.cn/raw/9dc95f9ef0c564ec6435c4b7f0635cdd.png)
2. Klik **Add Parameter** (Tambahkan Parameter) untuk menambahkan parameter nama dan nilai header permintaan. Nilai variabel dari header yang membawa IP sebenarnya pengguna adalah `$remote_addr` (secara default, header `X-Forwarded-For` membawa IP klien untuk origin-pull). Saat ini, kecuali variabel `$remote_addr`, variabel lain yang mengandung `$` tidak didukung.

> !
>
> 1. Nilai `Key` untuk nama header HTTP dapat berisi 1–100 digit (0–9), huruf (a–z, A–Z), dan simbol khusus (-, _, :, dan spasi). `Nilai` dapat berisi 1–100 karakter. Kecuali `$remote_addr`, item konfigurasi lainnya tidak dapat berisi karakter `$`;
> 2. Hingga 10 header permintaan HTTP origin-pull dapat dikonfigurasikan untuk setiap aturan;
> 3. Header standar yang tercantum di bawah ini tidak dapat diatur/ditambahkan/dihapus secara mandiri.

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
        <td>Accept</td>
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

Buka tab **HTTP/HTTPS Listener Management** (Manajemen Pendengar HTTP/HTTPS), klik **Delete** (Hapus) di sebelah kanan pendengar yang dipilih. Jika pendengar telah terikat ke server asal, Anda perlu mencentang **Allow force deletion of listeners bound with origin servers** (Izinkan penghapusan paksa pendengar yang terikat ke server asal) terlebih dahulu. Setelah pendengar dihapus, akselerasi port pendengar akan berhenti.
 ![](https://main.qcloudimg.com/raw/5df2bff2fb4f07ce2631824792429147.png)