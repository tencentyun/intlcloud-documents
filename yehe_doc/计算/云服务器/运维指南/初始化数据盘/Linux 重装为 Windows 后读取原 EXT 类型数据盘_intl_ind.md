
## Skenario
Windows menggunakan dua sistem file utama, NTFS atau FAT32, sedangkan EXT adalah sistem file de factor untuk Linux. Ketika sistem operasi diubah dari Linux ke Windows setelah penginstalan ulang, disk data tetap dalam format aslinya. Oleh karena itu, sistem mungkin tidak dapat mengakses sistem file disk data. Dalam kasus ini, Anda perlu menggunakan konverter format untuk membaca disk data. 

Dokumen ini menjelaskan cara membaca disk data ketika sistem operasi telah [diinstal ulang](https://intl.cloud.tencent.com/document/product/213/4933) dari Linux ke Windows.


## Prasyarat
- DiskInternals Linux Reader telah diinstal pada CVM Windows yang diinstal ulang.
Unduh DiskInternals Linux Reader: `http://www.diskinternals.com/download/Linux_Reader.exe `
- Misalkan disk data yang dipasang ke CVM Linux sebelum penginstalan ulang memiliki dua partisi, vdb1 dan vdb2, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/ef515a31c27e5ea96993af60dfc9ab55.png)

## Petunjuk
### Memasang disk data

> Jika disk data telah dipasang, lewati langkah ini.
>
1. Login ke [Konsol Tencent Cloud CVM](https://console.cloud.tencent.com/cvm/).
2. Klik **Cloud Block Storage** (Cloud Block Storage) dari bilah sisi kiri untuk masuk ke halaman pengelolaan Cloud Block Storage.
3. Temukan instans dengan sistem yang diinstal ulang, lalu klik **More** (Lainnya) > **Mount** (Pasang) di sebelah kanan seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/a3100055adb58330591e277c4e7f72eb.png)
4. Di jendela pop-up, pilih CVM Windows yang diinstal ulang dan klik **Submit** (Kirim).

### Melihat informasi disk data 
1. Jalankan DiskInternals Linux Reader untuk melihat informasi disk data yang baru dipasang. `/root/mnt` dan `/root/mnt1` masing-masing sesuai dengan vdb1 dan vdb2, yang merupakan 2 partisi disk data pada CVM Linux sebelum penginstalan ulang seperti yang ditunjukkan di bawah ini:
> Perhatikan bahwa disk data Linux saat ini bersifat hanya-baca. Untuk melakukan operasi baca dan tulis pada disk data seperti yang Anda lakukan pada disk data Windows, cadangkan file yang diperlukan dan format ulang disk ke dalam sistem file standar yang didukung Windows. Untuk informasi selengkapnya, harap lihat [Partisi Disk Data dan Pemformatan CVM Windows](https://intl.cloud.tencent.com/document/product/213/2158).
>
![](https://main.qcloudimg.com/raw/490428b0668dcd61c4c60bcb75121462.png)
2. Klik dua kali untuk masuk ke direktori `/root/mnt`, klik kanan file yang ingin Anda salin, lalu pilih **Save** (Simpan) seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/f36cbf32a7b423b8800e1fda6ba1c038.png)




