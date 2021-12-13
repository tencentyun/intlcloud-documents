Grup keamanan dapat mengelola akses ke CVM. Anda dapat mengonfigurasi aturan masuk dan keluar untuk grup keamanan guna menentukan apakah server Anda dapat diakses oleh atau dapat mengakses sumber daya jaringan lainnya.
Aturan masuk dan keluar default untuk grup keamanan adalah sebagai berikut:
- **To ensure data security, the inbound rule for a security group is a rejection policy that forbids remote access from external networks.** (Untuk memastikan keamanan data, aturan masuk untuk grup keamanan berupa kebijakan penolakan yang melarang akses jarak jauh dari jaringan eksternal.) Untuk mengaktifkan akses publik ke CVM Anda, Anda perlu membuka port yang sesuai ke Internet dalam aturan masuk.
- Aturan keluar untuk grup keamanan menentukan apakah CVM Anda dapat mengakses sumber daya jaringan eksternal. Jika Anda memilih **Open all ports** (Buka semua port) atau **Open ports 22, 80, 443, and 3389 and the ICMP protocol** (Buka port 22, 80, 443, dan 3389 dan protokol ICMP), aturan keluar untuk grup keamanan akan membuka semua port ke Internet. Jika Anda memilih aturan grup keamanan kustom, aturan keluar akan memblokir semua port secara default, dan Anda perlu mengonfigurasi aturan keluar untuk membuka port terkait ke Internet.

## Kasus Penggunaan Umum
Dokumen ini menyediakan beberapa kasus penggunaan umum grup keamanan. Anda dapat langsung menggunakan konfigurasi grup keamanan yang direkomendasikan jika kasus penggunaan memenuhi persyaratan Anda.

### Skenario 1: menghubungkan CVM Linux dari jarak jauh melalui SSH
**Case** (Kasus): Anda telah membuat CVM Linux dan ingin menghubungkannya dari jarak jauh melalui SSH.
**Solution** (Solusi): saat [menambahkan aturan grup keamanan](https://intl.cloud.tencent.com/document/product/213/34272), atur **Type** (Jenis) ke **Login Linux CVMs(22)** (Login Linux CVM(22)), masukkan alamat IP proksi WebShell untuk **Source** (Sumber), dan buka port TCP 22 ke Internet untuk mengaktifkan login Linux melalui SSH.
Anda dapat membuka semua alamat IP atau alamat IP tertentu (atau rentang IP) ke Internet sesuai kebutuhan. Tindakan ini memungkinkan Anda mengonfigurasi alamat IP sumber CVM yang dapat dihubungkan dari jarak jauh melalui SSH.
<table>
<tr><th>Petunjuk</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Login Linux</td><td><ul style="margin: 0;"><li>Semua alamat IP: 0.0.0.0/0</li>
<li>Alamat IP proksi WebShell: seperti yang dijelaskan dalam <a href="https://cloud.tencent.com/document/product/213/52645">Pembaruan Alamat IP Proksi WebShell</a>
</li>
<li>Alamat IP yang ditentukan: masukkan alamat IP atau rentang IP yang Anda tentukan</li></ul></td><td>TCP:22</td><td>Izinkan</td></tr>
</table>

### Skenario 2: menghubungkan dari jarak jauh ke Windows CVM melalui RDP
**Case** (Kasus): Anda telah membuat CVM Windows dan ingin menghubungkannya dari jarak jauh menggunakan Remote Desktop (RDP).
**Solution** (Solusi): saat [menambahkan aturan grup keamanan](https://intl.cloud.tencent.com/document/product/213/34272), atur **Type** (Jenis) ke **Login Windows CVMs(3389)** (Login Windows CVM(3389)), masukkan alamat IP proksi WebRDP untuk **Source** (Sumber), dan buka port TCP 3389 ke Internet untuk mengaktifkan login jarak jauh ke Windows.
Anda dapat membuka semua alamat IP atau alamat IP tertentu (atau rentang IP) ke Internet sesuai kebutuhan. Tindakan ini memungkinkan Anda mengonfigurasi alamat IP sumber CVM yang dapat dihubungkan dari jarak jauh melalui RDP.
<table>
<tr><th>Petunjuk</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Login Windows</td><td></td><td><ul style="margin: 0;"><li>Semua alamat IP: 0.0.0.0/0</li>
<li>Alamat IP proksi WebRDP:
 <ol>81.69.102.0/24</ol>
<ol>106.55.203.0/24</ol>
<ol>101.33.121.0/24</ol>
<ol>101.32.250.0/24</ol>
</li>
<li>Alamat IP yang ditentukan: masukkan alamat IP atau rentang IP yang Anda tentukan</li></ul></td><td>TCP:3389</td><td>Izinkan</td></tr>
</table>

### Skenario 3: melakukan ping ke CVM di Internet
**Case** (Kasus): Anda telah membuat CVM dan ingin menguji apakah komunikasinya dengan CVM lain normal.
**Solution** (Solusi): uji koneksi dengan menggunakan perintah `ping`. Khususnya, saat [menambahkan aturan grup keamanan](https://intl.cloud.tencent.com/document/product/213/34272), atur **Type** (Jenis) ke **Ping** (Ping) dan buka port Internet Control Message Protocol (ICMP) ke Internet untuk memungkinkan CVM lain mengakses CVM ini melalui ICMP.
Anda dapat membuka semua alamat IP atau alamat IP tertentu (atau rentang IP) ke Internet sesuai kebutuhan. Tindakan ini memungkinkan Anda mengonfigurasi alamat IP sumber CVM yang dapat mengakses CVM ini melalui ICMP.
<table>
<tr><th>Petunjuk</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Ping</td><td><ul style="margin: 0;"><li>Semua alamat IP: 0.0.0.0/0</li><li>Alamat IP yang ditentukan: masukkan alamat IP atau rentang IP yang Anda tentukan</li></ul></td><td>ICMP</td><td>Izinkan</td></tr>
</table>

### Skenario 4: login jarak jauh ke CVM melalui Telnet
**Case** (Kasus): Anda ingin login ke CVM dari jarak jauh dengan menggunakan Telnet.
**Solution** (Solusi): saat [menambahkan aturan grup keamanan](https://intl.cloud.tencent.com/document/product/213/34272), konfigurasikan aturan grup keamanan berikut:
<table>
<tr><th>Petunjuk</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Kustom</td><td><ul style="margin: 0;"><li>Semua alamat IP: 0.0.0.0/0</li><li>Alamat IP yang ditentukan: masukkan alamat IP atau rentang IP yang Anda tentukan</li></ul></td><td>TCP: 23</td><td>Izinkan</td></tr>
</table>

### Skenario 5: mengizinkan akses ke layanan web melalui HTTP atau HTTPS
**Case** (Kasus): Anda telah membuat situs web dan ingin mengizinkan akses ke situs web Anda melalui HTTP atau HTTPS.
**Solution** (Solusi): saat [menambahkan aturan grup keamanan](https://intl.cloud.tencent.com/document/product/213/34272), konfigurasikan aturan grup keamanan berikut sesuai kebutuhan:
- Izinkan semua alamat IP publik untuk mengakses situs web ini
<table>
<tr><th>Petunjuk</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>HTTP (80)</td><td>0.0.0.0/0</td><td>TCP: 80</td><td>Izinkan</td></tr>
<tr><td>Masuk</td><td>HTTPS (443)</td><td>0.0.0.0/0</td><td>TCP: 443</td><td>Izinkan</td></tr>
</table>
- Izinkan beberapa alamat IP publik untuk mengunjungi situs web ini.
<table>
<tr><th>Petunjuk</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>HTTP (80)</td><td>Alamat IP atau rentang IP yang diizinkan untuk mengakses situs web Anda</td><td>TCP: 80</td><td>Izinkan</td></tr>
<tr><td>Masuk</td><td>HTTPS (443)</td><td>Alamat IP atau rentang IP yang diizinkan untuk mengakses situs web Anda</td><td>TCP: 443</td><td>Izinkan</td></tr>
</table>

### Skenario 6: mengizinkan alamat IP eksternal untuk mengakses port tertentu
**Case** (Kasus): Anda telah men-deploy layanan dan ingin port layanan yang ditentukan (seperti port 1101) dapat diakses secara eksternal.
**Solution** (Solusi): saat [menambahkan aturan grup keamanan](https://intl.cloud.tencent.com/document/product/213/34272), atur **Type** (Jenis) ke **Custom** (Kustom) dan buka port TCP 1101 ke Internet untuk mengizinkan akses eksternal ke port layanan yang ditentukan.
Anda dapat membuka semua alamat IP atau alamat IP tertentu (atau rentang IP) ke Internet sesuai kebutuhan. Tindakan ini memungkinkan alamat IP sumber untuk mengakses port layanan yang ditentukan.
<table>
<tr><th>Petunjuk</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Kustom</td><td><ul style="margin: 0;"><li>Semua alamat IP: 0.0.0.0/0</li><li>Alamat IP yang ditentukan: masukkan alamat IP atau rentang IP yang Anda tentukan</li></ul></td><td>TCP: 1101</td><td>Izinkan</td></tr>
</table>

### Skenario 7: menolak alamat IP eksternal untuk mengakses port tertentu
**Case** (Kasus): Anda telah men-deploy layanan dan ingin mencegah akses eksternal ke port layanan tertentu (seperti port 1102).
**Solution** (Solusi): saat [menambahkan aturan grup keamanan](https://intl.cloud.tencent.com/document/product/213/34272), atur **Type** (Jenis) ke **Custom** (Kustom), konfigurasikan port TCP 1102, dan atur **Policy** (Kebijakan) ke **Reject ** (Tolak), sehingga layanan eksternal tidak dapat mengakses port layanan yang ditentukan.
<table>
<tr><th>Petunjuk</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Masuk</td><td>Kustom</td><td><ul style="margin: 0;"><li>Semua alamat IP: 0.0.0.0/0</li><li>Alamat IP yang ditentukan: masukkan alamat IP atau rentang IP yang Anda tentukan</li></ul></td><td>TCP: 1102</td><td>Tolak</td></tr>
</table>

### Skenario 8: mengizinkan CVM mengakses hanya alamat IP eksternal tertentu
**Case** (Kasus): Anda ingin CVM Anda hanya mengakses alamat IP eksternal yang ditentukan.
**Solution** (Solusi): tambahkan dua aturan grup keamanan keluar sebagai berikut.
- Izinkan instans CVM mengakses alamat IP eksternal yang ditentukan.
- Larang instans CVM mengakses alamat IP publik apa pun melalui protokol apa pun.

>! Aturan pertama lebih diprioritaskan daripada yang kedua.
>
<table>
<tr><th>Petunjuk</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Keluar</td><td>Kustom</td><td>Alamat IP publik tertentu yang dapat diakses CVM</td><td>Protokol dan nomor port yang diperlukan</td><td>Izinkan</td></tr>
<tr><td>Keluar</td><td>Kustom</td><td>0.0.0.0/0</td><td>Semua</td><td>Tolak</td></tr>
</table>

### Skenario 9: melarang CVM mengakses alamat IP eksternal tertentu
**Case** (Kasus): Anda tidak ingin CVM Anda mengakses alamat IP eksternal yang ditentukan.
**Solution** (Solusi): tambahkan aturan grup keamanan sebagai berikut.
<table>
<tr><th>Petunjuk</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>Keluar</td><td>Kustom</td><td>Alamat IP publik yang ditentukan yang tidak dapat diakses oleh instans CVM Anda</td><td>Semua</td><td>Tolak</td></tr>
</table>

### Skenario 10: mengunggah atau mengunduh file dari CVM melalui FTP
**Case** (Kasus): Anda ingin mengizinkan unggahan dan unduhan melalui FTP.
**Solution** (Solusi): tambahkan aturan grup keamanan sebagai berikut.
<table>
<tr><th>Petunjuk</th><th>Jenis</th><th>Sumber</th><th>Port Protokol</th><th>Kebijakan</th></tr>
<tr><td>TCP</td><td>Kustom</td><td>0.0.0.0/0</td><td>Masuk: 20 hingga 21</td><td>Izinkan</td></tr>
</table>

## Konfigurasi Multi-skenario
Anda dapat mengonfigurasi beberapa aturan grup keamanan untuk memenuhi kebutuhan bisnis Anda. Misalnya, aturan masuk dan keluar dapat dikonfigurasi secara bersamaan. Instans CVM dapat diikat ke satu atau beberapa grup keamanan. Ketika terikat ke beberapa grup keamanan, aturan grup keamanan akan dicocokkan secara berurutan dari atas ke bawah. Anda dapat menyesuaikan prioritas grup keamanan kapan saja. Untuk informasi selengkapnya tentang prioritas, lihat [Prioritas Aturan](https://intl.cloud.tencent.com/document/product/213/12452).



