

## Ikhtisar Konfigurasi

HTTP Strict Transport Security (HSTS) adalah protokol keamanan web yang dipromosikan oleh Institution of Electronics and Telecommunication Engineers (IETE). Protokol keamanan ini memaksa klien (seperti peramban) untuk menggunakan HTTPS untuk membuat koneksi dengan server untuk membantu mengenkripsi situs web secara global.

## Batasan Konfigurasi

- `expireTime` dapat memiliki rentang dari 0 hingga 365 hari dan dikonfigurasi dalam hitungan detik.
- Beri centang pada `includeSubDomain` jika Anda perlu menyertakan nama subdomain.
- Untuk mengaktifkan konfigurasi HSTS, konfigurasi akselerasi HTTPS harus diselesaikan terlebih dahulu.
- Setelah konfigurasi HSTS diaktifkan, sebaiknya aktifkan [Konfigurasi Pengalihan Paksa](https://intl.cloud.tencent.com/document/product/228/35214) untuk mengalihkan permintaan HTTP ke permintaan HTTPS. Jika tidak, peramban tidak akan membuat cache HSTS untuk permintaan HTTP.

## Panduan Konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Buka tab **HTTPS Configuration** (Konfigurasi HTTPS) untuk menemukan bagian **HSTS Configuration** (Konfigurasi HSTS). Ini dinonaktifkan secara default.
![](https://main.qcloudimg.com/raw/4e44076b3485c9de15776134af7d5e96.png)
Aktifkan dan lakukan konfigurasi yang sesuai:
![](https://main.qcloudimg.com/raw/5a98a2ede54d4eceb8b5f4f0a8bbaa3b.png)
Klik **Confirm** (Konfirmasikan) untuk menerapkan konfigurasi ke header respons. Anda dapat mengeklik **Edit** untuk mengubahnya nanti.
![](https://main.qcloudimg.com/raw/e22e2cf4ad493379db7f1bcf49cfa03a.png)

## Sampel Konfigurasi

Jika konfigurasi HSTS nama domain `cloud.tencent.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/58e49b2b5a0b94f21fa3547dda08daed.png)
Maka, header respons-nya adalah:
![](https://main.qcloudimg.com/raw/910e57e5abdedba4a33b4e4748a81318.png)

