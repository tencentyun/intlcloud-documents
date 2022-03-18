## Ikhtisar
RabbitMQ adalah perantara pesan sumber terbuka berdasarkan Advanced Message Queuing Protocol (AMQP). RabbitMQ mengutamakan kegunaan, skalabilitas, dan ketersediaan tinggi dengan server yang diprogram Erlang, dan mendukung banyak klien termasuk Python, Ruby, .NET, Java, JMS, C, PHP, ActionScript, XMPP, STOMP, dan AJAX. Dokumen ini menjelaskan cara men-deploy RabbitMQ di CVM Tencent Cloud.

## Perangkat Lunak
Dokumen ini menggunakan perangkat lunak berikut sebagai contoh untuk men-deploy RabbitMQ:
- Linux: Sistem operasi Linux. Dokumen ini menggunakan CentOS 7.7 sebagai contoh.
- RabbitMQ Server: perantara pesan sumber terbuka. Dokumen ini menggunakan RabbitMQ Server 3.6.9 sebagai contoh.
- Erlang: bahasa pemrograman. Dokumen ini menggunakan Erlang 19.3 sebagai contoh.


## Prasyarat
- CVM Linux diperlukan untuk men-deploy RabbitMQ. Jika Anda belum membeli CVM Linux, lihat [Menyesuaikan Konfigurasi CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517).
- Aturan grup keamanan untuk instans Linux telah dikonfigurasi. Buka port 80, 5672, dan 15672. Untuk informasi selengkapnya, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).

## Petunjuk
### Menginstal Erlang
1. [Login ke instans Linux menggunakan metode login standar](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang lebih nyaman bagi Anda:
	- [Login ke Instans Linux melalui Fitur Login Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32502)
	- [Login ke Instans Linux melalui Kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501)
1. Jalankan perintah berikut untuk menginstal dependensi.
```
yum -y install make gcc gcc-c++ m4 ncurses-devel openssl-devel unixODBC-devel
```
2. Jalankan perintah berikut untuk mengunduh paket penginstalan Erlang.
```
wget http://erlang.org/download/otp_src_19.3.tar.gz
```
3. Jalankan perintah berikut untuk mendekompresi paket penginstalan Erlang.
```
tar xzf otp_src_19.3.tar.gz
```
4. Jalankan perintah berikut untuk membuat folder erlang.
```
mkdir /usr/local/erlang
```
5. Jalankan perintah berikut secara berurutan untuk mengompilasi dan menginstal Erlang.
```
cd otp_src_19.3
```
```
./configure --prefix=/usr/local/erlang --without-javac
```
```
make && make install
```
6. Jalankan perintah berikut untuk membuka file konfigurasi profil.
```
vi /etc/profile
```
7. Tekan **i** (i) untuk masuk ke mode edit, dan tambahkan hal berikut ini di akhir file.
```
export PATH=$PATH:/usr/local/erlang/bin
```
8. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.

### Menginstal RabbitMQ Server
1. Jalankan perintah berikut untuk mengunduh paket penginstalan RabbitMQ Server.
```
wget https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_v3_6_9/rabbitmq-server-3.6.9-1.el7.noarch.rpm
```
Contoh ini menggunakan RabbitMQ 3.6.9 sebagai contoh. Jika tautan unduhan di atas telah kedaluwarsa, atau jika Anda ingin menggunakan versi RabbitMQ lainnya, buka [rabbitmq-server](https://github.com/rabbitmq/rabbitmq-server/releases).
10. Jalankan perintah berikut untuk mengimpor kunci tanda tangan.
```
rpm --import https://www.rabbitmq.com/rabbitmq-release-signing-key.asc
```
11. Jalankan perintah berikut secara berurutan untuk menginstal RabbitMQ Server.
```
cd
```
```
yum install rabbitmq-server-3.6.9-1.el7.noarch.rpm
```
12. Jalankan perintah berikut secara berurutan untuk mengaktifkan mulai otomatis RabbitMQ dan memulai RabbitMQ.
```
systemctl enable rabbitmq-server
```
```
systemctl start rabbitmq-server
```
13. Jalankan perintah berikut untuk menghapus akun tamu default RabbitMQ.
```
rabbitmqctl delete_user guest
```
14. <span id="Step6"></span>Jalankan perintah berikut untuk membuat akun.
```
rabbitmqctl add_user Nama Pengguna Kata Sandi
```
15. Jalankan perintah berikut untuk mengatur akun baru sebagai akun admin.
```
rabbitmqctl set_user_tags Nama pengguna administrator
```
16. Jalankan perintah berikut untuk memberikan semua izin kepada akun admin.
```
rabbitmqctl set_permissions -p / Username ".*" ".*" ".*"
```


### Memverifikasi penginstalan
1. Jalankan perintah berikut untuk membuka halaman manajemen Web RabbitMQ.
```
rabbitmq-plugins enable rabbitmq_management
```
2. Buka browser dan kunjungi:
```
http://Instance public IP:15672
```
Untuk informasi selengkapnya tentang cara mendapatkan alamat IP publik instans, lihat [Mendapatkan Alamat IP Publik](https://intl.cloud.tencent.com/document/product/213/17940).
Jika Anda melihat halaman berikut, ini menunjukkan bahwa RabbitMQ telah berhasil diinstal.
![](https://main.qcloudimg.com/raw/aacb15db11b5cf80dd6b7ba1dc80d331.png)
3. Login ke RabbitMQ dengan akun admin yang dibuat di [Langkah 6](#Step6) dan akses halaman manajemen RabbitMQ, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/7f8d24062541be6ba8b271483343b20a.png)
