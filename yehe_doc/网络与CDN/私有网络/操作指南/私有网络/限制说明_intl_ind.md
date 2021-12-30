### Batasan penggunaan
- Rentang IP VPC dan subnet tidak dapat diubah setelah dibuat.
- Untuk setiap subnet, Tencent Cloud mencadangkan dua IP pertama dan yang terakhir untuk jaringan IP. Misalnya, jika [blok CIDR subnet](https://intl.cloud.tencent.com/document/product/215/4925) adalah `172.16.0.0/24`, maka `172.16.0.0`, `172.16.0.1`, dan `172.16.0.255` dicadangkan oleh Tencent Cloud.
- Saat Anda menambahkan CVM ke VPC, instans akan ditetapkan secara acak dengan IP pribadi dari subnet yang ditentukan. Anda dapat menetapkan ulang IP pribadi setelah instans dibuat.
- Di VPC, IP pribadi CVM sesuai dengan satu alamat IP publik.
- CVM berbasis jaringan klasik tidak dapat terhubung dengan sumber informasi cloud di blok CIDR sekunder.
- Peering connection tidak mendukung blok CIDR sekunder.
- Cloud Connect Network, VPN gateway, dan standard direct connect gateway mendukung blok CIDR sekunder.

### Batasan kuota
| Sumber Informasi | Batas |
|---------|---------|
| Jumlah instans VPC per wilayah per akun | 20 | 
| Jumlah subnet per VPC | 100 | 
| Jumlah blok CIDR sekunder per VPC | 5 |

>?Jika Anda ingin meningkatkan kuota, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1) untuk mendaftar.
