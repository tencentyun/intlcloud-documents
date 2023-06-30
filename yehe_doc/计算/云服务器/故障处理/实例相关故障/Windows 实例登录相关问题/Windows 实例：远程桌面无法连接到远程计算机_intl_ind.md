## Skenario
Saat mencoba menghubungkan dari jarak jauh ke instans Windows dari Windows, Anda akan diminta sesuai pesan yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/8c79cadc3e14c9c4e0cbb5303b79f74a.png)

Anda tidak dapat menghubungkan ke komputer jarak jauh menggunakan Desktop Jarak Jauh karena salah satu alasan berikut:
1) Akses jarak jauh ke server tidak diaktifkan.
2) Komputer jarak jauh mati.
3) Komputer jarak jauh tidak tersedia di jaringan.

Periksa apakah komputer jarak jauh hidup dan terhubung ke jaringan, dan akses jarak jauh diaktifkan.


## Kemungkinan Penyebab

Kemungkinan penyebab masalah ini termasuk namun tidak terbatas pada hal-hal berikut. Memecahkan masalah berdasarkan keadaan aktual Anda.
- Instans dalam status tidak normal.
- CVM tidak memiliki alamat IP publik atau bandwidth jaringan publik adalah 0.
- Port login jarak jauh (port 3389 secara default) tidak dibuka ke Internet dalam grup keamanan yang terikat dengan instans.
- Layanan Desktop Jarak Jauh belum dimulai.
- Pengaturan Desktop Jarak Jauh salah.
- Pengaturan Windows Firewall salah.

## Langkah Pemecahan Masalah

### Memeriksa apakah instans sedang berjalan
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman manajemen instans, periksa apakah instans **Running** (Berjalan), seperti yang ditunjukkan pada gambar berikut:
![Halaman daftar CVM](https://main.qcloudimg.com/raw/03cf75228bc468d2e436f876f229ebc9.png)
 - Jika ya, [periksa apakah CVM memiliki alamat IP publik](#step01).
 - Jika tidak, jalankan instans Windows.

<span id="step01"></span>
### Memeriksa apakah CVM memiliki alamat IP publik
Periksa apakah CVM memiliki alamat IP publik di konsol CVM, seperti yang ditunjukkan pada gambar berikut:
![Tidak ada alamat IP publik](https://main.qcloudimg.com/raw/58c75d68372069652ec09ab93cfdbdc0.png)
 - Jika ya, [periksa apakah Anda sudah membeli bandwidth jaringan publik](#step02).
 - Jika tidak, [terapkan alamat IP publik elastis dan ikat dengan CVM](https://intl.cloud.tencent.com/document/product/213/16586).
 
<span id="step02"></span>
### Memeriksa apakah Anda sudah membeli bandwidth jaringan publik
Periksa apakah bandwidth jaringan publik adalah 0 Mbps. Anda perlu memastikan setidaknya 1 Mbps bandwidth jaringan publik.
 - Jika ya, tingkatkan bandwidth menjadi 1 Mbps atau lebih dengan [menyesuaikan konfigurasi jaringan](https://intl.cloud.tencent.com/document/product/213/15517).
![](https://main.qcloudimg.com/raw/29b771d9de5d1ecdadb872c0378a31c7.png)
 - Jika tidak, [periksa apakah port login jarak jauh (3389) instans sudah dibuka ke Internet](#step03).

<span id="step03"></span>
### Memeriksa apakah port login jarak jauh (3389) instans sudah dibuka ke Internet
1. Pada halaman pengelolaan instans di konsol CVM, klik ID atau nama instans untuk login guna membuka halaman detail instans.
2. Pada halaman tab "Security Groups" (Grup Keamanan), periksa apakah port login jarak jauh (port 3389 secara default) telah dibuka ke Internet dalam grup keamanan telah terikat dengan instans, seperti yang ditunjukkan pada gambar berikut:
![Grup keamanan](https://main.qcloudimg.com/raw/28b5f0a038dd354346745bd97f724350.png)
 - Jika ya, [periksa pengaturan sistem instans Windows](#step04).
 - Jika tidak, edit aturan grup keamanan yang sesuai untuk membuka port ke Internet. Untuk petunjuk, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).

<span id="step04"></span>
### Memeriksa pengaturan sistem instans Windows
1. [Login ke instans Windows menggunakan VNC](https://main.qcloudimg.com/raw/6c781636c69eacae76a08b88f9e32b99.png) dan periksa pengaturan sistem instans Windows.
> Operasi berikut menggunakan contoh Windows Server 2012.
>
2. Di sistem operasi instans yang telah login, klik kanan <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>, pilih **Run** (Jalankan), masukkan **services.msc** (services.msc) di **Run** (Jalankan), dan tekan Enter untuk membuka Jendela "Service" (Layanan).
3. Klik dua kali "Remote Desktop Services" (Layanan Desktop Jarak Jauh) untuk membuka jendela "Remote Desktop Services Properties" (Properti Layanan Desktop Jarak Jauh) dan periksa apakah Layanan Desktop Jarak Jauh sedang berjalan, seperti yang ditunjukkan pada gambar berikut:
![Layanan Desktop Jarak Jauh](https://main.qcloudimg.com/raw/6c781636c69eacae76a08b88f9e32b99.png)
 - Jika ya, lanjutkan ke [langkah 4](#step04_4).
 - Jika tidak, atur "Startup type" (Jenis startup) ke "Automatic" (Otomatis) dan klik **Start** (Mulai) untuk mengatur "Service status" (Status layanan) ke "Running" (Berjalan).
4. <span id="step04_4">Klik kanan <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>, pilih **Run** (Jalankan), masukkan **sysdm.cpl** (sysdm.cpl) di **Run** (Jalankan), dan tekan Enter untuk membuka jendela "System Settings" (Pengaturan Sistem).</span>
5. Pada halaman tab "Remote" (Jarak Jauh), periksa apakah "Remote Desktop" (Desktop Jarak Jauh) diatur ke "Allow remote connections to this computer" (Izinkan koneksi jarak jauh ke komputer ini), seperti yang ditunjukkan pada gambar berikut:
![Pengaturan Desktop Jarak Jauh](https://main.qcloudimg.com/raw/cbf2b2797bd48777008753f389574674.png)
 - Jika ya, lanjutkan ke [langkah 6](#step04_6).
 - Jika tidak, atur Desktop Jarak Jauh ke "Allow remote connections to this computer" (Izinkan koneksi jarak jauh ke komputer ini).
6. <span id="step04_6">Klik <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> dan pilih **Control Panel** (Panel Kontrol) untuk membuka panel kontrol.</span>
7. Di "Control Panel" (Panel Kontrol), pilih **System and Security** (Sistem dan Keamanan) > **Windows Defender Firewall** (Windows Defender Firewall) untuk membuka "Windows Defender Firewall" (Windows Defender Firewall).
8. Pada "Windows Defender Firewall" (Windows Defender Firewall), periksa status Windows Defender Firewall, seperti yang ditunjukkan pada gambar berikut:
![Status Windows Defender Firewall](https://main.qcloudimg.com/raw/e74937594a03c141e6e5ac753f025d91.png)
 - Jika statusnya "On" (Aktif), lanjutkan ke [langkah 9](#step04_9).
 - Jika statusnya "Off" (Nonaktif), [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
9. <span id = “step04_9”>Di "Windows Defender Firewall" (Windows Defender Firewall), pilih **Allow an app through Windows Firewall** (Izinkan aplikasi melalui Windows Firewall) untuk membuka jendela "Allowed apps" (Aplikasi yang diizinkan).</span>
10. Di jendela "Allowed apps" (Aplikasi yang diizinkan), periksa apakah "Remote Desktop" (Desktop Jarak Jauh) dipilih di "Allowed apps and features" (Aplikasi dan fitur yang diizinkan), seperti yang ditunjukkan pada gambar berikut:
![Memilih Desktop Jarak Jauh](https://main.qcloudimg.com/raw/dfed8792ce1dd8b32bee4aaa02ef6bbf.png)
 - Jika ya, lanjutkan ke [langkah 11](#step04_11).
 - Jika tidak, pilih "Remote Desktop" (Desktop Jarak Jauh) untuk mengizinkan "Remote Desktop" (Desktop Jarak Jauh) melalui Windows Firewall.
11. <span id = “step04_11”>Di "Windows Defender Firewall" (Windows Defender Firewall), pilih **Turn Windows Defender Firewall on or off** (Aktifkan atau nonaktifkan Windows Defender Firewall) untuk membuka jendela "Customize Settings" (Sesuaikan Pengaturan).</span>
12. Di jendela "Customize Settings" (Sesuaikan Pengaturan), atur "Private network settings" (Pengaturan jaringan pribadi) dan "Public network settings" (Pengaturan jaringan publik) ke "Turn off Windows Defender Firewall (not recommended)" (Nonaktifkan Windows Defender Firewall (tidak direkomendasikan)), seperti yang ditunjukkan pada gambar berikut:
![Menonaktifkan Windows Defender Firewall](https://main.qcloudimg.com/raw/5d5f8c4d7b783bc1018e03368ae400bc.png)

Jika Anda masih tidak dapat terhubung ke instans Windows melalui Desktop Jarak Jauh setelah menyelesaikan langkah-langkah sebelumnya, [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).

