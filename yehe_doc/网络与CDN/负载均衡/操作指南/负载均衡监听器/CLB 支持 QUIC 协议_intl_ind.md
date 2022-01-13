Protokol QUIC membantu Anda mengakses aplikasi lebih cepat dan mencapai multiplexing tanpa membutuhkan koneksi ulang pada skenario seperti jaringan lemah atau sering beralih antara Wi-Fi dan 4G.Dokumen ini memperkenalkan cara mengonfigurasi protokol QUIC di Konsol CLB.
## Ikhtisar QUIC
Quick UDP Internet Connection ([QUIC](https://www.chromium.org/quic) adalah protokol jaringan lapisan transportasi yang didesain oleh Google, aliran data bersamaan multiplexing menggunakan UDP.Dibandingkan dengan protokol TCP+TLS+HTTP2 yang populer, QUIC memiliki keunggulan sebagai berikut:
- Mengurangi waktu untuk membuat koneksi.
- Meningkatkan kontrol kemacetan.
- Multiplex tanpa pemblokiran head-of-line (HOL).
- Migrasi koneksi.

Setelah QUIC diaktifkan, klien bisa membuat koneksi QUIC dengan instance CLB.Jika koneksi QUIC gagal karena negosiasi antara klien dan instance CLB, HTTPS atau HTTP/2 akan digunakan.Namun, instance CLB dan server asli masih menggunakan protokol HTTP1.x.
>?Saat ini, CLB mendukung QUIC Q044 dan versi lebih awal.

## Batasan Penggunaan
- Protokol QUIC di CLB saat ini ada di pengujian beta.Untuk menggunakannya, harap ajukan permohonan.
- Protokol QUIC kini tersedia di Beijing, Shanghai, dan Mumbai.
- Saat ini, hanya CLB jaringan publik dengan pendengar HTTPS lapisan 7 yang mendukung protokol QUIC.
-Protokol QUIC saat ini hanya mendukung instance CLB AZ tunggal.

## Petunjuk[](id:making)
1.Buat instance CLB sesuai kebutuhan.Untuk informasi selengkapnya, lihat [Membuat Instance CLB](https://intl.cloud.tencent.com/document/product/214/6149).
>?Saat membuat instance CLB, pilih “Beijing”, “Shanghai” atau “Mumbai” untuk **Region** (Wilayah), dan “Public Network” (Jaringan Publik) untuk **Network Type** (Jenis Jaringan).
2.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb), dan klik **Instance Management** (Manajemen Instance) di bilah sisi kiri.
2.Di halaman **Instance Management** (Manajemen Instance), pilih tab **Cloud Load Balancer** (Penyeimbang Beban Cloud).
3.Temukan instance CLB jaringan publik yang dibuat di wilayah Beijing, Shanghai atau Mumbai, dan klik **Configure Listener** (Konfigurasi Pendengar) di bawah kolom **Operation** (Operasi).
4.Di halaman **Listener Management** (Manajemen Pendengar), klik **Create** (Buat) di bawah **HTTP/HTTPS Listener** (Pendengar HTTP/HTTPS).
5.Di halaman **Create Listener** (Buat Pendengar), pilih “HTTPS” sebagai protokol port pendengaran.Selesaikan konfigurasi lainnya, lalu klik **Submit** (Kirim).
6.Di halaman **Listener Management** (Manajemen Pendengar), klik simbol **+** di samping pendengar yang baru Anda buat.
7.Di halaman **CreateForwarding rules** (Buat aturan Penerusan), aktifkan **QUIC** dan buat aturan lapisan 7.Isi bidang yang relevan dan klik **Next** (Berikutnya) untuk menyelesaikan konfigurasi dasar.
>?
>- Jika Anda mengaktifkan protokol QUIC saat membuat aturan penerusan HTTPS, Anda bisa mengaktifkan atau menonaktifkan protokol QUIC nanti sesuai kebutuhan.Jika Anda tidak mengaktifkan protokol QUIC saat membuat aturan penerusan HTTPS, Anda tidak bisa mengaktifkannya nanti.
>- Berdasarkan protokol UDP, QUIC akan menggunakan port UDP dari instance CLB.Jika Anda mengaktifkan QUIC untuk pendengar HTTPS, port UDP dan TCP akan digunakan.Contohnya, Anda mengaktifkan QUIC untuk pendengar HTTPS:443, baik port TCP:443 dan UDP:443 digunakan, dan Anda tidak bisa membuat pendengar TCP:443 atau UDP:443.
>

## Operasi Selanjutnya
Setelah konfigurasi dasar diselesaikan, Anda bisa mengonfigurasi [pemeriksaan kesehatan](https://intl.cloud.tencent.com/document/product/214/6097) dan [persistensi sesi](https://intl.cloud.tencent.com/document/product/214/6154).

