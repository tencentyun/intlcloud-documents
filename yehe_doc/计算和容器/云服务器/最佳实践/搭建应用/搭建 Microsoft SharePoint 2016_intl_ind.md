## Ikhtisar
Dokumen ini memperkenalkan cara membangun Microsoft SharePoint 2016 pada instans CVM.

## Versi Perangkat Lunak
Dokumen ini menggunakan instans CVM dengan spesifikasi perangkat keras berikut sebagai contoh:
- vCPU: 4 core
- Memori: 8 GB

Dokumen ini menggunakan versi perangkat lunak berikut sebagai contoh:
- Sistem operasi: Windows Server 2012 R2 Datacenter 64-bit (Inggris)
- Database: SQL Server 2014

## Prasyarat
Anda telah membeli CVM Windows. Jika Anda belum melakukannya, lihat [Menyesuaikan Konfigurasi CVM Windows](https://intl.cloud.tencent.com/document/product/213/10516).

## Petunjuk

### Langkah 1: login ke instans Windows
Anda dapat [login ke instans Windows menggunakan file RDP (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5435) atau [login ke instans Windows melalui desktop jarak jauh](https://intl.cloud.tencent.com/document/product/213/32498).

<span id="AddAD_DHCP_DNS_IIS"></span>
### Langkah 2: menambahkan layanan AD, DHCP, DNS, dan IIS
1. Di desktop, klik <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> untuk membuka **Server Manager** (Pengelola Server).
2. Pilih **Local Server** (Server Lokal) di bilah sisi kiri, dan cari **IE Enhanced Security Configuration** (Konfigurasi Keamanan yang Didukung IE), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/c2b0791555bbc910cea70732c75daa0f.png)
3. Nonaktifkan **IE Enhanced Security Configuration** (Konfigurasi Keamanan yang Didukung IE), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/6acbf171bc703100401e48e362539b21.png)
4. Pilih **Dashboard** (Dasbor) di bilah sisi kiri, dan klik **Add roles and features** (Tambahkan peran dan fitur).
5. Di jendela “Add Roles and Features Wizard” (Wizard Tambahkan Peran dan Fitur)”, pertahankan konfigurasi default dan klik **Next** (Selanjutnya) 3 kali.
6. Pada halaman **Server Roles** (Peran Server), pilih **Active Directory Domain Services** (Layanan Domain Direktori Aktif), **DHCP Server** (Server DHCP), **DNS Server** (Server DNS), **Web Server (IIS)** (Server Web (IIS)), dan klik **Add Features ** (Tambahkan Fitur) di jendela pop-up, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/a2bb1c86c9277ca870c629ecf5b0d3f5.png)
7. Klik **Next** (Selanjutnya).
8. Pada halaman **Features** (Fitur), pilih **.NET Framework 3.5 Features** (Fitur .NET Framework 3.5) untuk menambahkan fitur, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/bf47abbb95ad42b9d6c720c3bb2c846b.png)
9. Pertahankan konfigurasi default dan klik **Next** (Selanjutnya) hingga halaman **Confirmation** (Konfirmasi) muncul.
10. Konfirmasikan penginstalan, dan klik **Install** (Instal).
11. Setelah penginstalan selesai, mulai ulang CVM.
12. Di desktop, klik <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> untuk membuka **Server Manager* (Pengelola Server).
13. Klik <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img> dan pilih **Promote this server to a domain controller** (Promosikan server ini ke pengontrol domain), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/1e6aa1d75044898357709909bb969c6f.png)
14. <span id="step14"></span>Di jendela **Active Directory Domain Services Configuration Wizard** (Wizard Konfigurasi Layanan Domain Direktori Aktif), pilih **Add a new forest** (Tambahkan hutan baru), masukkan nama domain di bidang **Root domain name** (Nama domain root), dan klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/017acc0e5939632f3808698f36320fd2.png)
15. <span id="step15"></span>Di bawah **Type the Directory Services Restore Mode (DSRM) password** (Ketik kata sandi Mode Pemulihan Layanan Direktori (DSRM)), atur kata sandi, dan klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/078672b95294790e4985108bd58d8504.png)
16. Pertahankan konfigurasi default dan klik **Next** (Selanjutnya) hingga konfigurasi selesai.
17. Klik **Install** (Instal).
18. Di desktop, klik <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> untuk membuka **Server Manager** (Pengelola Server).
19. Klik <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img> dan pilih **Complete DHCP configuration** (Selesaikan konfigurasi DHCP), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/4c65a7990acc647866d73c1b5ba20a6c.png)
20. Di jendela **DHCP Post-Install configuration wizard** (Wizard konfigurasi Pasca Penginstalan DHCP), klik **Next** (Selanjutnya).
21. Pertahankan konfigurasi default dan klik **Commit** (Terapkan) untuk menyelesaikan penginstalan.
![](https://main.qcloudimg.com/raw/4162a8fbde1b7af1d8fadacaa61965cf.png)
22. Klik **Close** (Tutup).

### Langkah 3: menginstal database SQL Server 2014

1. Buka browser di CVM dan unduh paket penginstalan SQL Server 2014 dari situs resmi SQL Server 2014.
> Anda juga dapat memperoleh paket penginstalan SQL Server 2014 dari situs web pihak ketiga atau saluran valid lainnya.
>
2. Klik dua kali file "Setup.exe" untuk memulai wizard penginstalan, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/f2cc33aef5ec2662238ffeca56d08a7d.png)
3. Pilih **New SQL Server stand-alone installation or add features to an existing installation** (Penginstalan mandiri SQL Server baru atau tambahkan fitur ke penginstalan yang sudah ada).
4. Pada halaman **Product Key** (Kunci Produk), masukkan kunci produk dan klik **Next** (Selanjutnya).
5. Pilih **I accept the license terms** (Saya menyetujui persyaratan lisensi), dan klik **Next** (Selanjutnya).
6. Pertahankan konfigurasi default, dan klik **Next** (Selanjutnya).
7. Setelah pemeriksaan penginstalan selesai, klik **Next** (Selanjutnya).
8. Pertahankan konfigurasi default, dan klik **Next** (Selanjutnya).
9. Pada halaman **Feature Selection** (Pilihan Fitur), klik **Select All** (Pilih Semua) untuk memilih semua fitur, dan klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/92eac7b681dae5937bafa484874ae122.png)
10. Pada halaman **Instance Configuration** (Konfigurasi Instans), pilih **Default instance** (Instans default), dan klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/2bf1682b927b66224c574435ee35e7af.png)
11. Pada halaman **Server Configuration -> Service Accounts** (Konfigurasi Server -> Akun Layanan), konfigurasikan akun dan kata sandi untuk SQL Server Database Engine dan SQL Server Analysis Services, lalu klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/1310d9db077772be6dad6f58a698273e.png)
 - Atur nama akun **SQL Server Database Engine** (Mesin Databese Server SQL) ke “NT AUTHORITY\NETWORK SERVICE”.
 - atur nama akun dan kata sandi **SQL Server Analysis Services** (Layanan Analisis Server SQL) ke nama domain dan kata sandi yang dikonfigurasi di [14](#step14) hingga [15](#step15) di [Langkah 2: menambahkan layanan AD, DHCP, DNS , dan IIS](#AddAD_DHCP_DNS_IIS).
12. Pada halaman **Database Engine Configuration -> Server Configuration** (Konfigurasi Mesin Database -> Konfigurasi Server), pilih **Add Current User** (Tambahkan Pengguna Saat Ini) untuk menggunakan akun saat ini sebagai akun administrator SQL Server, dan klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/90ac80988b45a6b08650d97fd0d08c09.png)
13. Pada halaman **Analysis Services Configuration -> Account Provisioning** (Konfigurasi Layanan Analisis -> Penyediaan Akun), pilih **Add Current User** (Tambahkan Pengguna Saat Ini) untuk memberi akun saat ini izin administrator untuk Layanan Analisis, dan klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/5fda4e9b2ac31d8394ab0dfa14847d73.png)
14. Pertahankan konfigurasi default, dan klik **Next** (Selanjutnya).
15. Pada halaman **Distributed Replay Controller** (Pengontrol Pemutaran Ulang Terdistribusi), klik **Add Current User** (Tambahkan Pengguna Saat Ini) untuk memberi akun saat ini izin akses untuk layanan pengontrol Pemutaran Ulang Terdistribusi.
![](https://main.qcloudimg.com/raw/2b67cc38051c51cb88ba7bbb740027b3.png)
16. Pertahankan konfigurasi default, dan klik **Next** (Selanjutnya).
17. Konfirmasi konfigurasi SQL Server, dan klik **Install** (Instal).
18. Setelah penginstalan selesai, klik **Close** (Tutup).


### Langkah 4: menginstal SharePoint 2016

1. Buka browser di CVM dan unduh paket penginstalan Microsoft SharePoint 2016 dari situs resmi Microsoft SharePoint 2016.
2. Buka file citra “Microsoft SharePoint 2016”, klik dua kali file `prerequisiteinstaller.exe` yang dapat dijalankan dari fitur persiapan untuk menginstal Fitur Persiapan Microsoft SharePoint 2016, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/1c6c2e0970ea456bbabd4a77ef454a5e.png)
3. Buka wizard penginstalan Fitur Persiapan Microsoft SharePoint 2016 dan klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/4b42cde60ca558a7c905c6f8031e3a50.png)
4. Pilih **I accept the terms of the License Agreement(s)** (Saya menyetujui persyaratan Perjanjian Lisensi), dan klik **Next** (Selanjutnya).
5. Setelah fitur persiapan diinstal, klik **Finish** (Selesai) untuk memulai ulang CVM.
![](https://main.qcloudimg.com/raw/a8c14625c359decb9941511e267ea2a6.png)
6. Buka file citra “Microsoft SharePoint 2016”, klik dua kali pada file penginstalan `setup.exe` untuk menginstal Microsoft SharePoint 2016.
![](https://main.qcloudimg.com/raw/2614739955551657148d9c3a72e566df.png)
7. Masukkan kunci produk, dan klik **Continue** (Lanjutkan).
8. Pilih **I accept the terms of this agreement** (Saya menyetujui persyaratan perjanjian ini), dan klik **Continue** (Lanjutkan).
9. Pilih direktori penginstalan (contoh ini mempertahankan konfigurasi default tetapi Anda dapat menentukan direktori sesuai kebutuhan), dan klik **Install Now** (Instal Sekarang).
![](https://main.qcloudimg.com/raw/3ea703e1632ec78b3f8f4b961c189208.png)
10. Setelah penginstalan selesai, pilih **Run the SharePoint Products Configuration Wizard now** (Jalankan Wizard Konfigurasi Produk SharePoint sekarang), dan klik **Close** (Tutup).
![](https://main.qcloudimg.com/raw/368fa9a4cdb3b47a77c554db855737e0.png)

### Langkah 5: mengonfigurasi SharePoint 2016

1. Di jendela **SharePoint Products Configuration Wizard** (Wizard Konfigurasi Produk SharePoint), klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/73aa25130b0e24e6784760a28d6d8fe2.png)
2. Klik **Yes** (Ya) di kotak dialog pop-up untuk mengizinkan layanan dimulai ulang selama konfigurasi.
3. Pilih **Create a new server farm** (Buat farm server baru), dan klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/b66da626c4883f2f2fb1b75bce6042f6.png)
4. Pada halaman **Specify Configuration Database Settings** (Tentukan Pengaturan Database Konfigurasi), atur database konfigurasi dan akun akses.
Database SharePoint ada di host lokal, jadi Anda harus memasukkan database dan akun lokal. Kemudian, klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/d1ccac780ddb9fb308b071fe385ad3f6.png)
5. Masukkan kata sandi farm server, lalu klik **Next** (Selanjutnya).
6. Pilih **Front-end** (Front-end) untuk “Farm Multi-Server”, lalu klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/c23051f73ae543002bc9c15d3d2b3387.png)
7. Tentukan nomor port Aplikasi Web Administrasi Pusat SharePoint (contoh ini menggunakan “10000” tetapi Anda dapat mengonfigurasi nomor sesuai kebutuhan), dan klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/c7622761e6eb45b1935fccc851379b29.png)
8. Konfirmasikan konfigurasi SharePoint, lalu klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/8d97c6aff42bb8b27fb3e108fa3d16d8.png)
9. Setelah konfigurasi selesai, klik **Finish** (Selesai).

