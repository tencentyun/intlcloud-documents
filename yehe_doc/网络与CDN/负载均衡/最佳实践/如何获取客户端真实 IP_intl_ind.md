## Catatan tentang Mendapatkan IP Klien Nyata dengan CLB
Semua layanan CLB lapisan 4 (TCP/UDP/TCP SSL) dan lapisan 7 (HTTP/HTTPS) dapat digunakan untuk memperoleh IP klien nyata langsung di instance CVM backend tanpa memerlukan konfigurasi tambahan.
- Untuk CLB lapisan 4, IP sumber yang didapatkan di instance CVM backend merupakan IP klien.
- Untuk CLB lapisan 7, Anda dapat menggunakan bidang `X-Forwarded-For` atau `remote_addr` untuk mendapatkan IP klien secara langsung.Untuk melihat log akses CLB lapisan 7, silakan lihat [Menyimpan Log Akses di CLS](https://intl.cloud.tencent.com/document/product/214/35063).

>?
>- Untuk instance CLB lapisan 4, IP klien bisa didapatkan secara langsung tanpa memerlukan konfigurasi tambahan pada instance CVM backend.
>- Untuk layanan penyeimbangan beban lapisan 7 lainnya yang mengaktifkan SNAT, Anda perlu mengonfigurasi instance CVM backend kemudian menggunakan `X-Forwarded-For` untuk mendapatkan IP klien nyata.

Berikut adalah skema konfigurasi server aplikasi yang biasa digunakan.

## Skema Konfigurasi IIS 6
1.Unduh dan instal modul plugin [F5XForwardedFor](https://devcentral.f5.com/s/articles/x-forwarded-for-log-filter-for-windows-servers), salin `F5XForwardedFor.dll` dari direktori `x86\Release` atau `x64\Release`, tergantung versi sistem pengoperasian server Anda, ke direktori tertentu (seperti `C:\ISAPIFilters` di dokumen ini), dan pastikan bahwa proses IIS memiliki izin untuk membaca direktori ini.
2.Buka Pengelola IIS, cari situs web yang saat ini sedang dibuka, klik kanan pada situs web tersebut, lalu pilih **Properties** (Properti) untuk membuka halaman properti.
3.Di halaman properti, ubah ke **ISAPI Filters** (Filter ISAPI) lalu klik **Add** (Tambahkan) untuk memunculkan jendela "Add" (Tambahkan).
4.Di jendela "Add" (Tambahkan), masukkan "F5XForwardedFor" pada bagian "Filter Name" (Nama Filter) dan path lengkap menuju `F5XForwardedFor.dll` pada bagian "Executable" (Dapat Dijalankan) lalu klik **OK**.
5.Mulai ulang server IIS agar konfigurasi diterapkan.

## Skema Konfigurasi IIS 7
1.Unduh dan instal modul plugin [F5XForwardedFor](https://devcentral.f5.com/s/articles/x-forwarded-for-log-filter-for-windows-servers), salin `F5XFFHttpModule.dll` dan `F5XFFHttpModule.ini` dari direktori `x86\Release` atau `x64\Release`, tergantung versi sistem pengoperasian server Anda, ke direktori tertentu (seperti `C:\x_forwarded_for` di dokumen ini), dan pastikan bahwa proses IIS memiliki izin untuk membaca direktori ini.
2.Pilih **IIS Server** (Server IIS) lalu klik dua kali pada **Modules** (Modul).
![](https://main.qcloudimg.com/raw/21372379584488e72ae3d22af44a5017.png)
3.Klik **Configure Native Modules** (Konfigurasi Modul Native).
![](https://main.qcloudimg.com/raw/280f11e95b7ac8cd4a754d98ad0cd2b7.png)
4.Klik **Register** (Daftar) di kotak pop-up.
![](https://main.qcloudimg.com/raw/1d6f7bd38077f2c9f089eb84a1995aa1.png)
5.Tambahkan file DLL yang telah diunduh seperti berikut ini:
![](https://main.qcloudimg.com/raw/354a35a203c24d802d59782c91dfe02a.png)
6.Periksa sekali lagi setelah menambahkan file DLL tersebut, lalu klik **OK**.
![](https://main.qcloudimg.com/raw/9fffdfa02fba225f13090ef2598e1c0e.png)
7.Tambahkan dua file DLL di atas ke "ISAPI and CGI Restrictions" (Pembatasan ISAPI dan CGI) lalu atur pembatasannya menjadi "Allow" (Izinkan).
![](https://main.qcloudimg.com/raw/8585122da39f14d734eb9d6ded7e486c.png)
8.Mulai ulang server IIS agar konfigurasi diterapkan.

## Skema Konfigurasi Apache
1.Instal modul Apache pihak ketiga "mod_rpaf".
```
wget http://stderr.net/apache/rpaf/download/mod_rpaf-0.6.tar.gz
tar zxvf mod_rpaf-0.6.tar.gz
cd mod_rpaf-0.6
/usr/bin/apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
```
2.Modifikasi konfigurasi Apache `/etc/httpd/conf/httpd.conf` dengan menambahkan tulisan berikut pada bagian akhir file:
```
LoadModule rpaf_module modules/mod_rpaf-2.0.so
RPAFenable On
RPAFsethostname On
RPAFproxy_ips IP address (yang dimaksud bukanlah IP publik yang disediakan oleh CLB. Kueri log Apache untuk mengetahui IP spesifiknya. Umumnya, terdapat dua alamat IP dan Anda perlu memasukkan keduanya)
RPAFheader X-Forwarded-For
```
3.Setelah menambahkan tulisan di atas, mulai ulang Apache.
```
/usr/sbin/apachectl restart
```

## Skema Konfigurasi Nginx
1.Anda bisa menggunakan `http_realip_module` untuk mendapatkan IP klien nyata ketika menggunakan Nginx sebagai server.Namun, modul ini tidak terpasang dalam Nginx secara default dan Anda perlu menyusun ulang Nginx untuk menambahkan `--with-http_realip_module`.
```
wget  http://nginx.org/download/nginx-1.14.0.tar.gz
tar  zxvf nginx-1.14.0.tar.gz
cd nginx-1.14.0
./configure --user=www --group=www --with-http_stub_status_module --without-http-cache --with-http_ssl_module --with-http_realip_module
make
make install
```
2.Modifikasi `nginx.conf`.
```
vi /etc/nginx/nginx.conf
```
Modifikasi konten yang berwarna merah seperti berikut ini:
<div class="code">
<p>
</p>
<pre>
fastcgi connect_timeout 300;
fastcgi send_timeout 300;
fastcgi read_timeout 300;
fastcgi buffer_size 64k;
fastcgi buffers 4 64k;
fastcgi busy_buffers_size 128k;
fastcgi temp_file_write_size 128k;
<font color="#f2777a">
set_real_ip_from IP address; (yang dimaksud bukanlah IP publik yang disediakan oleh CLB. Kueri log Nginx untuk mengetahui IP spesifiknya. Jika terdapat lebih dari satu alamat IP, Anda perlu memasukkan semuanya)
real_ip_header X-Forwarded-For;
</font>
</pre>
</div>
3.Mulai ulang Nginx.
```
mulai ulang layanan nginx
```
