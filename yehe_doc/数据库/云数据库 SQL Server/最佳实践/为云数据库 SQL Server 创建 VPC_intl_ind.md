Tencent Cloud menyediakan [Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215/535), platform untuk menghosting instans TencentDB. Anda dapat meluncurkan sumber daya Tencent Cloud di VPC, seperti instans TencentDB.

Skema umum yang digunakan adalah berbagi data antara instans TencentDB dan server web yang berjalan di VPC yang sama. Dokumen ini menggunakan skema ini untuk membuat VPC dan menambahkan instans TencentDB ke dalamnya.
Dokumen ini menjelaskan cara menambahkan instans CVM dan TencentDB for SQL Server di VPC yang sama untuk interkoneksi antara sumber daya Tencent Cloud melalui jaringan pribadi di VPC.

## Langkah 1. Buat VPC
VPC memiliki setidaknya satu subnet, dan sumber daya layanan Tencent Cloud hanya dapat ditambahkan dalam subnet.
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih wilayah VPC di bagian atas daftar dan klik **+Create** (+Buat).
3. Masukkan informasi VPC dan informasi subnet awal lalu klik **Create** (Buat). CIDR dari VPC dan subnet tidak dapat diubah setelah dibuat.
 - CIDR VPC dapat berupa salah satu dari rentang IP berikut. Jika Anda ingin dua VPC berkomunikasi satu sama lain melalui jaringan pribadi, CIDR kedua VPC tersebut tidak boleh tumpang tindih:
    - `10.0.0.0` - `10.255.255.255` (rentang mask harus di antara 16 hingga 28)
    - `172.16.0.0` - `172.31.255.255` (rentang mask harus di antara 16 hingga 28)
    - `192.168.0.0` - `192.168.255.255` (rentang mask harus di antara 16 hingga 28)
 - CIDR subnet harus berada di dalam atau sama dengan CIDR VPC.
 Misalnya, jika rentang IP VPC adalah `192.168.0.0/16`, maka rentang IP subnet di dalamnya bisa jadi `192.168.0.0/16` atau `192.168.0.0/17`, misalnya.  


## Langkah 2. Buat subnet
Anda dapat membuat satu atau lebih subnet secara bersamaan.
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Subnet** (Subnet) di bilah sisi kiri untuk masuk ke halaman pengelolaan.
3. Pilih wilayah dan VPC dari subnet yang akan dibuat dan klik **+Create** (+Buat).
4. Masukkan nama subnet, CIDR, zona ketersediaan, dan tabel rute terkait.

5. (Opsional) Klik **+New Line** (+Baris Baru) untuk membuat beberapa subnet sekaligus.
6. Klik **Create** (Buat).

## Langkah 3. Buat tabel rute dan kaitkan dengan subnet
Anda dapat membuat tabel rute kustom, mengedit kebijakan peruteannya, dan mengaitkannya dengan subnet tertentu. Tabel perutean yang terkait dengan subnet digunakan untuk menentukan rute keluar subnet tersebut.
1. Masuk ke Konsol VPC dan pilih **Route Tables** (Tabel Rute) di bilah sisi kiri.
2. Pilih wilayah dan VPC di bagian atas daftar lalu klik **+Create** (+Buat).
3. Pada kotak dialog yang muncul, masukkan nama, jaringan, dan kebijakan perutean baru, lalu klik **Create** (Buat). Kembali ke daftar tabel rute dan Anda dapat melihat tabel perutean yang dibuat.

4. Pilih **Subnet** (Subnet) di bilah sisi kiri di konsol, pilih subnet yang akan dikaitkan dengan tabel perutean, lalu klik ***Change Route Table** (Ubah Tabel Rute) di kolom **Operation** (Operasi) untuk mengaitkannya.

## Langkah 4. Tambahkan instans CVM
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Subnet** (Subnet) di bilah sisi kiri untuk masuk ke halaman pengelolaan.
3. Klik ikon "Tambahkan CVM" di baris subnet tempat CVM akan ditambahkan.

4. Selesaikan pembelian instans CVM seperti yang diminta di halaman. Untuk informasi selengkapnya, silakan lihat [Metode Pembelian](https://intl.cloud.tencent.com/document/product/213/506) di dokumentasi CVM.

## Langkah 5. Tambahkan instans TencentDB
1. Login ke [Konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver) dan klik **Create Instance** (Buat Instans) untuk masuk ke halaman pembelian. 
2. Di bagian **Network Type** (Jenis Jaringan) pada halaman pembelian, pilih **VPC** (VPC), pilih VPC yang dibuat sebelumnya dan subnet terkait, lalu tambahkan instans TencentDB yang baru dibeli ke VPC.



