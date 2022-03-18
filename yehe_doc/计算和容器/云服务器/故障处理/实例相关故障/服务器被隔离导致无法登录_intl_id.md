Dokumen ini menjelaskan cara mengatasi kegagalan login jika CVM diisolasi dari jaringan publik.

## Masalah
CVM mungkin telah diisolasi karena melanggar undang-undang dan peraturan saat ini. Anda dapat menggunakan metode berikut untuk memeriksa apakah CVM diisolasi.
- Saat CVM diisolasi dari jaringan publik, Anda akan diberi tahu tentang isolasi tersebut melalui [pesan internal di konsol](https://console.cloud.tencent.com/message) atau pesan teks.
<!--
 - Pesan Internal:
![](//mc.qcloudimg.com/static/img/3c8ecd4ac301180e3632a25343be0697/image.png)
Atau
![](//mc.qcloudimg.com/static/img/cd3fbf748d3ff61adf3d2198853d18de/image.png)
 - SMS:
![](//mc.qcloudimg.com/static/img/afaff154fa12695844055422f4f103e6/image.png)
- Tab **Monitoring/Status** (Pemantauan/Status) di [Konsol CVM](https://console.cloud.tencent.com/cvm/index) menampilkan status CVM: Diisolasi.
-->

## Penyebab
Ketika pelanggaran peraturan atau peristiwa risiko terjadi untuk CVM, mesin yang melanggar akan diisolasi sebagian (kecuali untuk port login jaringan pribadi 22, 36000, dan 3389, semua akses jaringan akan diisolasi. Pengembang dapat menggunakan server lompat untuk login ke server.
Untuk detailnya, lihat Klasifikasi Tingkat Pelanggaran Keamanan Cloud dan Deskripsi Hukuman.

## Solusi

 1. Hapus konten yang melanggar seperti yang diperintahkan oleh pesan internal atau pesan teks. Atasi risiko keamanan dan instal ulang sistem jika perlu.
 2. Jika pelanggaran tersebut tidak disebabkan oleh tindakan Anda sendiri, CVM Anda mungkin mengalami gangguan berbahaya. Untuk mengatasi ini, lihat [Keamanan Host](https://intl.cloud.tencent.com/document/product/296).
 3. Setelah mengatasi risiko keamanan dan menghapus konten yang melanggar, Anda dapat [kirim tiket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM) untuk menghubungi layanan pelanggan untuk menghapus isolasi.

