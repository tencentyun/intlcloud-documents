Dokumen ini menjelaskan cara memigrasikan instans dari jaringan klasik ke VPC dan mengonfigurasi solusi akses hibrida selama migrasi.

## Memigrasikan Satu Instans
Anda dapat dengan mudah memigrasikan instans dari jaringan klasik ke VPC. Lihat di bawah untuk detailnya.
<table >
<th>Jenis instans</th>
<th>Deskripsi</th>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/213/20278>CVM</a></td>
<td> <li>Instans akan dimulai ulang.<li>IP jaringan klasik akan langsung dikonversi menjadi IP VPC.</td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/236/31915>TencentDB for MySQL</a></td>
<td rowspan=5>Baik IP jaringan klasik maupun IP VPC tersedia selama jangka waktu tertentu. IP jaringan klasik asli tetap valid sebagai berikut: <ul><li>MySQL:  periode default: 24 jam (1 hari); periode maksimum: 168 jam (7 hari)<li>MariaDB:  valid selama 24 jam (1 jam)<li>TDSQL:  valid selama 24 jam (1 jam)<li>Redis:  opsi yang tersedia: rilis sekarang, rilis setelah 1 hari, rilis setelah 2 hari, rilis setelah 3 hari, dan rilis setelah 7 hari<li>MongoDB:  alamat IP asli akan segera menjadi tidak valid untuk versi 4.0 atau yang lebih baru. Versi lain mendukung opsi: rilis sekarang, rilis setelah 1 hari, rilis setelah 2 hari, rilis setelah 3 hari, dan rilis setelah 7 hari</td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/237/40160>TencentDB for MariaDB</a></td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/1042/33340>TDSQL for MySQL</a></td>
</tr>
<td><a href=https://intl.cloud.tencent.com/document/product/239/31944>TencentDB for Redis</a></td>
</tr>
<td><a href=https://intl.cloud.tencent.com/document/product/240/40126>TencentDB for MongoDB</a></td>
</tr>
</table>

>? Jika Anda ingin mempertahankan agar alamat IP sumber daya tidak berubah setelah beralih jaringan, coba buat VPC yang memiliki IP jaringan klasik. Jika upaya ini tidak memungkinkan, lihat solusi berikut:
>+ Buat layanan DNS pribadi dan selesaikan nama domainnya. Setelah memigrasikan sumber daya ke VPC, gunakan Tencent Cloud [DNS pribadi](https://intl.cloud.tencent.com/document/product/1097/40551).
>+ Gunakan IP publik. 
>

## Solusi Akses Hibrida Selama Migrasi
Akses hibrida berarti layanan yang dimigrasikan dapat mengakses jaringan klasik dan VPC. Tencent Cloud memberikan solusi akses hibrida berikut:
+ Aksesibilitas IP jaringan klasik dan IP VPC dari layanan TencentDB memastikan akses hibrida di tingkat instans TencentDB.
    ![]()
+ Akses Cloud Object Storage (COS) melalui nama domain menyediakan kemampuan akses hibrida.
+ Untuk menerapkan interkoneksi selama migrasi, gunakan bersama dengan:
  + Classiclink: memungkinkan CVM berbasis jaringan klasik untuk saling terhubung dengan sumber daya VPC seperti instans CVM, TencentDB, dan CLB.
  + Koneksi terminal:  memungkinkan instans dalam VPC berkomunikasi dengan sumber daya di jaringan klasik (kecuali CVM).
  ![]()
   >? 
   >+ Jika Anda ingin membuat koneksi terminal, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category). Fitur ini hanya mendukung akses CVM berbasis jaringan klasik. Sebaiknya migrasikan sumber daya Anda ke VPC.
   >+ Untuk mempelajari selengkapnya tentang solusi VPC dan Classiclink, lihat [Berkomunikasi dengan Jaringan Klasik](https://intl.cloud.tencent.com/document/product/215/35505). Untuk informasi selengkapnya tentang cara mengonfigurasi Classiclink, lihat [Classiclink](https://intl.cloud.tencent.com/document/product/215/41418).

