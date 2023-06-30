### Berapa kapasitas default disk sistem CVM?

Disk sistem CVM baru memiliki ruang kosong sebesar 50 GB secara default.

### Bisakah saya mengubah disk sistem lokal CVM menjadi disk cloud?

- Saat membeli instans CVM,
Anda bisa memilih jenis disk yang diinginkan untuk disk sistem CVM.
- Untuk instans CVM yang dibeli,
jika zona ketersediaan tempat pembelian CVM memiliki disk cloud yang tersedia, Anda bisa menggunakan fitur [ubah jenis media disk](https://intl.cloud.tencent.com/document/product/213/32365) untuk mengubah disk sistem lokal menjadi disk cloud.

### Wilayah dan zona ketersediaan mana yang mendukung penambahan kapasitas disk sistem hingga lebih dari 50 GB?

Jika disk sistem merupakan disk cloud, kapasitas disk sistem dapat disesuaikan hingga lebih dari 50 GB di semua wilayah yang mendukung snapshot.

### Bisakah saya menambah kapasitas disk sistem CVM saat menginstal ulang sistem operasi?

Tergantung jenis disk sistem.
**If the system disk is a cloud disk** (Jika disk sistem adalah disk cloud),
  kapasitas disk sistem bisa ditambah tetapi tidak dapat dikurangi.
**If the system disk is a local disk** (Jika disk sistem adalah disk lokal),
  tergantung ukuran disk sistem.
  - Jika kapasitas disk sistem default pada instans yang dibeli adalah 50 GB, disk sistem tidak dapat ditambah.
  - Untuk instans yang dibeli sebelumnya: jika kapasitas disk sistem adalah 20 GB atau lebih kecil, disk sistem bisa ditambah hingga 20 GB secara default. Jika kapasitas disk sistem lebih dari 20 GB, disk sistem bisa ditambah hingga 50 GB secara default.

### Bisakah saya menambah kapasitas disk sistem lalu menginstal ulang sistem operasi untuk mengurangi kapasitas disk sistem?

Kapasitas disk sistem tidak bisa dikurangi.

### Bagaimana cara menyimpan data di instans CVM lalu menambah kapasitas disk sistem?

Untuk menambah kapasitas disk sistem, Anda bisa membuat citra lalu menggunakan citra tersebut untuk menginstal ulang sistem operasi.

### Berapa kapasitas disk sistem jika saya menggunakan citra kurang dari 50 GB untuk membuat atau menginstal ulang CVM?

Kapasitas citra tidak memengaruhi kapasitas disk sistem. Kapasitas disk sistem minimum adalah 50 GB.
