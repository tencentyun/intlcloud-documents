Ketika VPC tidak lagi digunakan dan tidak memiliki sumber daya lain (Peering Connection, ClassicLink, NAT Gateway, VPN Gateway, Direct Connect Gateway, CCN, dan koneksi pribadi) kecuali subnet kosong, tabel perutean, dan ACL jaringan, VPC dapat dihapus.
>?Subnet kosong mengacu pada subnet yang tidak menggunakan IP apa pun; yaitu, ketika hanya ada subnet kosong, tabel perutean, dan ACL jaringan di VPC, VPC dapat dihapus; ketika ada penggunaan IP di subnet, VPC tidak dapat dihapus.
>

## Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih wilayah VPC di bagian atas halaman **VPC** (VPC).
3. Dalam daftar VPC, temukan VPC yang akan dihapus, klik **Delete** (Hapus) di bawah kolom **Operation** (Operasi), lalu konfirmasi penghapusan.
![](https://qcloudimg.tencent-cloud.cn/raw/ac7203b074651d3a7bab148496094054.png)
