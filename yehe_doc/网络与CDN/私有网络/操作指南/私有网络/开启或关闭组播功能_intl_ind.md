Dokumen ini menjelaskan cara mengaktifkan atau menonaktifkan multicast untuk VPC.

## Latar belakang
Broadcast dan multicast adalah mode komunikasi satu-ke-semuanya, yang dapat menghemat bisnis di bandwidth jaringan dan mengurangi beban jaringan melalui transmisi data efisien point-to-multipoint.
Dalam mode unicast, server yang memulai mengirimkan data ke N server secara terpisah. Jika multicast digunakan, server mengirimkan data yang sama ke N server hanya sekali, yang mengurangi konsumsi sumber informasi server serta sumber informasi bandwidth jaringan backbone.
>?
>- Fitur broadcast dan multicast saat ini dalam uji beta. Jika diperlukan, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category).
>- Saat ini wilayah yang mendukung multicast dan broadcast adalah: Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, Nanjing, Hong Kong (Tiongkok), Singapura, Seoul, Tokyo,  Bangkok, Toronto, Silicon Valley, Virginia, Frankfurt, dan Moscow.
>

- Multicast: Tencent Cloud mendukung multicast pada dimensi VPC.
- Broadcast: Tencent Cloud mendukung broadcast pada dimensi subnet.

## Ikhtisar
Multicast dan broadcast sebagian besar digunakan dalam industri keuangan dan game:
- Layanan broadcast atau data pasar industri keuangan. Misalnya, setelah mendapatkan harga saham dan data real-time lainnya, broker dapat mem-broadcast data saham ke banyak klien secara real time, yang secara efektif mengurangi beban jaringan.
- Untuk industri game, broadcast dan multicast terutama digunakan untuk menahan heartbeat di antara beberapa server.

## Petunjuk
### Mengaktifkan multicast
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Di daftar VPC, temukan VPC yang diinginkan, dan aktifkan **Multicast** (Multicast).
![]()


### Menonaktifkan multicast
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Di daftar VPC, temukan VPC yang diinginkan, dan nonaktifkan **Multicast** (Multicast).
![]()

## Referensi
Untuk petunjuk selengkapnya mengenai broadcast tingkat subnet, lihat [Mengaktifkan atau Menonaktifkan Broadcast](https://intl.cloud.tencent.com/document/product/215/31809).

