## Skenario

[USB/IP](http://usbip.sourceforge.net/) adalah proyek sumber terbuka dan telah digabungkan ke dalam kernel. Di lingkungan Linux, Anda dapat menggunakan USB/IP untuk berbagi perangkat USB dari jarak jauh. Dokumen ini menggunakan versi lingkungan berikut sebagai contoh untuk menjelaskan cara menggunakan USB/IP untuk berbagi perangkat USB.
Klien USB: CVM dengan CentOS 7.6
Server USB: PC lokal dengan Debian

## Catatan
Metode penginstalan USB/IP dan nama modul kernel berbeda-beda tergantung pada versi OS Linux. Periksa apakah OS Linux Anda saat ini mendukung fitur USB/IP.


## Petunjuk

### Mengonfigurasi server USB

1. Pada PC lokal, jalankan perintah berikut secara berurutan untuk menginstal USB/IP dan memuat modul kernel terkait:
```
sudo apt-get install usbip
sudo modprobe usbip-core
sudo modprobe vhci-hcd
sudo modprobe usbip_host
```
2. Masukkan perangkat USB dan jalankan perintah berikut untuk melihat perangkat USB yang tersedia:
```
usbip list --local
```
Misalnya, jika kunci USB Feitian dimasukkan ke PC lokal, hasil berikut akan ditampilkan:
```
busid 1-1.3(096e:031b)
Feitian Technologies, Inc.: unknown product(096e:031b)
```
3. Catat nilai busid dan jalankan perintah berikut secara berurutan untuk mengaktifkan operasi mendengarkan, tentukan port USB/IP, dan bagikan perangkat USB:
```
sudo usbipd -D [--tcp-port PORT]
sudo usbip bind -b [busid]
```
Misalnya, jika port USB/IP yang ditentukan adalah port 3240 (port USB/IP default) dan busid adalah `1-1.3`, jalankan perintah berikut:
```
sudo usbipd -D
sudo usbip bind -b 1-1.3
```
(Opsional) 4. Jalankan perintah berikut untuk membuat tunnel SSH dan menggunakan pendengaran port:
> Lewati langkah ini jika PC lokal memiliki alamat IP publik.
>
```
ssh -Nf -R specified USB/IP port:localhost:specified USB/IP port root@your_host
```
`your_host` menunjukkan alamat IP CVM.
Misalnya, jika port USB/IP adalah port 3240 dan alamat IP CVM adalah 192.168.15.24, jalankan perintah berikut:
```
ssh -Nf -R 3240:localhost:3240 root@192.168.15.24
```


### Mengonfigurasi klien USB

> Berikut ini menggunakan PC lokal tanpa IP publik sebagai contoh. Jika PC lokal Anda memiliki IP publik, ganti `127.0.0.1` dalam langkah-langkah berikut dengan IP publik PC lokal Anda.
>

1. [Login ke instans Linux menggunakan metode login standar (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5436).
2. Jalankan perintah berikut secara berurutan untuk mengunduh sumber USB/IP:
```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -ivh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
```
3. Jalankan perintah berikut secara berurutan untuk menginstal USB/IP:
```
yum -y install kmod-usbip usbip-utils
modprobe usbip-core
modprobe vhci-hcd
modprobe usbip-host
```
4. Jalankan perintah berikut untuk mengkueri perangkat USB yang tersedia dari CVM:
```
usbip list --remote 127.0.0.1
```
Misalnya, jika informasi kunci USB Feitian ditemukan, hasil berikut akan ditampilkan:
```
Perangkat USB yang dapat diekspor
======================
-127.0.0.1 1-1.3: Feitian Technologies, Inc.: unknown product(096e:031b):/sys/devices/platform/scb/fd500000.pcie/pci0000:00/0000:00:00.0/0000:01:00.0/usb1/1-1/1-1.3:(Defined at Interface level)(00/00/00)
```
5. Jalankan perintah berikut untuk mengikat perangkat USB ke CVM:
```
usbip attach --remote=127.0.0.1 --busid=1-1.3
```
6. Jalankan perintah berikut untuk mengkueri daftar perangkat USB:
```
lsusb
```
Jika informasi yang mirip dengan berikut ini ditampilkan, perangkat USB telah dibagikan.
```
Bus 002 Device 002:ID096e:031b Feitian Technologies, Inc.
Bus 002 Device 001:ID1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 001:ID1d6b:0001 Linux Foundation 1.1 root hub
```
