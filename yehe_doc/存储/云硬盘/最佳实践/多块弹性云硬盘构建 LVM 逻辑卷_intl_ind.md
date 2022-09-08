## Pengantar LVM
Logical Volume Manager (Pengelola Volume Logis/LVM) menciptakan lapisan logis di atas disk atau partisi Anda untuk membaginya menjadi unit physical extent (batas fisik/PE) dengan ukuran yang sama.Ini mengategorikan disk atau partisi ke dalam volume group (kelompok volume/VG), tempat Anda dapat membuat logical volume (volume logis/LV), kemudian membuat sistem file di LV.
LVM berbeda dari pembuatan partisi disk langsung karena memungkinkan penskalaan sistem file yang elastis.
- Sistem file tidak dibatasi oleh ukuran fisik disk.Justru, sistem file dapat didistribusikan di antara beberapa disk:
Misalnya, Anda dapat membeli tiga buah disk cloud elastis berukuran 4-TB dan menggunakan LVM untuk membuat sistem file besar-besaran berukuran 12 TB.
- Anda dapat mengubah ukuran LV secara dinamis alih-alih mempartisi ulang disk.
Jika kapasitas VG LVM Anda tidak memenuhi kebutuhan, Anda dapat membeli disk cloud elastis, memasangkannya ke instance CVM, kemudian menambahkannya ke VG LVM untuk meningkatkan kapasitasnya.

## Membuat LVM
<dx-alert infotype="explain" title="">
Contoh berikut menggunakan tiga disk cloud elastis untuk membuat sistem file yang dapat diubah ukurannya secara dinamis melalui LVM.

![](https://main.qcloudimg.com/raw/81086e80477ff7e374e7c3f0fe9d2788.png)
</dx-alert>

### Langkah 1: buatlah physical volume (volume fisik/PV)
1.[Masuk ke instance CVM Linux](https://intl.cloud.tencent.com/document/product/213/5436) sebagai pengguna root.
2.Jalankan perintah berikut untuk membuat PV.

```plaintext
pvcreate <disk path 1> ... <disk path N>
​``` 
Sebagai contoh, buatlah PV menggunakan disk `/dev/vdc`, `/dev/vdd` dan `/dev/vde` dengan menjalankan perintah berikut.
​```plaintext
pvcreate /dev/vdc /dev/vdd /dev/vde
​``` 
Pembuatan yang berhasil akan tampak seperti gambar berikut:
![](https://main.qcloudimg.com/raw/5b92a6c7878e22906599af48bfa09d95.png)

3.Jalankan perintah berikut untuk melihat volume fisik sistem.
​```plaintext
lvmdiskscan | grep LVM
​``` 
![](https://main.qcloudimg.com/raw/1de75af4a49c2deea689a2576eb075d9.png)

### Langkah 2: buatlah volume group (kelompok volume/VG)
1.Jalankan perintah berikut untuk membuat VG.
​```plaintext
vgcreate [-s <specified PE size> (ukuran PE yang dipilih)] <VG name> (nama VG) <PV path> (path PV).
​``` 
Sebagai contoh, buatlah VG dengan nama `lvm_demo0` dengan menjalankan perintah berikut:
​```plaintext
vgcreate lvm_demo0 /dev/vdc /dev/vdd
​``` 
Pembuatan yang berhasil akan tampak seperti gambar berikut:
![](https://main.qcloudimg.com/raw/3b8dba3329f62e85d2075fad10898632.png)
Jika muncul tulisan **Volume group" (kelompok volume) <VG name> (nama VG) "successfully created** (berhasil dibuat), itu artinya VG telah dibuat.
- Anda kemudian dapat menjalankan perintah berikut untuk menambahkan PV baru ke VG.
​```plaintext
vgextend [VG name] [Path of the new PV]
​``` 
Penambahan PV yang berhasil akan tampak seperti gambar berikut:
![](https://main.qcloudimg.com/raw/105e5a77472f173ffd4a58624f20a863.png)
- Setelah VG dibuat, Anda dapat menjalankan `vgs`, `vgdisplay` atau perintah lain untuk menanyakan informasi tentang VG sistem, seperti yang terlihat di bawah ini:
![](https://main.qcloudimg.com/raw/309c991d32cf4b801ddbe8d898f1bfbb.png)

### Langkah 3: buatlah logical volume (volume logis/LV)
1.Jalankan perintah berikut untuk membuat LV.
​```plaintext
lvcreate [-L <LV size>][-n <LV name>] <VG name>.
​``` 
Sebagai contoh, buatlah volume logis 8 GB dengan nama `lv_0` dengan menjalankan perintah berikut:
​```plaintext
lvcreate -L 8G -n lv_0 lvm_demo0
​``` 
Pembuatan yang berhasil akan tampak seperti gambar berikut:
![](https://main.qcloudimg.com/raw/ed6d2f827ae7c4a4630bf17e24d90df2.png)

<dx-alert infotype="explain" title="">
Jalankan perintah `pvs`.Anda dapat melihat bahwa hanya kapasitas disk `/dev/vdc` yang dikurangi sebesar 8 GB, seperti yang terlihat di bawah ini:
![](https://main.qcloudimg.com/raw/2718d08f7c74b7b469a23473a1398dfe.png)
</dx-alert>

### Langkah 4: buat dan pasangkan sistem file
1.Jalankan perintah berikut untuk membuat sistem file pada LV yang ada.
​```plaintext
mkfs.ext3 /dev/lvm_demo0/lv_0
```
2.Jalankan perintah berikut untuk membuat `/vg0` titik pemasangan.
```plaintext
mkdir /vg0
```
3.Jalankan perintah berikut untuk memasang sistem file.
```plaintext
mount /dev/lvm_demo0/lv_0 /vg0
​``` 
Pemasangan yang berhasil akan tampak seperti gambar berikut:
![](https://main.qcloudimg.com/raw/34af8440192a1fa74f85ea44b6354194.png)

### Langkah 5: ubah ukuran volume logis dan sistem file secara dinamis

<dx-alert infotype="notice" title="">
LV dapat diperluas secara dinamis hanya jika kapasitas VG tidak habis digunakan.Setelah meningkatkan kapasitas LV, Anda perlu memperluas sistem file yang dibuat pada LV ini.
</dx-alert>

1.Jalankan perintah berikut untuk memperluas LV.
​```plaintext
lvextend [-L +/- <scale capacity> (kapasitas skala)] <LV path> (path LV)
​``` 
Sebagai contoh, perluas LV dengan nama `lv_0` sebesar 4 GB dengan menjalankan perintah berikut:
​```plaintext
lvextend -L +4G /dev/lvm_demo0/lv_0
​``` 
Perluasan yang berhasil akan tampak seperti gambar berikut:
![](https://main.qcloudimg.com/raw/eccd7d6aec587eb90ec655a384367595.png)

<dx-alert infotype="explain" title="">
Jalankan perintah `pvs`.Anda akan melihat bahwa kapasitas disk `/dev/vdc` telah habis digunakan dan kapasitas disk `/dev/vdd` telah digunakan sebesar 2 GB, seperti yang terlihat di bawah ini:

![](https://main.qcloudimg.com/raw/189155ca377ef9550c4587ca78ab5b27.png)
</dx-alert>

2.Jalankan perintah berikut untuk memperluas sistem file.
​```plaintext
resize2fs /dev/lvm_demo0/lv_0
​``` 
Perluasan yang berhasil akan tampak seperti gambar berikut:
![](https://main.qcloudimg.com/raw/2e37f35678014ab1ca398fe5470a754b.png)
Setelah perluasan, jalankan perintah berikut untuk memeriksa apakah kapasitas LV-nya sebesar 12 GB.
​```plaintext
df -h
```




