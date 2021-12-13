## Ikhtisar
Dokumen ini menjelaskan cara mengubah subnet instans CVM di VPC melalui konsol.

## Batas

- CVM terkait dimulai ulang secara otomatis setelah subnetnya diubah.
- Subnet ENI sekunder tidak dapat diubah.

## Petunjuk

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Di **Instances** (Instans), pilih wilayah tempat instans yang subnetnya perlu diubah berada.
3. Temukan instans yang subnetnya perlu diubah, klik ID/Namanya dan masuk ke halaman detail instans.
4. Pilih tab **ENI** (ENI), klik ID ENI primer, 
dan masuk ke halaman manajemen ENI, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/feeec3ecd76a2f5710d1b775b9f7f1d9.png)
5. Klik **Change Subnet** (Ubah Subnet), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/713d6383b128a66ae25f5342a7387631.jpg)
6. Pilih subnet baru di kotak pop-up. Masukkan IP baru, lalu klik **OK** (OKE), seperti yang ditunjukkan di bawah ini:
Konfigurasi akan berlaku setelah instans dimulai ulang.
>! 
> - Buat subnet jika tidak ada subnet yang dapat ditemukan di zona ketersediaan ini.
> - Hanya alamat IP pribadi dari CIDR subnet saat ini yang dapat digunakan sebagai IP baru.
>
![](https://main.qcloudimg.com/raw/58c3534b2d6c9da255c5a32bbde8a4c1.png)
