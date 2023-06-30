## Skenario

Anda dapat mengubah IP pribadi instans CVM di VPC langsung di konsol atau dengan mengubah subnet instans CVM. Dokumen ini menjelaskan cara mengubah IP pribadi instans CVM di konsol VPC.
Untuk detail tentang mengubah subnet, lihat [Ubah Subnet Instans](http://intl.cloud.tencent.com/document/product/213/16565).

## Batas

- Memodifikasi IP primer dari ENI primer dapat menyebabkan CVM dimulai ulang.
- IP primer ENI sekunder tidak dapat diubah.

## Petunjuk

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pilih wilayah instans yang IP pribadinya yang ingin Anda ubah, dan klik ID/nama instans untuk masuk ke halaman detailnya.
3. Pada halaman detail instans, pilih tab [ENI] dan klik <img src = "https://main.qcloudimg.com/raw/57a0c76b72cd97bd80bf857cd30c867a.png" style = "margin: 0;"> untuk memperluas ENI primer.
4. Dalam daftar operasi ENI utama, klik **Modify Primary IP** (Modifikasi IP Primer).
5. Di jendela “Modify Primary IP” (Modifikasi IP Primer) yang muncul, masukkan IP baru lalu klik **OK** (OKE). Ini berlaku setelah instans dimulai ulang.
>! Anda hanya dapat memasukkan IP pribadi di CIDR subnet saat ini.
>

