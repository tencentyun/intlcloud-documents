## Ikhtisar
Bottleneck Bandwidth dan Round-trip propagation time (BBR) adalah algoritme kontrol kemacetan TCP yang dikembangkan oleh Google pada tahun 2016. Ini membantu meningkatkan throughput dan latensi koneksi TCP dari server Linux secara signifikan. Namun, mengaktifkan BBR memerlukan kernel Linux versi 4.10 atau yang lebih baru. Jika menggunakan versi yang lebih lama, Anda perlu meningkatkan kernel Anda. Dokumen ini memandu Anda melalui cara mengubah kernel secara manual dan mengaktifkan BBR di server Linux Anda.

## Petunjuk

### Memperbarui paket kernel
1. Jalankan perintah berikut untuk memeriksa versi kernel saat ini.
```
uname -r
```
2. Jalankan perintah berikut untuk memperbarui paket perangkat lunak.
```
yum update -y
```
3. Jalankan perintah berikut untuk mengimpor kunci publik ELRepo.
```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
```
4. Jalankan perintah berikut untuk menginstal repositori yum dari ELRepo.
```
yum install https://www.elrepo.org/elrepo-release-7.0-4.el7.elrepo.noarch.rpm
```


### Menginstal kernel baru
1. Jalankan perintah berikut untuk memeriksa paket kernel yang didukung di repositori ELRepo.
```
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
```
2. Jalankan perintah berikut untuk menginstal kernel stabil jalur utama terbaru.
```
yum --enablerepo=elrepo-kernel install kernel-ml
```

### Memodifikasi konfigurasi grub
1. Jalankan perintah berikut untuk membuka file `/etc/default/grub`.
```
vim /etc/default/grub
```
2. Tekan **i** (i) untuk beralih ke mode edit dan ubah `GRUB_DEFAULT=saved` menjadi `GRUB_DEFAULT=0`.
![](https://main.qcloudimg.com/raw/484e7a6e818dc44c2d4debb9230e0b46.png)
3. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.
4. Jalankan perintah berikut untuk menghasilkan konfigurasi kernel lagi.
```
grub2-mkconfig -o /boot/grub2/grub.cfg
```
5. Jalankan perintah berikut untuk memulai ulang server.
```
reboot
```
6. Jalankan perintah berikut untuk memeriksa apakah modifikasi berhasil.
```
uname -r
```

### Menghapus kernel yang tidak diperlukan
1. Jalankan perintah berikut untuk melihat semua kernel.
```
rpm -qa | grep kernel
```
2. Jalankan perintah berikut untuk menghapus kernel lama.
```
yum remove kernel-old_kernel_version
```
Misalnya:
```
yum remove kernel-3.10.0-957.el7.x86_64
```

### Mengaktifkan BBR
1. Jalankan perintah berikut untuk mengedit file `/etc/sysctl.conf`.
```
vim /etc/sysctl.conf
```
2. Tekan **i** (i) untuk beralih ke mode edit dan masukkan nilai berikut:
```
net.core.default_qdisc=fq
net.ipv4.tcp_congestion_control=bbr
```
3. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.
4. Jalankan perintah berikut untuk memuat pengaturan parameter kernel ke file konfigurasi `/etc/sysctl.conf`.
```
sysctl -p
```
5. Jalankan perintah berikut untuk memverifikasi apakah BBR telah berhasil diaktifkan.
```
sysctl net.ipv4.tcp_congestion_control
# Nilai berikut akan muncul jika konfigurasi berhasil:
# net.ipv4.tcp_congestion_control = bbr
```
```
sysctl net.ipv4.tcp_available_congestion_control
# Nilai berikut akan muncul jika konfigurasi berhasil:
# net.ipv4.tcp_available_congestion_control = reno cubic bbr
```
6. Jalankan perintah berikut untuk memeriksa apakah modul kernel dimuat.
```
lsmod | grep bbr
```
Jika informasi berikut ditampilkan, BBR telah berhasil diaktifkan.
![](https://main.qcloudimg.com/raw/7d736afd8ce22f421315e149a86527e5.png)



