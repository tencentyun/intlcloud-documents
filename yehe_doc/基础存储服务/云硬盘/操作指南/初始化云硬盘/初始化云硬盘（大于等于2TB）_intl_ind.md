## Ikhtisar
Dokumen ini menjelaskan cara menginisialisasi disk cloud dengan kapasitas lebih besar atau sama dengan 2 TB.Untuk kasus lainnya, lihat [Skenario Inisialisasi](https://intl.cloud.tencent.com/document/product/362/31596).
MBR mendukung disk dengan kapasitas maksimum 2 TB.Saat Anda mempartisi disk dengan kapasitas lebih besar dari 2 TB, sebaiknya gunakan format partisi GPT.Ketika GPT digunakan pada sistem operasi Linux, fdisk tidak dapat digunakan lagi dan alat parted harus digunakan.

## Prasyarat
Anda telah [melampirkan disk cloud](https://intl.cloud.tencent.com/document/product/362/32401) ke CVM Anda.

## Catatan
- Untuk melindungi data penting, lihat [Pertanyaan Umum Penggunaan](https://intl.cloud.tencent.com/document/product/362/32409) sebelum mengoperasikan disk cloud CBS Anda.
- Memformat disk data akan menghapus semua data.Pastikan disk tidak berisi data, atau data penting telah dicadangkan.
- Untuk mencegah pengecualian layanan, pastikan CVM telah berhenti menyediakan layanan eksternal sebelum memformat.

## Petunjuk[](id:Steps)

<dx-tabs>
:::Menginisialisasi\sdisk\scloud\s(Windows)  [](id:2TBWindows2013)
Dokumen ini menggunakan CVM dengan Windows Server 2012 yang diinstal sebagai contoh.Perhatikan bahwa langkah-langkahnya dapat berbeda sesuai dengan versi sistem operasi.

1.[Masuk ke instance CVM Windows](https://intl.cloud.tencent.com/document/product/213/5435).
2.Pada desktop, klik <img src="https://main.qcloudimg.com/raw/0a02193a82217974f650bbcaf4e1ed2d.png"  style="margin:-5px 0px"> untuk masuk ke halaman **Server Manager** (Pengelola Server).
3.Di pohon navigasi kiri, klik **File and Storage Services** (Layanan File dan Penyimpanan).
4.Di pohon navigasi kiri, pilih **Volumes** > **Disks** (Volume > Disk).

Jika disk yang baru ditambahkan dalam status offline, jalankan [Langkah 5](#online) sebelum [Langkah 6](#initialize) untuk melakukan inisialisasi.Jika tidak, Anda dapat langsung menjalankan [Langkah 6](#initialize).

5. [](id:online)Disk terdaftar di panel sisi kanan.Klik kanan baris tempat 1 berada, dan pilih **Online** untuk membuatnya menjadi online.Maka statusnya menjadi **Online**.

6. [](id:initialize)Klik kanan baris tempat 1 berada, dan pilih **Initialize** (Inisialisasi) di menu.

7.Ikuti petunjuk pada antarmuka, dan klik **Yes** (Ya).

8.Setelah inisialisasi, partisi 1 berubah dari **Unknown** (Tidak Diketahui) menjadi **GPT**.Klik kanan baris tempat 1 berada dan pilih **New Simple Volume** (Volume Sederhana Baru) di menu.

9.Di kotak dialog pop-up **New Volume Wizard** (Wizard Volume Baru), ikuti petunjuk pada antarmuka dan klik **Next** (Selanjutnya).

10.Pilih server dan disk, dan klik **Next** (Selanjutnya).

11.Tentukan ukuran volume sesuai kebutuhan, yang merupakan nilai maksimum secara default.Klik **Next** (Selanjutnya).

12.Tetapkan huruf drive, dan klik **Next** (Selanjutnya).

13.Konfigurasikan parameter sesuai kebutuhan, format partisi, dan klik **Next** (Selanjutnya) untuk menyelesaikan pembuatan partisi.

14.Konfirmasikan informasi dan klik **Create** (Buat).

15.Tunggu hingga pembuatan volume selesai, lalu klik **Finish** (Selesai).
Setelah inisialisasi selesai, masuk ke antarmuka **My Computer** (Komputer Saya) untuk melihat disk baru.

:::
:::Menginisialisasi\sdisk\scloud\s(Linux)  [](id:2TBLinux)
Pilih metode inisialisasi sesuai dengan kasus penggunaan aktual Anda:
- Jika seluruh disk ditampilkan sebagai satu partisi terpisah (tidak ada disk logis seperti vdb1 dan vdb2), kami sangat menyarankan Anda untuk tidak menggunakan partisi, dan langsung [membuat sistem file pada perangkat kosong](#CreateFileSystemOnBareDevice).
- Jika seluruh disk perlu disajikan sebagai beberapa partisi logis (ada beberapa disk logis), Anda harus terlebih dahulu mempartisi disk, dan kemudian [membuat sistem file pada partisi](#CreateFileSystemOnPartition).


### Membuat sistem file pada perangkat kosong[](id:CreateFileSystemOnBareDevice)

1.[Masuk ke instance CVM Linux](https://intl.cloud.tencent.com/document/product/213/5436).
2.Jalankan perintah berikut sebagai pengguna root untuk melihat nama disk.
```
fdisk -l
``` Jika hasil yang dikembalikan seperti yang ditunjukkan pada gambar berikut, CVM saat ini memiliki dua disk, dengan `/dev/vda` adalah disk sistem dan `dev/vdb` adalah disk data yang baru ditambahkan.
![](https://main.qcloudimg.com/raw/aad842b12fec3ca583790bff609c9fb7.png)
3.Jalankan perintah berikut untuk membuat sistem file pada perangkat kosong `/dev/vdb`.
``` 
mkfs -t <Format sistem file> /dev/vdb
``` Ukuran partisi yang didukung oleh berbagai sistem file berbeda.Pilih sistem file yang sesuai dengan kebutuhan.Contoh berikut menggunakan `EXT4` sebagai sistem file:
```
mkfs -t ext4 /dev/vdb
```
>! Pemformatan membutuhkan waktu.Perhatikan status sistem yang berjalan dan jangan keluar.
4.Jalankan perintah berikut untuk membuat titik pemasangan baru.
```
mkdir <Mount point>
``` Gunakan membuat titik pemasangan baru `/data` sebagai contoh:
```
mkdir /data
```
5.Jalankan perintah berikut untuk memasang partisi baru ke titik pemasangan yang baru dibuat.
```
mount /dev/vdb <Mount point>
``` Gunakan membuat titik pemasangan baru `/data` sebagai contoh:
```
mount /dev/vdb /data
```
6.Jalankan perintah berikut untuk melihat hasil pemasangan.
```
df -TH
```
Jika Anda tidak perlu mengonfigurasi pemasangan otomatis disk saat startup, lewati langkah-langkah berikut.
7.Konfirmasikan metode pemasangan dan dapatkan informasi yang sesuai.
Berdasarkan kebutuhan bisnis, Anda dapat menggunakan tautan lunak disk cloud elastis, UUID sistem file (pengidentifikasi unik universal), atau nama perangkat untuk memasang disk secara otomatis.Deskripsi dan metode perolehan informasi adalah sebagai berikut:
<table>
<tr>
<th>Metode pemasangan</th>
<th>Kelebihan dan kekurangan</th>
<th>Metode perolehan informasi</th>
</tr>
<tr>
<td nowrap="nowrap">Menggunakan tautan lunak disk cloud elastis <b>(direkomendasikan)</b></td>
<td><b>Kelebihan</b>: tautan lunak disk cloud elastis bersifat tetap dan unik.Tautan tersebut tidak berubah dengan operasi seperti pemasangan, pelepasan, dan pemformatan partisi.</br><b>Kekurangan</b>: hanya disk cloud elastis yang dapat menggunakan tautan lunak, yang beroperasi tanpa terasa untuk operasi pemformatan partisi.</td>
<td nowrap="nowrap">Menjalankan perintah berikut untuk mendapatkan tautan lunak dari disk cloud elastis.</br><pre style="color:white;">ls -l /dev/disk/by-id</pre></td>
</tr>
<tr>
<td nowrap="nowrap">Menggunakan UUID sistem file</td>
<td>Konfigurasi pemasangan otomatis mungkin gagal karena perubahan UUID sistem file.</br>Misalnya, memformat ulang sistem file akan mengubah UUID-nya.</td>
<td nowrap="nowrap">Menjalankan perintah berikut untuk mendapatkan UUID sistem file.</br><pre style="color:white;">blkid /dev/vdb</pre></td>
</tr>
<tr>
<td nowrap="nowrap">Menggunakan nama perangkat</td>
<td>Konfigurasi pemasangan otomatis mungkin gagal karena perubahan nama perangkat.</br>Misalnya, jika disk cloud elastis di CVM dilepas dan dipasang kembali, nama perangkat dapat berubah saat sistem operasi mengenali sistem file lagi.</td>
<td nowrap="nowrap">Menjalankan perintah berikut untuk mendapatkan nama perangkat.</br><pre style="color:white;">fdisk -l</pre></td>
</tr>
</table>
8.Jalankan perintah berikut untuk mencadangkan file `/etc/fstab` ke direktori `/home`, misalnya:
```
cp -r /etc/fstab /home
```
9.Jalankan perintah berikut untuk menggunakan editor VI untuk membuka file `/etc/fstab`.
```
vi /etc/fstab
```
10.Tekan **i** untuk masuk ke mode edit.
11.Pindahkan kursor ke akhir file, tekan **Enter**, dan tambahkan konten berikut.
```plaintext
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency>
<Urutan pemeriksaan sistem file saat startup>
```
- **(Direkomendasikan)** Gunakan pemasangan otomatis menggunakan tautan lunak disk cloud elastis sebagai contoh.Tambahkan konten berikut:
```
/dev/disk/by-id/virtio-disk-drkhklpe /data ext4 defaults 0 0
```
- Gunakan pemasangan otomatis menggunakan UUID partisi disk sebagai contoh.Tambahkan konten berikut:
```
UUID=d489ca1c-5057-4536-81cb-ceb2847f9954 /data  ext4 defaults     0   0
```
- Gunakan pemasangan otomatis menggunakan nama perangkat sebagai contoh.Tambahkan konten berikut:
```
/dev/vdb /data   ext4 defaults     0   0
```
12.Tekan **Esc**, masukkan **:wq**, dan tekan **Enter**.
Simpan konfigurasi dan keluar dari editor.
13.Jalankan perintah berikut untuk memeriksa apakah file `/etc/fstab` telah berhasil ditulis.
```
mount -a
``` Jika perintah berhasil dijalankan, file telah ditulis.Sistem file yang baru dibuat akan dipasang secara otomatis saat sistem operasi dijalankan.


### Membuat sistem file pada partisi[](id:CreateFileSystemOnPartition)

Contoh ini menggunakan alat partisi parted di sistem operasi CentOS 7.5 untuk mengonfigurasi disk data `/dev/vdc` sebagai partisi utama.GPT digunakan sebagai format partisi default, format EXT4 sebagai sistem file, dan `/data/newpart2` sebagai titik pemasangan.Pemasangan otomatis disk saat startup dikonfigurasi.Perhatikan bahwa operasi pemformatan dapat berbeda berdasarkan sistem operasi.

1.[Masuk ke instance CVM Linux](https://intl.cloud.tencent.com/document/product/213/5436).
2.Jalankan perintah berikut sebagai pengguna root untuk melihat nama disk.
 ```
lsblk
``` Jika hasil yang dikembalikan seperti yang ditunjukkan pada gambar berikut, CVM saat ini memiliki dua disk, dengan `/dev/vda` adalah disk sistem dan `/dev/vdc` adalah disk data yang baru ditambahkan.
![](https://main.qcloudimg.com/raw/72a7a48c59c13a44958a6b1aa0407ac2.png)
3.Jalankan perintah berikut untuk menggunakan alat parted untuk mempartisi disk data yang baru ditambahkan.
```
parted <Disk data yang baru ditambahkan>
``` Gunakan disk data yang baru dipasang `/dev/vdc` sebagai contoh:
```
parted /dev/vdc
``` Informasi yang dikembalikan mirip dengan yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/0b2c9164f9fec125a72dee8861b7327d.png)
4.Masukkan `p` dan tekan **Enter** untuk melihat format partisi disk saat ini.
Informasi yang dikembalikan mirip dengan yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/af906521dd6a7f3b948cfad42745aaba.png)
**Partition Table: unknown** (Tabel Partisi: tidak diketahui) menunjukkan bahwa format partisi disk tidak diketahui.
5.Jalankan perintah berikut untuk mengonfigurasi format partisi disk.
```
mklabel <Format partisi disk>
``` Jika kapasitas disk lebih besar atau sama dengan 2 TB, hanya format partisi GPT yang dapat digunakan:
```
mklabel gpt
```
6.Masukkan `p` dan tekan **Enter** untuk memeriksa apakah format partisi disk telah berhasil dikonfigurasi.
Informasi yang dikembalikan mirip dengan yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/3dfec9aba75cd3cb6dcfb06729f5ff26.png)
**Partition Table: gpt** (Tabel Partisi: gpt) menunjukkan bahwa format partisi disk adalah GPT.
7.Masukkan `unit s` dan tekan **Enter** untuk mengatur unit disk ke sektor.
8.Gunakan membuat satu partisi untuk seluruh disk sebagai contoh, masukkan `mkpart opt ​​2048s 100%` dan tekan **Enter**.
Nilai 2048s menunjukkan kapasitas disk awal dan 100% menunjukkan kapasitas disk akhir.Ini hanya untuk referensi.Anda dapat memilih jumlah partisi disk dan kapasitasnya berdasarkan kebutuhan bisnis.
9.Masukkan `p` dan tekan **Enter** untuk melihat informasi tentang partisi yang baru dibuat.
Informasi yang dikembalikan mirip dengan yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/ee406e75c689f48d59e863adc768aa36.png)
Ini menunjukkan informasi detail dari partisi `/dev/vdc1` yang baru dibuat.
10.Masukkan `q` dan tekan **Enter** untuk keluar dari alat partisi parted.
11.Jalankan perintah berikut untuk melihat nama disk.
```
lsblk
``` Informasi yang dikembalikan mirip dengan yang ditunjukkan di bawah ini.Anda sekarang dapat melihat partisi baru `/dev/vdc1`.
![](https://main.qcloudimg.com/raw/f95f599f11f88b8bcb89d4f02bb41292.png)
12.Jalankan perintah berikut untuk mengonfigurasi sistem file dari partisi yang baru dibuat ke yang diperlukan oleh sistem.
```
mkfs -t <Format sistem file> /dev/vdc1
``` Ukuran partisi yang didukung oleh berbagai sistem file berbeda.Pilih sistem file yang sesuai dengan kebutuhan.Contoh berikut menggunakan `EXT4` sebagai sistem file:
```
mkfs -t ext4 /dev/vdc1
```  Informasi yang dikembalikan mirip dengan yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/3cd6bbd019dd9bdc85ad4ed11ba64f0b.png)
Pemformatan membutuhkan waktu.Perhatikan status sistem yang berjalan dan jangan keluar.
13.Jalankan perintah berikut untuk membuat titik pemasangan baru.
```
mkdir <Mount point>
``` Gunakan membuat titik pemasangan baru `/data/newpart2` sebagai contoh:
```
mkdir /data/newpart2
```
14.Jalankan perintah berikut untuk memasang partisi baru ke titik pemasangan yang baru dibuat.
```
mount /dev/vdc1 <Mount point>
``` Gunakan membuat titik pemasangan baru `/data/newpart2` sebagai contoh:
```
mount /dev/vdc1 /data/newpart2
```
15.Jalankan perintah berikut untuk melihat hasil pemasangan.
```
df -TH
```Informasi yang dikembalikan mirip dengan yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/774c2d9ff266634c4836df6456b9dd4d.png)
Ini menunjukkan bahwa partisi `/dev/vdc1` yang baru dibuat telah dipasang ke `/data/newpart2`.
Jika Anda tidak perlu mengonfigurasi pemasangan otomatis disk saat startup, lewati langkah-langkah berikut.
>
16.Konfirmasikan metode pemasangan dan dapatkan informasi yang sesuai.
Berdasarkan kebutuhan bisnis, Anda dapat menggunakan tautan lunak disk cloud elastis, UUID sistem file (pengidentifikasi unik universal), atau nama perangkat untuk memasang disk secara otomatis.Deskripsi dan metode perolehan informasi adalah sebagai berikut:
<table>
<tr>
<th>Metode pemasangan</th>
<th>Kelebihan dan kekurangan</th>
<th>Metode perolehan informasi</th>
</tr>
<tr>
<td nowrap="nowrap">Menggunakan tautan lunak disk cloud elastis<b>(direkomendasikan)</b></td>
<td><b>Kelebihan</b>: tautan lunak disk cloud elastis bersifat tetap dan unik.Tautan tersebut tidak berubah dengan operasi seperti pemasangan, pelepasan, dan pemformatan partisi.</br><b>Kekurangan</b>: hanya disk cloud elastis yang dapat menggunakan tautan lunak, yang beroperasi tanpa terasa untuk operasi pemformatan partisi.</td>
<td nowrap="nowrap">Menjalankan perintah berikut untuk mendapatkan tautan lunak dari disk cloud elastis.</br><pre style="color:white;">ls -l /dev/disk/by-id</pre></td>
</tr>
<tr>
<td nowrap="nowrap">Menggunakan UUID sistem file</td>
<td>Konfigurasi pemasangan otomatis mungkin gagal karena perubahan UUID sistem file.</br>Misalnya, memformat ulang sistem file akan mengubah UUID-nya.</td>
<td nowrap="nowrap">Jalankan perintah berikut untuk mendapatkan UUID sistem file.</br><pre style="color:white;"> blkid /dev/vdc1</pre></td>
</tr>
<tr>
<td nowrap="nowrap">Menggunakan nama perangkat</td>
<td>Konfigurasi pemasangan otomatis mungkin gagal karena perubahan nama perangkat.</br>Misalnya, jika disk cloud elastis di CVM dilepas dan dipasang kembali, nama perangkat dapat berubah saat sistem operasi mengenali sistem file lagi.</td>
<td>Menjalankan perintah berikut untuk mendapatkan nama perangkat.</br><pre style="color:white;">fdisk -l</pre></td>
</tr>
</table>
17.Jalankan perintah berikut untuk mencadangkan file `/etc/fstab` ke direktori `/home`, misalnya:
```
cp -r /etc/fstab /home
```
18.Jalankan perintah berikut untuk menggunakan editor VI untuk membuka file `/etc/fstab`.
 ```
vi /etc/fstab
```
19.Tekan **i** untuk masuk ke mode edit.
20.Pindahkan kursor ke akhir file, tekan **Enter**, dan tambahkan konten berikut.
```plaintext
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency>
<Urutan pemeriksaan sistem file saat startup>
```
- **(Direkomendasikan)** Gunakan pemasangan otomatis menggunakan tautan lunak disk cloud elastis sebagai contoh.Tambahkan konten berikut:
 ```
/dev/disk/by-id/virtio-disk-bm42ztpm-part1 /data/newpart2   ext4 defaults     0   2
```
- Gunakan pemasangan otomatis menggunakan UUID partisi disk sebagai contoh.Tambahkan konten berikut:
```
UUID=fc3f42cc-2093-49c7-b4fd-c616ba6165f4 /data/newpart2   ext4 defaults     0   2
```
- Gunakan pemasangan otomatis menggunakan nama perangkat sebagai contoh.Tambahkan konten berikut:
```
/dev/vdc1 /data/newpart2   ext4 defaults     0   2
```
20.Tekan **Esc**, masukkan **:wq**, dan tekan **Enter**.
Simpan konfigurasi dan keluar dari editor.
21.Jalankan perintah berikut untuk memeriksa apakah file `/etc/fstab` telah berhasil ditulis.
```
mount -a
``` Jika perintah berhasil dijalankan, file telah ditulis.Sistem file yang baru dibuat akan dipasang secara otomatis saat sistem operasi dijalankan.
:::
</dx-tabs>


## Operasi yang Relevan
[Menginisialisasi Disk Cloud (<2 TB)](https://intl.cloud.tencent.com/document/product/362/31597).
