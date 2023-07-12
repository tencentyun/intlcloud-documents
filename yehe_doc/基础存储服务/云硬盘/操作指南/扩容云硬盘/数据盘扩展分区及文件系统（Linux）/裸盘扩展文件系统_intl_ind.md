## Ikhtisar
Dokumen ini menjelaskan cara memperluas sistem file setelah masuk ke instance CVM.Metode ini cocok untuk skenario ketika sistem file dibuat langsung tanpa mempartisi disk cloud.

## Petunjuk
1.Jalankan perintah berikut untuk menentukan jenis sistem file.
```
df -ihT
```
- Hasil berikut menunjukkan sistem file EXT.
![](https://main.qcloudimg.com/raw/198ad9bcb209db6ed1934e02f3234f8b.png)
- Hasil berikut menunjukkan sistem file XFS.
![](https://main.qcloudimg.com/raw/50ecea03c960daa2d04b734226ad69a0.png)
2.Gunakan perintah khusus sistem file untuk memperluas sistem file.
>?Perhatikan batas kapasitas berikut untuk sistem file EXT:
> - EXT3 mendukung hingga 16 TB, dan setiap file tidak boleh melebihi 2 TB.
> - EXT4 mendukung hingga 1 EB, dan setiap file tidak boleh melebihi 16 TB.
>
- Jalankan perintah berikut untuk memperluas sistem file EXT `/dev/vdb`.
```
resize2fs /dev/vdb
```
Jika output perintah berikut dikembalikan, perluasan berhasil.
![](https://main.qcloudimg.com/raw/9f68b0ab1e6446943da4e426df92919b.png)
- Jalankan perintah berikut untuk memperluas sistem file XFS `/dev/vdc`.
```
xfs_growfs /dev/vdc
```
Jika output perintah berikut dikembalikan, perluasan berhasil.
![](https://main.qcloudimg.com/raw/56fac50edbb153585adb67b2eb246cf4.png)
3.Jalankan perintah berikut untuk melihat ruang disk dari sistem file.
```
df -h
```
