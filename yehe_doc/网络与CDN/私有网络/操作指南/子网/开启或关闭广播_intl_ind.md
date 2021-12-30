## Latar belakang
Multicast dan broadcast adalah mode komunikasi satu-ke-semuanya, yang dapat membantu perusahaan mengurangi konsumsi bandwidth jaringan dan beban jaringan melalui transmisi data efisien point-to-multipoint.
Jika unicast digunakan, server pengirim perlu mengirim secara terpisah ke N server untuk total N kali. Jika multicast digunakan, server mengirimkan data yang sama ke N server hanya sekali, yang mengurangi konsumsi sumber informasi server dan juga sumber informasi bandwidth jaringan backbone.
- Multicast: Tencent Cloud mendukung multicast pada dimensi VPC.
- Broadcast: Tencent Cloud mendukung broadcast pada dimensi subnet.

>?
>- Fitur broadcast dan multicast saat ini dalam fase beta. Untuk menjadi pengguna beta, kirimkan permohonan untuk broadcast atau multicast.
>- Saat ini, fitur broadcast dan multicast tersedia di Beijing, Shanghai, Guangzhou, Nanjing, Chengdu, Chongqing, dan Hong Kong, Tiongkok.
>

## Ikhtisar
Multicast dan broadcast sebagian besar digunakan dalam industri keuangan dan game:
- Layanan broadcast atau data pasar industri keuangan. Misalnya, setelah mendapatkan harga saham dan data real-time lainnya, pialang dapat mem-broadcast data saham ke banyak klien secara real time, yang secara efektif mengurangi beban jaringan.
- Untuk industri game, broadcast dan multicast terutama digunakan untuk menahan heartbeat di antara beberapa server.

Dokumen ini menjelaskan cara mengaktifkan atau menonaktifkan broadcast untuk subnet.

## Petunjuk
### Mengaktifkan broadcast
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Subnet** (Subnet) di bilah sisi kiri untuk mengakses halaman pengelolaan.
3. Di daftar VPC, temukan VPC yang broadcast-nya ingin Anda aktifkan, dan geser ke **Enable** (Aktifkan) di bawah kolom **Subnet broadcast** (Broadcast subnet).

### Menonaktifkan broadcast
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Subnet** (Subnet) di bilah sisi kiri untuk mengakses halaman pengelolaan.
3. Di daftar VPC, temukan VPC yang broadcast-nya ingin Anda nonaktifkan, dan geser ke **Disable** (Nonaktifkan) di bawah kolom **Subnet broadcast** (Broadcast subnet).

## Operasi yang Relevan
Untuk petunjuk detail mengenai multicast VPC, lihat [Mengaktifkan atau Menonaktifkan Multicast](https://intl.cloud.tencent.com/document/product/215/40072).

