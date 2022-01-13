Setelah membuat instance CLB, Anda harus mengonfigurasikan pendengar untuknya.Pendengar mendengarkan permintaan di instance dan mengarahkan lalu lintas ke server asli sesuai kebijakan penyeimbangan beban.

Anda harus mengonfigurasikan pendengar CLB dengan item-item berikut:
1.Protokol dan port pendengaran.Port pendengaran, atau port frontend, digunakan untuk menerima dan meneruskan permintaan ke server asli.
2.Kebijakan pendengaran, seperti kebijakan penyeimbangan beban dan [persistensi sesi](https://intl.cloud.tencent.com/document/product/214/6154).
3.Kebijakan [pemeriksaan kesehatan](https://intl.cloud.tencent.com/document/product/214/6097).
4.Server asli.Ikat server asli dengan memilih IP dan port-nya.Port layanan, atau port backend, digunakan oleh server asli untuk menerima permintaan.

## Jenis Protokol Yang Didukung
Satu pendengar CLB bisa mendengar permintaan lapisan 4 dan lapisan 7 di instance CLB dan mengarahkannya ke server asli untuk pemrosesan.Perbedaan utama antara CLB lapisan 4 dan CLB lapisan 7 adalah apakah protokol lapisan 4 atau lapisan 7 digunakan untuk meneruskan lalu lintas untuk penyeimbangan beban permintaan pengguna.
- Protokol lapisan 4: membawa protokol layer yang menerima permintaan dan meneruskan lalu lintas ke server asli terutama melalui VIP dan port.
- Protokol lapisan 7: protokol layer aplikasi yang mendistribusikan lalu lintas berdasarkan informasi layer aplikasi seperti URL dan header HTTP.

Jika Anda menggunakan pendengar lapisan 4 (misalnya, penerusan protokol lapisan 4), instance CLB akan menyambungkan koneksi TCP dengan server asli di port pendengaran, dan langsung meneruskan permintaan ke server asli.Proses ini tidak mengubah paket data apa pun (dalam mode pass-through) dan memiliki efisiensi penerusan tinggi.

CLB Tencent Cloud mendukung penerusan permintaan melalui protokol-protokol berikut ini:
- TCP (layer transportasi)
- UDP (layer transportasi)
- TCP SSL (layer transportasi)
- HTTP (layer aplikasi)
- HTTPS (layer aplikasi)

>? Pendengar TCP SSL saat ini mendukung instance CLB jaringan publik, tetapi tidak mendukung jaringan pribadi atau instance CLB klasik.

<table>
<thead>
<tr>
<th width="12%">Jenis Protokol</th>
<th width="12%">Protokol</th>
<th width="40%">Deskripsi</th>
<th width="36%">Kasus Penggunaan</th>
</tr>
<tr>
<td rowspan="3">Protokol lapisan 4</td>
<td>TCP</td>
<td>Protokol dan layer transportasi andal dan berorientasi koneksi:<li>Ujung sumber dan tujuan harus melakukan jabat tangan tiga arah untuk membuat koneksi sebelum transfer data.</li><li>Mendukung persistensi sesi berbasis IP Klien (IP sumber).</li><li>IP klien bisa ditemukan di layer jaringan.</li><li>Server bisa memperoleh IP klien secara langsung.</li></td>
<td>Itu cocok untuk skenario yang sangat membutuhkan keandalan dan akurasi data, tetapi tidak terlalu membutuhkan kecepatan transfer, seperti transfer file, menerima dan mengirim email, dan masuk jarak jauh. <br>Untuk informasi selengkapnya, silakan lihat <a href="https://intl.cloud.tencent.com/document/product/214/32517">Mengonfigurasikan Pendengar TCP</a>.</td>
</tr>
<tr>
<td>UDP</td>
<td>Protokol layer transportasi tanpa koneksi:<li>Ujung sumber dan tujuan tidak membuat koneksi atau mempertahankan status koneksi. </li><li>Setiap koneksi UDP adalah point-to-point. </li><li>Mendukung komunikasi satu-ke-satu, satu-ke-semuanya, semuanya-ke-satu, dan semuanya-ke-semuanya.</li><li>Mendukung persistensi sesi berbasis IP Klien (IP sumber).</li><li>Server bisa memperoleh IP klien secara langsung.</li></td>
<td>Itu cocok untuk skenario yang sangat membutuhkan efisiensi transfer, tetapi tidak terlalu membutuhkan akurasi, seperti pesan singkat dan video online. <br>Untuk informasi selengkapnya, silakan lihat <a href="https://intl.cloud.tencent.com/document/product/214/32518">Mengonfigurasikan Pendengar UDP</a>.</td>
</tr>
<tr>
<td>TCP SSL</td>
<td>TCP Aman: <li>Pendengar TCP SSL mendukung sertifikat konfigurasi untuk mencegah permintaan akses tidak resmi.</li><li>Manajemen sertifikat terpadu disediakan bagi CLB untuk mengimplementasi dekripsi.</li><li>Mendukung autentikasi bersama dan satu arah.</li><li>Server bisa memperoleh IP klien secara langsung.</li></td>
<td>Ini cocok untuk skenario yang sangat membutuhkan keamanan saat TCP digunakan dan mendukung protokol khusus berbasis TCP. <br>Untuk informasi selengkapnya, silakan lihat <a href="https://intl.cloud.tencent.com/document/product/214/32519">Mengonfigurasikan Pendengar TCP SSL</a>.</td>
</tr>
<tr>
<td rowspan="2">Protokol lapisan 7</td>
<td>HTTP</td>
<td>Protokol layer aplikasi: <li>Mendukung penerusan berdasarkan nama domain dan URL yang diminta. </li><li>Mendukung persistensi sesi berbasis cookie.</li></td>
<td>Ini cocok untuk aplikasi tempat konten permintaan perlu diidentifikasi, seperti aplikasi web, aplikasi seluler, dan sebagainya. <br>Untuk informasi selengkapnya, silakan lihat <a href="https://intl.cloud.tencent.com/document/product/214/32515">Mengonfigurasikan Pendengar HTTP</a>.</td>
</tr>
<tr>
<td>HTTPS</td>
<td>Protokol layer aplikasi terenkripsi:<li>Mendukung penerusan berdasarkan nama domain dan URL yang diminta.</li><li>Mendukung persistensi sesi berbasis cookie.</li><li>Manajemen sertifikat terpadu disediakan bagi CLB untuk mengimplementasi dekripsi.</li><li>Mendukung autentikasi bersama dan satu arah.</li></td>
<td>Ini cocok untuk aplikasi HTTP yang membutuhkan transmisi terenkripsi.<br>Untuk informasi selengkapnya, silakan lihat <a href="https://intl.cloud.tencent.com/document/product/214/32516">Mengonfigurasikan Pendengar HTTPS</a>.</td>
</tr>
</tbody></table>

## Konfigurasi Port
<table>
<thead>
<tr>
<th width="16%">Jenis Port</th>
<th>Catatan</th>
<th width="50%">Pembatasan</th>
</tr>
</thead>
<tbody><tr>
<td>Port pendengaran (port frontend)</td>
<td>Port pendengaran digunakan oleh instance CLB untuk menerima dan meneruskan permintaan ke server asli<br/>Anda bisa mengonfigurasikan instance CLB untuk port 1 sampai 65535, seperti port 21 (FTP), 25 (SMTP), 80 (HTTP), dan 443 (HTTPS), dll.</td>
<td><ul>Pada satu instance CLB:<li>Port pendengaran UDP bisa digunakan untuk TCP; misalnya, pendengar `TCP:80` bisa berdampingan dengan pendengar `UDP:80`.</li><li>Port pendengaran harus unik untuk jenis protokol yang sama.TCP, TCP SSL, HTTP, dan HTTPS adalah dari TCP, jadi misalnya, pendengar `TCP:80` tidak bisa berdampingan dengan pendengar `HTTP:80`.</li></ul></td>
</tr>
<tr>
<td>Port layanan (port backend)</td>
<td>Port layanan digunakan oleh instance CVM untuk memberikan layanan, menerima dan memproses lalu lintas dari instance CLB.<br/>Pada satu instance CLB, satu port pendengaran bisa meneruskan lalu lintas ke port-port beberapa instance CVM.</td>
<td><ul>Pada satu instance CLB:<li>Port layanan dari protokol pendengaran berbeda tidak harus unik; misalnya, pendengar `HTTP:80` dan `HTTPS:443` bisa ditemukan di port instance CVM yang sama.</li><li>Saat menggunakan protokol pendengaran yang sama, setiap port layanan backend hanya bisa diikat ke satu pendengar, artinya, lipat empat (VIP, protokol pendengaran, IP pribadi server asli, dan port layanan backend) harus unik.</li></ul></td>
</tr>
</tbody></table>
