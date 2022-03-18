## Pengantar

Mesin x86 menggunakan dua metode manajemen daya, **APM** (APM) (Advanced Power Management) dan **ACPI** (ACPI) (Advanced Configuration and Power Interface). ACPI adalah standar manajemen daya yang dikembangkan bersama oleh Intel, Microsoft, dan Toshiba, yang menyediakan antarmuka yang lebih fleksibel untuk manajemen komputer dan perangkat, sedangkan APM adalah standar manajemen daya lama.
Linux mendukung APM dan ACPI, tetapi kedua standar tersebut tidak dapat berjalan secara bersamaan. Linux menjalankan ACPI secara default. Tencent Cloud juga merekomendasikan ACPI. 
Jika ACPI tidak diinstal di sistem Linux, soft shutdown akan gagal. Dokumen ini menjelaskan cara memeriksa apakah ACPI telah diinstal dan cara menginstalnya jika belum melakukannya.

## Catatan

Untuk CoreOS, tidak perlu menginstal ACPI.

## Petunjuk
 
1. Jalankan perintah berikut untuk melihat apakah ACPI telah diinstal.
```
ps -ef|grep -w "acpid"|grep -v "grep"
```
 - Jika tidak ada proses yang berjalan, berarti ACPI belum diinstal. Harap lanjutkan ke langkah berikutnya.
 - Jika ada proses yang berjalan, berarti ACPI sudah terinstal.
2. Jalankan perintah berikut untuk menginstal ACPI.
 - Untuk Ubuntu atau Debian:
```
sudo apt-get install acpid
```
 - Untuk Redhat atau CentOS:
```
yum install acpid
```
 - Untuk SUSE:
```
in apcid
```
