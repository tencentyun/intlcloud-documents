
Perlindungan hotlink keamanan mengacu pada bidang `txSecret` di URL push dan pemutaran ulang, yang digunakan untuk mencegah penyerang memalsukan backend Anda untuk pembuatan URL push atau mencuri alamat pemutaran ulang Anda guna mendapatkan keuntungan dengan cara yang melanggar hukum.

## Cara Kerja
Untuk mencegah penyerang memalsukan server Anda guna membuat URL push dan pemutaran ulang, Anda dapat mengonfigurasikan kunci enkripsi perlindungan hotlink di Konsol CSS seperti yang ditunjukkan di bawah ini (jangan beri tahu kunci ini kepada orang lain) agar penyerang tidak dapat dengan mudah memalsukan URL push dan pemutaran ulang yang valid, sebagaimana yang ditampilkan oleh gambar di bawah ini.

![](https://main.qcloudimg.com/raw/ea3a932bd9e4e35fc95560cfbc4b3241.jpg)

## Proses Perhitungan
### Langkah 1. Kunci autentikasi
Pertama, Anda harus mengonfigurasikan kunci enkripsi di konsol, yang digunakan untuk membuat tanda tangan perlindungan hotlink di server Anda. Tencent Cloud juga memiliki kunci yang sama dengan Anda sehingga dapat mendekripsi dan mengonfirmasi tanda tangan yang Anda buat.

 Kunci enkripsi bisa berupa kunci perlindungan hotlink push atau kunci perlindungan hotlink pemutaran ulang. Kunci perlindungan hotlink push digunakan untuk membuat URL perlindungan hotlink push, sedangkan kunci perlindungan hotlink pemutaran ulang digunakan untuk membuat URL perlindungan hotlink pemutaran ulang. Buka **CSS Console** > **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Konsol CSS > Manajemen Domain), klik nama domain atau **Manage** (Kelola), lalu pilih **Push Configuration** (Konfigurasi Push) untuk mengonfigurasi kunci perlindungan hotlink push, seperti yang ditampilkan oleh gambar berikut.

![](https://main.qcloudimg.com/raw/0833ac9f646507a3bf1f288709dddd20.png)

Informasi selengkapnya tentang kunci perlindungan hotlink pemutaran ulang dapat dilihat di [Bagaimana cara mengaktifkan perlindungan hotlink pemutaran ulang?](https://intl.cloud.tencent.com/document/product/267/35598#que6). 

### Langkah 2. Membuat `txTime`
Plaintext (teks biasa) di tanda tangan adalah `txTime`, yang merupakan periode validitas tautan. Sebagai contoh, jika waktu saat ini adalah 2018-12-29 11:13:45 dan URL yang harus dibuat diharapkan akan berlaku selama 3 jam, `txTime` harus diatur ke 2018-12-29 14:13:45.
Namun, memasukkan string waktu yang sangat panjang ke URL bukan langkah yang tepat. Dalam penggunaan aktual, kami terlebih dahulu mengonversi 2018-12-29 14:13:45 menjadi stempel waktu UNIX, yaitu, 1546064025 (Anda dapat memanggil fungsi waktu dalam bahasa pemrograman untuk melakukan konversi dan pemrosesan), lalu mengonversikannya ke string heksadesimal untuk mengurangi panjang karakter lebih lanjut, yaitu txTime = 1546064025 (desimal) = 5C271099 (heksadesimal). Penggunaan string desimal juga didukung.

>!
>- Waktu akhir aktual adalah `txTime` ditambah periode validitas autentikasi. Modifikasi periode validitas autentikasi tidak akan memengaruhi pembuatan URL.
>- Waktu kedaluwarsa tidak boleh terlalu awal atau terlalu akhir:
	- Jika waktu kedaluwarsa terlalu awal, ketika host mengalami jitter jaringan selama streaming langsung, push tidak akan dilanjutkan kembali karena URL push pasti telah kedaluwarsa.
	- Jika waktu kedaluwarsa terlalu akhir, ada risiko push tidak diizinkan.

### Langkah 3. Membuat `txSecret`
Metode pembuatan `txSecret` adalah `MD5(KEY + StreamName + txTime)`. `KEY` adalah kunci enkripsi yang dikonfigurasikan di langkah 1. `StreamName`, yang juga disebut stream ID (ID streaming), merupakan Pengujian dalam contoh ini (sebaiknya gunakan bilangan acak atau ID pengguna). `txTime` adalah 5C271099 yang dihitung di langkah terakhir, sedangkan MD5 adalah algoritme hash MD5 satu arah standar yang tidak dapat dikembalikan.
Contoh:
```
KEY adalah e12c46f2612d5106e2034781ab261ca3
Jadi, txSecret = MD5(e12c46f2612d5106e2034781ab261ca3test5C271099) = f85a2ab363fe4deaffef9754d79da6fe
```

### Langkah 4. Membuat URL perlindungan hotlink
URL push yang mematuhi standar Tencent Cloud terdiri atas empat bagian berikut ini:
![](https://main.qcloudimg.com/raw/679602c838e8dfd3b61acefebb221d13.jpg)
Kita dapat membuat URL standar menggunakan `txTime` (yang berisi informasi waktu kedaluwarsa URL push/pemutaran ulang kepada Tencent Cloud), `txSecret` (yang dapat didekripsi dan diverifikasi hanya oleh Tencent Cloud), `StreamName`, dan nama domain push (misalnya "livepush.tcloud.com"). Dalam contoh ini, URL push adalah:

```
rtmp://livepush.tcloud.com/live/test?txSecret=f85a2ab363fe4deaffef9754d79da6fe&txTime=5C271099
```


## Kode Push Sampel
Buka **CSS Console** > **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Konsol CSS > Manajemen Domain), pilih nama domain push yang sudah dikonfigurasikan sebelumnya, klik **Manage** > **Push Configuration** (Kelola > Konfigurasi Push) untuk menampilkan **Push Address Sample Code** (Kode Sampel Alamat Push) (untuk PHP dan Java) yang menampilkan cara membuat alamat perlindungan hotlink. Keterangan selengkapnya dapat dilihat di [Push Configuration (Konfigurasi Push)](https://intl.cloud.tencent.com/document/product/267/31059#sample-code-of-push-url).
