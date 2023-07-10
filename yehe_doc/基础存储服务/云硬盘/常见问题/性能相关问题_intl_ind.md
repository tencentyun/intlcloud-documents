### Bagaimana cara mengukur kinerja disk cloud?
Metrik berikut umumnya digunakan untuk menggambarkan kinerja perangkat penyimpanan:
- IOPS: Jumlah baca/tulis per detik. IOPS bervariasi menurut jenis drive yang mendasari perangkat penyimpanan.
- Throughput: Volume data yang dibaca/ditulis per detik, satuan dalam MB/dtk.
- Latensi: Waktu yang dibutuhkan untuk mengirim operasi I/O sampai menerima konfirmasi (dalam detik).

### Bagaimana cara menguji kinerja disk?
Sebaiknya gunakan FIO untuk melakukan uji tekanan dan verifikasi pada disk cloud. Untuk informasi selengkapnya, lihat [Mengukur performa disk cloud](https://intl.cloud.tencent.com/document/product/362/6741).

### Apakah ukuran I/O baca-tulis aplikasi memengaruhi kinerja IOPS?
Ya. Untuk sumber daya tertentu, IOPS yang Anda dapatkan ditentukan oleh ukuran I/O dari operasi baca dan tulis aplikasi. Biasanya, saat membaca dan menulis blok kecil (misalnya, ukuran I/O 256 KB), kinerja IOPS disk dapat digunakan sepenuhnya.

### Apakah ukuran I/O aplikasi baca-tulis memengaruhi kinerja throughput?
Ya. Untuk sumber daya tertentu, throughput yang Anda dapatkan ditentukan oleh ukuran I/O dari operasi baca dan tulis aplikasi. Biasanya, saat membaca dan menulis blok besar (misalnya, ukuran I/O 1MB), kinerja throughput disk dapat digunakan sepenuhnya.

### Dapatkah beberapa disk digabungkan secara logis menjadi satu disk untuk mendapatkan kinerja yang lebih baik?
Ya. Anda dapat menggabungkan beberapa disk cloud yang dipasang ke CVM untuk menyeimbangkan beban I/O ke beberapa disk, meningkatkan kapasitas paralel I/O untuk menerapkan kinerja yang lebih baik daripada satu disk. Untuk informasi selengkapnya, lihat [Membuat volume logis LVM dari beberapa disk cloud elastis](https://intl.cloud.tencent.com/document/product/362/2933).

