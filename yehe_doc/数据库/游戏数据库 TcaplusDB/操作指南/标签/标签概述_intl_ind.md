## Ikhtisar
Tag adalah pasangan nilai kunci yang disediakan oleh Tencent Cloud untuk mengidentifikasi sumber daya di cloud. Untuk informasi selengkapnya, lihat [Ikhtisar Tag](https://intl.cloud.tencent.com/document/product/651/13334).

Anda dapat mengelola sumber daya TcaplusDB dengan cara yang dikategorikan dengan menggunakan tag dalam berbagai dimensi seperti bisnis, tujuan, dan penanggung jawab, sehingga lebih mudah untuk menemukan sumber daya yang tepat. Tag tidak memiliki arti semantik untuk Tencent Cloud dan diurai dan dicocokkan secara ketat berdasarkan string. Selama penggunaan, Anda hanya perlu memperhatikan [batas penggunaan](https://intl.cloud.tencent.com/document/product/651/13354) yang berlaku.

Di bawah ini adalah kasus penggunaan khusus untuk menunjukkan cara menggunakan tag.

## Latar Belakang Kasus Penggunaan
Sebuah perusahaan memiliki tiga kluster TcaplusDB di Tencent Cloud, yang didistribusikan di tiga bisnis game yang pemilik OPSnya masing-masing adalah John, Jane, dan Harry.

## Mengatur Tag
Untuk memfasilitasi manajemen, perusahaan mengkategorikan sumber daya TcaplusDB dengan tag dan menentukan pasangan nilai kunci tag berikut:

| Kunci Tag | Nilai Tag |
| :---------- | ---------------------------------- |
| Bisnis | Game 1, Game 2, dan Game 3 |
| Pemilik OPS | John, Jane, dan Harry |

Tag ini terikat ke sumber daya TcaplusDB dengan cara berikut:

| ID Sumber Daya		| Bisnis	| Pemilik OPS |
|---------------------|----|--------------|
| tcaplus-abcdef1	| Game 1	| Harry |
| tcaplus-abcdef2	| Game 2 | Jane |
| tcaplus-abcdef3	| Game 3	| John |

## Menggunakan Tag
- Untuk informasi selengkapnya tentang cara membuat dan menghapus tag, silakan lihat [Memulai Tag](https://intl.cloud.tencent.com/document/product/651/32582).
- Untuk informasi selengkapnya tentang cara mengedit tag di TcaplusDB, silakan lihat [Mengedit Tag](https://intl.cloud.tencent.com/document/product/1016/36551).
