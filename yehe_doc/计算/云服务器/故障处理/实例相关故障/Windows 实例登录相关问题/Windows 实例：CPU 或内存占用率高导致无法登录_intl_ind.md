Dokumen ini menjelaskan cara memecahkan masalah kegagalan login CVM Windows karena penggunaan CPU atau memori yang tinggi.
>? Contoh berikut ini menggunakan Windows Server 2012 R2. Langkah-langkahnya mungkin berbeda menurut versi sistem operasi (OS).

## Kemungkinan Penyebab

Perangkat keras, proses sistem, proses layanan, trojan, dan virus dapat menyebabkan penggunaan CPU atau memori yang tinggi, mengakibatkan kecepatan respons layanan yang lambat atau kegagalan login CVM. Anda dapat menggunakan [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248/32799) untuk membuat ambang batas alarm untuk penggunaan CPU atau memori. Anda akan segera diberi tahu ketika ambang batas yang dikonfigurasi terlampaui.

### Pemecahan Masalah

1. Identifikasi proses yang menyebabkan penggunaan CPU atau memori yang tinggi.
2. Analisis prosesnya.
 - Jika prosesnya tidak sehat, mungkin disebabkan oleh virus atau trojan. Hentikan proses atau gunakan aplikasi antivirus untuk memindai sistem.
 - Jika ini adalah proses layanan, periksa apakah penggunaan CPU atau memori yang tinggi disebabkan oleh lalu lintas akses dan apakah itu dapat dioptimalkan.
 - Jika ini adalah proses komponen Tencent Cloud, [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk bantuan.

## Alat

**Task Manager** (Pengelola Tugas): aplikasi dan pengelola proses yang disertakan dengan OS Microsoft Windows. Ini memberikan informasi tentang performa komputer dan perangkat lunak yang berjalan, seperti nama proses yang berjalan, beban CPU, penggunaan memori, I/O, pengguna yang telah login, dan layanan Windows.
- **Processes** (Proses): daftar dari semua proses yang berjalan.
- **Performance** (Performa): statistik performa sistem seperti penggunaan CPU secara keseluruhan dan penggunaan memori saat ini.
- **Users** (Pengguna): semua pengguna dengan sesi.
- **Details** (Detail): versi tab proses yang ditingkatkan, termasuk informasi detail tentang PID, status, penggunaan CPU, dan penggunaan memori.
- **Services** (Layanan): daftar dari semua layanan, termasuk yang tidak berjalan.


## Metode Pemecahan Masalah

### Login ke instans CVM menggunakan VNC
>? Jika Anda tidak dapat login ke instans CVM karena penggunaan CPU atau memori yang tinggi, sebaiknya [login ke instans Windows melalui VNC](https://intl.cloud.tencent.com/document/product/213/32496). 
>
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman manajemen instans, cari instans CVM dan klik **Log In** (Login), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Di jendela pop-up "Log into Windows instance" (Login ke instans Windows), pilih **Alternative login methods (VNC)** (Metode login alternatif (VNC)) dan klik **Log In Now** (Login Sekarang) untuk login ke instans CVM.
4. Di jendela login pop-up, pilih "Send CtrlAltDel" (Kirim CtrlAltDel) di sudut kiri atas dan klik **Ctrl-Alt-Delete** (Ctrl-Alt-Delete) untuk membuka halaman login OS, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Melihat penggunaan sumber daya dari proses

1. Di CVM, klik kanan "taskbar" (bilah tugas) dan pilih **Task Manager** (Pengelola Tugas), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/a795f4948fae3eab8a44ec0a3a4ee352.png)
2. Lihat penggunaan sumber daya di jendela "Task Manager" (Pengelola Tugas), seperti yang ditunjukkan pada gambar berikut:
>? Anda dapat mengklik kolom CPU atau memori untuk mengurutkan proses dalam urutan menaik atau menurun.
>
![](https://main.qcloudimg.com/raw/56a4be427be5046a15a05b02abbacf66.png)

### Menganalisis proses

Menganalisis proses di Task Manager untuk mengidentifikasi penyebab dan memecahkan masalah yang sesuai.
#### Proses sistem menyebabkan masalah
Jika proses sistem menyebabkan penggunaan CPU dan memori yang tinggi, selesaikan masalah dengan cara berikut:
1. Periksa nama prosesnya.
 Beberapa virus menggunakan nama yang mirip dengan proses sistem, seperti svch0st.exe, explore.exe, iexplorer.exe, dll.
2. Periksa lokasi file yang dapat dieksekusi dari suatu proses.
 File yang dapat dieksekusi dari proses sistem biasanya terletak di `C:\Windows\System32` dengan tanda tangan dan deskripsi yang valid. Untuk menemukan file yang dapat dieksekusi dari suatu proses, seperti `svchost.exe`, klik kanan proses di Task Manager dan pilih **Open file location** (Buka lokasi file).
 - Jika file yang dapat dieksekusi tidak ada di `C:\Windows\System32`, instans CVM Anda mungkin terkena virus. Pindai virus dengan aplikasi antivirus atau perbaiki masalah secara manual.
 - Jika file yang dapat dieksekusi ada di `C:\Windows\System32`, mulai ulang instans CVM Anda atau hentikan proses sistem yang tidak perlu tetapi aman.

Berikut daftar proses sistem yang umum:
 - Proses Diam Sistem: proses yang menampilkan persentase waktu prosesor dalam keadaan diam
 - system: menunjukkan proses manajemen memori
 - explorer: menunjukkan proses manajemen desktop dan file
 - iexplore: menunjukkan proses Microsoft Internet Explorer
 - csrss: menunjukkan subsistem runtime pada klien atau server Microsoft
 - svchost: menunjukkan proses sistem untuk menjalankan DLL
 - Taskmgr: menunjukkan manajer tugas
 - Isass: menunjukkan layanan otoritas keamanan lokal

#### Proses yang tidak sehat menyebabkan masalah
Jika penggunaan CPU atau memori yang tinggi disebabkan oleh proses yang memiliki nama aneh, seperti xmr64.exe (malware cryptomining), instans CVM Anda mungkin terkena virus atau trojan. Sebaiknya Anda menggunakan mesin pencari untuk memverifikasi.
 - Jika prosesnya adalah virus atau trojan, gunakan aplikasi antivirus untuk menghapus virus atau trojan tersebut. Jika perlu, lakukan pencadangan data dan instal ulang sistem operasi.
 - Jika prosesnya bukan virus atau trojan, mulai ulang instans CVM Anda atau hentikan proses yang tidak perlu tetapi aman.

#### Proses layanan menyebabkan masalah
Jika proses layanan seperti IIS, HTTPD, PHP, atau Java menyebabkan masalah, sebaiknya analisis lebih lanjut.
Misalnya, periksa apakah volume bisnis Anda tinggi.
- Jika ya, kami sarankan [mengupgrade konfigurasi](https://intl.cloud.tencent.com/document/product/213/2178) untuk instans CVM Anda. Atau, Anda dapat mengoptimalkan proses layanan.
- Jika tidak, gunakan log kesalahan layanan untuk menganalisis lebih lanjut masalah tersebut. Misalnya, periksa apakah konfigurasi parameter yang salah menyebabkan pemborosan sumber daya.

#### Proses Tencent Cloud menyebabkan masalah

- Jika proses komponen Tencent Cloud menyebabkan masalah, [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk menghubungi kami untuk mendapatkan bantuan.

