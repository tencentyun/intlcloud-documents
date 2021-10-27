Dokumen ini menguraikan cara menggunakan Tencent Cloud CDN untuk mempercepat akses ke CVM.

## Jaringan Pengiriman Konten (CDN)
Dengan mengirim sumber daya ke sejumlah besar simpul cache yang di-deploy secara global dan memanfaatkan sistem penjadwalan GSLB Tencent yang dibuat secara independen, CDN memungkinkan akses dekat ke sumber daya yang diperlukan bagi pengguna akhir.Ini mengurangi penundaan akses yang disebabkan oleh kemacetan jaringan, jarak, dan masalah ISP serta secara efektif meningkatkan kecepatan unduh, responsivitas, dan pengalaman pengguna.

## Mesin Virtual Cloud (CVM)
CVM menyediakan sumber daya komputasi virtual yang dapat disesuaikan di cloud.Anda dapat meluncurkan contoh CVM pada sistem operasi yang berbeda dan memuatnya ke dalam lingkungan aplikasi khusus Anda.Jika bisnis Anda memerlukan perubahan, Anda dapat menyesuaikan sumber daya komputasi Anda dengan segera dan dengan demikian menyesuaikan spesifikasi contoh CVM Anda.


## Praktik Pengiriman Konten

CDN dapat mempercepat pengiriman global sumber daya statis, seperti sejumlah besar file audio/video, gambar, dan file yang disimpan di CVM.Dengan simpul cache global dan kemampuan penjadwalan CDN, sumber daya yang sering diminta dapat dikirimkan sebelumnya ke server tepi.Ketika sumber daya tersebut diakses atau diunduh oleh pengguna akhir, sumber daya yang ter-cache di simpul yang dekat akan dikembalikan.

Akselerasi CDN untuk CVM tidak hanya mengurangi tekanan pada server asal, penundaan transfer, dan biaya bandwidth, tetapi juga meningkatkan secara signifikan ketersediaan layanan.
![](https://main.qcloudimg.com/raw/66e176f86760440228d930e077f21247.png)

>! [Jaringan Pengiriman Konten Tencent Cloud Enterprise (ECDN)](https://intl.cloud.tencent.com/product/ecdn) dapat digunakan untuk mempercepat pengiriman sumber daya dinamis/statis atau sumber daya dinamis yang disimpan di CVM.


## Implementasi

Akselerasi CDN dapat diimplementasikan untuk CVM dengan cara berikut:

Mengikatkan nama domain akselerasi CDN ke nama domain CVM atau alamat IP dan mengaktifkan layanan akselerasi CDN.Untuk mendapatkan petunjuk selengkapnya, silakan lihat [Implementasi via Konsol CDN](https://intl.cloud.tencent.com/document/product/228/32988).
