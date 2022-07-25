## Latar Belakang Solusi
Penjadwalan push dan pemutaran ulang global CSS didasarkan pada DNS nama domain secara default. Metode akses ini paling umum dan paling sederhana. Karena kompleksitas lingkungan jaringan global, sering terjadi kesalahan resolusi nama domain atau lalu lintas antarjaringan. Anda sebaiknya menggunakan solusi HttpDNS untuk mengoptimalkan penjadwalan siaran langsung global.

Jalur keluar LocalDNS ISP melakukan NAT berdasarkan alamat IP tujuan DNS yang otoritatif atau meneruskan permintaan penyelesaian ke server DNS lain sehingga DNS yang otoritatif tidak dapat mengidentifikasi IP LocalDNS ISP dengan benar. Akibatnya, terjadi kesalahan resolusi nama domain dan lalu lintas antarjaringan.
Berkat teknologi kluster DNS terbaik di dunia, HttpDNS Tencent Cloud mendukung banyak ISP dan lini kustom untuk penjadwalan yang optimal. Informasi selengkapnya dapat dilihat di [HttpDNS].


> Dokumen ini menggunakan edisi gratis HttpDNS sebagai contoh untuk menjelaskan cara menggunakan solusi penjadwalan HttpDNS untuk keperluan streaming langsung global Tencent Cloud. Informasi seputar API edisi gratis dapat dilihat di [dokumentasi] terkait. 

## Menjadwalkan Push Upstream Menggunakan HttpDNS

### 1. Meminta IP titik akses upstream
`http://119.29.29.29/d?dn=$push_domain.&ip=$ip`, yang merupakan permintaan Dapatkan HTTP. Berikut adalah pengertian berbagai parameternya:
- push_domain merupakan nama domain push.
- Bidang IP merupakan IP jalur keluar jaringan eksternal milik pembuat permintaan, yang menunjukkan wilayah dan ISP lokasi IP poin akses terjadwal.


### 2. Menyambungkan URL push upstream
Di sini, server_ip adalah IP yang diperoleh di tahap **Meminta IP Titik Akses Upstream**, dan berikut adalah URL push hasil penyambungan:
`rtmp://server_ip/live/streamname?txTime=xxx&txSecret=xxx&txHost=domain`. Langkah paling penting adalah menambahkan bidang txHost, yang merupakan nama domain push layanan, ke parameter push asal.

## Menjadwalkan Pemutaran Ulang Downstream Menggunakan HttpDNS

### 1. Meminta IP titik akses downstream
`http://119.29.29.29/d?dn=$domain.&ip=$ip`, yang merupakan permintaan Dapatkan HTTP. Berikut adalah pengertian berbagai parameternya:
- domain merupakan nama domain pemutaran ulang.
- Bidang IP merupakan IP jalur keluar jaringan eksternal milik pembuat permintaan, yang menunjukkan wilayah dan ISP lokasi IP poin akses terjadwal.


### 2. Menyambungkan URL pemutaran ulang downstream
- HTTP: Meliputi protokol pemutaran ulang FLV dan HLS. Di sini, server_ip adalah IP yang diperoleh di tahap **Meminta IP Titik Akses Downstream** dan play_domain merupakan nama domain pemutaran ulang. Berikut adalah URL pemutaran ulang HTTP setelah penyambungan:

```
http://server_ip/play_domain/live/streamname.flv?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname.m3u8?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname -123.ts?xxxxxxxxxx
```

- HTTPS: Meliputi protokol pemutaran ulang FLV dan HLS. Di sini, server_ip adalah IP yang diperoleh di tahap **Meminta IP Titik Akses Downstream** dan play_domain merupakan nama domain pemutaran ulang. Aturan penyambungan HTTPS mengikuti logika pemutar. **IP tujuan tempat disambungkannya koneksi berdasarkan TCP harus berupa server_ip penjadwalan HttpDNS**, dan URL pemutaran ulang spesifik yang diminta harus ditujukan untuk permintaan pemutaran ulang umum:

```java
https://play_domain/live/ streamname.flv?xxxxxxxxxx
https://play_domain/live/ streamname.m3u8?xxxxxxxxxx
https://play_domain/live/ streamname -123.ts?xxxxxxxxxx
```

- RTMP: Di sini, server_ip adalah IP yang diperoleh di tahap **Meminta IP Titik Akses Downstream** dan play_domain merupakan nama domain pemutaran ulang. Berikut adalah URL pemutaran ulang RTMP setelah penyambungan:

```
rtmp://server_ip/play_domain/live/ streamname?xxxxxxxxxx
```

>Semua skema di atas didasarkan pada platform penjadwalan global CSS sehingga tidak dapat digunakan untuk penjadwalan di Tiongkok Daratan tanpa modifikasi yang diperlukan.
