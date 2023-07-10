Untuk menjaga keandalan data yang tinggi, penting untuk menyediakan lingkungan pemantauan yang baik untuk disk cloud.Anda dapat menggunakan Cloud Monitor untuk memantau disk cloud yang ***telah dipasang ke sebuah instance***.Saat Anda perlu mengumpulkan statistik disk cloud, lakukan operasi Memasang Disk Cloud ke Instance CVM.Dengan Cloud Monitor, Anda dapat melihat data metrik disk cloud, dan menganalisis serta mengatur alarm untuk disk cloud.Sekarang, Cloud Monitor menyediakan disk cloud dengan metrik pemantauan berikut:


| Item Pemantauan | Metrik Pemantauan | Arti di Linux | Arti di Windows | Satuan | Dimensi
|---------|---------|--|--|--|--|
| Lalu lintas baca disk | disk_read_traffic | Volume data rata-rata yang dibaca dari disk ke memori per detik, ambil nilai maksimum di antara semua partisi | Volume data rata-rata yang dibaca dari disk ke memori per detik, ambil nilai maksimum di antara semua partisi | KB/dtk | unInstanceId |
| Lalu lintas penulisan disk | disk_write_traffic | Volume data rata-rata yang ditulis dari memori ke disk per detik, ambil nilai maksimum di antara semua partisi | Volume data rata-rata yang ditulis dari memori ke disk per detik, ambil nilai maksimum di antara semua partisi | KB/dtk | unInstanceId |
| Penggunaan disk | disk_usage | Persentase ruang disk yang digunakan, ditampilkan berdasarkan partisi | Persentase ruang disk yang digunakan, ditampilkan berdasarkan partisi | % | unInstanceId |
| Disk I/O tunggu| disk_io_await| Waktu tunggu rata-rata untuk setiap operasi I/O perangkat, ambil nilai maksimum di antara semua partisi | Waktu tunggu rata-rata untuk operasi I/O perangkat, ambil nilai maksimum di antara semua partisi | ms | unInstanceId |

Untuk informasi selengkapnya tentang metrik pemantauan, lihat [Dokumentasi Produk Cloud Monitor](https://intl.cloud.tencent.com/doc/product/248).

Cloud Monitor mengumpulkan data mentah disk dari instance CVM yang berjalan dan menampilkan data dalam diagram yang mudah dibaca.Statistik dapat disimpan selama satu bulan secara default sehingga Anda dapat mengamati situasi disk cloud selama bulan tersebut, dan memiliki pemahaman yang lebih baik tentang penggunaan dan membaca/menulis data.

Anda bisa mendapatkan data melalui [Konsol Cloud Monitor](https://console.cloud.tencent.com/monitor/cvm) atau API Cloud Monitor.Konsol juga menyediakan diagram yang divisualisasikan dari metrik yang sesuai.Untuk informasi selengkapnya, lihat [Mendapatkan Data Pemantauan Metrik Tertentu](https://intl.cloud.tencent.com/document/product/248/6141) dan [Melihat Diagram Pemantauan](https://intl.cloud.tencent.com/document/product/248/6142).