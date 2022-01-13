Anda bisa mengimplementasikan layanan web backend dengan menulis fungsi SCF dan mengikatnya dengan instance CLB untuk menyediakan layanan.
>? Pengikatan instance CLB dengan fungsi SCF sedang dalam pengujian beta.Jika ingin menggunakannya, silakan hubungi perwakilan penjualan Anda.
>

## Latar belakang
Tencent Cloud [Fungsi Cloud Tanpa Server (SCF)](https://intl.cloud.tencent.com/document/product/583) adalah lingkungan eksekusi tanpa server yang membuat Anda bisa membangun dan menjalankan aplikasi tanpa harus membeli dan mengelola server.Setelah membuat fungsi, Anda bisa membuat pemicu CLB untuk mengikat fungsi dan event.Pemicu CLB akan meneruskan konten permintaan sebagai parameter fungsi dan mengembalikan hasil dari fungsi tersebut ke pemohon sebagai respons.

## Kasus Penggunaan
<dx-accordion>
::: \sHTTP/HTTPS\sgeneral\saccess
Berlaku pada aplikasi untuk ecommerce, media sosial dan layanan lainnya, dan aplikasi web untuk blog pribadi, halaman event dan lainnya.Alur kerjanya adalah sebagai berikut:
1.Permintaan HTTP/HTTPS yang dimulai oleh aplikasi, peramban, halaman H5, atau Program Mini mengakses fungsi SCF melalui instance CLB.
2.Setelah instance CLB menyelesaikan pelepasan instalasi sertifikat, SCF hanya perlu menyediakan layanan HTTP.
3.Permintaan kemudian ditransfer ke fungsi SCF untuk pemrosesan berikutnya, seperti penulisan ke database cloud dan memanggil API lainnya.
![](https://main.qcloudimg.com/raw/534ca758662eaffdd40d243bd8384739.svg)
:::
::: Switching\sbetween\sCVM\sand\sSCF
Berlaku untuk memigrasikan layanan HTTP/HTTPS dari CVM ke SCF, terutama jika terjadi failover.Alur kerjanya adalah sebagai berikut:
1.Aplikasi, peramban, H5, atau Program Mini Wechat memulai permintaan HTTP/HTTPS.
2.Permintaan itu kemudian diselesaikan ke dua VIP instance CLB oleh DNS.
3.Satu instance CLB meneruskan permintaan ke CVM dan yang lainnya meneruskannya ke SCF.
4.Peralihan dari CVM ke SCF di backend telah selesai tanpa memengaruhi pihak klien.
![](https://main.qcloudimg.com/raw/d285c006b5945486a725936385d9dcb2.svg)
:::
::: CVM/SCF\sbusiness\sdiversion
Berlaku saat pemakaian SCF untuk menangani layanan yang sangat elastis dan CVM untuk menangani bisnis harian dalam skenario seperti penjualan kilat dan pembelian snap-up.
1.Melalui resolusi DNS, nama domain A diselesaikan ke satu VIP instance CLB dan nama domain B diselesaikan ke VIP instance CLB lainnya.
2.Satu instance CLB meneruskan permintaan ke CVM dan yang lainnya meneruskannya ke SCF.
![](https://main.qcloudimg.com/raw/96a77f06ecad23ddf13282aa2e6a496b.svg)
:::

</dx-accordion>



## Batasan
- Pengikatan dengan SCF hanya tersedia di Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (Tiongkok), Singapore, Mumbai, Tokyo, dan Silicon Valley.
- Fungsi SCF hanya bisa diikat dengan instance CLB dari akun tagihan per IP, tetapi tidak dengan akun tagihan per CVM.Jika Anda menggunakan akun tagihan per CVM, kami menyarankan untuk meng-upgrade-nya ke akun tagihan per IP.Untuk informasi selengkapnya, silakan lihat [Memeriksa Tipe Akun](https://intl.cloud.tencent.com/document/product/684/15246).
- Fungsi SCF tidak bisa diikat dengan instance CLB klasik.
- Fungsi SCF tidak bisa diikat dengan instance CLB jaringan klasik.
- Fungsi SCF hanya bisa diikat lintas VPC, tetapi tidak lintas wilayah.
- Fungsi SCF hanya bisa diikat dengan instance CLB IPv4 dan IPv6 NAT64, tetapi saat ini tidak dengan instance CLB IPv6.
- Fungsi SCF hanya bisa diikat dengan pendengar HTTP dan HTTPS lapisan 7, tetapi tidak dengan pendengar QUIC lapisan 7 atau pendengar (TCP, UDP, dan TCP SSL) lapisan 4.


## Prasyarat
1.Anda telah membuat [Instance CLB](https://intl.cloud.tencent.com/document/product/214/6149).
2.Anda telah mengonfigurasikan pendengar [HTTP](https://intl.cloud.tencent.com/document/product/214/32515) atau [HTTPS](https://intl.cloud.tencent.com/document/product/214/32516).

## Petunjuk
![](https://main.qcloudimg.com/raw/eca21ba71ea22a6c240d3b4a05dfdce0.svg)

### Langkah 1.Buat fungsi
1.Masuk ke [Konsol SCF](https://console.cloud.tencent.com/scf) dan klik **Function Service** (Layanan Fungsi) di bilah sisi kiri.
2.Di halaman **Function Service** (Layanan Fungsi), klik **Create** (Buat).
3.Di halaman **Create** (Buat), pilih **Custom** (Khusus) untuk mode kreasinya, dan masukkan nama fungsi.Lalu pilih wilayah yang sama yang Anda pilih untuk instance CLB Anda dan **Python3.6** untuk lingkungan runtime, masukkan kode berikut ke kotak input (Hello CLB digunakan untuk ilustrasi), dan klik **Complete** (Selesai).
>!Saat Anda mengikat instance CLB ke fungsi SCF, konten harus dikembalikan dalam format integrasi respons tertentu.Untuk informasi selengkapnya, lihat [Pemicu CLB](https://intl.cloud.tencent.com/document/product/583/39849).
```plaintext
# -*- coding: utf8 -*-
import json
def main_handler(event, context):

return {
"isBase64Encoded":False,
"statusCode":200,
"headers":{"Content-Type":"text/html"},
"body": "<html><body><h1>Hello CLB</h1></body></html>"
   }
```

### Langkah 2.Deploy fungsi
1.Di halaman daftar "Fungsi", klik nama fungsi yang Anda buat.
2.Di halaman **Function Management** (Manajemen Fungsi), pilih tab **Function Codes** (Kode Fungsi) dan klik **Deploy** di bagian bawah.

### Langkah 3.Ikat fungsinya
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb) dan klik **Instance Management** (Manajemen Instance) di bilah sisi kiri.
2.Di halaman **Instance Management** (Manajemen Instance), klik **Configure Listener** (Konfigurasikan Pendengar) di sebelah kanan instance.
3.Di bagian **HTTP/HTTPS Listener** (Pendengar HTTP/HTTPS), pilih pendengar yang akan diikat dengan fungsi SCF.Klik ikon **+** di sebelah kiri pendengar dan nama domain di bawahnya, pilih jalur URL yang ditampilkan, dan klik **Bind** (Ikat).
4.Di jendela pop-up, pilih SCF sebagai tipe target, atur item konfigurasi, dan klik **Confirm** (Konfirmasi).
5.Pada tab **Listener Management** (Manajemen Pendengar), Anda seharusnya melihat fungsi yang terikat pada instance CLB di bagian **Forwarding Rules** (Aturan Penerusan), yang menunjukkan pemicu CLB sudah dibuat.
>? Anda juga bisa membuat pemicu CLB di konsol SCF untuk mengikat instance CLB dengan fungsi SCF.Untuk informasi selengkapnya, silakan lihat [Membuat Pemicu](https://intl.cloud.tencent.com/document/product/583/31441).

## Validasi Hasil
1.Masuk ke [Konsol SCF](https://console.cloud.tencent.com/scf) dan klik **Function Service** (Layanan Fungsi) di bilah sisi kiri.
2.Pada halaman **Function Service** (Layanan Fungsi), klik fungsi yang baru saja Anda buat.
3.Klik **Trigger Management** (Manajemen Pemicu) di sebelah kiri.
4.Di halaman **Trigger Management** (Manajemen Pemicu), klik **Access Path** (Jalur Akses).
5.Buka jalur akses di peramban.Jika "Hello CLB" ditampilkan, fungsi sudah berhasil di-deploy.


## Referensi
[Membuat fungsi dengan konsol](https://intl.cloud.tencent.com/document/product/583/32742)
