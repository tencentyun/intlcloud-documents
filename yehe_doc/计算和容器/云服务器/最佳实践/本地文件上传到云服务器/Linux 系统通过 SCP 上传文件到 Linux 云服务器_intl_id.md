## Pengantar
Dokumen tersebut menggunakan CVM dengan CentOS 7.6 sebagai contoh untuk menjelaskan cara mengunggah dan mengunduh file melalui SCP.


## Prasyarat
Anda telah membeli CVM Linux.

## Petunjuk
### Mendapatkan IP publik
Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index), buka halaman daftar instans, dan catat IP publik CVM tempat Anda ingin mengunggah file seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)


### Mengunggah file
1. Jalankan perintah berikut di komputer dengan OS Linux untuk mengunggah file ke CVM Linux.
```
Nama domain/IP publik instans CVM account@CVM alamat file lokal scp: Lokasi file CVM
```
Misalnya, jika Anda ingin mengunggah file lokal `/home/lnmp0.4.tar.gz` ke direktori yang sesuai dari CVM yang IP publiknya adalah `129.20.0.2`, jalankan perintah berikut:
```
scp /home/Inmp0.4.tar.gz root@129.20.0.2:/home/Inmp0.4.tar.gz
```
2. Masukkan **yes** (ya) dan tekan **Enter** (Enter) untuk mengonfirmasi unggahan dan masukkan kata sandi login untuk menyelesaikan unggahan.
 - Jika Anda menggunakan kata sandi default sistem untuk login ke instans, Anda dapat melihat kata sandi di [Pusat Pesan](https://console.cloud.tencent.com/message).
 - Jika Anda lupa kata sandi Anda, harap [atur ulang kata sandi instans](https://intl.cloud.tencent.com/document/product/213/16566).

### Mengunduh file
1. Jalankan perintah berikut di komputer dengan OS Linux untuk mengunduh file dari CVM Linux.
```
Nama domain/IP publik instans scp CVM account@CVM: Lokasi file CVM alamat file lokal   
```
Misalnya, jika Anda ingin mengunduh file `/home/lnmp0.4.tar.gz` dari CVM yang IP publiknya adalah `129.20.0.2` ke direktori lokal yang sesuai, jalankan perintah berikut:
```
scp root@129.20.0.2:/home/Inmp0.4.tar.gz /home/Inmp0.4.tar.gz
```
