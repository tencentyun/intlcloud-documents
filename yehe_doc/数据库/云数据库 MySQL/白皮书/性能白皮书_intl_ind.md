## Alat Pengujian
Sysbench 0.5 adalah alat yang digunakan untuk menguji performa pengukuran database.

Konfigurasi alat:
Skrip OTLP yang disertakan dengan Sysbench telah dimodifikasi. Secara khusus, rasio baca/tulis diubah menjadi 1:1 dan dikontrol oleh parameter perintah pengujian `oltp_point_selects` dan `oltp_index_updates`. Dalam dokumen ini, semua kasus uji melibatkan empat operasi SELECT dan satu operasi UPDATE dengan rasio baca/tulis pada 4:1.

#### Penginstalan alat
Jalankan kode berikut untuk menginstal Sysbench 0.5:
```
git clone https://github.com/akopytov/sysbench.git
git checkout 0.5
yum -y install make automake libtool pkgconfig libaio-devel
yum -y install mariadb-devel
./autogen.sh
./configure
make -j
make install
```
>?Petunjuk penginstalan di atas berlaku untuk pengujian tekanan performa pada instans CentOS CVM. Untuk petunjuk tentang menginstal alat pada sistem operasi lain, harap lihat [dokumentasi resmi Sysbench](https://github.com/akopytov/sysbench?spm=a2c4g.11186623.2.12.36061072oZL2qS).

## Lingkungan Pengujian

| Jenis | Deskripsi |
|--|--|
| Mesin fisik | Satu mesin dapat mendukung instans database dua node dengan memori hingga 488 GB dan disk 6 TB |
| Spesifikasi instans | Spesifikasi yang umum tersedia (harap lihat [kasus pengujian](#cscs) di bawah) |
| Konfigurasi klien | CPU 4-core dan memori 8 GB |
| Jumlah klien | 1-6 (lebih banyak klien perlu ditambahkan saat konfigurasi ditingkatkan) |
| Lingkungan jaringan | Pusat data dengan koneksi 10-Gigabit dan latensi jaringan di bawah 0,05 md |
| Beban lingkungan | Beban pada mesin tempat MySQL diinstal di atas 70% (untuk instans non-eksklusif) |

- Catatan tentang spesifikasi klien: mesin klien dengan spesifikasi tinggi digunakan untuk memastikan bahwa performa instans database dapat diukur melalui pengujian tekanan pada satu klien. Untuk klien dengan spesifikasi rendah, disarankan untuk menggunakan beberapa klien untuk pengujian tekanan secara bersamaan dan menggabungkan hasilnya.
- Catatan tentang latensi jaringan: di lingkungan pengujian, harus dipastikan bahwa klien dan instans database berada di zona ketersediaan yang sama untuk mencegah hasil pengujian terpengaruh oleh faktor jaringan.

## Metode Pengujian
### 1. Struktur tabel database pengujian
```
CREATE TABLE `sbtest1` ( 
`id` int(10) unsigned NOT NULL AUTO_INCREMENT, 
`k` int(10) unsigned NOT NULL DEFAULT '0', 
`c` char(120) NOT NULL DEFAULT '', 
`pad` char(60) NOT NULL DEFAULT '',
 PRIMARY KEY (`id`), KEY `k_1` (`k`) 
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

### 2. Format baris data pengujian
```
id: 1
k: 20106885
C: 08566691963-88624912351-16662227201-46648573979-64646226163-77505759394-75470094713-41097360717-15161106334-50535565977
pad: 63188288836-92351140030-06390587585-66802097351-4928296184
```

### 3. Persiapan data
```
sysbench --mysql-host=xxxx --mysql-port=xxxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --mysql-table-engine=innodb --test=tests/db/oltp.lua --oltp_tables_count=20 --oltp-table-size=10000000  --rand-init=on prepare
```

Deskripsi parameter persiapan data:
- `--test=tests/db/oltp.lua` menunjukkan cara mengimplementasikan pengujian OLTP dengan memanggil skrip `tests/db/oltp.lua`.
- `--oltp_tables_count=20` menunjukkan bahwa jumlah tabel untuk pengujian adalah 20.
- `--oltp-table-size=10000000` menunjukkan bahwa setiap tabel pengujian diisi dengan 10 juta baris data.
- `--rand-init=on` menunjukkan bahwa setiap tabel pengujian diisi dengan data acak.
  

### 4. Perintah untuk pengujian tekanan
```
sysbench --mysql-host=xxxx --mysql-port=xxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua --oltp_tables_count=xx --oltp-table-size=xxxx --num-threads=xxx --oltp-read-only=off --rand-type=special --max-time=600 --max-requests=0 --percentile=99 --oltp-point-selects=4 run
```

Deskripsi parameter pengujian tekanan:
- `--test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua` menunjukkan cara mengimplementasikan pengujian OLTP dengan memanggil skrip `/root/sysbench_for_z3/sysbench/tests/db/oltp.lua`.
- `--oltp_tables_count=20` menunjukkan bahwa jumlah tabel untuk pengujian adalah 20.
- `--oltp-table-size=10000000` menunjukkan bahwa setiap tabel pengujian diisi dengan 10 juta baris data.
- `--num-threads=128` menunjukkan bahwa koneksi konkuren klien untuk pengujian adalah 128.
- `--oltp-read-only=off` menunjukkan bahwa model pengujian baca saja dinonaktifkan dan model baca/tulis hibrida digunakan.
- `--rand-type=special` menunjukkan bahwa model acak bersifat spesifik.
- `--max-time=1800` menunjukkan waktu eksekusi pengujian ini.
- `--max-requests=0` menunjukkan bahwa tidak ada batasan yang dikenakan pada jumlah total permintaan dan pengujian dijalankan sesuai dengan `max-time`.
- `--percentile=99` menunjukkan tingkat pengambilan sampel. Di sini, 99 berarti membuang 1% permintaan panjang dari semua permintaan dan mengambil nilai maksimum di antara 99% permintaan yang tersisa. Nilai default adalah 95%.
- `--oltp-point-selects=4` menunjukkan bahwa jumlah operasi SELECT dalam perintah pengujian SQL dalam skrip OLTP adalah 4. Nilai defaultnya adalah 1.

### 5. Model skenario
Semua kasus pengujian dalam dokumen ini mengadopsi skrip `lua` dari Sysbench yang dimodifikasi untuk menjalankan empat operasi SELECT dan satu operasi UPDATE (kolom indeks) dengan rasio baca/tulis pada 4:1.
Untuk konfigurasi maksimum, model penyetelan parameter ditambahkan ke skenario data. Untuk hasil pengujian, harap lihat [Hasil Pengujian](#document_test_result) di bawah.


<span id="cscs"></span>
## Parameter Pengujian

| Spesifikasi Instans | Kapasitas Penyimpanan | Jumlah Tabel | Jumlah Baris | Ukuran Kumpulan Data | KKonkurensi | Waktu Eksekusi (Menit) |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1-core, 1 GB|200 GB|4|20 juta |19 GB|128|30|
|1-core, 2 GB|200 GB|4|40 juta |38 GB|128|30|
|2-core, 4 GB|200 GB|8|40 juta|76 GB|128|30|
|4-core, 8 GB|200 GB|15|40 juta |142 GB|128|30|
|4-core, 16 GB|400 GB|25|40 juta|238 GB|128|30|
|8-core, 32 GB|700 GB|25|40 juta|238 GB|128|30|
|16-core, 64GB|1 TB|40|40 juta|378 GB|256|30|
|16-core, 96 GB|1,5 TB|40|40 juta|378 GB|128|30|
|16-core, 128 GB|2 TB|40|40 juta|378 GB|128|30|
|24-core, 244 GB|3 TB|60|40 juta|567 GB|128|30|
|48-core, 488 GB|6 TB|60|40 juta|567 GB|128|30|
|48-core, 488 GB (disesuaikan)|6 TB|60|10 juta|140 GB|128|30|

<span id="document_test_result"></span>
## Hasil pengujian

| Spesifikasi Instans | Kapasitas Penyimpanan | Kumpulan Data | Jumlah Klien | Konkurensi klien tunggal | QPS | TPS |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1-core, 1 GB|200 GB|19 GB|1|128|1,757|97|
|1-core, 2 GB|200 GB|38 GB|1|128|3,016|167|
|2-core, 4 GB|200 GB|76 GB|1|128|4.082|816|
|4-core, 8 GB|200 GB|142 GB|1|128|6.551|1.310|
|4-core, 16 GB|400 GB|238 GB|1|128|11.098|2.219|
|8-core, 32 GB|700 GB|238 GB|2|128|20.484|3.768|
|16-core, 64 GB|1 TB|378 GB|2|128|36.395|7.279|
|16-core, 96 GB|1,5 TB|378 GB|3|128|56.464|11.292|
|16-core, 128 GB|2 TB|378 GB|3|128|81.752|16.350|
|24-core, 244 GB|3 TB|567 GB|4|128|98.528|19.705|
|48-core, 488 GB|6 TB|567 GB|6|128|142.246|28.449|
|48-core, 488 GB (disesuaikan) |6 TB|140 GB|6|128|245.509|46.304|
