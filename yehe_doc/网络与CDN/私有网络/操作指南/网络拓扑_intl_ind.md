Peta topologi jaringan menampilkan semua sumber informasi VPC, sehingga Anda dapat memperoleh deployment dan koneksi VPC secara real time.

## Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Klik **Network Topology Map** (Peta Topologi Jaringan) di bilah sisi kiri.
    ![](https://main.qcloudimg.com/raw/c7e8ecf743767784df696cf149413d75.png)
3. Pilih wilayah dan VPC untuk melihat sumber informasi cloud VPC seperti CVM, CLB, TencentDB, dan NoSQL, dan relasi topologi jaringannya.
  Dalam dua subnet sampel VPC seperti yang ditampilkan di bawah ini, subnet `test6` berisi dua instans CLB. VPC ini berkomunikasi dengan Internet melalui NAT Gateway dan CLB jaringan publik. Ini berkomunikasi dengan VPC yang berlawanan melalui peering connection.
    ![](https://main.qcloudimg.com/raw/1cc6ff3a212bc7ef26b261ba8610cba5.png)
