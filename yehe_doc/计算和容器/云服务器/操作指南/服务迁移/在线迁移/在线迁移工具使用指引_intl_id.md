## Ikhtisar
Migrasi online mengacu pada migrasi atau sinkronisasi sistem dan aplikasi pada server sumber atau mesin virtual dari IDC Anda atau platform cloud lainnya ke Tencent Cloud tanpa waktu henti sistem.
Tencent Cloud menyediakan alat migrasi [go2tencentcloud](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip). Setelah Anda menjalankan alat migrasi di server sumber, seluruh server sumber dapat dimigrasikan ke Tencent Cloud CVM tujuan. Dengan alat migrasi ini, Anda tidak perlu menyiapkan, mengunggah, atau mengimpor citra. Server sumber dimigrasikan secara langsung ke cloud, memenuhi persyaratan bisnis untuk cloudifikasi perusahaan, migrasi lintas-cloud, migrasi lintas-akun atau lintas-wilayah, dan deployment cloud hibrida.

## Alat Migrasi

### Mode migrasi yang didukung

<span id="DefaultMode"></span>
#### Mode default
Jika server sumber dan CVM tujuan Anda dapat mengakses jaringan publik, Anda dapat menggunakan mode migrasi default.
Dalam mode default saat ini, server sumber memanggil Tencent Cloud API melalui Internet untuk memulai permintaan migrasi, dan mentransfer data ke CVM tujuan untuk menyelesaikan migrasi.
![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)

#### Mode migrasi jaringan pribadi
Jika server sumber atau CVM tujuan Anda berada di jaringan pribadi atau Virtual Private Cloud (VPC), server sumber tidak dapat secara langsung membuat koneksi dengan CVM tujuan melalui Internet. Dalam hal ini, Anda dapat menggunakan mode migrasi jaringan pribadi dari alat tersebut. Anda perlu membuat koneksi antara server sumber dan CVM tujuan melalui [Koneksi Peering VPC](https://intl.cloud.tencent.com/document/product/553), [Koneksi VPN](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003), atau [Direct Connect](https://intl.cloud.tencent.com/document/product/216).

- <span id="Scenario1">Skenario 1</span>: jika server sumber atau CVM tujuan Anda tidak dapat mengakses jaringan publik, gunakan server (seperti gateway) yang dapat mengakses jaringan publik untuk memanggil Tencent Cloud API melalui Internet untuk memulai migrasi permintaan, lalu transfer data ke CVM tujuan melalui koneksi untuk menyelesaikan migrasi. Skenario ini tidak memerlukan server sumber maupun CVM tujuan untuk dapat mengakses jaringan publik.
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- <span id="Scenario2">Skenario 2</span>: jika server sumber Anda dapat mengakses jaringan publik, gunakan server sumber untuk memanggil Tencent Cloud API melalui Internet untuk memulai permintaan migrasi, lalu mentransfer data ke CVM tujuan melalui koneksi untuk menyelesaikan migrasi. Skenario ini memerlukan server sumber, tetapi bukan CVM tujuan, untuk dapat mengakses jaringan publik.
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- <span id="Scenario3">Skenario 3</span>: jika server sumber Anda dapat mengakses jaringan publik melalui proksi, gunakan server sumber untuk memanggil Tencent Cloud API melalui proksi jaringan untuk memulai permintaan migrasi, lalu mentransfer data ke CVM tujuan melalui koneksi untuk menyelesaikan migrasi. Skenario ini tidak memerlukan server sumber maupun CVM tujuan untuk dapat mengakses jaringan publik.
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)

### Sistem operasi yang didukung
Sistem operasi yang didukung oleh alat migrasi online termasuk namun tidak terbatas pada hal berikut (32-bit atau 64-bit):
<table>
	<tr><th>Linux</th><th>Windows</th></tr>
	<tr><td>CentOS 5/6/7/8</td><td rowspan=7>-</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18</td></tr>
	<tr><td>Debian 7/8/9</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 7/8</td></tr>
</table>

### File dalam paket terkompresi

<table>
	<tr><th>Nama File</th><th>Deskripsi</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>Program yang dapat dijalankan dari alat migrasi untuk sistem operasi Linux 64-bit</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>Program yang dapat dijalankan dari alat migrasi untuk sistem operasi Linux 32-bit</td></tr>
	<tr><td>user.json</td><td>File konfigurasi server sumber dan CVM tujuan selama migrasi. Anda perlu mengubah konfigurasi berdasarkan <a href="#userJsonState">deskripsi parameter di file user.json</a>.</td></tr>
	<tr><td>client.json</td><td>File konfigurasi alat migrasi. Anda perlu mengubah konfigurasi berdasarkan <a href="#clientJsonState">deskripsi parameter di file client.json</a>.</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>file konfigurasi rsync, yang mengecualikan file dan direktori yang tidak perlu dimigrasikan di sistem Linux.</td></tr>
</table>

>? File konfigurasi tidak dapat dihapus. Anda harus menyimpannya di folder yang sama dengan program yang dapat dijalankan go2tencentcloud. 
>

- <span id="userJsonState">Deskripsi parameter dalam file user.json:</span>
<table>
	<tr><th>Parameter</th><th>Jenis</th><th>Diperlukan</th><th>Deskripsi</th></tr>
	<tr><td>SecretId</td><td>String</td><td>Ya</td><td>ID Rahasia akun Anda untuk mengakses API. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/598/32675">Kunci Akses</a>.</td></tr>
	<tr><td>SecretKey</td><td>String</td><td>Ya</td><td>Kunci rahasia akun Anda untuk mengakses API. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/598/32675">Kunci Akses</a>.</td></tr>
	<tr><td>Wilayah</td><td>String</td><td>Ya</td><td>Wilayah CVM tujuan. Anda hanya perlu menentukan wilayah, bukan zona ketersediaan. Untuk informasi selengkapnya tentang nilai, lihat <a href="https://intl.cloud.tencent.com/document/product/213/6091">daftar wilayah</a>.</td></tr>
	<tr><td>InstanceId</td><td>String</td><td>Ya</td><td>ID Instans CVM tujuan. Format ID adalah <code>ins-xxxxxxxx</code>.</td></tr>
	<tr><td>DataDisks</td><td>Array</td><td>Tidak</td><td>Daftar disk data yang akan dimigrasikan dari server sumber. Setiap entri mewakili satu disk data, dan didukung hingga 20 disk data.</td></tr>
	<tr><td>DataDisks.Index</td><td>Bilangan Bulat</td><td>Tidak</td><td>Nomor seri disk data. Rentang nilai: [1,20]. Nilai <code>1</code> menunjukkan bahwa disk data ini akan dimigrasikan ke disk data pertama yang dipasang pada CVM tujuan. Demikian pula, nilai <code>2</code> menunjukkan bahwa disk data ini akan dimigrasikan ke disk data kedua yang dipasang pada CVM tujuan.</td></tr>
	<tr><td>DataDisks.Size</td><td>Bilangan Bulat</td><td>Tidak</td><td>Ukuran disk data di server sumber. Unit: GB. Rentang nilai: [10,16000].</td></tr>
	<tr><td>DataDisks.MountPoint</td><td>String</td><td>Tidak</td><td>Titik pemasangan disk data di server sumber, misalnya, <code>"/mnt/ disk1"</code>.</td></tr>
</table>
Contoh 1: untuk memigrasi server sumber Linux ke CVM yang berlokasi di Guangzhou, konfigurasikan file user.json sebagai berikut:

 ```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
}  
```
>? Anda perlu mengganti nilai parameter dengan nilai aktual.
>
Misalnya, server sumber Linux memiliki satu disk data, titik pemasangannya adalah `/mnt/disk1`, dan ukuran disk datanya adalah `10` GB. Untuk memigrasi server ini ke CVM (dengan setidaknya satu disk data terpasang) yang berada di wilayah Guangzhou, konfigurasikan file user.json sebagai berikut:
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		}
	]
}  
```
Misalnya, server sumber Linux memiliki dua disk data. Titik pemasangan untuk disk 1 adalah `/mnt/disk1`, dan ukurannya adalah `10` GB. Titik pemasangan untuk disk 2 adalah `/mnt/disk2`, dan ukurannya adalah `20` GB. Untuk memigrasi server ini ke CVM (dengan setidaknya dua disk data terpasang) yang berada di Guangzhou, dengan disk 1 dan disk 2 dari server sumber yang akan dimigrasikan ke disk data pertama dan kedua dari CVM tujuan, konfigurasikan file user.json sebagai berikut:
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		},
		{
			"Index": 2,
			"Size": 20,
			"MountPoint": "/mnt/disk2"
		}
	]
}  
```
>? Anda perlu mengganti nilai parameter dengan nilai aktual.
>
- <span id="clientJsonState">Deskripsi parameter dalam file client.json:</span>
<table>
	<tr><th>Parameter</th><th>Jenis</th><th>Diperlukan</th><th>Deskripsi</th></tr>
	<tr><td>Client.Net.Mode</td><td>Bilangan Bulat</td><td>Ya</td><td>Nilai default: <code>0</code>. Nilai yang valid:<code>0</code> (<a href="#DefaultMode">mode default)</a>), <code>1</code> (<a href="#Scenario1">mode migrasi jaringan pribadi: skenario 1</a>), <code>2</code> (<a href="#Scenario2">mode migrasi jaringan pribadi: skenario 2</a>), <code>3</code> (<a href="#Scenario3">mode migrasi jaringan pribadi: skenario 3</a>). Masukkan nilai berdasarkan mode atau skenario migrasi Anda secara aktual.</td></tr>
	<tr><td>Client.Net.Proxy.Ip</td><td>String</td><td>Tidak</td><td>Alamat IP proksi jaringan. Jika Anda memilih <a href="#Scenario3">mode migrasi jaringan pribadi: skenario 3</a>, parameter ini harus ditentukan.</td></tr>
	<tr><td>Client.Net.Proxy.Port</td><td>Bilangan Bulat</td><td>Tidak</td><td>Port proksi jaringan. Jika Anda memilih <a href="#Scenario3">mode migrasi jaringan pribadi: skenario 3</a>, parameter ini harus ditentukan.</td></tr>
	<tr><td>Client.Net.Proxy.User</td><td>String</td><td>Tidak</td><td>Nama pengguna proksi jaringan. Jika Anda memilih <a href="#Scenario3">mode migrasi jaringan pribadi: skenario 3</a>, dan proksi jaringan perlu diautentikasi, parameter ini harus ditentukan.</td></tr>
	<tr><td>Client.Net.Proxy.Password</td><td>String</td><td>Tidak</td><td>Kata sandi proksi jaringan. Jika Anda memilih <a href="#Scenario3">mode migrasi jaringan pribadi: skenario 3</a>, dan proksi jaringan perlu diautentikasi, parameter ini harus ditentukan.</td></tr>
	<tr><td>Client.Extra.IgnoreCheck</td><td>Bool</td><td>Tidak</td><td>Nilai default: <code>false</code>. Saat diluncurkan, alat migrasi secara otomatis memeriksa lingkungan server sumber. Untuk melewati pemeriksaan ini, konfigurasikan parameter ini ke <code>true</code>.</td></tr>
	<tr><td>Client.Rsync.BandwidthLimit</td><td>String</td><td>Tidak</td><td>Batas bandwidth dalam KByte/dtk. Nilai defaultnya kosong, artinya tidak ada batasan bandwidth selama transfer.</td></tr>
	<tr><td>Client.Rsync.Checksum</td><td>Bool</td><td>Tidak</td><td>Transfer checksum. Jika parameter ini dikonfigurasikan ke <code>true</code>, parameter ini dapat memperkuat pemeriksaan konsistensi transfer, tetapi akan menambah beban CPU dari server sumber dan memperlambat kecepatan transfer. Nilai defaultnya adalah <code>false</code>, artinya tidak ada pemeriksaan yang dilakukan secara default.</td></tr>
</table>
<blockquote class="doc-tip"><p class="doc-tip-tit"><i class="doc-icon-tip"></i>Catatan: </p><p>Kecuali parameter di atas, item konfigurasi lain di file client.json biasanya tidak perlu ditentukan.</p>
</blockquote>
- <span id="_linuxTxtState">Deskripsi file rsync\_excludes\_linux.txt:</span>
File ini digunakan untuk mengecualikan file di server sumber Linux atau file konfigurasi di bawah direktori tertentu yang tidak perlu dimigrasikan. Secara default, file rsync\_excludes\_linux.txt sudah mengecualikan direktori dan file berikut. **Do not delete or modify the EXISTING configurations.** (Jangan hapus atau modifikasi konfigurasi yang ADA.)
```sh
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
```
Untuk mengecualikan direktori atau file lain, tambahkan ke file rsync\_excludes\_linux.txt. Misalnya, untuk mengecualikan semua konten disk data yang dipasang pada `/mnt/disk1`, konfigurasikan file rsync\_excludes\_linux.txt sebagai berikut:
```sh
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
/mnt/disk1/*
```

### Parameter alat migrasi
Parameter | Deskripsi
---|---
`--help` | Mencetak informasi bantuan.
`--check` | Memeriksa server sumber tanpa migrasi.
`--log-file`| Mengonfigurasi nama file log, yaitu `log` secara default.
`--log-level`| Mengonfigurasi level logging. Nilai yang valid: `1` (tingkat KESALAHAN), `2` (tingkat INFO), dan `3` (tingkat DEBUG). Nilai default: `2`.
`--clean` | Memungkinkan CVM tujuan keluar secara paksa dari mode migrasi dan membersihkan situs. Misalnya, jika konsol meminta `Harap jalankan opsi '--clean' secara manual.`, Anda perlu menentukan parameter ini dan menjalankan alat untuk CVM tujuan untuk keluar dari mode migrasi.
`--version` | Mencetak nomor versi.

## Memeriksa sebelum migrasi
Sebelum migrasi, periksa item berikut dari server sumber dan CVM tujuan:
<table>
	<tr><th style="width: 15%;">CVM Tujuan</th><td><ol  style="margin: 0;"><li>Penyimpanan: disk cloud (termasuk disk sistem dan disk data) dari CVM tujuan harus memiliki kapasitas penyimpanan yang cukup untuk menyimpan data dari server sumber.</li><li>Grup keamanan: Port 443 dan 80 harus terbuka ke Internet dalam grup keamanan.</li><li>Bandwidth: sebaiknya Anda meningkatkan bandwidth masuk dan keluar untuk migrasi yang lebih cepat. Lalu lintas yang terpakai selama migrasi kira-kira sama dengan volume data. Jika perlu, ubah metode penagihan jaringan Anda terlebih dahulu.</li><li>Sistem operasi: sebaiknya gunakan sistem operasi yang sama pada server sumber dan CVM tujuan. Sistem operasi yang berbeda akan mengakibatkan inkonsistensi antara citra yang akan dibuat dan sistem operasi aktual. Misalnya, saat memigrasi server sumber dengan sistem CentOS 7 yang diinstal, pilih CVM dengan sistem CentOS 7 yang diinstal sebagai tujuan migrasi.</li></ol></td></tr>
	<tr><th>Server sumber Linux</th><td><ol  style="margin: 0;"><li>Periksa dan instal Virtio. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/9929">Memeriksa Driver Virtio di Linux</a>.</li><li>Periksa apakah rsync diinstal dengan menjalankan <code>rsync</code> untuk verifikasi.</li><li>Periksa apakah SELinux sudah diaktifkan. Nonaktifkan jika statusnya diaktifkan.</li><li>Pastikan waktu sistem saat ini sudah benar, karena Tencent Cloud API akan menggunakan stempel waktu UNIX untuk memeriksa token yang dihasilkan setelah menerima permintaan migrasi.</li></ol></td> </tr>
</table>

>? 
> - Anda dapat menggunakan perintah alat seperti `sudo ./go2tencentcloud_x64 --check` untuk memeriksa server sumber secara otomatis.
> - Secara default, alat migrasi go2tencentcloud secara otomatis melakukan pemeriksaan saat diluncurkan. Untuk melewati pemeriksaan dan melakukan migrasi paksa, konfigurasikan `Client.Extra.IgnoreCheck` ke `true` di file client.json.
> 

## Petunjuk Migrasi
Jika Anda menggunakan go2tencentcloud yang disediakan oleh Tencent Cloud untuk migrasi, proses migrasi mencakup tiga tahap berikut. Anda dapat secara intuitif melihat kemajuan migrasi saat alat ini berjalan.
- **Stage 1** (Tahap 1): CVM tujuan memasuki mode migrasi, dan siap melakukan migrasi
- **Stage 2** (Tahap 2): CVM tujuan berada dalam mode migrasi, dan menerima data yang dimigrasi
- **Stage 3** (Tahap 3): CVM tujuan keluar dari mode migrasi, dan migrasi selesai

Setiap tahap akan menghasilkan beberapa subtugas untuk melakukan operasi terkait, dan beberapa subtugas yang memakan waktu mungkin memiliki periode waktu habis maksimum secara default. Waktu yang diperlukan untuk transfer data tergantung pada ukuran data di server sumber, bandwidth jaringan, dll. Harap tunggu hingga proses migrasi selesai. Alat migrasi mendukung mulai ulang checkpoint.

>! CVM tujuan memasuki mode migrasi setelah migrasi dimulai. Jangan menginstal ulang sistem, mematikan, menghentikan, atau mengatur ulang kata sandi CVM tujuan hingga migrasi selesai dan CVM tujuan keluar dari mode migrasi. 
>

### Petunjuk migrasi dalam mode default

1. Di file user.json, konfigurasikan CVM tujuan untuk migrasi.
Konfigurasikan parameter yang diperlukan berdasarkan [deskripsi parameter di file user.json](#userJsonState).
2. Di file client.json, konfigurasikan mode migrasi dan parameter lainnya.
Konfigurasikan `Client.Net.Mode` di file client.json ke `0`, yaitu, pilih [mode default](#DefaultMode). Jika perlu, konfigurasikan parameter lain berdasarkan [deskripsi parameter di file client.json](#clientJsonState).
3. (Opsional) Kecualikan file dan direktori di server sumber yang tidak perlu dimigrasikan.
Jika Anda ingin mengecualikan beberapa file dan direktori yang tidak perlu dimigrasikan saat memigrasi server sumber Linux, tambahkan file dan direktori tersebut ke [file rsync\_excludes\_linux.txt](#_linuxTxtState).
4. Jalankan alat.
Misalnya, pada server sumber Linux 64-bit, jalankan perintah berikut sebagai pengguna root untuk menjalankan alat.
```
sudo ./go2tencentcloud_x64
```
Untuk mengonfigurasi nama file log dan level logging saat menjalankan alat, jalankan perintah berikut:
```
sudo ./go2tencentcloud --log-file=my.log --log-level=3
```
Harap tunggu hingga proses migrasi selesai. 
Jika migrasi dalam mode default berhasil, output konsol adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)

### Petunjuk migrasi dalam mode migrasi jaringan pribadi

#### Skenario 1
1. Buat koneksi antara server sumber dan CVM tujuan.
Buat koneksi antara server sumber dan CVM tujuan dengan menggunakan [koneksi peering VPC](https://intl.cloud.tencent.com/document/product/553), [koneksi VPN](https://intl.cloud.tencent.com/document/product/1037), atau [CCN](https://intl.cloud.tencent.com/document/product/1003).
2. Di file user.json, konfigurasikan CVM tujuan untuk migrasi.
 Konfigurasikan parameter yang diperlukan berdasarkan [deskripsi parameter di file user.json](#userJsonState).
3. Di file client.json, konfigurasikan mode migrasi dan parameter lainnya.
Konfigurasikan `Client.Net.Mode` di file client.json ke `1`, yaitu, pilih [mode migrasi jaringan pribadi: skenario 1](#Skenario1). Jika perlu, konfigurasikan parameter lain berdasarkan [deskripsi parameter di file client.json](#clientJsonState).
4. (Opsional) Kecualikan file dan direktori di server sumber yang tidak perlu dimigrasikan.
Jika Anda ingin mengecualikan beberapa file dan direktori yang tidak perlu dimigrasikan saat memigrasi server sumber Linux, tambahkan file dan direktori tersebut ke [file rsync_excludes_linux.txt](#_linuxTxtState).
5. <span id="Scenario1_step05">Jalankan alat di server (seperti gateway) yang dapat mengakses jaringan publik.</span>
Misalnya, pada server yang dapat mengakses jaringan publik, jalankan perintah berikut untuk menjalankan alat untuk migrasi tahap 1.
```
sudo ./go2tencentcloud_x64
```
Jika `Tahap 1 selesai dan harap jalankan tahap selanjutnya di mesin sumber` diminta, artinya tahap 1 selesai.
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)
6. <span id="Scenario1_step06">Jalankan alat di server sumber.</span>
Setelah [langkah 5](#Scenario1_step05) (tahap 1) selesai, salin seluruh direktori alat di tahap 1 ke server sumber, lalu jalankan alat untuk migrasi tahap 2.
Jalankan perintah berikut untuk menjalankan alat untuk migrasi tahap 2.
```
sudo ./go2tencentcloud_x64
```
Jika `Tahap 2 selesai dan harap jalankan tahap selanjutnya di mesin gateway` diminta, artinya tahap 2 selesai.
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
7. Jalankan alat di server (seperti gateway) yang dapat mengakses jaringan publik.
Setelah [langkah 6](#Scenario1_step06) (tahap 2) selesai, salin seluruh direktori alat di tahap 2 ke server di tahap 1, lalu jalankan alat untuk migrasi tahap 3.
Jalankan perintah berikut untuk menjalankan alat untuk migrasi tahap 3.
```
sudo ./go2tencentcloud_x64
```
Jika `Migrasi berhasil` diminta, seluruh tugas migrasi telah selesai.
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)
   
#### Skenario 2

1. Buat koneksi antara server sumber dan CVM tujuan.
Buat koneksi antara server sumber dan CVM tujuan dengan menggunakan [koneksi peering VPC](https://intl.cloud.tencent.com/document/product/553), [koneksi VPN](https://intl.cloud.tencent.com/document/product/1037), atau [CCN](https://intl.cloud.tencent.com/document/product/1003).
2. Di file user.json, konfigurasikan CVM tujuan untuk migrasi.
 Konfigurasikan parameter yang diperlukan berdasarkan [deskripsi parameter di file user.json](#userJsonState).
3. Di file client.json, konfigurasikan mode migrasi dan parameter lainnya.
 Konfigurasikan `Client.Net.Mode` di file client.json ke `2`, yaitu, pilih [mode migrasi jaringan pribadi: skenario 2](#Skenario2). Jika perlu, konfigurasikan parameter lain berdasarkan [deskripsi parameter di file client.json](#clientJsonState).
4. (Opsional) Kecualikan file dan direktori di server sumber yang tidak perlu dimigrasikan.
Jika Anda ingin mengecualikan beberapa file dan direktori yang tidak perlu dimigrasikan saat memigrasi server sumber Linux, tambahkan file dan direktori tersebut ke [file rsync_excludes_linux.txt](#_linuxTxtState).
5. Jalankan alat.
Misalnya, pada server sumber Linux 64-bit, jalankan perintah berikut sebagai `root` untuk menjalankan alat.
```
sudo ./go2tencentcloud_x64
```
Harap tunggu hingga proses migrasi selesai.
Jika hal berikut ini muncul di konsol, artinya migrasi telah berhasil diselesaikan.
![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png)
  
#### Skenario 3

1. Buat koneksi antara server sumber dan CVM tujuan.
 Buat koneksi antara server sumber dan CVM tujuan dengan menggunakan [koneksi peering VPC](https://intl.cloud.tencent.com/document/product/553), [koneksi VPN](https://intl.cloud.tencent.com/document/product/1037), atau [CCN](https://intl.cloud.tencent.com/document/product/1003).
2. Di file user.json, konfigurasikan CVM tujuan untuk migrasi.
Konfigurasikan parameter yang diperlukan berdasarkan [deskripsi parameter di file user.json](#userJsonState).
3. Di file client.json, konfigurasikan mode migrasi dan parameter lainnya.
 1. Konfigurasikan `Client.Net.Mode` di file client.json ke `3`, yaitu, pilih [mode migrasi jaringan pribadi: skenario 3](#Scenario3).
 2. Konfigurasikan `Client.Net.Proxy.Ip` dan `Client.Net.Proxy.Port` di file client.json ke alamat IP dan port proksi jaringan.
Jika proksi jaringan Anda perlu diautentikasi, konfigurasikan `Client.Net.Proxy.User` dan `Client.Net.Proxy.Password` ke nama pengguna dan kata sandi proksi jaringan. Anda dapat membiarkannya kosong jika autentikasi tidak diperlukan. Jika perlu, Anda dapat mengonfigurasi parameter lain berdasarkan [deskripsi parameter di file client.json](#clientJsonState).
4. (Opsional) Kecualikan file dan direktori di server sumber yang tidak perlu dimigrasikan.
Jika Anda ingin mengecualikan beberapa file dan direktori yang tidak perlu dimigrasikan saat memigrasi server sumber Linux, tambahkan file dan direktori tersebut ke [file rsync_excludes_linux.txt](#_linuxTxtState).
5. Jalankan alat.
Misalnya, pada server sumber Linux 64-bit, jalankan perintah berikut sebagai `root` untuk menjalankan alat.
```
sudo ./go2tencentcloud_x64
```
Harap tunggu hingga proses migrasi selesai.
Jika hal berikut ini muncul di konsol, artinya migrasi telah berhasil diselesaikan.
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)

## Memeriksa setelah migrasi
1. Jika migrasi gagal, periksa informasi kesalahan dalam file log (di bawah direktori alat migrasi secara default), panduan operasi, atau [Tentang Migrasi Layanan](https://intl.cloud.tencent.com/document/product/213/32395) untuk metode pemecahan masalah.
2. Jika migrasi berhasil, periksa apakah CVM tujuan dapat dimulai secara normal, apakah data di CVM tujuan konsisten dengan data di server sumber, apakah jaringannya normal, dan apakah layanan sistem lainnya berjalan normal.
3. Jika Anda memiliki pertanyaan atau migrasi memiliki pengecualian, lihat [Tentang Migrasi Layanan](https://intl.cloud.tencent.com/document/product/213/32395) atau [hubungi kami](https://intl.cloud.tencent.com/support).

