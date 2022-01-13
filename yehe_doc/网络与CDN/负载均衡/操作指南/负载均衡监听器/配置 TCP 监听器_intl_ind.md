## Ikhtisar Pendengar TCP
Anda bisa membuat pendengar TCP ke instance CLB untuk meneruskan permintaan TCP dari klien.TCP cocok untuk skenario yang sangat membutuhkan keandalan dan akurasi data, tetapi tidak terlalu membutuhkan kecepatan transfer, seperti transfer file, pesan email, dan masuk jarak jauh.Untuk pendengar TCP, server asli bisa memperoleh IP klien asli secara langsung.

## Prasyarat
Anda harus [membuat instance CLB](http://intl.cloud.tencent.com/document/product/214/6149) dahulu.

## Mengonfigurasi Pendengar TCP
### Langkah 1.Buka halaman "Manajemen Pendengar"
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb).
2.Pilih **Instance Management** (Manajemen Instance) di bilah sisi kiri.
3.Di daftar instance, klik ID instance yang akan dikonfigurasi untuk masuk ke halaman detail instance.
4.Klik tab **Listener Management** (Manajemen Pendengar) atau klik **Configure Listener** (Konfigurasi Pendengar) di kolom "Operation" (Operasi).
![](https://main.qcloudimg.com/raw/c222786c42bace0f1366def6a5a3d1b2.png)
5.Halaman "Listener Management" (Manajemen Pendengar) adalah seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/31f6e12c1520d3cb4759b8e063bcdb40.png)

### Langkah 2.Konfigurasikan pendengar
Klik **Create** (Buat) di **TCP/UDP/TCP SSL Listener** (Pendengar TCP/UDP/TCP SSL) dan konfigurasikan pendengar TCP di jendela pop-up.
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
<td><span>test-tcp-80&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Protokol pendengar dan port pendengaran</td>
<td>Protokol pendengar dan port pendengaran. <br><li>Protokol pendengar:CLB mendukung berbagai protokol, termasuk TCP, UDP, HTTP, dan HTTPS.TCP digunakan dalam contoh ini.</li><li>Port pendengaran:Port digunakan untuk menerima permintaan dan meneruskannya ke server asli.Rentang port: 1-65535.</li><li>Port pendengar harus unik di instance CLB yang sama.</li></td>
<td>TCP:80</td>
</tr>
<tr>
<td>Metode penyeimbangan</td>
<td>Untuk pendengar TCP, CLB mendukung dua algoritme penjadwalan: round robin tertimbang (WRR) dan koneksi terkecil tertimbang (WLC). <br><li>WRR:Permintaan dikirimkan secara berurutan ke server-server asli berbeda sesuai bobotnya.Penjadwalan dilakukan berdasarkan <strong>jumlah koneksi baru</strong>, tempat server dengan bobot lebih tinggi akan melalui lebih banyak polling (dengan kata lain, kemungkinan yang lebih tinggi), sementara server dengan bobot yang sama memproses jumlah koneksi yang sama.</li><li>WLC:Beban server dinilai sesuai dengan jumlah koneksi aktif ke server-server.Penjadwalan dilakukan berdasarkan beban dan bobot server.Jika bobotnya sama, server dengan koneksi aktif yang lebih sedikit akan menjalani lebih banyak polling (dengan kata lain, kemungkinan yang lebih tinggi).</li></td>
<td>WRR</td>
</tr>
</tbody></table>

Konfigurasi tertentu pendengar TCP yang dibuat adalah seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/089a45fae94bda88e28ee30dc29159e5.png)

#### 2.Pemeriksaan kesehatan
| Item Konfigurasi | Deskripsi | Contoh |
| ------- | ------------------------ | ---------------------------------------- |
| Status pemeriksaan kesehatan | Pemeriksaan kesehatan bisa diaktifkan atau dinonaktifkan.Di pendengar TCP, instance CLB mengirimkan paket SYN ke port server tertentu untuk melakukan pemeriksaan kesehatan.| Diaktifkan |
| Periode waktu habis respons | <li> Periode waktu habis respons maksimum untuk pemeriksaan kesehatan.</li><li>Jika satu server asli gagal merespons dengan tepat dalam periode waktu habis, pemeriksaan kesehatan dianggap abnormal.</li><li>Rentang nilai: 2-60s.Nilai default: 2s.</li> | 2s |
| Interval pemeriksaan | <li>Interval antara dua pemeriksaan kesehatan.</li><li>Rentang nilai: 5-300s.Nilai default: 5s.</li> | 5s |
| Ambang batas tidak sehat | <li>Jika hasil pemeriksaan kesehatan menerima n kali (n adalah jumlah yang dimasukkan) gagal berturut-turut, instance akan dianggap tidak sehat, dan status yang ditampilkan di konsol akan menjadi **Abnormal**.</li><li>Rentang nilai:2-10.Nilai default: 3.</li> | 3 kali |
| Ambang batas sehat | <li>Jika hasil pemeriksaan kesehatan menerima n kali (n adalah jumlah yang dimasukkan) berhasil berturut-turut, instance akan dianggap sehat, dan status yang ditampilkan di konsol akan menjadi **Healthy** (Sehat).</li><li>Rentang nilai:2-10.Nilai default: 3.</li> | 3 kali |

Konfigurasi khusus pemeriksaan kesehatannya seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/9c19b0d3db249d2bb37f5dc7c8238384.png)

#### 3.Persistensi sesi
| Item Konfigurasi | Deskripsi | Contoh |
| ------- | ------------------------ | ---------------------------------------- |
| Status persistensi sesi | Persistensi sesi bisa diaktifkan atau dinonaktifkan. <br><li>Jika persistensi sesi diaktifkan, pendengar CLB akan mengirimkan permintaan akses dari klien yang sama ke server asli yang sama.</li><li>Persistensi sesi TCP diimplementasikan berdasarkan alamat IP klien, misalnya, permintaan akses dari alamat IP yang sama diteruskan ke server asli yang sama.</li><li>Persistensi sesi bisa diaktifkan untuk penjadwalan WRR, tetapi tidak untuk penjadwalan WLC.</li> | Diaktifkan |
| Waktu persistensi sesi | Waktu persistensi sesi. <br><li>Jika tidak ada permintaan baru di koneksi dalam waktu persistensi sesi, persistensi sesi akan diputus secara otomatis.</li><li>Rentang nilai: 30-3,600s.</li> | 30s |

Konfigurasi khusus persistensi sesi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/449fc0611325c37aafe9815921b2471d.png)

### Langkah 3.Mengikat server asli
1.Di halaman "Manajemen Pendengar", klik pendengar `TCP:80` yang dibuat untuk melihat server asli yang diikat di sebelah kanan pendengar.
![](https://main.qcloudimg.com/raw/7082206ee1b28031d6a11f9b887684dd.png)
2.Klik **Bind** (Ikat), pilih server asli yang akan diikat dan konfigurasikan port server dan bobot di jendela pop-up.
1.Tambahkan Port:Di kotak "Terpilih" di sebelah kanan, klik **Add Port** (Tambahkan Port) untuk menambahkan beberapa port untuk instance CVM yang sama, seperti port 80, 81, dan 82.
2.Port Default:Masukkan “Port Default” dahulu, kemudian pilih instance CVM.Port dari setiap instance CVM adalah port default.
![](https://main.qcloudimg.com/raw/4c749af9416903a471a72c67e00125e1.png)

Setelah tiga langkah ini selesai, aturan pendengar TCP sudah dikonfigurasi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/9dc06223e43fe6216f8a1cc74821dc48.png)

### Langkah 4.Grup keamanan (opsional)
Anda dapat mengonfigurasi grup keamanan CLB untuk mengisolasi lalu lintas jaringan publik.Untuk informasi selengkapnya, lihat [Mengonfigurasi Grup Keamanan CLB](https://intl.cloud.tencent.com/document/product/214/14733).

### Langkah 5.Modifikasi/hapus satu pendengar (opsional)
Jika Anda perlu memodifikasi atau menghapus pendengar yang dibuat, klik pendengar di halaman "Manajemen Pendengar" dan pilih **Modify** (Modifikasi) atau **Delete** (Hapus).
![](https://main.qcloudimg.com/raw/d4d79dd4618bbe5cea3f36d719ddf5ec.png)
