## Skenario Operasi

Grup keamanan adalah firewall virtual guna memfilter paket dan digunakan untuk mengatur kontrol akses jaringan untuk satu atau beberapa CVM. Ini adalah metode isolasi keamanan jaringan penting yang disediakan oleh Tencent Cloud. Saat membuat instans CVM, Anda harus mengonfigurasi grup keamanannya. Tencent Cloud memungkinkan Anda mengonfigurasi grup keamanan baru untuk instans CVM setelah dibuat.
> Untuk mengonfigurasi grup keamanan baru untuk instans, buat grup keamanan terlebih dahulu. Untuk informasi selengkapnya, lihat [Membuat Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34271).

## Prasyarat

Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).

## Petunjuk

### Mengubah grup keamanan yang dikonfigurasi

Untuk meningkatkan pengalaman Anda di Konsol CVM, grup keamanan dapat dikonfigurasi di halaman manajemen instans atau di halaman detail instans.

#### Mengonfigurasi grup keamanan di halaman manajemen instans

1. Pilih CVM yang akan ditetapkan ulang ke grup keamanan baru di halaman manajemen instans dan klik **More** (Lainnya) > **Security Groups** (Grup Keamanan) > **Configure Security Groups** (Konfigurasi Grup Keamanan), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/68a30faac347446e57d87e8a1c30ef11.png)
2. Pada jendela pop-up “Configure Security Group” (Konfigurasi Grup Keamanan), periksa nama grup keamanan baru (beberapa nama dapat dipilih) dan klik **Confirm** (Konfirmasi) untuk mengubah grup keamanan.
 
#### Mengonfigurasi grup keamanan di halaman detail instans
 
1. Pada halaman manajemen instans, klik ID/nama instans CVM yang ingin Anda ubah grup keamanannya dan masuk ke halaman detail instans.
2. Klik **More Actions** (Tindakan Lainnya) > **Security Groups** (Grup Keamanan) > **Configure Security Groups** (Konfigurasi Grup Keamanan) di sudut kanan atas halaman detail instans, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/c7a1d76159feaa66f52eb16c7787432d.png)
3. Pada jendela pop-up “Configure Security Group” (Konfigurasi Grup Keamanan), periksa nama grup keamanan baru (beberapa nama dapat dipilih) dan klik **Confirm** (Konfirmasi).

### Mengubah grup keamanan terikat

1. Pada halaman manajemen instans, klik ID/nama instans CVM yang ingin Anda ikat grup keamanannya dan masuk ke halaman detail instans.
2. Pada halaman detail instans, pilih tab **Security Groups** (Grup Keamanan) dan klik **Bind** (Ikat) pada kolom “Ikat ke grup keamanan”, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/2ea553a1f2f589c6202245addfd62523.png)
3. Pada jendela pop-up “Security Groups” (Grup Keamanan), centang nama grup keamanan (beberapa nama dapat dipilih) untuk diikat berdasarkan kebutuhan Anda yang sebenarnya, lalu klik **OK** (OKE) untuk mengikat grup keamanan.
![](https://main.qcloudimg.com/raw/ac58322e8b11db8497d79eb54ecc67f6.png)
