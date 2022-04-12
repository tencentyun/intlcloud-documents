Baik klasik maupun VPC adalah ruang jaringan di cloud. VPC lebih aman dan terkendali. Meskipun sebagian besar CVM di-deploy di Tencent Cloud VPC, beberapa aplikasi tetap berjalan di jaringan klasik yang memerlukan interkoneksi dengan VPC. Untuk mengatasi masalah ini, Tencent Cloud memberikan solusi berikut.

## Saling Menghubungkan Jaringan Klasik dan VPC
   ![](https://qcloudimg.tencent-cloud.cn/raw/736af560727e55c1f907d873f357473b.png)
+  **Classiclink**
Ini menghubungkan CVM berbasis jaringan klasik dengan VPC tertentu sehingga CVM ini dapat berkomunikasi dengan sumber daya VPC seperti instans CVM dan TencentDB. Namun, ini hanya menyediakan akses antara CVM berbasis VPC dan CVM berbasis jaringan klasik, alih-alih sumber daya cloud lainnya, termasuk TencentDB dan CLB dalam jaringan klasik.
+  **Terminal connection** (Koneksi terminal)
 Koneksi ini membantu instans dalam VPC berkomunikasi dengan sumber daya di jaringan klasik (kecuali CVM) melalui jaringan pribadi. Koneksi terminal membuat pemetaan antara alamat IP instans jaringan klasik dan alamat IP VPC sehingga instans jaringan klasik dapat diakses dengan mengakses alamat IP VPC. Produk jaringan klasik yang mendukung koneksi terminal mencakup instans CLB, MySQL, Memcached, Redis, MariaDB, SQL Server, PostgreSQL, MongoDB, dan TDSQL.
>?Koneksi terminal tidak mendukung komunikasi lintas wilayah atau lintas akun. Jika Anda ingin membuat koneksi terminal, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category).


## Migrasi dari Jaringan Klasik ke VPC
 Tencent Cloud VPC direkomendasikan karena keamanan, fleksibilitas, dan kemampuan kontrolnya. Saat ini, Tencent Cloud mendukung migrasi sumber daya dari jaringan klasik ke VPC. Untuk informasi selengkapnya, lihat [Migrasi dari Jaringan Klasik ke VPC](https://intl.cloud.tencent.com/document/product/215/41414).
## Referensi
+ Untuk informasi selengkapnya tentang jaringan klasik dan perbedaannya dengan VPC, lihat [Jaringan Klasik](https://cloud.tencent.com/document/product/215/58039).
+ Untuk informasi selengkapnya tentang konfigurasi Classiclink, lihat [Classiclink](https://intl.cloud.tencent.com/document/product/215/41418).
