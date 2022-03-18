Artikel ini menjelaskan cara memecahkan masalah kegagalan login jarak jauh yang disebabkan oleh masalah port.
> Berikut ini menggunakan instans CVM yang menjalankan Windows Server 2012 sebagai contoh untuk menjelaskan langkah-langkahnya.
>

## Alat
Anda dapat menggunakan alat berikut untuk memeriksa apakah masalah login terkait dengan port dan konfigurasi grup keamanan:
- [Diagnosis mandiri](https://console.cloud.tencent.com/workorder/check) 
- [Pembantu grup keamanan (port)](https://console.cloud.tencent.com/vpc/helper) 

Jika masalahnya memang masalah konfigurasi grup keamanan, gunakan **Open all ports** (Buka semua port) di [Pembantu grup keamanan (port)](https://console.cloud.tencent.com/vpc/helper) untuk membuka port terkait dan coba login lagi. Jika Anda masih tidak dapat login setelah membuka port, lihat hal berikut untuk pemecahan masalah.

## Pemecahan Masalah

### Memeriksa konektivitas jaringan

Anda dapat menggunakan perintah Ping untuk menguji konektivitas jaringan dari PC Anda. Anda harus menjalankan pengujian dari komputer di lingkungan jaringan yang berbeda (seperti rentang IP atau ISP yang berbeda) untuk memeriksa apakah masalahnya adalah jaringan lokal atau masalah server.

1. Buka alat baris perintah di komputer lokal Anda.
 - Windows: Klik **Start** (Mulai) -> **Run** (Jalankan) dan masukkan **cmd** (cmd). Jendela Prompt Perintah muncul.
 - MacOS: Buka jendela Terminal.
2. Jalankan perintah berikut untuk menguji koneksi jaringan.
```
ping + CVM_Instance_public_IP_address
```
Misalnya, `ping 139.199.xxx.xxx`.
 - Jika Anda melihat hasil yang mirip dengan yang ditunjukkan pada gambar berikut, koneksi jaringan Anda ke instans CVM adalah normal. Dalam hal ini, [periksa konfigurasi desktop jarak jauh](#F2).
![](https://main.qcloudimg.com/raw/52e6c15bc862dd7724643747ed8abcfb.png)
 - Jika **Request Timeout** (Waktu Permintaan Habis) muncul, koneksi jaringan Anda ke instans CVM tidak berfungsi dengan benar. Dalam hal ini, lihat [Kegagalan Ping Alamat IP Instans](https://intl.cloud.tencent.com/document/product/213/14639) untuk petunjuk pemecahan masalah.
3. Jalankan perintah berikut untuk memeriksa apakah port jarak jauh terbuka.
```
telnet CVM_instance_public_IP_address port_number
```
Misalnya, `telnet 139.199.xxx.xxx 3389`, seperti yang ditunjukkan pada gambar berikut:
![](https://mc.qcloudimg.com/static/img/e18be3704977545d5c952d3a583f2ccc/image.png)
 - Jika Anda melihat layar hitam hanya dengan kursor, itu menunjukkan port (3389) terbuka. Untuk langkah selanjutnya, [periksa apakah layanan desktop jarak jauh diaktifkan pada instans](#F2).
 - Jika koneksi gagal, seperti yang ditunjukkan pada gambar berikut, itu berarti terjadi pengecualian jaringan. Periksa bagian jaringan yang sesuai.
 ![](https://main.qcloudimg.com/raw/e3996140e2c1895d2ba2b1dfa637f998.png)
 
<span id = "F2"></span>
### Memeriksa konfigurasi desktop jarak jauh

#### Login ke instans CVM menggunakan VNC

> Sebaiknya gunakan VNC untuk login hanya jika metode login standar gagal.
>
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/).
2. Pilih CVM yang diinginkan dan klik **Log In** (Login), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Halaman **Log into Windows instance** (Login ke instans Windows) muncul. Pilih **Alternative login methods (VNC)** (Metode login alternatif (VNC)) dan klik **Log In Now** (Login Sekarang) untuk login ke instans CVM.
4. Halaman login muncul. Pilih **Send Ctrl-Alt-Del** (Kirim Ctrl-Alt-Del) di sudut kiri atas dan klik **Ctrl-Alt-Delete** (Ctrl-Alt-Delete) untuk login ke antarmuka login sistem, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

#### Memeriksa apakah desktop jarak jauh diaktifkan pada instans CVM

1. Login ke instans CVM. Klik kanan **This Computer** (Komputer ini) dari Desktop dan pilih **Properties** (Properti) untuk membuka jendela **System** (Sistem).
2. Di jendela **System** (Sistem), pilih **Advanced System Configurations** (Konfigurasi Sistem Lanjutan) untuk membuka jendela **System Properties** (Properti Sistem).
3. Di jendela **System Properties** (Properti Sistem), pilih tab **Remote** (Jarak Jauh). Periksa apakah **Allow remote connections to this computer** (Izinkan koneksi jarak jauh ke komputer ini) di bawah **Remote Desktop** (Desktop Jarak Jauh) dipilih, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/2ee4d1abf5ebf351ed814d6644bc7d58.png)
 - Jika dipilih, koneksi jarak jauh diaktifkan. Selanjutnya, Anda harus [memeriksa apakah port akses jarak jauh terbuka](#F3).
 - Jika dihapus, pilih **Allow remote connections to this computer** (Izinkan koneksi jarak jauh ke komputer ini) dan coba hubungkan ke instans lagi.

<span id = "F3"></span>
### Memeriksa apakah port akses jarak jauh terbuka

1. Login ke instans CVM. Klik <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> untuk membuka jendela **Windows PowerShell** (Windows PowerShell).
2. Di jendela **Windows PowerShell** (Windows PowerShell), jalankan perintah berikut untuk memeriksa status desktop jarak jauh (secara default, desktop jarak jauh menggunakan port 3389).
```
netstat -ant | findstr 3389
```
 - Jika Anda melihat hasil yang mirip dengan yang ditunjukkan pada gambar berikut, statusnya adalah normal. Anda dapat mencoba [memulai ulang desktop jarak jauh](#F4) dan menghubungkan ke instans lagi untuk memeriksa apakah koneksi berhasil.
![](https://main.qcloudimg.com/raw/5206af71e86f8126e9e6845bbeef21b2.png)
 - Jika tidak ada koneksi yang ditampilkan, desktop jarak jauh tidak berfungsi dengan benar. Anda dapat [memeriksa apakah port desktop jarak jauh di registri konsisten](#F5).

<span id = "F5"></span>
### Memeriksa apakah port desktop jarak jauh di registri konsisten

> Bagian ini menjelaskan cara memeriksa nilai **TCP PortNumber** (TCP PortNumber) dan **RDP Tcp PortNumber** (RDP Tcp PortNumber). Mereka harus sama.
>
1. Login ke instans CVM, klik <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>, pilih <img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>, dan masukkan **regedit** (regedit). Tekan **Enter** (Enter) untuk membuka jendela **Registry Editor** (Editor Registri).
2. Di panel navigasi di sebelah kiri, perluas direktori berikut: **HKEY_LOCAL_MACHINE** (HKEY_LOCAL_MACHINE) -> **SYSTEM** (SISTEM) -> **CurrentControlSet** (CurrentControlSet) -> **Control** (Kontrol) -> **Terminal Server** (Server Terminal) -> **Wds** (Wds) -> **rdpwd** (rdpwd) -> **Tds** (Tds) -> **tcp** (tcp).
3. Temukan PortNumber di **tcp** (tcp) dan catat nomor port (3389 secara default), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/6762d059263b1c589414461e522d1e9f.png)
4. Di panel navigasi di sebelah kiri, perluas direktori berikut: **HKEY_LOCAL_MACHINE** (HKEY_LOCAL_MACHINE) -> **SYSTEM** (SISTEM) -> **CurrentControlSet** (CurrentControlSet) -> **Control** (Kontrol) -> **Terminal Server** (Server Terminal) -> **WinStation** (WinStation) -> **RDP-Tcp** (RDP-Tcp).
5. Temukan PortNumber di **RDP-Tcp** (RDP-Tcp) dan periksa apakah nilai PortNumber di **RDP-Tcp** (RDP-Tcp) sama dengan yang ada di **tcp** (tcp), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/9d68cec10e75afe621beb6c914d393cb.png)
 - Jika tidak sama, ikuti [Langkah 6](#F5_step6).
 - Jika sama, [mulai ulang desktop jarak jauh](#F4).
6. Klik dua kali PortNumber di **RDP-Tcp** (RDP-Tcp).
7. Pada kotak dialog yang muncul, modifikasi **Value Data** (Data Nilai) ke nomor port kosong antara 0 - 65535. Pastikan **TCP PortNumber** (Nomor Port TCP) dan **RDP TCP PortNumber** (Nomor Port RDP TCP) sama, lalu klik **OK** (OKE).
7. Mulai ulang instans menggunakan [Konsol CVM](https://console.cloud.tencent.com/cvm), dan coba hubungkan lagi ke instans dari jarak jauh untuk memeriksa apakah koneksi berhasil.


<span id = "F4"></span>
### Memulai ulang desktop jarak jauh

1. Login ke instans CVM. Klik <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> dan pilih <img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>. Masukkan **services.msc** (services.msc) dan tekan **Enter** (Enter) untuk membuka jendela **Services** (Layanan).
2. Di jendela **Services** (Layanan), klik kanan **Remote Desktop Services** (Layanan Desktop Jarak Jauh) dan pilih **Restart** (Mulai Ulang) untuk memulai ulang layanan desktop jarak jauh, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/396ee711bb64c8fb1966112a81dd0fd4.png)

## Jika Semua Yang Lain Gagal

Jika Anda masih tidak dapat login dari jarak jauh setelah melakukan langkah-langkah yang disebutkan di atas, [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2) untuk bantuan lebih lanjut.
