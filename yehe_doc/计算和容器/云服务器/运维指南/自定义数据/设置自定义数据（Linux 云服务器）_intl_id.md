## Skenario

Saat membuat CVM, Anda dapat mengonfigurasi instans dengan menentukan **custom data** (data kustom). Selama **first launch** (peluncuran pertama) CVM, data kustom akan diteruskan ke CVM dalam format teks dan dieksekusi. Jika Anda membeli beberapa CVM sekaligus, semua CVM akan menjalankan data kustom pada peluncuran pertamanya.
Artikel ini menjelaskan cara meneruskan skrip Shell saat meluncurkan CVM Linux untuk pertama kalinya.

## Catatan
- Sistem operasi Linux yang mendukung data kustom meliputi:
	- Sistem operasi 64-bit: CentOS 6.8 64-bit atau versi yang lebih baru, Ubuntu Server 14.04.1 LTS 64-bit atau versi yang lebih baru, dan suse42.3x86_64
	- Sistem operasi 32-bit: CentOS 6.8 32-bit atau versi yang lebih baru
- Suatu perintah dapat dijalankan dengan melanjutkan teks hanya ketika CVM diluncurkan untuk pertama kalinya.
- Data kustom harus dikodekan dengan Base64 dan kemudian diteruskan. **For a compatible format, encode the custom data in Linux environment.** (Untuk format yang kompatibel, kodekan data kustom di lingkungan Linux.)
- Jalankan data kustom sebagai `root`. Oleh karena itu, perintah `sudo` tidak diperlukan dalam skrip. Pengguna `root` dapat mengakses semua file yang Anda buat. Jika Anda perlu memberikan izin akses kepada pengguna lain, ubah izin dalam skrip.
- Selama peluncuran, menjalankan tugas data kustom akan meningkatkan waktu mulai CVM. Tunggu beberapa menit hingga tugas selesai, lalu uji apakah tugas telah berhasil dijalankan
* Dalam contoh ini, skrip Shell harus dimulai dengan `#!` dan jalur ke interpreter yang membaca skrip (biasanya `/bin/bash`).

## Petunjuk

### Menulis skrip Shell
1. Jalankan perintah berikut untuk membuat skrip Shell bernama “script_text.sh”.
```
vi script_text.sh
```
2. Tekan **i** (i) untuk beralih ke mode pengeditan, masukkan berikut ini dan simpan skrip “script_text.sh”.
```
#!/bin/bash
echo "Hello Tencent Cloud."
```
> Skrip shell harus dimulai dengan `#!` dan jalur ke interpreter yang membaca skrip (biasanya `/bin/bash`). Untuk informasi selengkapnya tentang skrip Shell, lihat Pemrograman BASH dari Proyek Dokumentasi Linux (tldp.org) (http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html).

<span id="Base64Script"></span>
### Mengodekan skrip dengan Base64

1. Jalankan perintah berikut untuk mengodekan skrip “script_text.sh” dengan Base64.
```
# Skrip yang dikodekan dengan Base64
base64 script_text.sh
```
Anda akan melihat informasi berikut:
```
# Hasil yang dikodekan
IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
```
2. Jalankan perintah berikut untuk memverifikasi hasil skrip yang dikodekan dengan Base64.
```
# Kodekan hasil yang ditampilkan dengan Base64 dan pastikan apakah berupa perintah yang akan dieksekusi.
echo "IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==" | base64 -d
```

### Meneruskan teks

Anda dapat meluncurkan instans melalui beberapa metode, dan di sini kami memperkenalkan dua di antaranya. Pilih metode sesuai kebutuhan Anda:
- [Menggunakan situs resmi atau konsol](#Consoletrans)
- [Menggunakan API](#APItrans)

<span id="Consoletrans"></span>
#### Menggunakan situs web resmi atau konsol

1. Lihat [Membuat Instans](https://intl.cloud.tencent.com/document/product/213/4855) untuk membeli instans, dan klik **Advanced Settings** (Pengaturan Lanjutan) di “4. Grup Keamanan dan CVM”, seperti yang ditunjukkan di bawah:
![](https://main.qcloudimg.com/raw/28baf2764488ecfaf5bbac791cec7ea3.png)
2. Di **Advanced Settings** (Pengaturan Lanjutan), masukkan hasil [skrip yang dikodekan dengan Base64](#Base64Script) yang ditampilkan dalam kotak teks Data Kustom, seperti yang ditunjukkan di bawah:
Misalnya, hasil yang dikodekan dengan Base64 dari skrip `script_text` adalah `IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==`.
![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
3. Buat instans CVM seperti yang diminta oleh halaman.
>Tencent Cloud CVM mengeksekusi skrip menggunakan cloud-init perangkat lunak sumber terbuka. Untuk informasi selengkapnya tentang cloud-init, lihat [situs web resmi cloud-init](https://cloud-init.io/).

<span id="APItrans"></span>
#### Menggunakan API

Saat membuat CVM menggunakan API, Anda dapat meneruskan teks dengan menetapkan nilai hasil yang dikodekan yang ditampilkan dalam [skrip yang dikodekan dengan Base64](#Base64Script) ke parameter UserData dari RunInstances API.
Berikut adalah contoh permintaan pembuatan CVM dengan UserData:
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
  &<Common request parameters>
```
