## Ikhtisar
Dokumen ini menjelaskan cara menginisialisasi disk cloud yang baru saja dipasang ke CVM, membuat sistem file, dan menulis file dengan nama `qcloud.txt`.
<dx-alert infotype="explain" title="">
Untuk informasi selengkapnya tentang menginisialisasi disk cloud, silakan lihat [Skenario Inisialisasi](https://intl.cloud.tencent.com/document/product/362/31596).
</dx-alert>

## Catatan
Untuk mencegah kehilangan data, silakan lihat [Pertanyaan Umum Penggunaan](https://intl.cloud.tencent.com/document/product/362/32409#.E4.BA.91.E7.A1.AC.E7.9B.98.E4.BD.BF.E7.94.A8.E4.B8.8A.E6.9C.89.E4.BB.80.E4.B9.88.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9.EF.BC.9F) sebelum mengoperasikan disk cloud CBS Anda.

## Prasyarat
- Anda telah memasangkan disk cloud **cbs-test** ke CVM.Untuk petunjuk lengkapnya, lihat [Langkah 2.Memasang Disk Cloud](https://intl.cloud.tencent.com/document/product/362/39991).

## Petunjuk
<dx-tabs>
::: Memformat,membuat\ssistem\sfile,\sdan\smenulis\sfile\s(Windows)
<dx-alert infotype="explain" title="">

Dokumen ini menggunakan CVM dengan Windows Server 2012 R2 DataCenter 64-bit Tiongkok yang diinstal sebagai contoh.Perhatikan bahwa langkah-langkahnya dapat berbeda sesuai dengan versi sistem operasi.
</dx-alert>

1.Masuk ke instance CVM Windows sebagai pengguna admin.Lihat [Masuk ke Instance Windows Menggunakan RDP (Direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5435).
2.Di desktop, klik kanan <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-6px 0px"> di sudut kiri bawah.
3.Pilih **Disk Management** (Manajemen Disk) di menu pop-up untuk membuka jendela **Disk Management** (Manajemen Disk).
4.(Opsional) Klik kanan pada disk kosong yang Anda butuhkan, lalu pilih **Online**.
Ketika status disk berubah menjadi **Not Initialized** (Tidak Diinisialisasi), itu berarti disk kini tersedia secara online.
5.(Opsional) Klik kanan pada disk cloud yang baru saja tersedia secara online.Pilih **Initialize Disk** (Inisialisasi Disk) kemudian **Master Boot Record** di jendela pop-up **Initialize Disk** (Inisialisasi Disk), dan klik **OK**.
<dx-alert infotype="explain" title="">
- Format partisi Master Boot Record (MBR) mendukung disk dengan kapasitas maksimum sebesar 2 TB, dan and GUID Partition Table (GPT) mendukung disk dengan kapasitas maksimum sebesar 18 EB.Jika Anda membutuhkan kapasitas disk yang lebih besar dari 2 TB, silakan pilih format partisi GPT.
- Jika format partisi disk diubah setelah disk digunakan, data asli pada disk akan dihapus.Harap berhati-hati dalam memilih format partisi ketika menginisialisasi disk.
</dx-alert>
6.Klik kanan pada disk yang Anda butuhkan, pilih **New Simple Volume** (Volume Sederhana Baru), kemudian klik **Next** (Selanjutnya) di jendela pop-up.
7.Masukkan ukuran volume sederhana kemudian klik **Next** (Selanjutnya).
8.Pilih huruf drive atau path drive kemudian klik **Next** (Selanjutnya).Contoh ini menggunakan driver dengan huruf E.

9.Pilih sistem file, lakukan format cepat, kemudian klik **Next** (Selanjutnya).

10.Klik **Finish** (Selesai).
Status disk akan berubah menjadi **Formatting** (Memformat).Tunggu hingga inisialisasi selesai.Saat status volume menjadi **Healthy** (Sehat), inisialisasi disk berhasil.Anda dapat melihat disk data yang baru saja diformat di antarmuka **PC**.
11.Masukkan disk data yang baru saja diformat, buat file dengan nama `qcloud.txt`, masukkan konten yang Anda perlukan, kemudian pilih **File** > **Save** (File > Simpan).
:::
::: Memformat,\smembuat\ssistem\sfile,\sdan\smenulis\sfile\s(Linux)
<dx-alert infotype="notice" title="">
- Dokumen ini menggunakan CVM dengan CentOS 7.8 yang diinstal sebagai contoh.Perhatikan bahwa langkah-langkahnya dapat berbeda sesuai dengan versi sistem operasi.
- Contoh ini menggunakan sistem file EXT4.
- Ketika CVM Linux dimulai ulang atau dijalankan, disk data tidak akan terpasang secara otomatis.Anda dapat melihat [Langkah 9](#Step09) - [Langkah 14](#Step14) untuk mengonfigurasi pemasangan otomatis disk saat startup.
</dx-alert>
1.Masuk ke instance CVM Linux sebagai pengguna root.Lihat [Masuk ke Instance Linux Menggunakan Metode Masuk Standar](https://intl.cloud.tencent.com/document/product/213/5436).
2.Jalankan perintah berikut untuk melihat nama disk data yang terpasang pada instance.
 ```
fdisk -l
​``` Jika hasil yang dikembalikan seperti yang ditunjukkan pada gambar berikut, CVM saat ini memiliki dua disk, di antaranya `/dev/vda`, yaitu disk sistem dan `/dev/vdb`, yaitu disk data yang baru ditambahkan.
Dalam contoh ini, disk yang terpasang pada instance bernama `/dev/vdb`:
![](https://main.qcloudimg.com/raw/969d3ca3d95b16d47103886e11714868.png)
3.Jalankan perintah berikut untuk memformat disk.
 ```
mkfs.ext4 /dev/vdb
```
4.Jalankan perintah berikut untuk memasang disk ke titik pemasangan `/data`.
```
mount /dev/vdb /data
```
5.Jalankan perintah berikut untuk memasukkan disk dan membuat file baru `qcloud.txt`.
```
cd /data
``` 
```
vi qcloud.txt
```
6.Tekan **i** untuk masuk ke mode edit dan tuliskan **This is my first test.** (Ini adalah pengujian pertama saya.)
7.Tekan **Esc** untuk keluar dari mode edit, masukkan **:wq**, dan tekan **Enter** untuk menyimpan keluar dari file.
8.Jalankan perintah `ls`, dan Anda dapat melihat bahwa file `qcloud.txt` telah dituliskan dalam disk.
<dx-alert infotype="explain" title="">
Lihat [Langkah 9](#Step09) - [Langkah 14](#Step14) untuk mengonfigurasi pemasangan otomatis disk saat startup.Jika Anda tidak memerlukan pemasangan otomatis disk saat startup, lewati langkah-langkah berikut.
</dx-alert>
9. [](id:Step09)Jalankan perintah berikut untuk mencadangkan file `/etc/fstab` ke direktori `/home`, misalnya:
```
cp -r /etc/fstab /home
```
10.Jalankan perintah berikut untuk menggunakan editor VI untuk membuka file `/etc/fstab`.
```
vi /etc/fstab
```
11.Tekan **i** untuk masuk ke mode edit.
12.Pindahkan kursor ke akhir file, tekan **Enter**, dan tambahkan konten berikut.
​```plaintext
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency>
<Urutan pemeriksaan sistem file saat startup>
​``` Gunakan pemasangan otomatis menggunakan tautan lunak disk cloud elastis sebagai contoh.Tambahkan konten berikut:
```
/dev/disk/by-id/virtio-disk-drkhklpe /data ext4 defaults 0 0
```
<dx-alert infotype="explain" title="">
Anda dapat menjalankan perintah `ls -l /dev/disk/by-id` untuk mendapatkan tautan lunak disk cloud elastis.
</dx-alert>
13.Tekan **Esc**, masukkan `:wq`, dan tekan **Enter**.
Simpan konfigurasi dan keluar dari editor.
14. [](id:Step14)Jalankan perintah berikut untuk memeriksa apakah file `/etc/fstab` telah berhasil ditulis.
```
mount -a
``` 
Jika perintah berhasil dijalankan, file telah ditulis.Sistem file yang baru dibuat akan dipasang secara otomatis saat sistem operasi dijalankan.
:::

</dx-tabs>

## Operasi Berikutnya
Disk cloud adalah perangkat penyimpanan yang dapat diperluas di cloud.Anda dapat memperluas kapasitas disk cloud kapan saja tanpa kehilangan data apa pun di dalamnya agar sesuai dengan bisnis Anda.Untuk petunjuk lengkapnya, lihat [Langkah 4.Memperluas Kapasitas Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31646).
