## Ikhtisar
Dokumen tersebut menggunakan CVM dengan CentOS 7.6 sebagai contoh untuk menjelaskan cara mengunggah dan mengunduh file melalui SCP.


## Prasyarat
Anda telah membeli CVM Linux.

## Petunjuk
### Mendapatkan IP publik
Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index), buka halaman **Instances** (Instans), dan catat IP publik CVM tempat Anda ingin mengunggah file, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/4ffafbd2f6ab65d55e56fe59b669363a.png)


### Mengunggah file
1. Jalankan perintah berikut untuk mengunggah file ke CVM Linux.
```
scp [alamat file lokal] [akun CVM]@[nama domain/IP publik instans CVM]:[lokasi file CVM]
```
Misalkan Anda ingin mengunggah file lokal `/home/lnmp0.4.tar.gz` ke CVM (IP: 129.20.0.2) berdasarkan direktori yang sama, perintahnya harus sebagai berikut:
```
scp /home/Inmp0.4.tar.gz root@129.20.0.2:/home/Inmp0.4.tar.gz
```
2. Masukkan **yes** (ya) dan tekan **Enter** (Enter) untuk mengonfirmasi unggahan dan masukkan kata sandi login untuk menyelesaikan unggahan.
 - Jika Anda menggunakan kata sandi default sistem untuk login ke instans, buka [Pusat Pesan](https://console.cloud.tencent.com/message) untuk mendapatkan kata sandi terlebih dahulu.
 - Jika lupa kata sandi, Anda dapat [mengatur ulang kata sandi instans](https://intl.cloud.tencent.com/document/product/213/16566).

### Mengunduh file
1. Jalankan perintah berikut untuk mengunduh file dari CVM Linux.
```
Nama domain/IP publik instans scp CVM account@CVM: Lokasi file CVM alamat file lokal 
```
Misalnya, Anda dapat menjalankan perintah berikut untuk mengunduh file `/home/lnmp0.4.tar.gz` dari CVM yang IP publiknya adalah `129.20.0.2` ke direktori lokal yang sama:
```
scp root@129.20.0.2:/home/Inmp0.4.tar.gz /home/Inmp0.4.tar.gz
```


