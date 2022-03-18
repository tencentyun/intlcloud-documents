## Pengantar

Artikel ini menggunakan Windows Server 2012 sebagai contoh untuk menunjukkan cara memperbarui sistem operasi Windows Anda.

## Petunjuk

### Memperbarui Windows menggunakan jaringan publik
Anda dapat menggunakan layanan Windows Update untuk memperbarui sistem operasi Anda. Langkah-langkah detailnya adalah sebagai berikut:
1. Login ke instans CVM Windows.
2. Klik <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> -> **Control Panel** (Panel Kontrol) -> **Windows Update** (Windows Update). Jendela **Windows Update** (Windows Update) akan muncul.
3. Klik **Check for updates** (Periksa pembaruan), dan tunggu hingga pemeriksaan selesai.
4. Setelah pemeriksaan selesai, klik **N Important Updates Available** (Pembaruan Penting N Tersedia) atau **N Optional Updates Available** (Pembaruan Opsional N Tersedia) di “Windows Update”. Jendela **Choose the Update to Install** (Pilih Pembaruan yang Akan Diinstal) akan muncul.
5. Pilih pembaruan yang ingin Anda instal, lalu klik **Install** (Instal).
Jika diminta untuk memulai ulang sistem Anda setelah pembaruan selesai, lakukan langkah tersebut.
> Jika Anda login menggunakan VNC setelah instans di-boot ulang dan pesan "Updating...Do not turn off the power" (Memperbarui...Jangan matikan daya) atau "Configuration has not been completed" (Konfigurasi belum selesai) muncul, jangan lakukan pematian paksa. Karena tindakan ini dapat merusak instans CVM Anda.

### Memperbarui Windows menggunakan jaringan pribadi
Jika instans CVM Anda tidak memiliki akses jaringan publik, Anda dapat menggunakan server Windows Update pribadi Tencent Cloud untuk memperbarui sistem operasi Anda. Server Tencent Cloud Windows Update memiliki sebagian besar pembaruan, tetapi tidak memiliki paket driver perangkat keras dan beberapa pembaruan yang tidak umum. Oleh karena itu, layanan yang tidak umum mungkin tidak mendapatkan pembaruan menggunakan server Tencent Cloud Windows Update.
Ikuti langkah-langkah ini untuk menggunakan server Tencent Cloud Windows Update:
1. Login ke instans CVM Windows.
2. Gunakan Internet Explorer untuk mengunduh file konfigurasi jaringan pribadi Tencent Cloud wusin.bat dari alamat berikut:
http://mirrors.tencentyun.com/install/windows/wusin.bat
3. Jalankan wusin.bat di Command Prompt dengan hak administrator, seperti yang ditunjukkan di bawah ini:
> Jika Anda membuka wusin.bat menggunakan Internet Explorer setelah selesai mengunduh, jendela konsol akan tertutup secara otomatis dan Anda tidak dapat melihat hasilnya.
>
Anda dapat menyimpan wusin.bat ke hard drive Anda, seperti C:\, dan membuka jendela Command Prompt dengan hak administrator untuk menjalankannya.

Jika Anda tidak ingin lagi menggunakan server Tencent Cloud Windows Update, Anda dapat mengunduh wusout.bat clean it up. Ikuti langkah-langkah ini untuk melakukannya:
1. Login ke instans CVM Windows.
2. Gunakan Internet Explorer untuk mengunduh file konfigurasi jaringan pribadi Tencent Cloud wusout.bat dari alamat berikut:
http://mirrors.tencentyun.com/install/windows/wusout.bat
3. Jalankan wusout.bat di Command Prompt dengan hak administrator, seperti yang ditunjukkan di bawah ini:
> Jika Anda membuka wusout.bat menggunakan Internet Explorer setelah selesai mengunduh, jendela konsol akan tertutup secara otomatis dan Anda tidak dapat melihat informasi hasil-nya.
>
Anda dapat menyimpan wusout.bat ke hard drive Anda seperti C:\, dan membuka jendela Command Prompt dengan hak administrator untuk menjalankannya.
