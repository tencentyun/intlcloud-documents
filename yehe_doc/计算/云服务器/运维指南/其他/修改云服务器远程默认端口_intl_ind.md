## Skenario
Port default CVM rentan terhadap pemindaian dan serangan oleh perangkat lunak berbahaya. Oleh karena itu, Anda perlu mengubah port jarak jauh default CVM ke port yang kurang umum untuk mencegah kegagalan dalam mengakses CVM dari jarak jauh karena serangan tersebut. Ini memastikan keamanan CVM.

Modifikasi pada port hanya akan valid jika dibuat dalam aturan grup keamanan dan CVM secara bersamaan. Tindakan ini dapat memodifikasi port jarak jauh default CVM seperti yang dijelaskan di bawah ini. Metode modifikasi berbeda-beda tergantung pada sistem operasi CVM.
- [Memodifikasi port jarak jauh default CVM Windows](#ModifyWindowsCVMPort)
- [Memodifikasi port jarak jauh default CVM Linux](#ModifyLinuxCVMPort)

## Petunjuk

<span id="ModifyWindowsCVMPort"></span>
### Memodifikasi port jarak jauh default dari CVM Windows
> Operasi berikut menggunakan Windows Server 2012 sebagai contoh. Prosedurnya mungkin sedikit berbeda tergantung pada sistem operasi dan bahasa.
>
1. [Login ke instans Windows dengan menggunakan VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Di sistem operasi, klik <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> untuk membuka jendela “Windows PowerShell”.
3. Di jendela “Windows PowerShell”, masukkan **regedit** (regedit) dan tekan **Enter** (Enter) untuk membuka jendela “Registry Editor”.
4. Di panel navigasi registri sisi kiri, perluas hierarki berikut secara berurutan: **HKEY_LOCAL_MACHINE** (HKEY_LOCAL_MACHINE) > **SYSTEM** (SISTEM) > **CurrentControlSet** (CurrentControlSet) > **Control** (Kontrol) > **Terminal Server** (Server Terminal) > **Wds** (Wds) > **rdpwd** (rdpwd) > **Tds** (Tds) > **tcp** (tcp).
5. <span id="Windows_step05"></span>Cari PortNumber di **tcp** (tcp). Kemudian, ubah nilai PortNumber dari 3389 menjadi nomor port kosong dengan rentang 0 hingga 65535, seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/7044cef95fd7e56b56946afdb64de346.png)
6. Di panel navigasi registri sisi kiri, perluas hierarki berikut secara berurutan: **HKEY_LOCAL_MACHINE** (HKEY_LOCAL_MACHINE) > **SYSTEM** (SISTEM) > **CurrentControlSet** (CurrentControlSet) > **Control** (Kontrol) > **Terminal Server** (Server Terminal) > **WinStations** (WinStations) > **RDP-Tcp** (RDP-Tcp).
7. Cari dan ubah PortNumber di **RDP-Tcp** (RDP-Tcp) agar sama dengan nilai yang ada di **tcp** (tcp).
![](https://main.qcloudimg.com/raw/fa54eb32c20dcc8a7c942c8e707fa665.png)
8. (Opsional) Jika firewall diaktifkan untuk CVM Anda, pastikan untuk menambahkan port baru ke daftar firewall yang diizinkan dan atur untuk mengizinkan koneksi.
 1. Di jendela “Windows PowerShell”, masukkan **wf.msc** (wf.msc) dan tekan **Enter** (Enter) untuk membuka jendela “Windows Firewall with Advanced Security”.
 2. Di jendela “Windows Firewall with Advanced Security”, pilih **Inbound Rules** (Aturan Masuk) dan klik **New rule** (Aturan baru), seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/ac93eed862e215971073912030fdbc41.png)
 3. Pada halaman “Rule Type” (Jenis Aturan) di jendela “New Inbound Rule Wizard” (Wizard Aturan Masuk Baru), pilih **Port** (Port) dan klik **Next** (Selanjutnya).
 4. Pada halaman “Protocol and Ports” (Protokol dan Port) di jendela **New Inbound Rule Wizard** (Wizard Aturan Masuk Baru), pilih **TCP** (TCP) dan masukkan nomor port yang diatur di [Langkah 5](#Window_step05) di **Specific Port** (Port Khusus). Kemudian, klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar berikut.
 ![](https://main.qcloudimg.com/raw/73a7ca280f4f6b733d687597014b57b4.png)
 5. Pada halaman **Action** (Tindakan) di jendela “New Inbound Rule Wizard” (Wizard Aturan Masuk Baru), pilih **Allow connections** (Izinkan koneksi) dan klik **Next** (Selanjutnya).
 6. Pada halaman “Profile” (Profil) di jendela “New Inbound Rule Wizard” (Wizard Aturan Masuk Baru), terapkan profil default dan klik **Next** (Selanjutnya).
 7. Pada halaman “Name” (Nama) di jendela “New Inbound Rule Wizard” (Wizard Aturan Masuk Baru), masukkan nama aturan dan klik **Finish** (Selesai).
9. Di jendela “Windows PowerShell”, masukkan **services.msc** (services.msc) dan tekan **Enter** (Enter) untuk membuka jendela “Services” (Layanan).
10. Cari dan klik kanan **Remote Desktop Services** (Layanan Desktop Jarak Jauh) di jendela “Services” (Layanan). Kemudian, pilih **Restart** (Mulai ulang) untuk memulai ulang layanan login jarak jauh.
11. Lihat [Memodifikasi Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34825) untuk memodifikasi aturan grup keamanan dengan port protokol “TCP:3389” dengan mengubah nomor port sesuai yang ditetapkan di [Langkah 5](#Windows_step05).
![](https://main.qcloudimg.com/raw/a447d7e69ce95d349f0d78b5b72b9228.png)


<span id="ModifyLinuxCVMPort"></span>
### Memodifikasi port jarak jauh default CVM Linux
>
> - Sebelum Anda mengubah port jarak jauh default, sebaiknya tambahkan nomor port SSH dan uji apakah port tersebut berhasil terhubung ke CVM. Kemudian, hapus port default 22. Pastikan port default 22 tidak dapat terhubung ke CVM saat port baru gagal terhubung ke CVM.
> - Operasi berikut menggunakan CentOS 7.3 sebagai contoh. Operasi spesifik sedikit berbeda menurut versi dan bahasa sistem operasi.
>
1. [Login ke instans Linux menggunakan VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Jalankan perintah berikut untuk memodifikasi file konfigurasi:
```
vim /etc/ssh/sshd_config
```
3. <span id="Linux_step03"></span>Tekan **i** (i) untuk beralih ke mode pengeditan dan menambahkan port baru. Tambahkan `Port x` (dengan x adalah nomor port dari port baru) di baris baru di bawah `#Port 22`, dan hapus `#` untuk mengomentari `Port 22`, seperti yang ditunjukkan pada gambar berikut.
Misalnya, tambahkan `Port 23456` di baris.
![](https://main.qcloudimg.com/raw/54e5d9b4301271fbbeca8b2718b985dc.png)
4. Tekan **Esc** (Esc), masukkan **:wq** (:wq), dan simpan perubahannya.
5. Jalankan perintah berikut agar konfigurasi baru berlaku:
```
systemctl restart sshd.service
```
6. (Opsional) Konfigurasikan firewall.
 - Secara default, layanan iptables digunakan sebagai firewall untuk CVM Linux dengan CentOS lebih awal dari CentOS 7. Konfigurasikan firewall sebagai berikut jika aturan iptables telah dikonfigurasi untuk CVM.
    1. Jalankan perintah berikut untuk mengonfigurasi firewall:
```
iptables -A INPUT -p tcp --dport <New port number> -j ACCEPT
```
Misalnya, jika nomor port baru adalah 23456, jalankan perintah berikut:
```
iptables -A INPUT -p tcp --dport 23456 -j ACCEPT
```
    2. Jalankan perintah berikut untuk memulai ulang firewall:
```
service iptables restart
```
 - Layanan Firewalld digunakan sebagai firewall untuk CVM Linux dengan CentOS 7 atau versi yang lebih baru. Konfigurasikan firewall sebagai berikut jika layanan Firewalld telah diaktifkan pada CVM.
Jalankan perintah berikut untuk mengizinkan akses dengan nomor port yang ditambahkan di [Langkah 3](#Linux_step03):
```
firewall-cmd --add-port=<New port number>/tcp --permanent
```
Misalnya, jika nomor port baru adalah 23456, jalankan perintah berikut:
```
firewall-cmd --add-port=23456/tcp --permanent
```
Jika `success` ditampilkan, artinya port telah berhasil dikonfigurasi.
7. Lihat [Memodifikasi Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34825) untuk mengubah aturan grup keamanan dengan port protokol “TCP:22” dengan mengubah nomor port ke yang ditetapkan di [Langkah 3](#Linux_step03).
![](https://main.qcloudimg.com/raw/add0bba23dc32f73b5d1fbbdad71c9ab.png)


## Verifikasi

### CVM Windows

1. Misalnya sistem operasi Windows diinstal di komputer lokal. Buka kotak dialog “Remote Desktop Connection” (Koneksi Desktop Jarak Jauh).
2. Masukkan `IP internet untuk server Windows: nomor port setelah modifikasi` setelah **Computer** (Komputer) dan klik **Connect** (Hubungkan), seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/1452f968e3c2c4d4c1083bdf0742df9d.png)
3. Masukkan akun admin dan kata sandi seperti yang diminta, lalu klik **OK** (OKE).
Jika antarmuka sistem operasi CVM Windows muncul, artinya koneksi sudah dibuat.
> Jika Anda login ke CVM Windows menggunakan file RDP, ubah parameter `full address:s` di file RDP, seperti yang ditunjukkan pada gambar berikut:
>[](https://main.qcloudimg.com/raw/84dd85a9547fc64f2daccba32f1d59d7.png)
>

### CVM Linux

1. Asumsikan bahwa PuTTY digunakan untuk login jarak jauh. Mulai klien PuTTY.
2. Di jendela “PuTTY Configuration” (Konfigurasi PuTTY), masukkan alamat IP publik CVM Linux, atur **Port** (Port) ke nomor port baru, lalu klik **Open** (Buka), seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/c89c2064ed82e738fd60fcab39b09206.png)
3. Masukkan nama pengguna dan sandi CVM Linux seperti yang diminta dan tekan **Enter** (Enter).
Jika output berikut muncul, artinya koneksi sudah dibuat.
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
4. Setelah menggunakan port baru untuk berhasil membuat koneksi ke CVM Linux, jalankan perintah berikut:
```
vim /etc/ssh/sshd_config
```
5. Tekan **i** (i) untuk beralih ke mode pengeditan, dan tambahkan `#` di depan `Port 22` untuk memberi komentar di luar port.
6. Tekan **Esc** (Esc), masukkan **:wq** (:wq), dan simpan perubahannya.
7. Jalankan perintah berikut agar konfigurasi baru diterapkan. Pastikan Anda menggunakan port baru untuk login jarak jauh berikutnya ke CVM Linux.
```
systemctl restart sshd.service
```
