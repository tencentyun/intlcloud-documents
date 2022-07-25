## Ikhtisar   
Konten di CSS terbuka secara default. Semua pengguna yang memiliki alamat pemutaran ulang dapat mengakses konten. Untuk mengontrol akses ke konten streaming langsung, Anda dapat mengaktifkan autentikasi pemutaran ulang.


## Cara Mengonfigurasi
Untuk mengaktifkan autentikasi pemutaran ulang, Anda perlu membuat URL terenkripsi dan memberikannya kepada pengguna akhir. Saat pengguna akhir meminta konten menggunakan URL terenkripsi dari node cache CSS, node tersebut akan memeriksa informasi autentikasi permintaan untuk menentukan validitas permintaan. Jika permintaan valid, node akan menampilkan konten; jika permintaan tidak valid, node akan menolak permintaan guna melindungi konten streaming langsung Anda dari akses tidak sah.
 

## Prasyarat
Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live).
- Anda telah menambahkan **nama domain pemutaran ulang**.

## Petunjuk
1. Pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **playback domain** (domain pemutaran ulang) yang autentikasinya ingin Anda aktifkan atau klik **Manage** (Kelola).
2. Klik **Access Control** (Kontrol Akses) dan, di area **Key Authentication** (Autentikasi Kunci), klik **Edit**.
3. Selesaikan pengaturan berikut di halaman konfigurasi autentikasi:
	1. Klik tombol di sebelah **Playback Authentication** (Autentikasi Pemutaran Ulang) untuk mengaktifkan autentikasi pemutaran ulang.
	2. Masukkan kunci utama kustom, misalnya `testlive`.
	3. (Opsional) Masukkan kunci cadangan kustom, misalnya `testing`.
	4. Masukkan masa berlaku tanda tangan, misalnya `20`.
	5. Klik **Save** (Simpan) untuk menyimpan konfigurasi.

>?
>- Autentikasi pemutaran ulang nama domain pemutaran ulang **dinonaktifkan** secara default.
> - **Authentication Key** (Kunci Autentikasi): Kunci ini ditentukan pengguna dan dapat berisi huruf besar dan kecil serta angka. Kunci ini terdiri dari kunci utama (wajib) dan kunci cadangan (opsional). Anda dapat beralih dengan mudah ke kunci cadangan jika kunci utama telah diketahui orang lain.
> - **Validity Period** (Masa Berlaku): masa berlaku tanda tangan, yang merupakan stempel waktu Unix heksadesimal.

![](https://main.qcloudimg.com/raw/b2dcc1a646a2e9e6c9bcac665aa5043c.png)
>! Setelah autentikasi diaktifkan untuk nama domain pemutaran ulang, URL pemutaran ulang asli tidak akan dapat diakses dan kesalahan 403 akan ditampilkan. Sebelum fitur ini diaktifkan, pastikan platform streaming langsung Anda kompatibel dengan algoritma autentikasi berikut agar layanan streaming Anda tidak terpengaruh.

## Contoh
URL pemutaran ulang asli:
```
http://www.test.com/live/test01.flv
```

Berikut adalah parameter autentikasi yang dikonfigurasikan:
```
Primary key (Kunci utama): ngoeiq03
Backup key (Kunci cadangan): -
Validity period (Masa berlaku): 12.495 detik
```

>! 
>- Jika Anda telah mengaktifkan autentikasi, waktu kedaluwarsa aktual URL adalah `txTime` ditambah masa berlaku kunci.
>- Demi kenyamanan, waktu yang Anda atur di konsol adalah waktu kedaluwarsa aktual. **Jika Anda telah mengaktifkan autentikasi, sistem akan menghitung `txTime` saat membuat URL pemutaran ulang.**
>- Push atau pemutaran ulang dapat tetap dilanjutkan bahkan setelah URL kedaluwarsa asalkan Anda memulai push atau pemutaran ulang sebelum waktu kedaluwarsa dan streaming tidak terputus.

Perhitungan stempel waktu:
```
Waktu pengaturan: 2018.12.01 08:30:00
Stempel waktu Unix desimal: 1543624200
Stempel waktu Unix heksadesimal: 5C01D608 (tidak peka huruf besar/kecil). CSS menggunakan stempel waktu heksadesimal untuk autentikasi.
```

Perhitungan tanda tangan autentikasi:
```
txSecret = MD5(key+StreamName+txTime) 
StreamName adalah nama streaming, yang sama dengan StreamID
txTime adalah stempel waktu
key (kunci) adalah kunci autentikasi
txSecret = MD5(ngoeiq03+test01+5C01D608)
txSecret = MD5(ngoeiq03test015C01D608)
txSecret = ce797dc6238156d548ef945e6ad1ea20
```

URL pemutaran ulang baru:
```
http://www.test.com/live/test01.flv?txSecret=ce797dc6238156d548ef945e6ad1ea20&txTime=5C01D608
```
Waktu kedaluwarsa URL ini adalah pada 2018.12.01 08:30:00 + 12.495 detik, yaitu pada tanggal 01-12-2018 pukul 11.58.15 waktu Beijing.
Jika autentikasi gagal atau URL kedaluwarsa, CSS akan menampilkan pesan 403.
