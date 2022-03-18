## Skenario

Sistem file Windows biasanya menggunakan format NTFS atau FAT32, sedangkan sistem file Linux sering menggunakan format seri EXT. Ketika sistem operasi CVM diubah dari Windows ke Linux, disk data CVM tetap dalam format yang sama dengan sistem operasi aslinya. Akibatnya, setelah penginstalan ulang sistem, CVM mungkin tidak dapat mengakses sistem file dari disk data. Dokumen ini menjelaskan cara membaca disk data di sistem Windows asli setelah sistem operasi diinstal ulang dari Windows ke Linux.

## Petunjuk

### Mengaktifkan sistem Linux untuk mendukung NTFS 

1. Login ke CVM Linux setelah penginstalan ulang.
2. Jalankan perintah berikut untuk menginstal program perangkat lunak ntfsprogs guna mengaktifkan CVM Linux untuk mendukung akses ke sistem file NTFS.
>? Dokumen ini menggunakan CentOS sebagai contoh. Perhatikan bahwa berbagai jenis sistem Linux memerlukan perintah penginstalan yang berbeda. Dengan demikian, selalu jalankan perintah penginstalan yang sesuai untuk jenis sistem operasi Anda.
>
```
yum install ntfsprogs
```


### Memasang disk data dari CVM Windows ke CVM Linux

>? Jika disk data di CVM Windows Anda telah dipasang ke CVM Linux, lewati operasi ini.
>
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Di bilah sisi kiri, klik **[Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs)** ([Cloud Block Storage]) untuk membuka halaman pengelolaan Cloud Block Storage.
3. Pilih disk data Windows yang akan dipasang, lalu pilih **More** (Lainnya) > **Mount** (Pasang).
4. Di jendela "Pasang ke CVM" yang muncul, pilih CVM Linux target dan klik **OK** (Oke).
5. Login ke CVM Linux tempat disk data Windows telah dipasang.
6. Jalankan perintah berikut untuk mengkueri disk data yang dipasang dari Windows CVM.
```
parted -l
```
Informasi yang serupa dengan berikut ini akan ditampilkan:
```
Model: Virtio Block Device (virtblk)
Disk /dev/vdb: 53,7 GB
Ukuran sektor (logis/fisik): 512 B/512 B
Tabel Partisi: gpt
Flag Disk: 
Nomor  Mulai   Akhir     Ukuran    Sistem file Nama                          Flag
 1      17.4kB  134MB   134MB                Microsoft reserved partition  msftres
 2      135MB   53.7GB  53.6GB  ntfs         Basic data partition
```
7. Jalankan perintah berikut untuk memasang disk data.
```
mount -t ntfs-3g data disk path mount target
```
Misalnya, untuk memasang disk data di `/dev/vdb2` ke `/mnt`, jalankan perintah berikut:
```
mount -t ntfs-3g /dev/vdb2 /mnt
```
Karena sistem file dapat dikenali oleh sistem operasi, sistem Linux dapat langsung membaca data dari dan menulis data ke disk data yang terpasang.

