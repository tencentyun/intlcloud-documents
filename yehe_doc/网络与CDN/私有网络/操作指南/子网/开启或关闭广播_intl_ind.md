## Latar belakang
Multicast dan broadcast adalah mode komunikasi satu ke semuanya, yang dapat membantu perusahaan mengurangi konsumsi bandwidth jaringan dan beban jaringan melalui transmisi data efisien point-to-multipoint.
Dalam mode unicast, server yang memulai mengirimkan data ke N server secara terpisah. Jika multicast digunakan, server mengirimkan data yang sama ke N server hanya sekali, yang mengurangi konsumsi sumber informasi server serta sumber informasi bandwidth jaringan backbone.
- Multicast: Tencent Cloud mendukung multicast pada dimensi VPC.
- Broadcast: Tencent Cloud mendukung broadcast pada dimensi subnet.

>?
>- Fitur broadcast dan multicast saat ini dalam uji beta. Jika diperlukan, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category).
>- Saat ini wilayah yang mendukung multicast dan broadcast adalah: Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, Nanjing, Hong Kong (Tiongkok), Singapura, Seoul, Tokyo,  Bangkok, Toronto, Silicon Valley, Virginia, Frankfurt, dan Moscow.
>

## Ikhtisar
Multicast dan broadcast sebagian besar digunakan dalam industri keuangan dan game:
- Layanan broadcast atau data pasar industri keuangan. Misalnya, setelah mendapatkan harga saham dan data real-time lainnya, broker dapat mem-broadcast data saham ke banyak klien secara real time, yang secara efektif mengurangi beban jaringan.
- Untuk industri game, broadcast dan multicast terutama digunakan untuk menahan heartbeat di antara beberapa server.

Dokumen ini menjelaskan cara mengaktifkan atau menonaktifkan broadcast untuk subnet.

## Petunjuk
### Mengaktifkan broadcast 
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Subnet** (Subnet) di bilah sisi kiri untuk mengakses halaman admin.
3. Dalam daftar VPC, cari VPC target, dan alihkan tombol ke **Enable** (Aktifkan) di bawah kolom **Subnet broadcast** (Broadcast subnet).
![]()

### Menonaktifkan broadcast
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Subnet** (Subnet) di bilah sisi kiri untuk mengakses halaman admin.
3. Dalam daftar VPC, cari VPC target, dan alihkan tombol ke **Disable** (Nonaktifkan) di bawah kolom **Subnet broadcast** (Broadcast subnet).
![]()

## Referensi
Untuk informasi selengkapnya mengenai multicast tingkat VPC, lihat [Mengaktifkan atau Menonaktifkan Multicast](https://intl.cloud.tencent.com/document/product/215/40072).

