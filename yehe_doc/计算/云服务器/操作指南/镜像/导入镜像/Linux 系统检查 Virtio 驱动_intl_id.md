## Pengantar
Untuk menjalankan di Tencent Cloud, CVM harus memiliki kernel yang mendukung driver virtio, termasuk driver perangkat blok `virtio_blk` dan driver NIC `virtio_net`. Untuk memastikan CVM yang dibuat dengan citra kustom dapat dimulai dengan benar, harap periksa apakah citra Anda mendukung driver virtio di server sumber sebelum mengimpor citra. Dokumen ini menggunakan CentOS sebagai contoh untuk menjelaskan cara memeriksa apakah citra mendukung driver virtio.

## Petunjuk

<span id="CheckVirtioForKernel"></span>
### Langkah 1: Periksa apakah kernel mendukung driver virtio
Jalankan perintah berikut untuk memeriksa apakah kernel saat ini mendukung driver virtio:
```
grep -i virtio /boot/config-$(uname -r)
```
Respons yang mirip dengan berikut ini akan ditampilkan:
![](https://main.qcloudimg.com/raw/8c32c3dd554700a0c17ff0c7e5675090.png)
 - Jika nilai `CONFIG_VIRTIO_BLK` dan `CONFIG_VIRTIO_NET` adalah `m` dalam respons, harap lanjutkan ke [Langkah 2](#CheckVirtioForInitramfs).
 - Jika nilai `CONFIG_VIRTIO_BLK` dan `CONFIG_VIRTIO_NET` adalah `y` dalam respons, yang berarti OS berisi driver virtio, Anda dapat mengimpor citra kustom ke Tencent Cloud. Untuk mengetahui detailnya, lihat [Impor Citra > Ikhtisar](https://intl.cloud.tencent.com/document/product/213/4945).
 - Jika Anda tidak dapat menemukan `CONFIG_VIRTIO_BLK` dan `CONFIG_VIRTIO_NET` dalam respons, artinya citra dengan OS **cannot** (tidak dapat) diimpor ke Tencent Cloud. Harap [unduh dan kompilasi kernel](#DownloadCompileKernel).

<span id="CheckVirtioForInitramfs"></span>
### Langkah 2: Periksa apakah driver virtio ada di sistem file sementara
Jika nilai parameternya adalah `m` di [Langkah 1](#CheckVirtioForKernel), Anda perlu memeriksa apakah `initramfs` atau `initrd` berisi driver `virtio`. Harap jalankan perintah yang sesuai berdasarkan pada sistem operasi:
- Untuk CentOS 6/CentOS 7/CentOS 8/RedHat 6/RedHat 7:
```
lsinitrd /boot/initramfs-$(uname -r).img | grep virtio
```
- Untuk RedHat 5/CentOS 5:
```
mkdir -p /tmp/initrd && cd /tmp/initrd
zcat /boot/initrd-$(uname -r).img | cpio -idmv
find . -name "virtio*"
```
- Untuk Debian/Ubuntu:
```
lsinitramfs /boot/initrd.img-$(uname -r) | grep virtio
```

Jika hasilnya mirip dengan berikut ini ditampilkan:
<img src="https://main.qcloudimg.com/raw/a5e22f75f48ce26a6b03f65588a52877.png" />
Artinya <code>initramfs</code> berisi driver <code>virtio_blk</code> dan <code>virtio.ko</code>, <code>virtio_pci.ko</code>, dan <code>virtio_ring.ko</code> yang digunakan oleh driver. Dalam hal ini, Anda dapat mengimpor citra kustom ke Tencent Cloud. Untuk detailnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/4945">Impor Citra > Ikhtisar</a>.
Jika <code>initramfs</code> atau <code>initrd</code> tidak berisi driver <code>virtio</code>, harap lanjutkan ke [Langkah 3](#ReconfigureInitramfs).

<span id="ReconfigureInitramfs"></span>
### Langkah 3: Konfigurasi ulang sistem file sementara
Jika Anda menemukan bahwa `initramfs` atau `initrd` tidak berisi driver `virtio` di [Langkah 2]](#CheckVirtioForInitramfs), Anda perlu mengonfigurasi ulang sistem file sementara untuk memastikan bahwa `initramfs` atau `initrd` berisi driver `virtio`. Harap jalankan perintah yang sesuai berdasarkan pada sistem operasi:
 - Untuk CentOS 6/CentOS 7/RedHat 6/RedHat 7:
```
cp /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r).img.bak
mkinitrd -f --with=virtio_blk --with=virtio_pci /boot/initramfs-$(uname -r).img $(uname -r)
```
 - Untuk RedHat 5/CentOS 5:
```
cp /boot/initrd-$(uname -r).img /boot/initrd-$(uname -r).img.bak
mkinitrd -f --with=virtio_blk --with=virtio_pci /boot/initrd-$(uname -r).img $(uname -r)
```
 - Untuk Debian/Ubuntu:
```
echo -e "virtio_pci\nvirtio_blk" >> /etc/initramfs-tools/modules
update-initramfs  -u
```

## Lampiran
<span id="DownloadCompileKernel"></span>
### Mengunduh dan mengompilasi kernel

#### Mengunduh paket penginstalan kernel
1. Jalankan perintah berikut untuk menginstal komponen yang diperlukan untuk kompilasi kernel.
```
yum install -y ncurses-devel gcc make wget
```
2. Jalankan perintah berikut untuk melihat versi kernel saat ini.
```
uname -r
```
Respons yang mirip dengan berikut ini akan ditampilkan, menunjukkan versi kernel saat ini adalah 2.6.32-642.6.2.el6.x86_64.
![](https://main.qcloudimg.com/raw/739b19fc7af96d6de7872df0a498b7b6.png)
2. Masuk ke [Halaman Unduh Kernel Linux](https://www.kernel.org/pub/linux/kernel/?spm=a2c4g.11186623.2.26.7e4179b4zo5WVJ) untuk mengunduh kode sumber dari versi kernel yang sesuai.
Misalnya, untuk versi `2.6.32-642.6.2.el6.x86_64`, Anda harus mengunduh `linux-2.6.32.tar.gz` di `https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz`.
4. Jalankan perintah berikut untuk berpindah direktori.
```
cd /usr/src/
```
5. Jalankan perintah berikut untuk mengunduh paket penginstalan.
```
wget https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz
```
6. Jalankan perintah berikut untuk mendekompresi paket penginstalan.
```
tar -xzf linux-2.6.32.tar.gz
```
7. Jalankan perintah berikut untuk membuat koneksi.
```
ln -s linux-2.6.32 linux
```
8. Jalankan perintah berikut untuk berpindah direktori.
```
cd /usr/src/linux
```

#### Mengompilasi kernel

1. Jalankan perintah berikut untuk mengompilasi kernel.
```
make mrproper
cp /boot/config-$(uname -r) ./.config
make menuconfig
```
Masukkan antarmuka “Linux Kernel vX.X.XX Configuration” (Konfigurasi vX.X.XX Kernel Linux) seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/72c3bea10627aaef022f1a72b72ac79a.png)
>? Jika Anda tidak diarahkan ke antarmuka "Linux Kernel vX.X.XX Configuration" (Konfigurasi vX.X.XX Kernel Linux), harap buka [Langkah 18](# OptionalStep).
> Antarmuka “Konfigurasi vX.X.XX Kernel Linux”:
> - Tekan “Tab” atau “↑” “↓” untuk menggerakkan kursor.
> - Tekan “Enter” untuk memilih atau menjalankan item yang dipilih oleh kursor.
> - Tekan bilah spasi untuk memilih item yang dipilih oleh kursor. “\*” berarti kompilasi ke kernel, dan "M" berarti kompilasi ke modul. 
> 
2. Tekan tombol "↓" untuk memindahkan kursor ke "Virtualization" (Virtualisasi) dan tekan spasi untuk memilih "Virtualization" (Virtualisasi).
3. Tekan "Enter" untuk masuk ke antarmuka detail Virtualisasi.
4. Di antarmuka detail Virtualisasi, periksa apakah opsi dukungan Mesin Virtual (KVM) berbasis Kernel dipilih seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/d5614d31ebaed0f0b270dc1046b9ff2e.png)
Jika tidak dipilih, tekan bilah spasi untuk memilih opsi “Kernel-based Virtual Machine (KVM) support” (Dukungan Mesin Virtual Berbasis Kernel (KVM)).
5. Tekan "Esc" untuk kembali ke antarmuka utama "Linux Kernel vX.X.XX Configuration" (Konfigurasi vX.X.XX Kernel Linux).
6. Tekan tombol "↓" untuk memindahkan kursor ke "Processor type and features" (Jenis dan fitur prosesor) dan tekan "Enter" untuk masuk ke antarmuka detail jenis dan fitur prosesor.
7. Tekan tombol "↓" untuk memindahkan kursor ke "Paravirtualized guest support" (Dukungan tamu Paravirtualisasi) dan tekan "Enter" untuk masuk ke antarmuka detail dukungan tamu Paravirtualisasi.
8. Di antarmuka detail dukungan tamu Paravirtualisasi, periksa apakah "KVM paravirtualized clock" (Jam paravirtualisasi KVM) dan "KVM Guest support" (Dukungan Tamu KVM) dipilih seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/2e49f9b46ecb9f9d272db36dffbade07.png)
Jika tidak dipilih, tekan bilah spasi untuk memilih opsi "KVM paravirtualized clock" (Jam paravirtualisasi KVM) dan "KVM Guest support" (Dukungan Tamu KVM).
9. Tekan "Esc" untuk kembali ke antarmuka utama "Linux Kernel vX.X.XX Configuration" (Konfigurasi vX.X.XX Kernel Linux).
10. Tekan tombol "↓" untuk memindahkan kursor ke "Device Drivers" (Driver Perangkat) dan tekan "Enter" untuk masuk ke antarmuka detail Driver Perangkat.
11. Tekan tombol "↓" untuk memindahkan kursor ke "Block devices" (Perangkat pemblokiran) dan tekan "Enter" untuk masuk ke antarmuka detail Perangkat pemblokiran.
12. Di antarmuka detail Perangkat pemblokiran, periksa apakah "Virtio block driver (EXPERIMENTAL)" (Driver pemblokiran Virtio (EKSPERIMENTAL)) dipilih seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/79f3e29a6d77224a164c6c716e41fa84.png)
Jika tidak dipilih, tekan spasi untuk memilih opsi "Virtio block driver (EXPERIMENTAL)" (Driver pemblokiran Virtio (EKSPERIMENTAL)).
13. Tekan "Esc" untuk kembali ke antarmuka detail Driver Perangkat.
14. Tekan tombol "↓" untuk memindahkan kursor ke "Network device support" (Dukungan perangkat jaringan) dan tekan "Enter" untuk masuk ke antarmuka detail dukungan perangkat Jaringan.
15. Di antarmuka detail dukungan perangkat Jaringan, periksa apakah "Virtio network driver (EXPERIMENTAL)" (Driver jaringan Virtio (EKSPERIMENTAL)) dipilih seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/811388c89393882ea83bceb7a00bc1b7.png)
Jika tidak dipilih, tekan spasi untuk memilih opsi "Virtio network driver (EXPERIMENTAL)" (Driver jaringan Virtio (EKSPERIMENTAL)).
16. Tekan "Esc" untuk keluar dari antarmuka konfigurasi kernel, dan pilih "YES" (YA) untuk menyimpan file `.config`.
17. Lakukan [Langkah 1: Periksa apakah kernel mendukung driver virtio](#CheckVirtioForKernel) untuk memverifikasi apakah driver virtio telah dikonfigurasi dengan benar.
18. <span id = "OptionalStep"></span> (Opsional) Jalankan perintah berikut untuk mengedit file `.config` secara manual.
>? Langkah ini disarankan jika salah satu dari dua hal berikut ini benar:
> - Kernel masih tidak berisi informasi konfigurasi yang terkait dengan driver virtio setelah Anda selesai memeriksanya.
> - Saat mengompilasi kernel, Anda tidak dapat masuk ke antarmuka konfigurasi kernel atau menyimpan file `.config`.
> 
```
make oldconfig
make prepare
make scripts
make
make install
```
19. Jalankan perintah berikut untuk memeriksa penginstalan driver virtio.
```
find /lib/modules/"$(uname -r)"/ -name "virtio.*" | grep -E "virtio.*"
grep -E "virtio.*" < /lib/modules/"$(uname -r)"/modules.builtin
```
Jika salah satu perintah menampilkan daftar file seperti `virtio_blk`,` virtio_pci.virtio_console`, artinya Anda telah menginstal driver virtio dengan benar.





