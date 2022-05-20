

## Alat Pengujian
Uji performa dalam dokumen ini dilakukan dengan beban tolok ukur TPC-C yang dibangun di HammerDB. TPC-C adalah beban kerja OLTP tipikal yang mensimulasikan skenario di mana pedagang grosir dengan banyak gudang mengirimkan barang ke sejumlah besar pelanggan. Penyesuaian jumlah gudang dapat mencerminkan ukuran data yang dapat dipertahankan database dalam pengujian.
- [Alamat unduhan HammerDB](https://www.hammerdb.com/download.html)
- [Panduan Pengguna HammerDB](https://www.hammerdb.com/document.html)
- [Ikhtisar beban pengujian TPC-C yang dibangun di HammerDB](https://www.hammerdb.com/docs/ch03.html)

## Lingkungan dan Parameter Pengujian
### Edisi instans pengujian 
Instans pengujian adalah 2008 R2 Enterprise Edition, 2012 Enterprise Edition, 2014 Enterprise Edition, 2016 Enterprise Edition, 2017 Enterprise Edition, dan 2019 Enterprise Edition.

### Spesifikasi instans pengujian 
##### Edisi ketersediaan tinggi
Contoh pengujian edisi ketersediaan tinggi mencakup semua spesifikasi yang dapat dibeli, termasuk 1-core 2 GB, 1-core 4 GB, 1-core 8 GB, 2-core 16 GB, 4-core 32 GB, 8-core 64 GB, 12 -core 96 GB, 16-core 128 GB, 24-core 192 GB, 32-core 256 GB, 48-core 384 GB, 64-core 512 GB, dan 90-core 720 GB.

#### Edisi dasar
Instans pengujian edisi dasar mencakup semua spesifikasi yang dapat dibeli, termasuk 1-core 2 GB, 1-core 4 GB, 2-core 4 GB, 2-core 8 GB, 4-core 8 GB, dan 4-core 16 GB.

### Lingkungan pembuatan beban
Mesin tempat HammerDB diinstal memiliki model yang sama dengan instans database, sehingga memastikan bahwa kinerja instans SQL Server dapat diukur sepenuhnya dalam pengujian ketahanan.

### Parameter tolok ukur TPC-C
- Jumlah Gudang = 100: mengatur jumlah gudang menjadi 100.
- Menit Waktu Peningkatan = 2: mengatur waktu pemanasan sebelum pengujian menjadi 2 menit.
- Menit Durasi Pengujian = 5: mengatur durasi pengujian menjadi 5 menit.

### Jumlah pengguna virtual
Jumlah pengguna virtual adalah jumlah koneksi bersamaan. Dalam dokumen ini, jumlah koneksi bersamaan yang berbeda diuji pada instans edisi berbeda dengan spesifikasi berbeda.

##### Edisi ketersediaan tinggi
| Koneksi Bersamaan | 2        | 4        | 8        | 16       | 32       | 64       | 128      | 256      | 512      | 1,024     |
| ---------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| 1-core 2 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -   | -    |
| 1-core 4 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -   | -    |
| 1-core 8 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -   | -    |
| 2-core 16 GB   | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -        |
| 4-core 32 GB   | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -        |
| 8-core 64 GB   | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -        |
| 12-core 96 GB   | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 16-core 128 GB  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 24-core 192 GB  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 32-core 256 GB  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 48-core 384 GB  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 64-core 512 GB  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 90-core 720 GB  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

#### Edisi dasar
| Koneksi Bersamaan | 2        | 4        | 8        | 16       | 32       | 64       | 128      | 256      | 512      | 1,024 |
| ---------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | ---- |
| 1-core 2 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -        | -    |
| 1-core 4 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -        | -    |
| 2-core 4 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -    |
| 2-core 8 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -    |
| 4-core 8 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -    |
| 4-core 16 GB    | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -    |

## Metode Pengujian
 ## Metode Pengujian
1. Siapkan beban kerja TPC-C.
 - Jumlah Gudang: jumlah gudang, yang akan memengaruhi ukuran database pengujian yang dihasilkan.
 - Pengguna Virtual untuk Membangun Skema: jumlah koneksi bersamaan saat menghasilkan data beban, yang tidak boleh lebih besar dari jumlah gudang. Nilai ini memengaruhi efisiensi pembangkitan data beban, sehingga disarankan untuk sama dengan jumlah inti CPU dari perangkat pembangkit beban.
![](https://main.qcloudimg.com/raw/976f094fdf0e32dcfb5537bc6cf2cf0b.png)
2. Atur skrip pengujian.
 - Total Transaksi per Pengguna: jumlah total transaksi per pengguna. Anda disarankan untuk mengatur parameter ini ke nilai yang lebih tinggi untuk memastikan bahwa pengguna tidak akan keluar karena penyelesaian transaksi selama pengujian ketahanan.
 - Menit Waktu Peningkatan: waktu pemanasan untuk pengujian ketahanan.
 - Menit Durasi Pengujian: durasi pengujian ketahanan.
![](https://main.qcloudimg.com/raw/c0225b4272891c94f58ffb6645ca0da1.png)
3. Atur skrip pengujian otomatis.
 - Menit per Pengujian dalam Urutan Pengguna Virtual: interval antara dua sesi pengujian otomatis selama program menyelesaikan berbagai tugas seperti membuat pengguna virtual, melakukan pemanasan, menjalankan pengujian, dan menghentikan pengujian. Nilai ini harus lebih besar dari jumlah "Menit Waktu Peningkatan" dan "Menit Durasi Pengujian".
 - Urutan Pengguna Virtual Aktif (Dipisahkan Spasi): jumlah pengguna virtual yang dihasilkan oleh setiap iterasi pengujian otomatis. Jumlah ini dapat dipahami sebagai jumlah koneksi bersamaan.
![](https://main.qcloudimg.com/raw/c6657ad27fb862ab2d758d5e06c4dfb6.png)
4. Pilih **Autopilot** (Autopilot) > **Autopilot** (Autopilot) di panel kiri untuk memulai pengujian.
![](https://main.qcloudimg.com/raw/786137e8672adac87b224a7bfc783f51.png)
5. Hasil pengujian akan ditampilkan dalam file hammerdb.log.
![](https://main.qcloudimg.com/raw/89d6adf0bf52b416fda5a387ff48ea49.png)

## Hasil Pengujian
>?
>- TPM di HammerDB diperoleh melalui penghitung kinerja SQL Server "permintaan batch/detik", jadi TPM sebenarnya mengacu pada permintaan batch per menit.
>- Ukuran kumpulan data pengujian untuk spesifikasi instans lebih besar dari ukuran memori spesifikasi.

#### Edisi ketersediaan tinggi (SSD lokal)
#### Perbandingan kinerja berbagai edisi ketersediaan tinggi (SSD lokal)
![](https://qcloudimg.tencent-cloud.cn/raw/2811a30c30849a8eb6d0a0d3e39e4e5b.png)

#### Perbandingan TPM dari berbagai edisi ketersediaan tinggi (SSD lokal)
| Spesifikasi Instans Edisi Ketersediaan Tinggi | Koneksi Bersamaan | 2008 R2 Enterprise Edition | 2012 Enterprise Edition | 2014 Enterprise Edition | 2016 Enterprise Edition | 2017 Enterprise Edition | 2019 Enterprise Edition |
| ------------------ | ---------- | --------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 1-core 2 GB       | 256        | 279.798          | 229.854        | 261.396        | 219.142        | 201.851        | 181.198        |
| 1-core 4 GB       | 256        | 284.680          | 234.401        | 288.282        | 222.796        | 202.510        | 268.330        |
| 1-core 8 GB       | 256        | 269.039          | 236.773        | 303.002        | 219.676        | 208.685        | 300.385        |
| 2-core 16 GB     | 256        | 368.366          | 333.797        | 446.344        | 336.843        | 331.650        | 390.546        |
| 4-core 32 GB     | 256        | 657.641          | 608.801        | 621.186        | 665.065        | 625.370        | 670.666        |
| 8-core 64 GB     | 256        | 1.164.062         | 1.020.500       | 924.915        | 1.070.826       | 1.102.296       | 1.007.612       |
| 12-core 96 GB   | 1.024       | 1.348.121         | 1.266.868       | 1.153.585       | 1.337.473       | 1.325.010       | 1.367.211       |
| 16-core 128 GB  | 1.024       | 1.357.678         | 1.385.158       | 1.260.322       | 1.705.660       | 1.716.818       | 1.629.583       |
| 24-core 192 GB  | 1.024       | 1.226.621         | 1.500.900       | 1.406.203       | 2.261.815       | 1.950.871       | 2.198.697       |
| 32-core 256 GB  | 1.024       | 1.401.600         | 1.526.762       | 1.462.100       | 2.280.252       | 2.520.856       | 2.771.797       |
| 48-core 384 GB    | 1.024       | 2.127.159         | 1.486.582       | 1.637.912       | 2.806.496       | 2.683.302       | 3.358.182       |
| 64-core 512 GB    | 1.024       | 2.136.500         | 1.512.763       | 1.789.105       | 2.630.581       | 2.814.599       | 3.635.133       |
| 90-core 720 GB    | 1.024       | 2.205.323         | 1.602.736       | 1.813.094       | 2.948.427       | 3.391.680       | 4.579.980       |

### Edisi dasar (disk cloud premium)
#### Perbandingan kinerja berbagai edisi dasar (disk cloud premium)
![](https://qcloudimg.tencent-cloud.cn/raw/dab7533cd878b8bc2f976e96cf04d0b8.png)

#### Perbandingan TPM dari berbagai edisi dasar (disk cloud premium)
| Spesifikasi Instans Edisi Dasar | Koneksi Bersamaan | 2008 R2 Enterprise Edition | 2012 Enterprise Edition | 2014 Enterprise Edition | 2016 Enterprise Edition | 2017 Enterprise Edition | 2019 Enterprise Edition |
| ---------------- | ---------- | --------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 1-core 2 GB     | 256        | 271.822          | 201.348        | 239.864        | 155.318        | 180.204        | 181.062        |
| 1-core 4 GB     | 256        | 271.311          | 224.851        | 263.445        | 206.871        | 218.065        | 226.523        |
| 2-core 4 GB     | 256        | 300.573          | 286.984        | 349.251        | 301.520        | 282.145        | 280.967        |
| 2-core 8 GB     | 256        | 343.630          | 312.184        | 379.705        | 315.539        | 304.840        | 331.574        |
| 4-core 8 GB     | 256        | 569.589          | 557.047        | 567.886        | 464.900        | 457.702        | 507.047        |
| 4-core 16 GB   | 256        | 578.367          | 560.981        | 602.897        | 504.379        | 537.819        | 592.712        |



