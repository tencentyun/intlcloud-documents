## Ikhtisar Pendengar TCP SSL
Anda bisa menambahkan pendengar TCP SSL ke instance CLB untuk meneruskan permintaan TCP terenkripsi dari klien.Protokol TCP SSL cocok untuk skenario yang menuntut performa offloading TLS sangat tinggi dan skala besar.Dengan pendengar TCP SSL, server backend bisa memperoleh IP nyata klien secara langsung.

>?Pendengar TCP SSL saat ini hanya mendukung CLB, tetapi tidak mendukung CLB klasik.
>

## Prasyarat
Anda harus [membuat instance CLB](http://intl.cloud.tencent.com/document/product/214/6149) dahulu.

## Mengonfigurasi Pendengar TCP SSL
### Langkah 1.Buka halaman "Manajemen Pendengar"
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb).
2.Pilih **Instance Management** (Manajemen Instance) di bilah sisi kiri.
3.Di daftar instance, klik ID instance yang akan dikonfigurasi untuk masuk ke halaman detail instance.
4.Klik tab **Listener Management** (Manajemen Pendengar) atau klik **Configure Listener** (Konfigurasi Pendengar) di kolom "Operation" (Operasi).
![](https://main.qcloudimg.com/raw/ec8e5fd6668f0d58a88d6da66a4424e9.png)
5.Halaman "Listener Management" (Manajemen Pendengar) adalah seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/5d5f9cdb61a7ea3e4fd88036a7c01d0d.png)

### Langkah 2.Konfigurasikan pendengar
Klik **Create** (Buat) di **TCP/UDP/TCP SSL Listener** (Pendengar TCP/UDP/TCP SSL) dan konfigurasikan pendengar TCP SSL di jendela pop-up.
#### 1.Konfigurasi dasar
<table>
<thead>
<tr>
<th width="15%">Item Konfigurasi</th>
<th width="70%">Deskripsi</th>
<th width="15%">Contoh</th>
</tr>
</thead>
<tbody><tr>
<td>Nama</td>
<td>Nama pendengar</td>
<td><span>test-tcpssl-9000&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Protokol pendengar dan port pendengaran</td>
<td>Protokol pendengar dan port pendengaran. <br><li>Protokol pendengar:CLB mendukung berbagai protokol, termasuk TCP, UDP, TCP SSL, HTTP, dan HTTPS.TCP SSL digunakan dalam contoh ini.</li><li>Port pendengaran:Port digunakan untuk menerima permintaan dan meneruskannya ke server asli.Rentang port: 1-65535.</li><li>Port pendengar harus unik di instance CLB yang sama.</li></td>
<td>TCP SSL:9000</td>
</tr>
<tr>
<td>Mertode parsing SSL</td>
<td>Mendukung autentikasi satu arah dan autentikasi bersama</td>
<td>Autentikasi satu arah</td>
</tr>
<tr>
<td>Sertifikat server</td>
<td>Anda bisa memilih sertifikat yang ada di <a href="https://console.cloud.tencent.com/ssl">layanan sertifikat SSL</a> atau mengunggah sertifikat</td>
<td>Pilih sertifikat yang ada cc/UzxFoXsE</td>
</tr>
<tr>
<td>Metode penyeimbangan</td>
<td>Untuk pendengar TCP SSL, CLB mendukung dua algoritme penjadwalan: round robin tertimbang (WRR) dan koneksi terkecil tertimbang (WLC). <br><li>WRR:Permintaan dikirimkan secara berurutan ke server-server asli berbeda sesuai bobotnya.Penjadwalan dilakukan berdasarkan <strong>jumlah koneksi baru</strong>, tempat server dengan bobot lebih tinggi akan melalui lebih banyak polling (dengan kata lain, kemungkinan yang lebih tinggi), sementara server dengan bobot yang sama memproses jumlah koneksi yang sama.</li><li>WLC:Beban server dinilai sesuai dengan jumlah koneksi aktif ke server-server.Penjadwalan dilakukan berdasarkan beban dan bobot server.Jika bobotnya sama, server dengan koneksi aktif yang lebih sedikit akan menjalani lebih banyak polling (dengan kata lain, kemungkinan yang lebih tinggi).</li></td>
<td>WRR</td>
</tr>
</tbody></table>

Konfigurasi tertentu pendengar TCP SSL yang dibuat adalah seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/7107604b6c756183c4ea329c20bcbf00.png)

#### 2.Pemeriksaan kesehatan
| Item Konfigurasi | Deskripsi | Contoh |
| ------- | ------------------------ | ---------------------------------------- |
| Status pemeriksaan kesehatan | Pemeriksaan kesehatan bisa diaktifkan atau dinonaktifkan.Di pendengar TCP SSL, instance CLB mengirimkan paket SYN ke port server tertentu untuk melakukan pemeriksaan kesehatan.| Diaktifkan |
| Periode waktu habis respons | <li> Periode waktu habis respons maksimum untuk pemeriksaan kesehatan.</li><li>Jika satu server asli gagal merespons dengan tepat dalam periode waktu habis, pemeriksaan kesehatan dianggap abnormal.</li><li>Rentang nilai: 2-60s.Nilai default: 2s.</li> | 2s |
| Interval pemeriksaan | <li>Interval antara dua pemeriksaan kesehatan.</li><li>Rentang nilai: 5-300s.Nilai default: 5s.</li> | 5s |
| Ambang batas tidak sehat | <li>Jika hasil pemeriksaan kesehatan menerima n kali (n adalah jumlah yang dimasukkan) gagal berturut-turut, instance akan dianggap tidak sehat, dan status yang ditampilkan di konsol akan menjadi **Abnormal**.</li><li>Rentang nilai:2-10.Nilai default: 3.</li> | 3 kali |
| Ambang batas sehat | <li>Jika hasil pemeriksaan kesehatan menerima n kali (n adalah jumlah yang dimasukkan) berhasil berturut-turut, instance akan dianggap sehat, dan status yang ditampilkan di konsol akan menjadi **Healthy** (Sehat).</li><li>Rentang nilai:2-10.Nilai default: 3.</li> | 3 kali |

Konfigurasi khusus pemeriksaan kesehatannya seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/6d57f6df374edba777d3a8841f50adc2.png)

#### 3.Persistensi sesi (saat ini tidak didukung)
![](https://main.qcloudimg.com/raw/8cde7bd598be6bdb8d5c300e32c90659.png)

### Langkah 3.Mengikat server asli
1.Di halaman "Manajemen Pendengar", klik pendengar `TCP SSL:9000` yang dibuat untuk melihat server asli yang diikat di sebelah kanan pendengar.
![](https://main.qcloudimg.com/raw/6dc93b60bb493c58a067604d69dd309b.png)
2.Klik **Bind** (Ikat), pilih server asli yang akan diikat dan konfigurasikan port server dan bobot di jendela pop-up.
1.Tambahkan Port:Di kotak "Terpilih" di sebelah kanan, klik **Add Port** (Tambahkan Port) untuk menambahkan beberapa port untuk instance CVM yang sama, seperti port 80, 81, dan 82.
2.Port Default:Masukkan “Port Default” dahulu, kemudian pilih instance CVM.Port dari setiap instance CVM adalah port default.
![](https://main.qcloudimg.com/raw/0285f5f04916c94c9549baae5bdffda6.png)

Setelah tiga langkah ini selesai, aturan pendengar TCP SSL sudah dikonfigurasi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/bfa1e03aec1f29b24d9bf9929edef49d.png)

### Langkah 4.Grup keamanan (opsional)
Anda dapat mengonfigurasi grup keamanan CLB untuk mengisolasi lalu lintas jaringan publik.Untuk informasi selengkapnya, lihat [Mengonfigurasi Grup Keamanan CLB](https://intl.cloud.tencent.com/document/product/214/14733).

### Langkah 5.Modifikasi/hapus satu pendengar (opsional)
Jika Anda perlu memodifikasi atau menghapus pendengar yang dibuat, klik pendengar di halaman "Manajemen Pendengar" dan pilih **Modify** (Modifikasi) atau **Delete** (Hapus).
![](https://main.qcloudimg.com/raw/8a3ddb3d362434e283ec563dcc9e14f5.png)
