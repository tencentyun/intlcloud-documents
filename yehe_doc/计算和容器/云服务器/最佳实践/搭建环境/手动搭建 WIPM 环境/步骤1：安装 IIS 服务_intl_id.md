## Ikhtisar

Dokumen ini menjelaskan cara menambahkan dan menginstal peran IIS pada instans CVM dengan Windows Server 2012 R2 atau Windows Server 2008.

## Petunjuk
### Windows Server 2012 R2 
1. Login ke CVM Windows.
2. Di desktop, klik <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> dan buka **Server Manager** (Pengelola Server), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/cae0fe0bfebf5ad58b6e5d3451795230.png)
3. Klik **Add roles and features** (Tambahkan peran dan fitur) dan masuk ke jendela “Add Roles and Features Wizard” (Wizard Tambahkan Peran dan Fitur).
4. Di jendela pop-up, klik **Next** (Selanjutnya) dan masuk ke halaman “Select installation type” (Pilih jenis penginstalan).
5. Pilih **Role-based or feature-based installation** (Penginstalan berbasis peran atau berbasis fitur) dan klik **Next** (Selanjutnya) dua kali, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/9eaff4f125fb23a7180cba6f38f9f879.png)
6. Centang **Web Server (IIS)** (Web Server (IIS)) pada halaman “Select server roles” (Pilih peran server), seperti yang ditunjukkan di bawah ini:
Kotak dialog “Add features that are required for Web Server (IIS)** (Tambahkan fitur yang diperlukan untuk Server Web (IIS)) akan muncul.
![](https://main.qcloudimg.com/raw/d0aa5fa075275bfb2bd0c68da66616e4.png)
7. Klik **Add Features** (Tambahkan Fitur) di kotak dialog pop-up, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/817d1f22107836c77af2fd963888824f.png)
8. Klik **Next** (Selanjutnya).
9. Pada halaman **Features** (Fitur), centang **.NET Framework 3.5 Features** (Fitur .NET Framework 3.5) dan klik **Next** (Selanjutnya) dua kali, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/4876efa4308912eb4bdbb6074d35fd20.png)
10. Pada halaman **Role Services** (Layanan Peran), centang **CGI** (CGI) dan klik **Next** (Selanjutnya), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/c571820b1a4290d9b04abbc65cf81fd9.png)
11. Tinjau pilihan penginstalan Anda dan klik **Install** (Instal). Tunggu hingga proses penginstalan selesai.
![](https://main.qcloudimg.com/raw/1e51aed773aad8eac28f88c401a1814e.png)
12. Setelah penginstalan selesai, buka browser di CVM dan kunjungi `http://localhost/` untuk memverifikasi apakah IIS telah berhasil diinstal.
Jika halaman berikut muncul, ini menunjukkan bahwa IIS telah berhasil diinstal.
![](https://mc.qcloudimg.com/static/img/e064cc1f765d68edf3dcfb0051d5dbfa/image.png)

### Windows Server 2008

1. Login ke CVM Windows.
2. Di desktop, klik <img src="https://main.qcloudimg.com/raw/0e33f3dc1042244ab225ca32c5396296.png" style="margin: 0;"></img> dan buka **Server Manager** (Pengelola Server), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/36c9cf3d9fd246f0930a4be3516446b5.png)
3. Pilih **Roles** (Peran) di bilah sisi kiri, dan klik **Add Roles** (Tambahkan Peran) di panel kanan, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/b18a3c84aa193d3c64d1e25353154baf.png)
4. Klik **Next** (Selanjutnya) di jendela “Add Roles Wizard” (Tambahkan Peran Wizard), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/4ab72f46730ecf10f2fe2768b2cc24cc.png)
5. Pada halaman “Server Roles” (Peran Server), centang **Web Server (IIS)** (Web Server (IIS)), dan klik **Next** (Selanjutnya) dua kali, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/7a41185e562a62ca586b6b677381b3a1.png)
6. Pada halaman **Role Services** (Layanan Peran), centang **CGI** (CGI) dan klik **Next** (Selanjutnya), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/7e7a96b106292e87d44807369db66842.png)
7. Tinjau pilihan penginstalan Anda dan klik **Install** (Instal). Tunggu hingga proses penginstalan selesai.
![](https://main.qcloudimg.com/raw/877b71930f11d9d2a6fecf946f0bebfe.png)
8. Setelah penginstalan selesai, buka browser di CVM dan kunjungi `http://localhost/` untuk memverifikasi apakah IIS telah berhasil diinstal.
Jika halaman berikut muncul, ini menunjukkan bahwa IIS telah berhasil diinstal.
![](https://main.qcloudimg.com/raw/b11cd8170e7646daa3b9ca904b181cf4.png)

