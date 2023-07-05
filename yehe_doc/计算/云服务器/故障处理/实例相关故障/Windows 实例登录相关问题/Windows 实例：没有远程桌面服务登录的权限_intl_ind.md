## Deskripsi Kesalahan

<span id="FaultPhenomenon1"> </span>
**Case 1** (Kasus 1): Saat mencoba terhubung ke instans Windows melalui Desktop Jarak Jauh dari Windows, pengguna melihat kesalahan yang mengatakan **The connection was denied because the user account is not authorized for remote login.** (Koneksi ditolak karena akun pengguna tidak diotorisasi untuk login jarak jauh.)

<span id="FaultPhenomenon2"> </span>
**Case 2** (Kasus 2): Saat mencoba menghubungkan ke instans Windows melalui Desktop Jarak Jauh Windows, pengguna melihat kesalahan yang mengatakan **To sign in remotely, you need the right to sign in through Remote Desktop Services. By default, members of the Remote Desktop Users group have this right. If the group you’re in doesn’t have the right, or if the right has been removed from the Remote Desktop Users group, you need to be granted the right manually.** (Untuk masuk dari jarak jauh, Anda memerlukan hak untuk masuk melalui Layanan Desktop Jarak Jauh. Secara default, anggota grup Pengguna Desktop Jarak Jauh memiliki hak ini. Jika grup tempat Anda berada tidak memiliki hak ini, atau jika hak sudah dihapus dari grup Pengguna Desktop Jarak Jauh, Anda harus diberikan hak tersebut secara manual.)

## Kemungkinan Alasan

Pengguna tidak diizinkan untuk login ke instans Windows melalui koneksi Desktop Jarak Jauh.

## Solusi
- Untuk [Kasus 1](#FaultPhenomenon1), tambahkan akun pengguna ke daftar akun yang diizinkan oleh instans Windows untuk login melalui Layanan Desktop Jarak Jauh. Untuk petunjuk detail, lihat [Mengizinkan login jarak jauh](#ConfigurationToAllowAccess).
- Untuk [Kasus 2](#FaultPhenomenon2), hapus akun pengguna dari daftar akun yang ditolak oleh instans Windows untuk login melalui Layanan Desktop Jarak Jauh. Untuk petunjuk detail, lihat [Menolak login jarak jauh](#ModifyLoginAuthority).

## Petunjuk

### Login ke CVM menggunakan VNC
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman manajemen instans, cari instans CVM target dan klik **Log In** (Login), seperti yang ditunjukkan pada gambar berikut:
![Halaman daftar CVM](https://main.qcloudimg.com/raw/bd24015a7332c824e649c034417f708d.png)
3. Pada jendela **Log in to Windows Instance** (Login ke Instans Windows) yang muncul, pilih “Alternative login methods (VNC)” (Metode login alternatif (VNC)), klik **Log In Now** (Login Sekarang) untuk login ke CVM.
4. Pada jendela login yang muncul, pilih **Send CtrlAltDel** (Kirim CtrlAltDel) di sudut kiri atas, dan tekan **Ctrl-Alt-Delete** (Ctrl-Alt-Delete) untuk membuka jendela login sistem, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)


<span id="ConfigurationToAllowAccess"> </span>
### Mengizinkan login jarak jauh

>? Operasi berikut menggunakan contoh Windows Server 2016.
>
1. Di desktop, klik <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, masukkan **gpedit.msc**, dan tekan **Enter** untuk membuka “Local Group Policy Editor” (Editor Kebijakan Grup Lokal).
2. Di pohon navigasi kiri, pilih **Computer Configuration** (Konfigurasi Komputer) > **Windows Settings** (Pengaturan Windows) > **Security Settings** (Pengaturan Keamanan) > **Local Policies** (Kebijakan Lokal) > **User Rights Assignment** (Penetapan Hak Pengguna), dan klik kanan **Allow log on through Remote Desktop Services** (Izinkan logon melalui Layanan Desktop Jarak Jauh).
![](https://main.qcloudimg.com/raw/69a452fc83bb2d9013c1830ae67996ac.png)
3. Di jendela “Allow log on through Remote Desktop Services Properties” (Izinkan logon melalui Properti Layanan Desktop Jarak Jauh) yang muncul, periksa apakah akun pengguna yang ingin Anda gunakan untuk login jarak jauh ada di daftar pengguna “Allow log on through Remote Desktop Services” (Izinkan logon melalui Layanan Desktop Jarak Jauh).
![Izinkan logon melalui Layanan Desktop Jarak Jauh](https://main.qcloudimg.com/raw/a3d28bd18e13fe2c0ce1fceb850a3284.png)
 - Jika pengguna tidak ada dalam daftar, lanjutkan ke [langkah 4](#step04).
 - Jika pengguna ada dalam daftar, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
4. <span id="step04">Klik **Add User or Group** (Tambahkan Pengguna atau Grup) untuk membuka jendela **Select User or Group** (Pilih Pengguna atau Grup).</span>
5. Masukkan akun yang ingin Anda gunakan untuk login jarak jauh lalu klik **OK** (Oke).
6. Klik **OK** (Oke) dan tutup “Editor Kebijakan Grup Lokal” (Editor Kebijakan Grup Lokal).
7. Mulai ulang instans dan coba hubungkan ke instans Windows dengan akun melalui Desktop Jarak Jauh lagi.


<span id="ModifyLoginAuthority"> </span>
### Menolak login jarak jauh

>? Operasi berikut menggunakan contoh Windows Server 2016.
>
1. Di desktop, klik <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, masukkan **gpedit.msc**, dan tekan **Enter** untuk membuka “Local Group Policy Editor” (Editor Kebijakan Grup Lokal).
2. Di pohon navigasi kiri, pilih **Computer Configuration** (Konfigurasi Komputer) > **Windows Settings** (Pengaturan Windows) > **Security Settings** (Pengaturan Keamanan) > **Local Policies** (Kebijakan Lokal) > **User Rights Assignment** (Penetapan Hak Pengguna), dan klik dua kali **Deny log on through Remote Desktop Services** (Tolak logon melalui Layanan Desktop Jarak Jauh) seperti yang ditunjukkan di bawah ini:
![Tolak logon melalui Layanan Desktop Jarak Jauh](https://main.qcloudimg.com/raw/4c4d47a70c0d55e9c7de1f9351f4b0ab.png)
3. Di jendela pop-up, periksa apakah akun yang ingin Anda gunakan untuk login jarak jauh ada dalam daftar pengguna "Deny log in through Remote Desktop Services" (Tolak login melalui Layanan Desktop Jarak Jauh).
 - Jika pengguna ada dalam daftar, hapus akun pengguna dari daftar dan mulai ulang instans.
 - Jika pengguna tidak ada dalam daftar, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).

 

