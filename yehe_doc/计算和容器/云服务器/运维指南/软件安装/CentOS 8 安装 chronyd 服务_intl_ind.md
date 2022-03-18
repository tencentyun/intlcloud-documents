## Ikhtisar
Saat ini, CentOS 8 native tidak mendukung pengaturan layanan NTP. Sebagai gantinya, Anda perlu menggunakan chronyd untuk memberikan waktu yang akurat. Dokumen ini menjelaskan cara menginstal dan mengonfigurasi chronyd pada instans Tencent Cloud CVM berbasis CentOS 8.

## Petunjuk
### Menginstal dan mengonfigurasi layanan chronyd
1. [Login ke instans Linux menggunakan metode login standar](https://intl.cloud.tencent.com/document/product/213/5436).
2. Jalankan perintah berikut untuk menginstal layanan chronyd.
```
yum -y install chrony
```
3. Jalankan perintah berikut untuk memodifikasi file konfigurasi `chrony.conf`.
```
vim /etc/chrony.conf
```
4. Tekan **i** (i) untuk masuk ke mode edit, dan tambahkan konten berikut ke baris berikutnya dari `#log measurements statistics tracking`.
```
server time1.tencentyun.com iburst
server time2.tencentyun.com iburst
server time3.tencentyun.com iburst
server time4.tencentyun.com iburst
server time5.tencentyun.com iburst
```
Hasilnya harus sebagai berikut:
![](https://main.qcloudimg.com/raw/578e072599f8d50ea188d3911a9d76c7.png)
5. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.
6. Jalankan perintah berikut secara berurutan untuk mengaktifkan dan memulai ulang chronyd autostart.
```
systemctl restart chronyd
```
```
systemctl enable chronyd
```

### Memverifikasi konfigurasi
1. Jalankan perintah berikut untuk memeriksa apakah jam disinkronkan.
```
tanggal
```
2. Jalankan perintah berikut untuk memeriksa status sumber jam.
```
chronyc sourcestats -v
```
Jika ditampilkan hasil yang mirip dengan berikut, artinya konfigurasi berhasil.
![](https://main.qcloudimg.com/raw/6a5f584638de922f5e80b5b138541c9e.png)

## Lampiran
### Perintah
<table>
<tr>
<th>Perintah</th><th>Deskripsi</th>
</tr>
<tr>
<td>
<code>chronyc sources -v</code>
</td>
<td>Periksa sumber jam.</td>
</tr>
<tr>
<td>
<code>chronyc sourcestats -v</code>
</td>
<td>Periksa status sumber jam.</td>
</tr>
<tr>
<td>
<code>timedatectl set-local-rtc 1</code>
</td>
<td>Atur jam real-time. Format default-nya adalah UTC.
</td>
</tr>
<tr>
<td>
<code>timedatectl set-ntp yes</code>
</td>
<td>Aktifkan layanan NTP untuk sinkronisasi.</td>
</tr>
<tr>
<td>
<code>chronyc tracking</code>
</td>
<td>Kalibrasi server NTP.</td>
</tr>
<tr>
<td>
<code>chronyc -a makestep</code>
</td>
<td>Paksa sinkronisasi jam sistem.</td>
</tr>
</table>
