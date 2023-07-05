## Deskripsi Masalah

Akses situs web lambat.

## Analisis Masalah

Permintaan HTTP yang lengkap termasuk menyelesaikan nama domain, membuat koneksi TCP, memulai permintaan, CVM menerima dan memproses permintaan, mengembalikan hasilnya, browser mengurai kode HTML, meminta sumber daya lain, dan merender halaman. Proses ini melibatkan klien lokal, node jaringan antara klien dan server, dan server. Masalah dengan salah satu dari mereka dapat menyebabkan latensi akses jaringan.

## Solusi

### Periksa klien lokal
1. Akses [situs web pengujian jaringan](https://ping.huatuo.qq.com) untuk menguji kecepatan akses ke nama domain yang berbeda dari klien lokal.
2. Berdasarkan hasil pengujian, periksa apakah jaringan lokal memiliki pengecualian.
Misalnya, hasil pengujian seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/1dfe4866d4572d82841225b60d127a1c.png)
Hasil pengujian menunjukkan latensi akses untuk setiap nama domain dan apakah jaringan normal.
 - Jika jaringan memiliki pengecualian, hubungi ISP Anda untuk mencari dan memecahkan masalah.
 - Jika jaringan normal, silakan [periksa tautan jaringan](#CheckNetworkLink).

<span id="CheckNetworkLink"></span>
### Periksa tautan jaringan

1. Lakukan ping IP publik server dari klien lokal untuk memeriksa apakah ada paket yang hilang atau latensi tinggi.
 - Jika salah satu masalah terjadi, gunakan MTR untuk pemecahan masalah. Untuk informasi selengkapnya, silakan lihat [Latensi Jaringan CVM dan Kehilangan Paket](https://intl.cloud.tencent.com/document/product/213/14638).
 - Jika uji ping tidak menunjukkan kehilangan paket atau latensi tinggi, jalankan [langkah 2](#CheckNetworkLink_step2).
2. <span id="CheckNetworkLink_step2">Gunakan perintah `dig/nslookup` untuk memeriksa apakah masalah disebabkan oleh resolusi DNS. </span>
Anda juga dapat mengakses halaman secara langsung dengan IP jaringan publik untuk memeriksa apakah DNS telah menyebabkan latensi akses.
- Jika DNS memiliki pengecualian, periksa resolusi DNS.
- Jika DNS normal, silakan [periksa server](#CheckServer).
<span id="CheckServer"></span>
### Periksa server

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Klik ID/nama instans yang ingin Anda periksa untuk masuk ke halaman detailnya.
3. Pilih tab **Monitoring** (Pemantauan) pada halaman detail untuk melihat penggunaan sumber daya instans, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/b8396a4507dd6a9808f9907b90e881fa.png)
 - Jika penggunaan CPU/memori terlalu tinggi, silakan lihat [Gagal login ke CVM Windows karena penggunaan CPU dan memori yang tinggi](https://intl.cloud.tencent.com/document/product/213/32405) dan [Gagal login ke CVM Linux karena penggunaan CPU dan memori yang tinggi](https://intl.cloud.tencent.com/document/product/213/32387) untuk pemecahan masalah.
 - Jika penggunaan bandwidth terlalu tinggi, silakan lihat [Kegagalan Login Karena Penggunaan Bandwidth Tinggi](https://intl.cloud.tencent.com/document/product/213/32542) untuk pemecahan masalah. 
 - Jika penggunaan sumber daya instans normal, silakan [periksa masalah lain](#CheckOtherProblems).

<span id="CheckOtherProblems"></span>
### Periksa masalah lain

Berdasarkan penggunaan sumber daya instans, periksa apakah peningkatan konsumsi sumber daya disebabkan oleh beban server.
 - Jika ya, kami sarankan Anda mengoptimalkan proses bisnis, [mengubah konfigurasi instans](https://intl.cloud.tencent.com/document/product/213/2178), atau membeli server baru untuk mengurangi tekanan pada server yang ada.
 - Jika tidak, kami sarankan Anda memeriksa file log untuk menemukan masalah dan melakukan pengoptimalan yang ditargetkan.

