## Skenario
Dokumen ini menunjukkan kepada Anda cara mengonfigurasi login jarak jauh multi-pengguna ke CVM Windows, mengambil CVM dengan Windows Server 2012 R2 sebagai sistem operasi sebagai contoh.

## Langkah-Langkah
### Menambahkan layanan desktop jarak jauh
1. Login ke CVM Windows.
2. Di antarmuka sistem operasi, klik <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> untuk membuka **Server Manager** (Pengelola Server), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/66bb5237846f1dd79e3145bfd82d9257.png)
3. Klik **Add roles and features** (Tambahkan peran dan fitur), dan jendela **Add Roles and Features Wizard** (Wizard Tambahkan Peran dan Fitur) akan muncul.
4. Di jendela “Add Roles and Features Wizard” (Wizard Tambahkan Peran dan Fitur), jangan ubah parameter default untuk 3 langkah pertama.
5. Di halaman **Select server roles** (Pilih peran server), centang **Remote Desktop Services** (Layanan Desktop Jarak Jauh) dan klik **Next** (Selanjutnya), seperti yang ditunjukkan di bawah ini: 
![](https://main.qcloudimg.com/raw/54d329c2667ac5c60ffdc2b74f1fc555.png)
6. Pertahankan parameter default dan klik **Next** (Selanjutnya) dua kali berturut-turut.
7. Di antarmuka **Select Role Service** (Pilih Layanan Peran), centang **Remote Desktop Session Host** (Host Sesi Desktop Jarak Jauh), seperti yang ditunjukkan di bawah ini:
Kotak perintah “Add features that are required for remote desktop session host?” (Tambahkan fitur yang diperlukan untuk host sesi desktop jarak jauh?) akan muncul.
![](https://main.qcloudimg.com/raw/8d24fd515bd363dc020257c2843c5562.png)
8. Dalam kotak perintah “Add features that are required for remote desktop session host?” (Tambahkan fitur yang diperlukan untuk host sesi desktop jarak jauh?), klik **Add Features** (Tambahkan Fitur), seperti yang ditunjukkan di bawah ini: 
![](https://main.qcloudimg.com/raw/2a33d896c16b1d98012536cdc3776248.png)
9. Di halaman **Select Role Service** (Pilih Layanan Peran), centang **Remote Desktop Licensing** (Pemberian Lisensi Desktop Jarak Jauh), seperti yang ditunjukkan di bawah ini:
Kotak perintah “Add features that required for Remote Desktop Licensing?” (Tambahkan fitur yang diperlukan untuk Lisensi Desktop Jarak Jauh?) akan muncul.
![](https://main.qcloudimg.com/raw/1c908dc77f50488387a2fdbfda08ba35.png)
10. Dalam kotak perintah “Add features that required for Remote Desktop Licensing?” (Tambahkan fitur yang diperlukan untuk Lisensi Desktop Jarak Jauh?), klik **Add Features** (Tambahkan Fitur).
![](https://main.qcloudimg.com/raw/d7aa066366b168ac8a7475155d34ea19.png)
11. Klik **Next** (Selanjutnya).
12. Centang **Restart the destination server automatically if required** (Mulai ulang server tujuan secara otomatis jika diperlukan), dan klik **Yes** (Ya) di kotak perintah pop-up, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/df280b0a66470be404f114bd17c47d21.png)
13. Klik **Install** (Instal) dan tunggu hingga penginstalan layanan desktop jarak jauh selesai.

### Mengonfigurasi login jarak jauh multi-pengguna ke instans
1. Gunakan VNC untuk login ke CVM Windows.
2. Di antarmuka sistem operasi, klik <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> untuk membuka jendela Windows PowerShell.
3. Di jendela Windows PowerShell, masukkan **gpedit.msc** (gpedit.msc) dan tekan **Enter** (Enter) untuk membuka **Local Group Policy Editor** (Editor Kebijakan Grup Lokal).
4. Di pohon navigasi kiri, pilih **Computer Configuration** (Konfigurasi Komputer) > **Administrative Templates** (Templat Administratif) > **Windows Components** (Komponen Windows) > **Remote Desktop Services** (Layanan Desktop Jarak Jauh) > **Remote Desktop Session Host** (Host Sesi Desktop Jarak Jauh) > **Connections** (Koneksi), lalu klik dua kali **Limit number of connections** (Batasi jumlah koneksi), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/e0420d2bb8ddd3e1524ee688173cb9d1.png)
5. Di jendela **Limit number of connection** (Batasi jumlah koneksi) yang muncul, pilih **Enabled** (Diaktifkan), dan masukkan jumlah maksimum pengguna jarak jauh secara serentak di **RD Maximum Connections Allowed** (Koneksi Maksimum RD yang Diizinkan), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/066c9dfb06dc4c092424c4e1142f7471.png)
6. Klik **OK** (OKE).
4. Di pohon navigasi kiri, pilih **Computer Configuration** (Konfigurasi Komputer) > **Administrative Templates** (Templat Administratif) > **Windows Components** (Komponen Windows) > **Remote Desktop Services** (Layanan Desktop Jarak Jauh) > **Remote Desktop Session Host** (Host Sesi Desktop Jarak Jauh) > **Connections** (Koneksi), lalu klik dua kali **Restrict Remote Desktop Services users to a single Remote Desktop Services session** (Batasi pengguna Layanan Desktop Jarak Jauh ke satu sesi Layanan Desktop Jarak Jauh), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/1183e9f4c6c08b6f99746db42b0d183e.png)
8. Di jendela “Restrict Remote Desktop Services users to a single Remote Desktop Services session” (Batasi pengguna Layanan Desktop Jarak Jauh ke sesi Layanan Desktop Jarak Jauh tunggal) yang muncul, pilih **Disabled** (Dinonaktifkan), lalu klik **OK** (OKE), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/56d910ea359024d34dc05de3a274c91a.png)
9. Tutup editor kebijakan grup lokal.
10. Mulai ulang instans.



