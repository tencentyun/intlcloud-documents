## Ikhtisar Konfigurasi

CDN Tencent Cloud mendukung penambahan header permintaan tarik-asal:

- Membawa IP klien yang sebenarnya ke server asal melalui header `X-Forward-For`.
- Membawa port klien yang sebenarnya ke server asal untuk analisis melalui header `X-Forward-Port`.
- Menambahkan header khusus.

Anda juga dapat mengatur dan menghapus permintaan tarik-asal khusus.

## Panduan Konfigurasi

### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, lalu klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Pilih tab **Origin-pull Configuration** (Konfigurasi Origin-pull) untuk menemukan bagian **Origin-pull Request Header Configuration** (Konfigurasi Header Permintaan Tari-asal). Fitur ini dinonaktifkan dan tidak dikonfigurasi sebelumnya secara default.
![img](https://main.qcloudimg.com/raw/c41a39a9a851fbe3778ca325edc2e3f8.png)

### Operasi

| Operasi | Deskripsi                                                         |
| -------- | ------------------------------------------------------------ |
| Set (Atur) | Mengatur nilai parameter header permintaan yang ditentukan.<br/>Jika header target tidak ada, header target yang baru akan ditambahkan.<br/>Jika parameter header permintaan tarik-asal sudah ada, header permintaan baru akan menimpa yang lama karena header duplikat tidak diperbolehkan.|
| Add (Tambahkan) | Menambahkan parameter header permintaan tarik-asal yang ditentukan.<br/>Jika header target sudah ada, header permintaan baru akan menimpa yang lama karena header duplikat tidak diperbolehkan.|
| Delete (Hapus) | Menghapus parameter header permintaan yang ditentukan. |

>!
> - Aturan dijalankan dari bawah ke atas, dan prioritas hanya bermakna untuk jenis operasi yang sama sehingga prioritas beberapa aturan seperti "Set", "Add", dan "Delete" adalah terpisah.
> - Jika parameter header permintaan tarik-asal dikonfigurasi dengan beberapa aturan operasi yang berbeda, operasinya akan dilakukan dalam urutan "Add", "Delete", dan "Set". Misalnya, jika header `X-CDN` dikonfigurasi dengan aturan "Add", "Delete", dan "Set", header tersebut akan ditambahkan, kemudian dihapus, dan akhirnya diatur.

### Parameter header

| Parameter Header | Deskripsi |
| -------------- | ------------------------------------------------------------ |
| X-Forward-For  | Header ini digunakan untuk membawa IP klien yang sebenarnya. Nilainya default ke variabel `$client_ip`, yang tidak dapat dimodifikasi. |
| X-Forward-Port | Header ini digunakan untuk membawa port klien yang sebenarnya. Nilainya default ke variabel `$remote_port`, yang tidak dapat dimodifikasi. |
| Header khusus | Kunci: 1 hingga 100 karakter, termasuk angka (0 - 9), huruf kecil (a - z), huruf besar (A - Z), dan tanda hubung (-).<br>Nilai: 1 hingga 1000 karakter. Karakter bahasa Mandarin tidak didukung.<br>Beberapa header standar tidak dapat diatur, ditambahkan, atau dihapus oleh pengguna. Untuk daftar mendetail, silakan lihat [Catatan](#pemberitahuan). |

> !
> - Hingga 10 aturan header permintaan tarik-asal dapat dikonfigurasi.
> - Jenis aturan yang didukung: semua konten, jenis file tertentu, folder tertentu, dan file tertentu. Pencocokan ekspresi reguler saat ini tidak didukung.



## Sampel Konfigurasi

Konfigurasi header permintaan tarik-asal dari nama domain akselerasi `cloud.tencent.com` adalah sebagai berikut:
![img](https://main.qcloudimg.com/raw/397759f6f138183d3f1ba60b33c7effc.png)
Jika sumber daya yang diakses adalah `http://cloud.tencent.com/test/test.mp4`,:

1. Ini mengenai hit aturan `*` sehingga header `X-Forward-For:$client_ip` akan ditambahkan, dan `$client_ip` akan diganti dengan IP klien yang sebenarnya selama tarik-asal.
2. Ini mengenai hit baik aturan jenis file `.mp4` dan aturan jalur `/test`. Kedua aturan tersebut memiliki jenis yang sama, "Add". Karena aturan yang lebih rendah memiliki prioritas yang lebih tinggi, header `x-cdn:Tencent` ditambahkan.

<span id="notice"></span>

## Catatan
Dalam aturan header permintaan tarik-asal, header standar berikut saat ini tidak dapat diatur, ditambahkan, atau dihapus:

| www-authenticate              | authorization                    | proxy-authenticate             | proxy-authorization                 |
| ----------------------------- | -------------------------------- | ------------------------------ | ----------------------------------- |
| age                           | cache-control                    | clear-site-data                | expires                             |
| pragma                        | warning                          | accept-ch                      | accept-ch-lifetime                  |
| early-data                    | content-dpr                      | dpr                            | device-memory                       |
| save-data                     | viewport-width                   | width                          | last-modified                       |
| etag                          | if-match                         | if-none-match                  | if-modified-since                   |
| if-unmodified-since           | vary                             | connection                     | keep-alive                          |
| accept                        | accept-charset                   | expect                         | max-forwards                        |
| access-control-allow-origin   | access-control-max-age           | access-control-allow-headers   | access-control-allow-methods        |
| access-control-expose-headers | access-control-allow-credentials | access-control-request-headers | access-control-request-method       |
| origin                        | timing-allow-origin              | dnt                            | tk                                  |
| content-disposition           | content-length                   | content-type                   | content-encoding                    |
| content-language              | content-location                 | forwarded                      | x-forwarded-host                    |
| x-forwarded-proto             | via                              | from                           | host                                |
| referer-policy                | allow                            | server                         | accept-ranges                       |
| range                         | if-range                         | content-range                  | cross-origin-embedder-policy        |
| cross-origin-opener-policy    | cross-origin-resource-policy     | content-security-policy        | content-security-policy-report-only |
| expect-ct                     | feature-policy                   | strict-transport-security      | upgrade-insecure-requests           |
| x-content-type-options        | x-download-options               | x-frame-options(xfo)           | x-permitted-cross-domain-policies   |
| x-powered-by                  | x-xss-protection                 | public-key-pins                | public-key-pins-report-only         |
| sec-fetch-site                | sec-fetch-mode                   | sec-fetch-user                 | sec-fetch-dest                      |
| last-event-id                 | nel                              | ping-from                      | ping-to                             |
| report-to                     | transfer-encoding                | te                             | trailer                             |
| sec-websocket-key             | sec-websocket-extensions         | sec-websocket-accept           | sec-websocket-protocol              |
| sec-websocket-version         | accept-push-policy               | accept-signature               | alt-svc                             |
| date                          | large-allocation                 | link                           | push-policy                         |
| retry-after                   | signature                        | signed-headers                 | server-timing                       |
| service-worker-allowed        | sourcemap                        | upgrade                        | x-dns-pramuat-control              |
| x-firefox-spdy                | x-pingback                       | x-requested-with               | x-robots-tag                        |
| x-ua-compatible               | max-age                          |                                |                                     |
