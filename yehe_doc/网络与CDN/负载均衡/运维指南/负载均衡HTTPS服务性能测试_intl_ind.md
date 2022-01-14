
## 1.Kemampuan HTTPS dari CLB
Dengan mengoptimalkan tumpukan protokol dan server, Tencent Cloud CLB meningkatkan kinerja HTTPS secara signifikan.Selain itu, Tencent Cloud sangat menghemat biaya sertifikat melalui kerja sama internasional.Tencent CLB dapat menguntungkan bisnis Anda untuk hal-hal berikut:
1.Penggunaan HTTPS tidak memengaruhi kecepatan akses klien.
2.Kinerja enkripsi dan dekripsi SSL dari satu server dalam sebuah kluster mendukung handshake penuh hingga 65.000 koneksi per detik (CPS), yang sekurang-kurangnya 3,5 kali lebih tinggi daripada CPU berkinerja tinggi.Keunggulan ini mengurangi biaya server, meningkatkan kemampuan layanan secara tajam selama jam-jam kerja bisnis dan puncak lalu lintas, serta memperkuat kemampuan tangkal serangan.
3.Offloading dan konversi beberapa protokol didukung, yang mengurangi tekanan bisnis dalam beradaptasi dengan beragam protokol klien.Backend bisnis hanya perlu mendukung HTTP/1.1 untuk menggunakan protokol dengan versi berbeda, seperti HTTP/2, SPDY, SSL 3.0, dan TLS 1.2.
4.Aplikasi, pemantauan, dan penggantian sertifikat SSL satu atap didukung.Tencent Cloud bekerja sama dengan dua otoritas sertifikat internasional, Comodo dan Symantec, untuk menyederhanakan proses aplikasi sertifikat dan menurunkan biaya.
5.Tersedia Fitur Anti-CC dan WAF untuk menghadang serangan lapisan-aplikasi, seperti serangan HTTP lambat, serangan dengan target frekuensi tinggi, injeksi SQL, dan trojan situs web.

## 2.Tujuan Pengujian
Layanan HTTPS memiliki keunggulan seperti autentikasi identitas, enkripsi informasi, dan verifikasi integritas.Akan tetapi, penggunaan protokol SSL untuk menerapkan komunikasi yang aman mengakibatkan hilangnya kinerja tertentu, termasuk meningkatnya latensi dan konsumsi sumber daya CPU oleh enkripsi dan dekripsi.Dokumen ini mencakup data pengujian kinerja ekstrem dari layanan HTTPS Tencent Cloud selama enkripsi dan dekripsi SSL.Anda dapat membandingkannya dengan data kinerja HTTPS tradisional.

## 3.Lingkungan Pengujian
- Alat pengujian tekanan: wrk 4.0.2
- Lingkungan layanan penopang Tencent Cloud:Nginx 1.1.6–1.9.9 + OpenSSL 1.0.2h
- Informasi tentang OS untuk menginstal Nginx:Linux TENCENT64.site 3.10.94-1-tlinux2-0036.tl2 # 1 SMP Kam Jan 21 03:40:59 CST 2016 x86_64 x86_64 x86_64 GNU/Linux
- OS untuk server tekanan lainnya:Linux TENCENT64.site 2.6.32.43-tlinux-1.0.17-default #1 SMP Sel Nov 17 18:03:12 CST 2015 x86_64 x86_64 x86_64 GNU/Linux

## 4.Skema pengujian kluster WebServer
Tekanan dari satu server tidak cukup untuk menguji batas kinerja layanan HTTPS dari Tencent Cloud.Beberapa server tekanan diperlukan.Pengujian meliputi tiga bagian:
1.Kluster pengujian tekanan.Kluster pengujian ini digunakan untuk mendistribusikan tekanan HTTP/HTTPS dan memberikan output hasil pengujian tekanan dari satu server tekanan.
2.Server kontrol pusat, yang mengontrol permulaan dan akhir kluster pengujian tekanan, mendapatkan data pengujian dari setiap server tekanan lalu mengagregat dan memberikan output data.
3.Server web, berupa instance CVM yang menghosting layanan HTTPS dari Tencent Cloud.Ketika kinerja WebServer diuji, sebuah halaman dapat dikembalikan langsung tanpa koneksi upstream.
Koneksinya adalah sebagai berikut:

![](https://mc.qcloudimg.com/static/img/180044320ba540f396a06925d8f07bbd/CLB-OPS+Guidelines-Load+Balancer+HTTPS+Service+Performance+Test.jpg)

## 5.Data pengujian kinerja dari WebServer HTTPS

| Jenis Koneksi | Cache Sesi | Ukuran Paket (dalam byte) | Paket Enkripsi | Kinerja (QPS) |
|---------|---------|---------|---------|---------|
| Persisten | Aktif | 230 | ECDHE-RSA-AES128-GCM-SHA256 | 296241 |
| Tidak Persisten | Nonaktif | 230 | ECDHE-RSA-AES128-GCM-SHA256 | 65630 |

## 6.Kesimpulan pengujian kemampuan HTTPS CLB
Menurut tabel di atas, layanan HTTPS dari Tencent Cloud mendukung enkripsi dan dekripsi SSL.Layanannya memiliki beberapa kluster server di backend, dan satu server dalam sebuah kluster dapat meraih kinerja hingga 65.000 QPS selama handshake penuh dan sekitar 300.000 QPS selama koneksi tanpa putus.

Dalam kondisi normal, protokol HTTPS menambahkan sedikitnya satu proses handshake penuh ketika menggunakan protokol SSL, dan latensi meningkat sebesar 2 * waktu round-trip (RTT).Selain itu, enkripsi simetris/asimetris SSL mengonsumsi sumber daya CPU dalam jumlah besar.Kemampuan dekripsi RSA merupakan penghalang utama bagi akses berbasis HTTPS.

Dengan layanan HTTPS Tencent Cloud, Anda tidak perlu men-deploy layanan tambahan untuk enkripsi dan dekripsi SSL.Tanpa beban biaya tambahan, layanan ini memudahkan Anda menikmati kemampuan hosting bisnis dan tangkal serangan yang andal.
