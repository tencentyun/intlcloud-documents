VPC adalah jaringan virtual yang terisolasi secara logis yang dapat Anda gunakan secara eksklusif dan direncanakan secara mandiri di Tencent Cloud. Untuk menggunakan sumber informasi Tencent Cloud, Anda harus membuat VPC dan subnet. Subnet adalah ruang jaringan di VPC. Anda setidaknya dapat membagi VPC menjadi satu subnet. VPC bersifat regional, sedangkan subnet dikhususkan untuk zona ketersediaan. Subnet di VPC yang sama dapat berkomunikasi satu sama lain melalui jaringan pribadi secara default.

Semua sumber informasi cloud seperti CVM dan CLB dalam VPC harus di-deploy di subnet.


## Siklus Pemakaian VPC
Siklus pemakaian VPC berbeda-beda sesuai dengan kebutuhan, seperti yang ditampilkan di bawah ini:
![](https://main.qcloudimg.com/raw/68556cee99a7ececc3936b45cdaa3ca5.svg)
1. [Membuat VPC](https://intl.cloud.tencent.com/document/product/215/31805): Anda harus berhati-hati [merencanakan jaringan Anda](https://intl.cloud.tencent.com/document/product/215/31795) sebelum membuat VPC. Blok CIDR dari VPC dan subnet tidak dapat diubah setelah dibuat.
2. [Melihat VPC](https://intl.cloud.tencent.com/document/product/215/40069): Anda dapat melihat informasi dasar VPC, hubungan CCN-nya, dan sumber informasi yang dikandungnya.
3. (Opsional) Pilih operasi yang berlaku untuk kasus penggunaan Anda:
 - Jika blok CIDR utama tidak mencukupi, lihat [Mengedit Blok CIDR IPv4](https://intl.cloud.tencent.com/document/product/215/40070):
    - [Membuat blok CIDR sekunder](https://intl.cloud.tencent.com/document/product/215/40070#21): Anda dapat membuat blok CIDR sekunder untuk memenuhi permintaan jaringan Anda secara aktual.
    - [Menghapus blok CIDR sekunder](https://intl.cloud.tencent.com/document/product/215/40070#32): Anda dapat menghapus blok CIDR sekunder jika Anda tidak lagi membutuhkannya.
4. [Menghapus VPC](https://intl.cloud.tencent.com/document/product/215/40073): setelah VPC dihapus, subnet dan tabel rutenya juga dihapus.

