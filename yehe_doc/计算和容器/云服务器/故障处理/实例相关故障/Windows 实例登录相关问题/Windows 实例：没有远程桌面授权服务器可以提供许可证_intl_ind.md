Dokumen ini menjelaskan cara mengelola permintaan alarm seperti "Remote session has been disconnected as no remote desktop authorization server is available for licensing" (Sesi jarak jauh telah diputus koneksinya karena tidak ada server otorisasi desktop jarak jauh yang tersedia untuk pemberian lisensi) saat Anda mencoba menghubungkan ke instans Windows dari jarak jauh.

## Masalah

Ketika Anda mencoba untuk menghubungkan ke instans Windows menggunakan Windows Remote Desktop, prompt yang menyatakan "Remote session has been disconnected as no remote desktop authorization server is available for licensing. For assistance, please contact your system administrator" (Sesi jarak jauh telah diputus sambungannya karena tidak ada server otorisasi desktop jarak jauh yang tersedia untuk lisensi. Untuk bantuan, hubungi administrator sistem Anda) muncul, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/0034f9d4e822ca556bd54dafb9b13c17.png)

## Analisis Masalah

Kemungkinan penyebab masalah ini termasuk tetapi tidak terbatas pada hal berikut. Oleh karena itu, selalu analisis masalahnya berdasarkan situasi aktual.
- Batas RDP-TCP ditetapkan oleh sistem secara default, dan hanya mengizinkan satu sesi untuk setiap pengguna. Jika akun sudah login, tidak ada sesi tambahan yang dapat dibuat.
- Fitur peran "Remote Desktop Session Host" (Host Sesi Desktop Jarak Jauh) telah ditambahkan oleh sistem, tetapi masa berlaku fitur tersebut telah kedaluwarsa.
Fitur peran "Remote Desktop Session Host" (Host Sesi Desktop Jarak Jauh) gratis untuk digunakan selama 120 hari. Setelah periode tersebut, Anda harus membayar fitur tersebut untuk terus menggunakannya.

### Solusi
### Login CVM melalui VNC

1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman manajemen instans, cari instans CVM target dan klik **Log In** (Login), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Di jendela **Log in to Windows instance** (Login ke instans Windows) yang muncul, pilih **Alternative login methods (VNC)** (Metode login alternatif (VNC)), dan klik **Log In Now** (Login Sekarang) untuk login ke CVM.
4. Di jendela login yang muncul, pilih **Send Remote Command** (Kirim Perintah Jarak Jauh) di sudut kiri atas, dan tekan **Ctrl-Alt-Delete** (Ctrl-Alt-Delete) untuk masuk ke antarmuka login sistem, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Solusi 1: Memodifikasi konfigurasi kebijakan
1. Pada antarmuka sistem operasi, klik <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> untuk membuka jendela Windows PowerShell.
2. Di jendela Windows PowerShell, masukkan **gpedit.msc** (gpedit.msc) dan tekan **Enter** (Enter) untuk membuka **Local Group Policy Editor** (Editor Kebijakan Grup Lokal).
3. Di pohon navigasi kiri, pilih **Computer Configuration**(Konfigurasi Komputer) > **Administrative Templates** (Templat Administratif) > **Windows Components** (Komponen Windows) > **Remote Desktop Services** (Layanan Desktop Jarak Jauh) > **Remote Desktop Session Host** (Host Sesi Desktop Jarak Jauh) > **Connections** (Koneksi), dan klik dua kali **Limit number of connections** (Batasi jumlah koneksi), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/e0420d2bb8ddd3e1524ee688173cb9d1.png)
4. Di jendela "Limit number of connections" (Batasi jumlah koneksi) yang muncul, ubah **Maximum RD connections supported** (Koneksi RD maksimum yang didukung) dan klik **OK** (Oke), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/066c9dfb06dc4c092424c4e1142f7471.png)
5. Beralih ke jendela Windows PowerShell.
6. Di jendela Windows PowerShell, masukkan **gpupdate** (gpupdate) dan tekan **Enter** (Enter) untuk memperbarui kebijakan.


### Solusi 2: Hapus peran "Remote Desk Session Host" (Host Sesi Desktop Jarak Jauh)
> Jika Anda ingin mempertahankan peran "Remote Desktop Session Host" (Host Sesi Desktop Jarak Jauh), lewati langkah ini dan buka [situs web resmi Microsoft](https://www.microsoft.com/) untuk membeli dan mengonfigurasi sertifikat yang sesuai.
>
1. Pada antarmuka sistem operasi, klik <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"> untuk membuka **Server Manager** (Pengelola Server).
2. Klik **Manage** (Kelola) di sudut kanan atas jendela "Server Manager" (Pengelola Server) dan pilih **Delete role and features** (Hapus peran dan fitur), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/373ef0a31c2b8e8fd1539e29852c4fab.png)
3. Di wizard "Delete roles and features" (Hapus peran dan fitur), klik **Next** (Selanjutnya).
4. Pada halaman "Delete server roles" (Hapus peran server), hapus centang **Remote Desktop Services** (Layanan Desktop Jarak Jauh). Pada kotak prompt yang muncul, pilih **Remove Feature** (Hapus Fitur).
6. Klik **Next** (Selanjutnya) dua kali.
6. Centang **Restart the destination server automatically if required** (Mulai ulang server tujuan secara otomatis jika diperlukan), dan klik **Yes** (Ya) di kotak prompt yang muncul.
8. Klik **Delete** (Hapus).
Tunggu hingga CVM dimulai ulang.






