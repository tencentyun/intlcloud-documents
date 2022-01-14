Dokumen ini menjelaskan cara men-deploy proyek-proyek Web Java di CentOS dan cocok untuk setiap pengguna baru Tencent Cloud.
## Versi Perangkat Lunak
Versi alat perangkat lunak yang digunakan dalam dokumen ini adalah sebagai berikut, yang mungkin berbeda dengan versi perangkat lunak Anda selama operasi aktual.
- Sistem operasi:CentOS 7.5
- Tomcat: apache-tomcat-8.5.39
- JDK:JDK 1.8.0_201

## Menginstal JDK
Setelah membeli CVM, Anda dapat mengeklik **Login** (Masuk) di halaman detail CVM untuk masuk ke instance CVM Anda agar dapat memasukkan nama pengguna dan kata sandi guna menyiapkan lingkungan web Java.Untuk informasi selengkapnya tentang cara membuat instance CVM, lihat [CVM - Membuat Instance](https://intl.cloud.tencent.com/document/product/213/4855).

### Mengunduh JDK
Masukkan perintah berikut:
```
mkdir /usr/java  # Buat folder `java`
cd /usr/java     # Masukkan folder `java`
```
<pre>
<code># Mengunggah paket penginstalan JDK (disarankan)
Anda sebaiknya menggunakan alat seperti <a href="https://winscp.net/eng/docs/lang:chs" target="_blank">WinSCP</a> untuk mengunggah paket penginstalan JDK ke folder `java` di atas lalu mendekompresinya.
Atau
# Gunakan perintah (Anda sebaiknya mengunggah paket penginstalan): jalankan `wget` untuk mengunduh paket, yang tidak dapat didekompresi karena paket unduhan secara default menolak Lisensi Oracle BSD.Silakan buka https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html untuk menerima persetujuan lisensi dan mendapatkan tautan unduh beserta cookie.
wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.tar.gz</code>
</pre>
```
# Dekompresi
chmod +x jdk-8u201-linux-x64.tar.gz
tar -xzvf jdk-8u201-linux-x64.tar.gz
```

### Mengatur variabel lingkungan
1.Buka file `/etc/profile`.
```
vi /etc/profile
```
2.Tekan I untuk masuk ke mode pengeditan dan tambahkan informasi berikut ke dalam file.
```
# atur lingkungan java
ekspor JAVA_HOME=/usr/java/jdk1.8.0_201
ekspor CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
ekspor PATH=$JAVA_HOME/bin:$PATH
```
3.Tekan Esc untuk keluar dari mode pengeditan dan masukkan `:wq` untuk menyimpan dan menutup file.
4.Muat variabel lingkungan.
```
source /etc/profile
```

### Melihat hasil penginstalan JDK
Jalankan perintah `java -version`.Jika informasi versi JDK ditampilkan, JDK telah berhasil diinstal.
![](https://main.qcloudimg.com/raw/6d3531f4d466e5428885ec38a3542c2e.png)

## Menginstal Tomcat
### Mengunduh Tomcat
Masukkan perintah-perintah berikut:
```
# Alamat cermin dapat berubah dan versi Tomcat mungkin terus-menerus ditingkatkan.Jika tautan unduh kedaluwarsa, silakan buka [situs web resmi Tomcat](https://tomcat.apache.org/download-80.cgi) dan pilih alamat paket penginstalan yang sesuai.
wget http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.39/bin/apache-tomcat-8.5.39.tar.gz
tar -xzvf apache-tomcat-8.5.39.tar.gz
mv apache-tomcat-8.5.39 /usr/local/tomcat/
```
File-file berikut ada di dalam direktori `/usr/local/tomcat/`:
- bin: file skrip, yang berisi skrip untuk memulai dan menghentikan layanan Tomcat.
- conf: file-file konfigurasi global, dengan file-file terpenting berupa `server.xml` dan `web.xml`.
- webapps: direktori rilis web utama di Tomcat, yang merupakan direktori default untuk menyimpan file-file aplikasi web.
- logs:file log Tomcat.

>!Jika tautan unduh kedaluwarsa, silakan ganti dengan tautan terbaru di [situs web resmi Tomcat](https://tomcat.apache.org/download-80.cgi).

### Menambahkan pengguna
```
# Tambahkan `www` pengguna umum untuk menjalankan Tomcat
useradd www
# Buat direktori root situs web
mkdir -p /data/wwwroot/default
# Unggah file proyek web Java (paket WAR) ke direktori root situs web dan ubah izin file di bagian direktori ke `www`.Contoh ini menunjukkan cara membuat halaman pengujian Tomcat di dalam direktori root situs web:
echo Halo Tomcat! > /data/wwwroot/default/index.jsp
chown -R www.www /data/wwwroot
```

### Mengatur parameter memori JVM
1.Buat file skrip `/usr/local/tomcat/bin/setenv.sh`.
```
vi /usr/local/tomcat/bin/setenv.sh
```
2.Tekan I untuk masuk ke mode pengeditan dan tambahkan berikut ini.
```
JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'
```
3.Tekan Esc untuk keluar dari mode pengeditan dan masukkan `:wq` untuk menyimpan dan keluar.

### Mengonfigurasi server.xml
1.Beralihlah ke direktori `/usr/local/tomcat/conf/`.
```
cd /usr/local/tomcat/conf/
```
2.Cadangkan file `server.xml`.
```
mv server.xml server_default.xml
```
3.Buat file `server.xml` yang baru.
```
vi server.xml
```
4.Tekan I untuk masuk ke mode pengeditan dan tambahkan berikut ini.
```
<?xml version="1.0" encoding="UTF-8"?>
<Server port="8006" shutdown="SHUTDOWN">
<Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener"/>
<Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener"/>
<Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener"/>
<Listener className="org.apache.catalina.core.AprLifecycleListener"/>
<GlobalNamingResources>
<Resource name="UserDatabase" auth="Container"
type="org.apache.catalina.UserDatabase"
deskripsi="User database that can be updated and saved" (Database pengguna yang dapat diperbarui dan disimpan)
factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
pathname="conf/tomcat-users.xml"/>
</GlobalNamingResources>
<Service name="Catalina">
<Connector port="8080"
protocol="HTTP/1.1"
connectionTimeout="20000"
redirectPort="8443"
maxThreads="1000"
minSpareThreads="20"
acceptCount="1000"
maxHttpHeaderSize="65536"
debug="0"
disableUploadTimeout="true"
useBodyEncodingForURI="true"
enableLookups="false"
URIEncoding="UTF-8"/>
<Engine name="Catalina" defaultHost="localhost">
<Realm className="org.apache.catalina.realm.LockOutRealm">
<Realm className="org.apache.catalina.realm.UserDatabaseRealm"
resourceName="UserDatabase"/>
</Realm>
<Host name="localhost" appBase="/data/wwwroot/default" unpackWARs="true" autoDeploy="true">
<Context path="" docBase="/data/wwwroot/default" debug="0" reloadable="false" crossContext="true"/>
<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
prefix="localhost_access_log."suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" />
</Host>
</Engine>
</Service>
</Server>
```
5.Tekan Esc untuk keluar dari mode pengeditan dan masukkan `:wq` untuk menyimpan dan keluar.

## Memulai Tomcat
### Metode 1
Masukkan direktori `bin` dari server Tomcat lalu jalankan perintah `./startup.sh` untuk memulai server Tomcat.
```
cd /usr/local/tomcat/bin
./startup.sh
```
Hasil eksekusi adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/c118899986968ecd5982eb8cdb2beff9.png)
### Metode 2
1.Siapkan mulai cepat agar server Tomcat dapat dimulai di mana saja melalui `service tomcat start`.
```
wget https://github.com/lj2007331/oneinstack/raw/master/init.d/Tomcat-init
mv Tomcat-init /etc/init.d/tomcat
chmod +x /etc/init.d/tomcat
```
2.Jalankan perintah berikut dan atur skrip startup `JAVA_HOME`.
```
sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/java/jdk1.8.0_201@' /etc/init.d/tomcat
```
3.Atur jalankan otomatis.
```
chkconfig --tambahkan tomcat
chkconfig tomcat di
```
4.Mulai Tomcat.
```
# Mulai Tomcat
mulai layanan tomcat
# Lihat status server Tomcat
status layanan tomcat
# Hentikan Tomcat
hentikan layanan tomcat
```
Hasil eksekusi adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/78800e85c09820d98a0a15dc2792aaa8.png)
5.Jika sistem menampilkan prompt bahwa Anda tidak memiliki izin, beralihlah ke pengguna root dan ubah izinnya.
```
cd /usr/local
chmod -R 777 tomcat
```
6.Masukkan `http://public IP:port` (di sini port adalah port konektor yang diatur dalam `server.xml`) di bilah alamat peramban.Jika muncul halaman berikut, penginstalan berhasil.
![](https://main.qcloudimg.com/raw/a8d7c77aafc94c9bba262c06125b6c18.png)

### Mengonfigurasi grup keamanan
Jika terjadi kegagalan akses, periksa grup keamanan.Seperti yang terpampang pada contoh di atas, port konektor adalah 8080 di `server.xml` sehingga Anda harus membuka TCP:8080 ke internet di grup keamanan yang terikat dengan instance CVM yang sesuai.
![](https://main.qcloudimg.com/raw/6ffabfd2ef027e4fc69e4fc1a85dde9f.png)
