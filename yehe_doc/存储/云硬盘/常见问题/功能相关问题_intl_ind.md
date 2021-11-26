### Apa itu Cloud Block Storage Tencent?
Cloud Block Storage (CBS) Tencent adalah perangkat penyimpanan blok yang sangat tersedia dan sangat andal untuk instance CVM.Perangkat penyimpanan ini menyediakan berbagai macam disk untuk memenuhi persyaratan baca/tulis yang beragam.Untuk informasi selengkapnya tentang CBS, lihat [Ikhtisar](https://intl.cloud.tencent.com/document/product/362/2345).
Kami merekomendasikan CBS ketika data sering berubah dan Anda ingin terus menyimpannya pada kecepatan baca/tulis yang lebih cepat.CBS dapat dilampirkan ke instance apa pun yang berjalan di zona ketersediaan yang sama, memungkinkan Anda menggunakan sistem file dan penyimpanan basis data instance tanpa mengikuti siklus hidup instance.Untuk informasi selengkapnya tentang operasi CBS, lihat [Ikhtisar Operasi](https://intl.cloud.tencent.com/document/product/362/33140).

### Apa saja fitur Tencent Cloud CBS?
Tencent Cloud CBS hadir dengan empat jenis disk:Premium Cloud Storage, SSD, Enhanced SSD, dan Tremendous SSD.Keempat jenis disk tersebut menawarkan fitur berikut:
- Pelampiran dan pelepasan elastis: disk cloud elastis dapat dilampirkan dan dilepas.Hingga 20 disk cloud elastis dapat dilampirkan ke CVM sebagai disk data.
- Perluasan elastis: satu disk mendukung kapasitas maksimum 32 TB.Anda dapat meningkatkan penskalaan disk kapan saja.
- Pencadangan snapshot: Anda dapat membuat snapshot untuk mencadangkan data.Fitur ini meningkatkan keandalan data dan memungkinkan pemulihan data yang cepat bila diperlukan.Anda juga dapat membuat disk cloud dari snapshot untuk mempercepat deployment bisnis Anda.

### Apa perbedaan antara COS dan CBS?
[Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436) tersedia melalui API Web, dan tidak dibatasi oleh sistem file, struktur direktori, jumlah file, atau penyimpanan kapasitas.Layanan ini menawarkan berbagai SDK dan alat untuk integrasi bisnis, yang juga dapat digunakan secara terpisah dari CVM.COS sangat bagus ketika Anda perlu mengakses data dalam jumlah besar tetapi tidak ideal untuk respons tingkat milidetik atau skenario baca/tulis acak.
[CBS](https://intl.cloud.tencent.com/document/product/362) perlu digunakan bersama dengan CVM dan hanya dapat dilampirkan dan digunakan setelah sistem file dipartisi atau diformat.Baik COS maupun CBS memiliki metrik kinerja yang berbeda untuk kasus penggunaan yang berbeda.

### Batasan apa yang dimiliki disk cloud?
- Disk cloud elastis tunggal dapat ditingkatkan penskalaanya hingga 32 TB, dan tidak dapat diturunkan penskalaannya.
- Disk cloud elastis hanya dapat dilampirkan ke CVM dalam zona ketersediaan yang sama.
- Hingga 20 disk cloud elastis dapat dilampirkan ke satu CVM sebagai disk data.Anda dapat langsung melampirkan disk cloud elastis ke CVM yang Anda beli atau [melakukannya nanti](https://intl.cloud.tencent.com/document/product/362/32401).
- Anda dapat membeli hingga 50 disk cloud elastis sekaligus di [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).


### Apa kelebihan dari disk cloud?
Disk cloud menawarkan keandalan, elastisitas, dan kinerja yang tinggi.Disk cloud mudah digunakan dan mendukung pencadangan snapshot.Untuk informasi selengkapnya, lihat [Kelebihan Produk](https://intl.cloud.tencent.com/document/product/362/3039).

### Dapatkah disk cloud digunakan sebagai disk sistem?
Ya.

[](id:Q1)
### Dapatkah disk cloud digunakan sebagai disk data?
Ya.Semua jenis disk lokal dan disk cloud dapat digunakan sebagai disk data.

### Dapatkah disk cloud dilampirkan dan dilepas?
- Disk cloud dapat dilampirkan dan dilepas saat digunakan sebagai disk data.
- Namun, disk cloud tidak dapat dilampirkan dan dilepas saat digunakan sebagai disk sistem.
