Unduh dan dekompresi paket TOA yang sesuai dengan versi OS Linux di Tencent Cloud:
- **arm64**
	- [kernel-4.18.0 ](https://gaap-1251337138.file.myqcloud.com/kernel-4.18.0.rar)
- **centos**
	- [CentOS 6.5 64](https://gaap-1251337138.file.myqcloud.com/CentOS%206.5%2064.rar)
	- [CentOS 7.2 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.2%2064.rar)
	- [CentOS 7.3 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.3%2064.rar)
	- [CentOS 7.4 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.4%2064.rar)
	- [CentOS 7.5 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.5%2064.rar)
	- [CentOS 7.6 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.6%2064.rar)
	- [CentOS 7.7 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.7%2064.rar)
	- [CentOS 7.8 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.8%2064.rar)
	- [CentOS 7.9 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.9%2064.rar)
	- [CentOS 8.0 64](https://gaap-1251337138.file.myqcloud.com/CentOS%208.0%2064.rar)
	- [CentOS 8.2 64](https://gaap-1251337138.file.myqcloud.com/CentOS%208.2%2064.rar)
- **debian**
	- [Debian 8.2 64](https://gaap-1251337138.file.myqcloud.com/Debian%208.2%2064.rar)
	- [Debian 9.0 64](https://gaap-1251337138.file.myqcloud.com/Debian%209.0%2064.rar)
	- [Debian 10.2 64](https://gaap-1251337138.file.myqcloud.com/Debian%2010.2%2064.rar)
- **suse linux**
	- [SUSE Linux Enterprise Server 11 SP3 64](http://toamodule-1253438722.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2011%20SP3%2064.zip)
	- [SUSE Linux Enterprise Server 12 64](http://toamodule-1253438722.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2012%2064.zip)
	- [SUSE Linux Enterprise Server 12 SP3 64](https://gaap-1251337138.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2012%20SP3%2064%E4%BD%8D.rar)
- **ubuntu**
	- [Ubuntu Server 14.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2014.04.1%20LTS%2064.rar)
	- [Ubuntu Server 16.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2016.04.1%20LTS%2064.rar)
	- [Ubuntu Server 18.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2018.04.1%20LTS%2064.rar)
	- [Ubuntu Server 20.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2020.04.1%20LTS%2064.rar)




1. Setelah dekompresi selesai, jalankan perintah `cd` untuk mengakses folder yang didekompresi dan jalankan perintah pemuatan modul:
```
insmod toa.ko
```
2. Jalankan perintah berikut untuk memeriksa apakah pemuatan berhasil:
```
lsmod | grep toa
```
3. Jika ya, muat file `toa.ko` dalam skrip startup (file `toa.ko` perlu dimuat ulang jika server dimulai ulang).

Jika tidak dapat menemukan paket penginstalan yang sesuai dengan versi OS Anda dari daftar di atas, harap unduh dan kumpulkan paket sumber versi umum untuk OS Linux. Versi ini mendukung sebagian besar distribusi Linux seperti CentOS 6.9, CentOS 7, dan Ubuntu 14.04.
1. Dapatkan paket sumber.
	- Paket sumber untuk CentOS 7 dan versi di atasnya
```
wget "http://thunder-pro-mainland-1258348367.cos.ap-guangzhou.myqcloud.com/gaap-toa%E6%BA%90%E7%A0%81(centos7%E4%BB%A5%E4%B8%8A).zip"
```
	- Paket sumber untuk versi di bawah CentOS 7
```
wget "http://thunder-pro-mainland-1258348367.cos.ap-guangzhou.myqcloud.com/gaap-toa%E6%BA%90%E7%A0%81(centos7%E4%BB%A5%E4%B8%8B).zip"
```
2. Kumpulkan paket sumber untuk menghasilkan file modul TOA.
```
yum install gcc
yum install kernel-headers
yum install kernel-devel
unzip gaap-toa*.zip //Dekompresi paket sumber di atas
cd gaap-toa* //Akses direktori yang sesuai
make
```
3. Muat file modul TOA.
```
mv toa.ko /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
insmod /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
```

Jika kesalahan pengumpulan dilaporkan, kesalahan tersebut mungkin disebabkan oleh inkonsistensi antara versi kernel yang diinstal dan versi yang ditampilkan `uname -r`. Di direktori `/lib/modules/`, periksa versi kernel yang sebenarnya terinstal, ubah `uname -r` di `Makefile` ke versi kernel yang sebenarnya, dan kumpulkan kembali file tersebut.
