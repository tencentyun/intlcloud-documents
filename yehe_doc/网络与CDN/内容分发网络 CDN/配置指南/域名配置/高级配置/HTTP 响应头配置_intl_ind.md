## Ikhtisar Konfigurasi

Saat pengguna akhir meminta sumber daya bisnis, Anda dapat menambahkan header khusus di **response message** (pesan respons) yang dikembalikan untuk mengimplementasikan berbagi sumber daya lintas origin.
Header respons dikonfigurasi pada tingkat nama domain. Setelah konfigurasi diterapkan, konfigurasi akan disinkronkan ke pesan respons dari setiap sumber daya di bawah nama domain. Konfigurasi header respons hanya membuat perubahan pada respons klien (peramban) tetapi tidak pada cache simpul CDN.

## Panduan Konfigurasi

### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Buka tab **Advanced Configuration** (Konfigurasi Lanjutan) untuk melihat bagian **Response Header Configuration** (Konfigurasi Header Respons). Ini dinonaktifkan secara default. Anda dapat mengeklik **Add Rule** (Tambahkan Aturan) untuk menambahkan aturan header respons.
![img](https://main.qcloudimg.com/raw/979a6f3254776cdadd5ca4dc71d631a6.png)

### Operasi

| Operasi | Deskripsi                                                         |
| :------- | :----------------------------------------------------------- |
| Set (Atur)    | Mengubah nilai parameter header respons yang ditentukan.<br/>Jika header target tidak ada, header target akan ditambahkan setelah perubahan.<br/>Jika parameter header sudah ada, semua duplikat akan diubah dan digabungkan menjadi satu header. Misalnya, setelah aturan "Set - `x-cdn: value1`" dikonfigurasi, jika permintaan berisi beberapa header `x-cdn`, header akan diubah dan digabungkan menjadi satu header `x-cdn: value1`. |
| Delete (Hapus)     | Menghapus parameter header respons yang ditentukan.                                       |

> !
> - Beberapa header tidak dapat diatur atau dihapus secara mandiri. Untuk daftar mendetail, silakan lihat [Catatan](#pemberitahuan).
> - Hingga 10 aturan header respons dapat dikonfigurasi.
> - Prioritas aturan dapat disesuaikan. Aturan yang lebih rendah dalam daftar memiliki prioritas lebih tinggi. Jika parameter header dikonfigurasi dengan beberapa aturan, aturan bawah akan diterapkan saat aturan dijalankan dari bawah ke atas.

### Parameter header

<table>
<thead>
<tr>
<th style="width:230px">Parameter Header</th>
<th>Deskripsi</th>
</tr>
</thead>
<tbody><tr>
<td>Access-Control-Allow-Origin</td>
<td>Header terkait izin lintas origin, yang menentukan domain yang diizinkan untuk mengakses sumber daya. Hingga 10 domain dapat dikonfigurasi. Jika host permintaan sumber dikonfigurasi sebagai nilai parameter header, akan diisi ke header respons. Anda juga dapat mengaturnya sebagai `*` untuk mengizinkan semua domain mengakses sumber daya. Untuk informasi selengkapnya, silakan lihat <a href="#acao">Deskripsi Mode Pencocokan Access-Control-Allow-Origin</a>.<br>Kartubebas `*`, nama domain, dan IP didukung. `http://` atau `https://` harus tercakup. Pisahkan beberapa entri dengan `,`, dan hingga 66 entri didukung. Misalnya, `http://test.com,http://1.1.1.1`. </td>
</tr>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>Menentukan metode permintaan HTTP lintas origin dan mendukung beberapa metode sekaligus: <br>`Access-Control-Allow-Methods: <code>POST, GET, OPTIONS`</code>.</td>
</tr>
<tr>
<td>Access-Control-Max-Age</td>
<td>Menentukan periode validitas (dalam detik) permintaan preflight.<br>Untuk permintaan lintas origin yang tidak sederhana, permintaan kueri HTTP, yaitu permintaan preflight, diperlukan sebelum komunikasi resmi untuk memeriksa apakah permintaan lintas origin aman untuk diterima. Permintaan lintas origin tidak sederhana jika:<br>Bukan permintaan GET, HEAD, atau POST, atau permintaan POST tetapi jenis data permintaannya adalah `application/xml`, `text/xml`, atau jenis data lainnya kecuali `application/x-www-form-urlencoded`, `multipart/form-data`, dan `text/plain`.<br>Misalnya, jika header permintaan khusus adalah `Access-Control- Max-Age: 1728000`, ini menunjukkan bahwa tidak akan ada permintaan preflight lain yang dikirim untuk berbagi sumber daya lintas origin dalam waktu 1.728.000 detik (20 hari).</td>
</tr>
<tr>
<td>Access-Control-Expose-Headers</td>
<td>Menentukan header mana yang dapat diungkapkan ke klien sebagai bagian dari respons.<br>Secara default, 6 header berikut dapat diungkapkan ke klien: `Cache-Control`, `Content-Language`, `Content-Type`, `Expires`, `Last-Modified`, dan `Pragma`.<br>Jika Anda ingin membuat header lain dapat diakses oleh klien, Anda dapat memisahkan beberapa header dengan `,`, misalnya, `Access-Control-Expose-Headers: Content-Length,X-My-Header`. Dengan cara ini, klien dapat mengakses dua header `Content-Length` dan `X-My-Header`.</td>
</tr>
<tr>
<td>Content-Disposition</td>
<td>Mengaktifkan unduhan di peramban dan menetapkan nama file default dari sumber daya yang diunduh.<br>Saat server mengirim file ke peramban klien, jika jenis file didukung oleh peramban, seperti TXT dan JPG, file akan langsung dibuka di peramban secara default. Jika Anda ingin pengguna menyimpan file, Anda dapat mengonfigurasi bidang `Content-Disposition` untuk mengesampingkan perilaku default peramban. Konfigurasi umumnya adalah sebagai berikut:<br>`Content-Disposition:attachment;filename=FileName.txt`</td>
</tr>
<tr>
<td>Content-Language</td>
<td>Menentukan kode bahasa yang digunakan di halaman. Konfigurasi umumnya adalah sebagai berikut:<br>`Content-Language: zh-CN`<br>`Content-Language: en-US`</td>
</tr>
<tr>
<td>Custom</td>
<td>Mendukung pengaturan header khusus dan pasangan nilai kunci.<br>Persyaratan pada parameter header khusus: terdiri dari 1 hingga 100 karakter huruf besar dan kecil, angka, dan tanda hubung (-).<br>Persyaratan pada nilai header khusus : terdiri dari 1 hingga 1000 karakter; Karakter bahasa Mandarin tidak didukung.</td>
</tr>
</tbody></table>

[](id:acao)
### Pengenalan mode pencocokan Access-Control-Allow-Origin

| **Mode Pencocokan**   | **Nilai Origin**                                                     | **Deskripsi**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Pencocokan penuh         | *                                                            | Jika diatur ke `*`, header `Access-Control-Allow-Origin:*` akan ditambahkan ke respons. |
| Pencocokan tetap       | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` | Sumber `https://cloud.tencent.com` mengenai hit dalam daftar sehingga header `Access-Control-Allow-Origin: https://cloud.tencent.com` akan ditambahkan ke respons. Sumber `https://www.qq.com` tidak mengenai hit daftar, jadi responsnya tidak akan berubah. |
| Pencocokan nama domain kartubebas tingkat kedua | `http://*.tencent.com` | Sumber `https://cloud.tencent.com` mengenai hit dalam daftar sehingga header `Access-Control-Allow-Origin: https://cloud.tencent.com` akan ditambahkan ke respons. Sumber `https://cloud.qq.com` tidak mengenai hit daftar, jadi responsnya tidak akan berubah. |
| Pencocokan port | `https://cloud.tencent.com:8080` | Sumber `https://cloud.tencent.com:8080` mengenai hit dalam daftar sehingga header `Access-Control-Allow-Origin:https://cloud.tencent.com:8080` akan ditambahkan ke respons. Sumber `https://cloud.tencent.com` tidak mengenai hit dalam daftar, jadi responsnya tidak akan berubah. |

> ! Jika ada port khusus, Anda harus memasukkan informasi yang relevan dalam daftar. Pencocokan port sembarangan tidak didukung, dan Anda harus menentukan port-nya.

[](id:notice)
### Catatan

Header di bawah ini tidak didukung dan tidak akan diterapkan meskipun dikonfigurasi:

```
Date
Expires
Content-Type
Content-Encoding
Content-Length
Transfer-Encoding
Cache-Control
If-Modified-Since
Last-Modified
Connection
Content-Range
ETag
Accept-Ranges
Age
Authentication-Info
Proxy-Authenticate
Retry-After
Set-Cookie
Vary
WWW-Authenticate
Content-Location
Content-MD5
Content-Range
Meter
Allow
Error
```
