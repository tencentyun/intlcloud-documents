## Skenario

Dokumen ini menjelaskan cara menyelidiki dan memecahkan masalah seperti kegagalan login ke CVM Linux karena penggunaan CPU dan memori yang tinggi.

## Petunjuk

### Login dan melihat beban sistem

1. Login ke CVM dengan cara yang berbeda tergantung kebutuhan aktual Anda.
	- Login ke CVM Linux melalui perangkat lunak pihak ketiga dari jarak jauh.
	> Ketika CVM Linux memiliki beban CPU yang tinggi, Anda mungkin gagal untuk login.
	>
	- Login ke CVM melalui **VNC**.
	Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm) > klik **Log in** (Login) di kolom operasi kanan > login dengan metode login alternatif (VNC).
	> Ketika CVM Linux memiliki beban CPU yang tinggi, Anda mungkin dapat login melalui konsol secara normal.
	>
2. Jalankan perintah berikut untuk melihat beban sistem. Lihat kolom `%CPU` dan kolom `%MEM` dan identifikasi proses mana yang menghabiskan lebih banyak sumber daya.
```
atas
```

### Mengakhiri proses

1. Bandingkan penggunaan sumber daya dari proses yang berbeda dan catat PID dari proses yang perlu dihentikan.
2. Masukkan ` k `.
3. Masukkan PID dari proses yang perlu dihentikan, dan tekan **Enter** untuk menghentikannya seperti yang ditunjukkan di bawah ini:
Misalnya, Anda perlu menghentikan proses yang PID-nya 23.
![](//mc.qcloudimg.com/static/img/61cd74354cf2b4d2a80a83528a500f5c/image.png)
> Jika `kill PID 23 with signal [15]:` muncul setelah Anda menekan **Enter**, tekan **Enter** lagi untuk mempertahankan pengaturan default.
>
4. Jika operasi berhasil, pesan berikut, ` Send PID 23 signal [15/sigterm] ` akan muncul. Tekan **Enter** untuk mengonfirmasi penghentian.

### Penggunaan CPU rendah tetapi rata-rata beban tinggi

### Deskripsi Masalah

Rata-rata beban merupakan indikator beban CPU. Rata-rata beban tinggi menunjukkan antrean panjang dari proses yang menunggu untuk dijalankan.
Menjalankan `top` mengembalikan penggunaan CPU yang sangat rendah tetapi rata-rata beban yang sangat tinggi seperti yang ditunjukkan di bawah ini.
![](//mc.qcloudimg.com/static/img/4ddf663a68ee602d8cf8075d88edccf6/image.png)
 
#### Solusi
 
Jalankan perintah berikut untuk melihat status proses dan memeriksa apakah ada proses dalam status D seperti yang ditunjukkan di bawah ini:
```
ps -axjf
```
![](//mc.qcloudimg.com/static/img/32420d3fe022b57d85120c941705dbf6/image.png)
 > Proses dalam status D berada dalam mode siaga tanpa gangguan. Proses dalam status tidak dapat dihentikan atau keluar dengan sendirinya. Jika ada banyak proses dalam status D, Anda dapat memecahkan masalah dengan memulihkan sumber daya yang bergantung pada proses atau memulai ulang sistem.
 >


### proses kswapd0 menggunakan banyak CPU

### Deskripsi Masalah

Linux mengelola memori dengan mekanisme penomoran halaman, dan juga menyisihkan sebagian dari disk untuk memori virtual. kswapd0 adalah proses yang bertanggung jawab untuk penggantian halaman dalam manajemen memori virtual sistem Linux. Ketika tidak ada cukup memori sistem, kswapd0 akan sering mengganti halaman, yang sangat memakan CPU. Itu sebabnya prosesnya menggunakan banyak CPU.
 
#### Solusi

1. Jalankan perintah berikut dan temukan proses kswapd0.
```
atas
```
2. Amati status proses kswapd0.
Jika proses tidak tidur, berjalan lama, dan menggunakan banyak CPU, lakukan [Step3](#kswapd0_step3) untuk memeriksa tingkat penggunaan memori.
3. <span id="kswapd0_step3">Jalankan perintah, seperti `free`，`ps` untuk memeriksa berapa banyak memori yang digunakan oleh proses dalam sistem.</span>
Mulai ulang sistem atau hentikan proses yang aman tetapi tidak perlu berdasarkan tingkat penggunaan memori.

Jika masalah belum terselesaikan, silakan merujuk ke [Tingkat penggunaan CPU tinggi (sistem Linux)](https://intl.cloud.tencent.com/document/product/213/14634) untuk detail selengkapnya.
