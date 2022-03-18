## Skenario

Mulai 1 Maret 2018, citra publik Linux yang disediakan oleh Tencent Cloud memiliki fitur sumber terbuka Cloud-Init yang telah diinstal sebelumnya, dan semua operasi inisialisasi pada sebuah instans akan dilakukan melalui Cloud-Init, sehingga membuat operasi internal instans menjadi lebih transparan. Untuk informasi selengkapnya, lihat Cloud-Init.
Dalam **each launch** (setiap peluncuran), Cloud-Init menghasilkan file `/etc/hosts` baru sesuai dengan templat `/etc/cloud/templates/hosts.${os_type}.tmpl` dan menimpa file `/etc/hosts` asli dari instans. Dengan demikian, setelah pengguna secara manual memodifikasi konfigurasi `/etc/hosts` internal instans dan memulai ulang, konfigurasi `/etc/hosts` akan kembali ke konfigurasi default asli.

## Prasyarat
Tencent Cloud telah memperbaiki masalah ini untuk instans yang dibuat **after September 2018** (setelah September 2018), dan konfigurasi `/etc/hosts` tidak akan ditimpa.
Untuk instans yang dibuat **before September 2018** (sebelum September 2018), ikuti langkah-langkah di bawah ini untuk modifikasi.

## Langkah-Langkah

### Solusi 1 
1. Login ke CVM Linux.
2. Jalankan perintah berikut untuk mengubah `- update_etc_hosts` di file konfigurasi `/etc/cloud/cloud.cfg` menjadi `- ['update-etc-hosts', 'once-per-instans']`.
```
sed -i "/update_etc_hosts/c \ - ['update_etc_hosts', 'once-per-instance']" /etc/cloud/cloud.cfg
```
3. Jalankan perintah berikut untuk membuat file `config_update_etc_hosts` di bawah jalur `/var/lib/cloud/instans/sem/`.
```
touch /var/lib/cloud/instance/sem/config_update_etc_hosts
```

### Solusi 2
>Solusi ini mengambil sistem operasi CentOS 7.2 sebagai contoh.
>
#### Mendapatkan Jalur File Templat `hosts`
1. Login ke CVM Linux.
2. Jalankan perintah berikut untuk melihat file templat `hosts` sistem.
```
cat /etc/hosts
```
File templat `hosts` adalah seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/f51f9c53004574f72d32f5ed790c8563.png)


#### Memodifikasi File Templat `hosts`
>Dengan menambahkan `127.0.0.1 test test` sebagai contoh, Anda dapat memodifikasi templat `hosts` dan file `/etc/hosts` sesuai kebutuhan.
>
1. Jalankan perintah berikut untuk memodifikasi file templat `hosts`.
```
vim /etc/cloud/templates/hosts.redhat.tmpl
```
2. Tekan **i** (i) atau **Insert** (Sisipkan) untuk beralih ke mode pengeditan.
3. Tambahkan konten berikut ke bagian akhir file.
```
127.0.0.1 test test
```
4. Tekan **Esc** (Esc), masukkan **:wq** (:wq), simpan lalu kembalikan file.

#### Memodifikasi File /etc/hosts
1. Jalankan perintah berikut untuk memodifikasi file `/etc/hosts`.
```
vim /etc/hosts
```
2. Tekan **i** (i) atau **Insert** (Sisipkan) untuk beralih ke mode pengeditan.
3. Tambahkan konten berikut ke bagian akhir file.
```
127.0.0.1 test test
```
4. Tekan **Esc** (Esc), masukkan **:wq** (:wq), simpan lalu kembalikan file.
