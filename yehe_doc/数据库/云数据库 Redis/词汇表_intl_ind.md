

### Wilayah

Wilayah mengacu pada lokasi geografis tempat pusat data yang dihosting oleh Tencent Cloud berada. Setiap wilayah memiliki beberapa zona ketersediaan.
Misalnya, wilayah satu pusat data yang dihosting adalah Beijing, dan zona ketersediaannya adalah Zona Beijing 1. Layanan Tencent Cloud di wilayah yang sama dapat berkomunikasi satu sama lain melalui jaringan pribadi, tetapi layanan di wilayah yang berbeda tidak bisa. Oleh karena itu, disarankan untuk memilih wilayah yang paling dekat dengan pelanggan Anda untuk meminimalkan latensi akses dan meningkatkan kecepatan unduh.

### Pemisahan Baca/Tulis 

Pemisahan Baca/Tulis memungkinkan instans master untuk melakukan operasi transaksi seperti penyisipan, pembaruan, dan penghapusan (INSERT, UPDATE, dan DELETE) dan instans slave (baca-saja) untuk melakukan operasi kueri SELECT.



## Zona ketersediaan

Zona ketersediaan (AZ) adalah IDC fisik Tencent Cloud dengan catu daya dan sumber daya jaringan independen di satu wilayah. AZ dirancang untuk memastikan stabilitas bisnis karena kegagalan di satu AZ diisolasi tanpa memengaruhi AZ lain di wilayah yang sama.



### QPS

QPS (Kueri per Detik) mengukur permintaan yang diproses secara bersamaan per detik. 1 QPS berarti bahwa API memproses 1 permintaan per detik; 50 QPS berarti API memproses 50 permintaan per detik.



### Mesin database

Mesin database adalah layanan inti untuk menyimpan, memproses, dan melindungi data. Mesin database memungkinkan Anda untuk mengontrol izin akses dan memproses transaksi dengan cepat untuk memenuhi persyaratan sebagian besar aplikasi untuk memproses sejumlah besar data dalam skenario perusahaan. Mesin database didukung oleh setiap instans database.



### TencentDB for Redis

TencentDB for Redis adalah database yang disediakan oleh Tencent Cloud berdasarkan protokol Redis dan pengalaman teknologi Tencent selama bertahun-tahun dalam caching terdistribusi, yang menampilkan ketersediaan, keandalan, dan fleksibilitas tinggi. Kompatibel dengan protokol Redis 2.8, 4.0, dan 5.0 dan tersedia dalam arsitektur standar dan klaster, TencentDB for Redis mendukung kapasitas penyimpanan hingga 4 TB dan puluhan juta permintaan bersamaan, sehingga memenuhi kebutuhan skenario yang berbeda seperti caching, penyimpanan, dan komputasi.