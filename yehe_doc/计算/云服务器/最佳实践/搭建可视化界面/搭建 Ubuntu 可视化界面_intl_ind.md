## Ikhtisar
Virtual Network Console (VNC) adalah perangkat lunak fitur kendali jarak jauh yang dikembangkan oleh AT&T European Research Laboratory. Sebuah perangkat lunak sumber terbuka berdasarkan sistem operasi UNIX dan Linux, VNC memiliki kemampuan kendali jarah jauh yang andal, efisiensi tinggi, dan kepraktisan yang kuat. Performanya sebanding dengan perangkat lunak kendali jarak jauh apa pun di Windows atau Mac. Dokumen ini akan memandu Anda tentang cara membangun desktop visual Ubuntu menggunakan VNC.

## Prasyarat
Anda telah membeli CVM Linux dengan OS Ubuntu. Jika tidak, lihat [Menyesuaikan Konfigurasi CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517).


## Petunjuk

1. [Login ke instans Linux menggunakan VNC](https://intl.cloud.tencent.com/document/product/213/5436).
2. Jalankan perintah berikut untuk beralih ke akun “root”.
```
sudo su root
```
3. Jalankan perintah berikut untuk mendapatkan dan memperbarui ke versi terbaru.
```
apt-get update
```
4. Pilih dan jalankan perintah di bawah ini sesuai dengan versi sistem Anda untuk menginstal VNC.
<dx-tabs>
::: Ubuntu 16.04/18.04
```
apt-get install vnc4server
```
:::
::: Ubuntu 20.04
```
apt-get install tightvncserver
```
:::
</dx-tabs>
5. <span id="step05"></span>Jalankan perintah berikut untuk meluncurkan VNC dan mengatur kata sandi.
```
vncserver
```
Jika hasil yang ditampilkan mirip dengan berikut ini, ini menunjukkan bahwa VNC telah berhasil diluncurkan.
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
6. Jalankan perintah berikut untuk menginstal paket dasar X-windows.
```
sudo apt-get install x-window-system-core
```
7. Jalankan perintah khusus sistem berikut untuk menginstal manajer login.
<dx-tabs>
::: Ubuntu 16.04/18.04
```
sudo apt-get install gdm
```
:::
::: Ubuntu 20.04
```
sudo apt-get install gdm3
```
:::
</dx-tabs>
8. Jalankan perintah berikut untuk menginstal desktop Ubuntu.
```
sudo apt-get install ubuntu-desktop
```
Selama penginstalan, pilih “gdm3” untuk `Default display manager:`.
9. Jalankan perintah berikut untuk menginstal perangkat lunak pendukung GNOME.
```
sudo apt-get install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
```
10. Jalankan perintah berikut untuk mengakses file konfigurasi VNC.
```
vi ~/.vnc/xstartup
```
11. Tekan **i** (i) untuk masuk ke mode edit, dan ubah file konfigurasi sebagai berikut.
```
#!/bin/sh
# Batalkan komentar pada dua baris berikut untuk desktop normal:
export XKL_XMODMAP_DISABLE=1
 unset SESSION_MANAGER
# exec /etc/X11/xinit/xinitrc
unset DBUS_SESSION_BUS_ADDRESS
gnome-panel &
gnome-settings-daemon &
metacity &
nautilus &
gnome-terminal &
```
12. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.
13. Jalankan perintah berikut untuk memulai ulang proses desktop.
```
vncserver -kill :1 # Masukkan perintah untuk menghentikan proses desktop asli (di mana :1 adalah nomor desktop)
```
```
vncserver :1 # Buat sesi baru
```
14. [Klik di sini](https://www.realvnc.com/en/connect/download/viewer/) untuk mengunduh dan menginstal VNC Viewer. Pilih versi yang cocok dengan sistem operasi Anda.
15. Ketik `CVM IP address: 1` ke dalam VNC Viewer, dan tekan **Enter** (Enter).
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
16. Klik **Continue** (Lanjutkan) di kotak dialog pop-out.
17. Masukkan kata sandi VNC yang ditetapkan di [Langkah 5](#step05) dan klik **OK** (Oke).
>? Jika waktu koneksi habis, periksa koneksi jaringan dan konfigurasi grup keamanan. Buat aturan masuk `TCP:5901` untuk grup keamanan untuk membuka port mendengarkan 5901 dari VNC Server. Untuk petunjuk terperinci, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).









