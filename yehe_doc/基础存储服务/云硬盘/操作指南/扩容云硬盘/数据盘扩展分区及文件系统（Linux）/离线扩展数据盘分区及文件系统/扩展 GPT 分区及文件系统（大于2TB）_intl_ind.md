## Ikhtisar
Jika disk cloud Anda memiliki partisi GPT yang berisi sistem file, Anda dapat menggunakan salah satu metode berikut untuk memperluas partisi dan sistem file:
- [Menetapkan kapasitas yang diperluas ke partisi GPT yang ada](#Add)
- [Memformat kapasitas yang diperluas menjadi partisi GPT baru yang terpisah](#New)



## Prasyarat
Anda dapat menggunakan alat perluasan otomatis termasuk e2fsck dan resize2fs untuk menambahkan kapasitas disk cloud yang diperluas ke sistem file yang ada di CVM Linux.Untuk memastikan perluasan yang sukses, persyaratan berikut harus dipenuhi:
- Cara untuk memperluas dan mempartisi telah dikonfirmasi.Untuk informasi selengkapnya, lihat [Menentukan Metode Perluasan](https://intl.cloud.tencent.com/document/product/362/39995).
- Sistem file-nya adalah EXT atau XFS.
- Sistem file saat ini tidak memiliki kesalahan.


## Petunjuk

[](id:Add)
### Menetapkan kapasitas yang diperluas ke partisi GPT yang ada
1.Jalankan perintah berikut sebagai pengguna root untuk mengonfirmasi perubahan kapasitas disk cloud.
```
parted <Disk path> print
```
Dengan menggunakan jalur disk `/dev/vdc` sebagai contoh, jalankan perintah berikut:
```
parted /dev/vdc print
```
Jika pesan seperti yang ditunjukkan pada gambar berikut muncul dalam proses, masukkan `Fix`.
![](https://main.qcloudimg.com/raw/bdc9f2fcb281e24ec5799e73c08535eb.png)
Ukuran disk cloud adalah 2.040 GB setelah perluasan dan kapasitas partisi yang ada adalah 10,7 GB, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/40a1141f65ba7ac15b8dac4b94e0d6a5.png)
2.Jalankan perintah berikut untuk memeriksa apakah disk cloud memiliki partisi yang terpasang.
```
mount | grep '<Disk path>'
```
Dengan menggunakan jalur disk `/dev/vdc` sebagai contoh, jalankan perintah berikut:
```
mount | grep '/dev/vdc'
```
- Hasil berikut menunjukkan bahwa disk cloud memiliki satu partisi (vdc1) yang dipasang ke `/data`.
![](https://main.qcloudimg.com/raw/61ae197d19c522f6ebd1e9c7bf4b4d88.png)
Jalankan perintah berikut untuk melepas **semua partisi** dari disk cloud.
```
umount <Mount point>
```
Dengan menggunakan titik pemasangan `/data` sebagai contoh, jalankan perintah berikut:
```
umount /data
```
- Hasil berikut menunjukkan bahwa tidak ada partisi yang terpasang.Lanjutkan ke langkah berikutnya.
![](https://main.qcloudimg.com/raw/4a6d070830fd0629a336836fd6b4c1fd.png)
3.Jalankan perintah berikut untuk menggunakan alat partisi parted.
```
parted '<Disk path>'
```
Dengan menggunakan jalur disk `/dev/vdc` sebagai contoh, jalankan perintah berikut:
```
parted '/dev/vdc'
```
4.Jalankan perintah berikut untuk mengubah unit dari pengaturan default "GB" menjadi "sector" untuk tampilan dan pengoperasian.
```
unit s
```
5. [](id:step5)Jalankan perintah berikut untuk melihat partisi dan mencatat nilai `Start`.
```
print
```
>! Catat nilai `Start`.Setelah partisi dihapus dan partisi yang baru dibuat, nilai `Start` harus tetap tidak berubah.Jika tidak, data akan hilang.
>
![](https://main.qcloudimg.com/raw/a4b3b6710d2d03549c26b8efd7d844db.png)
6.Jalankan perintah berikut untuk menghapus partisi yang ada.
```
rm <Partition Number>
```
Misalnya, jalankan perintah berikut untuk menghapus partisi “1” dari disk cloud.
```
rm 1
```
7.Jalankan perintah berikut untuk mengonfirmasi penghapusan.Informasi yang dikembalikan adalah seperti yang ditunjukkan di bawah ini:
```
print
```
![](https://main.qcloudimg.com/raw/fbac9760d06da56e3f3be3a61309cc10.png)
>!Anda dapat segera menjalankan perintah `rescue`, dan memasukkan nilai `Start` dan `End` saat diminta untuk memulihkan partisi yang terhapus secara tidak sengaja.
>
8.Jalankan perintah berikut untuk membuat partisi utama baru.
```
mkpart primary <Sektor awal dari partisi asli> 100%
```
100% dalam perintah menunjukkan partisi ini untuk akhir disk.Masukkan nilai `Start` yang diperoleh di [langkah 5](#step5).Dalam dokumen ini, sektor awal dari partisi asli adalah 2048s (yaitu, nilai `Start` adalah 2048s), jalankan perintah berikut:
```
mkpart primary 2048s 100%
```
Jika status muncul seperti yang ditunjukkan pada gambar berikut, masukkan `Ignore`.
![](//mccdn.qcloud.com/static/img/c45966e20dc856817c65fd6b81155e4a/image.png)
9.Jalankan perintah berikut untuk memeriksa apakah partisi baru telah berhasil dibuat.
```
print
```
Jika hasil seperti yang ditunjukkan pada gambar berikut dikembalikan, partisi baru telah berhasil dibuat.
![](https://main.qcloudimg.com/raw/823646dcfd0e42ece63a37338e0d4e16.png)
10.Jalankan perintah berikut untuk menutup alat parted.
```
quit
```
11.Jalankan perintah berikut untuk memeriksa partisi yang diperluas.
```
e2fsck -f <Partition path>
```
Dengan menggunakan partisi baru “1” (jalur partisinya adalah `/dev/vdc1`) sebagai contoh, jalankan perintah berikut:
```
e2fsck -f /dev/vdc1
```
Gambar berikut menunjukkan output perintah.
![](https://main.qcloudimg.com/raw/12c917c78829014cd784e3f184c01eed.png)
12.Gunakan perintah khusus sistem file untuk mengubah ukuran setiap sistem file di partisi baru.
- Jalankan perintah berikut pada **Sistem file EXT**.
```
resize2fs <Partition path>
```
Dengan menggunakan jalur partisi `/dev/vdc1 sebagai contoh, jalankan perintah berikut:
```
resize2fs /dev/vdc1
```
Jika hasil seperti yang ditunjukkan pada gambar berikut dikembalikan, perluasan berhasil.
![](https://main.qcloudimg.com/raw/7daebff27ce10c66b63c2b35c9712418.png)
- Jalankan perintah berikut pada **sistem file XFS**.
```
xfs_growfs <Partition path>
```
Dengan menggunakan jalur partisi `/dev/vdc1` sebagai contoh, jalankan perintah berikut:
```
xfs_growfs /dev/vdc1
```
13.Jalankan perintah berikut untuk memasang partisi baru secara manual.
```
mount <Partition path> <Mount point>
```
Dengan menggunakan jalur partisi `/dev/vdc1` dan titik pemasangan `/data` sebagai contoh, jalankan perintah berikut:
```
mount /dev/vdc1 /data
```
14.Jalankan perintah berikut untuk melihat partisi baru.
```
df -h
```
Jika hasil seperti yang ditunjukkan pada gambar berikut dikembalikan, pemasangan berhasil, dan Anda dapat melihat disk data.
![](https://main.qcloudimg.com/raw/476829f5a9cb6aef62f3cace31cb2586.png)

[](id:New)
### Memformat kapasitas yang diperluas menjadi partisi GPT baru yang terpisah
1.Jalankan perintah berikut sebagai pengguna root untuk mengonfirmasi perubahan kapasitas disk cloud.
```
parted <Disk path> print
```
Dengan menggunakan jalur disk `/dev/vdc` sebagai contoh, jalankan perintah berikut:
```
parted /dev/vdc print
```
Jika pesan seperti yang ditunjukkan pada gambar berikut muncul dalam proses, masukkan `Fix`.
![](https://main.qcloudimg.com/raw/c69cd8b3741675f1a96715c4679ce6e6.png)
Ukuran disk cloud adalah 2.147 GB setelah perluasan dan kapasitas partisi yang ada adalah 2.040 GB, seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/8d8e72b1a5716443673453f67c1d798d.png)
2.Jalankan perintah berikut untuk memeriksa apakah disk cloud memiliki partisi yang terpasang.
```
mount | grep '<Disk path>'
```
Dengan menggunakan jalur disk `/dev/vdc` sebagai contoh, jalankan perintah berikut:
```
mount | grep '/dev/vdc'
```
- Hasil berikut menunjukkan bahwa disk cloud memiliki satu partisi (vdc1) yang dipasang ke `/data`.
![](https://main.qcloudimg.com/raw/1703f6594a1fbff86dd1d1dfb2ab124d.png)
Jalankan perintah berikut untuk melepas **semua partisi** dari disk cloud.
```
umount <Mount point>
```
Dengan menggunakan titik pemasangan `/data` sebagai contoh, jalankan perintah berikut:
```
umount /data
```
- Hasil berikut menunjukkan bahwa tidak ada partisi yang terpasang.Lanjutkan ke langkah berikutnya.
![](https://main.qcloudimg.com/raw/d10d74c1fff5e8ffdb306d5acb664ae1.png)
3.Jalankan perintah berikut untuk menggunakan alat partisi parted.
```
parted '<Disk path>'
```
Dengan menggunakan jalur disk `/dev/vdc` sebagai contoh, jalankan perintah berikut:
```
parted '/dev/vdc'
```
4. [](id:Step4)Jalankan perintah berikut untuk melihat partisi dan mencatat nilai `End`, yang akan digunakan sebagai offset awal partisi berikutnya.
```
print
```
![](https://main.qcloudimg.com/raw/7f11b89e481035897d525fa8a93cb7e7.png)
5.Jalankan perintah berikut untuk membuat partisi utama.Partisi ini dimulai pada akhir partisi yang ada, dan mencakup semua ruang baru pada disk.
```
mkpart primary start end
```
Dapatkan nilai `End` di [langkah 4](#Step4).Dalam contoh ini, nilai `End` adalah 2.040 GB, jalankan perintah berikut:
```
mkpart primary 2040GB 100%
```
6.Jalankan perintah berikut untuk memeriksa apakah partisi baru telah dibuat.
```
print
```
Jika output berikut dikembalikan, partisi telah dibuat.
![](https://main.qcloudimg.com/raw/5e1418caaddf22932ac624ff906cf302.png)
7.Jalankan perintah berikut untuk menutup alat parted.
```
quit
```
8.Jalankan perintah berikut untuk memformat partisi baru menjadi EXT2, EXT3, dll. sesuai kebutuhan.
```
mkfs.<fstype> <Partition path>
```
Dengan menggunakan EXT4 sebagai contoh, jalankan perintah berikut:
```
mkfs.ext4 /dev/vdc2
```
9.Jalankan perintah berikut untuk memasang partisi baru secara manual.
```
mount <Partition path> <Mount point>
```
Dengan menggunakan jalur partisi `/dev/vdc2` dan titik pemasangan `/data` sebagai contoh, jalankan perintah berikut:
```
mount /dev/vdc2 /data
```
10.Jalankan perintah berikut untuk melihat partisi baru:
```
df -h
```
Jika hasil seperti yang ditunjukkan pada gambar berikut dikembalikan, pemasangan berhasil, dan Anda dapat melihat disk data.
![](https://main.qcloudimg.com/raw/cd9d36d49388882f0cb898c13d565bb0.png)

## Dokumentasi
[Memperluas Partisi dan Sistem File (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)

## Pertanyaan Umum
Jika Anda mengalami masalah saat menggunakan Tencent Cloud CBS, baca dokumen berikut untuk penanggulangan masalah sesuai  keperluan:
- [Pertanyaan Umum Penggunaan](https://cloud.tencent.com/document/product/362/17819)
- [Pertanyaan Umum Fitur](https://cloud.tencent.com/document/product/362/17818)
