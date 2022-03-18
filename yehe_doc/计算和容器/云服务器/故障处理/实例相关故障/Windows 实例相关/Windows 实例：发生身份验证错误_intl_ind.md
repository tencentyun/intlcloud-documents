## Deskripsi Masalah

Saat pengguna mencoba login ke instans Windows melalui Koneksi Desktop Jarak Jauh, terjadi kesalahan.
- Pesan kesalahan menyatakan "Authentication error. The token supplied to the function is invalid." (Kesalahan autentikasi. Token yang diberikan ke fungsi tidak valid.).
- "Authentication error. The requested function is not supported." (Kesalahan autentikasi. Fungsi yang diminta tidak didukung.).

## Analisis Masalah

Microsoft menerbitkan pembaruan keamanan pada Maret 2018. Dengan mengoreksi bagaimana protokol Penyedia Dukungan Keamanan Kredensial (CredSSP) memvalidasi permintaan selama autentikasi, pembaruan ini memperbaiki kerentanan eksekusi kode jarak jauh di CredSSP. Klien dan server perlu menginstal pembaruan keamanan, atau kesalahan sebelumnya mungkin terjadi.
Koneksi jarak jauh gagal dalam kondisi berikut:

- Kondisi 1: pembaruan keamanan diinstal pada server tetapi tidak pada klien, dan kebijakan "memaksa klien diperbarui" dikonfigurasi.
- Kondisi 2: pembaruan keamanan diinstal pada klien tetapi tidak pada server, dan kebijakan "memaksa klien diperbarui" dikonfigurasi.
- Kondisi 3: pembaruan keamanan diinstal pada klien tetapi tidak pada server, dan kebijakan "dikurangi" dikonfigurasi.

## Solusi

> Jika Anda hanya perlu mengupgrade klien secara lokal, gunakan [Solusi 1: Menginstal pembaruan keamanan (direkomendasikan)](#langkah4).
>
### Login ke CVM menggunakan VNC

1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Di halaman manajemen instans, cari instans CVM target dan klik **Log In** (Login).
3. Di jendela **Log into Windows instance** (Login ke instans Windows) yang muncul, pilih **Alternative login methods (VNC)** (Metode login alternatif (VNC)), lalu klik **Log In Now** (Login Sekarang).
4. Di jendela login yang muncul, pilih **Send CtrlAltDel** ( Kirim CtrlAltDel) di sudut kiri atas dan klik **Ctrl-Alt-Delete** (Ctrl-Alt-Delete) untuk membuka halaman login sistem.

<span id="step4"></span>
### Solusi 1: Menginstal pembaruan keamanan (direkomendasikan)

Instal pembaruan keamanan pada klien atau server yang belum di-patching. Untuk pembaruan pada sistem operasi yang berbeda, lihat [CVE-2018-0886 | Kerentanan eksekusi kode jarak jauh CredSSP](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886). Solusi ini menggunakan Windows Server 2016 sebagai contoh.
Di sistem operasi lain, Anda dapat menggunakan metode berikut untuk membuka **Windows Update** (Pembaruan Windows).
- Windows Server 2012: <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;width: 22px;"></img> > **Control Panel** (Panel Kontrol) > **System and Security** (Sistem dan Keamanan) > **Windows Update** (Pembaruan Windows)
- Windows Server 2008: **Start** (Mulai) > **Control Panel** (Panel Kontrol) > **System and Security** (Sistem dan Keamanan) > **Windows Update** (Pembaruan Windows)
- Windows 10: <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> > **Settings** (Pengaturan) > **Update and Security** (Pembaruan dan Keamanan)
- Windows 7: <img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: 0;width: 28px;"></img> > **Control Panel** (Panel Kontrol) > **System and Security** (Sistem dan Keamanan) > **Windows Update** (Pembaruan Windows)


1. Di desktop, klik <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> dan pilih **Settings** (Pengaturan).
2. Di jendela **Settings** (Pengaturan), pilih **Update and Security** (Pembaruan dan Keamanan).
3. Pada halaman **Update and Security** (Pembaruan dan Keamanan), pilih **Windows Update** (Pembaruan Windows) dan klik **Check for updates** (Periksa pembaruan).
4. Klik **Install updates** (Instal pembaruan).
5. Setelah penginstalan selesai, mulai ulang instans untuk menyelesaikan pembaruan.

### Solusi 2: Memodifikasi kebijakan

Dalam CVM dengan pembaruan keamanan yang diinstal, atur kebijakan **Encryption Oracle Remediation** (Enkripsi Remediasi Oracle) ke **vulnerable** (rentan). Solusi ini menggunakan Windows Server 2016 sebagai contoh. Selesaikan langkah-langkah berikut.
> Jika tidak ada editor kebijakan grup yang tersedia di sistem operasi Windows 10 Home, Anda dapat mengubah kebijakan di registri. Untuk detailnya, lihat [Solusi 3: Memodifikasi registri](#Plan3).
>
1. Di desktop, klik <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>, masukkan **gpedit.msc**, dan tekan **Enter** untuk membuka "Local Group Policy Editor" (Editor Kebijakan Grup Lokal).
> Anda juga dapat menekan **Win+R** (Win+R) untuk membuka kotak dialog **Run** (Jalankan).
>
3. Di pohon navigasi sisi kiri, pilih **Computer Configuration** (Konfigurasi Komputer) > **Administrative Templates** (Templat Administratif) > **System** (Sistem) > **Credentials Delegation** (Delegasi Kredensial) dan klik dua kali **Encryption Oracle Remediation** (Enkripsi Remediasi Oracle).
4. Di jendela **Encryption Oracle Remediation** (Enkripsi Remediasi Oracle), pilih **Enabled** (Diaktifkan) dan atur **Protection Level** (Tingkat Perlindungan) ke **Vulnerable** (Rentan).
5. Klik **OK** (Oke) untuk menyelesaikan konfigurasi.

<span id="Plan3"></span>
### Solusi 3: Memodifikasi registri

1. Di desktop, klik <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>, masukkan **regedit**, dan tekan **Enter** untuk membuka "Registry Editor" (Editor Registri).
> Anda juga dapat menekan **Win+R** (Win+R) untuk membuka kotak dialog **Run** (Jalankan).
> 
2. Di pohon navigasi sisi kiri, pilih **Computer** (Komputer) > **HKEY_LOCAL_MACHINE** (HKEY_LOCAL_MACHINE) > **Software** (Perangkat Lunak) > **Microsoft** > **Windows** > **CurrentVersion** > **Policies** (Kebijakan) > **System** (Sistem) > **CredSSP** > **Parameters** (Parameter).
> Jika jalur ini tidak ada, buat jalur secara manual.
>
4. Klik kanan **Parameters** (Parameter) , pilih **New** (Baru) > **DWORD (32-bit) value** (Nilai DWORD (32-bit)), dan beri nama file "AllowEncryptionOracle".
5. Klik dua kali file "AllowEncryptionOracle" yang baru dibuat, atur "Data nilai" ke "2", dan klik **OK** (Oke).
6. Mulai ulang instans.

## Dokumen Terkait

- [CVE-2018-0886 | Kerentanan eksekusi kode jarak jauh CredSSP](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)
- [Pembaruan CredSSP untuk CVE-2018-0886](https://support.microsoft.com/zh-cn/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)
