## Skenario
Very Secure FTP Daemon (Vsftpd) adalah server FTP default untuk sebagian besar distribusi Linux. Dokumen ini menggunakan CentOS 7.6 64-bit CVM sebagai contoh untuk menjelaskan cara menggunakan vsftpd untuk menyiapkan layanan FTP untuk CVM Linux.

## Perangkat Lunak
Berikut ini daftar program perangkat lunak untuk menyiapkan layanan FTP.
- Linux: Citra publik CentOS 7.6
- Vsftpd: vsftpd 3.0.2


## Petunjuk
### Langkah 1: Login ke CVM
[Login ke instans Linux menggunakan WebShell (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan salah satu metode login berikut yang paling nyaman bagi Anda.
- [Login ke instans Linux menggunakan perangkat lunak login jarak jauh](https://intl.cloud.tencent.com/document/product/213/32502)
- [Login ke instans Linux menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Langkah 2: Instal vsftpd
1. Jalankan perintah berikut untuk menginstal vsftpd:
```
yum install -y vsftpd
```
2. Jalankan perintah berikut untuk memulai vsftpd secara otomatis saat startup sistem:
```
systemctl enable vsftpd
```
3. Jalankan perintah berikut untuk memulai layanan FTP:
```
systemctl start vsftpd
```
4. Jalankan perintah berikut untuk memeriksa apakah layanan telah dimulai:
```
netstat -antup | grep ftp
```
Jika informasi berikut muncul, layanan FTP telah dimulai.
![](https://main.qcloudimg.com/raw/2a7abf80253a8469c9340878d89b452a.png)
Secara default, vsftpd telah mengaktifkan mode akses anonim. Anda dapat login ke server FTP tanpa memasukkan nama pengguna atau kata sandi. Namun, Anda tidak memiliki izin untuk mengubah atau mengunggah file dalam mode login ini.

<span id="user"></span>
### Langkah 3: Konfigurasikan vsftpd
1. Jalankan perintah berikut untuk membuat pengguna untuk layanan FTP, yaitu ftpuser dalam hal ini:
```
useradd ftpuser
```
2. Jalankan perintah berikut untuk mengatur kata sandi untuk ftpuser:
```
passwd ftpuser
```
Setelah memasukkan kata sandi, tekan **Enter** (Enter) untuk mengonfirmasi. Secara default, kata sandi tidak ditampilkan. Di sini, `tf7295TFY` digunakan sebagai contoh kata sandi.
3. Jalankan perintah berikut untuk membuat direktori file untuk layanan FTP, yaitu `/var/ftp/test` dalam hal ini:
```
mkdir /var/ftp/test
```
4. Jalankan perintah berikut untuk mengubah izin direktori:
```
chown -R ftpuser:ftpuser /var/ftp/test
```
5. Jalankan perintah berikut untuk membuka file `vsftpd.conf`:
```
vim /etc/vsftpd/vsftpd.conf
```
6. Tekan **i** (i) untuk beralih ke mode pengeditan. Pilih mode FTP berdasarkan kebutuhan aktual Anda dan ubah file konfigurasi `vsftpd.conf`.
<span id="config"></span>
> Server FTP dapat terhubung ke klien dalam mode aktif atau pasif untuk transmisi data. Karena pengaturan firewall sebagian besar klien dan fakta bahwa alamat IP aktual tidak dapat diperoleh, sebaiknya gunakan mode pasif untuk menyiapkan layanan FTP. Modifikasi berikut menggunakan mode pasif sebagai contoh. Untuk menggunakan mode aktif, lihat [Mengatur mode aktif FTP](#port).
>
 1. Modifikasi parameter konfigurasi berikut untuk mengatur izin login untuk pengguna anonim dan lokal, mengatur jalur untuk menyimpan daftar pengguna yang luar biasa, dan mengaktifkan operasi mendengar pada soket IPv4.
```
anonymous_enable=NO
local_enable=YES
chroot_local_user=YES
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
listen=YES
```
  2. Tambahkan tanda pagar (`#`) di awal baris berikut untuk menyertakan keterangan `listen_ipv6=YES` dan menonaktifkan operasi mendengarkan pada soket IPv6.
```
#listen_ipv6=YES
```
  3. Tambahkan parameter konfigurasi berikut untuk mengaktifkan mode pasif, atur direktori tempat pengguna lokal berada setelah login, dan atur rentang port untuk mentransmisikan data oleh CVM.
```
local_root=/var/ftp/test
allow_writeable_chroot=YES
pasv_enable=YES
pasv_address=xxx.xx.xxx.xx # Ganti xxx.xx.xxx.xx dengan alamat IP publik CVM Linux Anda
pasv_min_port=40000
pasv_max_port=45000
```
7. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq). Kemudian, simpan perubahan dan tutup file.
<span id="create"></span>
8. Jalankan perintah berikut untuk membuat dan mengedit file `chroot_list`:
```
vim /etc/vsftpd/chroot_list
```
9. Tekan **i** (i) untuk login ke mode pengeditan, lalu masukkan nama pengguna. Perhatikan bahwa setiap nama pengguna menempati satu baris. Setelah menyelesaikan konfigurasi, tekan **Esc** (Esc) dan masukkan **:wq** (:wq). Kemudian, simpan perubahan dan tutup file.
Jika Anda tidak perlu mengatur pengguna luar biasa, lewati langkah ini dengan memasukkan **:wq** (:wq) dan menutup file.
10. Jalankan perintah berikut untuk memulai ulang layanan FTP:
```
systemctl restart vsftpd
```

### Langkah 4: Konfigurasikan grup keamanan
Setelah menyiapkan layanan FTP, konfigurasikan **inbound rules** (aturan masuk) untuk CVM Linux berdasarkan mode FTP yang digunakan secara aktual. Untuk detailnya, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).
Sebagian besar klien mengonversi alamat IP dalam LAN. Jika Anda menggunakan mode aktif FTP, pastikan bahwa klien telah memperoleh alamat IP aktual. Jika tidak, klien mungkin gagal login ke server FTP.
- Untuk mode aktif: buka port 21.
- Untuk mode pasif: buka port 21 dan semua port mulai dari `pasv_min_port` hingga `pasv_max_port` diatur dalam [file konfigurasi](#config), seperti port 40000 hingga 45000 dalam dokumen ini.

### Langkah 5: Verifikasi layanan FTP
Anda dapat memverifikasi server FTP menggunakan alat seperti klien FTP, browser, atau Windows Explorer. Di sini, Windows Explorer digunakan sebagai contoh.
1. Buka Internet Explorer pada klien, pilih **Tools** (Alat) > **Internet Options** (Opsi Internet), dan klik tab **Advanced** (Lanjutan). Lakukan modifikasi berikut berdasarkan mode FTP yang dipilih.
 - Untuk mode aktif: batalkan pilihan **Passive FTP** (FTP Pasif).
 - Untuk mode pasif: pilih **Passive FTP** (FTP Pasif).
2. Buka Windows Explorer pada klien, masukkan alamat berikut di kotak alamat dan tekan **Enter** (Enter), seperti yang ditunjukkan pada gambar berikut.
```
ftp://<CVM public IP address:21>
```
![](https://main.qcloudimg.com/raw/40cef1738cb1d2fad07d2ef219822d2f.png)
3. Pada halaman login yang muncul, masukkan nama pengguna dan kata sandi yang ditetapkan di [Mengonfigurasi vsftpd](#user).
Di sini, nama pengguna adalah `ftpuser` dan kata sandinya adalah `tf7295TFY`.
4. Setelah berhasil login, Anda dapat mengunggah dan mengunduh file.


## Lampiran
<span id="port"></span>
### Mengatur mode aktif FTP
Untuk menggunakan mode aktif, ubah parameter konfigurasi berikut dan biarkan parameter lain sebagai default:
```
anonymous_enable=NO      # Larang pengguna anonim untuk login
local_enable=YES         # Izinkan pengguna lokal untuk login
chroot_local_user=YES    # Batasi semua pengguna hanya untuk mengakses direktori root
chroot_list_enable=YES   # Aktifkan daftar pengguna yang luar biasa
chroot_list_file=/etc/vsftpd/chroot_list  # Tentukan daftar pengguna, tempat pengguna yang terdaftar tidak dibatasi hanya untuk mengakses direktori root
listen=YES               # Aktifkan operasi mendengarkan pada soket IPv4
# Tambahkan tanda pagar (#) di awal baris berikut untuk mengomentari parameter berikut.
#listen_ipv6=YES         # Nonaktifkan operasi mendengarkan pada soket IPv6
# Menambahkan parameter berikut
allow_writeable_chroot=YES
local_root=/var/ftp/test # Atur direktori tempat pengguna lokal berada setelah login
```
Tekan **Esc** (Esc) dan masukkan **:wq** (:wq). Kemudian, simpan perubahan dan tutup file. Setelah itu, buka [Langkah 8](#buat) untuk mengonfigurasi vsftpd.

### Gagal mengunggah file dari klien FTP
#### Deskripsi masalah
Di lingkungan Linux, pengguna menemukan pesan kesalahan berikut saat mengunggah file dengan vsftpd.
```
553 Tidak dapat membuat file
```

#### Solusi
1. Jalankan perintah berikut untuk memeriksa penggunaan ruang disk server:
```
df -h
```
 - Jika ruang disk tidak mencukupi, File tidak dapat diunggah. Dalam hal ini, sebaiknya hapus beberapa file besar yang tidak diperlukan dari disk.
 - Jika ruang disk cukup, lanjutkan ke langkah berikutnya.
2. Jalankan perintah berikut untuk memeriksa apakah Anda memiliki izin menulis ke direktori FTP:
```
ls -l /home/test      
# Di sini, /home/test menunjukkan direktori FTP. Ganti dengan direktori FTP aktual Anda.
```
 - Jika `w` tidak ditampilkan dalam hasil, Anda tidak memiliki izin menulis ke direktori. Dalam hal ini, lanjutkan ke langkah berikutnya.
 - Jika `w` ditampilkan dalam hasil, [kirimkan tiket](https://console.cloud.tencent.com/workorder/category) untuk pemecahan masalah lebih lanjut.
3. Jalankan perintah berikut untuk memberikan izin menulis ke direktori FTP:
```
chmod +w /home/test 
# Di sini, /home/test menunjukkan direktori FTP. Ganti dengan direktori FTP aktual Anda.
```
4. Jalankan perintah berikut untuk memeriksa apakah izin menulis berhasil diberikan:
```
ls -l /home/test   
# Di sini, /home/test menunjukkan direktori FTP. Ganti dengan direktori FTP aktual Anda.
``` 




