CLB mendukung pembuatan instance CLB Anycast.CLB Anycast adalah layanan penyeimbangan beban yang mendukung akselerasi dinamis lintas wilayah.VIP CLB dipublikasikan di beberapa wilayah.Klien menghubungkan ke POP terdekat dan meneruskan lalu lintas ke instance CVM melalui internet kecepatan tinggi IDC Tencent Cloud.
CLB Anycast bisa mencapai pengoptimalan transfer jaringan dan akses multi-entri terdekat dan mengurangi jitter jaringan dan kehilangan paket, yang pada akhirnya bisa meningkatkan kualitas layanan aplikasi dalam cloud, memperluas cakupan layanan, dan mempersingkat deployment backend.
>?Fitur ini sedang dalam pengujian beta.Untuk menerapkan uji coba, kirimkan tiket untuk kelayakan pengujian beta.

## Apa itu Anycast?
Anycast artinya, saat IP yang sama dipublikasikan di beberapa lokasi secara bersamaan, algoritme perutean akan mengirimkan lalu lintas pengguna ke router terdekat.
Keunggulan CLB Anycast:
- **Low latency** (Latensi rendah)
CLB Anycast memublikasikan VIP ke beberapa wilayah sekaligus melalui Anycast.Berdasarkan protokol transfer, paket permintaan akan tiba di wilayah publikasi VIP yang optimal untuk memperoleh akses khusus ke Tencent Cloud dan kemudian mencapai instance CVM melalui jaringan pribadi Tencent Cloud, menghindari kemacetan jaringan publik dan mengurangi latensi.
- **Reduced jitter and packet loss** (Mengurangi jitter dan kehilangan paket)
Ketidakstabilan transmisi jaringan publik lintas batas atau lintas pembawa bisa menyebabkan jitter jaringan dan kehilangan paket, dan merusak pengalaman layanan.Sebaliknya, CLB Anycast menawarkan kestabilan transmisi tinggi.Hal ini memberikan permintaan klien terdekat akses ke Tencent Cloud dan mengaktifkan transmisi lintas wilayah melalui koneksi jaringan pribadi khusus Tencent Cloud, membantu menghilangkan jitter dan kehilangan paket.
- **High reliability** (Keandalan tinggi)
Transmisi melalui jaringan publik mungkin tidak bisa diandalkan.Saat masalah baris khusus ISP membuat layanan tidak bisa diakses, pengguna biasanya harus menunggu hingga layanan kembali.Dengan bantuan CLB Anycast, jaringan pribadi Tencent Cloud, jaringan ISP, dan Tencent Cloud POP bisa mencapai beberapa jalur dan entri jaringan untuk menghilangkan kegagalan yang disebabkan oleh satu wilayah atau jalur dan meningkatkan kestabilan jaringan.
- **Simplified deployment** (Deployment disederhanakan)
Saat klien Anda tersebar di seluruh wilayah dan membutuhkan akses terdekat, Anda harus men-deploy server di semua wilayah itu dan mengonfigurasikan DNS untuk mencapai penyeimbangan beban, dan IP yang bervariasi per wilayah membuat deployment jadi lebih rumit.Melalui CLB Anycast, atribut wilayah dipusatkan di level IP sehingga tidak membutuhkan konfigurasi IP untuk setiap wilayah.Selain itu, Anda hanya perlu mempertahankan satu set logika bisnis di backend, dan permintaan dari berbagai wilayah diarahkan langsung ke server-server asli melalui akselerasi jaringan pribadi.

## Arsitektur CLB Anycast
Arsitektur CLB Anycast seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/22e2999156768fa7866b70001280fce5.png)
VIP CLB Anycast dipublikasikan ke berbagai wilayah di seluruh dunia.Klien terhubung ke POP terdekat dan meneruskan lalu lintas akses secara ultra cepat ke instance CVM melalui jaringan pribadi Tencent Cloud.

### Wilayah publikasi Anycast
Wilayah publikasi Anycast adalah tempat alamat IP yang dipercepat dipublikasikan, yaitu, POP tempat VIP CLB Anycast dipublikasikan.Klien mengakses POP terdekat.Saat ini, CLB Anycast mendukung publikasi serentak di wilayah-wilayah berikut ini:Beijing, Shanghai, Guangzhou, Hong Kong (Tiongkok), Toronto, Silicon Valley, Frankfurt, Virginia, Moscow, Singapore, Seoul, Mumbai, Bangkok, dan Tokyo.

### Wilayah CLB Anycast
Seperti wilayah instance CLB generik, wilayah CLB Anycast adalah wilayah yang Anda pilih saat membeli instance CLB Anycast atau wilayah tempat server asli Anda berada.Saat ini, CLB Anycast tersedia di sebagian besar wilayah.
- Tiongkok:Beijing, Shanghai, Guangzhou, dan Hong Kong SAR.
- Eropa dan Amerika Utara:Toronto, Silicon Valley, Frankfurt, Virginia, dan Moscow.
- Asia Tenggara:Singapore, Seoul, Mumbai, Bangkok, dan Tokyo.

>?
>- Kemampuan anycast dari CLB Anycast diimplementasikan dengan mengikat EIP Anycast ke instance CLB jaringan pribadi.
>- EIP Anycast bisa diikat ke instance CLB jaringan pribadi, tetapi tidak ke instance CLB jaringan pribadi klasik atau instance CLB jaringan klasik.
>

## Kasus Penggunaan CLB Anycast
### Server terpadu untuk akses lintas wilayah
Jika Anda dalam industri game, Anda bisa berharap para pemain dari berbagai tempat ada di satu wilayah server atau bahwa cabang-cabang Anda di seluruh dunia bisa berbagi IDC yang sama.Anda bisa menggunakan CLB Anycast untuk men-deploy server-server asli di satu wilayah (seperti Guangzhou), membeli instance CLB Anycast di wilayah tersebut dan memilih wilayah publikasi sesuai kebutuhan.Dengan cara ini, pemain atau karyawan bisa memperoleh akses terdekat ke server asli yang sama.
![](https://main.qcloudimg.com/raw/548f5853d5d56af85a248d5ee64d2c39.png)

### Akselerasi game
CLB Anycast telah digunakan secara luas dalam akselerasi game.Melalui CLB Anycast CLB, permintaan game bisa mendapat akses terdekat ke Tencent Cloud dan mencapai server game melalui jaringan pribadi Tencent Cloud, mempersingkat jalur jaringan publik dan mengurangi masalah seperti penundaan, jitter, dan kehilangan paket.Dibandingkan akselerasi tradisional, CLB Anycast tidak membutuhkan deployment penerima lalu lintas ekstra pada entri dan menghapus kebutuhan zoning sehingga menyederhanakan deployment DNS.
![](https://main.qcloudimg.com/raw/c1db004b30c41a6c0968e95a2197332b.png)


## Panduan Pengoperasian
### Prasyarat
Fitur ini saat ini dalam versi beta.Pastikan aplikasi Anda untuk kelayakan pengujian beta sudah disetujui sebelum memakainya.

### Petunjuk
1.Masuk ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2.Pada bilah sisi kiri, klik **[EIP](https://console.cloud.tencent.com/cvm/eip2)** untuk masuk ke halaman manajemen EIP.
3.Klik **Apply** (Terapkan).Di jendela pop-up, pilih **Accelerated IP** (IP Dipercepat) sebagai jenis alamat IP dan klik **OK**.
![](https://main.qcloudimg.com/raw/838f629b9d40c4db3be1e98dbd95c7f3.png)
4.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb), pilih instance CLB jaringan pribadi (instance CLB klasik tidak didukung), dan klik **More** (Lainnya) > **Bind Accelerated IP** (Ikat IP Dipercepat) di kolom "Operasi".
![](https://main.qcloudimg.com/raw/e4877ad575321d2599b3258cf741a8a3.png)
5.Setelah instance CLB jaringan pribadi terikat ke IP yang dipercepat, layanan CLB Anycast bisa diberikan.Untuk informasi selengkapnya tentang konfigurasi CLB, silakan lihat [Ikhtisar Pendengar CLB](https://intl.cloud.tencent.com/document/product/214/6151).
![](https://main.qcloudimg.com/raw/f8e1334deb5679de7b5330208782a5e4.png)
