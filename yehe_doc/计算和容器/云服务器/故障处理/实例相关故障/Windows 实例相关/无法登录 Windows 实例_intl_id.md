Dokumen ini menjelaskan kemungkinan penyebab kegagalan login instans Windows dan metode pemecahan masalahnya. Anda dapat mengikuti petunjuk untuk mengidentifikasi penyebab masalah Anda dan mempelajari cara memperbaikinya.

## Kemungkinan Penyebab
Kegagalan untuk login ke instans Windows mungkin disebabkan oleh:
- [Masalah kata sandi](#CryptographicProblem)
- [Penggunaan bandwidth tinggi](#BandwidthUtilization)
- [Beban server tinggi](#HighServerLoad)
- [Konfigurasi port jarak jauh tidak tepat](#RemotePortConfiguration)
- [Aturan grup keamanan tidak tepat](#SafetyGroupRule)
- [Pengecualian yang disebabkan oleh firewall atau perangkat lunak keamanan](#LoginSecuritySoftware)
- [Kesalahan autentikasi selama akses melalui desktop jarak jauh](#AuthenticationError)

Jika Anda tidak dapat memecahkan masalah dengan alat diagnosis, kami sarankan Anda [login melalui VNC](#VNC) dan ikuti petunjuk pada CVM.

<span id="TroubleshootingIdeas"></span>
## Pemecahan Masalah

<span id="VNC"></span>
### Login melalui VNC

Jika Anda tidak dapat login ke instans Windows melalui RDP atau perangkat lunak akses jarak jauh, Anda dapat login melalui VNC, yang membantu Anda mengidentifikasi penyebab masalah.
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman manajemen instans, pilih intans yang akan diakses dan klik **Log In** (Login), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Di jendela **Log into Windows instance** (Login ke instans Windows) yang muncul, pilih **Alternative methods (VNC)** (Metode alternatif (VNC)) dan klik **Log In Now** (Login Sekarang).
> Jika Anda lupa kata sandi untuk instans, Anda dapat mengatur ulang di konsol. Untuk informasi selengkapnya, lihat [Mengatur Ulang Kata Sandi Instans](https://intl.cloud.tencent.com/document/product/213/16566).
>
4. Pada jendela login yang muncul, pilih **Send CtrlAltDel** (Kirim CtrlAltDel) di sudut kiri atas, dan tekan **Ctrl-Alt-Delete** (Ctrl-Alt-Delete) untuk membuka jendela login sistem, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)


<span id="CryptographicProblem"></span>
### Masalah kata sandi

**Problem** (Masalah): upaya login gagal karena Anda lupa kata sandi, memasukkan kata sandi yang salah, atau gagal mengatur ulang kata sandi.
**Procedure** (Prosedur): atur ulang kata sandi untuk instans ini di [Konsol CVM](https://console.cloud.tencent.com/cvm/index) dan mulai ulang instans. Untuk informasi selengkapnya, lihat [Mengatur Ulang Kata Sandi Instans](https://intl.cloud.tencent.com/document/product/213/16566).

<span id="BandwidthUtilization"></span>
### Penggunaan bandwidth tinggi

**Procedure** (Prosedur):
1. Login ke instans dengan menggunakan [login VNC](#VNC).
2. Periksa penggunaan bandwidth instans dan atasi masalah yang sesuai. Untuk detailnya, lihat [Kegagalan Login Karena Pendudukan Bandwidth Tinggi](https://intl.cloud.tencent.com/document/product/213/32542).

<span id="HighServerLoad"></span>
### Beban server tinggi

**Problem** (Masalah): Cloud Monitor menunjukkan beban yang tinggi pada CPU server, dan sistem tidak dapat diakses dari jarak jauh atau aksesnya lambat.
**Possible cause** (Kemungkinan penyebab): virus, trojan, perangkat lunak antivirus pihak ketiga, pengecualian aplikasi, pengecualian driver, dan pembaruan otomatis perangkat lunak di backend dapat menyebabkan penggunaan CPU yang tinggi, menyebabkan kegagalan login CVM atau akses lambat.
**Procedure** (Prosedur):
1. Login ke instans dengan menggunakan [login VNC](#VNC).
2. Di **Task Manager** (Pengelola Tugas), temukan proses yang menyebabkan beban tinggi. Untuk detailnya, lihat [Gagal Login ke CVM Windows Karena Penggunaan CPU dan Memori yang Tinggi](https://intl.cloud.tencent.com/document/product/213/32405).

<span id="RemotePortConfiguration"></span>
### Konfigurasi port jarak jauh tidak benar

**Problem** (Masalah): upaya akses jarak jauh ke instans gagal, port akses jarak jauh bukan port default atau telah dimodifikasi, atau port 3389 tidak terbuka.
**Diagnosis** (Diagnosis): lakukan ping ke alamat IP publik instans untuk memeriksa konektivitas jaringan dan jalankan telnet untuk memeriksa apakah port terbuka.
**Procedure** (Prosedur): Lihat [Kegagalan Login Jarak Jauh Karena Masalah Port](https://intl.cloud.tencent.com/document/product/213/32540) untuk prosedur terperinci.

<span id="SafetyGroupRule"></span>
### Aturan grup keamanan yang tidak tepat

**Procedure** (Prosedur): Pecahkan masalah dengan [alat verifikasi grup keamanan (port)](https://console.cloud.tencent.com/vpc/helper).
> Untuk instans Windows yang login dari jarak jauh, Anda perlu membuka port 3389.
> 
![](https://main.qcloudimg.com/raw/27b5aa974a2263719574dfc3bb7c0c6d.png)
Jika masalah disebabkan oleh masalah port grup keamanan, Anda dapat menggunakan fungsi **Open all ports** (Buka semua port) untuk membuka semua port.
![](https://main.qcloudimg.com/raw/bd91ec53dfd0df6bd1127a7f4f9db35c.png)
Untuk menentukan aturan khusus bagi grup keamanan, lihat [Menambahkan Aturan untuk Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).


<span id="LoginSecuritySoftware"></span>
### Pengecualian yang disebabkan oleh firewall atau perangkat lunak keamanan

**Problem** (Masalah): upaya login gagal karena firewall CVM atau software keamanan.
**Diagnosis** (Diagnosis): login ke instans Windows melalui VNC untuk memeriksa apakah firewall diaktifkan dan apakah perangkat lunak keamanan seperti 360 Total Security atau dongle keamanan diinstal di server.
> Operasi ini melibatkan dilakukannya pematian firewall CVM. Untuk melakukannya, periksa apakah Anda memiliki izin yang sesuai.
>
**Procedure** (Prosedur): matikan firewall atau perangkat lunak keamanan yang diinstal, lalu coba akses lagi dari jarak jauh. Misalnya, Anda dapat mematikan firewall Windows Server 2016 sebagai berikut:
1. Login ke instans dengan menggunakan [login VNC](#VNC).
2. Di desktop sistem operasi, klik <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"> dan pilih **Control Panel** (Panel Kontrol).
3. Di jendela **Control Panel** (Panel Kontrol), klik **Windows Firewall** (Windows Firewall).
4. Di jendela **Windows Firewall** (Windows Firewall), klik **Enable or Disable Windows Firewall** (Aktifkan atau Nonaktifkan Windows Firewall) di sebelah kiri untuk membuka **Custom Settings** (Pengaturan Kustom).
5. Atur **Private Network Settings** (Pengaturan Jaringan Pribadi) dan **Public Network Settings** (Pengaturan Jaringan Publik) ke **Disable Windows Firewall** (Nonaktifkan Windows Firewall), lalu klik **OK** (OKE).
6. Mulai ulang instans dan coba akses dari jarak jauh lagi.

<span id="AuthenticationError"></span>
### Kesalahan autentikasi selama akses melalui desktop jarak jauh

**Problem** (Masalah): saat Anda mencoba login ke instans Windows melalui desktop jarak jauh, prompt yang menyatakan "Authentication error. Invalid flag is provided to the function." (Kesalahan autentikasi. Bendera yang tidak valid disediakan untuk fungsi tersebut.) atau "Authentication error. The required function is not supported." (Kesalahan autentikasi. Fungsi yang diperlukan tidak didukung.) muncul.
**Possible cause** (Kemungkinan penyebab): Microsoft merilis pembaruan keamanan pada Maret 2018. Pembaruan ini memperbaiki kerentanan eksekusi kode jarak jauh di program pendukung keamanan kredensial (CredSSP) dengan mengoreksi bagaimana CredSSP memvalidasi permintaan selama proses autentikasi. Klien dan server perlu diperbarui atau kesalahan sebelumnya dapat terjadi.
**Procedure** (Prosedur): instal pembaruan keamanan (direkomendasikan). Untuk detailnya, lihat [Terjadi Kesalahan Autentikasi saat Anda Mencoba Login ke Instans Windows dari Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32421).

## Solusi Lain
Setelah mencoba metode sebelumnya, jika Anda masih tidak dapat login ke instans Window, harap simpan hasil diagnosis mandiri Anda dan [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk bantuan.
