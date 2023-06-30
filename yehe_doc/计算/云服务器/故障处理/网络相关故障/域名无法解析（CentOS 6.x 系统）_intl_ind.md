## Deskripsi Masalah
Setelah CVM dengan sistem operasi CentOS 6.x dimulai ulang atau dijalankan pada perintah `service network restart`, nama domainnya tidak dapat terselesaikan. Selain itu, informasi DNS dalam file konfigurasi `/etc/resolv.conf` yang ditemukan telah dihapus.

## Kemungkinan Alasan
Di sistem operasi CentOS 6.x, skrip init dengan versi lebih awal dari 9.03.49-1 memiliki cacat karena versi grep yang berbeda.

## Solusi
Tingkatkan skrip init ke versi terbaru dan buat informasi DNS lagi.

## Petunjuk
1. Login ke CVM.
2. Jalankan perintah berikut untuk memeriksa versi skrip init, dan verifikasi apakah ada kerusakan karena versi skrip init lebih lama dari versi 9.03.49-1.
```
rpm -q initscripts
```
Pesan yang mirip dengan yang di bawah ini ditampilkan:
```
initscripts-9.03.40-2.e16.centos.x86_64
```
Seperti yang ditunjukkan di atas, versi initscripts-9.03.40-2 lebih lama dari versi initscripts-9.03.49-1 yang cacat. Ada risiko informasi DNS akan dihapus.
3. Jalankan perintah berikut untuk meningkatkan skrip init ke versi terbaru dan menghasilkan informasi DNS lagi.
```
yum makecache
yum -y update initscripts
pemulaian ulang jaringan layanan
```
4. Jalankan perintah berikut setelah peningkatan selesai untuk memeriksa informasi versi skrip init, dan memverifikasi apakah peningkatan berhasil.
```
rpm -q initscripts
```
Pesan yang mirip dengan yang di bawah ini ditampilkan:
```
initscripts-9.03.58-1.el6.centos.2.x86_64
```
Seperti yang ditunjukkan di atas, versi yang ditampilkan berbeda dari versi sebelum peningkatan dan versi lebih baru dari initscripts-9.03.49-1. Ini menunjukkan bahwa skrip init telah berhasil ditingkatkan.
