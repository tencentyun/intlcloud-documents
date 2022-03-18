
Dokumen ini menjelaskan cara mendiagnosis dan memecahkan masalah login CVM Linux atau Windows yang disebabkan oleh penggunaan bandwidth yang tinggi.

## Masalah
- Di [Konsol CVM](https://console.cloud.tencent.com/cvm/index), data pemantauan bandwidth dari CVM menunjukkan bahwa penggunaan bandwidth terlalu tinggi, dan koneksi ke CVM gagal.

## Menemukan dan memecahkan masalah

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pilih CVM yang akan diperiksa dan klik **Log In** (Login). Hal ini ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Di jendela **Log into Windows/Linux instance** (Login ke instans Windows/Linux) yang muncul, pilih **Alternative login methods (VNC)** (Metode login alternatif (VNC)), lalu klik **Log In Now** (Login Sekarang), untuk login ke CVM.
4. Pada jendela login yang muncul, pilih **Send Remote Command** (Kirim Perintah Jarak Jauh) di sudut kiri atas, dan klik **Ctrl-Alt-Delete** (Ctrl-Alt-Delete) untuk masuk ke antarmuka login sistem seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### CVM Windows
Setelah menggunakan VNC untuk login ke CVM Windows, lakukan operasi berikut:
> Operasi berikut menggunakan CVM dengan sistem Windows Server 2012 sebagai contoh.
>
1. Di CVM, klik <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>. Pilih **Task Manager** (Pengelola Tugas) untuk membuka jendela **Task Manager** (Pengelola Tugas).
2. Pilih halaman tab **Performance** (Performa) dan klik **Open Resource Monitor** (Buka Pemantau Sumber Daya). Hal ini ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/a635da7e769cc1424b225674803e5cb1.png)
3. Setelah **Resource Monitor** (Pemantau Sumber Daya) terbuka, periksa proses mana yang menghabiskan lebih banyak bandwidth. Sesuai dengan bisnis aktual Anda, tentukan apakah prosesnya normal. Hal ini ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/6a131472fc52bb4f5c4d5f57a1b7b010.png)
 - Jika proses yang menghabiskan banyak bandwidth adalah normal, periksa apakah itu karena perubahan volume akses, dan apakah Anda perlu mengoptimalkan kapasitas atau [meningkatkan konfigurasi CVM](https://intl.cloud.tencent.com/document/product/213/2178).
 - Jika proses yang menghabiskan banyak bandwidth tidak normal, kemungkinan ada virus atau Trojan. Anda dapat menghentikan prosesnya sendiri atau menggunakan perangkat lunak keamanan. Anda juga dapat menginstal ulang sistem setelah pencadangan data.
 > Dalam sistem Windows, banyak proses virus yang disamarkan sebagai proses sistem. Anda dapat menggunakan informasi proses di **Task Manager** (Pengelola Tugas) > **Processes** (Proses) untuk melakukan pemeriksaan awal:
 > Proses sistem normal memiliki tanda tangan dan deskripsi lengkap, dan sebagian besar terletak dalam direktori C:\Windows\System32. Program virus mungkin memiliki nama yang sama dengan proses sistem, tetapi tidak memiliki tanda tangan atau deskripsi. Lokasinya juga akan menjadi tidak normal.
 > 
 - Jika proses yang menghabiskan banyak bandwidth adalah proses komponen Tencent Cloud, [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk menghubungi kami. Kami akan membantu Anda menemukan dan memecahkan masalah.

### CVM Linux
Setelah menggunakan VNC untuk login ke CVM Linux, lakukan operasi berikut:
> Operasi berikut menggunakan CVM dengan sistem CentOS 7.6 sebagai contoh.
>
1. Jalankan perintah berikut untuk menginstal alat iftop. Alat iftop adalah gadget pemantauan lalu lintas untuk CVM Linux.
```
yum install iftop -y
```
> Untuk sistem Ubuntu, jalankan perintah `apt-get install iftop -y`.
>
2. Jalankan perintah berikut untuk menginstal lsof.
```
yum install lsof -y
```
3. Jalankan perintah berikut untuk menjalankan iftop. Hal ini ditunjukkan pada gambar berikut:
```
iftop
```
![](https://main.qcloudimg.com/raw/7fccea56d998a65df6ff7e9348772910.png)
 - `<=`、`=>` menunjukkan arah lalu lintas
 - TX menunjukkan lalu lintas pengiriman
 - RX menunjukkan lalu lintas penerima
 - TOTAL menunjukkan lalu lintas total
 - cum menunjukkan total lalu lintas dari saat iftop mulai berjalan hingga sekarang
 - peak menunjukkan puncak lalu lintas
 - rates menunjukkan lalu lintas rata-rata selama 2dtk, 10dtk, dan 40dtk terakhir secara berurutan
4. Menurut IP lalu lintas yang digunakan di iftop, jalankan perintah berikut untuk memeriksa proses yang terhubung ke IP ini.
```
lsof -i | grep IP
```
Misalnya, jika IP lalu lintas yang digunakan adalah 201.205.141.123, jalankan perintah berikut:
```
lsof -i | grep 201.205.141.123
```
Jika hasil berikut ditampilkan, bandwidth CVM sebagian besar digunakan oleh proses SSH.
```
sshd       12145    root    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
sshd       12179  ubuntu    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
```
5. Lihat proses yang menghabiskan bandwidth, dan tentukan apakah prosesnya normal.
 - Jika proses yang menghabiskan banyak bandwidth adalah normal, periksa apakah itu karena perubahan volume akses, dan apakah Anda perlu mengoptimalkan kapasitas atau [meningkatkan konfigurasi CVM](https://intl.cloud.tencent.com/document/product/213/2178).
 - Jika proses yang menghabiskan banyak bandwidth tidak normal, kemungkinan ada virus atau Trojan. Anda dapat menghentikan prosesnya sendiri atau menggunakan perangkat lunak keamanan. Anda juga dapat menginstal ulang sistem setelah pencadangan data.
 - Jika proses yang menghabiskan banyak bandwidth adalah proses komponen Tencent Cloud, [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk menghubungi kami. Kami akan membantu Anda menemukan dan memecahkan masalah.


Sebaiknya periksa lokasi IP tujuan di [Apa yang Dimaksud dengan Alamat IP](https://whatismyipaddress.com/). Jika lokasi IP berada di negara/kawasan lain, risiko keamanannya lebih besar.

