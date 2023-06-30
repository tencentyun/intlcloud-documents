[Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/product/eni?from_cn_redirect=1) adalah antarmuka elastis untuk akses jaringan yang mengikat server Cloud Virtual Machine (CVM) pada Virtual Private Cloud (VPC) untuk migrasi yang lancar antara beberapa server CVM. Beberapa ENI dapat diikat ke satu server CVM untuk membuat jaringan yang sangat tersedia. 

ENI adalah bagian dari subnet, yang merupakan bagian dari VPC, yang pada gilirannya merupakan bagian dari zona ketersediaan. ENI hanya dapat dikaitkan dengan instans CVM di zona ketersediaan yang sama. Beberapa ENI dapat dikaitkan dengan instans CVM yang sama. Jumlah spesifik bergantung pada spesifikasi CVM.

## Konsep

 - **ENI primer dan ENI sekunder**: saat Anda membuat instans CVM, ENI otomatis dibuat dalam proses. Itulah ENI primer. Setiap ENI berikutnya yang Anda buat adalah ENI sekunder. Anda tidak dapat mengikat atau melepaskan ikatan ENI primer. ENI sekunder mendukung pengikatan dan pelepasan.
 - :**IP pribadi primer:** IP pribadi primer dari ENI ditetapkan oleh sistem atau ditentukan oleh pengguna saat ENI dibuat. Anda dapat mengubah IP pribadi primer dari ENI primer, tetapi tidak untuk ENI sekunder.
  **IP pribadi sekunder:** selain IP pribadi primer, semua alamat IP yang terikat ke ENI adalah IP pribadi sekunder. Anda dapat mengikat/melepaskan IP ini.
 - **EIP**: EIP dipetakan satu-ke-satu ke IP pribadi ENI.
 - **Grup keamanan**: ENI dapat dikaitkan dengan satu atau beberapa grup keamanan.
 - **Alamat MAC**: setiap ENI memiliki alamat MAC yang unik secara global.

## Kasus Penggunaan
- **Isolasi antara jaringan pribadi, jaringan publik, dan jaringan manajemen**:
Bisnis penting sering kali memerlukan kebijakan perutean dan grup keamanan yang berbeda untuk jaringan pribadi, jaringan publik, dan manajemen untuk memastikan keamanan data dan isolasi jaringan. Anda dapat menggunakan CVM untuk mencapai tingkat isolasi yang sama dengan server fisik yang berbeda. Cukup tetapkan ENI yang berbeda ke subnet yang berbeda.
**Deployment aplikasi yang sangat andal:**
Komponen sistem penting memerlukan beberapa cadangan panas untuk memastikan ketersediaan tinggi. Pengikatan dan pelepasan ENI dan IP pribadi yang fleksibel adalah dasar dari arsitektur ketersediaan tinggi Tencent Cloud. Gunakan Keepalive untuk mengimplementasikan fitur ini.

## Batasan Penggunaan

Jumlah ENI yang dapat dikaitkan dengan instans CVM dan jumlah IP pribadi yang dapat dikaitkan dengan ENI bergantung pada konfigurasi CPU dan memori. Jumlah tersebut ditunjukkan dalam tabel berikut:
> Jumlah alamat IP yang terikat pada satu ENI hanya mewakili batas atas alamat IP yang dapat diikat oleh ENI, bukan kuota EIP yang tersedia. Untuk kuota EIP akun Anda, lihat EIP [batasan penggunaan](https://intl.cloud.tencent.com/document/product/213/5733).

| Spesifikasi CVM | Jumlah ENI | Jumlah IP pribadi |
| ------------------- | :---- | :------ |
| CPU: 1 core </br>Memori: 1 GB | 2 | 2 |
| CPU: 1 core </br>Memori: > 1 GB | 2 | 6 |
| CPU: 2 core | 2 | 10 |
| CPU: 4 core </br>Memori: < 16 GB | 4 | 10 |
| CPU: 4 core </br>Memori: > 16 GB | 4 | 20 |
| CPU: 8 - 12 core | 6 | 20 |
| CPU: > 12 core | 8 | 30 |


## Ikhtisar API
Berikut adalah daftar API yang terkait dengan ENI dan CVM. Untuk informasi selengkapnya, lihat [Ikhtisar API ENI](https://intl.cloud.tencent.com/document/product/215/15755?from_cn_redirect=1#.E5.BC.B9.E6.80.A7.E7.BD.91.E5.8D.A1.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3).

| Fitur | ID Tindakan | Deskripsi |
|---------|---------|---------|
| Buat ENI | [CreateNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15818?from_cn_redirect=1) | Membuat ENI |
| Terapkan untuk IP pribadi | [AssignPrivateIpAddresses](https://intl.cloud.tencent.com/document/api/215/15813?from_cn_redirect=1) | Berlaku untuk IP pribadi untuk ENI |
| Ikat ENI ke instans CVM | [AttachNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15819?from_cn_redirect=1) | Mengikat ENI ke instans CVM |
