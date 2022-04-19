## Hubungan antara snapshot dan disk cloud sumber
Snapshot adalah pencadangan data dari disk cloud pada titik waktu tertentu.Penulisan dan modifikasi data ke disk cloud tidak memengaruhi snapshot yang sudah dibuat.Berdasarkan fitur ini, pengguna dapat menggunakan snapshot untuk merekam data disk cloud pada titik waktu yang berbeda, yang dapat digunakan untuk memenuhi persyaratan pemulihan sistem, pemulihan bencana, dan replikasi disk cloud.
Seperti yang ditunjukkan pada gambar berikut, Snapshot 1 menyimpan informasi blok data disk cloud pada 10:00 (waktu pembuatan snapshot), terlepas dari perubahan apa pun pada disk yang terjadi setelah snapshot dibuat.
![](https://main.qcloudimg.com/raw/1f7e576a6ea9e4f85273b0b147108c9b.png)

## Hubungan antara ukuran snapshot dan disk cloud sumber
Snapshot hanya menyimpan blok data di disk cloud yang telah ditulis atau dimodifikasi.Oleh karena itu, ukuran snapshot yang terkait dengan disk cloud akan lebih kecil dari ukuran disk cloud.
Hubungan antara ukuran snapshot dan disk data ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/00913478170abba28952aa9c8dc13c82.png)

## Proses pembuatan snapshot tambahan
Snapshot Tencent Cloud menggunakan mekanisme snapshot tambahan.Saat Anda terus membuat beberapa snapshot dari disk cloud yang sama, hanya snapshot pertama yang merupakan snapshot penuh, dan snapshot berikutnya hanya berisi data yang telah dimodifikasi tergantung pada snapshot sebelumnya (snapshot tambahan).Ini dapat meminimalkan total kapasitas penyimpanan yang digunakan saat pengguna terus membuat snapshot sehingga mengurangi biaya pengguna.
Misalnya:Asumsikan bahwa disk cloud memiliki tiga blok data, A, B, dan C. Anda membuat snapshot masing-masing pada pukul 10:00, 11:00, dan 12:00.Perubahan blok data pada disk antara titik waktu ini ditunjukkan pada gambar berikut, dan setiap snapshot harus menyimpan data berikut:
- Snapshot 1 (snapshot awal):Berisi cadangan data dari semua blok data pada disk cloud pada saat itu.
- Snapshot 2:Selama periode tersebut, blok data A pada disk cloud berubah.Snapshot 2 hanya berisi cadangan data terbaru blok A (biasanya disebut snapshot tambahan).
- Snapshot 3:Selama periode tersebut, blok data B pada disk cloud berubah.Snapshot 3 hanya berisi cadangan data terbaru blok B (biasanya disebut snapshot tambahan).

![](https://main.qcloudimg.com/raw/bcdf30c658a08ef47196f8127608423b.png)

## Proses pengembalian snapshot tambahan
Berdasarkan contoh sebelumnya, saat Anda menggunakan Snapshot 3 untuk melakukan pengembalian data, sistem akan menggabungkan data di Snapshot 1, Snapshot 2, dan Snapshot 3.Jika ada blok data di lokasi yang sama, data di snapshot terbaru akan diambil.Selama pengembalian terakhir, data yang digabungkan akan ditulis ke disk cloud untuk dikembalikan.
Proses pengembalian snapshot tambahan adalah seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/745e412b2dfa84ea6ba5e8e0fc720fc8.png)

## Proses penghapusan dan penggabungan snapshot tambahan
- Saat menghapus snapshot penuh (yaitu, snapshot pertama), sistem secara otomatis menggabungkan snapshot penuh dengan snapshot tambahan berikutnya.
- Saat menghapus snapshot tambahan, sistem secara otomatis menggabungkan snapshot tambahan dengan snapshot tambahan berikutnya.Jika tidak ada snapshot tambahan berikutnya, snapshot tersebut langsung dihapus.

Berdasarkan contoh sebelumnya, jika Anda menghapus Snapshot 1, sistem akan menggabungkan Snapshot 1 dan Snapshot 2, dan akan menggunakan data Snapshot 2 untuk menimpa data Snapshot 1 di lokasi yang sama.Setelah digabungkan, Snapshot 2 adalah snapshot penuh yang baru.
Proses penghapusan snapshot tambahan adalah seperti yang ditunjukkan pada gambar berikut:
![](https://qcloudimg.tencent-cloud.cn/raw/2f2bb2449450a52df265537da14768b5.png)
