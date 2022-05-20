Anda sekarang dapat menerapkan node master dan replika TencentDB for Redis di zona ketersediaan (AZ) yang berbeda di wilayah yang sama. Instans yang di-deploy multi-AZ memiliki ketersediaan yang lebih tinggi dan kemampuan pemulihan bencana yang lebih baik daripada instans yang di-deploy dengan AZ tunggal.
- Instans yang di-deploy AZ tunggal: Pemulihan bencana tingkat host dan rak
- Instans yang di-deploy Multi-AZ: Pemulihan bencana level host, rak, dan AZ

## Arsitektur Deployment
![](https://main.qcloudimg.com/raw/855cfa6d9f004b589c708eeb12de1518.png)
Deskripsi:
- LB (Load Balancer): Instans TencentDB for Redis dalam arsitektur standar atau arsitektur kluster memiliki setidaknya tiga proksi yang perlu diakses melalui LB.
- VIP: Instans yang di-deploy multi-AZ hanya memiliki satu VIP. Anda dapat menggunakan VIP ini untuk mengakses semua node instans yang di-deploy di wilayah tersebut. Peralihan Replika Master instans tidak akan mengubah VIP-nya.
- Proksi: Sebuah instans memiliki setidaknya tiga proksi. Untuk instans arsitektur standar, jumlah proksi = 3 + (jumlah replika -1); untuk instans arsitektur kluster, jumlah proksi = jumlah pecahan * jumlah replika.
- Master (Grup): "Master" adalah node master dari instans TencentDB for Redis dalam arsitektur standar; "Grup Master" adalah node master dari semua pecahan instans TencentDB for Redis dalam arsitektur kluster.
- Replika (Grup): “Replika" adalah node replika dari instans TencentDB for Redis dalam arsitektur standar; "Grup Replika" adalah kumpulan node replika, yang masing-masing berasal dari pecahan berbeda dari instans TencentDB for Redis dalam arsitektur kluster. Untuk instans arsitektur kluster, replika pecahan dibagi menjadi beberapa Grup Replika sehingga Grup Replika ini dapat di-deploy di AZ yang berbeda.
- AZ Master: AZ Master adalah AZ tempat node master berada. Kecuali jika diubah secara manual di konsol, AZ master akan tetap sama. Jika node master gagal, mungkin untuk sementara dialihkan ke replika AZ, dan akan secara otomatis dialihkan kembali ke AZ master dalam beberapa menit setelah kondisi tertentu terpenuhi. Proses pengalihan kembali ini tidak akan memengaruhi bisnis Anda, kecuali bisnis Anda menggunakan perintah blokir, seperti `blpop` atau `blpush`.

## Failover (HA)
- Deteksi node yang gagal: TencentDB for Redis dalam arsitektur standar atau arsitektur kluster mengadopsi mekanisme manajemen kluster yang sama dengan Kluster Redis, yang menggunakan protokol Gossip untuk mendeteksi status node dalam sebuah kluster. Parameter `cluster-node-timeout` digunakan untuk menentukan jumlah waktu maksimum node kluster Redis dapat tidak tersedia, tanpa dianggap gagal. Kami sarankan Anda mengatur parameter ini ke nilai default (15 d) dan jangan mengubahnya. Untuk informasi selengkapnya, lihat [tutorial kluster Redis](https://redis.io/topics/cluster-tutorial).
- Mempromosikan replika ke master: TencentDB for Redis mengadopsi mekanisme failover yang berbeda dari Kluster Redis, yang memberikan prioritas untuk mempromosikan replika di AZ master untuk mengurangi penundaan akses AZ master. Langkah-langkah detailnya adalah sebagai berikut:
 - Promosikan replika jika memiliki data terbaru
 - Promosikan replika di AZ master jika semua replika memiliki data yang sama

## Akses Lintas-AZ
### Instans tanpa replika baca saja
Pemisahan Baca/Tulis dinonaktifkan (yaitu, replika dapat ditulis dan dibaca dari): Permintaan tulis/baca di AZ replika dirutekan oleh proksi ke node master, dan node master disinkronkan dengan node replika untuk memastikan data yang konsisten di semua node. Dalam proses ini, hanya satu akses lintas-AZ yang terjadi.

### Instans dengan replika baca saja
Pemisahan Baca/Tulis diaktifkan (yaitu, replika hanya dapat dibaca dari): Permintaan tulis dirutekan oleh proksi ke node master, tetapi permintaan baca dirutekan ke node replika di AZ yang sama dengan proksi, sehingga permintaan baca dapat ditanggapi oleh node terdekat.
>?Ada penundaan 2–5 mdtk selama akses lintas-AZ.

## Solusi Deployment yang Disarankan
### Deployment dua AZ
Deploy node master dan satu node replika di AZ master, dan dua node replika di AZ replika. Kedua AZ, yang masing-masing memiliki dua node, diakses melalui LB. Jika satu node di AZ gagal, permintaan baca dapat diproses oleh node lain di AZ. Jika AZ gagal, AZ lainnya masih sangat tersedia. Solusi ini berlaku untuk kasus penggunaan yang memiliki persyaratan tinggi pada ketersediaan dan penundaan.
![](https://main.qcloudimg.com/raw/5a3cc43871565e6371d1d990e9845324.png)

### Deployment tiga AZ
Deploy node master di AZ master, satu node replika di AZ replika 1, dan satu node replika di AZ replika 2. Jika satu node atau satu AZ gagal, seluruh arsitektur masih memiliki ketersediaan tinggi lintas-AZ. Solusi ini berlaku untuk kasus penggunaan yang memiliki persyaratan ketersediaan yang sangat tinggi tetapi tidak sensitif terhadap penundaan.
![](https://main.qcloudimg.com/raw/d2c4ad9ce6354559eaee7e191be59b7e.png)
 
## Operasi Terkait
- Untuk informasi selengkapnya tentang cara mengonfigurasi dan melihat deployment multi-AZ di konsol TencentDB for Redis, lihat [Mengonfigurasi Deployment Multi-AZ](https://intl.cloud.tencent.com/document/product/239/39799).
- Untuk informasi selengkapnya tentang cara meningkatkan deployment dari AZ tunggal ke multi-AZ di konsol TencentDB for Redis, lihat [Meningkatkan ke Deployment Multi-AZ](https://intl.cloud.tencent.com/document/product/239/39982).
- Untuk informasi selengkapnya tentang cara mengaktifkan dan menonaktifkan pemisahan baca/tulis di konsol TencentDB for Redis, lihat [Mengaktifkan/Menonaktifkan Pemisahan Baca/Tulis](https://intl.cloud.tencent.com/document/product/239/31935).
- Instans TencentDB for Redis yang di-deploy AZ tunggal dapat diakses oleh VIP. Jadi instans dapat di-deploy multi-AZ. Untuk informasi selengkapnya, lihat [Mengakses Instans yang Di-deploy Multi-AZ:](https://intl.cloud.tencent.com/document/product/239/41053).
- TencentDB for Redis mendukung auto-failover untuk memastikan ketersediaan layanan database yang tinggi. Untuk informasi selengkapnya, lihat [Failover](https://intl.cloud.tencent.com/document/product/239/41052).
- Instans TencentDB for Redis yang di-deploy Multi-AZ mendukung auto-failback. Untuk informasi selengkapnya, lihat [Auto-Failback](https://intl.cloud.tencent.com/document/product/239/41051).
- Untuk instans TencentDB for Redis yang di-deploy multi-AZ, Anda dapat secara manual mempromosikan node replika (grup) di AZ tertentu ke node master (grup) dan AZ akan secara otomatis dipromosikan ke AZ master. Untuk informasi selengkapnya, lihat [Mempromosikan Secara Manual ke Node Master (Grup)](https://intl.cloud.tencent.com/document/product/239/41050).
- Untuk mengurangi latensi dalam mengakses instans TencentDB for Redis yang di-deploy multi-AZ, Anda hanya dapat membaca node lokal. Untuk informasi selengkapnya, lihat [Membaca Node Lokal Saja](https://intl.cloud.tencent.com/document/product/239/41049).

