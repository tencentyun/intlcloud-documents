## Pengantar
Artikel ini menjelaskan cara menyiapkan lingkungan Web Java di CVM Linux.

Langkah ini mengharuskan Anda untuk memahami perintah Linux yang umum, seperti [Menginstal Perangkat Lunak melalui YUM di Lingkungan CentOS](https://intl.cloud.tencent.com/document/product/213/2046), dan memahami versi perangkat lunak yang diinstal.

## Perangkat Lunak
Berikut adalah perangkat lunak yang digunakan:
- CentOS adalah distribusi dari sistem operasi Linux. Kami menggunakan CentOS 7.6 dalam artikel ini.
- Apache Tomcat menyediakan lingkungan server web HTTP "pure Java" tempat kode Java dapat dijalankan. Kami menggunakan Apache Tomcat 8.5.47.
- JDK, atau Java Development Kit, adalah implementasi dari Java Platform. Kami menggunakan JDK 1.8.0_221 dalam artikel ini.


## Prasyarat
Menyiapkan lingkungan Web Java memerlukan CVM Linux. Jika Anda belum membelinya, lihat [Memulai CVM Linux](http://intl.cloud.tencent.com/document/product/213/2936).

## Petunjuk
### Langkah 1: Login ke instans Linux
- [Login ke instans Linux menggunakan WebShell (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang nyaman bagi Anda:
- [Login ke instans Linux menggunakan perangkat lunak login jarak jauh](https://intl.cloud.tencent.com/document/product/213/32502).
- [Login ke Instans Linux menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32501)


### Langkah 2: Menginstal JDK
1. Unduh file penginstalan JDK. Buka [halaman unduhan Java SE](https://www.oracle.com/technetwork/java/javase/downloads/index.html) untuk memilih versi dan mengunduhnya.
>Unduh file JDK, simpan secara lokal, dan unggah ke CVM Anda. Jika tidak, mendekompresi file akan menghasilkan kesalahan.
> - Jika Anda menggunakan Windows, gunakan [WinSCP](https://intl.cloud.tencent.com/document/product/213/2131) untuk mengunggah file.
> - Jika Anda menggunakan MacOS atau Linux, gunakan [SCP](https://intl.cloud.tencent.com/document/product/213/2133) untuk mengunggah file.
>
2. Jalankan perintah berikut untuk membuat direktori untuk penginstalan JDK.
```
mkdir /usr/java
```
3. Jalankan perintah berikut untuk mendekompresi JDK ke direktori.
```
tar xzf jdk-8u221-linux-x64.tar.gz -C /usr/java
```
4. Jalankan perintah berikut untuk membuka `profile`.
```
vim /etc/profile
```
5. Tekan **i** (i) untuk masuk ke mode edit. Mulai baris baru setelah `export PATH USER ...` dan tambahkan berikut ini:
```
export JAVA_HOME=/usr/java/jdk1.8.0_221 (ganti 1.8.0_221 dengan nomor versi JDK Anda)
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH
```
Hasilnya harus sebagai berikut:
![](https://main.qcloudimg.com/raw/a4d0466eca6c4c0ef219f571b7d165de.png)
6. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file dan kembali.
7. Jalankan perintah berikut untuk membaca variabel lingkungan sistem.
```
source /etc/profile
```
8. Jalankan perintah berikut untuk memeriksa apakah JDK diinstal dengan benar.
```
java -version
```
Jika muncul hasil berikut, artinya penginstalan berhasil.
![](https://main.qcloudimg.com/raw/f12cfeed5d8aa15cccb9836637e9555f.png)

### Langkah 3: Menginstal Tomcat
1. Jalankan perintah berikut untuk mengunduh kode sumber Tomcat. Pilih versi yang cocok bagi Anda.
>Lihat [situs web resmi Apache Tomcat](https://tomcat.apache.org/) untuk mengetahui informasi selengkapnya.
>
```
wget http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.47/bin/apache-tomcat-8.5.47.tar.gz
```
2. Jalankan perintah berikut untuk mendekompresi file.
```
tar xzf apache-tomcat-8.5.47.tar.gz
```
3. Jalankan perintah berikut untuk memindahkan direktori yang berisi Tomcat ke `/usr/local/Tomcat/`.
```
mv apache-tomcat-8.5.47 /usr/local/tomcat/
```
4. Jalankan perintah berikut untuk membuka `server.xml`.
```
vim /usr/local/tomcat/conf/server.xml
```
5. Cari `<Host … appBase="webapps”>` dan tekan **i** (i) untuk masuk ke mode edit. Ganti `appBase="webapps"` dengan hal berikut:
```
appBase="/usr/local/tomcat/webapps"
```
6. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file dan kembali.
7. Jalankan perintah berikut untuk membuat file bernama `setenv.sh`.
```
vi /usr/local/tomcat/bin/setenv.sh
```
8. Tekan **Enter** (Enter) untuk masuk ke mode edit dan masukkan hal berikut untuk mengatur variabel memori JVM.
```
JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8' 
```
9. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file dan kembali.
10. Jalankan perintah berikut untuk memulai Tomcat.
```
/usr/local/tomcat/bin/startup.sh
```
Jika muncul hasil berikut, artinya Tomcat berhasil dijalankan.
![](https://main.qcloudimg.com/raw/64bdd25e734db46464655f15acae4c2f.png)

## Memverifikasi Konfigurasi Lingkungan
1. Jalankan perintah berikut untuk membuat file pengujian.
```
echo Hello World! > /usr/local/tomcat/webapps/ROOT/index.jsp
```
2. Buka jendela browser di mesin lokal Anda dan kunjungi URL berikut untuk memeriksa apakah konfigurasi lingkungan berhasil.
```
http://[Alamat IP publik instans CVM]:8080
```
Jika hasil berikut muncul, artinya konfigurasi lingkungan berhasil.
![](https://main.qcloudimg.com/raw/359b7119e9e7d81e2e2728dabd57456a.png)

## Pertanyaan Umum
Jika Anda mengalami masalah saat menggunakan CVM, lihat dokumen berikut untuk pemecahan masalah berdasarkan situasi aktual Anda.
- Untuk masalah terkait login CVM, lihat [Login Kata Sandi dan Login Kunci SSH](https://intl.cloud.tencent.com/document/product/213/18120) dan [Akses Login dan Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278).
- Untuk masalah terkait jaringan CVM, lihat [Alamat IP](https://intl.cloud.tencent.com/document/product/213/17285) dan [Grup Port dan Keamanan](https://intl.cloud.tencent.com/document/product/213/2502).
- Untuk masalah terkait disk CVM, lihat [Disk Sistem dan Data](https://intl.cloud.tencent.com/document/product/213/17351).
