### Bagaimana Anda membangun komunikasi antara subnet VPC yang berbeda?
- Setiap VPC memiliki interkoneksi jaringan pribadi secara default, dan Anda dapat melihat rute default di tabel rute yang sesuai. Rute ini menunjukkan bahwa semua sumber daya di VPC ini dapat saling terhubung melalui jaringan pribadi.
- Subnet di VPC yang berbeda tidak dapat terhubung melalui jaringan pribadi dan dapat saling berkomunikasi hanya dengan menggunakan [Koneksi Peering](https://intl.cloud.tencent.com/document/product/553) atau [CCN](https://intl.cloud.tencent.com/document/product/1003).

### Dapatkah CVM yang berbeda di-deploy di zona ketersediaan yang berbeda di VPC yang sama?
Ya. VPC memiliki atribut wilayah (seperti Guangzhou, Beijing, atau Seoul), dan subnet di VPC memiliki atribut zona ketersediaan (seperti Zona 1 Guangzhou atau Zona 2 Guangzhou), sehingga subnet dalam VPC yang sama dapat digunakan di zona ketersediaan yang berbeda di wilayah yang sama. Atribut zona ketersediaan CVM mewarisi karakter subnetnya, dan CVM dibeli di bawah subnet di zona ketersediaan. Dengan demikian, CVM yang berbeda dapat digunakan di zona ketersediaan yang berbeda.

### Bagaimana Anda membangun komunikasi antara CVM dan database di zona ketersediaan yang berbeda?
- VPC yang sama: ada interkoneksi secara default. Jika tidak terhubung, Anda dapat memprioritaskan pemecahan masalah kebijakan firewall [grup keamanan](https://intl.cloud.tencent.com/document/product/215/38750) dan [ACL jaringan](https://intl.cloud.tencent.com/document/product/215/31850) .
- VPC yang berbeda: Anda dapat menggunakan [Peering Connection](https://intl.cloud.tencent.com/document/product/553) atau [CCN](https://intl.cloud.tencent.com/document/product/1003) untuk mengimplementasikan interkoneksi melalui jaringan pribadi antara dua VPC.

### Berapa banyak alamat IP pribadi yang dapat diberikan setiap VPC untuk instans layanan Tencent Cloud?
Setiap VPC dapat menyediakan hingga 65.533 alamat IP pribadi untuk instans layanan Tencent Cloud.

### Apa itu CIDR?
Classless Inter-Domain Routing (CIDR) mengimplementasikan pembagian jaringan secara keseluruhan menggunakan blok alamat ruang jaringan independen yang Anda tentukan bersama dengan IP dan mask. Ini menghilangkan konsep tradisional rentang dan subnetting tradisional kelas A, kelas B, dan kelas C serta mengalokasikan ruang alamat IP lebih efektif. Saat membuat VPC dan subnet, Anda perlu membuat rentang IP yang sesuai dalam bentuk blok CIDR. Misalnya, untuk membuat rentang IP `10.0.16.0 - 10.0.17.255`, maka:
Konversi `10.0.16.0 - 10.0.17.255` ke format biner `00001010.00000000.0001000.000000000 - 00001010.00000000.00010001.11111111`, dengan 23 bit pertama harus sama. Format blok CIDR setelah konversi adalah `10.0.16.0/23`.


### Mengapa saya tidak dapat menghapus VPC dan subnet setelah secara manual menghentikan instans TencentDB for Redis?
Jika hanya ada satu instans TencentDB for Redis di VPC, setelah instans dihentikan secara manual, instans tersebut akan dipindahkan ke keranjang sampah TencentDB. Saat ini, sumber daya Redis belum benar-benar dilepas, sehingga VPC tidak dapat segera dihapus. Anda dapat mengatasi masalah ini dengan cara berikut:
+ Di keranjang sampah TencentDB, **eliminate** (hilangkan) instans TencentDB for Redis, lalu hapus VPC dan subnet.
+ Tunggu hingga instans TencentDB for Redis kedaluwarsa secara otomatis di keranjang sampah TencentDB, lalu hapus VPC dan subnet.
Untuk informasi selengkapnya, lihat [Menghentikan Instans](https://intl.cloud.tencent.com/document/product/239/31937).


### Mengapa aplikasi untuk EIP gagal?
Jika kuota EIP terlampaui, aplikasi EIP akan gagal. Untuk informasi selengkapnya tentang cara melihat detail kuota, harap lihat [Batas kuota EIP](https://intl.cloud.tencent.com/document/product/213/5733).
