## Ikhtisar Konfigurasi

Di bagian **Origin Server Configuration** (Konfigurasi Server Asal), Anda dapat memodifikasi informasi dasar server asal, protokol tarik-asal, domain asal, dan informasi lainnya dari nama domain.


## Panduan Konfigurasi

### Konfigurasi server asal utama

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya.Buka tab **Basic Configuration** (Konfigurasi Dasar) untuk melihat bagian **Origin Server Information** (Informasi Server Asal).
![img](https://main.qcloudimg.com/raw/524f3c9aa2f9f2017d53409ee610bb5b.png)
**Origin server type** (Jenis server asal):
External origin (Origin eksternal):Pilih opsi ini jika Anda sudah memiliki server bisnis Anda sendiri (yaitu, server asal), dan masukkan daftar alamat IP yang sesuai atau nama domain sebagai alamat server asal.
[Asal COS](https://intl.cloud.tencent.com/product/cos):Jika sumber daya Anda disimpan di COS, bucket tersebut dapat dipilih sebagai server asal.

**Origin-pull protocol** (Protokol tarik-asal)
Protokol yang digunakan ketika simpul cache CDN meneruskan permintaan ke server asal untuk tarik-asal.Anda dapat memilih HTTP atau HTTPS.

Anda dapat mengonfigurasi protokol tarik-asal untuk nama domain ke HTTP, HTTPS, atau protokol ikuti dalam konfigurasi server asal:

- **HTTP**:Tarik-asal HTTP digunakan untuk permintaan akses melalui HTTP dan HTTPS.
- **HTTPS**:Tarik-asal HTTPS digunakan untuk permintaan akses melalui HTTP dan HTTPS.
- **Follow protocol** (Protokol ikuti):Permintaan HTTP menggunakan tarik-asal HTTP, sedangkan permintaan HTTPS menggunakan tarik-asal HTTPS.

> !
> - Jika Anda memilih tarik-asal HTTPS, pastikan server asal mendukung akses HTTPS, jika tidak, tarik-asal akan gagal.
> - Saat ini, Anda masih dapat mengubah item konfigurasi ini di halaman pengelolaan sertifikat.Namun, item ini akan dimigrasikan di masa depan.



**Origin server address** (Alamat server asal)
<table>
<thead>
<tr>
<td style="width:80px">Asal eksternal</td>
<td style="padding-bottom:0px;padding-top:15px"><ul><li>Anda dapat memasukkan nama domain atau beberapa IP (satu entri per baris) sebagai server asal:
<br><strong>Tarik-asal polling beberapa IP: </strong>Beberapa IP (satu entri per baris) dapat diatur sebagai server asal dan di-polling selama tarik-asal.CDN memeriksa server asal secara default.Jika IP gagal untuk waktu tertentu selama tarik-asal, IP akan diblokir secara otomatis untuk periode waktu tertentu dan dilanjutkan lagi nanti, di mana pada periode tersebut, tidak ada permintaan tarik-asal yang dikirim ke sana.<br>Jika Anda diterima sebagai pengguna beta server asal IPv6 dan mengaktifkan server asal IPv6 saat menambahkan nama domain, Anda dapat memasukkan server asal IPv6.<br><strong>Tarik-asal nama domain: </strong>Satu nama domain dapat dikonfigurasi sebagai server asal, yang harus berbeda dengan nama domain akselerasi bisnis (nama domain IPv6 tidak dapat digunakan di sini).<br><li>Port dan bobot dapat dikonfigurasi: port range (rentang port): 0-65535; weight (bobot): 1-100; format: server asal:port:bobot (port dapat dihilangkan, format: server asal::bobot)<br><strong>Catatan: </strong>Jika "HTTPS" atau "Follow Protocol" dipilih sebagai protokol tarik-asal, port harus diisi dengan 443 atau dibiarkan kosong.<br><li>Hingga 511 karakter dapat dimasukkan di kotak input server asal.</td></ul>
</tr>
</thead>
<tbody><tr>
<td>Asal COS</td>
<td>Anda dapat memilih bucket COS sebagai server asal.Akses bucket privat dapat diaktifkan.</td>
</tr>
</tbody></table>




**Origin domain** (Domain asal)
Domain origin mengacu pada nama domain situs web yang diakses di alamat IP server asal oleh simpul CDN selama tarik-asal.Domain ini diatur secara default ke nama domain akselerasi saat ini atau nama domain kartubebas jika kartubebas terhubung, dan domain asal yang sebenarnya adalah nama domain akses.Anda dapat memodifikasinya sesuai kebutuhan kecuali untuk kasus ketika asal COS digunakan.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Server Asal](https://intl.cloud.tencent.com/document/product/228/6289).

> ?Perbedaan antara alamat server asal dan domain asal adalah sebagai berikut:
> - Alamat server asal menentukan alamat IP tujuan pengiriman permintaan tarik-asal.
> - Domain origin menentukan situs web yang sesuai dengan alamat IP yang menjadi tujuan pengiriman permintaan tarik-asal.

### Konfigurasi server asal hot backup

Anda dapat menambahkan server asal hot backup untuk server asal utama Anda.Semua permintaan tarik-asal akan diteruskan ke server asal utama terlebih dahulu.Jika kode kesalahan 4XX atau 5XX dikembalikan atau pengecualian seperti waktu habis koneksi atau ketidakcocokan protokol terjadi, permintaan akan diteruskan ke server asal hot backup untuk menarik sumber daya, memastikan ketersediaan tinggi tarik-asal.

Server asal hot backup dapat dikonfigurasi dengan alamat server asal dan domain asal-nya sendiri.
![img](https://main.qcloudimg.com/raw/4d2ba172412182eb87ba40149775689f.png)

>!Jika server asal IPv6 digunakan sebagai server asal utama, server tersebut tidak dapat dikonfigurasi dengan server asal hot backup.

### Konfigurasi khusus wilayah

Jika nama domain akselerasi Anda dikonfigurasi untuk akselerasi global dan Anda ingin menghindari lalu lintas antarbatas, Anda dapat mengeklik **Add Special Configuration** (Tambahkan Konfigurasi Khusus) untuk mengonfigurasi server asal yang berbeda untuk wilayah layanan yang berbeda dari nama domain akselerasi:
![img](https://main.qcloudimg.com/raw/d4a7a61ed28daa2c3eb0febf02ca931c.png)
Pilih wilayah yang memerlukan kebijakan tarik-asal yang berbeda dan masukkan informasi server asal yang sesuai.

>!
> - Setelah konfigurasi khusus wilayah ditambahkan, saat ini konfigurasi tersebut tidak dapat langsung dihapus.
> - Jika konfigurasi khusus wilayah sama persis dengan konfigurasi dasar, konfigurasi tersebut akan digabungkan secara otomatis.Anda dapat mengonfigurasinya agar sama untuk menghapus konfigurasi khusus wilayah.

## Sampel Konfigurasi
[](id:exp)
### Konfigurasi domain asal

Jika server asal CDN dan nama domain akselerasi `www.test.com` dikonfigurasi sebagai berikut:
![img](https://main.qcloudimg.com/raw/ec2e007bb32723f7dd12aac17524c8af.png)
Rute akses untuk pengguna adalah:
Saat pengguna mengakses sumber daya `http://www.test.com/test.txt`, yang tidak di-cache pada simpul CDN, simpul akan menyelesaikan nama domain `www.abc.com` untuk mendapatkan server asal alamat `1.1.1.1`.Kemudian, simpul CDN akan mengakses server `1.1.1.1`, menemukan file `test.txt` di jalur situs web `www.def.com`, dan mengembalikan file tersebut ke pengguna.

### Konfigurasi khusus wilayah

Jika server asal CDN dan nama domain akselerasi `www.test.com` dikonfigurasi sebagai berikut:
![img](https://main.qcloudimg.com/raw/e9104ca2b0e38c62bdffb022a933b2b9.png)
Proses tarik-asal yang sebenarnya adalah:

1.Saat pengguna di Tiongkok Daratan mengakses file `http://www.test.com/test.txt` dan simpul di Tiongkok Daratan belum meng-cache sumber daya ini, simpul tersebut akan meneruskan permintaan ke server `1.1.1.1 ` dan mencoba mencari file `test.txt` di jalur situs web `1.test.com`.Jika sumber daya tersebut ada, simpul akan langsung mengembalikan file ke pengguna.Jika tidak, simpul akan melanjutkan ke Langkah 2.
2.Karena simpul CDN di Tiongkok Daratan gagal meneruskan permintaan ke server asal utama dan tidak dapat menemukan sumber daya, simpul CDN akan meneruskan permintaan ke server `2.2.2.2`, menemukan file `test.txt` di jalur situs web `1.test.com`, lalu meng-cache dan mengembalikannya ke pengguna.
3.Saat ini, pengguna di luar Tiongkok Daratan mengakses file `http://www.test.com/test.txt`.Karena simpul di luar Tiongkok Daratan belum menyimpan sumber daya ini, simpul tersebut akan meneruskan permintaan ke server `3.3.3.3` dan mencoba menemukan file `test.txt` di jalur situs web `3.test.com`.Jika sumber daya tersebut ada, simpul akan langsung mengembalikan file ke pengguna.Jika tidak, simpul akan melanjutkan ke langkah 4.
4.Karena simpul CDN di luar Tiongkok Daratan gagal meneruskan permintaan ke server asal utama di luar Tiongkok Daratan dan tidak dapat menemukan sumber daya, simpul CDN akan meneruskan permintaan ke server `4.4.4.4`, mencari file `test.txt` di jalur situs web `4.test.com`, lalu meng-cache dan mengembalikannya ke pengguna di luar Tiongkok Daratan.
