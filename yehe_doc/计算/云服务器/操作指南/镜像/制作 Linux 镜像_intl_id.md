## Ikhtisar

Dokumen ini menjelaskan cara membuat citra disk sistem dari server Linux lokal Anda atau server Linux yang digunakan pada platform cloud lainnya. 

## Petunjuk

### Persiapan

Sebelum menyiapkan dan mengekspor citra disk sistem, selesaikan pemeriksaan berikut.
>? Jika Anda perlu menyiapkan dan mengekspor citra disk data, lewati operasi ini.
>

#### Memeriksa mode partisi dan mulai OS
1. Jalankan perintah berikut untuk memeriksa apakah partisi OS adalah partisi GPT.
```
sudo parted -l /dev/sda | grep 'Partition Table'
```
 - Jika hasil yang ditampilkan adalah `msdos`, partisi MBR akan digunakan. Dalam hal ini, lanjutkan ke langkah selanjutnya.
 - Jika hasil yang ditampilkan adalah `gpt`, partisi GPT akan digunakan, yang saat ini tidak tersedia untuk migrasi layanan. Dalam hal ini, [kirim tiket](https://console.cloud.tencent.com/workorder/category).
2. Jalankan perintah berikut untuk memeriksa apakah OS dimulai dalam mode EFI.
```
sudo ls /sys/firmware/efi
```
 - Jika file EFI ada, sistem operasi dimulai dalam mode EFI. Dalam hal ini, [kirim tiket](https://console.cloud.tencent.com/workorder/category).
 - Jika tidak ada file, lanjutkan ke langkah selanjutnya.

#### Memeriksa file penting sistem
Periksa file penting sistem termasuk namun tidak terbatas pada hal berikut:
>? Ikuti standar distribusi untuk memastikan bahwa jalur dan izin file penting sistem sudah benar dan file dapat dibaca dan ditulis secara normal.
>
 - /etc/grub2.cfg: sebaiknya gunakan `uuid` dalam parameter `kernel` untuk memasang root. Metode lain (seperti `root=/dev/sda`) dapat menyebabkan kegagalan startup sistem.
 - /etc/fstab: tidak ada disk lain yang dipasang. Jika tidak, disk ini mungkin hilang dan menyebabkan kegagalan startup sistem setelah migrasi.
 - /etc/shadow: diberikan dengan izin baca-tulis.

#### Menghapus penginstalan perangkat lunak
Hapus penginstalan driver dan program perangkat lunak yang bertentangan (termasuk alat VMware, alat Xen, Virtualbox GuestAdditions, dan perangkat lunak lain yang disertakan dengan driver yang mendasarinya).

#### Memeriksa driver virtio
Untuk informasi selengkapnya, lihat [Memeriksa Driver Virtio di Linux](https://intl.cloud.tencent.com/document/product/213/9929).

#### Menginstal cloud-init
Untuk informasi selengkapnya, lihat [Menginstal Cloud-Init di Linux](https://intl.cloud.tencent.com/document/product/213/12587).

#### Memeriksa konfigurasi perangkat keras lainnya
Setelah migrasi ke cloud, perubahan perangkat keras termasuk namun tidak terbatas pada:
 - Kartu grafis berubah menjadi Cirrus VGA.
 - Disk berubah menjadi Virtio Disk. Nama perangkatnya adalah vda atau vdb.
 - ENI berubah menjadi Virtio Nic. Secara default, hanya eth0 yang tersedia.

### Mengkueri partisi dan ukurannya
Jalankan perintah berikut untuk mengkueri format partisi OS saat ini dan menentukan partisi yang akan disalin dan ukurannya.
```
pemasangan
```
Hasil yang mirip dengan berikut ini akan ditampilkan:
```
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
sys on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
dev on /dev type devtmpfs (rw,nosuid,relatime,size=4080220k,nr_inodes=1020055,mode=755)
run on /run type tmpfs (rw,nosuid,nodev,relatime,mode=755)
/dev/sda1 on / type ext4 (rw,relatime,data=ordered)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
cgroup on /sys/fs/cgroup/unified type cgroup2 (rw,nosuid,nodev,noexec,relatime,nsdelegate)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpu,cpuacct)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,rdma)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls,net_prio)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
systemd-1 on /home/libin/work_doc type autofs (rw,relatime,fd=33,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=12692)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=39,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=12709)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,pagesize=2M)
tmpfs on /tmp type tmpfs (rw,nosuid,nodev)
configfs on /sys/kernel/config type configfs (rw,relatime)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,size=817176k,mode=700,uid=1000,gid=100)
gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=1000,group_id=100)
```
Menurut hasilnya, partisi root berada di `/dev/sda1`. Tidak ada partisi independen yang berada di `/boot` atau `/home`. `sda1` berisi partisi boot, dan `mbr` tidak ada. Dengan demikian, kita hanya perlu menyalin seluruh `sda`.
<dx-alert infotype="notice">
Citra yang diekspor harus berisi setidaknya partisi root dan mbr. Jika mbr hilang, sistem operasi tidak dapat dimulai.
Jika `/boot` dan `/home` adalah partisi independen dalam sistem operasi saat ini, citra yang diekspor juga harus berisi partisi tersebut.
</dx-alert>

### Mengekspor citra
Pilih metode ekspor citra yang sesuai berdasarkan kebutuhan.


<dx-tabs>

<span id="Useplatform"></span>
::: Using\sa\splatform\stool\sto\sexport\san\simage
Untuk informasi selengkapnya tentang cara menggunakan alat ekspor citra dari platform virtualisasi, seperti VMWare vCenter Converter dan Citrix XenConvert, lihat dokumen untuk masing-masing platform.
<dx-alert infotype="explain">
Migrasi layanan Tencent Cloud mendukung citra dalam format qcow2, vhd, raw, dan vmdk.
</dx-alert>
:::
<span id="ExportImageForUsingCommand"></span>
::: Using\scommands\sto\sexport\san\simage
<dx-alert infotype="notice">Metode ini menimbulkan risiko yang lebih tinggi. Misalnya, metadata sistem file mungkin rusak saat I/O sibuk. Sebaiknya [periksa citra](#CheckMirror) untuk memastikan bahwa citra tersebut utuh dan benar setelah diekspor.
</dx-alert>

Anda dapat menggunakan perintah [qemu-img](#qemuimg) atau [dd](#dd) untuk mengekspor citra.
- **Use the `qemu-img` command** (Gunakan perintah` qemu-img`)<span id="qemuimg"></span>
 1. Jalankan perintah berikut untuk menginstal paket yang diperlukan. Dokumen ini menggunakan Debian sebagai contoh. Nama paket dapat berbeda-beda menurut distribusi, seperti `qemu-img` untuk CentOS.
```
apt-get install qemu-utils
```
 2. Jalankan perintah berikut untuk mengekspor `/dev/sda` ke `/mnt/sdb/test.qcow2`.
```
sudo qemu-img convert -f raw -O qcow2 /dev/sda /mnt/sdb/test.qcow2
```
Dalam perintah ini, `/mnt/sdb` menunjukkan disk baru yang dipasang atau penyimpanan jaringan lain.
Untuk mengonversi formatnya, ubah nilai parameter `-O` ke salah satu dari berikut ini:
<span id="-OParameterValue"></span>
<table>
	<tr><th>Nilai Parameter</th><th>Deskripsi</th></tr>
	<tr><td>qcow2</td><td>format qcow2</td></tr>
	<tr><td>vpc</td><td>format vhd</td></tr>
	<tr><td>vmdk</td><td>format vmdk</td></tr>
	<tr><td>raw</td><td>No format</td></tr>
</table>
- **Use the `dd` command** (Gunakan perintah `dd`)<span id="dd"></span>
Misalnya, jalankan perintah berikut untuk mengekspor citra dalam format mentah.
```
sudo dd if=/dev/sda of=/mnt/sdb/test.imag bs=1K count=$count
```
Parameter `count` menentukan jumlah partisi yang akan disalin, yang dapat ditanyakan dengan menjalankan perintah `fdisk`. Untuk menyalin semua partisi, abaikan `count`.
Misalnya, jalankan perintah berikut untuk melihat jumlah partisi `/dev/sda`.
```
fdisk -lu /dev/sda
```
Hasil yang mirip dengan berikut ini akan ditampilkan:
```
Disk /dev/sda: 1495.0 GB, 1494996746240 byte
255 utama, 63 sektor/track, 181756 silinder, total 2919915520 sektor
Unit = sektor 1 * 512 = 512 byte
Ukuran sektor (logis/fisik): 512 byte/4096 byte
Ukuran I/O (minimum/optimal): 4096 byte/4096 byte
Pengidentifikasi disk: 0x0008f290

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048    41945087    20971520   83  Linux
/dev/sda2        41945088    46123007     2088960   82  Linux swap / Solaris
/dev/sda3        46123008    88066047    20971520   83  Linux
/dev/sda4        88066048  2919910139  1415922046   8e  Linux LVM
```
Menurut hasil yang ditampilkan dari perintah `fdisk`, sda1 berakhir pada 41945087 \* 512 byte, jadi atur `count` ke 20481 MB.
<dx-alert infotype="explain">
Citra yang diekspor dengan menggunakan perintah `dd` dalam format mentah. Sebaiknya [konversi ke qcow2, vhd, atau format citra lainnya](#ImageFormatConversion).
</dx-alert>
:::
</dx-tabs>

<span id="ImageFormatConversion"></span>
### Mengonversi format citra
>? Saat ini, migrasi layanan Tencent Cloud mendukung citra dalam format qcow2, vpc, vmdk, dan mentah. Sebaiknya gunakan format citra terkompresi untuk mempersingkat waktu transmisi dan migrasi.
> 
Konversi format citra menggunakan perintah `qemu-img`.
Misalnya, jalankan perintah berikut untuk mengonversi citra dalam format mentah ke format qcow2.
```
sudo qemu-img convert -f raw -O qcow2 test.img test.qcow2
```
- `-f` adalah format file citra sumber.
- `-O` menunjukkan format citra tujuan. Untuk format yang didukung, lihat [Nilai Parameter `-O`](#-OPParameterValue).

<span id="CheckMirror"></span>
### Memeriksa citra
>? Sistem file citra yang Anda siapkan mungkin rusak karena Anda menyiapkan citra tanpa menghentikan layanan atau karena alasan lain. Dengan demikian, sebaiknya periksa citra setelah menyiapkannya.
>
Jika format citra didukung oleh platform saat ini, Anda dapat langsung membuka dan memeriksa sistem file citra. Misalnya, platform Windows mendukung citra VHD, platform Linux memungkinkan Anda menggunakan `qemu-nbd` untuk membuka citra QCOW2, dan platform Xen memungkinkan Anda membuka file VHD secara langsung. Dokumen ini menggunakan platform Linux sebagai contoh:
1. Jalankan perintah berikut secara berurutan untuk memeriksa apakah komponen nbd ada.
```
modprobe nbd
```
```
lsmod | grep nbd
```
Jika hasilnya mirip dengan berikut ini ditampilkan, artinya komponen nbd ada. Jika tidak ada yang ditampilkan, periksa apakah opsi kompilasi kernel `CONFIG_BLK_DEV_NBD` diaktifkan. Jika tidak, aktifkan atau ubah sistem sebelum mengompilasi kernel lagi.
![](https://main.qcloudimg.com/raw/190bd78d60c7340fb95210f60e126105.png)
2. Jalankan perintah berikut secara berurutan untuk memeriksa citra.
```
qemu-nbd -c /dev/nbd0 xxxx.qcow2
```
```
mount /dev/nbd0p1 /mnt
```
Setelah Anda menjalankan perintah `qemu-nbd`, `/dev/nbd0` akan memetakan ke `xxx.qcow2`, dan `/dev/nbd0p1` menunjukkan partisi pertama dari disk virtual. Jika nbd0p1 tidak ada atau pemasangan gagal, citra mungkin salah.
Anda juga dapat memulai CVM untuk memeriksa apakah file citra berfungsi sebelum mengunggah citra.


