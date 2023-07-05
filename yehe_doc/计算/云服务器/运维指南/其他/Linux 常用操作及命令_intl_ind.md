## 1. Berapa rata-rata beban server Linux?

Beban digunakan untuk mengukur beban kerja server; yaitu, panjang antrean tugas yang akan dijalankan oleh CPU. Semakin besar nilainya, semakin banyak proses yang sedang berjalan atau menunggu untuk dijalankan.

## 2. Bagaimana cara memeriksa beban server Linux?

Anda dapat menjalankan perintah `w`, `top`, `uptime`, dan `procinfo` atau mengakses file `/proc/loadavg` untuk melihat bebannya.
Harap lihat "Menginstal Perangkat Lunak di Lingkungan Linux" untuk mendapatkan petunjuk tentang cara menginstal fitur procinfo. 

## 3. Apa yang harus saya lakukan ketika beban server terlalu tinggi?

Rata-rata beban/beban server ditampilkan berdasarkan panjang antrean proses. Beban server yang tinggi (sebaiknya lihat waktu rata-rata 15 menit) mungkin disebabkan oleh sumber daya CPU yang tidak mencukupi, kendala baca/tulis I/O, sumber daya memori yang tidak mencukupi, atau tugas komputasi yang intensif. Sebaiknya jalankan perintah `vmstat`, `iostat`, dan `top` untuk mengidentifikasi alasan beban tinggi dan mengoptimalkan proses. 

## 4. Bagaimana cara memeriksa penggunaan memori server?

Anda dapat memeriksa penggunaan memori server dengan menjalankan perintah `free`, `top` (setelah dijalankan, Anda dapat menekan `shift+m` untuk mengurutkan memori), `vmstat`, dan perintah `procinfo` atau dengan mengakses `/ file proc/meminfo`. 

## 5. Bagaimana cara memeriksa penggunaan memori dari satu proses?

Anda dapat memeriksa penggunaan memori dari satu proses dengan menjalankan perintah `top -p PID`, `pmap -x PID`, dan `ps aux|grep PID` atau dengan mengakses file `/proc/$process_id (PID proses) /status` (misalnya, file `/proc/7159/status`). 

## 6. Bagaimana cara memeriksa layanan dan port yang sedang digunakan?

Anda dapat memeriksa layanan dan port yang sedang digunakan dengan menjalankan perintah `netstat -tunlp`, `netstat -antup`, dan `lsof -i:PORT`. 

## 7. Bagaimana cara memeriksa informasi proses server?

Anda dapat memeriksa informasi proses server dengan menjalankan perintah `ps auxww|grep PID`, `ps -ef`, `lsof -p PID`, dan `top -p PID`. 

## 8. Bagaimana cara menghentikan proses?

Anda dapat menjalankan `kill -9 PID` (PID menunjukkan ID proses) dan `killall program name` (misalnya, killall cron) untuk menghentikan proses.
Untuk menghentikan proses zombie, Anda perlu menghentikan proses induk dengan menjalankan `kill -9 ppid` (ppid menunjukkan ID proses induk, yang dapat dikueri dengan menjalankan `ps -o ppid PID` (misalnya, ps -o ppid 32535)). 

## 9. Bagaimana cara menemukan proses zombie?

Anda dapat menjalankan `top` untuk melihat total proses zombie, dan menjalankan `ps -ef | grep defunct | grep -v grep` untuk menemukan proses zombie tertentu. 

## 10. Mengapa saya tidak dapat mengaktifkan port server?

Anda perlu memeriksa sistem operasi dan aplikasi untuk memastikan bahwa port sudah diaktifkan.
Hanya pengguna `root` yang dapat mengaktifkan port di bawah 1024 pada sistem operasi Linux. Jalankan `sudo su -` untuk mendapatkan izin root sebelum mengaktifkan port server.
Untuk masalah aplikasi seperti konflik port atau masalah konfigurasi, gunakan log startup aplikasi untuk memecahkan masalah tersebut. Sistem server Tencent menggunakan port 36000. 

## 11. Perintah apa yang biasa digunakan untuk memeriksa performa server Linux?
<table class="t">
<tbody><tr>
<th width="100"><b>Nama Perintah</b>
</th><th> <b>Deskripsi</b>
</th></tr>
<tr>
<td>top
</td><td>top adalah program pengelola tugas yang memantau keseluruhan performa sistem.<br>
<p>Perintah ini dapat digunakan untuk menampilkan informasi seperti beban sistem, proses, CPU, memori, dan penomoran halaman. Gunakan `shift+m` dan `shift+p` untuk mengurutkan proses berdasarkan penggunaan memori dan penggunaan CPU.
</p>
</td></tr>
<tr>
<td>vmstat
</td><td>vmstat adalah fitur pemantauan sistem komputer yang terutama digunakan untuk memori virtual yang mengumpulkan dan menampilkan informasi ringkasan tentang CPU, proses, penomoran halaman memori, dan IO.<br>
<p>Misalnya, vmstat 3 10 mengeluarkan hasil setiap 3 detik dan dijalankan 10 kali.
</p>
</td></tr>
<tr>
<td>iostat
</td><td>iostat adalah alat pemantauan sistem komputer yang mengumpulkan dan menampilkan statistik tentang CPU dan IO.<br>
<p>Misalnya, iostat -dxmt 10 menampilkan informasi terperinci tentang IO dalam MB setiap 10 detik.
</p>
</td></tr>
<tr>
<td>df
</td><td>df adalah perintah yang digunakan untuk menampilkan jumlah ruang disk yang tersedia.<br>
<p>Misalnya: df -m menampilkan penggunaan ruang disk dalam ukuran MB.
</p>
</td></tr>
<tr>
<td>lsof
</td><td>lsof melaporkan daftar semua file yang terbuka, yang sangat berguna untuk pengelolaan sistem Linux.<br>
<p>Misalnya:<br>
lsof -i: 36000 menampilkan proses menggunakan port 36000.
<br>
lsof -u root menampilkan program yang dijalankan oleh root.
<br>
lsof -c php-fpm menampilkan file yang dibuka oleh proses php-fpm.
<br>
lsof php.ini menampilkan proses yang dibuka oleh php.ini.
</p>
</td></tr>
<tr>
<td>ps
</td><td>ps adalah perintah kueri proses yang menampilkan informasi yang terkait dengan proses.<br>
<p>Kombinasi parameter perintah yang umum digunakan adalah `ps -ef` dan `ps aux`. Gunakan `ps -A -o` untuk menampilkan bidang kustom. <br>
Misalnya:<br>
`ps -A -o pid,stat,uname,%cpu,%mem,rss,args,lstart,etime |sort -k6,6 -rn` mengeluarkan hasil sesuai dengan bidang yang terdaftar dan mengurutkannya menggunakan bidang ke-6.
<br>
`ps -A -o comm |sort -k1 |uniq -c|sort -k1 -rn|head` mencantumkan proses dengan jumlah terbesar yang menjalankan instans.
</p>
</td></tr></tbody></table>

Perintah dan file lain yang umum digunakan: `free -m`, `du`, `uptime`, `w`, `/proc/stat`, `/proc/cpuinfo`, dan `/proc/meminfo`. 

## 12. Apa yang harus saya lakukan ketika Cron tidak berfungsi?
Ikuti langkah-langkah di bawah ini untuk memecahkan masalah ini:
1. Verifikasi apakah crontab berjalan normal.
 1. Jalankan `crontab -e` untuk menambahkan item pengujian berikut.
```
 \*/1 \* \* \* \* /bin/date >> /tmp/crontest 2>&1 &
```
 2. Periksa file `/tmp/crontest`. 
Jika ada masalah, jalankan `ps aux|grep cron` untuk mencari pid dari cron, jalankan `kill -9 PID` untuk menghentikan proses cron, lalu jalankan `/etc/init.d/cron start` untuk mulai ulang cron. 
2. Verifikasi apakah jalur skrip di entri cron adalah jalur absolut.
3. Periksa apakah Anda menggunakan akun yang tepat untuk menjalankan cron. Selain itu, periksa apakah akun disertakan dalam `/etc/cron.deny`.
4. Periksa izin eksekusi skrip, direktori skrip, dan izin file log.
5. Sebaiknya jalankan skrip di latar belakang dengan menambahkan "&" di akhir entri skrip. Misalnya, `\*/1 \* \* \* \* /bin/date >> /tmp/crontest 2>&1 &`.

## 13. Bagaimana cara menyiapkan tugas startup untuk instans CVM saya?

Urutan startup kernel Linux adalah sebagai berikut:
1. Mulai proses `/sbin/init`.
2. Jalankan skrip awal init secara berurutan.
3. Jalankan skrip level `/etc/rc.d/rc\*.d`, tempat nilai \* berarti mode berjalan, yang dapat dikueri di `/etc/inittab`.
4. Jalankan `/etc/rc.d/rc.local`.

>? Tugas startup dapat dikonfigurasi di `/etc/rc.d/rc.local` atau di file `S\*\*rclocal` di `/etc/rc.d/rc\*.d`. 

## 14. Mengapa disk server bersifat hanya-baca?

Alasan umum untuk disk server bersifat hanya-baca adalah sebagai berikut:
- Ruang disk penuh
Anda dapat menjalankan `df -m` untuk memeriksa penggunaan disk, lalu menghapus file yang tidak perlu untuk mengosongkan ruang disk. (Sebaiknya jangan hapus file non-pihak ketiga. Harap periksa file sebelum Anda menghapusnya). 
- Semua sumber daya inode disk terisi
Anda dapat menjalankan `df -i` untuk melihat dan mengonfirmasi proses yang relevan. 
- Ada kegagalan perangkat keras

Jika tidak ada cara di atas yang berhasil, harap hubungi hotline atau kirimkan tiket. 

## 15. Bagaimana cara melihat log sistem Linux?

- Jalur penyimpanan untuk file log tingkat sistem adalah `/var/log`.
- Log sistem yang umum digunakan adalah `/var/log/messages`.

## 16. Bagaimana cara menemukan file besar di sistem file?

Anda dapat menemukannya dengan mengikuti langkah-langkah di bawah ini:
1. Jalankan `df` untuk mengkueri penggunaan partisi disk (misalnya, `df -m`).
2. Jalankan `du` untuk mengkueri ukuran folder tertentu (misalnya, `du -sh ./\*`, `du -h --max-depth=1|head -10`).
3. Jalankan `ls` untuk membuat daftar file dan ukuran file (misalnya, `ls -lSh`).
Anda juga dapat langsung memeriksa ukuran file pada bagian direktori tertentu dengan menggunakan perintah `find` (misalnya, `find / -type f -size +10M -exec ls -lrt {} \`).

## 17. Bagaimana cara memeriksa versi sistem operasi server?

Anda dapat menjalankan perintah berikut untuk memeriksa versi sistem operasi server:
- uname -a
- cat /proc/version
- cat /etc/issue 

## 18. Mengapa karakter bahasa Mandarin ditampilkan sebagai kode yang tidak dapat dipahami di terminal Linux?

Server itu sendiri tidak memberlakukan batasan pada bahasa tampilan. Dengan demikian, kemungkinan besar ini adalah masalah klien. Jika Anda menggunakan secureCRT, coba ubah pengaturan di **Options** (Opsi) -> **Session Options** (Opsi Sesi) -> **Appearance** (Tampilan). Jika Anda menggunakan perangkat lunak terminal lain, harap cari di Google untuk mencari solusi.
Jika masalah ini muncul di shell Linux murni, jalankan `export` untuk memeriksa variabel lingkungan pengguna seperti LANG dan LC_CTYPE.

## 19. Bagaimana cara mengonfigurasi batas waktu koneksi menggunakan SecureCRT?

Anda dapat mengonfigurasi pengaturan berikut agar koneksi ke instans CVM Anda tetap stabil saat terhubung ke CVM melalui SecureCRT:
1. Buka SecureCRT, lalu pilih **Options** (Opsi).
2. Pilih **Session Options** (Opsi Sesi), lalu klik **Terminal** (Terminal).
3. Pilih **Send protocol NO-OP** (Kirim NO-OP protokol) di kotak **Anti-idle** (Anti-Jeda) di sebelah kanan dan atur waktunya ke “setiap 120 detik”. 

## 20. Mengapa ruang disk di server Linux tidak dikosongkan setelah file dihapus?

**Cause:** (Penyebab:)

Setelah login ke instans CVM Linux Anda dan menghapus file menggunakan `rm`, Anda mungkin menemukan bahwa ruang disk yang tersedia tidak bertambah saat menggunakan `df` untuk memeriksa ruang disk. Ini karena ketika file dihapus, jika proses lain sedang mengakses file, ruang yang ditempati oleh file yang dihapus tidak akan segera dikosongkan pada saat Anda memeriksa ruang disk.

**Solution:** (Solusi:)

1. Jalankan `lsof |grep deleted` menggunakan izin root dan temukan PID dari proses yang menggunakan file yang dihapus.
2. Hentikan proses menggunakan `kill -9 PID`. 


## 21. Bagaimana cara menghapus file di server Linux?
Anda dapat menjalankan `rm` untuk menghapus file. File yang dihapus dengan perintah ini tidak dapat dipulihkan. Dengan demikian, harap gunakan perintah ini dengan hati-hati.
Format `rm`: `rm (opsi) (parameter)`.
- Opsi:
**-d** (-d): langsung menghapus semua data bawaan yang terdapat dalam direktori yang akan dihapus, lalu menghapus direktori itu sendiri.
**-f** (-f): menghapus file atau direktori secara paksa.
**-i** (-i): menanyakan kepada pengguna sebelum menghapus file atau direktori yang sudah ada.
**-r** (-r) atau **-R** (-R): menghapus semua file dan sub-direktori pada bagian direktori tertentu bersama-sama menggunakan pemrosesan rekursif.
**--preserve-root** (--preserve-root): tidak mengimplementasikan operasi rekursif pada direktori root.
**-v** (-v): menampilkan detail proses eksekusi perintah.
- Parameter: menentukan file atau daftar file yang akan dihapus. Jika parameter berisi direktori, tambahkan opsi `-r` atau `-R`.
- Contoh:
	- Jalankan `rm test.txt` untuk menghapus file `test.txt`.
	- Jalankan `rm -r test` untuk menghapus direktori `test`.
	- Jalankan `rm -r *` untuk menghapus semua file dan sub-direktori pada bagian direktori saat ini.
