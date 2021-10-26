
Dokumen ini menguraikan cara menggunakan Tencent Cloud CDN untuk mempercepat akses ke COS.


## Jaringan Pengiriman Konten (CDN)
Dengan mengirim sumber daya ke sejumlah besar simpul cache yang di-deploy secara global dan memanfaatkan sistem penjadwalan GSLB Tencent yang dibuat secara independen, CDN memungkinkan akses dekat ke sumber daya yang diperlukan bagi pengguna akhir.Ini mengurangi penundaan akses yang disebabkan oleh kemacetan jaringan, jarak, dan masalah ISP serta secara efektif meningkatkan kecepatan unduh, responsivitas, dan pengalaman pengguna.


## Penyimpanan Objek Cloud (COS)
Anda dapat menyimpan semua sumber daya statis, seperti skrip statis, file audio/video, gambar, dan lampiran dalam penyimpanan standar di COS, yang menyediakan kapasitas tak terbatas dan pembacaan/penulisan frekuensi tinggi untuk memberikan penyimpanan yang dapat disesuaikan dan andal untuk sumber daya statis serta mengurangi tekanan pada server sumber daya.


## Praktik Pengiriman Konten
CDN dapat mempercepat pengiriman global sumber daya statis, seperti skrip statis, file audio/video, gambar, dan lampiran yang disimpan di COS.Dengan simpul cache global dan kemampuan penjadwalan CDN, sumber daya yang sering diminta dapat dikirimkan sebelumnya ke server tepi.Ketika sumber daya tersebut diakses atau diunduh oleh pengguna akhir, sumber daya yang ter-cache di simpul yang dekat akan dikembalikan.Ini mengurangi tekanan pada server asal serta penundaan transfer sehingga secara signifikan meningkatkan pengalaman pengguna.
![](https://main.qcloudimg.com/raw/6316f3fde6226ad974d0bc17592c1425.png)

>! [Jaringan Pengiriman Konten Tencent Cloud Enterprise (ECDN)](https://intl.cloud.tencent.com/product/ecdn) dapat digunakan untuk mempercepat pengiriman sumber daya dinamis/statis atau sumber daya dinamis yang disimpan di COS.


## Implementasi

Akselerasi CDN dapat diimplementasikan untuk COS dengan dua cara berikut.Pilih salah satu di antaranya untuk menyelesaikan akselerasi：

- Arahkan endpoint COS ke nama domain akselerasi CDN dan ikatkan nama domain Anda ke nama domain akselerasi CDN (melalui CNAME).Untuk mendapatkan petunjuk lengkap, silakan lihat [Implementasi via Konsol CDN](https://intl.cloud.tencent.com/document/product/228/32984).
- Ikatkan nama domain Anda ke endpoint COS dan aktifkan akselerasi CDN.Untuk mendapatkan petunjuk lengkap, silakan lihat [Pelaksanaan via Konsol COS](https://intl.cloud.tencent.com/document/product/228/32985).

