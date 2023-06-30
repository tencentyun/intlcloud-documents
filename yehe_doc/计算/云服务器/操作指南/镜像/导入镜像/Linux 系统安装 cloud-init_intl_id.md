## Ikhtisar

Cloud-init memungkinkan Anda menyesuaikan konfigurasi selama inisialisasi pertama instans. Jika citra yang diimpor tidak menginstal layanan cloud-init, instans yang di-boot melalui citra tidak dapat diinisialisasi dengan benar. Akibatnya, citra akan gagal diimpor. Dokumen ini menjelaskan cara menginstal layanan cloud-init.
Anda dapat menggunakan salah satu metode berikut untuk menginstal cloud-init:

- [Mengunduh paket sumber cloud-init secara manual](#ManualDown) 
- [Menggunakan paket cloud-init dari sumber perangkat lunak](#SoftSources)


## Prasyarat
Server dengan layanan cloud-init yang diinstal dapat mengakses jaringan publik.

## Petunjuk


<span id="ManualDown"></span>
### Mengunduh paket sumber cloud-init secara manual 

#### Mengunduh paket sumber cloud-init
>?  
> - Versi cloud-init-17.1 paling kompatibel dengan Tencent Cloud. Versi ini memastikan semua item konfigurasi CVM yang dibuat melalui citra dapat diinisialisasi dengan benar. Sebaiknya instal **cloud-init-17.1.tar.gz** (cloud-init-17.1.tar.gz). Anda juga dapat [klik di sini](https://launchpad.net/cloud-init/+download) untuk mengunduh versi lain. Dokumen ini menggunakan cloud-init-17.1 sebagai contoh.
> - Jika penginstalan gagal, [unduh paket green cloud-init secara manual](#greeninitCloudInit) untuk menginstal layanan.
>
Jalankan perintah berikut untuk mengunduh paket sumber cloud-init:
```
wget https://launchpad.net/cloud-init/trunk/17.1/+download/cloud-init-17.1.tar.gz
```

#### Menginstal cloud-init
1. Jalankan perintah berikut untuk mendekompresi paket penginstalan cloud-init:
>? Jika Anda menggunakan sistem operasi Ubuntu, jalankan perintah ini dengan akun “root”.
>
```
tar -zxvf cloud-init-17.1.tar.gz 
```
2. Jalankan perintah berikut untuk masuk ke direktori paket ipenginstalan cloud-init yang didekompresi; yaitu, direktori cloud-init-17.1:
```
cd cloud-init-17.1
```
3. Instal Python-pip sesuai dengan versi sistem operasi.
 - Untuk CentOS 6/7, jalankan perintah berikut:
```
yum install python-pip -y
```
 - Untuk Ubuntu, jalankan perintah berikut:
```
apt-get install python-pip -y
```
Selama penginstalan, jika terjadi kesalahan seperti “failed to install” (gagal menginstal) atau “installation package not found” (paket penginstalan tidak ditemukan), lihat [menyelesaikan kegagalan penginstalan Python-pip](#updateSoftware) untuk memecahkan masalah.
4. Jalankan perintah berikut untuk menginstal dependensi:
>!  Python 2.6 tidak didukung saat cloud-init menggunakan permintaan 2.20.0 atau versi yang lebih baru. Jika interpreter Python yang diinstal di lingkungan citra adalah Python versi 2.6 atau yang lebih lama, jalankan perintah `pip install 'requests<2.20.0'` untuk menginstal request 2.20.0 atau yang lebih baru sebelum menginstal dependensi cloud-init.
>
```
pip install -r requirements.txt
```
5. Instal komponen cloud-utils sesuai dengan versi sistem operasi.
 - Untuk CentOS 6, jalankan perintah berikut:
```
yum install cloud-utils-growpart dracut-modules-growroot -y
dracut -f
```
 - Untuk CentOS 7, jalankan perintah berikut:
```
yum install cloud-utils-growpart -y
```
 - Untuk Ubuntu, jalankan perintah berikut:
```
apt-get install cloud-guest-utils -y
```
6. Jalankan perintah berikut untuk menginstal cloud-init:
```
python setup.py build
python setup.py install --init-system systemd
```
>! `--init-system` dapat diikuti oleh salah satu systemd, sysvinit, sysvinit_deb, sysvinit_freebsd, sysvinit_openrc, sysvinit_suse, atau upstart [default: Tidak ada]. Harap konfigurasi parameter berdasarkan metode manajemen layanan mulai otomatis dari sistem operasi. Jika parameter yang salah dikonfigurasi, layanan cloud-init tidak dapat secara otomatis memulai saat startup sistem. Dokumen ini menggunakan metode manajemen layanan mulai otomatis systemd sebagai contoh.

#### Memodifikasi file konfigurasi cloud-init

1. Unduh cloud.cfg untuk sistem operasi Anda.
 - [Klik di sini](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg) untuk mengunduh cloud.cfg untuk Ubuntu.
 - [Klik di sini](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg) untuk mengunduh cloud.cfg untuk CentOS.
2. Ganti konten `/etc/cloud/cloud.cfg` dengan konten file cloud.cfg yang diunduh.

#### Menambahkan pengguna syslog
Jalankan perintah berikut untuk menambahkan pengguna syslog:
```
useradd syslog
```

#### Mengatur layanan cloud-init ke mulai otomatis
- **If your operating system uses the systemd auto-start service management method, run the following commands.** (Jika sistem operasi Anda menggunakan metode manajemen layanan mulai otomatis systemd, jalankan perintah berikut.)
>? Untuk memeriksa apakah sistem operasi menggunakan systemd, jalankan `strings /sbin/init | grep "/lib/system"`, dan Anda akan menerima pesan balasan.
>
 1. **Run the following command in Ubuntu or Debian:** (Jalankan perintah berikut di Ubuntu atau Debian:)
```
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```
 2. **Run the following commands in all operating systems:** (Jalankan perintah berikut di semua sistem operasi:)
```
systemctl enable cloud-init-local.service 
systemctl start cloud-init-local.service
systemctl enable cloud-init.service
systemctl start cloud-init.service
systemctl enable cloud-config.service
systemctl start cloud-config.service
systemctl enable cloud-final.service
systemctl start cloud-final.service
systemctl status cloud-init-local.service
systemctl status cloud-init.service
systemctl status cloud-config.service
systemctl status cloud-final.service
```
 3. **Run the following command in CentOS or Redhat.** (Jalankan perintah berikut di CentOS atau Redhat.)
 Ganti konten `/lib/systemd/system/cloud-init-local.service` dengan konten berikut:
```
[Unit]
Description=Initial cloud-init job (pre-networking)
Wants=network-pre.target
After=systemd-remount-fs.service
Before=NetworkManager.service
Before=network-pre.target
Before=shutdown.target
Conflicts=shutdown.target
RequiresMountsFor=/var/lib/cloud
[Service]
Type=oneshot
ExecStart=/usr/bin/cloud-init init --local
ExecStart=/bin/touch /run/cloud-init/network-config-ready
RemainAfterExit=yes
TimeoutSec=0
# Output perlu muncul di output konsol instans
StandardOutput=journal+console
[Install]
WantedBy=cloud-init.target
```
Ganti konten `/lib/systemd/system/cloud-init.service` dengan konten berikut:
```
[Unit]
Description=Initial cloud-init job (metadata service crawler)
Wants=cloud-init-local.service
Wants=sshd-keygen.service
Wants=sshd.service
After=cloud-init-local.service
After=systemd-networkd-wait-online.service
After=networking.service
After=systemd-hostnamed.service
Before=network-online.target
Before=sshd-keygen.service
Before=sshd.service
Before=systemd-user-sessions.service
Conflicts=shutdown.target
[Service]
Type=oneshot
ExecStart=/usr/bin/cloud-init init
RemainAfterExit=yes
TimeoutSec=0
# Output perlu muncul di output konsol instans
StandardOutput=journal+console
[Install]
WantedBy=cloud-init.target
```
- **If your operating system uses the sysvinit auto-start service management method, run the following commands:** (Jika sistem operasi Anda menggunakan metode manajemen layanan mulai otomatis sysvinit, jalankan perintah berikut:)
>? Untuk memeriksa apakah sistem operasi menggunakan sysvinit, jalankan perintah `strings /sbin/init | grep "sysvinit"`, dan Anda akan menerima pesan balasan.
>
```
chkconfig --add cloud-init-local
chkconfig --add cloud-init
chkconfig --add cloud-config
chkconfig --add cloud-final
chkconfig cloud-init-local on 
chkconfig cloud-init on 
chkconfig cloud-config on 
chkconfig cloud-final on 
```


<span id="SoftSources"></span>
### Menggunakan paket cloud-init dari sumber perangkat lunak

#### Menginstal cloud-init

Jalankan perintah berikut untuk menginstal cloud-init:
```
apt-get/yum install cloud-init
```
>? Secara default, versi cloud-init yang diinstal dengan menjalankan `apt-get` atau `yum` adalah versi cloud-init default di sumber perangkat lunak yang dikonfigurasi untuk sistem operasi. Beberapa item konfigurasi instans yang dibuat dengan menggunakan citra yang cloud-init-nya diinstal dengan cara ini mungkin tidak diinisialisasi seperti yang diharapkan. Dengan demikian, sebaiknya instal layanan dengan [mengunduh paket sumber cloud-init secara manual](#ManualDown).
>

#### Memodifikasi file konfigurasi cloud-init
1. Unduh cloud.cfg untuk sistem operasi Anda.
 - [Klik di sini](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg) untuk mengunduh cloud.cfg untuk Ubuntu.
 - [Klik di sini](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg) untuk mengunduh cloud.cfg untuk CentOS.
2. Ganti konten `/etc/cloud/cloud.cfg` dengan konten file cloud.cfg yang diunduh.

## Operasi yang Relevan
>! Jangan mulai ulang server setelah melakukan operasi di atas. Jika tidak, Anda harus melakukannya lagi.
>
1. Jalankan perintah berikut untuk memeriksa apakah konfigurasi cloud-init berhasil.
```
cloud-init init --local
rm -rf /var/lib/cloud
```
2. Jalankan perintah berikut di Ubuntu atau Debian:
```
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
3. Untuk Ubuntu atau Debian, ganti konten `/etc/network/interfaces` dengan konten berikut:
```
# File ini menjelaskan antarmuka jaringan yang tersedia di sistem Anda
# dan cara mengaktifkannya. Untuk informasi selengkapnya, lihat antarmuka(5).
source /etc/network/interfaces.d/*
```

## Catatan

<span id="greeninitCloudInit"></span>
### Mengunduh edisi portabel paket cloud-init
Jika Anda gagal menginstal cloud-init seperti yang diinstruksikan di [Mengunduh paket sumber cloud-init secara manual](#ManualDown), cobalah langkah-langkah berikut:
1. [Klik di sini](https://image-tools-1251783334.cos.ap-guangzhou.myqcloud.com/greeninit-x64-beta.tgz) untuk mendapatkan edisi portabel paket cloud-init.
2. Jalankan perintah berikut untuk mendekompresi paket portabel:
```
tar xvf greeninit-x64-beta.tgz 
```
3. Jalankan perintah berikut untuk masuk ke direktori paket yang didekompresi; yaitu, direktori `greeninit`:
```
cd greeninit
```
4. Jalankan perintah berikut untuk menginstal cloud-init:
```
sh install.sh 
```

<span id="updateSoftware"></span>

### Mengatasi kegagalan penginstalan Python-pip

Selama penginstalan, jika terjadi kesalahan seperti “failed to install” (gagal menginstal) atau “installation package not found” (paket penginstalan tidak ditemukan), selesaikan masalah berdasarkan sistem operasi sebagai berikut:
- Untuk CentOS 6/7:
  1. Jalankan perintah berikut untuk mengonfigurasi repositori penyimpanan EPEL.
```
yum install epel-release -y
```
  2. Jalankan perintah berikut untuk menginstal Python-pip.
```
yum install python-pip -y
```
- Untuk Ubuntu:
  1. Jalankan perintah berikut untuk memperbarui daftar paket perangkat lunak.
```
apt-get update -y
```
  2. Jalankan perintah berikut untuk menginstal Python-pip.
```
apt-get install python-pip -y
```


