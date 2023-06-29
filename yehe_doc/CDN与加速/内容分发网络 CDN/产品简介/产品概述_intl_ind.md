## Ikhtisar CDN

Content Delivery Network (CDN) adalah lapisan baru arsitektur jaringan yang dibangun pada internet yang sudah ada.CDN berupa simpul cache berperforma tinggi yang tersebar di seluruh dunia untuk mempercepat penayangan konten internet.Simpul tersebut menyimpan konten Anda berdasarkan kebijakan peng-cache-an.Ketika pengguna mengirim permintaan konten, permintaan tersebut akan diarahkan ke simpul yang terdekat dengan pengguna sehingga mengurangi penundaan akses dan meningkatkan ketersediaan.

CDN memberikan solusi yang efektif bagi masalah jaringan berikut:
1.Jarak fisik yang panjang antara pengguna dan server bisnis mengharuskan permintaan diteruskan beberapa kali sehingga mengakibatkan latensi tinggi dan ketidakstabilan.
2.ISP yang digunakan pengguna berbeda dengan yang digunakan server bisnis sehingga permintaan harus diteruskan antar-ISP setelah ISP-ISP tersebut saling terkoneksi.
3.Server bisnis memiliki keterbatasan bandwidth dan kemampuan pemrosesan sehingga mengakibatkan tanggapan yang lebih lambat dan ketersediaan lebih rendah ketika jumlah permintaan pengguna menumpuk..

CDN itu mudah digunakan.Anda tidak perlu menyesuaikan struktur bisnis atau mengelola konfigurasi yang kompleksUntuk informasi selengkapnya, silakan baca [Memulai](https://intl.cloud.tencent.com/document/product/228/32978).

## Cara Kerja Akselerasi
Misalnya, jika nama domain server asal bisnis Anda adalah `www.test.com` dan sudah terkoneksi dengan CDN untuk mengaktifkan layanan akselerasi, ketika seorang pengguna mengirim permintaan HTTP, maka permintaan akan diproses sebagai berikut:
![](https://main.qcloudimg.com/raw/c155f8268c6ebdcc84f50cfb06f1f638.png)

**The process is detailed below:** (Perincian proses tercantum di bawah):
1.Ketika pengguna mengirim permintaan akses ke sumber daya gambar (misalnya, 1.jpg) di `www.test.com`, permintaan penyelesaian nama domain akan diinisiasikan ke DNS lokal.
2.Ketika DNS lokal menyelesaikan `www.test.com`, CNAME `www.test.com.cdn.dnsv1.com` telah mengalami konfigurasi, maka permintaan penyelesaian akan dikirimkan ke Tencent DNS (GSLB), yaitu sistem penjadwalan milik Tencent Cloud yang akan menetapkan IP simpul optimal untuk permintaan tersebut.
3.DNS lokal menerima IP yang sudah jadi yang dikembalikan oleh Tencent DNS.
4.Pengguna menerima IP yang sudah jadi.
5.Pengguna mengirim permintaan akses untuk 1.jpg ke IP yang diterima.
6.Jika simpul CDN yang sesuai dengan IP sudah membuat cache 1.jpg, data akan langsung dikembalikan ke pengguna tersebut (10) dan permintaan pun selesai.Atau, simpul CDN akan menginisiasi permintaan 1.jpg ke server asal (6, 7, dan 8).Setelah menerima sumber daya, simpul CDN akan membuat cache sumber daya tersebut (9) berdasarkan kebijakan caching yang sudah terkonfigurasi (silakan baca [Konfigurasi Waktu Kedaluwarsa Cache](https://intl.cloud.tencent.com/document/product/228/35317) dan kembalikan kepada pengguna (10) untuk mengakhiri permintaan.
