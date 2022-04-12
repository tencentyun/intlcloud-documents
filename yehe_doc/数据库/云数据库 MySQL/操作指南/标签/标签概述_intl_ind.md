### Ikhtisar

**tag** (tag) adalah pasangan nilai kunci yang disediakan oleh Tencent Cloud untuk mengidentifikasi sumber daya di cloud. Untuk informasi selengkapnya, lihat [Ikhtisar Tag](http://intl.cloud.tencent.com/document/product/651/13334).
Anda dapat mengelola sumber daya TencentDB for MySQL dengan cara yang dikategorikan dengan menggunakan berbagai jenis tag, seperti bisnis, tujuan, dan penanggung jawab, sehingga memudahkan untuk menemukan sumber daya yang tepat. Tag tidak memiliki arti semantik untuk Tencent Cloud dan diurai dan dicocokkan secara ketat berdasarkan string. Bersama kami, Anda hanya perlu memperhatikan [batas penggunaan](http://intl.cloud.tencent.com/document/product/651/13354) yang berlaku.
Di bawah ini adalah kasus penggunaan khusus untuk menunjukkan bagaimana tag digunakan.

### Latar Belakang Kasus
Sebuah perusahaan memiliki 10 instans TencentDB for MySQL di Tencent Cloud. Didistribusikan di tiga departemen (ecommerce, game, dan hiburan), instans ini digunakan untuk melayani lini bisnis internal seperti pemasaran, game A, game B, dan pascaproduksi. Pemilik OPS dari ketiga departemen tersebut masing-masing adalah John, Jane, dan Harry.

### Mengatur Tag
Untuk memfasilitasi manajemen, perusahaan mengategorikan sumber daya TencentDB for MySQL dengan tag dan menentukan pasangan nilai kunci tag berikut.

| Kunci Tag     | Nilai Tag                             |
| :---------- | ---------------------------------- |
| Departmen       | Ecommerce, game, dan hiburan                   |
| Bisnis       | Pemasaran, game A, game B, dan pascaproduksi |
| pemilik OPS | John, Jane, dan Harry                   |

Kunci/nilai tag ini terikat ke instans TencentDB for MySQL dengan cara berikut:

|instance-id	|Departemen |Bisnis |Pemilik OPS|
|----------------|-------|----|--------------|
|cdb-abcdef1	|Ecommerce	|Marketing	|Harry|
|cdb-abcdef2	|Ecommerce	|Marketing	|Harry|
|cdb-abcdef3|Gaming|Game A|John|
|cdb-abcdef3|Gaming|Game B|John|
|cdb-abcdef4|Gaming|Game B|John|
|cdb-abcdef5|Gaming|Game B|Jane|
|cdb-abcdef6|Gaming|Game B|Jane|
|cdb-abcdef7|Gaming|Game B|Jane|
|cdb-abcdef8	|Entertainment	|Post-production|	Harry|
|cdb-abcdef9	|Entertainment	|Post-production|	Harry|
|cdb-abcdef10|	Entertainment	|Post-production|	Harry|

### Menggunakan Tag
Untuk informasi selengkapnya tentang cara membuat dan menghapus tag, lihat [Panduan Pengoperasian](https://intl.cloud.tencent.com/document/product/651/41684).

Untuk informasi selengkapnya tentang cara mengedit tag di TencentDB for MySQL, lihat [Mengedit Tag](https://intl.cloud.tencent.com/document/product/236/31918).

