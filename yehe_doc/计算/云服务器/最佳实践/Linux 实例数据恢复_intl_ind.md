## Ikhtisar
Extundelete adalah alat pemulihan data sumber terbuka. Fitur canggih ini mendukung pemulihan partisi ext3 dan ext4 dari file disk data yang terhapus secara tidak sengaja, asalkan disk tidak ditulis setelah kecelakaan. Dokumen ini menjelaskan cara menggunakan Extundelete untuk memulihkan data yang terhapus secara tidak sengaja pada CentOS 7.7 Tencent Cloud CVM dengan cepat.
Tencent Cloud juga menawarkan [snapshot](https://intl.cloud.tencent.com/document/product/362/5755), [citra kustom](https://intl.cloud.tencent.com/document/product/213/4942), dan [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436/6222) untuk menyimpan data. Sebaiknya buat cadangan data secara teratur untuk meningkatkan keamanan data.

## Perangkat Lunak
- Linux: Sistem operasi Linux. Dokumen ini menggunakan CentOS 7.7 sebagai contoh.
- Extundelete: alat pemulihan data sumber terbuka. Dokumen ini menggunakan Extundelete 0.2.4 sebagai contoh.


## Petunjuk
>!Lihat [Membuat Snapshot](https://intl.cloud.tencent.com/document/product/362/5755) dan [Membuat Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4942) untuk mencadangkan data sebelum melakukan operasi sehingga Anda dapat memulihkan instans ke status awalnya jika terjadi masalah.
>

### Menginstal Extundelete
1. Jalankan perintah berikut untuk menginstal dependensi dan pustaka Extundelete.
>!
>- Extundelete membutuhkan libext2fs versi 1.39 atau yang lebih baru.
>- Untuk mendukung format ext4, instal e1fsprogs versi 1.41 atau yang lebih baru. Anda dapat menggunakan perintah `dumpe2fs` untuk melihat versi. 
>
```
yum -y install  bzip2  e2fsprogs-devel  e2fsprogs  gcc-c++  make
```
2. Unduh paket penginstalan [Extundelete](https://sourceforge.net/projects/extundelete/).
3. Jalankan perintah berikut secara berurutan untuk mendekompresi paket penginstalan Extundelete dan mengakses direktorinya.
```
tar -xvjf extundelete-0.2.4.tar.bz2
```
```
cd extundelete-0.2.4 
```
4. Jalankan perintah berikut secara berurutan untuk mengompilasi dan menginstal Extundelete.
```
./configure   
```
```
make && make install
```
Setelah penginstalan selesai, Anda akan dapat melihat file yang dapat dijalankan “extundelete” di direktori `usr/local/bin`.

### Menguji pemulihan data
Pulihkan data sesuai kebutuhan dengan melakukan langkah-langkah berikut.
1. Inisialisasi dan partisi disk data dengan mengacu pada [Menginisialisasi Disk Cloud (Lebih Kecil dari 2 TB)](https://intl.cloud.tencent.com/document/product/362/31597). Jalankan perintah berikut untuk melihat disk yang ada dan partisi yang tersedia.
```
fdisk -l
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/34abb1b0c7a1f6fb4ff233a42a781123.png)
2. Jalankan perintah berikut secara berurutan untuk membuat titik pemasangan dan memasang partisi. Dokumen ini menggunakan pemasangan partisi `/dev/vdb1` ke `/test` sebagai contoh.
```
mkdir /test
```
```
mount /dev/vdb1 /test
```
3. Jalankan perintah berikut secara berurutan untuk membuat file pengujian “hello” di titik pemasangan.
```
cd /test
```
```
echo test > hello
```
4. <span id="Step4"></span>Jalankan perintah berikut untuk merekam nilai MD5 dari file “hello”. Nilai ini dapat digunakan untuk membandingkan file asli dan yang dipulihkan.
```
md5sum hello
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/230d4c9a4456df8b3623c0bd401d878a.png)
5. Jalankan perintah berikut secara berurutan untuk menghapus file “hello”.
```
rm -rf hello
```
```
cd ~
```
```
fuser -k /test
```
6. Jalankan perintah berikut untuk membongkar partisi.
```
umount /dev/vdb1
```
7. Jalankan perintah berikut untuk mencari partisi untuk file yang terhapus secara tidak sengaja.
```
extundelete --inode 2 /dev/vdb1
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/97a64a2e0de658f4ed55500f162b1eb7.png)
8. Jalankan perintah berikut untuk menggunakan Extundelete untuk memulihkan file.
```
/usr/local/bin/extundelete  --restore-inode 12  /dev/vdb1
```
Setelah file dipulihkan, Anda akan melihat folder `RECOVERED_FILES` di direktori level yang sama.
9. Akses folder `RECOVERED_FILES`, periksa file yang dipulihkan, dan jalankan perintah berikut untuk mendapatkan nilai MD5-nya.
```
md5sum Recovered file
```
Jika nilai MD5 yang diperoleh sama dengan nilai file “hello” yang direkam di [Langkah 4](#Step4), data telah berhasil dipulihkan.
