## Ikhtisar
Memperluas disk data melalui konsol hanya menambah ruang penyimpanannya.Anda perlu memperluas partisi atau sistem file disk cloud ke ukuran yang lebih besar.Dokumen ini menjelaskan cara memperluas partisi dan sistem file secara online.

## Prasyarat
- Sebelum memperluas partisi atau sistem file, buat snapshot dari disk cloud untuk mencadangkan data.Untuk informasi selengkapnya, lihat [Membuat Snapshot](https://intl.cloud.tencent.com/document/product/362/5755).
Praktik ini membantu Anda mengembalikan snapshot untuk memulihkan data jika terjadi kehilangan data karena kesalahan pengoperasian.
- Disk cloud telah diperluas dan dipasang ke CVM melalui konsol.Untuk informasi selengkapnya, lihat [Memperluas Kapasitas Disk Cloud](https://intl.cloud.tencent.com/document/product/362/5747).
- Kernel CVM Linux harus menggunakan versi 3.6.0 atau yang lebih baru.Anda dapat menggunakan perintah `uname -a` untuk memeriksa versi kernel.
Jika versi kernel lebih lama dari 3.6.0, lihat [Memperluas Partisi dan Sistem File (Linux)](https://intl.cloud.tencent.com/document/product/362/39995).

## Lingkungan Pengoperasian
<table>
<tr>
<th>Sumber Daya</th><th>Deskripsi</th>
</tr>
<tr>
<td>Sistem operasi</td>
<td>CentOS 8.0 64-bit</td>
</tr>
<tr>
<td>Cloud disk</td>
<td>
<ul style="margin-bottom:0px">
<li><code>/dev/vdb</code>: menggunakan partisi MBR dan sistem file EXT4, dan memperluas dari 50 GB menjadi 60 GB melalui konsol.</li>
<li><code>/dev/vdc</code>: menggunakan partisi GPT dan sistem file XFS, dan memperluas dari 50 GB menjadi 60 GB melalui konsol.</li>
</ul>
</td>
</tr>
</table>

## Petunjuk
### Melihat partisi disk cloud
1.[Masuk ke instance Linux menggunakan metode masuk standar](https://intl.cloud.tencent.com/document/product/213/5436).
2.Jalankan perintah berikut untuk mengueri partisi disk cloud.
```
fdisk -l
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/19d4f0ab6be5e332022efe9247069f35.png)
Seperti yang ditunjukkan pada gambar,
- Disk data `/dev/vdb` 60 GB berisi partisi MBR 50 GB `/dev/vdb1`.
- Disk data `/dev/vdc` 60 GB berisi partisi GPT 50 GB `/dev/vdc1`.
3. [](id:Step3)Jalankan perintah berikut untuk menentukan jenis sistem file dari partisi yang ada.
```
df -TH
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/384bd9556f09e973504ab93dbb6aa900.png)
Seperti yang ditunjukkan pada gambar,
- Partisi `/dev/vdb1` berada pada sistem file EXT4 yang telah dipasang ke `/mnt/disk1`.
- Partisi `/dev/vdc1` berada pada sistem file EXT4 yang telah dipasang ke `/mnt/disk2`.

### Memperluas partisi
1.Gunakan perintah sesuai kebutuhan untuk menginstal alat gdisk.
- Untuk partisi MBR, lewati langkah ini.
- Untuk partisi GPT, jalankan perintah berikut sesuai dengan sistem operasi CVM.

<dx-tabs>
::: CentOS
```
yum install gdisk -y
```
:::

::: Ubuntu\satau\sDebian
```
apt-get install gdisk -y
```
:::
</dx-tabs>
2.Jalankan perintah berikut untuk menginstal alat growpart sesuai dengan sistem operasi CVM.
<dx-tabs>
::: CentOS
```
yum install -y cloud-utils-growpart
```
:::
::: Ubuntu\satau\sDebian
```
apt-get install -y cloud-guest-utils
```
:::
</dx-tabs>

3.Jalankan perintah berikut untuk memperluas partisi menggunakan growpart.
Gunakan memperluas partisi `/dev/vdb1` sebagai contoh.Perhatikan bahwa ada spasi antara `/dev/vdb` dan `1` dalam perintah.Ganti dengan nilai aktual Anda.
```
growpart /dev/vdb 1
```
Jika informasi yang mirip dengan apa yang ditampilkan di bawah ini dikembalikan, partisi telah diperluas.
![](https://main.qcloudimg.com/raw/bc67dd4e8116510ea2cea5484529cdf1.png)

### Memperluas sistem file
1.Gunakan perintah khusus sistem file untuk mengubah ukuran sistem file berdasarkan jenis yang diperoleh di [langkah](#Step3).
<dx-tabs>
::: Memperluas\s\ssistem\sfile\sEXT

Jalankan perintah berikut untuk memperluas sistem file EXT.

```
resize2fs /dev/vdb1
```

Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/5bd3a9bba754bf21256e792860c6d799.png)
:::
::: Memperluas\s\ssistem\sfile\sXFS

Jalankan perintah berikut untuk memperluas sistem file XFS.

```
xfs_growfs <Mount point>
```

Gunakan memasang sistem file `/dev/vdc1` ke`/mnt/disk2` sebagai contoh, lalu jalankan perintah berikut:

```
xfs_growfs /mnt/disk2
```

Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/6e76842b419bb054c9cae9f96fa0250b.png)
:::
</dx-tabs>
2.Jalankan perintah berikut untuk melihat hasilnya.
```
df -TH
```
Jika informasi yang mirip dengan apa yang ditampilkan di bawah ini dikembalikan, sistem file telah diperluas.
![](https://main.qcloudimg.com/raw/45bc319770858880a6b3cf35505bce46.png)

3.Periksa integritas data dan status pengoperasian CVM setelah perluasan.
Anda dapat mengembalikan snapshot untuk memulihkan data jika ada pengecualian.Untuk informasi selengkapnya, lihat [Mengembalikan Snapshot](https://intl.cloud.tencent.com/document/product/362/5756).

