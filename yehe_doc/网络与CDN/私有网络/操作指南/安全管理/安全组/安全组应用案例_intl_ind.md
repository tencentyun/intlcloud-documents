Grup keamanan digunakan untuk mengelola apakah Cloud Virtual Machine (CVM) dapat diakses. Anda dapat mengonfigurasi aturan masuk dan keluar untuk grup keamanan guna menentukan apakah server Anda dapat diakses oleh atau dapat mengakses sumber daya jaringan lainnya.
Aturan masuk dan keluar default untuk grup keamanan adalah sebagai berikut:
- **Untuk memastikan keamanan data, aturan masuk untuk grup keamanan adalah kebijakan penolakan yang menolak akses jarak jauh dari jaringan eksternal.** Agar CVM dapat diakses oleh sumber daya eksternal, Anda harus mengizinkan aturan masuk untuk port yang sesuai.
- Aturan keluar untuk grup keamanan menentukan apakah CVM Anda dapat mengakses sumber daya jaringan eksternal. Jika Anda memilih **Open All Ports** (Buka Semua Port) atau **Open Ports 22, 80, 443, and 3389 and ICMP** (Buka Port 22, 80, 443, dan 3389 dan ICMP), aturan keluar untuk grup keamanan akan membuka port ke internet. Jika Anda memilih aturan grup keamanan kustom, aturan keluar akan memblokir semua port secara default, dan Anda perlu menetapkan aturan keluar untuk mengizinkan port terkait mengakses sumber daya jaringan eksternal.

## Kasus Penggunaan Umum
Dokumen ini menjelaskan beberapa kasus penggunaan umum untuk grup keamanan. Jika salah satu kasus berikut memenuhi persyaratan Anda, Anda dapat mengatur grup keamanan Anda sesuai dengan konfigurasi yang direkomendasikan untuk kasus penggunaan yang sesuai.

### Skenario 1: menghubungkan CVM Linux dari jarak jauh melalui SSH
**Case** (Kasus): Anda telah membuat CVM Linux dan ingin terhubung ke CVM dari jarak jauh melalui SSH.
**Solution** (Solusi): saat [menambahkan aturan masuk](https://intl.cloud.tencent.com/document/product/215/35513), atur **Type** (Jenis) ke **Linux Login** (Login Linux) dan buka port TCP 22 ke internet untuk mengizinkan login Linux melalui SSH.
Anda dapat membuka semua alamat IP atau alamat IP tertentu (atau rentang alamat IP) ke internet sesuai kebutuhan. Tindakan ini mengizinkan Anda untuk mengonfigurasi alamat IP sumber yang dapat mengakses CVM dari jarak jauh melalui SSH.
<table>
<tr><th>Arah</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Login Linux</td><td><ul style="margin: 0;"><li>Semua alamat IP: 0.0.0.0/0</li><li>Alamat IP yang ditentukan: alamat IP atau rentang alamat IP tertentu</li></ul></td><td>TCP: 22</td><td>Izinkan</td></tr>
</table>

### Skenario 2: menghubungkan dari jarak jauh ke Windows CVM melalui RDP
**Case** (Kasus): Anda telah membuat CVM Windows dan ingin terhubung ke CVM dari jarak jauh melalui Koneksi Desktop Jarak Jauh (RDP).
**Solution** (Solusi): saat [menambahkan aturan masuk](https://intl.cloud.tencent.com/document/product/215/35513), atur **Type** (Jenis) ke **Windows Login** (Login Windows) dan buka port TCP 3389 ke internet untuk mengaktifkan login jarak jauh ke Windows.
Anda dapat membuka semua alamat IP atau alamat IP tertentu (atau rentang alamat IP) ke internet sesuai kebutuhan. Ini mengizinkan Anda untuk mengonfigurasi alamat IP sumber yang dapat mengakses CVM dari jarak jauh melalui RDP.
<table>
<tr><th>Arah</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Login Windows</td><td><ul style="margin: 0;"><li>Semua alamat IP: 0.0.0.0/0</li><li>Alamat IP yang ditentukan: alamat IP atau rentang alamat IP tertentu</li></ul></td><td>TCP: 3389</td><td>Izinkan</td></tr>
</table>

### Skenario 3: melakukan ping CVM dari internet
**Case** (Kasus): Anda telah membuat CVM dan ingin memeriksa apakah komunikasi antara CVM dan CVM lain normal.
**Solution** (Solusi): uji koneksi dengan menggunakan program ping. Khususnya, saat [menambahkan aturan masuk](https://intl.cloud.tencent.com/document/product/215/35513), atur **Type** (Jenis) ke **Ping** (Ping) dan buka port Internet Control Message Protocol (ICMP) ke internet untuk memungkinkan CVM lain mendapatkan akses ke CVM ini melalui ICMP.
Anda dapat membuka semua alamat IP atau alamat IP tertentu (atau rentang alamat IP) ke internet sesuai kebutuhan. Tindakan ini memungkinkan Anda untuk mengonfigurasi alamat IP sumber yang dapat mengakses CVM ini melalui ICMP.
<table>
<tr><th>Arah</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Ping</td><td><ul style="margin: 0;"><li>Semua alamat IP: 0.0.0.0/0</li><li>Alamat IP tertentu: alamat IP atau rentang alamat tertentu</li></ul></td><td>ICMP</td><td>Izinkan</td></tr>
</table>

### Skenario 4: login jarak jauh ke CVM melalui Telnet
**Case** (Kasus): Anda ingin login jarak jauh ke CVM melalui Telnet.
**Solution** (Solusi): saat [menambahkan aturan masuk](https://intl.cloud.tencent.com/document/product/215/35513), konfigurasi aturan grup keamanan berikut:
<table>
<tr><th>Arah</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Kustom</td><td><ul style="margin: 0;"><li>Semua alamat IP: 0.0.0.0/0</li><li>Alamat IP yang ditentukan: alamat IP atau rentang alamat IP tertentu</li></ul></td><td>TCP: 23</td><td>Izinkan</td></tr>
</table>

### Skenario 5: mengotorisasi akses ke layanan web melalui HTTP atau HTTPS
**Case** (Kasus): Anda telah membuat situs web dan ingin mengizinkan pengguna mengakses situs web Anda melalui HTTP atau HTTPS.
**Solution** (Solusi): saat [menambahkan aturan masuk](https://intl.cloud.tencent.com/document/product/215/35513), konfigurasi aturan grup keamanan berikut sesuai kebutuhan:
- Izinkan semua alamat IP di internet untuk mengakses situs web ini
<table>
<tr><th>Arah</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>HTTP (80)</td><td>0.0.0.0/0</td><td>TCP: 80</td><td>Izinkan</td></tr>
<tr><td>Masuk</td><td>HTTPS (443)</td><td>0.0.0.0/0</td><td>TCP: 443</td><td>Izinkan</td></tr>
</table>
- Izinkan beberapa alamat IP di internet untuk mengakses situs web ini
<table>
<tr><th>Arah</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>HTTP (80)</td><td>Alamat IP atau rentang alamat IP yang diizinkan untuk mengakses situs web Anda</td><td>TCP: 80</td><td>Izinkan</td></tr>
<tr><td>Masuk</td><td>HTTPS (443)</td><td>Alamat IP atau rentang alamat IP yang diizinkan untuk mengakses situs web Anda</td><td>TCP: 443</td><td>Izinkan</td></tr>
</table>

### Skenario 6: mengizinkan alamat IP eksternal untuk mengakses port tertentu
**Case** (Kasus): Anda telah men-deploy layanan dan ingin port layanan tertentu (seperti port 1101) dapat diakses secara eksternal.
**Solution** (Solusi): saat [menambahkan aturan masuk](https://intl.cloud.tencent.com/document/product/215/35513), atur **Type** (Jenis) ke **Custom** (Kustom) dan buka port TCP 1101 ke internet untuk mengizinkan sumber daya eksternal mengakses port layanan tertentu.
Anda dapat membuka semua alamat IP atau alamat IP tertentu (atau rentang alamat IP) ke internet sesuai kebutuhan. Tindakan ini memungkinkan alamat IP sumber untuk mengakses port layanan tertentu.
<table>
<tr><th>Arah</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Kustom</td><td><ul style="margin: 0;"><li>Semua alamat IP: 0.0.0.0/0</li><li>Alamat IP yang ditentukan: alamat IP atau rentang alamat IP tertentu</li></ul></td><td>TCP: 1101</td><td>Izinkan</td></tr>
</table>

### Skenario 7: menolak akses ke port tertentu dari alamat IP eksternal
**Case** (Kasus): Anda telah men-deploy layanan dan ingin memblokir akses eksternal ke port layanan tertentu (seperti port 1102).
**Solution** (Solusi): saat [menambahkan aturan masuk](https://intl.cloud.tencent.com/document/product/215/35513), atur **Type** (Jenis) ke **Custom** (Kustom), konfigurasi port TCP 1102, dan atur **Policy** (Kebijakan) ke **Reject** (Tolak) untuk menolak akses eksternal ke port layanan tertentu.
<table>
<tr><th>Arah</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Kustom</td><td><ul style="margin: 0;"><li>Semua alamat IP: 0.0.0.0/0</li><li>Alamat IP yang ditentukan: alamat IP atau rentang alamat IP tertentu</li></ul></td><td>TCP: 1102</td><td>Tolak</td></tr>
</table>

### Skenario 8: mengizinkan CVM hanya mengakses alamat IP eksternal tertentu
**Case** (Kasus): Anda ingin CVM Anda hanya mengakses alamat IP eksternal yang ditentukan.
**Solution** (Solusi): tambahkan dua aturan grup keamanan keluar dengan mengacu pada konfigurasi berikut:
- Izinkan instans CVM mengakses alamat IP publik tertentu
- Larang instans CVM mengakses alamat IP publik apa pun melalui protokol apa pun

> Aturan yang mengizinkan akses harus memiliki prioritas lebih tinggi dari aturan yang menolak akses.
>
<table>
<tr><th>Arah</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Keluar</td><td>Kustom</td><td>Alamat IP publik tertentu yang dapat diakses oleh CVM</td><td>Protokol dan port yang diperlukan</td><td>Izinkan</td></tr>
<tr><td>Keluar</td><td>Kustom</td><td>0.0.0.0/0</td><td>Semua</td><td>Tolak</td></tr>
</table>

### Skenario 9: menolak CVM mengakses alamat IP eksternal tertentu
**Case** (Kasus): Anda tidak ingin CVM Anda mengakses alamat IP eksternal yang ditentukan.
**Solution** (Solusi): tambahkan aturan grup keamanan dengan mengacu pada konfigurasi berikut:
<table>
<tr><th>Arah</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Keluar</td><td>Kustom</td><td>Alamat IP publik tertentu yang tidak ingin diakses oleh CVM</td><td>Semua</td><td>Tolak</td></tr>
</table>

### Skenario 10: mengunggah file ke atau mengunduh file dari CVM melalui FTP
**Case** (Kasus): Anda ingin mengunggah file ke atau mengunduh file dari CVM dengan menggunakan program FTP.
**Solution** (Solusi): tambahkan aturan grup keamanan dengan mengacu pada konfigurasi berikut:
<table>
<tr><th>Arah</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Kustom</td><td>0.0.0.0/0</td><td>TCP: 20-21</td><td>Izinkan</td></tr>
</table>

## Kombinasi Beberapa Skenario
Dalam skenario aktual, Anda mungkin ingin mengonfigurasi beberapa aturan grup keamanan berdasarkan persyaratan layanan, misalnya, mengonfigurasi aturan masuk atau keluar secara bersamaan. Satu CVM mungkin terikat ke satu atau lebih grup keamanan. Ketika CVM terikat ke beberapa grup keamanan, grup keamanan ini dicocokkan dan dijalankan dalam urutan prioritas yang menurun. Anda dapat menyesuaikan prioritas grup keamanan ini kapan pun diperlukan. 

