Anda dapat menggunakan disk cloud elastis sebagai disk data dan memasangnya ke CVM mana pun di zona ketersediaan yang sama.Setiap CVM dapat memiliki hingga 20 disk data yang terpasang padanya.Anda dapat menggunakan metode berikut untuk memasang disk cloud.
- Saat meluncurkan CVM baru, tentukan image khusus dan snapshot disk data yang sesuai.
Setelah pemasangan otomatis, membaca dan menulis pada disk data dapat langsung dilakukan tanpa operasi inisialisasi disk seperti mempartisi dan memformat.
- Saat membeli disk cloud elastis, pasang disk secara manual ke instance CVM yang ada di zona ketersediaan yang sama melalui konsol atau API.
- Membuat disk cloud secara langsung
Setelah pemasangan manual, Anda perlu menginisialisasi disk cloud dengan memformat dan mempartisinya.Untuk informasi selengkapnya, lihat [Menginisialisasi Disk Cloud (Lebih Kecil dari 2 TB)](https://intl.cloud.tencent.com/document/product/362/31597) atau [Menginisialisasi Disk Cloud (Lebih besar dari 2 TB)](https://intl.cloud.tencent.com/document/product/362/31598).
- Membuat disk cloud dari snapshot
Jika kapasitas disk cloud sama dengan ukuran snapshot, Anda dapat langsung membaca dan menulis di disk cloud tanpa operasi inisialisasi disk seperti mempartisi dan memformat.
Jika kapasitas disk cloud lebih besar dari ukuran snapshot, Anda perlu memperluas sistem file atau mengonversi format partisi.

>?Beberapa CVM Linux mungkin tidak mengenali disk cloud elastis.Anda harus terlebih dahulu mengaktifkan fitur hot swapping disk di CVM.Untuk informasi lebih lanjut, lihat [Mengaktifkan fitur hot swapping disk](#modprobeacpiphp).

## Pemasangan Otomatis
### Memasang disk data (Windows)
Jika Anda menggunakan image khusus untuk membuat instance CVM Windows, disk cloud yang dibuat dari snapshot disk data yang sesuai akan dipasang secara otomatis.Image khusus dan snapshot disk data harus memenuhi persyaratan berikut:
- Disk data **harus** diformat ke `ntfs` atau `fat32` sebelum Anda membuat snapshot.
- Kebijakan SAN dalam image khusus adalah `onlineAll`.
>?Tencent Cloud menyediakan image publik yang telah dikonfigurasi sebelumnya untuk Windows secara default, tetapi kami tetap menyarankan Anda untuk melakukan langkah-langkah berikut untuk memeriksa konfigurasi sebelum membuat image khusus.
![](https://main.qcloudimg.com/raw/edac7337395de380c0ec801646e0a627.png)


### Memasang disk data (Linux)
Jika Anda menggunakan image khusus untuk membuat instance CVM Linux, disk cloud yang dibuat dari snapshot disk data yang sesuai akan dipasang secara otomatis.Image khusus dan snapshot disk data harus memenuhi persyaratan berikut:
- Disk data **harus** diformat dan berhasil dipasang ke CVM sumber sebelum snapshot dibuat.
- Tambahkan perintah berikut ke file `/etc/rc.local` untuk mengonfigurasi titik pemasangan disk data sebelum membuat disk sistem pada disk sistem.
 ```
mkdir -p <mount-point>
mount <device-id> <mount-point>
 ```
>?
> - Ganti `<mount-point>` dengan titik pemasangan sistem file, seperti `/mydata`.
> - Ganti `<device-id>` dengan jalur partisi sistem file.Misalnya, masukkan `/dev/vdb` jika sistem file tidak memiliki partisi, dan `/dev/vdb1` jika sistem file memiliki partisi.

## Pemasangan Secara Manual

### Menggunakan konsol untuk memasang disk cloud
1.Masuk ke [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
2.Pada halaman daftar disk cloud, Anda dapat menggunakan metode berikut untuk memasang disk cloud.
a.Pilih disk cloud yang **to be mounted** (akan dipasang), dan klik **More** > **Mount** (Selengkapnya > Pasang) di bawah kolom **Operation** (Operasi).
b.Pilih beberapa disk cloud yang **to be mounted** (akan dipasang), dan klik **Mount** (Pasang) di bagian atas daftar disk cloud.
3.Di kotak pop-up, pilih instance CVM target dan klik **OK**.
4.Segarkan daftar disk cloud.
Jika status disk cloud ini berubah menjadi **Mounted** (Dipasang), ini menunjukkan bahwa pemasangan berhasil.
5.Lakukan operasi berikutnya seperti yang ditunjukkan di bawah ini untuk membuat disk cloud dapat digunakan.
<table>
<tr>
<th>Mode pembuatan</th>
<th>Kapasitas disk cloud</th>
<th>Operasi berikutnya</th>
</tr>
<tr>
<td  rowspan="2">Buat langsung</td>
<td>Kapasitas disk cloud < 2TB</td>
<td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Menginisialisasi disk cloud (< 2 TB)</a></td>
</tr>
<tr>
<td>Kapasitas disk cloud ≥ 2 TB</td>
<td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Menginisialisasi disk cloud (≥ 2 TB)</a></td>
</tr>
<tr>
<td  rowspan="3">Buat dari snapshot</td>
<td>Kapasitas disk cloud = Kapasitas snapshot</td>
<td><ul><li>Memasang ke CVM Windows: setelah masuk ke instance, buat disk online melalui **Server Management** > **Storage** > **Disk Management** (Manajemen Server > Penyimpanan > Manajemen Disk).</li>
<li>Memasang ke CVM Linux: setelah masuk ke instance, jalankan perintah <code>mount <disk partition> <mount point></code>, misalnya <code>mount /dev/vdb /mnt</code>.</li>
</ul>
</li></td>
</tr>
</tr>
<tr>
<td nowrap="nowrap">Kapasitas snapshot < kapasitas disk cloud ≤ 2 TB <br/>atau<br/>2 TB < kapasitas snapshot < kapasitas disk cloud</td>
<td><ul><li>Memasang ke CVM Windows: <a href="https://intl.cloud.tencent.com/document/product/362/31601">memperluas partisi dan sistem file (Windows)</a></li><li>Memasang ke CVM Linux: <a href="https://intl.cloud.tencent.com/document/product/362/31602">memperluas partisi dan sistem file (Linux)</a></li></ul></td>
</tr>
<tr>
<td>Kapasitas snapshot ≤ 2 TB < kapasitas disk cloud</td>
<td nowrap="nowrap"><ul><li>Jika snapshot menggunakan format partisi MBR:</li>lihat <a href="https://intl.cloud.tencent.com/document/product/362/31598">Menginisialisasi Disk Cloud (Lebih Besar dari 2 TB)</a> untuk menggunakan partisi GPT.<b>Operasi ini akan menghapus data asli.</b><li>Jika snapshot menggunakan format partisi GPT:<ul><li>Memasang ke CVM Windows:<a href="https://intl.cloud.tencent.com/document/product/362/31601">memperluas partisi dan sistem file (Windows)</a></li><li>Memasang ke CVM Linux:<a href="https://intl.cloud.tencent.com/document/product/362/31602">memperluas partisi dan sistem file (Linux)</a></li></ul></td>
</tr>
</table>

### Menggunakan API untuk memasang disk cloud
Anda dapat menggunakan API `AttachDisks` untuk memasang disk cloud.Untuk informasi selengkapnya, lihat [AttachDisks](https://intl.cloud.tencent.com/document/product/362/16313).

[](id:modprobeacpiphp)
### Mengaktifkan fitur hot swapping disk
Semua image yang ada sudah mendukung pemasangan dan pelepasan disk cloud elastis.**Untuk melepas disk cloud, Anda harus terlebih dahulu menjalankan perintah `umount` di CVM Linux atau melakukan operasi offline di CVM Windows.Jika tidak, disk cloud elastis yang dipasang kembali mungkin tidak dikenali.**
Namun, jika Anda ingin memasang disk cloud elastis ke CVM dengan sistem operasi berikut, kami sarankan Anda menambahkan driver terlebih dahulu dan mengaktifkan fitur hot swapping di CVM.
<table>
<tbody>
<tr><th>Sistem operasi CVM</th><th>Versi</th>
<tr><td rowspan="4">CentOS</td><td>5.11 64-bit</td>
<tr><td>5.11 32-bit</td>
<tr><td>5.8 64-bit</td>
<tr><td>5.8 32-bit</td>
<tr><td >Debian</td><td>6.0.3 32-bit</td>
<tr><td rowspan="2">Ubuntu</td><td>10.04 64-bit</td>
<tr><td>10.04 32-bit</td>
<tr><td rowspan="2">openSUSE</td><td>12.3 64-bit</td>
<tr><td>12.3 32-bit</td>
</tbody>
</table>

1.[Masuk ke CVM Linux](https://intl.cloud.tencent.com/document/product/213/5436) sebagai pengguna root.
2.Jalankan perintah berikut untuk menambahkan driver.
```
modprobe acpiphp
```
>?Jika Anda masih perlu memuat modul `acpiphp` setelah mematikan atau memulai kembali CVM, kami sarankan Anda menjalankan [Langkah 3](#step3) untuk mengatur modul `acpiphp` ke pemuatan otomatis.
<span id="step3"></span>
3.(Opsional) Jalankan perintah berikut sesuai dengan sistem operasi untuk mengatur modul `acpiphp` ke pemuatan otomatis:
- **Seri CentOS 5**
a.Jalankan perintah berikut untuk membuat dan membuka file `acpiphp.modules`.
```
vi /etc/sysconfig/modules/acpiphp.modules
```
b.Tambahkan konten berikut ke file, dan simpan.
```
#!/bin/bash
modprobe acpiphp >& /dev/null
```
c.Jalankan perintah berikut untuk memberikan izin eksekusi pada file.
```
chmod a+x /etc/sysconfig/modules/acpiphp.modules
```
- **Seri Debian 6, Seri Ubuntu 10.04**
a.Jalankan perintah berikut untuk memodifikasi file.
```
vi /etc/modules
```
b.Tambahkan konten berikut ke file, dan simpan.
```
acpiphp
```
- **Seri openSUSE 12.3**
a.Jalankan perintah berikut untuk memodifikasi file.
```
vi /etc/sysconfig/kernel
```
b.Tambahkan konten berikut ke file, dan simpan.
```
MODULES_LOADED_ON_BOOT="acpiphp"
```
