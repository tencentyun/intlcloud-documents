
## Ikhtisar
CLB Klasik mudah dikonfigurasi dan mendukung skenario penyeimbangan beban sederhana:
- CLB klasik **Public network** (Jaringan publik): mendukung protokol TCP/UDP/HTTP/HTTPS.
- CLB klasik **Private network** (Jaringan pribadi): mendukung protokol TCP/UDP.

Instance CLB bisa diklasifikasikan menjadi dua tipe:CLB (sebelumnya "CLB aplikasi") dan CLB klasik.

CLB mencakup semua fitur CLB klasik.Berdasarkan fitur dan performa mereka, Anda sebaiknya menggunakan CLB.Untuk perbandingan mendetail, lihat [Tipe Instance](https://intl.cloud.tencent.com/document/product/214/8847).
>!Saat ini, ada dua jenis akun Tencent Cloud: tagihan per EIP/CLB dan tagihan per CVM.Semua akun Tencent Cloud yang terdaftar setelah 17 Juni 2020 00.00.00 adalah akun tagihan per EIP/CLB.Untuk akun Tencent Cloud yang terdaftar sebelum 17 Juni 2020, [periksa tipe akun Anda](https://intl.cloud.tencent.com/document/product/684/15246) di konsol.Akun tagihan per EIP/CLB tidak lagi mendukung CLB klasik.Anda kini hanya bisa membeli instance CLB.
>
Dokumen ini memperkenalkan instance CLB klasik.Setelah membuat instance, Anda perlu mengonfigurasikan pendengar untuknya.Pendengar mendengar permintaan di instance CLB dan mendistribusikan lalu lintas ke server asli sesuai kebijakan penyeimbangan beban.

## Konfigurasi Pendengar
Anda harus mengonfigurasi pendengar CLB seperti di bawah ini:
1.Protokol pendengar dan port pendengaran.Port pendengaran, atau port frontend, digunakan untuk menerima dan meneruskan permintaan ke server asli.
2.Port backend.Ini adalah port tempat instance CVM menyediakan layanan, menerima dan memproses lalu lintas dari instance CLB.
3.Kebijakan pendengaran, seperti kebijakan penyeimbangan beban dan persistensi sesi.
4.Kebijakan pemeriksaan kesehatan.
5.Server asli bisa diikat dengan memilih IP-nya.

> ?Jika Anda mengonfigurasi beberapa pendengar ke instance CLB klasik dan mengikat beberapa server asli, setiap pendengar akan meneruskan permintaan ke semua server asli sesuai konfigurasinya.

### Jenis protokol yang didukung
Satu pendengar CLB bisa mendengar permintaan Lapisan 4 dan Lapisan 7 di instance CLB dan mendistribusikannya ke server asli untuk pemrosesan.Perbedaan utama antara CLB Lapisan 4 dan CLB Lapisan 7 adalah protokol mana yang digunakan untuk meneruskan lalu lintas saat menyeimbangkan beban permintaan pengguna.
- Protokol Lapisan 4: protokol layer transportasi, termasuk TCP dan UDP.
- Protokol Lapisan 7: protokol layer aplikasi, termasuk HTTP dan HTTPS.

>? 
>1.Instance CLB klasik menerima permintaan dan meneruskan lalu lintas ke server asli melalui VIP dan port.Protokol Lapisan 7 tidak mendukung penerusan berdasarkan nama domain dan URL.
>2.Instance CLB klasik jaringan pribadi hanya mendukung protokol Lapisan 4, bukan protokol Lapisan 7.
>3.Jika Anda membutuhkan fitur-fitur lanjutan yang disebutkan di atas, kami menyarankan untuk memilih CLB daripada CLB klasik.Untuk informasi selengkapnya, lihat [Jenis Instance](https://intl.cloud.tencent.com/document/product/214/8847).

### Konfigurasi Port
<table>
<thead>
<tr>
<th width="30%">Port Pendengaran (port frontend)</th>
<th width="30%">Port Layanan (port backend)</th>
<th width="40%">Deskripsi</th>
</tr>
</thead>
<tbody><tr>
<td>Port pendengaran digunakan oleh instance CLB untuk menerima dan meneruskan permintaan ke server asli untuk penyeimbangan beban.<br><br>Anda bisa mengonfigurasikan CLB untuk rentang port 1-65535, seperti 21 (FTP), 25 (SMTP), 80 (HTTP), dan 443 (HTTPS).</td>
<td>Port layanan digunakan oleh CVM untuk memberikan layanan, menerima dan memproses lalu lintas dari instance CLB.<br><br>Pada satu instance CLB, satu port pendengaran bisa meneruskan lalu lintas ke port-port beberapa instance CVM.</td>
<td>Pada instance CLB,<li>port pendengaran harus unik.<br>Contohnya, pendengar TCP:80 dan HTTP:80 tidak bisa dibuat di waktu yang sama.</li><li>Hanya port TCP dan UDP yang boleh sama.<br>Contohnya, Anda bisa membuat baik pendengar TCP:80 dan UDP:80.</li><br>Port layanan yang sama bisa digunakan pada instance CLB.<br>Contohnya, pendengar HTTP:80 dan HTTPS:443 bisa diikat ke port instance CVM yang sama.</td>
</tr>
</tbody></table>

