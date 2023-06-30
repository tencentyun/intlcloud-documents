## Ikhtisar
Jika Anda memilih bandwidth dengan batas atas 0 Mbps saat membeli CVM, CVM tidak akan dapat mengakses jaringan publik. Dokumen ini menggunakan CentOS 7.5 sebagai contoh untuk menjelaskan bagaimana CVM tanpa alamat IP publik dapat mengakses jaringan publik dengan menghubungkan ke CVM dengan alamat IP publik melalui VPN PPTP.


## Prasyarat
- Dua CVM dalam instans VPC yang sama telah dibuat. Satu **CVM does not have a public IP address** (CVM tidak memiliki alamat IP publik) dan **CVM has a public IP address** (CVM lainnya memiliki alamat IP publik).
- Alamat IP pribadi CVM dengan alamat IP publik telah diperoleh.

## Petunjuk
### Mengonfigurasi PPTP pada CVM dengan alamat IP publik

1. Login ke CVM dengan alamat IP publik.
2. Jalankan perintah berikut untuk menginstal PPTP:
```
yum install -y pptpd
```
3. Jalankan perintah berikut untuk membuka file konfigurasi `pptpd.conf`:
```
vim /etc/pptpd.conf
```
4. Tekan **i** (i) untuk beralih ke mode pengeditan dan tambahkan kode berikut di bagian bawah file.
```
localip 192.168.0.1
remoteip 192.168.0.234-238,192.168.0.245
```
5. Tekan **Esc** (Esc), masukkan **:wq** (:wq), lalu simpan dan tutup file.
6. Jalankan perintah berikut untuk membuka file konfigurasi `/etc/ppp/chap-secrets`:
```
vim /etc/ppp/chap-secrets
```
7. <span id="step7">Tekan **i** (i) untuk beralih ke mode pengeditan dan menambahkan nama pengguna dan kata sandi untuk menghubungkan ke PPTP dalam format berikut di bagian bawah file.</span>
```
<Username>    pptpd    <Password>    *
```
Misalnya, jika nama pengguna dan kata sandi untuk menghubungkan ke PPTP masing-masing adalah root dan 123456, tambahkan kode berikut:
```
root    pptpd    123456    *
```
8. Tekan **Esc** (Esc), masukkan **:wq** (:wq), lalu simpan dan tutup file.
9. Jalankan perintah berikut untuk memulai layanan PPTP:
```
systemctl start pptpd
```
10. Jalankan perintah berikut secara berurutan untuk mengaktifkan penerusan:
```
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -o eth0 -s 192.168.0.0/24 -j MASQUERADE
```

### Mengonfigurasi PPTP pada CVM tanpa alamat IP publik

1. Login ke CVM tanpa alamat IP publik.
2. Jalankan perintah berikut untuk menginstal klien PPTP:
```
yum install -y pptp pptp-setup
``` 
3. Jalankan perintah berikut untuk membuat file konfigurasi:
```
pptpsetup --create <Configuration file name> --server <Private IP address of the CVM with a public IP address> --username <Username for connecting to PPTP> --password <Password for connecting to PPTP> --encrypt
```
Misalnya, jika Anda telah memperoleh alamat IP pribadi 10.100.100.1 dari CVM dengan alamat IP publik, jalankan perintah berikut untuk membuat file konfigurasi pengujian:
```
pptpsetup --create test --server 10.100.100.1 --username root --password 123456 --encrypt
```
4. Jalankan perintah berikut untuk terhubung ke PPTP:
```
pppd call test (nama file konfigurasi yang dibuat pada langkah 3)
```
5. Jalankan perintah berikut untuk mengatur rute:
```
route add -net 10.0.0.0/8 dev eth0
route add -net 172.16.0.0/12 dev eth0
route add -net 192.168.0.0/16 dev eth0
route add -net 169.254.0.0/16 dev eth0
route add -net 9.0.0.0/8 dev eth0
route add -net 100.64.0.0/10 dev eth0
route add -net 0.0.0.0 dev ppp0
```

### Memeriksa apakah konfigurasi berhasil
Jalankan perintah berikut pada CVM tanpa alamat IP publik untuk melakukan ping ke alamat jaringan eksternal apa pun dan periksa apakah alamat tersebut dapat di-ping melalui:
```
ping -c 4 <External network address>
```
Jika hasil yang mirip dengan berikut ini ditampilkan, artinya konfigurasi berhasil:
![](https://main.qcloudimg.com/raw/c841782ce0976982d1f289d3437ec0ed.png)



