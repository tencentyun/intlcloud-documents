

### Disk cloud elastis

Disk cloud elastis memiliki siklus pemakaian (siklus penagihan) yang terpisah dan dapat dipasang dan dilepas di antara berbagai instance CVM di wilayah dan zona ketersediaan yang sama.Namun, disk ini tidak dapat dipasang secara bersamaan di beberapa CVM.



### Disk cloud non-elastis

Disk cloud non-elastis dibuat bersamaan dengan Cloud Virtual Machine (CVM) dan memiliki siklus pemakaian yang sama dengan CVM tersebut.Disk ini tidak mendukung pemasangan elastis.



### GPT

Silakan lihat [GPT](https://www.tencentcloud.com/pt/document/product/362/18555#gpt2).



### Pengembalian

Pengembalian mampu memulihkan program atau data ke status benar terakhir ketika terjadi kesalahan pemrosesan.Terdapat dua jenis rollback, yaitu rollback program dan rollback data.



### IOPS

Input/Output Per Second (Input Output Per Detik/IOPS) mengacu pada jumlah baca (output) dan tulis(inputs) dalam satu detik.Ini adalah metrik penting untuk mengukur kinerja disk.IOPS menunjukkan jumlah permintaan I/O yang dapat diproses sistem dalam satuan waktu (per detik).Permintaan I/O umumnya adalah permintaan baca atau tulis.
Disk tradisional pada dasarnya adalah perangkat mekanis, seperti disk FC, SAS, dan SATA, yang biasanya memiliki kecepatan putaran sebesar 5.400/7.200/10.000/15.000 rpm.Faktor utama yang memengaruhi disk adalah waktu layanan disk, yaitu waktu yang dibutuhkan disk untuk menyelesaikan permintaan I/O.Waktu ini terdiri atas waktu pencarian, jeda rotasional, dan waktu transfer data.
Umumnya, HDD dengan kecepatan rotasi 7.200 rpm mampu menyediakan 75-150 IOPS, dan HDD dengan kecepatan rotasi 15.000 rpm mampu menyediakan 175-210 IOPS.Nilai aktualnya bergantung pada faktor-faktor seperti mode akses (berurutan atau acak) dan ukuran I/O.



### Rantai snapshot

Rantai snapshot adalah rantai hubungan yang terdiri atas semua snapshot dari disk yang sama, dan setiap simpul mewakili satu snapshot dari disk tersebut.



### MBR

Lihat [MBR](https://www.tencentcloud.com/document/product/362/18555#mbr2)



### GPT

GUID Partition Table (Tabel Partisi GUID/GPT) adalah tata letak partisi suatu disk fisik.GPT merupakan bagian dari standar Extensible Firmware Interface (Antarmuka Firmware yang Dapat Diperluas/EFI) dan merupakan pengganti untuk tabel partisi MBR yang digunakan oleh sebagian besar disk.

### Snapshot lengkap

Snapshot lengkap adalah snapshot pertama yang dibuat untuk sebuah disk yang menyimpan semua data disk tersebut.



### I/O berurutan

I/O berurutan berarti blok logis dibaca dan ditulis secara berurutan dari alamat yang berdekatan.Dalam akses I/O berurutan, waktu pencarian suatu disk jauh lebih singkat karena kepala baca-tulisnya hampir tidak perlu bergerak ketika mengakses blok berikutnya.Layanan seperti pencadangan data dan pencatatan merupakan I/O berurutan.

### I/O acak

I/O acak berarti alamat akses tidak tersusun secara berurutan, tetapi tersebar secara acak di berbagai bagian disk.Layanan seperti OLTP, SQL, dan instant messaging (pesan singkat) merupakan I/O acak.



### Striping

Striping adalah metode untuk menyeimbangkan beban I/O secara otomatis di beberapa disk fisik.

### Throughput

Throughput adalah jumlah data yang berhasil ditransfer dalam satuan waktu tertentu dalam suatu jaringan, perangkat, port, sirkuit virtual, atau perangkat lainnya.



### Snapshot disk cloud

Snapshot digunakan untuk menyimpan salinan disk cloud pada titik waktu tertentu.Anda dapat menggunakannya untuk memulihkan disk cloud ke titik waktu ketika snapshot tersebut dibuat.



### Snapshot tambahan

Snapshot tambahan adalah cadangan titik waktu tertentu yang hanya terdiri dari setiap perubahan sejak snapshot lengkap atau snapshot tambahan yang sebelumnya.

### MBR

Master Boot Record (MBR) adalah sektor pertama yang harus dibaca komputer ketika mengakses disk setelah startup.MBR mencatat informasi tentang disk, serta ukuran dan lokasi setiap partisi disk.MBR juga merupakan entri penting untuk informasi data.
