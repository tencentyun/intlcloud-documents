Fitur verifikasi port instans dapat membantu Anda mendeteksi aksesibilitas port grup keamanan yang terkait dengan instans CVM, menemukan kesalahan, dan meningkatkan pengalaman pengguna.
Fitur ini mendukung deteksi aksesibilitas port umum dan port kustom. Lihat di bawah ini untuk port umum.
 <table>
<thead>
<tr>
<th>Aturan</th>
<th>Port</th>
<th>Deskripsi</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="7">Aturan masuk</td>
<td>Protokol ICMP</td>
<td>Digunakan untuk meneruskan pesan kontrol seperti perintah ping. ICMP adalah protokol kontrol, dan tidak ada port yang terlibat.</td>
</tr>
<tr>
<td>TCP:20</td>
<td rowspan="2">Digunakan untuk mengizinkan unggah dan unduh melalui FTP.</td>
</tr>
<tr>
<td>TCP:21</td>
</tr>
<tr>
<td>TCP:22</td>
<td>Digunakan untuk mengizinkan login SSH Linux.</td>
</tr>
<tr>
<td>TCP:3389</td>
<td>Digunakan untuk mengizinkan login jarak jauh Windows.</td>
</tr>
<tr>
<td>TCP:443</td>
<td>Digunakan untuk menyediakan layanan HTTPS situs web.</td>
</tr>
<tr>
<td>TCP:80</td>
<td>Digunakan untuk menyediakan layanan HTTP situs web.</td>
</tr>
<tr>
<td>Aturan keluar</td>
<td>SEMUA</td>
<td>Digunakan untuk mengizinkan semua lalu lintas keluar untuk akses ke jaringan eksternal.</td>
</tr>
</tbody></table>

## Panduan Operasi
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Diagnostic Tools** (Alat Diagnostik) > **Port Verification** (Verifikasi Port) di bilah sisi kiri untuk mengakses halaman pengelolaan.
3. Pilih wilayah di bagian atas halaman, temukan instans yang ingin Anda verifikasi dalam daftar, dan klik **Quick Check** (Periksa Cepat).
![](https://main.qcloudimg.com/raw/7001bc40cd91f8c17070826ba62ce0ab.png)
4. Anda dapat melihat detail deteksi port di jendela pop-up. Lakukan operasi berikut sesuai kebutuhan.
   + Hapus centang port yang tidak ingin Anda deteksi.
   + Masukkan port kustom untuk mendeteksi dan klik **Save** (Simpan).
      + Protokol: pilih TCP atau UDP.
      + Port: masukkan satu nomor port untuk dideteksi, yang tidak boleh sama dengan port umum. 
      + Arah: pilih **Inbound** (Masuk) atau **Outbound** (Keluar).
      + IP: masukkan IP sumber untuk arah masuk dan IP tujuan untuk arah keluar. Masukkan **ALL** (SEMUA) untuk semua alamat IP sumber dan tujuan.
      + Hingga 15 port kustom dapat dideteksi.
   
 Jika Anda perlu mendeteksi lalu lintas keluar menuju IP 10.0.1.12 menggunakan protokol TCP melalui port 30, masukkan informasi berikut di area **Custom port detection** (Deteksi port kustom).
![](https://main.qcloudimg.com/raw/3f4067337a80ef596af55446cf5fead1.png)

5. Setelah konfigurasi selesai, klik **Detect** (Deteksi). Hasilnya akan ditampilkan di kolom **Policy** (Kebijakan).
![](https://main.qcloudimg.com/raw/ae7eb364c16c5bbcb52ce47615b15174.png)
<p>Asumsikan bahwa Anda perlu membuka port <b>Tidak dibuka</b>, misalnya <b>TCP:22</b>, </p>

 ![](https://main.qcloudimg.com/raw/40fc364c561308d97cc1aeca54cbb1b4.png)

 <p>Kemudian Anda dapat menambahkan aturan masuk untuk grup keamanan yang terkait dengan instans di <a href="https://console.cloud.tencent.com/vpc/securitygroup">konsol Grup Keamanan</a> untuk membuka port TCP:22. Anda dapat memilih <b>semua</b> untuk <b>Sumber</b> untuk mengizinkan semua IP, atau memasukkan IP tertentu (rentang IP).</p>

   ![](https://main.qcloudimg.com/raw/d1053c70ddce3f089737f4abf8e0c297.png)

## Informasi yang Relevan
- Untuk informasi tentang grup keamanan, lihat [Ikhtisar Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/38750) dan [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35513).
- Untuk informasi selengkapnya tentang port umum, lihat [Port Server Umum](https://intl.cloud.tencent.com/document/product/215/35520).
