## Ikhtisar

Untuk mengatasi masalah akses lambat ke sumber resmi saat menginstal dependensi, Tencent Cloud telah menyiapkan layanan cache untuk beberapa perangkat lunak. Anda dapat mempercepat penginstalan dependensi dengan menggunakan repositori perangkat lunak Tencent Cloud, yang saat ini mendukung akses jaringan publik dan akses jaringan pribadi.
- Alamat akses jaringan publik: `http://mirrors.tencent.com/` 
- Alamat akses jaringan pribadi: `http://mirrors.tencentyun.com/`

>?
> - Dokumen ini mengambil alamat akses jaringan publik dari repositori perangkat lunak Tencent Cloud sebagai contoh untuk memperkenalkan cara menggunakan sumber perangkat lunak di repositori perangkat lunak Tencent Cloud di CVM. Jika Anda mengakses repositori menggunakan jaringan pribadi, harap ganti alamat akses jaringan publik **with the private network access address** (dengan alamat akses jaringan pribadi).
> - Alamat sumber yang digunakan dalam dokumen ini hanya untuk referensi. Dapatkan alamat terbaru dari **Tencent Cloud software repository** (Repositori perangkat lunak Tencent Cloud).

## Catatan

Repositori perangkat lunak Tencent Cloud memperbarui sumber perangkat lunak dari situs web resmi setiap sumber perangkat lunak sekali sehari.

## Prasyarat

Anda sudah login ke CVM.

## Petunjuk

### Mempercepat pip menggunakan sumber citra Tencent Cloud
>! Sebelum menggunakan sumber citra Tencent Cloud, pastikan CVM Anda telah menginstal Python.

#### Menggunakan jalur sumber perangkat lunak untuk sementara
Jalankan perintah berikut untuk menginstal pip menggunakan Tencent Could PyPI.
```
pip install pip -i direktori tempat PyPI berada
```
Misalnya, jika PyPI yang perlu Anda gunakan ada di direktori `http://mirrors.cloud.tencent.com/pypi/simple`, jalankan perintah berikut:
```
pip install 17monip -i http://mirrors.cloud.tencent.com/pypi/simple --trusted-host mirrors.cloud.tencent.com 
```

#### Mengatur jalur sumber perangkat lunak default
Jalankan perintah berikut untuk memodifikasi parameter `index-url` di file `~/.pip/pip.conf` ke jalur sumber repositori perangkat lunak Tencent Cloud.

```
[global]
index-url = direktori tempat PyPI berada
trusted-host = jaringan publik/alamat akses jaringan pribadi
```
Misalnya, jika PyPI yang perlu Anda gunakan ada di direktori `http://mirrors.cloud.tencent.com/pypi/simple`, jalankan perintah berikut:
```
[global]
index-url = http://mirrors.cloud.tencent.com/pypi/simple
trusted-host = mirrors.cloud.tencent.com
```

### Mempercepat Maven menggunakan sumber citra Tencent Cloud
>! Sebelum menggunakan sumber citra Tencent Cloud, pastikan CVM Anda telah menginstal JDK dan Maven.

1. Buka file konfigurasi `settings.xml` dari Maven.
2. Cari `<mirrors> ... blok kode </ mirrors>` dan konfigurasikan konten berikut ke dalamnya.
```
    <mirror>
        <id>nexus-tencentyun</id>
        <mirrorOf>*</mirrorOf>
        <name>Nexus tencentyun</name>
        <url>http://mirrors.cloud.tencent.com/nexus/repository/maven-public/</url>
    </mirror> 
```

### Mempercepat NPM menggunakan sumber citra Tencent Cloud
>! Sebelum menggunakan sumber citra Tencent Cloud, pastikan CVM Anda telah menginstal Node.js dan NPM.
>
Jalankan perintah berikut untuk menginstal NPM menggunakan Tencent Cloud NPM.
```
npm config set registry http://mirrors.cloud.tencent.com/npm/
```

### Mempercepat Docker menggunakan sumber citra Tencent Cloud

#### Menggunakan Tencent Cloud Docker di kluster TKE

Tidak diperlukan konfigurasi manual. Saat CVM di kluster Tencent Kubernetes Engine (TKE) membuat node, Docker akan diinstal secara otomatis dan dikonfigurasi dengan citra jaringan pribadi Tencent Cloud.

#### Menggunakan Tencent Cloud Docker di CVM

>! Sebelum menggunakan Tencent Cloud Docker, pastikan CVM Anda telah menginstal Docker.
> Hanya Docker 1.3.2 atau versi yang lebih baru yang mendukung mekanisme Docker Hub Mirror. Jika Anda belum menginstal Docker 1.3.2 atau versi yang lebih baru, atau jika versi yang diinstal terlalu lama, harap instal atau tingkatkan terlebih dahulu.
 
Pilih langkah operasi yang berbeda berdasarkan sistem operasi CVM.
- Langkah-langkah berikut untuk Ubuntu 14.04, Debian, CentOS 6, Fedora, openSUSE, dan sistem operasi lainnya. Langkah-langkah spesifik untuk versi lain dari sistem operasi dapat berbeda-beda:
 1. Jalankan perintah berikut untuk membuka file konfigurasi `/etc/default/docker`.
```
vim /etc/default/docker
```
 2. Tekan **i** (i) untuk beralih ke mode pengeditan, masukkan konten berikut, dan simpan.
```
DOCKER_OPTS="--registry-mirror=https://mirror.ccs.tencentyun.com"
```
- Untuk Centos 7:
 1. Jalankan perintah berikut untuk membuka file konfigurasi `/etc/docker/daemon.json`.
```
vim /etc/docker/daemon.json
```
 2. Tekan **i** (i) untuk beralih ke mode pengeditan, masukkan konten berikut, dan simpan.
```
{
   "registry-mirrors": [
       "https://mirror.ccs.tencentyun.com"
  ]
}
```
- Untuk Windows yang menginstal Boot2Docker:
 1. Akses Boot2Docker Start Shell dan jalankan perintah berikut:
```
sudo su echo "EXTRA_ARGS=\"–registry-mirror=https://mirror.ccs.tencentyun.com\"" >> /var/lib/boot2docker/profile exit 
```
 2. Mulai ulang Boot2Docker.

### Mempercepat MariaDB menggunakan citra Tencent Cloud
>? Langkah-langkah berikut mengambil CentOS 7 sebagai contoh. Langkah-langkah spesifik berbeda-beda tergantung pada sistem operasi.

1. Jalankan perintah berikut untuk membuat file `MariaDB.repo` di bagian `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/MariaDB.repo
```
2. Tekan **i** (i) untuk beralih ke mode pengeditan, masukkan konten berikut, dan simpan.
```
# MariaDB 10.2 CentOS7-amd64
[mariadb]  
name = MariaDB  
baseurl = http://mirrors.cloud.tencent.com/mariadb/yum/10.2/centos7-amd64/
gpgkey = http://mirrors.cloud.tencent.com/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1  
```
3. Jalankan perintah berikut untuk mengosongkan cache YUM.
```
yum clean all
```
4. Jalankan perintah berikut untuk menginstal MariaDB.
```
yum install MariaDB-client MariaDB-server
```

### Mempercepat MongoDB menggunakan citra Tencent Cloud
>? Langkah-langkah berikut mengambil MongoDB 4.0 sebagai contoh. Jika Anda perlu menginstal versi lain, harap ubah nomor versi di jalur cermin (mirror).

#### Menggunakan Tencent Cloud MongoDB pada CVM dengan sistem CentOS atau Redhat

1. Jalankan perintah berikut untuk membuat file `mongodb.repo` pada bagian `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/mongodb.repo
```
2. Tekan **i** (i) untuk beralih ke mode pengeditan, masukkan konten berikut, dan simpan.
```
[mongodb-org-4.0]
name=MongoDB Repository
baseurl=http://mirrors.cloud.tencent.com/mongodb/yum/el7-4.0
gpgcheck=0
enabled=1
```
3. Jalankan perintah berikut untuk menginstal MongoDB.
```
yum install -y mongodb-org
```

#### Menggunakan Tencent Cloud MongoDB pada CVM dengan sistem Debian

1. Berdasarkan versi Debian yang berbeda, jalankan perintah berikut untuk mengimpor kunci publik GPG MongoDB.
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. Jalankan perintah berikut untuk mengonfigurasi jalur `mirror`.
```
#Debian 8
echo "deb http://mirrors.cloud.tencent.com/mongodb/apt/debian jessie/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Debian 9
echo "deb http://mirrors.cloud.tencent.com/mongodb/apt/debian stretch/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. Jalankan perintah berikut untuk menghapus cache.
```shell
sudo apt-get clean all
```
4. Jalankan perintah berikut untuk memperbarui daftar paket perangkat lunak.
```
sudo apt-get update
```
5. Jalankan perintah berikut untuk menginstal MongoDB.
```
sudo apt-get install -y mongodb-org
```

#### Menggunakan Tencent Cloud MongoDB pada CVM dengan sistem Ubuntu

1. Jalankan perintah berikut untuk mengimpor kunci publik GPG MongoDB.
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. Jalankan perintah berikut untuk mengonfigurasi jalur `mirror`.
```
#Ubuntu 14.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu trusty/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 16.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 18.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. Jalankan perintah berikut untuk menghapus cache.
```shell
sudo apt-get clean all
```
4. Jalankan perintah berikut untuk memperbarui daftar paket perangkat lunak.
```
sudo apt-get update
```
5. Jalankan perintah berikut untuk menginstal MongoDB.
```
sudo apt-get install -y mongodb-org
```

### Mempercepat Rubygem menggunakan sumber citra Tencent Cloud
>! Sebelum menggunakan sumber citra Tencent Cloud, pastikan CVM Anda telah menginstal Ruby.

Jalankan perintah berikut untuk mengubah alamat sumber RubyGems.
```
gem source -r https://rubygems.org/
gem source -a http://mirrors.cloud.tencent.com/rubygems/
```
