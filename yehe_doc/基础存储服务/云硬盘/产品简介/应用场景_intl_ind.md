## Kasus Penggunaan Standar
### Delokalisasi
- **Penyimpanan data dengan kinerja tinggi dan keandalan tinggi**:Cloud Block Storage (CBS) secara efisien mendukung migrasi panas CVM, mencegah gangguan bisnis yang disebabkan oleh kegagalan fisik.CBS menggunakan mekanisme redundansi data tiga salinan untuk mencadangkan data dan snapshot Anda, dan memulihkan data dalam hitungan detik sehingga cocok untuk sistem dengan beban tinggi dan misi penting.
- **Perluasan elastis**: disk cloud dapat dipasang dan dilepas secara bebas di zona ketersediaan yang sama tanpa mematikan atau memulai ulang CVM.Kapasitas disk cloud dapat dikonfigurasi secara elastis, dan diperluas sesuai permintaan.
![](https://main.qcloudimg.com/raw/1cdbb7fadac1aa88d823eba12a106522.png)

### Analisis data besar-besaran
Dalam kerangka kerja analisis data offline Spark-HDFS yang khas, pembacaan/penulisan RDD dan penulisan acak pada disk adalah IO berurutan, kecuali untuk I/O baca acak. Persentase I/O berurutan sebesar 95%.CBS menampilkan kinerja throughput bersamaan multi-utas yang sangat baik, memungkinkan pemrosesan data offline yang efisien pada tingkat terabyte dan petabyte untuk Hadoop-Mapreduce, HDFS, dan Spark.
Dengan konkurensi multi-disk, satu klaster HDFS dapat mencapai throughput hingga 1 GB/dtk.
CBS mendukung aplikasi data besar seperti analisis data, penambangan data, dan kecerdasan bisnis untuk perusahaan seperti Xiaohongshu, Giant Interactive Group, Ele, Yoho!BUY, dan wepiao.com.
![](https://main.qcloudimg.com/raw/4be675dc660f05c9a7fcd35d9e83973d.png)
**Lingkungan deployment**:5 server CVM (dengan RAM 12-Core 40 GB), mensimulasikan analisis data offline dengan volume data 1,5 TB.
**Uji kinerja**:

- Setiap CVM telah memasang satu disk cloud HDD 1 TB.Lima disk cloud HDD memberikan kecepatan baca 500 MB/dtk, memungkinkan data dibaca ke memori dalam 50 menit.
- Setiap CVM telah memasang satu SSD 1 TB, memungkinkan data dibaca ke memori dalam 25 menit.

### Basis data inti
SSD sangat ideal untuk skenario dengan persyaratan tinggi untuk kinerja IO dan keandalan data.Ini sangat cocok untuk aplikasi basis data relasional sedang dan besar seperti PostgreSQL, MySQL, Oracle, dan SQL Server; untuk sistem bisnis inti intensif IO dengan persyaratan keandalan data yang tinggi; dan untuk lingkungan pengembangan dan pengujian sedang dan besar dengan persyaratan keandalan data yang tinggi.
SSD menawarkan keandalan data dan kinerja tinggi.SSD terus-menerus memberikan dukungan yang dapat diandalkan untuk perusahaan seperti Heroes Evolved, Wendao, Yoho!BUY, weipiao.com, Xiaohongshu, dll.
![](https://main.qcloudimg.com/raw/a826f514194aad6d398069b00ab817da.png)
**Lingkungan deployment**:4 server CVM (dengan RAM 4-Core 8 GB).Masing-masing memiliki satu disk cloud SSD 800 GB yang terpasang, dengan MySQL versi 5.5.42 yang di-deploy.
**Uji kinerja**: menyimulasikan pengujian kinerja OLTP menggunakan sysbench, dengan set pengujian 10 juta catatan.Dalam pengujian ini, TPS dan QPS masing-masing mencapai 1.616 dan 29.000, artinya satu disk cukup untuk mendukung 10 ribu transaksi bersamaan per detik.



## Skenario bisnis umum untuk model I/O
- **Persistensi data per jam**
![](https://main.qcloudimg.com/raw/11e16a3ee744c3cdd313de199b461881.png)
- **Layanan OLTP beban tinggi**
![](https://main.qcloudimg.com/raw/a835908f6a9bcaf8407a299607d33dee.png)
- **Beban ultra-tinggi berkala**
![](https://main.qcloudimg.com/raw/66b6e76d8cc2d477698a21e12cffff8d.png)
- **Baca-tulis berurutan terus menerus**
![](https://main.qcloudimg.com/raw/f08c8eb9b38a1bf0a94cec35fea5538e.png)
