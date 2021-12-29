## Protokol TCP/UDP
Koneksi akselerasi dapat diakses dengan cara berikut:
- Klien mengakses "VIP + port" dari koneksi akselerasi.

- Klien mengakses "nama domain + port" dari koneksi akselerasi. 

- Jika klien awalnya mengakses nama domain, konfigurasikan cname untuk menyelesaikan nama domain ini ke koneksi akselerasi, atau memodifikasi host lokal klien untuk menyelesaikan nama domain asal ke VIP koneksi akselerasi.
Jika server asal perlu mendapatkan IP klien nyata (hanya protokol TCP), modul TOA harus diinstal. Untuk informasi selengkapnya, lihat [Dapatkan IP Klien Nyata (TCP)](https://intl.cloud.tencent.com/document/product/608/18946).

## Protokol HTTP/HTTPS
Konfigurasi cname untuk menyelesaikan nama domain yang diakses oleh klien untuk mempercepat koneksi nama domain, atau memodifikasi host lokal klien untuk menyelesaikan nama domain yang akan diakses oleh klien untuk koneksi akselerasi VIP, sehingga klien dapat mengakses koneksi dengan `protocol + URL` untuk mencapai akselerasi.
Server asal bisa langsung mendapatkan IP klien sebenarnya dari bidang `x-forward-for` di header permintaan HTTP.

