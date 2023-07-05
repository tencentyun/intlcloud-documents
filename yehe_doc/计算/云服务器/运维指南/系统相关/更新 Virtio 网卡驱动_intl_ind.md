## Ikhtisar

Windows Server 2008 R2 Enterprise SP1 dan Windows Server 2012 R2 Tencent Cloud CVM menggunakan driver Virtio ENI untuk mengoptimalkan performa jaringan perangkat keras virtualisasi. Tencent Cloud akan terus meningkatkan ENI untuk performa yang lebih baik dan pemecahan masalah yang mudah. Dokumen ini menjelaskan cara memperbarui driver Virtio ENI dan memeriksa versi driver.

## Prasyarat

Anda telah login ke CVM Tencent Cloud.

## Petunjuk

### Melihat informasi versi sistem

Lakukan langkah-langkah berikut untuk melihat versi sistem.
1. Masuk ke CVM dan akses jendela **System** (Sistem) sesuai dengan sistem operasi:
 - **Window Server 2008 R2 Enterprise SP1** (Window Server 2008 R2 Enterprise SP1): klik kanan **This PC** (PC Ini) > **Properties** (Properti) di desktop.
 - **Windows Server 2012 R2** (Windows Server 2012 R2): buka **Control Panel** (Panel Kontrol), dan pilih **System** (Sistem).
2. Di bagian **View basic information about your computer** (Lihat informasi dasar tentang komputer Anda), Anda dapat melihat informasi versi sistem.   

### Memperbarui driver Virtio ENI
>! CVM akan terputus sebentar selama pembaruan. Harap pastikan bahwa ini tidak akan memengaruhi layanan Anda sebelum melanjutkan. CVM perlu dimulai ulang setelah pembaruan.
>
1. Buka browser dan masukkan alamat berikut untuk mengunduh penginstal driver Virtio ENI untuk Windows Server 2008 R2 dan Windows Server 2012 R2. 
Pilih alamat unduhan berdasarkan lingkungan jaringan:
 - Alamat unduhan jaringan publik: `http://mirrors.tencent.com/install/windows/virtio_64_10003.msi`
 - Alamat unduhan jaringan pribadi: `http://mirrors.tencentyun.com/install/windows/virtio_64_10003.msi`
2. Setelah unduhan selesai, klik dua kali penginstal, pilih mode penginstalan **Classic** (Klasik), lalu klik **Next** (Selanjutnya).
3. Di jendela pop-up Windows Security, centang **Always trust the software from Tencent Technology (Shenzhen) Company Limited** (Selalu percayai perangkat lunak dari Tencent Technology (Shenzhen) Company Limited) dan klik **Install** (Instal). 
Selama proses penginstalan, pilih **Install this driver software anyway** (Tetap instal perangkat lunak driver ini) saat diminta.      
4. Mulai ulang komputer seperti yang diminta.


### Memeriksa versi driver

1. Klik <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png"  style="margin:0;">, ketik **ncpa.cpl** (ncpa.cpl) di kotak Jalankan, lalu tekan **Enter** (Enter).
2. Di jendela **Network Connection** (Koneksi Jaringan), klik kanan ikon "Ethernet" dan pilih **Properties** (Properti).
3. Di jendela **Ethernet Properties** (Properti Ethernet), klik **Configure** (Konfigurasi).
4. Di jendela **Tencent Virtio Ethernet Adapter Properties** (Properti Adaptor Ethernet Tencent Virtio), pilih tab **Driver** (Driver) untuk melihat versi driver saat ini.


