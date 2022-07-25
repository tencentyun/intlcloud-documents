## Catatan
Setelah membuat [templat transcoding](https://intl.cloud.tencent.com/document/product/267/31071) dan [mengikatnya](https://intl.cloud.tencent.com/document/product/267/31071#related) dengan nama domain pemutaran ulang, Anda harus menambahkan nama templat transcoding setelah `StreamName` streaming langsung dengan konfigurasi transcoding dalam format `StreamName_transcoding template name` (StreamName_nama templat transcoding). Penjelasan mendetail dapat dilihat di [Playback Configuration (Konfigurasi Pemutaran Ulang)](https://intl.cloud.tencent.com/document/product/267/31058).

## Prasyarat
- Anda telah membuat akun Tencent Cloud dan mengaktifkan [layanan CSS](https://intl.cloud.tencent.com/product/css).
- Anda telah mengajukan permohonan nama domain melalui [Tencent Cloud Domain Service (Layanan Domain Tencent Cloud)](https://dnspod.cloud.tencent.com/?from=qcloudProductDns).
- Anda telah menambahkan nama domain push/pemutaran ulang di **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) konsol CSS dan berhasil mengonfigurasi rekaman CNAME. Petunjuk selengkapnya dapat dilihat di [Adding Domain Names (Menambahkan Nama Domain)](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:push)
## Menyambungkan URL Push
Jika Anda menjalankan ruang streaming langsung dalam jumlah besar, URL push dan pemutaran ulang untuk setiap host tidak dapat dibuat secara manual. Dalam kasus tersebut, Anda dapat menggunakan server untuk **menyambungkan** alamat secara otomatis. Semua URL yang memenuhi standar Tencent Cloud dapat digunakan untuk push. URL push standar terdiri atas empat bagian, seperti yang ditunjukkan oleh gambar berikut:
![](https://main.qcloudimg.com/raw/679602c838e8dfd3b61acefebb221d13.jpg)
- **Domain**
Nama domain push, yang bisa berupa nama domain push default yang disediakan oleh CSS Tencent Cloud atau nama domain push dengan rekaman CNAME yang sudah Anda tambahkan dan buat.
- **AppName**
Nama aplikasi streaming langsung, yang secara default diberi nama `live`, tetapi dapat diubah.
- **StreamName (ID streaming)**
Nama streaming kustom, yang berupa ID unik suatu streaming langsung. Anda sebaiknya menggunakan string numerik atau alfanumerik acak untuk parameter ini.
- **Kunci autentikasi (opsional)**
Kunci autentikasi terdiri dari `txSecret` dan `txTime`: `txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.
Jika autentikasi push diaktifkan, URL yang digunakan untuk push harus berisi kunci autentikasi. Jika autentikasi push dinonaktifkan, URL push tidak harus berisi "?" dan konten yang mengikutinya.
 - **txTime (waktu kedaluwarsa URL)** 
Waktu ketika URL kedaluwarsa, dalam format stempel waktu Unix heksadesimal.
  >?Sebagai contoh, `5867D600` berarti bahwa URL kedaluwarsa pada pukul 00.00.00, tanggal 1 Januari 2017. Periode validitas sebaiknya tidak terlalu singkat atau terlalu lama. Sebagian besar klien kami mengatur `txTime` ke titik dengan jarak waktu 24 jam atau lebih lama dari waktu saat ini. Jika periode validitas terlalu singkat, setelah koneksi host terputus karena masalah jaringan selama siaran langsung, push akan sangat sulit dilanjutkan karena URL push sudah kedaluwarsa.
 - **txSecret (tanda tangan perlindungan hotlink)**
Tanda tangan `txSecret` berfungsi mencegah penyerang memalsukan backend untuk membuat URL push. Penjelasan seputar metode perhitungan dapat dilihat di [Best Practice - Hotlink Protection URL Calculation] (Praktik Terbaik - Perhitungan URL Perlindungan Hotlink) (https://intl.cloud.tencent.com/document/product/267/31560).

[](id:play)
## Menyambungkan URL Pemutaran Ulang
URL pemutaran ulang terdiri dari awalan protokol pemutaran ulang, nama domain (`domain`), nama aplikasi (`AppName`), nama streaming (`StreamName`), akhiran protokol pemutaran ulang, kunci autentikasi, dan parameter kustom lainnya. Berikut adalah beberapa contohnya. 

``` 
webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```

- **Playback prefix** (Awalan pemutaran ulang)  
<table>
    <tr><th>Protokol Pemutaran Ulang</th><th>Awalan Pemutaran Ulang</th><th>Catatan</th></tr>
		<tr>
        <td>WebRTC</td>
        <td><code>webrtc://</code> </td>
        <td>Penggunaan WebRTC sangat kami rekomendasikan karena memiliki performa streaming instan terbaik dan mendukung konkurensi ultra-tinggi.</td>
    </tr><tr>
        <td>HTTP-FLV </td>
        <td><code>http://</code> atau <code>https://</code></td>
        <td>Penggunaan HTTP-FLV kami rekomendasikan karena memiliki performa streaming instan yang baik dan mendukung konkurensi tinggi.</td>
    </tr><tr>
				<td>RTMP</td>
        <td><code>rtmp://</code> </td>
        <td>Penggunaan RTMP tidak kami rekomendasikan karena memiliki performa streaming instan yang buruk dan tidak mendukung konkurensi yang tinggi.</td>
    </tr><tr>
        <td>HLS (M3U8)</td>
        <td><code>http://</code> atau <code>https://</code></td>
        <td>Kami merekomendasikan HLS untuk klien seluler dan untuk browser Safari di macOS.</td>
    </tr>
</table>
- **Domain**  
  Nama domain pemutaran ulang, nama domain dengan rekaman CNAME yang sudah Anda tambahkan dan buat.
- **AppName** 
  Nama aplikasi streaming langsung yang digunakan untuk mengidentifikasi jalur penyimpanan file media streaming langsung. Secara default, aplikasi diberi nama `live`, tetapi nama ini dapat diubah.
- **StreamName (nama streaming)[](id:streamname)**  
  Nama streaming kustom, yang berupa ID unik suatu streaming langsung. Anda sebaiknya menggunakan string numerik atau alfanumerik acak.
- **Kunci autentikasi (opsional)** 
  Kunci autentikasi terdiri dari `txSecret` dan `txTime`: `txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.
Jika autentikasi pemutaran ulang diaktifkan, URL yang digunakan untuk pemutaran ulang harus berisi kunci autentikasi. Jika autentikasi pemutaran ulang dinonaktifkan, URL pemutaran ulang tidak harus berisi "?" dan konten yang mengikutinya.
 - **txTime (waktu kedaluwarsa alamat):** waktu ketika URL kedaluwarsa, dalam format stempel waktu Unix heksadesimal.
 - **txSecret (tanda tangan perlindungan hotlink):** berfungsi mencegah penyerang memalsukan backend untuk membuat URL pemutaran ulang. Penjelasan seputar metode perhitungan dapat dilihat di [Best Practice - Hotlink Protection URL Calculation] (Praktik Terbaik - Perhitungan URL Perlindungan Hotlink) (https://intl.cloud.tencent.com/document/product/267/31560).


[](id:push_code)
## Melihat Kode Push Sampel
Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) konsol CSS, pilih nama domain push yang sudah dikonfigurasikan sebelumnya, klik **Manage** > **Push Configuration** (Kelola > Konfigurasi Push) untuk menampilkan **Push Address Sample Code** (Kode Sampel Alamat Push) (untuk PHP dan Java) yang menunjukkan cara membuat alamat perlindungan hotlink. Petunjuk lengkap dapat dilihat di [Push Configuration (Konfigurasi Push)](https://intl.cloud.tencent.com/document/product/267/31059).


