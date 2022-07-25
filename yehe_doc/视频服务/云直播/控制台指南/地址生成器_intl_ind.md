Konsol CSS menyediakan pembuat alamat. Anda dapat memasukkan informasi URL di pembuat alamat untuk membuat URL push/pemutaran ulang dengan cepat. URL streaming langsung umumnya terdiri dari nama domain (`domain`), nama aplikasi (`AppName`), nama streaming (`StreamName`), dan kunci autentikasi (`Key`).
![](https://main.qcloudimg.com/raw/55879651fe2ca61a3699ab4ed9de41d4.jpg)
Setelah URL dibuat, Anda dapat **memilih dan menyalin URL**, **mengeklik tombol di sebelahnya untuk menyalin URL**, atau **memindai kode QR di sebelahnya untuk mendapatkan URL**.


## Catatan
- CSS tidak merekam URL yang dibuat sebelumnya. Harap salin URL setelah dibuat.
- Jika perlu membuat beberapa URL streaming langsung, sebaiknya Anda menyambungkan URL seperti yang diinstruksikan di [Splicing Live Streaming URLs (Menyambungkan URL Streaming Langsung)](https://intl.cloud.tencent.com/document/product/267/38393).
- CSS menyediakan nama domain pengujian `xxxx.livepush.myqcloud.com`. Anda dapat menggunakannya untuk pengujian push, tetapi kami tidak menyarankan Anda untuk menggunakannya sebagai nama domain push untuk bisnis real Anda.
- Anda bisa mendapatkan URL dengan memindai kode QR dengan [Toolkit Tencent Cloud](https://intl.cloud.tencent.com/document/product/1071/38147).
- Jika akhiran nama streaming sama dengan ID templat transcoding, streaming tidak dapat diputar ulang. Dalam situasi ini, harap ubah nama streaming.



## Prasyarat
Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live/livestat), dan telah menambahkan [nama domain push](https://intl.cloud.tencent.com/document/product/267/35970).

## Deskripsi Parameter

<table>
<thead><tr><th>Parameter</th><th>Deskripsi</th></tr></thead>
<tbody><tr>
<td>Domain Type (Jenis Domain)</td>
<td>Pilih <strong>Push Domain</strong> (Domain Push) atau <strong>Playback Domain</strong> (Domain Pemutaran Ulang).</td>
</tr><tr><td>AppName</td>
<td>Nama aplikasi streaming langsung, digunakan untuk mengidentifikasi jalur penyimpanan file streaming langsung. Nilai default: `live`.<br>Nama hanya boleh terdiri dari huruf, angka, dan simbol.</td>
</tr><tr><td>StreamName</td>
<td>Nama streaming kustom. Nama ini adalah pengidentifikasi unik streaming langsung.<br>Nama hanya boleh terdiri dari huruf, angka, dan simbol.</td>
</tr><tr><td>Expiration Time (Waktu Kedaluwarsa)</td>
<td><li>Waktu kedaluwarsa URL pemutaran ulang adalah waktu yang dikonfigurasikan ditambah periode valid autentikasi pemutaran ulang.<li>Waktu kedaluwarsa URL push sama dengan waktu kedaluwarsa yang dikonfigurasikan.</td>
</tr><tr><td>Transcoding Template (Templat Transcoding)</td>
<td><li>Hanya berlaku jika Anda memilih <strong>domain pemutaran ulang</strong>.<li>Jika Anda memilih <a href="https://intl.cloud.tencent.com/document/product/267/31071">templat transcoding</a>, URL yang dihasilkan akan menjadi URL untuk streaming yang di-transcoding. Untuk memutar ulang streaming langsung asli, Anda tidak perlu memilih templat transcoding.</td>
</tr>
</tbody></table>

[](id:push)
## Membuat URL Push
### Petunjuk
1. Login ke konsol CSS, lalu klik **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** (Pembuat Alamat).
2. Pilih **Push Domain** (Domain Push) sebagai jenis domain, lalu pilih nama domain push yang telah Anda tambahkan di halaman manajemen domain.
3. Masukkan **AppName**. Nama yang diberikan secara default adalah `live`.
4. Masukkan **StreamName**, misalnya `liveteststream`.
5. Pilih waktu kedaluwarsa URL, misalnya `2021-12-15 10:06:22`.
6. Klik **Generate Address** (Buat Alamat).

![](https://qcloudimg.tencent-cloud.cn/raw/68d6cc91bb1092b418f5863f7d91e832.png)

[](id:pushurl)
### Catatan
Karena protokol RTMP, WebRTC, dan SRT didukung untuk push, URL push yang dibuat memiliki awalan `rtmp://`, `webrtc://`, atau `srt://`.
![](https://qcloudimg.tencent-cloud.cn/raw/d866991901d2c780112da709d4e0ba3c.png)


[](id:play)
## Membuat URL Pemutaran Ulang
### Petunjuk
1. Login ke konsol CSS, lalu klik **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** (Pembuat Alamat).
2. Pilih **Playback Domain** (Domain Pemutaran Ulang) sebagai jenis domain, lalu pilih nama domain pemutaran ulang yang telah Anda tambahkan di halaman manajemen domain.
3. Masukkan **AppName**. Nama yang diberikan secara default adalah `live`.
4. Masukkan **StreamName**, misalnya `liveteststream`.
5. Pilih waktu kedaluwarsa URL, misalnya `2021-12-15 10:20:26`.
6. Pilih templat transcoding yang dibuat akan digunakan atau tidak.
6. Klik **Generate Address** (Buat Alamat).

![](https://qcloudimg.tencent-cloud.cn/raw/838b4bc6cf9df0c308f9636b1d7c06af.png)

[](id:playurl)
### Catatan
Jika Anda memilih templat transcoding, pembuat alamat akan membuat URL untuk streaming yang di-transcoding. Karena protokol RTMP, HTTP-FLV, HLS, dan WebRTC didukung untuk pemutaran ulang, URL pemutaran ulang yang dibuat memiliki awalan `rtmp://`, `http://`, atau `webrtc://`.
>! URL pemutaran ulang UDP adalah untuk [LEB](https://intl.cloud.tencent.com/document/product/267/41030). Penagihan LEB dapat dipelajari di [Pricing Overview (Ikhtisar Harga)](https://intl.cloud.tencent.com/document/product/267/2819).

![](https://qcloudimg.tencent-cloud.cn/raw/345cc01a3d77d6816d1789fe60b7184e.png)
