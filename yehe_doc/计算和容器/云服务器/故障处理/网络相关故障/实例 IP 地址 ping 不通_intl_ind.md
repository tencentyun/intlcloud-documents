## Masalah

Server lokal gagal melakukan ping ke instans. Kemungkinan penyebabnya termasuk:
- Konfigurasi server tujuan salah
- Resolusi nama domain tidak berhasil
- Kegagalan tautan

Jika jaringan lokal normal (situs web lain dapat di-ping dari jaringan lokal), selesaikan masalah seperti berikut:
- [Periksa apakah instans dikonfigurasi dengan alamat IP publik](#isConfigurePublicIP).
- [Periksa konfigurasi grup keamanan](#CheckSecurityGroupSetting).
- [Periksa konfigurasi sistem operasi](#CheckOSSetting).
- [Lakukan operasi lain](#OtherOperations).

## Petunjuk

<span id="isConfigurePublicIP"></span>
### Memeriksa apakah instans dikonfigurasi dengan alamat IP publik

>? Sebuah instans dapat mengakses komputer lain di Internet hanya jika instans tersebut memiliki alamat IP publik. Jika tidak, instans tersebut tidak dapat di-ping melalui alamat IP pribadi.
>
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman "Instances" (Instans), pilih ID/nama instans yang akan di-ping untuk masuk ke halaman detail instans, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/12dfabc6420688ebb0dd0f1a8f4d7188.png)
3. Periksa apakah instans dikonfigurasi dengan alamat IP publik di "Network Information" (Informasi Jaringan).
 - Jika ya, [periksa konfigurasi grup keamanan](#CheckSecurityGroupSetting).
 - Jika tidak, [ikatkan alamat IP publik elastis ke instans](https://intl.cloud.tencent.com/document/product/213/16586).

<span id="CheckSecurityGroupSetting"></span>
### Memeriksa konfigurasi grup keamanan

Grup keamanan adalah firewall virtual yang mengontrol lalu lintas masuk dan keluar dari instans terkait. Anda dapat menentukan protokol, port, dan kebijakan dalam aturan grup keamanan. Karena ICMP digunakan dalam pengujian ping, Anda perlu memeriksa apakah protokol diizinkan dalam grup keamanan yang terkait dengan instans. Untuk melihat grup keamanan yang terkait dengan instans serta aturan masuk dan keluarnya, lakukan langkah-langkah berikut:
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman "Instances" (Instans), pilih ID/nama instans yang akan dikonfigurasi dengan grup keamanan untuk masuk ke halaman detail instans, seperti yang ditunjukkan pada gambar berikut:
3. Klik tab **Security Groups** (Grup Keamanan) untuk masuk ke halaman manajemen grup keamanan dari instans ini, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/bf5881258356a0af748ae16d9cf321a2.png)
4. Periksa grup keamanan yang terkait dengan instans dan aturan masuk dan keluar terperinci untuk menentukan apakah grup keamanan ini mengizinkan ICMP.
 - Jika ya, [periksa konfigurasi sistem operasi](#CheckOSSetting).
 - Jika tidak, konfigurasikan kebijakan protokol ICMP untuk mengizinkan.

<span id="CheckOSSetting"></span>
### Memeriksa konfigurasi sistem operasi

Berdasarkan sistem operasi instans, pilih metode untuk memeriksa konfigurasi:
- Untuk sistem operasi Linux, [periksa parameter kernel Linux dan konfigurasi firewall](#CheckLinux).
-Untuk sistem operasi Windows, [periksa konfigurasi firewall Windows](#CheckLinux).

<span id="CheckLinux"></span>
#### Memeriksa parameter kernel Linux dan konfigurasi firewall

>? Apakah pengujian ping diizinkan di sistem operasi Linux bergantung pada konfigurasi kernel dan firewall. Jika salah satu dari kernel dan firewall menolak pengujian ping, "Request timeout" (Waktu permintaan habis) terjadi.

##### Memeriksa parameter kernel icmp_echo_ignore_all

1. Login ke instans.
2. Jalankan perintah berikut untuk melihat konfigurasi sistem icmp_echo_ignore_all.
```
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
 - Jika 0 ditampilkan, semua permintaan ICMP Echo diizinkan oleh sistem. Dalam kasus ini, [periksa konfigurasi firewall](#CheckLinuxFirewall).
 - Jika 1 ditampilkan, semua permintaan ICMP Echo ditolak oleh sistem. Dalam kasus ini, lakukan [langkah 3](#Linux_step03).
3. <span id = "Linux_step03"> Jalankan perintah berikut untuk memodifikasi konfigurasi parameter kernel icmp_echo_ignore_all.</ span>
```
echo "0" >/proc/sys/net/ipv4/icmp_echo_ignore_all
```

<span id="CheckLinuxFirewall"></span>
##### Memeriksa konfigurasi firewall

Jalankan perintah berikut untuk memeriksa apakah aturan firewall dan aturan ICMP yang sesuai dari server saat ini dinonaktifkan:
```
iptables -L
```
- Jika hasil berikut ditampilkan, aturan ICMP tidak dinonaktifkan. Dalam kasus ini, [periksa apakah nama domain memiliki pengajuan ICP](#CheckDomainRegistration) (untuk nama domain yang dilayani di Tiongkok Daratan).
```
Chain INPUT (ACCEPT kebijakan)
target     sumber prot opt               tujuan         
ACCEPT     icmp --  di mana saja             di mana saja             icmp echo-request
Chain FORWARD (ACCEPT kebijakan)
target     sumber prot opt               tujuan         
Chain OUTPUT (ACCEPT kebijakan)
target     sumber prot opt               tujuan  
ACCEPT     icmp --  di mana saja             di mana saja             icmp echo-request
```
- Jika hasil pengembalian menunjukkan bahwa aturan ICMP dinonaktifkan, jalankan perintah berikut untuk mengaktifkannya.
```
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

<span id="CheckWindows"></span>
#### Memeriksa konfigurasi firewall Windows

1. Login ke instans.
2. Buka **Control Panel** (Panel Kontrol) dan pilih **Windows Firewall**.
3. Pada halaman "Windows Firewall", pilih **Advanced settings** (Pengaturan lanjutan).
4. Di jendela pop-up "Windows Firewall with Advanced Security" (Windows Firewall dengan Keamanan Lanjutan), periksa apakah aturan masuk dan keluar ICMP dinonaktifkan.
 - Jika aturan masuk dan keluar ICMP dinonaktifkan, harap aktifkan.


<span id="OtherOperations"></span>
### Operasi lainnya

Jika operasi sebelumnya tidak dapat memecahkan masalah, lihat berikut ini:
- Jika nama domain tidak dapat di-ping, periksa konfigurasi situs web Anda.
- Jika alamat IP publik tidak dapat di-ping, lampirkan informasi pada instans dan data MTR dua arah (dari server lokal ke CVM dan dari CVM ke server lokal), dan [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk menghubungi teknisi kami untuk bantuan.
Untuk informasi selengkapnya tentang cara menggunakan MTR, lihat [Latensi Jaringan CVM dan Kehilangan Paket](https://intl.cloud.tencent.com/document/product/213/14638).
