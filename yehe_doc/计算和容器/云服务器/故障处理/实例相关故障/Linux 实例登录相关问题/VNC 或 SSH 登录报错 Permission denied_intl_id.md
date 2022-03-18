## Deskripsi Kesalahan
Pesan kesalahan “Permission denied” (Izin ditolak) dilaporkan ketika saya login menggunakan kunci VNC atau SSH.
- Kesalahan login VNC ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/5f1aedd75b6d99cddab4d83fa82d964f.png)
- Kesalahan login SSH ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/7ab31fbb82391da2c8ae28e8ad3b961f.png)

## Kemungkinan Alasan
Menggunakan login VNC atau SSH akan memanggil `system-auth` untuk autentikasi jika modul ini dikonfigurasi dalam file konfigurasi `/etc/pam.d/login`. Secara default, modul `system-auth` memperkenalkan modul `pam_limits.so`. Konfigurasi `system-auth` default adalah seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/e32db00ec665388bc4c7cb0454fd6fab.png)
Modul `pam_limits.so` terutama digunakan untuk membatasi penggunaan sumber daya sistem selama sesi pengguna. File konfigurasi default `/etc/security/limits.conf` menentukan jumlah maksimum file, jumlah maksimum utas, memori maksimum, dan sumber daya lain yang dapat digunakan pengguna. Lihat tabel di bawah untuk detailnya.
<table>
<tr>
<th style="width:20%">Parameter</th><th>Deskripsi</th>
</tr>
<tr>
<td><code>soft nofile</code></td>
<td>Jumlah maksimum deskriptor file terbuka (batas lunak)</td>
</tr>
<tr>
<td><code> hard nofile</code></td>
<td>Jumlah maksimum deskriptor file terbuka (batas keras), yang tidak dapat dilampaui.</td>
</tr>
<tr>
<td><code>fs.file-max </code></td>
<td>Jumlah maksimum pegangan file terbuka (file struct di kernel) di tingkat sistem.</td>
</tr>
<tr>
<td><code>fs.nr_open</code></td>
<td>Jumlah maksimum deskriptor file (fd) yang ditetapkan untuk suatu proses</td>
</tr>
</table> 

Kegagalan login mungkin disebabkan oleh konfigurasi yang salah dari jumlah maksimum deskriptor file terbuka untuk akun root dalam file konfigurasi `/etc/security/limits.conf`. Nilai set `soft nofile` tidak boleh lebih dari `hard nofile`, dan `hard nofile` tidak boleh lebih dari `fs.nr_open`.


## Solusi
Lakukan [prosedur pemecahan masalah](#ProcessingSteps) untuk memperbaiki konfigurasi hubungan `soft nofile`, `hard nofile` dan `fs.nr_open`.

[](id:ProcessingSteps)

## Prosedur Pemecahan Masalah

1. Coba [login ke CVM Linux melalui kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501).
	- Jika login berhasil, lanjutkan ke langkah berikutnya.
	- Jika login gagal, gunakan mode pengguna tunggal. Untuk informasi selengkapnya, lihat [Melakukan booting ke Mode Pengguna Tunggal Linux](https://intl.cloud.tencent.com/document/product/213/34819).
2. Periksa apakah nilai yang ditetapkan memenuhi hubungan `soft nofile hard nofile fs.nr_open`.
 - Jalankan perintah berikut untuk mendapatkan nilai `soft nofile` dan `hard nofile`.
```
/etc/security/limits.conf
```
Dalam contoh ini, nilainya masing-masing adalah 3000001 dan 3000002, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/3bc035efb6cf46f70b30017dbefe831a.png)
 - Jalankan perintah berikut untuk memeriksa nilai `fs.nr_open`.
```
sysctl -a 2>/dev/null | grep -Ei "file-max|nr_open"
```
Dalam contoh ini, nilainya adalah 1048576, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/0fee5e2cda62d6a558cf808652a6b9dd.png)
3. Edit file `/etc/security/limits.conf` untuk menambah atau memodifikasi konfigurasi berikut di akhir file. 
 - `root soft nofile`: 100001
 - `root hard nofile`: 100002
4. Edit file `/etc/sysctl.conf` untuk menambah atau memodifikasi konfigurasi berikut di akhir file.
>?Langkah ini opsional bila hubungan `soft nofile hard nofile fs.nr_open` terpenuhi. Lakukan langkah ini untuk meningkatkan batas sistem.
>
 - `fs.file-max` = 2000000
 - `fs.nr_open` = 2000000
5. Jalankan perintah berikut agar konfigurasi segera berlaku. Kemudian Anda dapat login secara normal.
```
sysctl -p
```

