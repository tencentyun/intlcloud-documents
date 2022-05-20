<div class="tab_list">
<ul>
    <li><a href="#A-E">A-E</a></li>
    <li><a href="#F-J">F-J</a></li>
    <li><a href="#K-O">K-O</a></li>
    <li><a href="#P-T">P-T</a></li>
    
</ul>
</div>

<span id="A-E"></span>
## A-E 

### Pencadangan Otomatis
Ini mengacu pada cadangan penuh dari instans database yang dibuat secara otomatis oleh sistem. Anda dapat mengonfigurasi periode waktu mulai dan periode penyimpanan cadangan otomatis.

### Periode Penyimpanan Cadangan
Ini mengacu pada periode penyimpanan cadangan otomatis. Cadangan yang melebihi periode penyimpanan akan dihapus secara otomatis.

### Penyimpanan Cadangan
Ini digunakan untuk menyimpan data database, log, atau sumber daya penyimpanan dasar cadangan lainnya secara terus-menerus.

### Admin Database
Admin Database (DBA) adalah orang yang bertanggung jawab untuk mengelola database menggunakan penyimpanan perangkat lunak khusus dan organisasi data. Tanggung jawab peran ini termasuk namun tidak terbatas pada perencanaan kapasitas, penginstalan, konfigurasi, desain database, migrasi, pemantauan performa, keamanan, pemecahan masalah, serta pencadangan dan pemulihan.

### Instans Database
Instans database adalah lingkungan database mandiri yang berjalan di cloud, yang dapat berisi beberapa database yang dibuat oleh pengguna database dan dapat diakses menggunakan alat dan aplikasi klien yang sama dengan yang digunakan untuk instans database mandiri.

### Siklus Hidup Instans Database
Siklus hidup instans database dimulai dari saat instans dibuat hingga rilis finalnya, selama siklus hidup tersebut, operasi seperti pencadangan, pemulihan, perubahan spesifikasi, perluasan kapasitas, mulai ulang, dan penghapusan dapat dilakukan pada database.

### Migrasi Database
Seiring perubahan bisnis, database juga perlu dimigrasikan dari satu lingkungan ke lingkungan lain bersama dengan bisnis aplikasi, seperti dari IDC lokal ke cloud atau dari satu cloud ke cloud yang lain.

### Replikasi Data
Dalam arsitektur ketersediaan tinggi master/slave, setelah data dikirimkan ke instans master, data tersebut disalin ke instans slave, dan proses ini disebut replikasi data, yang biasanya dapat dibagi menjadi replikasi sinkronisasi yang canggih, replikasi semisinkron, dan replikasi asinkron.

### Akun Pengguna Database
Akun pengguna database berbeda dari akun Tencent Cloud Anda dan hanya digunakan dalam lingkungan instans TencentDB yang ditentukan untuk mengontrol akses ke instans database Anda. Akun pengguna master database adalah akun pengguna database lokal yang dapat digunakan untuk terhubung ke instans database. Setelah instans database dibuat, Anda dapat terhubung ke database menggunakan akun pengguna database. Anda juga dapat membuat akun pengguna database tambahan untuk memenuhi kebutuhan akun Anda yang sebenarnya.

<span id="F-J"></span>
## F-J 

### Failover
Ketika gangguan tidak biasa terjadi pada instans database, sistem akan secara otomatis beralih ke instans slave sehingga dapat memulihkan operasi database secepat mungkin tanpa intervensi administratif. Waktu yang diperlukan untuk menyelesaikan failover bergantung pada aktivitas database dan kondisi lain saat instans database master menjadi tidak tersedia, yang umumnya berkisar dari hitungan detik hingga menit.

### Ketersediaan Tinggi
Ketersediaan Tinggi adalah kemampuan sistem untuk berfungsi dengan baik tanpa gangguan. Ini adalah tingkat ketersediaan sistem.

### Pencadangan Hot
Ini adalah metode pencadangan ketika sistem berjalan normal. Dalam hal ini, data dalam sistem diperbarui secara real time, dan kelambatan dapat terjadi antara data cadangan dan data sistem yang sebenarnya.

### ID Instans
Setiap instans database memiliki ID instans database. ID yang diberikan dapat secara unik mengidentifikasi instans database saat Anda berinteraksi dengan konsol dan API. ID instans database harus unik di tingkat wilayah.

### Spesifikasi Instans
Daya komputasi dan kapasitas memori dari instans database ditentukan oleh spesifikasi instans database. Anda dapat mengubah CPU dan memori yang tersedia untuk instans database dengan cara memodifikasi spesifikasinya.

### IOPS
Metrik operasi input/output per detik (IOPS) dilaporkan sebagai IOPS rata-rata selama periode waktu tertentu. Total IOPS adalah jumlah IOPS baca dan IOPS tulis. Nilai tipikal IOPS berkisar dari nol hingga puluhan ribu.


<span id="K-O"></span>
## K-O 

### Pencadangan Manual
Ini adalah pencadangan penuh dari instans database yang Anda lakukan, dan file cadangan akan disimpan hingga Anda menghapusnya secara manual.

### Instans Database Master
Ini adalah instans database yang menyediakan layanan baca dan tulis di antara node yang menyediakan layanan database.

### Lalu Lintas Jaringan
Ini mengacu pada throughput transfer jaringan, yang merupakan tingkat lalu lintas jaringan masuk dan keluar dari instans database per detik (dalam MB).

### Jumlah Koneksi Database
Ini mengacu pada jumlah sesi klien yang terhubung ke instans database.

## Metrik Performa
Metrik yang mencerminkan performa instans database, termasuk namun tidak terbatas pada penggunaan CPU, penggunaan memori, penggunaan penyimpanan, lalu lintas jaringan, jumlah koneksi database, tingkat transaksi/throughput database, latensi pengiriman, latensi penyimpanan, IOPS penyimpanan, throughput penyimpanan, dan kedalaman antrian penyimpanan.



<span id="P-T"></span>
## P-T 

### Database Relasional
Ini adalah database yang terhubung dan terorganisir berdasarkan struktur data relasional. Untuk model database relasional, struktur data yang kompleks disederhanakan menjadi relasi biner (tabel dua dimensi). Dalam database relasional, hampir semua operasi data dilakukan pada satu atau lebih tabel relasional. Anda dapat mengelola database dengan cara mengurutkan, menggabungkan, menghubungkan, atau memilih tabel terkait tersebut. Database relasional umum termasuk Oracle, MySQL, MariaDB, Microsoft SQL Server, Access, DB2, PostgreSQL, Informix, dan Sybase.



### Tingkat Transaksi/Throughput Database
Jumlah transaksi yang diselesaikan dalam jangka waktu tertentu biasanya dinyatakan dalam TPM (transaksi per menit) atau TPS (transaksi per detik). Istilah umum lainnya untuk tingkat transaksi adalah throughput database. Sebuah database memiliki tingkat transaksi yang tinggi; oleh karena itu, database memiliki throughput disk yang sangat rendah atau nol.

### Throughput/Throughput Disk
Ini mengacu pada jumlah byte yang masuk atau keluar dari disk per detik. Metrik ini dilaporkan sebagai throughput rata-rata selama periode waktu tertentu. Throughput baca dan throughput tulis dilaporkan sekali per menit dalam megabyte per detik (MB/detik). Nilai tipikal throughput berkisar dari nol hingga bandwidth maksimum saluran I/O.







