## Ikhtisar

Beberapa citra sistem Linux memiliki resolusi tampilan VNC yang lebih rendah secara default. Misalnya, resolusi VNC untuk CentOS hanya 720 \* 400. Anda dapat mengatur resolusi VNC ke 1024 \* 768 dengan memodifikasi parameter `grub`.
Jika citra sistem Windows memiliki resolusi VNC yang sangat rendah, beberapa aplikasi mungkin gagal ditampilkan atau dibuka dengan benar. Untuk menghindari masalah ini, modifikasi resolusi citra sistem Windows.

Dokumen ini menjelaskan cara menyesuaikan resolusi tampilan VNC dari CVM.

## Petunjuk

### Memodifikasi resolusi VNC dari instans CVM Windows

>? Langkah-langkah di bawah ini menjelaskan cara memodifikasi resolusi VNC instans Windows di sistem operasi Windows Server 2012.

1. [Login ke instans Windows melalui VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Klik kanan pada desktop dan pilih **Screen resolution** (Resolusi layar), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/b8ec8e8ec22002532a4a517150079d2d.png)
3. Di jendela “Screen Resolution” (Resolusi Layar), atur **Resolution** (Resolusi) ke nilai yang Anda inginkan dan klik **Apply** (Terapkan), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/b90a33fa0600846888a15154f1e656dc.png)
4. Di jendela pop-up, klik **Keep changes** (Simpan perubahan).
5. Klik **OK** (OKE) untuk menutup jendela “Screen Resolution” (Resolusi Layar).

### Memodifikasi resolusi VNC dari instans CVM Linux

Citra Linux yang lebih baru seperti CentOS 7, CentOS 8, Ubuntu, dan Debian 9.0 mengadopsi resolusi VNC default 1024 \* 768, yang dapat digunakan tanpa modifikasi apa pun. Panduan di bawah ini memperkenalkan cara memodifikasi resolusi VNC instans Linux pada sistem operasi CentOS 6 dan Debian 7.8.

#### CentOS 6

Citra CentOS 6 memiliki resolusi VNC 720 \* 400 secara default. Untuk mengatur resolusinya ke 1024 \* 768, modifikasi parameter peluncuran `grub` sebagai berikut:
- [Login ke Instans Linux Menggunakan Metode login Standar](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang lebih nyaman bagi Anda:
 - [Login ke Instans Linux melalui Alat Login Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32502).
 - [Login ke Instans Linux melalui Kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501)
 - [Login ke Instans Linux melalui VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Jalankan perintah berikut untuk membuka file `/etc/grub.conf`.
```
vi /etc/grub.conf
```
3. Tekan **i** (i) untuk beralih ke mode pengeditan, dan tambahkan `vga=792` ke parameter `grub`, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/3c2193fa370c48a7af149c63720da077.png)
4. Tekan **Esc** (Esc), masukkan **:wq** (:wq), lalu simpan dan tutup file.
5. Jalankan perintah berikut untuk melakukan boot ulang CVM.
```
melakukan boot ulang
```

#### Debian 7.8

Citra Debian 7.8 dan Debian 8.2 memiliki resolusi VNC 720 \* 400 secara default. Untuk mengatur resolusinya ke 1024 \* 768, modifikasi parameter peluncuran `grub` sebagai berikut:
- [Login ke Instans Linux Menggunakan Metode Login Standar](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang lebih nyaman bagi Anda:
 - [Login ke Instans Linux melalui Alat Login Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32502).
 - [Login ke Instans Linux melalui Kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501)
 - [Login ke Instans Linux melalui VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Jalankan perintah berikut untuk membuka file `grub`.
```
vi /etc/default/grub
```
3. Tekan **i** (i) untuk beralih ke mode pengeditan dan tambahkan `vga=792` di akhir nilai parameter `GRUB_CMDLINE_LINUX_DEFAULT`.
![](https://main.qcloudimg.com/raw/f8e275c35b65b7b2d26cfbd7a8ae4dd6.png)
4. Tekan **Esc** (Esc), masukkan **:wq** (:wq), lalu simpan dan tutup file.
5. Jalankan perintah berikut untuk memperbarui file `grub.cfg`.
```
grub-mkconfig -o /boot/grub/grub.cfg
```
6. Jalankan perintah berikut untuk melakukan boot ulang CVM.
```
melakukan boot ulang
```


## Lampiran

Tabel di bawah ini membandingkan resolusi instans Linux dan parameter VGA:
<table>
	<tr><th>Resolusi</th><td>640 * 480</td><td>800 * 600</td><td>1024 * 768</td></tr>
	<tr><th>VGA</th><td>786</td><td>789</td><td>792</td></tr>
</table>
