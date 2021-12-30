## Ikhtisar
Anda dapat memperluas disk cloud untuk menambah ruang penyimpanannya.Dokumen ini menjelaskan cara memperluas disk cloud melalui konsol dan menetapkan kapasitas tambahannya tersebut untuk sistem file yang sudah ada.
>?Untuk informasi selengkapnya tentang perluasan disk cloud, lihat [Memperluas Kapasitas Disk Cloud](https://intl.cloud.tencent.com/document/product/362/5747).
>

## Catatan
Untuk melindungi data penting, Anda dapat [membuat snapshot](https://intl.cloud.tencent.com/document/product/362/5755) guna mencadangkan data disk cloud sebelum memperluasnya.

## Prasyarat
Anda telah [menginisialisasi disk cloud `cbs-test`](https://intl.cloud.tencent.com/document/product/362/31646).

## Petunjuk

#### Memperluas disk cloud (Windows)
### Memperluas disk cloud melalui konsol
1.Masuk ke konsol CVM dan klik [**Cloud Block Storage** (Penyimpanan Blok Cloud)](https://console.cloud.tencent.com/cvm/cbs) di bilah sisi kiri.
2.Temukan disk cloud yang akan diperluas dan klik **More** > **Expand** (Selengkapnya > Perluas) di bawah kolom **Operation** (Operasi) di sebelah kanan.

3.Di jendela pop-up **Expand Disk Capacity** (Perluas Kapasitas Disk), pilih kapasitas baru kemudian klik **Next** (Selanjutnya).
4.Klik **Adjust Now** (Sesuaikan Sekarang).

### Memindai ulang disk
>?Dokumen ini menggunakan CVM dengan Windows Server 2012 R2 DataCenter 64-bit Tiongkok yang diinstal sebagai contoh.Perhatikan bahwa langkah-langkahnya dapat berbeda sesuai dengan versi sistem operasi.
>
1.Masuk ke CVM sebagai admin.Lihat [Masuk ke Instance Windows Menggunakan RDP](https://intl.cloud.tencent.com/document/product/213/5435).
2.Di desktop, klik kanan <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-6px 0px"> di sudut kiri bawah, kemudian pilih **Computer Management** (Manajemen Komputer).
3.Klik kanan **Disk Management** (Manajemen Disk), dan pilih **Rescan Disk** (Pindai Ulang Disk).
4.Setelah pemindaian, periksa apakah ukuran disk data telah berhasil diperluas.

### Memperluas sistem file dari partisi yang ada
>?Dalam contoh ini, kami akan menetapkan kapasitas yang telah diperluas ke drive E yang sudah ada.Untuk informasi selengkapnya, lihat [Memperluas Partisi dan Sistem File (Windows)](https://intl.cloud.tencent.com/document/product/362/31601).
>
1.Klik kanan di mana saja pada ruang kosong disk, dan pilih **Extend Volume** (Perluas Volume).
2.Ikuti Extend Volume Wizard (Wizard Perluas Volume) untuk memperluas volume.
Kapasitas disk data baru akan ditambahkan ke volume asli.

#### Memperluas disk cloud (Linux)
### Memperluas disk cloud melalui konsol
1.Masuk ke konsol CVM dan klik [**Cloud Block Storage** (Penyimpanan Blok Cloud)](https://console.cloud.tencent.com/cvm/cbs) di bilah sisi kiri.
2.Temukan disk cloud yang akan diperluas dan klik **More** > **Expand** (Selengkapnya > Perluas) di bawah kolom **Operation** (Operasi) di sebelah kanan.
3.Di jendela pop-up **Expand Disk Capacity** (Perluas Kapasitas Disk), pilih kapasitas baru kemudian klik **Next** (Selanjutnya).
4.Klik **Adjust Now** (Sesuaikan Sekarang).

### Memperluas sistem file
>?
>- Dokumen ini menggunakan CVM dengan CentOS 7.8 yang diinstal sebagai contoh.Perhatikan bahwa langkah-langkahnya dapat berbeda sesuai dengan versi sistem operasi.
>- Dalam contoh ini, kami akan menetapkan kapasitas yang telah diperluas ke `/dev/vdb`.Untuk informasi selengkapnya, lihat [Memperluas Partisi dan Sistem File Secara Online](https://intl.cloud.tencent.com/document/product/362/39999).
>
1.Jalankan perintah berikut untuk memperluas sistem file EXT.
```
resize2fs /dev/vdb
​``` 
Informasi berikut akan muncul:

![](https://main.qcloudimg.com/raw/181bba4f10d3d5b48e2cbf331121affd.png)
2.Jalankan perintah berikut untuk melihat hasilnya.
```
df -TH
``` 
Jika informasi yang mirip dengan apa yang ditampilkan di bawah ini dikembalikan, sistem file telah diperluas.

![](https://main.qcloudimg.com/raw/7bb79ee4eca78a6ae77d2747967c0647.png)



## Dokumentasi
- [Skenario Perluasan Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31600)
- [Ikhtisar Snapshot](https://intl.cloud.tencent.com/document/product/362/31638)
