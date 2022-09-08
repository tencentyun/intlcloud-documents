## Ikhtisar
Jika disk cloud Anda memiliki partisi MBR yang berisi sistem file, dengan ukuran disk kurang dari 2 TB setelah perluasan, Anda dapat menggunakan salah satu metode berikut untuk memperluas partisi dan sistem file:
- [Menetapkan kapasitas yang diperluas ke partisi MBR yang ada](#Add)
- [Memformat kapasitas yang diperluas menjadi partisi MBR baru yang terpisah](#New)


## Prasyarat
Anda dapat menggunakan alat perluasan otomatis termasuk fdisk, e2fsck dan resize2fs untuk menambahkan kapasitas disk cloud yang diperluas ke sistem file yang ada di CVM Linux.Untuk memastikan perluasan yang sukses, persyaratan berikut harus dipenuhi:
- Cara untuk memperluas dan mempartisi telah dikonfirmasi.Untuk informasi selengkapnya, lihat [Menentukan Metode Perluasan](https://intl.cloud.tencent.com/document/product/362/39995).
- Sistem file-nya adalah EXT2, EXT3, EXT4, atau XFS.
- Sistem file saat ini tidak memiliki kesalahan.
- Ukuran disk setelah perluasan tidak melebihi 2 TB.
- Hanya gunakan Python versi 2 karena kompatibilitas dengan alat perluasan dalam dokumen ini.



## Petunjuk

[](id:Add)
### Menetapkan kapasitas yang diperluas ke partisi MBR yang ada
Jalankan perintah berikut sebagai pengguna root untuk mengueri partisi disk cloud.
```
lsblk
```
- Output berikut menunjukkan bahwa hanya ada satu partisi.Dalam hal ini, Anda dapat melakukan [perluasan otomatis](#AutomaticExpansion) menggunakan alat.
![](https://main.qcloudimg.com/raw/297d678489b57dd70171a8882c9416f4.png)
- Output berikut menunjukkan bahwa ada dua partisi: `vdb1` dan `vdb2`.Dalam hal ini, Anda harus memilih partisi yang akan diperluas seperti yang diinstruksikan dalam [perluasan manual](#ManualExpansion).
![](https://main.qcloudimg.com/raw/070f2144acc543c84d4ab8ab3db25620.png)

<dx-tabs>
::: Perluasan\sOtomatis[](id:AutomaticExpansion)
a<blockquote class="doc-tip"><p class="doc-tip-tit"><i class="doc-icon-tip"></i>Note</p>Metode ini hanya berlaku untuk skenario ketika hanya ada satu partisi.Jika Anda memiliki dua atau lebih partisi, pilih [perluasan manual](#ManualExpansion).</p>
</blockquote>


1.Jalankan perintah berikut sebagai pengguna root untuk melepas partisi.
``` 
umount <Mount point>
```
Dengan menggunakan titik pemasangan `/data` sebagai contoh, jalankan perintah berikut:
```
umount /data
```
2.Jalankan perintah berikut untuk mengunduh alat perluasan.
```
wget -O /tmp/devresize.py https://raw.githubusercontent.com/tencentyun/tencentcloud-cbs-tools/master/devresize/devresize.py
```
3.Jalankan perintah berikut untuk menggunakan alat perluasan.
```
python /tmp/devresize.py <Disk path>
```
Dengan menggunakan jalur disk `/dev/vdb` dan sistem file `vdb1` sebagai contoh, jalankan perintah berikut:
```
python /tmp/devresize.py /dev/vdb
```
- Jika `The filesystem on /dev/vdb1 is now XXXXX blocks long.` ditampilkan sebagai berikut, perluasan berhasil.Selanjutnya, lakukan [langkah 4](#step4MBR).
![](https://main.qcloudimg.com/raw/689209e1d1f8a227274e8e65be07d2ec.png)
- Jika `[ERROR] - e2fsck failed!!` ditampilkan, lakukan langkah-langkah berikut:
a.Jalankan perintah berikut untuk memperbaiki partisi tempat sistem file berada.
```
fsck -a <Partition path>
```
Dengan menggunakan jalur disk `/dev/vdb` dan sistem file `vdb1` sebagai contoh, jalankan perintah berikut:
```
fsck -a /dev/vdb1
```
b.Setelah partisi diperbaiki, jalankan kembali perintah berikut untuk menggunakan alat perluasan.
```
python /tmp/devresize.py /dev/vdb
```
4. [](id:step4MBR)Jalankan perintah berikut untuk memasang partisi yang diperluas secara manual.Dokumen ini menggunakan titik pemasangan `/data` sebagai contoh.
```
mount <Partition path> <Mount point>
```
- Jika ada partisi di jalur partisi `/dev/vdb1` sebelum perluasan, jalankan perintah berikut:
```
mount /dev/vdb1 /data
```
5.Jalankan perintah berikut untuk melihat kapasitas partisi setelah perluasan.
```
df -h
```
Jika hasil yang mirip dengan gambar berikut dikembalikan, pemasangan berhasil, dan Anda dapat melihat disk data.
![](https://main.qcloudimg.com/raw/4f57fd2e0038dc1fba5a4389d01ab7dc.png)
6.Jalankan perintah berikut untuk melihat informasi data partisi asli setelah perluasan dan memeriksa apakah ruang penyimpanan baru telah ditambahkan ke sistem file.
```
ll /data
```
:::
::: Perluasan\sManual[](id:ManualExpansion)
1.Jalankan perintah berikut sebagai pengguna root untuk melepas partisi.
```
umount <Mount point>
```
Dengan menggunakan titik pemasangan `/data` sebagai contoh, jalankan perintah berikut:
```
umount /data
```
2.Jalankan perintah berikut untuk memperluas partisi `vdb2`.Ganti `vdb2` dengan partisi aktual Anda saat menggunakan perintah ini.
```
growpart /dev/vdb 2
```
3.Jalankan perintah berikut untuk memperluas sistem file partisi.
```
resize2fs /dev/vdb2
```
Jika output berikut dikembalikan, sistem file telah diperluas.
![](https://main.qcloudimg.com/raw/ba8d2693823a3eb0ccfc4dd097f09ed5.png)

4. [](id:step4MBR)Jalankan perintah berikut untuk memasang partisi yang diperluas secara manual.Dokumen ini menggunakan titik pemasangan `/data` sebagai contoh.
```
mount <Partition path> <Mount point>
```
Jika ada partisi di jalur partisi `/dev/vdb2` sebelum perluasan, jalankan perintah berikut:
```
mount /dev/vdb2 /data
```
5.Jalankan perintah berikut untuk melihat kapasitas partisi setelah perluasan.
```
df -h
```
Jika hasil yang mirip dengan gambar berikut dikembalikan, pemasangan berhasil, dan Anda dapat melihat disk data.

![](https://main.qcloudimg.com/raw/92cd4cc0e9b1c08975603f73e922266f.png)

6.Jalankan perintah berikut untuk melihat informasi data partisi asli setelah perluasan dan memeriksa apakah ruang penyimpanan baru telah ditambahkan ke sistem file.
```
ll /data
```
:::
</dx-tabs>


[](id:New)
### Memformat kapasitas yang diperluas menjadi partisi MBR baru yang terpisah
1.Jalankan perintah berikut sebagai pengguna root untuk melihat partisi yang dipasang dari disk data.
```
df -h
```
Seperti yang ditunjukkan pada gambar berikut, partisi yang dipasang dari disk data adalah 20 GB.
![](https://main.qcloudimg.com/raw/4f57fd2e0038dc1fba5a4389d01ab7dc.png)
2.Jalankan perintah berikut untuk melihat disk data yang tidak memiliki partisi setelah perluasan:
```
fdisk -l
```
Seperti yang ditunjukkan pada gambar berikut, disk data telah diperluas hingga 30 GB.

![](https://main.qcloudimg.com/raw/f21420374b4334a790022c95bac1fe0f.png)

3.Jalankan perintah berikut untuk melepas semua partisi yang terpasang.
```
umount <Mount point>
```
Dengan menggunakan titik pemasangan `/data` sebagai contoh, jalankan perintah berikut:
```
umount /data
```
>? Setelah semua partisi dilepas dari disk cloud, lakukan [langkah 4](#Step4MBR) lagi.
>

4. [](id:Step4MBR)Jalankan perintah berikut untuk membuat partisi.
```
fdisk <Disk path>
```
Dengan menggunakan jalur disk `/dev/vdb` sebagai contoh, jalankan perintah berikut:
```
fdisk /dev/vdb
```
Lakukan langkah-langkah berikut secara berurutan saat diminta.
1.Masukkan **p** untuk memeriksa partisi yang ada, seperti `/dev/vdb1` dalam dokumen ini.
2.Masukkan **n** untuk membuat partisi.
3.Masukkan **p** untuk membuat partisi utama.
4.Masukkan **2** untuk membuat partisi utama kedua.
5.Tekan **Enter** dua kali untuk menggunakan ukuran partisi default.
6.Masukkan **w** untuk menyimpan tabel partisi dan mulai mempartisi.
Lihat gambar di bawah ini:

![](https://main.qcloudimg.com/raw/894ba5a11a73d56a0a165ee7cb49e7c6.png)

>? Dokumen ini menggunakan membuat satu partisi sebagai contoh.Anda juga dapat membuat beberapa partisi untuk memenuhi kebutuhan Anda.
>
5.Jalankan perintah berikut untuk melihat partisi baru.
```
fdisk -l
```
Gambar berikut menunjukkan bahwa partisi baru `vdb2` telah dibuat.
![](https://main.qcloudimg.com/raw/d604d00955d0db5f052e964ecd409cc3.png)
6.Jalankan perintah berikut untuk memformat partisi baru dan membuat sistem file dalam format yang diinginkan, seperti EXT2 atau EXT3.
```
mkfs.<fstype> <Partition path>
```
Dengan menggunakan EXT4 sebagai contoh, jalankan perintah berikut:
```
mkfs.ext4 /dev/vdb2
```
Gambar berikut menunjukkan keberhasilan pembuatan sistem file EXT.
![](https://main.qcloudimg.com/raw/db15ed11252e6db8adb706f61ed14225.png)

7.Jalankan perintah berikut untuk membuat titik pemasangan.
```
mkdir <Titik pemasangan baru>
```
Dengan menggunakan titik pemasangan baru `/data1` sebagai contoh, jalankan perintah berikut:
```
mkdir /data1
```
8.Jalankan perintah berikut untuk memasang partisi baru secara manual.
```
mount <Jalur partisi baru> <Titik pemasangan baru>
```
Dengan menggunakan jalur partisi baru `/dev/vdb2` dan titik pemasangan baru `/data1` sebagai contoh, jalankan perintah berikut:
```
mount /dev/vdb1 /data2
```
9.Jalankan perintah berikut untuk melihat partisi baru.
```
df -h
```
Jika hasil seperti yang ditunjukkan pada gambar berikut dikembalikan, pemasangan berhasil, dan Anda dapat melihat disk data.
![](https://main.qcloudimg.com/raw/465c988014acc85957078335d776bfc3.png)
>? Untuk mengizinkan CVM memasang disk data secara otomatis saat mulai ulang atau startup, lakukan [langkah 10](#AddNewPartINFOstep10) dan [langkah 11](#AddNewPartINFOstep11) untuk menambahkan partisi baru ke `/etc/fstab`.

10. [](id:AddNewPartINFOstep10)Jalankan perintah berikut untuk menambahkan partisi.
```
echo '/dev/vdb2 /data1 ext4 defaults 0 0' >> /etc/fstab
```
11. [](id:AddNewPartINFOstep11)Jalankan perintah berikut untuk melihat partisi.
```
cat /etc/fstab
```
Jika hasil seperti yang ditunjukkan pada gambar berikut dikembalikan, partisi telah berhasil ditambahkan.
![](https://main.qcloudimg.com/raw/761a846bafe385b24dfb322a6ad2977f.png)

## Dokumentasi
[Memperluas Partisi dan Sistem File (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)

## Pertanyaan Umum
Jika Anda mengalami masalah saat menggunakan Tencent Cloud CBS, baca dokumen berikut untuk penanggulangan masalah sesuai  keperluan:
- [Pertanyaan Umum Penggunaan](https://intl.cloud.tencent.com/document/product/362/32409)
- [Pertanyaan Umum Fitur](https://intl.cloud.tencent.com/document/product/362/32408)
